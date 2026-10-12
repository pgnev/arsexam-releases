# ArsExam 4.1.1 — GitHub Stable

Published 12 October 2026 at 09:44:08 Europe/Sofia / `2026-10-12T06:44:08Z`. [Official release](https://github.com/pgnev/arsexam-releases/releases/tag/v4.1.1), [Stable manifest](update/stable-manifest.json), [exact QA report](QA-REPORT-4.1.1.md).

4.1.1 preserves the original request identity and DPAPI-protected retry state before HTTP, recovers the same committed request or redeemed license after an interrupted response, rejects stale applicant/institution identity at issuance, and improves the verified optional-email status/opt-out controls and their WPF dispatcher handling. Owner rights and revocation have a minimized retained ledger and explicit confirmation. Essential revocation notices are separate from voluntary reminders, use a single Brevo attempt and do not retry ambiguous outcomes.

Installed README, start/user/Recycler/update guidance, EULA and privacy have been reconciled to 4.1.1. The runtime remains self-contained Windows x64; installation does not grant a license. Individual licensing permits one approved device and institutional licensing up to two; normal term 12 months, warning 30 days, otherwise-valid grace 7 days. Offline devices receive new revocation only at a successful online check.

## Download and integrity

| Asset | SHA-256 |
|---|---|
| [Setup](https://github.com/pgnev/arsexam-releases/releases/download/v4.1.1/ArsExam_Setup_4.1.1_win-x64.exe) | A1FA607CAC04794E17A8B5A1977E907955416A902065B61FC11164D672159DF1 |
| [Update ZIP](https://github.com/pgnev/arsexam-releases/releases/download/v4.1.1/ArsExam_Update_4.1.1_win-x64.zip) | 32CEBC650F755C90FD965A60495DD589CF239F5EFFC74D0B8C4DAD33E538F80D |

Source tag `v4.1.1`: commit `38a2e0c74b83b869058244b5a133fae8397e0eb0`, tree `5b2e7b0c9218171c58aab975c06d610f04c0465c`. The exact commit was built and qualified before the immutable tag was created; the tag and unchanged final bytes were independently bound afterwards. `requiresInstaller=true`, minimum supported update version 3.0.1. Desktop and Portable use the full Setup.

**Authenticode: UNSIGNED.** Final Setup, Desktop and Launcher are NotSigned. SHA-256 verifies integrity, not publisher identity. License ECDSA signatures and synthetic Sandbox MSIX signatures are separate mechanisms. No publisher certificate was purchased or represented by a QA certificate.

## Qualification and limits

All 19 Windows Release gates passed. Full .NET: 1572 passed, zero failed, two conditional skips subsequently executed separately (stress 1/1 and actual Windows/local Worker/DPAPI/revocation 1/1). Final Node: 312 passed, zero failed/skipped. Real isolated workerd/D1 scenarios passed. Exact Setup clean Desktop/Portable installation, 3.9.8 upgrades/reinstallation, exact hashes, installed documentation, synthetic persistent-file preservation and normal launch/exit were verified.

The separately built final MSIX passed independent full WACK: overall PASS, 23/24 tests passed, zero required failures, one optional **Blocked executables** failure. Actual Store 3.9.8.0→4.1.1.0 and 4.1.0.0→4.1.1.0 upgrades preserved synthetic Data/Media/Licensing and launched/closed normally. QA signing was confined to the disposable Sandbox; it does not validate a Microsoft Store signature. See the [QA report](QA-REPORT-4.1.1.md) for exact evidence scopes, hashes and historical/superseded runs.

## Microsoft Store remains separate

Partner Center was independently read immediately before this GitHub publication: Submission 3 **In certification**, Publishing **Not started**, held until **Publish now**. Active Submission 2 package was 3.9.8.0. The new local QA MSIX was not uploaded, certification was not cancelled and Publish now was not pressed. This GitHub release does not announce a certified or published Store 4.1.1.

Support: **support@arsexam.com**. Previous public 4.0.0 bytes and source tag remain unchanged.


Latest Partner Center status: Rechecked 12 October 2026 at 07:17 UTC / 10:17 Europe/Sofia: Submission 3 has passed certification and is **Ready to publish**, with **ArsExam_Store_4.1.1.0_x64.msix**, x64, 74.6 MB. Publishing remains **Not started**, held until Publish now. Store presence remains Submission 2 with package 3.9.8.0. The new local QA MSIX was not uploaded; the previously submitted package SHA-256 has not been matched to that QA input. Publish now was not pressed.
