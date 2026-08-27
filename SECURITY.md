# ArsExam Security Policy

## Reporting a vulnerability

Report suspected ArsExam security vulnerabilities **privately** to **petkoganev@gmail.com** with subject `ArsExam security report`.

Do **not** publish exploitable details, credentials, personal data, examination-bank content, Recovery Keys, Backup passwords, Transfer codes or private diagnostic material in a public GitHub issue.

## Current public security model — ArsExam 3.2.1

ArsExam 3.2.1 is an offline-first Windows desktop application. Security-sensitive areas include authentication and lock state, Recovery Key lifecycle, encrypted local storage, protected Backup/Restore, Desktop ↔ Portable Transfer, import staging, Media disclosure boundaries, update integrity, diagnostics/privacy boundaries, dependency vulnerabilities and release provenance.

The 3.2.1 hotfix specifically removes raw plaintext SQLite mutation paths from staged import package management and hardens Desktop uninstall/update cleanup so only ArsExam-owned version directories are removed.

## Credentials and secrets

ArsExam must not embed or publish a universal profile password, master recovery key, Recovery Key, Backup password, Transfer code, signing private key, administrative credential or GitHub write credential.

Support must never request a user's plaintext profile password, Recovery Key, Backup password or Transfer code.

## Password recovery

ArsExam 3.2.1 uses a **local single-use Recovery Key**. There is no Supabase recovery backend, recovery e-mail enrollment, Request ID, support code or universal server-side/master-key bypass.

On successful forgotten-password recovery:

- the old profile password becomes invalid;
- the Recovery Key used for recovery becomes invalid;
- the new profile password becomes active;
- a new independent Recovery Key is generated.

For new 3.2+ profiles, active Recovery Key material can also be retained in an **AES-256-GCM encrypted, profile-bound local vault**. It is not stored as plaintext. After authentication with the current profile password, ArsExam can show/re-export that active key. Older profiles without a vault cannot reconstruct the old key from the verifier and may need one authenticated key replacement.

## Local-data boundary

The main SQLite database is accessed through an encrypted SQLite3 Multiple Ciphers connection path after the local security envelope is unlocked. The profile password is not the direct database-encryption key.

Standalone files in `Media` are **not individually encrypted** solely because the SQLite database is encrypted. Deployments requiring full device/removable-media confidentiality should also use appropriate Windows/storage controls such as BitLocker/BitLocker To Go.

Protected Backup and Transfer packages use authenticated encryption independently of the live database. No at-rest mechanism protects against malware or sufficiently privileged access to data in an already unlocked process/session.

## Import staging and encrypted database access

ArsExam 3.2.1 routes staged import update/delete operations through the already unlocked/keyed database service. Raw plaintext SQLite access to the protected `ArsExam.db` is not an authorized mutation path. This prevents the 3.2.0-era `SQLite Error 26: file is not a database` failure mode when editing or deleting staged packages against an encrypted profile database.

## Backup and Transfer secrets

- Recovery Key is for forgotten-password recovery and is single-use on successful recovery.
- Manual Backup password belongs to one specific Backup and is separate from the profile password and Recovery Key.
- Backup Registry may retain owner Backup credentials only inside its encrypted local registry.
- Transfer code is ephemeral and must not be retained in Transfer history/logs/diagnostics.
- These credentials must not be accepted interchangeably.

## Desktop install/update ownership boundary

Desktop uninstall and update cleanup must remove only ArsExam-owned program state/version directories. ArsExam-owned version directories carry an explicit ownership marker; unmarked/foreign folders in a custom/shared install root must not be recursively deleted merely because they are located under a directory named `versions`.

Persistent user data under `%LOCALAPPDATA%\ArsExam` is separate from the program root under `%LOCALAPPDATA%\Programs\ArsExam` and is subject to the user's uninstall/data-retention choice.

## Crash/error diagnostics

Crash/error diagnostics are **OFF by default** and require opt-in. ArsExam 3.2.1 does not send usage/behavior analytics for visited screens, banks or functions.

When remote diagnostics are configured, production ingest is restricted to the approved Sentry EU/DE host pattern `*.ingest.de.sentry.io` and uses a closed allow-list. Local minimized diagnostic history is limited to **20** reports and **30 days**. Remote diagnostic payloads must not contain profile passwords, Recovery Keys, Backup passwords, Transfer codes, question-bank content, databases, Media, screenshots or clipboard content.

## Update and release integrity

Official public binaries and manifests are distributed only through `pgnev/arsexam-releases` after controlled validation from the private canonical source repository.

A successful historical build does not validate a newer commit. Public promotion must use exact-source/exact-tag evidence and SHA-256 binding of release assets. Published Stable bytes are treated as immutable; fixes require a new version/tag rather than silent replacement.

ArsExam 3.2.1 Stable is published from source tag `v3.2.1` and is distributed unsigned under the current policy. Authenticode signing must not be claimed unless exact release evidence proves it.

## Reverse engineering and security research

ArsExam is proprietary software. The EULA restricts reverse engineering, decompilation, disassembly, source-code reconstruction and circumvention of technical protection measures **except to the extent applicable mandatory law expressly permits such activity or prevents contractual exclusion**. This security policy does not remove statutory rights or rights granted by licenses of third-party components.

Responsible vulnerability research should minimize access to real user/examination data and should be reported privately as described above.

## Disclosure

Please allow reasonable time for validation and remediation before public disclosure. No bug-bounty or guaranteed response-time program is offered unless explicitly announced in writing.
