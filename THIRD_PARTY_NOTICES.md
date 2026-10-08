# ArsExam Desktop — Third-Party Notices

Revision: 7 October 2026 — ArsExam Desktop 4.0.0

ArsExam Desktop is proprietary software, but it incorporates open-source components distributed under their own licenses. Those licenses apply to the corresponding third-party components and are not replaced by the ArsExam EULA.

## Content scope / Граница на съдържанието

Самата програма ArsExam не съдържа и не предоставя достъп до служебно, поверително или защитено съдържание, свързано с ДЗИ по Теория на професията „Музикално изкуство“. Тя предоставя единствено инструменти и работни процеси за упълномощени потребители за създаване, редактиране, организиране, валидиране и управление на такова съдържание.

## Direct runtime dependencies — ArsExam Desktop 4.0.0

The release source pins the following direct runtime packages (component names in the table match their NuGet package IDs):

| Component | Version | License | Project / license |
|---|---:|---|---|
| ClosedXML | 0.104.2 | MIT | https://github.com/ClosedXML/ClosedXML |
| DocumentFormat.OpenXml | 3.1.1 | MIT | https://github.com/dotnet/Open-XML-SDK |
| Microsoft.Data.Sqlite.Core | 10.0.11 | MIT | https://github.com/dotnet/efcore |
| PdfPig | 0.1.16 | Apache-2.0 | https://github.com/UglyToad/PdfPig |
| SQLite3MC.PCLRaw.bundle | 2.4.0 | MIT | https://github.com/utelle/SQLite3MultipleCiphers-NuGet |
| Sentry | 6.9.0 | MIT | https://github.com/getsentry/sentry-dotnet |

This list is reconciled against `src/ArsExam.Desktop/ArsExam.Desktop.csproj` for the exact release source. The release pipeline performs a NuGet vulnerability audit on the exact release source.

PdfPig is used locally by the Exam Recycler to extract text/content from PDF files. PDF parsing does not require a cloud service and does not upload exam documents.

`SQLite3MC.PCLRaw.bundle` provides the SQLitePCLRaw integration and native SQLite3 Multiple Ciphers runtime used for ArsExam encrypted local databases.

## Release identity

When ArsExam starts, it synchronizes this installed notice with the running application's version.

Public Stable status is determined by `Documentation/CURRENT_STABLE.json`, `pgnev/arsexam-releases/update/stable-manifest.json` and the latest non-draft, non-prerelease public release. This notice therefore does not hard-code one release number as the permanent current Stable authority.

Historical version-specific notices remain historical evidence and are not rewritten to claim that older binaries contained later dependencies or behavior.

## Restored transitive package closure for the installed Windows Desktop line

The pinned Windows Desktop dependency set for this release line is listed below. Exact source/tag identity and final artifact hashes are recorded in release qualification evidence rather than embedded as live release-status claims in this installed notice. Final exact-tag qualification must verify the restored dependency graph, vulnerability audit and shipped notices for the version being published.

| Transitive NuGet package | Resolved version | Declared upstream terms and shipped notice |
|---|---:|---|
| ClosedXML.Parser | 1.2.0 | MIT — `ClosedXML.Parser-1.2.0-MIT.txt` |
| DocumentFormat.OpenXml.Framework | 3.1.1 | MIT — uses the same upstream `DocumentFormat.OpenXml-3.1.1-MIT.txt` notice from `dotnet/Open-XML-SDK` |
| ExcelNumberFormat | 1.1.0 | MIT — `ExcelNumberFormat-1.1.0-MIT.txt`; text taken from the publisher's source repository `master` because a corresponding version tag was not established; final package license metadata/copyright must be reconciled |
| RBush | 4.0.0 | MIT — `RBush-4.0.0-MIT.txt` |
| SixLabors.Fonts | 1.0.0 | Apache-2.0 — `SixLabors.Fonts-1.0.0-Apache-2.0.txt`, from upstream tag `v1.0.0` |
| SQLite3MC.PCLRaw.lib | 2.4.0 | MIT — `SQLite3MC.PCLRaw-MIT.txt` plus `SQLite3MultipleCiphers-MIT.txt` for the native library |
| SQLite3MC.PCLRaw.provider | 2.4.0 | MIT — same upstream `SQLite3MC.PCLRaw-MIT.txt` |
| SQLitePCLRaw.core | 3.0.2 | Apache-2.0 — `SQLitePCLRaw.core-3.0.2-Apache-2.0.txt` and `SQLitePCLRaw.core-3.0.2-NOTICE.txt` |

**Version-specific caveat:** `SixLabors.Fonts` 1.0.0's upstream source tag contains the Apache License, Version 2.0. The later `main` branch describes a different Six Labors Split License; its terms must not be substituted for the pinned 1.0.0 package without separate evidence. The SQLite public-domain core does not eliminate MIT/Apache notice obligations for the surrounding packages.

All named license and notice files above are configured for distribution with both Desktop and Portable Setup and as loose readable files in the Desktop/Update ZIP payload. Those packaging declarations require actual final Windows build/Setup/ZIP verification. No claim is made here about different target frameworks or future package versions.

## License notices

MIT-licensed components above remain governed by their upstream MIT terms. PdfPig remains governed by its upstream Apache License 2.0 terms. SQLite3 Multiple Ciphers / SQLite3MC.PCLRaw are distributed under MIT terms and incorporate the public-domain SQLite core. Applicable SQLitePCLRaw infrastructure retains its upstream Apache-2.0 terms where applicable. SQLite core remains public-domain software according to the SQLite project.

Upstream references:
- https://opensource.org/license/mit/
- https://github.com/UglyToad/PdfPig
- https://www.apache.org/licenses/LICENSE-2.0
- https://github.com/utelle/SQLite3MultipleCiphers
- https://github.com/utelle/SQLite3MultipleCiphers-NuGet
- https://www.sqlite.org/copyright.html

## Pinned direct runtime package license texts included in Setup

Both Desktop and Portable Setup are configured to ship the following upstream license/copyright texts from the source tags corresponding to the pinned direct runtime package versions, under `Documentation/ThirdPartyLicenses/`. These are component-specific notices; they do not replace the separate notices required by transitive runtime libraries or the native SQLite3MC component.

| Component | Shipped upstream notice(s) | Upstream source revision |
|---|---|---|
| ClosedXML 0.104.2 | `ClosedXML-0.104.2-MIT.txt` | `ClosedXML/ClosedXML`, tag `0.104.2`, `LICENSE` |
| DocumentFormat.OpenXml 3.1.1 | `DocumentFormat.OpenXml-3.1.1-MIT.txt` | `dotnet/Open-XML-SDK`, tag `v3.1.1`, `LICENSE` |
| Microsoft.Data.Sqlite.Core 10.0.11 | `Microsoft.Data.Sqlite.Core-10.0.11-MIT.txt` | `dotnet/efcore`, tag `v10.0.11`, `LICENSE.txt` |
| PdfPig 0.1.16 | `PdfPig-0.1.16-Apache-2.0.txt`, `PdfPig-0.1.16-NOTICES.txt` | `UglyToad/PdfPig`, tag `v0.1.16`, `LICENSE` and `NOTICES.txt` |
| Sentry 6.9.0 | `Sentry-6.9.0-MIT.txt` | `getsentry/sentry-dotnet`, tag `6.9.0`, `LICENSE` |

The SQLite3MC direct bundle and its native dependency have separate notices in the section below. The exact package contents and any additional required third-party attributions must still be reconciled against the final restored dependency graph and binaries.

## SQLite3MC 2.4.0 native provenance and distributed MIT notices

The Windows x64 native `sqlite3mc.dll` is provided by the pinned NuGet package `SQLite3MC.PCLRaw.lib` 2.4.0, transitively introduced by the direct `SQLite3MC.PCLRaw.bundle` 2.4.0 dependency. The owner-local NuGet cache copy was observed at 2,373,120 bytes, file version 2.4.0, SHA-256 `C6499DD30FFE1A2F088240C1A5A190199161D2C2790CA58FA554B341FFFAE55C`; that observation does not by itself establish byte-for-byte identity with the final shipped DLL or the officially published package. Its package publisher identifies the authors as Ulrich Telle et al. and declares MIT licensing and package copyright 2023–2026. The SQLite3MC NuGet project sources place the Windows x64 native binary at `runtimes/win-x64/native/sqlite3mc.dll`, sourced from the upstream SQLite3 Multiple Ciphers build. These package and source declarations establish upstream attribution; independent byte-for-byte verification against the official published package is a separate final-binary provenance gate.

The official ArsExam Desktop/Portable Setup must distribute the following complete upstream notices alongside this document under `Documentation/ThirdPartyLicenses/`:

- `SQLite3MC.PCLRaw-MIT.txt` — upstream `utelle/SQLite3MultipleCiphers-NuGet` MIT license and copyright notice at tag `v2.4.0` (upstream LICENSE copyright 2023–2025 Ulrich Telle; the separate NuGet 2.4.0 package metadata states copyright 2023–2026 Ulrich Telle et al.).
- `SQLite3MultipleCiphers-MIT.txt` — upstream native SQLite3 Multiple Ciphers MIT license and copyright notice at tag `v2.4.0` (copyright 2019–2026 Ulrich Telle).

The included SQLite core is public-domain software according to its project; that status does not replace the separate SQLite3MC MIT notices. The main ArsExam EULA does not restrict the rights conferred by these upstream licenses. The package closure above now identifies and assigns notices to every resolved direct/transitive NuGet package for the observed target. Additional attributions embedded within package payloads, non-NuGet native/framework components and final-binary provenance remain subject to verification before publication.

Upstream source records:
- https://github.com/utelle/SQLite3MultipleCiphers-NuGet/blob/v2.4.0/LICENSE
- https://github.com/utelle/SQLite3MultipleCiphers/blob/v2.4.0/LICENSE
- https://github.com/utelle/SQLite3MultipleCiphers-NuGet/blob/v2.4.0/SQLite3MC.PCLRaw.lib/SQLite3MC.PCLRaw.lib.csproj
- https://www.nuget.org/packages/SQLite3MC.PCLRaw.lib/2.4.0

## Installer build tooling

Official Windows Setup is compiled with Inno Setup. Inno Setup is build/distribution tooling rather than a NuGet runtime dependency and remains governed by its upstream terms: https://jrsoftware.org/isinfo.php

Official release protection uses pinned Obfuscar.GlobalTool 2.2.50 as build tooling before single-file bundling. Obfuscar is not shipped as an ArsExam runtime dependency.

GitHub Actions and the official GitHub release infrastructure are release/build/distribution services; they are not embedded runtime libraries in ArsExam.

## Hosted services

ArsExam 4.0.0 can use the separately operated Cloudflare Workers/D1 licensing-request service through the configured official HTTPS endpoint. This is an activation/delivery service, not a library embedded in Desktop and not a profile-password recovery service. Signing remains owner-local; Desktop ships only public verification material. Provider hosting terms are separate from the ArsExam EULA and the licenses below.

The embedded Sentry .NET SDK is MIT-licensed client software. Hosted Sentry use is separate; ArsExam remote crash/error delivery remains opt-in and restricted to approved EU/DE ingest configuration. GitHub is used for official release/update distribution and is not a user-authentication or password-recovery service. ArsExam Desktop does not use a server-side password-recovery backend.

## Proprietary ArsExam code vs third-party rights

The original ArsExam application remains proprietary and is governed by the ArsExam EULA. Restrictions applicable to original ArsExam code do not remove rights granted by licenses of specific third-party components or rights that applicable mandatory law does not permit to be contractually excluded.

## Release verification

Release validation must confirm:

- exact direct runtime package IDs and versions from the release commit;
- successful NuGet vulnerability audit;
- any material dependency/license changes since this revision;
- native SQLite3MC provenance;
- alignment of this notice with the actual runtime, installer tooling and hosted services used by the release;
- current Stable identity alignment with `Documentation/CURRENT_STABLE.json` and the public Stable manifest.

Where a third-party license requires complete license/copyright notice distribution, that notice must be included with the official distribution.
