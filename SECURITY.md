# ArsExam Security Policy

Revision: 3 September 2026 — ArsExam 3.6.3 Stable

## Reporting a vulnerability

Report suspected ArsExam security vulnerabilities **privately** to **petkoganev@gmail.com** with subject `ArsExam security report`.

Do **not** publish exploitable details, credentials, personal data, examination-bank content, Recovery Keys, Backup passwords, Transfer codes or private diagnostic material in a public GitHub issue.

## Current public security model — ArsExam 3.6.3 Stable

ArsExam **3.6.3** is the current official Stable release. The authoritative Stable identity is `update/stable-manifest.json` plus the latest public release in this repository.

Canonical release binding:

- source repository: `pgnev/arsexam-source`;
- immutable source tag: `v3.6.3`;
- source/merge SHA: `ff852752ea802ae9e72046b9bd76d40a87a0a179`;
- validated release tree: `b7735f3284a3980ff781737ce7496e483368b159`;
- Setup SHA-256: `8C611D1A32A0835D3DCC07F3F327E874871F948D3D2C74A7C02C24030B5509DB`;
- Update ZIP SHA-256: `3BA2E518D63F648C46E23658765041BD320365767D4637A523171246AAFCCA49`.

Published Stable bytes are immutable. A defect in 3.6.3 must be corrected in a new version/tag; existing release assets and hashes must not be silently replaced.

## Credentials and recovery

ArsExam must not embed or publish a universal profile password, master recovery key, Recovery Key, Backup password, Transfer code, signing private key, administrative credential or GitHub write credential.

Forgotten-password recovery is local and uses a single-use Recovery Key. There is no recovery e-mail backend or universal server-side/master-key bypass. Support must never request plaintext profile passwords, Recovery Keys, Backup passwords or Transfer codes.

## Local-data boundary

The main SQLite database is accessed through an encrypted SQLite3 Multiple Ciphers path after the local security envelope is unlocked. The profile password is not the direct database-encryption key.

Standalone files in `Media` and Recycler source snapshots are not individually encrypted merely because the SQLite database is encrypted. Sensitive removable storage should additionally use appropriate Windows/storage controls such as BitLocker/BitLocker To Go when required.

Protected Backup and Transfer packages use authenticated encryption independently of the live database. No at-rest control protects against malware or sufficiently privileged access to an already unlocked process/session.

## Workflow, generator and Recycler integrity

Schema v8 persists official-bank workflow state, explicit generator eligibility, versioned difficulty methodologies, assessments and expert overrides. Generator eligibility is fail-closed and is not inferred merely from record existence.

Recycler/import processing preserves explicit per-record state/outcome. Ambiguous Media/key associations are not resolved by random fallback. Atomic Recycler source snapshots are local provenance/workflow artifacts and are not remote telemetry.

## Backup / Restore and Desktop / Portable safety

Normal `.arsexam-backup` files are protected data-only backups, not clones of the user's security identity. Mutating Restore creates a Safety Backup before live mutation and retains rollback semantics.

Desktop/Portable transfer is a local data workflow separate from the GitHub update channel. Update/uninstall cleanup may remove only ArsExam-owned program state; persistent user data remains separate from the program root.

## Crash/error diagnostics — consent 4.0

Crash/error diagnostics are **OFF by default** and require explicit opt-in. ArsExam does not send usage/behavior analytics for visited screens, banks, workflow states or functions.

ArsExam 3.6.3 uses diagnostics consent **4.0**. Eligible minimized application events may use a bounded Sentry store-and-forward cache. The Launcher has no Sentry SDK and does not send incidents remotely; it can record only a bounded local incident journal. A Launcher incident is eligible for later Desktop ingestion only when valid consent existed both at occurrence time and at ingestion time.

Remote delivery, when configured, is restricted to the approved Sentry EU/DE host pattern `*.ingest.de.sentry.io`. Intended remote payloads exclude profile credentials, Recovery Keys, Backup passwords, Transfer codes, question-bank content, databases, Media, screenshots, clipboard, filesystem paths and raw exception messages.

The detailed privacy/diagnostics contract is in `PRIVACY_POLICY_BG.md`.

## Update and release integrity

Official public binaries and manifests are distributed only through `pgnev/arsexam-releases` after controlled validation from the private canonical source repository.

The Stable feed is `update/stable-manifest.json` and resolves to **3.6.3**. Update packages are accepted only after SHA-256 verification against the authoritative manifest. 3.6.3 also includes bounded retry/fallback behavior for recoverable transport/DNS failures while preserving the existing installation and persistent data on failure.

The actual Release single-file application payload is protected before bundling by the pinned release-protection process and validated before packaging. This is defense-in-depth and does not replace normal secure development, integrity verification or legal licensing terms.

## Code signing

**ArsExam 3.6.3 Stable is unsigned with Authenticode.** HTTPS and SHA-256 provide transport/integrity controls but are not publisher-identity signing. Windows may therefore display SmartScreen/Unknown Publisher warnings depending on local policy and reputation state.

Public documentation must not claim signing until exact final release evidence proves a valid sign/timestamp/verification path.

## Reverse engineering and security research

ArsExam is proprietary software. The EULA restricts reverse engineering, decompilation, disassembly, source-code reconstruction and circumvention of technical protection measures except where applicable mandatory law or third-party licenses provide rights that cannot be excluded.

Responsible vulnerability research should minimize access to real user/examination data and should be reported privately as described above.

## Disclosure

Please allow reasonable time for validation and remediation before public disclosure. No bug-bounty or guaranteed response-time program is offered unless explicitly announced in writing.
