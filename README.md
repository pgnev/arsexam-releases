# ArsExam — Official Releases & Updates

This repository is the **official public distribution and update channel** for ArsExam Desktop.

**ArsExam** is a Windows desktop application for managing digital resources related to the Bulgarian State Matriculation Examination in Theory of the Profession — **“Musical Art”**.

**Author and developer:** Petko Ganev  
**Support:** petkoganev@gmail.com  
**Copyright © 2026 Petko Ganev. All rights reserved.**

> This repository contains distribution material only. It is **not** the ArsExam source-code repository and does not grant an open-source license to the ArsExam application.

## Current official publication status

| Channel | Published version | Status |
|---|---:|---|
| **Stable** | **3.0.2** | current supported Stable release |
| **Test** | **3.1.0-rc.9** | current published Test release |

A newer development/release-candidate build is **not official merely because it exists in private development**. In particular, ArsExam 3.1.0-rc.10 remains unpublished until all required technical, privacy, support, legal and operational release gates have been completed.

The authoritative current versions are always the values in:

- `update/stable-manifest.json`
- `update/test-manifest.json`

## Repository purpose

This repository is intentionally limited to public release infrastructure:

- official Windows Setup and update packages;
- Stable/Test update manifests;
- release notes and checksums;
- public legal/privacy/support notices;
- compatibility metadata required by supported ArsExam clients.

Source code, private development artifacts, credentials, signing material, support correspondence, diagnostic events and user data must never be published here.

## Licensing

ArsExam is **proprietary software**. Use of distributed ArsExam binaries is governed by the ArsExam End User License Agreement (EULA).

Hosting this repository on GitHub does **not** place ArsExam under MIT, GPL, Apache or another open-source license. Third-party libraries and components retain their respective licenses and copyright notices.

Public legal documents:

- `LICENSE.md`
- `COPYRIGHT.md`
- `EULA_BG.txt`
- `PRIVACY_POLICY_BG.md`
- `THIRD_PARTY_NOTICES.md`
- `SECURITY.md`
- `SUPPORT.md`

The legal documents included with a particular released build remain authoritative for that build.

## Offline-first model

ArsExam is designed so that normal work with examination banks, media, generated documents, imports, exports and backups remains local to the user's device.

Internet access is limited to explicitly defined and documented functions, depending on the released version, such as:

- checking/downloading official updates;
- opt-in crash/error diagnostics where enabled and consented;
- secure support-assisted password recovery where enabled.

ArsExam does not use this repository to upload examination content, user databases, documents, media or diagnostic payloads.

## Update channels

Current clients use these public manifests:

```text
https://raw.githubusercontent.com/pgnev/arsexam-releases/main/update/stable-manifest.json
https://raw.githubusercontent.com/pgnev/arsexam-releases/main/update/test-manifest.json
```

A manifest reference is not, by itself, sufficient trust for an update. The ArsExam update process also validates the expected version/channel metadata, HTTPS transport, package integrity and the applicable release/deployment contract before activation.

Stable and Test are separate channels. Test releases are prerelease builds intended for controlled validation and must not silently replace the Stable publication policy.

## Release integrity and provenance

Official public releases are produced from the **private canonical source repository** through a controlled Windows validation pipeline.

Publication is blocked unless the applicable release prerequisites are satisfied. The public publisher verifies the source workflow/run context, source commit SHA, version/tag relationship and expected release assets before publication.

Public release assets are treated as immutable release evidence. A development build, pull-request artifact or private branch is not an official release.

## Privacy

The public update repository receives no examination banks, questions, answers, generated documents, media or local databases during a normal update check.

Crash/error diagnostics, when available in a released version, are governed separately by the ArsExam Privacy Policy and require the documented consent model. Usage/behavior analytics must not be inferred from the mere presence of update infrastructure.

For the complete disclosure applicable to distributed builds, see `PRIVACY_POLICY_BG.md` and the copy shipped with the corresponding application release.

## Security and support

For product support, use **petkoganev@gmail.com** or the in-application **Help → Contact support** flow where available.

Do **not** send passwords, Recovery Kits, complete databases, examination-bank archives, documents or other sensitive working material by e-mail unless specifically requested through a documented secure support procedure.

Security issues should be reported privately; do not disclose exploitable details in a public GitHub issue. See `SECURITY.md`.

## Repository roles

- `pgnev/arsexam-releases` — **current official public distribution/update authority**;
- `pgnev/arsexam-desktop` — legacy compatibility repository for older clients; **not** the current distribution authority;
- canonical ArsExam source/development repository — private and not a public distribution surface.

## Publication rule

A release asset, tag or manifest is official only when it has been published through the controlled ArsExam release process in this repository and the corresponding channel manifest has been intentionally promoted.

No private RC, CI artifact or development tag should be presented as a supported public release before that process is complete.
