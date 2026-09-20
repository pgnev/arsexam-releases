# ArsExam Security Policy

Revision: 21 September 2026 — public Stable binding: ArsExam 3.9.4

## Reporting a vulnerability

Report suspected ArsExam security vulnerabilities **privately** to **petkoganev@gmail.com** with subject `ArsExam security report`.

Do **not** publish exploitable details, credentials, personal data, examination-bank content, Recovery Keys, Backup passwords, Transfer codes or private diagnostic material in a public GitHub issue.

## Current public Stable binding — ArsExam 3.9.4

The current official Stable release is **ArsExam 3.9.4**. Public Stable authority is the agreement of `update/stable-manifest.json`, the latest non-draft/non-prerelease public release, and the immutable canonical source identity.

Canonical release binding:

- source repository: `pgnev/arsexam-source`;
- immutable source tag: `v3.9.4`;
- exact tagged source commit: `0cdf230ccf69cd5102a0a0ad2b1e868178dca78b`;
- exact source tree: `fe78befa4e738ba7b2a104551d0dc4fc1f9a224a`;
- Setup SHA-256: `1D79812EBDC2DE18B65D600B5A9228DA8A81C2060E6986429FC8B0D08BCB79C0`;
- Update ZIP SHA-256: `6C0C1DDF127E47D9077DABA99BAE6700227E89576AA9B3010CEF27238566DFC9`;
- Authenticode: **unsigned**.

Published Stable bytes are immutable by release policy. A defect in 3.9.4 must be corrected in a new version/tag; existing release assets and hashes must not be silently replaced.

**ArsExam 3.8.0 remains WITHDRAWN / DO NOT INSTALL.** ArsExam 3.9.3 is the previous Stable and remains immutable historical release evidence; 3.9.2 and 3.9.1 are earlier historical Stable releases.

## Credentials and recovery

ArsExam must not embed or publish a universal profile password, master recovery key, Recovery Key, Backup password, Transfer code, signing private key, administrative credential or GitHub write credential.

Forgotten-password recovery is local and uses a single-use Recovery Key. There is no recovery e-mail backend or universal server-side/master-key bypass. Support must never request plaintext profile passwords, Recovery Keys, Backup passwords or Transfer codes.

## Local-data boundary

The main SQLite database is accessed through an encrypted SQLite3 Multiple Ciphers path after the local security envelope is unlocked. The profile password is not the direct database-encryption key.

Standalone files in `Media` and Recycler source snapshots are not individually encrypted merely because the SQLite database is encrypted. Sensitive removable storage should additionally use appropriate Windows/storage controls such as BitLocker/BitLocker To Go when required.

Protected Backup and Transfer packages use authenticated encryption independently of the live database. No at-rest control protects against malware or sufficiently privileged access to an already unlocked process/session.

## Security envelope

Security-envelope parsing/unlock must fail closed. Missing security state and malformed/corrupt security state are distinct conditions. Existing malformed state must not be silently replaced by first-run initialization.

## Workflow, generator and Recycler integrity

Schema v8 persists official-bank workflow state, explicit generator eligibility, versioned difficulty methodologies, assessments and expert overrides. Generator eligibility is fail-closed and is not inferred merely from record existence.

Recycler/import processing preserves explicit per-record state/outcome. Ambiguous Media/key associations are not resolved by random fallback. Atomic Recycler source snapshots are local provenance/workflow artifacts and are not remote telemetry.

Bank-search/filter state changes search UX only and does not change approval, workflow, generator eligibility or security authority.

## Backup / Restore / Transfer

Normal `.arsexam-backup` files are protected data-only backups, not clones of the user's security identity. Mutating Restore creates a Safety Backup before live mutation and retains rollback semantics.

Backup/Restore and Transfer credentials are separate from profile password and Recovery Key and must never be accepted interchangeably.

Desktop/Portable transfer is a local data workflow separate from the GitHub update channel.

## Desktop ownership cleanup

Desktop uninstall/update cleanup may delete only ArsExam-owned program state/version directories. Unmarked foreign directories in a custom/shared install root must survive cleanup.

Persistent user data under `%LOCALAPPDATA%\ArsExam` is separate from the program root under `%LOCALAPPDATA%\Programs\ArsExam`.

## Crash/error diagnostics — consent 4.0

Crash/error diagnostics are **OFF by default** and require explicit opt-in. ArsExam does not send usage/behavior analytics for visited screens, banks, workflow states or functions.

ArsExam 3.9.4 uses diagnostics consent **4.0**. Eligible minimized application events may use a bounded Sentry store-and-forward cache. The Launcher has no Sentry SDK and does not send incidents remotely; it can record only a bounded local incident journal. A Launcher incident is eligible for later Desktop ingestion only when valid consent existed both at occurrence time and at ingestion time.

Remote delivery, when configured, is restricted to the approved Sentry EU/DE host pattern `*.ingest.de.sentry.io`. Intended remote payloads exclude profile credentials, Recovery Keys, Backup passwords, Transfer codes, question-bank content, databases, Media, screenshots, clipboard, filesystem paths and raw exception messages.

The detailed privacy/diagnostics contract is in `PRIVACY_POLICY_BG.md`.

## Update and release integrity

Official public binaries and manifests are distributed only through `pgnev/arsexam-releases` after controlled validation from the private canonical source repository.

The Stable feed is `update/stable-manifest.json` and resolves to **3.9.4** with `requiresInstaller=true`. Update packages are accepted only after SHA-256 verification against the authoritative manifest. Bounded retry/fallback behavior for recoverable transport/DNS failures preserves the existing installation and persistent data on failure.

The real Release single-file application payload is protected before bundling by the pinned release-protection process and validated before packaging. This is defense-in-depth and does not replace normal secure development, integrity verification or legal licensing terms.

Exact-tag owner-local Windows qualification and exact-tag Setup acceptance on an isolated 3.9.3 Portable baseline passed, together with Recycler persistence after restart and final-version Sentry diagnostics acceptance. Seven automated updater/rollback matrix scenarios passed; a live public-feed updater handoff was not part of pre-publication acceptance. The public release, Stable manifest, source tag and asset hashes are reconciled.

## Code signing

**ArsExam 3.9.4 Stable is not Authenticode-signed.** HTTPS and SHA-256 provide transport/integrity controls but are not publisher-identity signing. Windows may therefore display SmartScreen/Unknown Publisher warnings depending on local policy and reputation state.

Public documentation must not claim signing until exact final release evidence proves a valid sign/timestamp/verification path.

## Reverse engineering and security research

ArsExam is proprietary software. The EULA restricts reverse engineering, decompilation, disassembly, source-code reconstruction and circumvention of technical protection measures except where applicable mandatory law or third-party licenses provide rights that cannot be excluded.

Responsible vulnerability research should minimize access to real user/examination data and should be reported privately as described above.

## Disclosure

Please allow reasonable time for validation and remediation before public disclosure. No bug-bounty or guaranteed response-time program is offered unless explicitly announced in writing.

## Граница на съдържанието

Софтуерът ArsExam не съдържа, не разпространява и не предоставя достъп до служебно, поверително или защитено съдържание, свързано с ДЗИ по Теория на професията „Музикално изкуство“. Програмата представлява единствено софтуерен инструмент за създаване, редактиране, организиране и управление на съдържание, въведено или създадено от надлежно оторизирани потребители.

Публично разпространяваният изпълним софтуер не включва база данни с реални служебни изпитни материали, задачи, отговори или други защитени данни.
