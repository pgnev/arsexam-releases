# ArsExam public update feeds

This directory contains the public update channel manifests consumed by installed ArsExam clients.

- `test-manifest.json` — current Test/Beta/RC channel.
- `stable-manifest.json` — current Stable channel after Stable migration is promoted.

The manifests contain only public release metadata: version, channel, minimum supported version, HTTPS download URLs, SHA-256 hashes, release notes and publication time.

They must never contain credentials, user data, diagnostics, local paths, private repository URLs requiring authentication, or source code.

During the repository migration, clients may temporarily retain a read-only fallback to the former public source repository so existing installations are not disconnected. That fallback is transitional and must be removed only after the public distribution repository has been proven end-to-end and all supported clients have a migration-capable updater.
