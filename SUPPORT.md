# ArsExam Support

Revision: 31 August 2026

## Official contact

**petkoganev@gmail.com**

For normal product support, prefer the in-application **Help → Contact support** flow when it is available in the installed version.

## Current supported public line

The current official Stable release is **ArsExam 3.5.0**. ArsExam 3.3.0 is the previous public Stable; 3.4.0 was not published separately. The Test channel currently remains on **3.2.0** and has no active prerelease.

ArsExam 3.5.0 adds schema-v8 workflow/generator eligibility, Recycler/import per-record outcomes and review tools, versioned difficulty methodology, Backup snapshot v2 compatibility and Bulgarian-first UX improvements.

The official Stable release is published through `pgnev/arsexam-releases`. ArsExam 3.5.0 is intentionally unsigned with Authenticode; download only from the official release and use the SHA-256 values from the Stable manifest/release metadata.

## What to include

A useful support request should contain only the minimum information necessary to investigate the case:

- ArsExam version and distribution mode (Desktop/Portable);
- a short description of the problem;
- exact steps that reproduce it;
- the exact error text shown by ArsExam, when relevant;
- the affected module/workflow state when relevant;
- a minimal privacy-safe diagnostic/support bundle only when relevant and intentionally attached by the user.

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

## Password recovery in ArsExam 3.5

Forgotten-password recovery is **local** and uses the active Recovery Key for the profile.

ArsExam 3.5.0 does **not** use:

- Supabase password recovery;
- recovery e-mail enrollment;
- Request ID;
- support-issued reset codes;
- a universal server-side/master password.

After a successful recovery, the old password and the Recovery Key used for that recovery become invalid, and a new Recovery Key is generated.

When the profile supports the encrypted profile-bound Recovery Key vault, a user who still knows the current profile password can authenticate and re-view/re-export the active key from the corresponding settings workflow.

If both the current profile password and the valid Recovery Key are lost, support has no hidden bypass capable of unlocking the profile.

## Recycler / import / workflow assistance

ArsExam 3.5 keeps explicit per-record staged state/outcome so analyzed records do not silently disappear.

When reporting Recycler/import problems, include:

- source type (DOCX/PDF/XLSX/ZIP/image/audio/folder);
- affected module when known;
- visible workflow state/outcome;
- any review code/error text;
- whether Media/key association was automatic or manually assigned.

Do not send full exam archives or confidential source material unless it is strictly necessary and a safe transfer method has been agreed.

Manual Media assignment does not approve a record and does not grant generator eligibility. If a generator does not pick up a record, include both its workflow status and generator-eligibility state in the report.

## Difficulty methodology assistance

For difficulty issues, include:

- methodology name/version;
- whether the value is automatic or an expert override;
- whether the issue occurred during preview/recalculation/migration;
- the visible rationale/factor summary where relevant.

Factory `ArsExam Standard 1.0` is protected. Automatic recalculation should preserve expert overrides and reasons.

## Backup / Restore assistance

ArsExam 3.5 data-only Backup snapshot v2 preserves work data plus schema-v8 workflow/generator eligibility and difficulty methodology/assessment state.

A Backup password is specific to its Backup and is not interchangeable with the profile password or Recovery Key.

Data-only Backup does not restore an old profile password/hash, Recovery Key/security envelope, Backup Registry secret vault, diagnostics/update settings or import-history credentials.

When reporting Backup/Restore problems, include Backup identifier, operation type (Preview/Merge/Replace), visible status/error text and ArsExam version, but do not send secret credentials themselves.

Legacy snapshot v1 remains readable through compatibility reconstruction of missing schema-v8 companion state.

## Desktop / Portable assistance

Desktop program files normally live under `%LOCALAPPDATA%\Programs\ArsExam`, while persistent user data lives separately under `%LOCALAPPDATA%\ArsExam`.

Portable mode uses its selected portable root and does not create a Windows uninstaller.

Supported updater and migration paths are designed to preserve persistent work data. If reporting an update/transfer issue, state the source version, target version, Desktop/Portable mode and whether the issue happened before or after launcher health/rollback handling.

## Update assistance

Current Stable feed: `update/stable-manifest.json` in this repository.

For ArsExam 3.5.0 the manifest declares `requiresInstaller=true`. If the application reports that a full Setup is required, use the official 3.5.0 Setup rather than manually replacing executable files.

ArsExam 3.5.0 Stable is **not Authenticode-signed**. Windows may therefore show SmartScreen/Unknown Publisher warnings. This alone is not evidence that the official file is modified; verify that the download is from the official GitHub release and that the SHA-256 matches the Stable manifest/release metadata.

## Crash/error diagnostics

Crash/error diagnostics are opt-in and OFF by default. ArsExam does not send usage/behavior analytics.

When enabled, remote delivery is restricted to the approved Sentry EU/DE ingest configuration. Local minimized diagnostic history is limited to 20 reports / 30 days according to the product privacy contract.

## Security reports

Suspected security vulnerabilities should be reported privately to the same contact with subject `ArsExam security report`. Do not publish exploitable details in a public GitHub issue. See `SECURITY.md`.

## Licensing questions

ArsExam is proprietary software. Questions about permitted use, redistribution, modification, reverse engineering or other licensing matters should refer first to `EULA_BG.txt`, `LICENSE.md` and `COPYRIGHT.md`. The EULA preserves rights that applicable mandatory law does not permit to be contractually excluded.

## Availability

Support is provided according to available capacity and is not a guaranteed service-level agreement unless explicitly agreed in writing.
