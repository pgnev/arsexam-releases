# ArsExam Support

Revision: 21 September 2026 — ArsExam 3.9.4 Stable

## Official contact

**petkoganev@gmail.com**

For normal product support, prefer the in-application **Help → Contact support** flow when available.

## Current supported public line

The current official Stable release is **ArsExam 3.9.4**. The authoritative current-version source is `update/stable-manifest.json` together with the latest non-draft, non-prerelease public release in this repository.

ArsExam 3.9.4 is intentionally **not Authenticode-signed** under the current release evidence; download only from the official release and verify SHA-256 against the Stable manifest/release metadata.

**ArsExam 3.8.0 remains WITHDRAWN / DO NOT INSTALL.** ArsExam 3.9.3 is the previous Stable and remains immutable historical release evidence; 3.9.2 and 3.9.1 are earlier historical Stable releases.

## What to include

A useful support request should contain only the minimum information necessary:

- ArsExam version and distribution mode (Desktop/Portable);
- a short problem description;
- exact reproduction steps;
- the exact user-facing error text, when relevant;
- affected module/workflow state, when relevant;
- a minimal privacy-safe diagnostic/support bundle only when relevant and intentionally attached.

For update problems also include source version, target version and the visible failure stage when known. Do not send raw credentials or complete databases merely to diagnose an update problem.

## Do not send

Do **not** send by ordinary e-mail plaintext profile passwords, Recovery Keys, Backup passwords, Transfer codes, complete databases/full Backup archives, confidential examination content that is not strictly required, signing material, API keys or unrelated personal data.

Support should never ask for your old plaintext password, Recovery Key, Backup password or Transfer code.

## Password recovery

Forgotten-password recovery is **local** and uses the active Recovery Key. ArsExam does not use recovery e-mail enrollment, support-issued reset codes or a universal server-side/master password.

After successful recovery, the used Recovery Key becomes invalid and a new independent Recovery Key is generated.

## Generator / workflow assistance

Generator eligibility is a separate fail-closed condition and should not be inferred solely from a visible workflow state. When reporting generator-readiness issues include the module, selected difficulty band, active methodology where visible, relevant theme/topic and the readiness explanation shown by ArsExam.

For Module 1 listening topics, availability depends on approved, generator-eligible questions in the selected difficulty band; a draft/unapproved record alone is not sufficient. In ArsExam 3.9.4 the four mandatory listening-topic indicators reflect actual candidate availability and are not manually toggled.

## Bank search / Bank Quality assistance

ArsExam 3.9.4 retains checkbox multi-select bank filters in Modules 1–3. OR applies inside one categorical filter and AND applies across different filters; Module 1 properties are cumulative/AND. If reporting a filter issue, include the module and the exact selected filters, but do not send confidential bank content unless strictly necessary.

For Bank Quality edit/repair issues include the visible issue class, the attempted action and the fail-closed validation message. Do not bypass review gates by editing databases directly.

## Backup / Restore assistance

A Backup password is specific to its Backup and is not interchangeable with the profile password or Recovery Key. Data-only Backup does not restore an old profile password/hash, Recovery Key/security envelope, Backup Registry secret vault or diagnostics/update settings.

When reporting Backup/Restore problems include Backup identifier, operation type (Preview/Merge/Replace), visible status/error text and ArsExam version, but not the secret credentials themselves.

## Desktop / Portable assistance

Desktop program files normally live under `%LOCALAPPDATA%\Programs\ArsExam`, while persistent user data lives separately under `%LOCALAPPDATA%\ArsExam`. Portable mode uses its selected portable root and does not create a Windows uninstaller.

Supported updater and migration paths are designed to preserve persistent work data.

## Update assistance

Current Stable feed: `update/stable-manifest.json`; it resolves to **3.9.4** with `requiresInstaller=true`.

Official 3.9.4 assets:

- `ArsExam_Setup_3.9.4_win-x64.exe` — SHA-256 `1D79812EBDC2DE18B65D600B5A9228DA8A81C2060E6986429FC8B0D08BCB79C0`;
- `ArsExam_Update_3.9.4_win-x64.zip` — SHA-256 `6C0C1DDF127E47D9077DABA99BAE6700227E89576AA9B3010CEF27238566DFC9`.

If automatic update fails because of a temporary DNS/network problem, the current installation should remain unchanged. Retry after connectivity recovers or use the official Setup from this repository.

The current Test feed is separate and currently resolves to **3.9.2-rc.2**. It is a prerelease/testing channel and must not be treated as Stable authority.

## Crash/error diagnostics

Crash/error diagnostics are opt-in and OFF by default. ArsExam 3.9.4 uses diagnostics consent 4.0 and does not send usage/behavior analytics. When enabled/configured, minimized remote delivery is restricted to the approved Sentry EU/DE ingest configuration. See `PRIVACY_POLICY_BG.md` for the current contract.

## Security and licensing

Suspected vulnerabilities should be reported privately with subject `ArsExam security report`; see `SECURITY.md`.

ArsExam is proprietary software. Licensing questions should refer to the EULA, `LICENSE.md` and `COPYRIGHT.md`. Applicable mandatory-law and third-party-license rights are preserved.

## Availability

Support is provided according to available capacity and is not a guaranteed service-level agreement unless explicitly agreed in writing.
