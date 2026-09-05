# ArsExam Security Policy

Revision: 5 September 2026 — ArsExam 3.7.1 Stable

## Reporting a vulnerability

Report suspected ArsExam security vulnerabilities **privately** to **petkoganev@gmail.com** with subject `ArsExam security report`.

Do **not** publish exploitable details, credentials, personal data, examination-bank content, Recovery Keys, Backup passwords, Transfer codes or private diagnostic material in a public GitHub issue.

## Current public security model — ArsExam 3.7.1 Stable

ArsExam **3.7.1** is the current official Stable release. The authoritative Stable identity is `update/stable-manifest.json` plus the latest public release in this repository.

Canonical release binding:

- source repository: `pgnev/arsexam-source`;
- immutable source tag: `v3.7.1`;
- exact tagged source SHA: `7eed9fafbe89cc399f0980856632dfc11637cc88`;
- validated release tree: `882779e4c1b27999547c085b411020a8b0b9e5ad`;
- Setup SHA-256: `EA3E7CB9D9D24D910A183412A9124015CE92A005FFC4FBDEE3B3018E952856F3`;
- Update ZIP SHA-256: `64B151B2514635C718D72CB6C9ECDD318F6EF1FED539BD72BF3F09F34ABA26B2`.

Published Stable bytes are immutable. A defect in 3.7.1 must be corrected in a new version/tag; existing release assets and hashes must not be silently replaced.

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

ArsExam 3.7.1 adds checkbox multi-select bank filtering as a search/UI layer only. Filter state does not change approval, workflow, generator eligibility or security authority.

## Backup / Restore and Desktop / Portable safety

Normal `.arsexam-backup` files are protected data-only backups, not clones of the user's security identity. Mutating Restore creates a Safety Backup before live mutation and retains rollback semantics.

Desktop/Portable transfer is a local data workflow separate from the GitHub update channel. Update/uninstall cleanup may remove only ArsExam-owned program state; persistent user data remains separate from the program root.

## Crash/error diagnostics — consent 4.0

Crash/error diagnostics are **OFF by default** and require explicit opt-in. ArsExam does not send usage/behavior analytics for visited screens, banks, workflow states or functions.

ArsExam 3.7.1 uses diagnostics consent **4.0**. Eligible minimized application events may use a bounded Sentry store-and-forward cache. The Launcher has no Sentry SDK and does not send incidents remotely; it can record only a bounded local incident journal. A Launcher incident is eligible for later Desktop ingestion only when valid consent existed both at occurrence time and at ingestion time.

Remote delivery, when configured, is restricted to the approved Sentry EU/DE host pattern `*.ingest.de.sentry.io`. Intended remote payloads exclude profile credentials, Recovery Keys, Backup passwords, Transfer codes, question-bank content, databases, Media, screenshots, clipboard, filesystem paths and raw exception messages.

The detailed privacy/diagnostics contract is in `PRIVACY_POLICY_BG.md`.

## Update and release integrity

Official public binaries and manifests are distributed only through `pgnev/arsexam-releases` after controlled validation from the private canonical source repository.

The Stable feed is `update/stable-manifest.json` and resolves to **3.7.1**. Update packages are accepted only after SHA-256 verification against the authoritative manifest. Bounded retry/fallback behavior for recoverable transport/DNS failures preserves the existing installation and persistent data on failure.

The actual Release single-file application payload is protected before bundling by the pinned release-protection process and validated before packaging. This is defense-in-depth and does not replace normal secure development, integrity verification or legal licensing terms.

Exact-tag hosted Actions for `v3.7.1` failed at infrastructure startup before jobs. Under the documented release policy, publication used the accepted exact-tag local fallback after the full local gate, Windows/Setup smoke and Sentry end-to-end acceptance all passed on the immutable tagged source.

## Code signing

**ArsExam 3.7.1 Stable is unsigned with Authenticode.** HTTPS and SHA-256 provide transport/integrity controls but are not publisher-identity signing. Windows may therefore display SmartScreen/Unknown Publisher warnings depending on local policy and reputation state.

Public documentation must not claim signing until exact final release evidence proves a valid sign/timestamp/verification path.

## Reverse engineering and security research

ArsExam is proprietary software. The EULA restricts reverse engineering, decompilation, disassembly, source-code reconstruction and circumvention of technical protection measures except where applicable mandatory law or third-party licenses provide rights that cannot be excluded.

Responsible vulnerability research should minimize access to real user/examination data and should be reported privately as described above.

## Disclosure

Please allow reasonable time for validation and remediation before public disclosure. No bug-bounty or guaranteed response-time program is offered unless explicitly announced in writing.
