# ArsExam Desktop — Third-Party Notices

Revision: 25 August 2026

This public-root notice describes the **currently published ArsExam channels**:

- Stable **3.0.2**;
- Test **3.1.0-rc.9**.

A release remains governed by the third-party notices and licenses shipped with that specific distribution. Unpublished development candidates are not presented here as if they were already part of the public runtime.

ArsExam Desktop is proprietary software, but it incorporates open-source components distributed under their own licenses. Those licenses apply to the corresponding third-party components and are not replaced by the ArsExam EULA.

## Direct runtime dependencies in the currently published Stable/Test builds

Both the published Stable 3.0.2 source and the published Test rc.9 line declare these direct runtime packages:

| Component | Version | License | Project / license |
|---|---:|---|---|
| ClosedXML | 0.104.2 | MIT | https://github.com/ClosedXML/ClosedXML |
| DocumentFormat.OpenXml | 3.1.1 | MIT | https://github.com/dotnet/Open-XML-SDK |
| Microsoft.Data.Sqlite | 8.0.10 | MIT | https://github.com/dotnet/efcore |

## Transitive runtime components

The direct packages above resolve additional dependencies. Depending on the exact published package graph they include components such as:

- ClosedXML.Parser;
- ExcelNumberFormat;
- Microsoft.Bcl.HashCode;
- RBush;
- SixLabors.Fonts;
- SQLitePCLRaw components and the SQLite native library required by Microsoft.Data.Sqlite;
- framework-support packages required by the selected target/runtime.

NuGet/package metadata and upstream license files remain authoritative for individual third-party components.

## License families

### MIT-licensed components

MIT-licensed components are used subject to their respective copyright notices and MIT license terms.

Canonical MIT license text: https://opensource.org/license/mit/

### SQLite and SQLitePCLRaw

Microsoft.Data.Sqlite uses SQLitePCLRaw/native SQLite components transitively. SQLite itself is released by the SQLite project as public-domain software; wrapper/provider components remain governed by their respective package licenses.

SQLite copyright information: https://www.sqlite.org/copyright.html

SQLitePCLRaw project: https://github.com/ericsink/SQLitePCL.raw

## Hosted services in currently published versions

### GitHub

Current public builds use GitHub infrastructure to retrieve official update manifests/packages. This is a hosted distribution service, not a library redistributed as part of the ArsExam executable.

### Test rc.9 diagnostics note

The published Test rc.9 contains an opt-in diagnostics/telemetry **client architecture**, but the official rc.9 build does not embed a production remote diagnostics endpoint. Its remote transport requires an externally supplied `ARSEXAM_DIAGNOSTICS_ENDPOINT`; without such external configuration, diagnostic/telemetry events are not transmitted to an ArsExam-operated remote provider.

No Sentry SDK or Supabase recovery integration is part of the currently published Stable 3.0.2 or Test rc.9 direct runtime dependency set.

## Unpublished candidates

Future candidates may introduce different dependencies or hosted-service integrations. Their notices are reviewed in the private canonical source repository and are copied to this public distribution repository only when the corresponding version is actually authorized for publication.

The existence of a private candidate does not change the dependency/legal scope of an already published release.

## Release verification

Before a new public Stable, RC or Beta release, the release procedure must confirm, using automated checks where available and manual review where necessary:

1. direct runtime package IDs and versions are represented in the release notice;
2. the resolved package graph has been checked for known vulnerabilities through the configured NuGet audit;
3. newly introduced or materially changed dependencies have been reviewed for license/notice obligations;
4. hosted-service integrations actually enabled by that release are accurately disclosed.

Where a third-party license requires distribution of its complete license or copyright notice, the corresponding notice must be included with the official distribution.

## No endorsement

Names and trademarks of third-party projects/services are used only for identification. Their inclusion does not imply endorsement of ArsExam.
