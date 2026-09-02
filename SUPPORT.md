# ArsExam Support

Revision: 2 September 2026 — ArsExam 3.6.2 Stable

## Official contact

**petkoganev@gmail.com**

For normal product support, prefer the in-application **Help → Contact support** flow when it is available in the installed version.

## Current supported public line

The current official Stable release is **ArsExam 3.6.2**. The authoritative current-version source is `update/stable-manifest.json` together with the latest public release in this repository.

ArsExam 3.6.2 consolidates the canonical six-state workflow vocabulary, generator readiness/help, fail-closed generator eligibility, active-methodology consistency and the expanded permanent WPF snapshot matrix.

The official Stable release is published only through `pgnev/arsexam-releases`. ArsExam 3.6.2 is intentionally **unsigned with Authenticode** under the current policy; download only from the official release and verify SHA-256 against the Stable manifest/release metadata.

## What to include

A useful support request should contain only the minimum information necessary to investigate the case:

- ArsExam version and distribution mode (Desktop/Portable);
- a short description of the problem;
- exact steps that reproduce it;
- the exact user-facing error text shown by ArsExam, when relevant;
- the affected module/workflow state when relevant;
- a minimal privacy-safe diagnostic/support bundle only when relevant and intentionally attached by the user.

For update problems also include:

- source version and target version;
- whether the failure happened during check, download, integrity verification, handoff, activation, health-check or rollback when that stage is visible;
- whether retry later succeeded.

Do not send raw credentials or entire databases merely to diagnose an update problem.

## Do not send

Do **not** send by e-mail:

- plaintext profile passwords;
- Recovery Keys;
- Backup passwords;
- Transfer codes;
- complete databases or full Backup archives unless a specific support case strictly requires one and a safe transfer method has been agreed;
- confidential examination content that is not strictly required;
- signing material, API keys or unrelated credentials;
- unrelated personal data.

ArsExam support should never ask for your old plaintext password, Recovery Key, Backup password or Transfer code.

## Password recovery

Forgotten-password recovery is **local** and uses the active Recovery Key for the profile. ArsExam does not use Supabase password recovery, recovery e-mail enrollment, Request ID, support-issued reset codes or a universal server-side/master password.

After a successful recovery, the old password and the Recovery Key used for that recovery become invalid, and a new Recovery Key is generated.

When the profile supports the encrypted profile-bound Recovery Key vault, a user who still knows the current profile password can authenticate and re-view/re-export the active key from the corresponding settings workflow.

If both the current profile password and the valid Recovery Key are lost, support has no hidden bypass capable of unlocking the profile.

## Recycler / import / workflow assistance

ArsExam 3.6.2 uses a canonical six-state user-facing workflow:

- Чернова;
- За преглед;
- За одобрение;
- Одобрен;
- Отхвърлен;
- Архивиран.

Generator eligibility is a separate fail-closed condition and should not be inferred solely from the visible workflow state.

When reporting Recycler/import problems, include source type, affected module, visible workflow state/outcome, any review/error code and whether Media/key association was automatic or manually assigned. Do not send full exam archives unless strictly necessary and a safe transfer method has been agreed.

## Difficulty / generator assistance

For difficulty or generator-readiness issues, include:

- module;
- active methodology name/version where visible;
- automatic assessment vs expert override;
- the visible readiness explanation for the requested generator;
- whether the issue appears before or after recalculation/import/approval.

Factory methodology definitions and expert overrides have distinct semantics; support should not ask users to destroy overrides merely to reproduce an unrelated issue.

## Backup / Restore assistance

A Backup password is specific to its Backup and is not interchangeable with the profile password or Recovery Key.

Data-only Backup does not restore an old profile password/hash, Recovery Key/security envelope, Backup Registry secret vault, diagnostics/update settings or import-history credentials.

When reporting Backup/Restore problems, include Backup identifier, operation type (Preview/Merge/Replace), visible status/error text and ArsExam version, but do not send secret credentials themselves.

## Desktop / Portable assistance

Desktop program files normally live under `%LOCALAPPDATA%\Programs\ArsExam`, while persistent user data lives separately under `%LOCALAPPDATA%\ArsExam`.

Portable mode uses its selected portable root and does not create a Windows uninstaller.

Supported updater and migration paths are designed to preserve persistent work data. If reporting an update/transfer issue, state the source version, target version, Desktop/Portable mode and whether the issue happened before or after launcher health/rollback handling.

## Update assistance

Current Stable feed: `update/stable-manifest.json` in this repository. It currently resolves to **3.6.2** with `requiresInstaller=true`.

Official 3.6.2 assets:

- `ArsExam_Setup_3.6.2_win-x64.exe` — SHA-256 `A5D4A81500307059171E49624BAB061CBA281BFFF5CAA7E6C2E802BA90BF80A6`;
- `ArsExam_Update_3.6.2_win-x64.zip` — SHA-256 `B8F46EC121D5BBA08627CCBBDDC124080EB20655887309F63E54B88B102DC051`.

If automatic update fails because of a temporary DNS/network problem, the current installation should remain unchanged. Retry after connectivity recovers or use the official Setup from this repository. Do not manually copy arbitrary executable files from third-party sources.

ArsExam 3.6.2 Stable is **not Authenticode-signed**. Windows may therefore show SmartScreen/Unknown Publisher warnings. Verify the official GitHub source and SHA-256 values.

## Crash/error diagnostics

Crash/error diagnostics are opt-in and OFF by default. ArsExam does not send usage/behavior analytics.

When enabled and configured, remote delivery is restricted to the approved Sentry EU/DE ingest configuration and the current privacy/consent contract. The exact behavior is described in `PRIVACY_POLICY_BG.md`.

## Security reports

Suspected security vulnerabilities should be reported privately to the same contact with subject `ArsExam security report`. Do not publish exploitable details in a public GitHub issue. See `SECURITY.md`.

## Licensing questions

ArsExam is proprietary software. Questions about permitted use, redistribution, modification, reverse engineering or other licensing matters should refer first to `EULA_BG.txt`, `LICENSE.md` and `COPYRIGHT.md`. The EULA preserves rights that applicable mandatory law does not permit to be contractually excluded.

## Availability

Support is provided according to available capacity and is not a guaranteed service-level agreement unless explicitly agreed in writing.
