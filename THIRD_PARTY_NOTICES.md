# ArsExam Desktop — Third-Party Notices

Revision: 25 August 2026

ArsExam Desktop is proprietary software, but it incorporates open-source components distributed under their own licenses. Those licenses apply to the corresponding third-party components and are not replaced by the ArsExam EULA.

The ArsExam release procedure combines automated package/version checks with manual license review. The release gate verifies that every direct runtime `PackageReference` and its declared version are represented in this notice; CI also performs a NuGet vulnerability audit including transitive dependencies. License classification and notice obligations for newly introduced or changed packages remain a release-review responsibility and are not represented as a fully automated legal analysis.

## Direct runtime dependencies

| Component | Version | License | Project / license |
|---|---:|---|---|
| ClosedXML | 0.104.2 | MIT | https://github.com/ClosedXML/ClosedXML |
| DocumentFormat.OpenXml | 3.1.1 | MIT | https://github.com/dotnet/Open-XML-SDK |
| Microsoft.Data.Sqlite | 8.0.10 | MIT | https://github.com/dotnet/efcore |
| SQLitePCLRaw.bundle_e_sqlite3 | 2.1.13 | Apache-2.0 | https://github.com/ericsink/SQLitePCL.raw |
| Sentry .NET SDK | 6.9.0 | MIT | https://github.com/getsentry/sentry-dotnet |

The table above describes the RC10 runtime dependency set. A released version remains governed by the third-party notices shipped with that specific distribution.

## Known transitive runtime dependencies

ClosedXML and the SQLite provider resolve additional NuGet runtime packages. The resolved graph can vary with the selected package versions and target runtime. Known transitive components include, as applicable:

- ClosedXML.Parser;
- ExcelNumberFormat;
- Microsoft.Bcl.HashCode;
- RBush;
- SixLabors.Fonts;
- System.Buffers / System.Memory and framework support packages where required by the selected target;
- SQLitePCLRaw.core, SQLitePCLRaw.provider.e_sqlite3 and the native `e_sqlite3` package used by the pinned SQLitePCLRaw 2.1.13 bundle.

NuGet/package metadata and the upstream license files remain authoritative for each component. A newly introduced or materially changed runtime dependency must be reviewed for licensing/notice obligations before a public release.

## License notices

### MIT-licensed components

The MIT-licensed components listed above are used under the MIT License. Their respective copyright notices and license terms are available in the upstream repositories and package metadata.

Canonical license text: https://opensource.org/license/mit/

### Apache-2.0 components

SQLitePCLRaw and its applicable components are used under the Apache License, Version 2.0. Copyright notices in the upstream project and package must be preserved as required by that license.

Canonical license text: https://www.apache.org/licenses/LICENSE-2.0

### SQLite native library

The bundled SQLite native library is supplied through SQLitePCLRaw. SQLite itself is released by the SQLite project as public-domain software; SQLitePCLRaw's wrapper/provider code remains subject to its own Apache-2.0 licensing and notices.

SQLite copyright: https://www.sqlite.org/copyright.html

## Hosted services

### Sentry

The **Sentry .NET SDK** embedded in the RC10 candidate is an MIT-licensed open-source client library. Use of the hosted Sentry service is separate and is governed by Sentry's service terms, privacy documentation and data-processing terms. ArsExam does not redistribute the Sentry server product.

### Supabase

The RC10 secure online password-recovery control plane uses the hosted **Supabase** service through HTTPS APIs. ArsExam does not redistribute Supabase server software. The hosted service is governed separately by Supabase service, privacy and data-processing terms. The fields, purpose and retention of the recovery integration are described in `PRIVACY_POLICY_BG.md`.

## No endorsement

Names and trademarks of third-party projects/services are used only to identify incorporated components or external processors. Their inclusion does not imply endorsement of ArsExam by the respective copyright holders/providers.

## Release verification requirement

Before publishing a Stable, RC or Beta build, the release procedure must confirm, using automated checks where available and manual review where necessary:

1. the direct runtime package IDs and versions in the application project are represented in this notice;
2. the resolved package graph has been checked for known vulnerabilities through the configured NuGet audit;
3. newly introduced or materially changed dependencies have been reviewed for license/notice obligations;
4. this notice matches the runtime components and hosted-service integrations actually enabled in the candidate being released.

Where a third-party license requires distribution of its complete license or copyright notice, the corresponding notice must be included with the official ArsExam distribution.
