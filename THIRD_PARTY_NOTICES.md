# ArsExam Desktop — Third-Party Notices

Revision: 3 September 2026 — ArsExam 3.6.3 Stable

ArsExam Desktop is proprietary software, but it incorporates open-source components distributed under their own licenses. Those licenses apply to the corresponding third-party components and are not replaced by the ArsExam EULA.

## Direct runtime dependencies — ArsExam 3.6.3 Stable

The ArsExam 3.6.3 release source pins the following direct runtime packages:

| Component | Version | License | Project / license |
|---|---:|---|---|
| ClosedXML | 0.104.2 | MIT | https://github.com/ClosedXML/ClosedXML |
| DocumentFormat.OpenXml | 3.1.1 | MIT | https://github.com/dotnet/Open-XML-SDK |
| Microsoft.Data.Sqlite.Core | 8.0.10 | MIT | https://github.com/dotnet/efcore |
| PdfPig | 0.1.16 | Apache-2.0 | https://github.com/UglyToad/PdfPig |
| SQLite3MC.PCLRaw.bundle | 2.4.0 | MIT | https://github.com/utelle/SQLite3MultipleCiphers-NuGet |
| Sentry .NET SDK | 6.9.0 | MIT | https://github.com/getsentry/sentry-dotnet |

This list is reconciled against `src/ArsExam.Desktop/ArsExam.Desktop.csproj` for the immutable `v3.6.3` release source. The release pipeline performs a NuGet vulnerability audit on the exact release source.

PdfPig is used locally by the Exam Recycler to extract text/content from PDF files. PDF parsing does not require a cloud service and does not upload exam documents.

`SQLite3MC.PCLRaw.bundle` provides the SQLitePCLRaw integration and native SQLite3 Multiple Ciphers runtime used for ArsExam encrypted local databases.

## Current public Stable line — ArsExam 3.6.3

ArsExam **3.6.3** is the current public Stable release. Current Stable identity is authoritative from `update/stable-manifest.json` and the latest public release in this repository.

Historical version-specific notices remain historical evidence and are not rewritten to claim that older binaries contained later dependencies or behavior.

## Known transitive runtime dependencies

Known transitive components include, as applicable: ClosedXML.Parser, ExcelNumberFormat, Microsoft.Bcl.HashCode, RBush, SixLabors.Fonts, System.Buffers/System.Memory, PdfPig transitive/runtime components, SQLitePCLRaw.core/provider infrastructure, SQLite3MC.PCLRaw.lib/provider, SQLite3 Multiple Ciphers and the SQLite core incorporated by the pinned native bundle.

NuGet/package metadata and upstream license files remain authoritative for each component. Newly introduced or materially changed dependencies must be reviewed for licensing/notice obligations before public release.

## License notices

MIT-licensed components above remain governed by their upstream MIT terms. PdfPig remains governed by its upstream Apache License 2.0 terms. SQLite3 Multiple Ciphers / SQLite3MC.PCLRaw are distributed under MIT terms and incorporate the public-domain SQLite core. Applicable SQLitePCLRaw infrastructure retains its upstream Apache-2.0 terms where applicable. SQLite core remains public-domain software according to the SQLite project.

Upstream references:
- https://opensource.org/license/mit/
- https://github.com/UglyToad/PdfPig
- https://www.apache.org/licenses/LICENSE-2.0
- https://github.com/utelle/SQLite3MultipleCiphers
- https://github.com/utelle/SQLite3MultipleCiphers-NuGet
- https://www.sqlite.org/copyright.html

## Installer build tooling

Official Windows Setup is compiled with Inno Setup. Inno Setup is build/distribution tooling rather than a NuGet runtime dependency and remains governed by its upstream terms: https://jrsoftware.org/isinfo.php

The release-protection build step uses the pinned Obfuscar Global Tool 2.2.50 as build tooling. It is not shipped as an ArsExam runtime dependency.

GitHub Actions and the official GitHub release infrastructure are release/build/distribution services; they are not embedded runtime libraries in ArsExam.

## Hosted services

The embedded Sentry .NET SDK is MIT-licensed client software. Hosted Sentry use is separate; ArsExam remote crash/error delivery remains opt-in under diagnostics consent 4.0 and restricted to the approved EU/DE ingest configuration. The Launcher itself has no Sentry SDK.

GitHub is used for official release/update distribution and is not a user-authentication or password-recovery service. ArsExam 3.6.3 does not use a server-side password-recovery backend.

## Proprietary ArsExam code vs third-party rights

The original ArsExam application remains proprietary and is governed by the ArsExam EULA. Restrictions applicable to original ArsExam code do not remove rights granted by licenses of specific third-party components or rights that applicable mandatory law does not permit to be contractually excluded.

## Release verification

Release validation must confirm exact direct runtime package IDs/versions, successful NuGet vulnerability audit, material dependency/license changes, native SQLite3MC provenance, alignment with installer/build tooling and current Stable alignment with `update/stable-manifest.json`.

Where a third-party license requires complete license/copyright notice distribution, that notice must be included with the official distribution.
