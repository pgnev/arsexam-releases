# ArsExam Security Policy

## Reporting a vulnerability

Report suspected ArsExam security vulnerabilities **privately** to **petkoganev@gmail.com** with subject `ArsExam security report`.

Do **not** publish exploitable details, credentials, personal data, examination-bank content, Recovery Keys, Backup passwords, Transfer codes or private diagnostic material in a public GitHub issue.

## Current public security model — ArsExam 3.2.0

ArsExam 3.2.0 is an offline-first Windows desktop application. Security-sensitive areas include authentication and lock state, Recovery Key lifecycle, encrypted local storage, protected Backup/Restore, Desktop ↔ Portable Transfer, Media disclosure boundaries, update integrity, diagnostics/privacy boundaries, dependency vulnerabilities and release provenance.

## Credentials and secrets

ArsExam must not embed or publish a universal profile password, master recovery key, Recovery Key, Backup password, Transfer code, signing private key, administrative credential or GitHub write credential.

Support must never request a user's plaintext profile password, Recovery Key, Backup password or Transfer code.

## Password recovery

ArsExam 3.2.0 uses a **local single-use Recovery Key**. There is no Supabase recovery backend, recovery e-mail enrollment, Request ID, support code or universal server-side/master-key bypass.

On successful forgotten-password recovery:

- the old profile password becomes invalid;
- the Recovery Key used for recovery becomes invalid;
- the new profile password becomes active;
- a new independent Recovery Key is generated.

For new 3.2+ profiles, active Recovery Key material can also be retained in an **AES-256-GCM encrypted, profile-bound local vault**. It is not stored as plaintext. After authentication with the current profile password, ArsExam can show/re-export that active key. Older profiles without a vault cannot reconstruct the old key from the verifier and may need one authenticated key replacement.

## Local-data boundary

The main SQLite database is accessed through an encrypted SQLCipher-capable connection path after the local security envelope is unlocked. The profile password is not the direct database-encryption key.

Standalone files in `Media` are **not individually encrypted** solely because the SQLite database is encrypted. Deployments requiring full device/removable-media confidentiality should also use appropriate Windows/storage controls such as BitLocker/BitLocker To Go.

Protected Backup and Transfer packages use authenticated encryption independently of the live database. No at-rest mechanism protects against malware or sufficiently privileged access to data in an already unlocked process/session.

## Backup and Transfer secrets

- Recovery Key is for forgotten-password recovery and is single-use on successful recovery.
- Manual Backup password belongs to one specific Backup and is separate from the profile password and Recovery Key.
- Backup Registry may retain owner Backup credentials only inside its encrypted local registry.
- Transfer code is ephemeral and must not be retained in Transfer history/logs/diagnostics.
- These credentials must not be accepted interchangeably.

## Crash/error diagnostics

Crash/error diagnostics are OFF by default and require opt-in. ArsExam 3.2.0 does not send usage/behavior analytics for visited screens, banks or functions.

When remote diagnostics are configured, the application restricts delivery to its approved Sentry EU/DE ingest channel and uses a closed allow-list. Remote diagnostic payloads must not contain profile passwords, Recovery Keys, Backup passwords, Transfer codes, question-bank content, databases, Media, screenshots or clipboard content.

## Update and release integrity

Official public binaries and manifests are distributed only through `pgnev/arsexam-releases` after controlled validation from the private canonical source repository.

A successful historical build does not validate a newer commit. Public promotion must use exact-source/exact-tag evidence and SHA-256 binding of release assets. Published Stable bytes are treated as immutable; fixes require a new version/tag rather than silent replacement.

Authenticode signing must not be claimed unless exact release evidence proves it. ArsExam 3.2.0 Stable is distributed unsigned under the current policy.

## Disclosure

Please allow reasonable time for validation and remediation before public disclosure. No bug-bounty or guaranteed response-time program is offered unless explicitly announced in writing.
