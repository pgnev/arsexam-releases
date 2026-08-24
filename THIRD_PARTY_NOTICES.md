# ArsExam Desktop — Third-Party Notices

Revision: 24 August 2026

ArsExam Desktop is proprietary software, but it incorporates open-source components distributed under their own licenses. Those licenses apply to the corresponding third-party components and are not replaced by the ArsExam EULA.

The release process validates this inventory against the resolved NuGet dependency graph before publishing a version.

## Direct runtime dependencies

| Component | ArsExam version | License | Project / license |
|---|---:|---|---|
| ClosedXML | 0.104.2 | MIT | https://github.com/ClosedXML/ClosedXML |
| DocumentFormat.OpenXml | 3.1.1 | MIT | https://github.com/dotnet/Open-XML-SDK |
| Microsoft.Data.Sqlite | 8.0.10 | MIT | https://github.com/dotnet/efcore |
| SQLitePCLRaw.bundle_e_sqlite3 | 2.1.13 | Apache-2.0 | https://github.com/ericsink/SQLitePCL.raw |
| Sentry .NET SDK | 6.9.0 | MIT | https://github.com/getsentry/sentry-dotnet |

## Known transitive runtime dependencies

ClosedXML and the SQLite provider resolve additional NuGet runtime packages. The exact resolved versions are verified in CI for each release. They include, as applicable:

- ClosedXML.Parser;
- ExcelNumberFormat;
- Microsoft.Bcl.HashCode;
- RBush;
- SixLabors.Fonts;
- System.Buffers / System.Memory and framework support packages where required by the selected target;
- SQLitePCLRaw.core, SQLitePCLRaw.provider.e_sqlite3 and the native `e_sqlite3` package used by the pinned SQLitePCLRaw 2.1.13 bundle.

NuGet/package license metadata and upstream license files remain authoritative. Any newly resolved runtime package must be reviewed before a public release.

## License notices

MIT-licensed components are used under the MIT License, subject to preservation of applicable copyright and permission notices. Canonical license text: https://opensource.org/license/mit/

SQLitePCLRaw and applicable components are used under the Apache License, Version 2.0. Canonical license text: https://www.apache.org/licenses/LICENSE-2.0

The bundled SQLite native library is supplied through SQLitePCLRaw. SQLite itself is released by the SQLite project as public-domain software. SQLite copyright information: https://www.sqlite.org/copyright.html

## Hosted services

The **Sentry .NET SDK** embedded in ArsExam is an MIT-licensed client library. Use of the hosted Sentry service is separate and governed by Sentry service/privacy/data-processing terms.

The secure online password-recovery control plane uses the hosted **Supabase** service through HTTPS APIs. ArsExam does not redistribute Supabase server software. The hosted service is governed separately by Supabase service/privacy/data-processing terms.

## No endorsement

Names and trademarks of third-party projects/services are used only to identify incorporated components or external processors. Their inclusion does not imply endorsement of ArsExam.

## Release verification requirement

Before publishing a Stable, RC or Beta build, the release process must verify:

1. the resolved direct and transitive NuGet package graph;
2. known package vulnerabilities;
3. that no dependency was silently replaced by a package with materially different licensing terms;
4. that this notice matches the distributed runtime components and active hosted-service integrations.

Where a third-party license requires distribution of its complete license/copyright notice, the corresponding notice must be included with the official ArsExam distribution.
