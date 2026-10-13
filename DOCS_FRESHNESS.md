# Documentation and release authority — 13 October 2026

## Current GitHub Stable: ArsExam 4.1.2

- Official release: https://github.com/pgnev/arsexam-releases/releases/tag/v4.1.2
- Immutable source tag: private `pgnev/arsexam-source/v4.1.2`, commit `7b3710377fbce8288b1488877e6a28b7ed2c3999`.
- Setup SHA-256: `0FDB942B1E4EC000A13F600B0E5519BF3D2570781F0F66F5CDE8136E597CA18D`.
- Update ZIP SHA-256: `CDEB7F22D7CA8FC32655432BA42E70E528F68CE869AC47BCBF8D4264A601FF87`.
- `requiresInstaller=true`; minimum supported update version `3.0.1`.
- GitHub Setup/Desktop/Launcher Authenticode: `NotSigned`. The Store MSIX is a separate candidate.
- [Independent QA report](QA-REPORT-4.1.2.md).
- Release publication time: 2026-10-13T03:25:20Z / 06:25:20 Europe/Sofia.

---

## Microsoft Store Submission 4 status — 13 October 2026

- Partner Center live status checked at `2026-10-13T03:57:50.7317497Z`: **ArsExam Submission 4 — Update in certification**.
- Uploaded, validated candidate: `ArsExam_Store_4.1.2.0_x64.msix`, x64, **78,204,135 bytes**, local upload-source SHA-256 `3812598F0ED3DC2A03FF89B543561B3ED0B4033B3D276D67417B7285967FECCF`.
- Previous **Submission 3 (MSIX 4.1.1.0)** remains live in Microsoft Store. Publishing remains on manual hold: **Publish now** is required after certification.
- Reviewer notes were updated for the exact 4.1.2 source and licensing workflow; the `runFullTrust` rationale is present. **Submission 4 is not yet certified or published.**
- Store product: https://apps.microsoft.com/detail/9PM6RKFN28HK. GitHub Stable 4.1.2 publication is independent of Microsoft Store certification.

---

## Historical 4.1.1 authority snapshot (preserved for provenance)


Current GitHub Stable is **[ArsExam v4.1.1](https://github.com/pgnev/arsexam-releases/releases/tag/v4.1.1)**, published `2026-10-12T06:44:08Z` / 09:44:08 Europe/Sofia. The latest public non-draft/non-prerelease release and [Stable manifest](update/stable-manifest.json) bind the qualified Setup/Update bytes to this version. The withdrawn Test feed follows the same installer and does not offer a separate prerelease.

| Authority | Verified value |
|---|---|
| Source repository/tag | private `pgnev/arsexam-source`, immutable `v4.1.1` |
| Exact source commit | 38a2e0c74b83b869058244b5a133fae8397e0eb0 |
| Exact source tree | 5b2e7b0c9218171c58aab975c06d610f04c0465c |
| Setup SHA-256 | A1FA607CAC04794E17A8B5A1977E907955416A902065B61FC11164D672159DF1 |
| Update SHA-256 | 32CEBC650F755C90FD965A60495DD589CF239F5EFFC74D0B8C4DAD33E538F80D |
| Installer requirement/minimum | true / 3.0.1 |
| Authenticode | NotSigned; explicitly disclosed unsigned release |

See [release notes](RELEASE-NOTES-4.1.1.md), [technical reference](TECHNICAL-REFERENCE-4.1.1.md) and [exact QA report](QA-REPORT-4.1.1.md). Source/package documents were corrected before building the final qualified source. Post-publication authority/report changes do not replace immutable package bytes.

Microsoft Store is independent. Partner Center was read before GitHub publication: Submission 3 **In certification**, Publishing **Not started**, held until Publish now; active Submission 2 package **3.9.8.0**. The separately built QA MSIX was not submitted. Neither a source merge nor this GitHub release proves Store certification/publication.

Cloudflare licensing was checked read-only: Worker `edbd0c64-1324-4e7a-95e3-7c7715442a4a`, migrations 0020/0021, 4 applications, 3 entitlements and one delivered essential revocation notice, with encrypted recipient cleared. No deployment, D1 write, new revocation or Brevo email was performed by the Work continuation.

4.0.0 remains immutable public historical evidence; releases before 4.0.0 are retained as owner drafts. Historical results identify their own commits/packages and cannot be relabeled as acceptance of the 4.1.1 bytes. Documentation validation must compare both repositories, actual installed files and release/manifest hashes; no evidence means no PASS.


Latest Partner Center status: Rechecked 12 October 2026 at 07:17 UTC / 10:17 Europe/Sofia: Submission 3 has passed certification and is **Ready to publish**, with **ArsExam_Store_4.1.1.0_x64.msix**, x64, 74.6 MB. Publishing remains **Not started**, held until Publish now. Store presence remains Submission 2 with package 3.9.8.0. The new local QA MSIX was not uploaded; the previously submitted package SHA-256 has not been matched to that QA input. Publish now was not pressed.
