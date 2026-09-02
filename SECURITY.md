# ArsExam Security Policy

Revision: 2 September 2026 — ArsExam 3.6.2 Stable

## Reporting a vulnerability

Report suspected ArsExam security vulnerabilities **privately** to **petkoganev@gmail.com** with subject `ArsExam security report`.

Do **not** publish exploitable details, credentials, personal data, examination-bank content, Recovery Keys, Backup passwords, Transfer codes or private diagnostic material in a public GitHub issue.

## Current public security model — ArsExam 3.6.2 Stable

ArsExam **3.6.2** is the current official Stable release. The authoritative Stable identity is `update/stable-manifest.json` plus the latest public release in this repository.

Canonical 3.6.2 release binding:

- source repository: `pgnev/arsexam-source`;
- immutable tag: `v3.6.2`;
- source/merge SHA: `1b52a37a186535435160fa19a6c4f92199687e9c`;
- validated release tree: `a96986932a527f72d0d0a54031588966081c3f5f`;
- Setup SHA-256: `A5D4A81500307059171E49624BAB061CBA281BFFF5CAA7E6C2E802BA90BF80A6`;
- Update ZIP SHA-256: `B8F46EC121D5BBA08627CCBBDDC124080EB20655887309F63E54B88B102DC051`.

Published Stable bytes are immutable. A defect in 3.6.2 must be corrected in a new version/tag; the existing tag/assets/hashes must not be silently replaced.

## Credentials and secrets

ArsExam must not embed or publish a universal profile password, master recovery key, Recovery Key, Backup password, Transfer code, signing private key, administrative credential or GitHub write credential.

Support must never request a user's plaintext profile password, Recovery Key, Backup password or Transfer code.

## Password recovery

ArsExam uses a **local single-use Recovery Key**. There is no Supabase recovery backend, recovery e-mail enrollment, Request ID, support code or universal server-side/master-key bypass.

On successful forgotten-password recovery:

- the old profile password becomes invalid;
- the Recovery Key used for recovery becomes invalid;
- the new profile password becomes active;
- a new independent Recovery Key is generated.

When supported by the profile, the active Recovery Key may be retained in an encrypted profile-bound vault and re-viewed/re-exported only after authentication with the current profile password.

## Local-data boundary

The main SQLite database is accessed through an encrypted SQLite3 Multiple Ciphers connection path after the local security envelope is unlocked. The profile password is not the direct database-encryption key.

Standalone files in `Media` and Recycler source snapshots are **not individually encrypted** solely because the SQLite database is encrypted. Deployments requiring full device/removable-media confidentiality should also use appropriate Windows/storage controls such as BitLocker/BitLocker To Go.

Protected Backup and Transfer packages use authenticated encryption independently of the live database. No at-rest mechanism protects against malware or sufficiently privileged access to data in an already unlocked process/session.

## Workflow, generator and Recycler integrity

Schema v8 persists official-bank workflow state, explicit generator eligibility, versioned difficulty methodologies, assessments and expert overrides.

Generator eligibility is not inferred merely from record existence or from a staged status. ArsExam 3.6.2 uses a canonical six-state workflow vocabulary and fail-closed generator readiness/eligibility checks.

Recycler/import processing preserves explicit per-record state/outcome so analyzed records do not silently disappear. Ambiguous Media/key associations are not resolved by random fallback. Atomic Recycler source snapshots are local provenance/workflow artifacts and are not remote telemetry.

## Backup / Restore and Desktop / Portable safety

Normal `.arsexam-backup` files are protected data-only backups, not clones of the user's security identity. Mutating Restore creates a Safety Backup before live mutation and retains rollback semantics.

Desktop/Portable transfer is a local data workflow and is separate from the GitHub update channel. Update/uninstall cleanup may remove only ArsExam-owned program state; persistent user data remains separate from the program root.

## Crash/error diagnostics

Crash/error diagnostics are **OFF by default** and require opt-in. ArsExam does not send usage/behavior analytics for visited screens, banks, workflow states or functions.

When remote diagnostics are configured, production ingest is restricted to the approved Sentry EU/DE host pattern `*.ingest.de.sentry.io` and requires current consent. Remote diagnostic payloads must not contain profile passwords, Recovery Keys, Backup passwords, Transfer codes, question-bank content, databases, Media, screenshots or clipboard content.

The current public 3.6.2 privacy contract is defined by `PRIVACY_POLICY_BG.md`. Any future material change to deferred delivery/caching or diagnostic fields requires an updated consent/privacy contract before publication.

## Update and release integrity

Official public binaries and manifests are distributed only through `pgnev/arsexam-releases` after controlled validation from the private canonical source repository.

The current Stable feed is `update/stable-manifest.json` and currently resolves to **3.6.2**. Update packages are accepted only after SHA-256 verification against the authoritative manifest.

A temporary DNS/transport failure must not mutate the current installation or persistent user data. Current post-3.6.2 development work may improve retry/fallback behavior, but such work is not retroactively part of immutable 3.6.2 binaries.

## Code signing

**ArsExam 3.6.2 Stable is unsigned with Authenticode.** HTTPS and SHA-256 provide transport/integrity controls but are not publisher-identity signing. Windows may therefore display SmartScreen/Unknown Publisher warnings depending on local policy and reputation state.

Future code signing is planned as a separate release hardening step. Public documentation must not claim signing until the exact final release evidence proves a valid sign/timestamp/verification path for the required artifacts.

## Reverse engineering and security research

ArsExam is proprietary software. The EULA restricts reverse engineering, decompilation, disassembly, source-code reconstruction and circumvention of technical protection measures **except to the extent applicable mandatory law expressly permits such activity or prevents contractual exclusion**. Third-party licenses retain their own rights.

Responsible vulnerability research should minimize access to real user/examination data and should be reported privately as described above.

## Disclosure

Please allow reasonable time for validation and remediation before public disclosure. No bug-bounty or guaranteed response-time program is offered unless explicitly announced in writing.
