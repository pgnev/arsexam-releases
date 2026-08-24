# ArsExam — Official Releases & Updates

This repository is the **official public distribution and update channel** for ArsExam Desktop.

**ArsExam** is a Windows desktop application for managing digital resources related to the Bulgarian State Matriculation Examination in Theory of the Profession — **“Musical Art”**.

**Author and developer:** Petko Ganev  
**Support:** petkoganev@gmail.com  
**Copyright © 2026 Petko Ganev. All rights reserved.**

> This repository contains distribution material only. It is **not** the ArsExam source-code repository and does not grant an open-source license to the ArsExam application.

## Repository purpose

The repository is intentionally limited to public release infrastructure:

- official Windows Setup and update packages;
- Stable/Test update manifests;
- release notes and checksums;
- public legal/privacy/support notices;
- compatibility metadata required by supported ArsExam clients.

Source code, private development artifacts, credentials, signing material, support correspondence, diagnostic events and user data must never be published here.

## Licensing

ArsExam is **proprietary software**. Use of distributed ArsExam binaries is governed by the ArsExam End User License Agreement (EULA).

Hosting this repository on GitHub does **not** place ArsExam under MIT, GPL, Apache or another open-source license. Third-party libraries and components retain their respective licenses and copyright notices.

See `LICENSE.md`, `COPYRIGHT.md` and the legal documents distributed with each official release.

## Offline-first model

ArsExam is designed so that normal work with examination banks, media, generated documents, imports, exports and backups remains local to the user's device.

Internet access is limited to explicitly defined functions such as:

- checking/downloading official updates;
- opt-in crash/error diagnostics;
- secure support-assisted password recovery where enabled.

ArsExam does not use this repository to upload examination content or user databases.

## Update channels

Current clients use these public manifests:

```text
https://raw.githubusercontent.com/pgnev/arsexam-releases/main/update/stable-manifest.json
https://raw.githubusercontent.com/pgnev/arsexam-releases/main/update/test-manifest.json
```

A manifest reference is not, by itself, sufficient trust for an update: the ArsExam updater also validates version metadata, expected package integrity and release context before installation.

## Release integrity

Official public releases are produced from the private canonical source repository through a controlled Windows validation pipeline. Publication is blocked unless the required technical, privacy, legal and operational release gates are satisfied.

The public publisher verifies the source workflow/run context, source commit SHA and version/tag consistency before immutable release assets are published.

## Security and support

For product support, use `petkoganev@gmail.com` or the in-application **Help → Contact support** flow.

Do **not** send passwords, Recovery Kits, complete databases, examination-bank archives or other sensitive working material by e-mail unless specifically requested through a documented secure support procedure.

Security issues should be reported privately; do not disclose exploitable details in a public GitHub issue. See `SECURITY.md`.

## Repository roles

- `pgnev/arsexam-releases` — current official public distribution/update repository.
- `pgnev/arsexam-desktop` — legacy compatibility repository for older clients; not the current distribution authority.
- canonical ArsExam source/development repository — private.

## Current publication policy

No release asset, update manifest promotion or version tag should be treated as official merely because it exists in a development context. Only assets published through the controlled release process in this repository are part of the supported public distribution channel.
