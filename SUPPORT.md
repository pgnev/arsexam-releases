# ArsExam Support

Revision: 3 September 2026 — ArsExam 3.6.3 Stable

## Official contact

**petkoganev@gmail.com**

For normal product support, prefer the in-application **Help → Contact support** flow when available.

## Current supported public line

The current official Stable release is **ArsExam 3.6.3**. The authoritative current-version source is `update/stable-manifest.json` together with the latest public release in this repository.

ArsExam 3.6.3 is intentionally **unsigned with Authenticode** under the current policy; download only from the official release and verify SHA-256 against the Stable manifest/release metadata.

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

For Module 1 listening topics, availability depends on approved, generator-eligible questions in the selected difficulty band; a draft/unapproved record alone is not sufficient.

## Backup / Restore assistance

A Backup password is specific to its Backup and is not interchangeable with the profile password or Recovery Key. Data-only Backup does not restore an old profile password/hash, Recovery Key/security envelope, Backup Registry secret vault or diagnostics/update settings.

When reporting Backup/Restore problems include Backup identifier, operation type (Preview/Merge/Replace), visible status/error text and ArsExam version, but not the secret credentials themselves.

## Desktop / Portable assistance

Desktop program files normally live under `%LOCALAPPDATA%\Programs\ArsExam`, while persistent user data lives separately under `%LOCALAPPDATA%\ArsExam`. Portable mode uses its selected portable root and does not create a Windows uninstaller.

Supported updater and migration paths are designed to preserve persistent work data.

## Update assistance

Current Stable feed: `update/stable-manifest.json`; it resolves to **3.6.3** with `requiresInstaller=true`.

Official 3.6.3 assets:

- `ArsExam_Setup_3.6.3_win-x64.exe` — SHA-256 `8C611D1A32A0835D3DCC07F3F327E874871F948D3D2C74A7C02C24030B5509DB`;
- `ArsExam_Update_3.6.3_win-x64.zip` — SHA-256 `3BA2E518D63F648C46E23658765041BD320365767D4637A523171246AAFCCA49`.

If automatic update fails because of a temporary DNS/network problem, the current installation should remain unchanged. Retry after connectivity recovers or use the official Setup from this repository.

## Crash/error diagnostics

Crash/error diagnostics are opt-in and OFF by default. ArsExam 3.6.3 uses diagnostics consent 4.0 and does not send usage/behavior analytics. When enabled/configured, minimized remote delivery is restricted to the approved Sentry EU/DE ingest configuration. See `PRIVACY_POLICY_BG.md` for the exact current contract.

## Security and licensing

Suspected vulnerabilities should be reported privately with subject `ArsExam security report`; see `SECURITY.md`.

ArsExam is proprietary software. Licensing questions should refer to the EULA, `LICENSE.md` and `COPYRIGHT.md`. Applicable mandatory-law and third-party-license rights are preserved.

## Availability

Support is provided according to available capacity and is not a guaranteed service-level agreement unless explicitly agreed in writing.
