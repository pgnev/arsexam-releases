# ArsExam Security Policy

Revision: 31 August 2026

## Reporting a vulnerability

Report suspected ArsExam security vulnerabilities **privately** to **petkoganev@gmail.com** with subject `ArsExam security report`.

Do **not** publish exploitable details, credentials, personal data, examination-bank content, Recovery Keys, Backup passwords, Transfer codes or private diagnostic material in a public GitHub issue.

## Current public security model — ArsExam 3.5.0 Stable

ArsExam 3.5.0 is the current official Stable release. Security-sensitive areas include authentication/lock state, Recovery Key lifecycle, encrypted local storage, protected Backup/Restore, Desktop ↔ Portable data movement, Recycler/import staging, workflow/generator eligibility, difficulty methodology state, Media disclosure boundaries, update integrity, diagnostics/privacy boundaries, dependency vulnerabilities and release provenance.

ArsExam 3.5.0 introduces schema-v8 workflow/generator-eligibility and difficulty-methodology companion state and covers that state through Backup/Restore/recovery regression gates.

The official `v3.5.0` source tag is bound to commit `6adc5a17f79f2396ca9eb4c5aa855d0c8841aa17`. The exact-tag Windows Release and public publisher completed successfully.

## Credentials and secrets

ArsExam must not embed or publish a universal profile password, master recovery key, Recovery Key, Backup password, Transfer code, signing private key, administrative credential or GitHub write credential.

Support must never request a user's plaintext profile password, Recovery Key, Backup password or Transfer code.

## Password recovery

ArsExam 3.5.0 uses a **local single-use Recovery Key**. There is no Supabase recovery backend, recovery e-mail enrollment, Request ID, support code or universal server-side/master-key bypass.

On successful forgotten-password recovery:

- the old profile password becomes invalid;
- the Recovery Key used for recovery becomes invalid;
- the new profile password becomes active;
- a new independent Recovery Key is generated.

When the profile supports the encrypted profile-bound Recovery Key vault, the active Recovery Key can be retained encrypted and re-viewed/re-exported only after authentication with the current profile password.

## Local-data boundary

The main SQLite database is accessed through an encrypted SQLite3 Multiple Ciphers connection path after the local security envelope is unlocked. The profile password is not the direct database-encryption key.

Standalone files in `Media` are **not individually encrypted** solely because the SQLite database is encrypted. Deployments requiring full device/removable-media confidentiality should also use appropriate Windows/storage controls such as BitLocker/BitLocker To Go.

Protected Backup and Transfer packages use authenticated encryption independently of the live database. No at-rest mechanism protects against malware or sufficiently privileged access to data in an already unlocked process/session.

## Schema-v8 workflow and difficulty integrity

Schema v8 persists:

- official-bank workflow state;
- explicit generator eligibility;
- versioned difficulty methodologies;
- content difficulty assessments and expert overrides.

Generator eligibility is not inferred merely from record existence. Backup validation rejects a v2 state that marks a non-Approved workflow row as generator-eligible.

Factory `ArsExam Standard 1.0` is protected; expert overrides are preserved across supported recalculation/migration paths.

## Recycler/import staging

Staged import update/delete operations use the already unlocked/keyed database service. Raw plaintext SQLite access to the protected `ArsExam.db` is not an authorized mutation path.

Recycler/import processing preserves explicit per-record state/outcome so analyzed records do not silently disappear. Ambiguous Media is not bound by random fallback; explicit expert manual assignment does not authorize approval or generator eligibility.

Supported image OCR uses the local Windows OCR path and does not require a cloud OCR service for that workflow.

## Data-only Backup v2

A normal `.arsexam-backup` remains a **data-only protected Backup**, not a clone of the user's security identity.

Snapshot v2 preserves working content plus official-bank workflow/generator-eligibility and difficulty methodology/assessment state required by ArsExam 3.5.

It deliberately does not restore old:

- profile password/hash;
- Recovery Key/security envelope;
- Backup Registry secret vault;
- diagnostics/update settings;
- import-history credentials.

Workflow `source_batch_id` is cleared when import-history tables are not part of the data-only snapshot, preventing dangling operational identity from being treated as restored provenance.

Backup creation validates schema-v8 semantic consistency before the protected package is registered as successful. Mutating Restore creates a Safety Backup before live mutation and keeps rollback behavior.

Merge is fail-closed for conflicting methodology definitions with the same ID/version and preserves the target installation's active methodology/existing-record companion state.

Legacy v1 snapshots remain readable but cannot contain provenance that the v1 format never stored; missing schema-v8 companion state is reconstructed by documented compatibility rules.

## Desktop / Portable boundary

Desktop and Portable data movement is not the GitHub update channel.

Supported Portable→Desktop import creates a Safety Backup before copying persistent work data and excludes device-local UpdateCache/Diagnostics. Protected Desktop↔Portable transfer has its own staging/authentication/recovery contract where used.

## Desktop install/update ownership boundary

Desktop uninstall and update cleanup remove only ArsExam-owned program state/version directories. Unmarked/foreign folders in a custom/shared install root must not be recursively deleted merely because they are located under a directory named `versions`.

Persistent user data under `%LOCALAPPDATA%\ArsExam` is separate from the program root under `%LOCALAPPDATA%\Programs\ArsExam`.

## Crash/error diagnostics

Crash/error diagnostics are **OFF by default** and require opt-in. ArsExam does not send usage/behavior analytics for visited screens, banks, workflow states or functions.

When remote diagnostics are configured, production ingest is restricted to the approved Sentry EU/DE host pattern `*.ingest.de.sentry.io` and requires current consent. Local minimized diagnostic history is limited to **20** reports and **30 days**. Remote diagnostic payloads must not contain profile passwords, Recovery Keys, Backup passwords, Transfer codes, question-bank content, databases, Media, screenshots or clipboard content.

## Update and release integrity

Official public binaries and manifests are distributed only through `pgnev/arsexam-releases` after controlled validation from the private canonical source repository.

A successful historical build does not validate a newer commit. Public promotion uses exact-source/exact-tag evidence and SHA-256 binding of release assets. Published Stable bytes are treated as immutable; fixes require a new version/tag rather than silent replacement.

ArsExam 3.5.0 Stable is published from source tag `v3.5.0` and is **unsigned with Authenticode** under the current policy. HTTPS and SHA-256 provide transport/integrity controls but are not Authenticode publisher identity. Windows may therefore display SmartScreen/Unknown Publisher warnings depending on local policy/reputation state.

Current public Stable feed: `update/stable-manifest.json` in this repository.

## Reverse engineering and security research

ArsExam is proprietary software. The EULA restricts reverse engineering, decompilation, disassembly, source-code reconstruction and circumvention of technical protection measures **except to the extent applicable mandatory law expressly permits such activity or prevents contractual exclusion**. This security policy does not remove statutory rights or rights granted by licenses of third-party components.

Responsible vulnerability research should minimize access to real user/examination data and should be reported privately as described above.

## Disclosure

Please allow reasonable time for validation and remediation before public disclosure. No bug-bounty or guaranteed response-time program is offered unless explicitly announced in writing.
