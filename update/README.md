# ArsExam Public Update Feeds

This directory contains the **machine-readable public update manifests** consumed by supported ArsExam Desktop clients.

## Channels

- `stable-manifest.json` — production Stable channel.
- `test-manifest.json` — Test/Beta/RC channel for explicitly opted-in users.

A Test/RC manifest must never be promoted to Stable merely by copying or renaming the file. Stable publication is a separate controlled release operation.

## Manifest contents

The manifests contain only public release metadata required by the updater, including:

- schema version;
- channel and application version;
- minimum supported version;
- HTTPS package/installer URL;
- SHA-256 package/installer digest;
- installer requirement flag;
- release notes;
- UTC publication timestamp.

They must never contain credentials, API secrets, user data, diagnostics, local paths, private repository URLs requiring authentication or application source code.

## Trust model

A manifest is only one part of the update trust chain. ArsExam also validates package integrity and release/version context before accepting an update. The controlled publisher verifies source workflow/run, source commit SHA, version/tag consistency and release artifacts before updating these feeds.

Do not manually edit a manifest to reference an artifact that was not produced and validated by the corresponding controlled release pipeline.

## Anti-downgrade rule

Publication must not silently replace a channel manifest with an older version. Any exceptional rollback must be an explicit, documented security/operations decision and must preserve data compatibility.

## Repository migration compatibility

Older ArsExam clients may temporarily retain a read-only fallback to legacy URLs under `pgnev/arsexam-desktop`. That repository is a compatibility bridge only and is not an independent release authority.

The current official public distribution authority is `pgnev/arsexam-releases`.
