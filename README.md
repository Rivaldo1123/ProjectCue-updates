# Project Cue Updates

Public release and update feed for **Project Cue**, a Windows desktop application by **Valdo Enterprises**.

> This repository is intentionally **binary-only**. The Project Cue source code is maintained in a separate private repository and is not published here.

## Purpose

This repository is used to distribute approved Project Cue builds and the metadata required by the application's Velopack updater.

Published releases may contain:

- `ProjectCue-win-Setup.exe` — Windows installer
- Full Velopack update package (`.nupkg`)
- Velopack release-feed metadata
- Release notes and version information

This repository must not contain:

- Application source code
- Private development documentation
- Signing credentials, API tokens, or secrets
- Workspace databases, tester data, or diagnostic logs
- Unreviewed development builds

## Current status

The update repository is provisioned and the Project Cue application is configured to use it as the public update endpoint. No installer or update package should be considered available until it appears under [Releases](../../releases).

## Installing Project Cue

When an approved build is published:

1. Open the repository's **Releases** page.
2. Select the required version.
3. Download `ProjectCue-win-Setup.exe`.
4. Run the installer and follow the Windows prompts.

The current beta installer is not code-signed, so Windows SmartScreen may display a warning. Testers should install only builds distributed through the approved Project Cue testing process.

## Update behaviour

Installed copies of Project Cue use this repository as their update feed. Updates are designed to remain offline-safe:

- The application remains usable without internet access.
- Update checks do not block normal work.
- Installation requires user confirmation.
- Updates should not interrupt active teacher work.
- Database migrations require a safety restore point first.
- A failed update must leave the existing installation usable.

## Publishing

Release artifacts are built from the private source repository using:

```powershell
pwsh ./scripts/package-installer.ps1 -Version <version>
```

They are then published to this repository with Velopack:

```powershell
vpk upload github `
  --repoUrl https://github.com/Rivaldo1123/ProjectCue-updates `
  --publish `
  --releaseName "Project Cue <version>" `
  --tag v<version> `
  --token <github-token>
```

Publishing credentials belong only in a secure local environment or protected CI secret. They must never be committed to either repository or bundled with the application.

## Source-code privacy

GitHub automatically adds source archives to tagged releases. In this repository, those archives contain only the small public update-feed repository—not the private Project Cue application source.

## Ownership

Project Cue is developed and maintained by **Valdo Enterprises**.
