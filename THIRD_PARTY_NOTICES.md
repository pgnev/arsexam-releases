# ArsExam Desktop — Third-Party Notices

Revision: 27 August 2026

This public-root notice describes the **currently published ArsExam channels**:

- Stable **3.2.1**;
- Test **3.2.0** (no active prerelease).

A release remains governed by the third-party notices and licenses shipped with that specific distribution. The Stable 3.2.1 and Test 3.2.0 application projects declare the same direct runtime package set listed below.

ArsExam Desktop is proprietary software, but it incorporates open-source components distributed under their own licenses. Those licenses apply to the corresponding third-party components and are not replaced by the ArsExam EULA.

## Direct runtime dependencies — ArsExam 3.2.0 / 3.2.1

| Component | Version | License | Project / license |
|---|---:|---|---|
| ClosedXML | 0.104.2 | MIT | https://github.com/ClosedXML/ClosedXML |
| DocumentFormat.OpenXml | 3.1.1 | MIT | https://github.com/dotnet/Open-XML-SDK |
| Microsoft.Data.Sqlite.Core | 8.0.10 | MIT | https://github.com/dotnet/efcore |
| SQLite3MC.PCLRaw.bundle | 2.4.0 | MIT | https://github.com/utelle/SQLite3MultipleCiphers-NuGet |
| Sentry .NET SDK | 6.9.0 | MIT | https://github.com/getsentry/sentry-dotnet |

`SQLite3MC.PCLRaw.bundle` provides the .NET/SQLitePCLRaw integration and native SQLite3 Multiple Ciphers runtime used for ArsExam encrypted local databases. ArsExam uses an application-generated 256-bit database key through the configured encrypted SQLite connection path.

## Known transitive runtime dependencies

ClosedXML and the SQLite provider resolve additional NuGet runtime packages. The resolved graph can vary with package versions and target runtime. Known transitive components include, as applicable:

- ClosedXML.Parser;
- ExcelNumberFormat;
- Microsoft.Bcl.HashCode;
- RBush;
- SixLabors.Fonts;
- System.Buffers / System.Memory and framework-support packages where required;
- SQLitePCLRaw.core and related provider infrastructure;
- SQLite3MC.PCLRaw.lib and SQLite3MC.PCLRaw.provider;
- SQLite3 Multiple Ciphers and the SQLite core incorporated by the pinned native bundle.

NuGet/package metadata and upstream license files remain authoritative for each component. Newly introduced or materially changed runtime dependencies must be reviewed for licensing/notice obligations before public release.

## License notices

### MIT-licensed components

The MIT-licensed components listed above are used under the MIT License. Their respective copyright notices and license terms are available in the upstream repositories and package metadata.

Canonical license text: https://opensource.org/license/mit/

### SQLite3 Multiple Ciphers / SQLite3MC.PCLRaw

SQLite3 Multiple Ciphers and the maintained SQLite3MC.PCLRaw NuGet integration are distributed under the MIT License. The project provides SQLite database encryption support and incorporates the public-domain SQLite core. ArsExam does not alter or replace the upstream license terms.

Upstream projects and license information:

- https://github.com/utelle/SQLite3MultipleCiphers
- https://github.com/utelle/SQLite3MultipleCiphers-NuGet
- https://utelle.github.io/SQLite3MultipleCiphers/

### Apache-2.0 components

SQLitePCLRaw infrastructure resolved transitively by the selected .NET SQLite integration remains governed by its applicable Apache License, Version 2.0 terms and upstream notices where applicable.

Canonical license text: https://www.apache.org/licenses/LICENSE-2.0

### SQLite

The SQLite core source is released by the SQLite project as public-domain software. Non-public-domain wrappers, integrations and encryption components remain governed by their respective upstream licenses.

SQLite copyright information: https://www.sqlite.org/copyright.html

## Installer build tooling

The official ArsExam Windows Setup is compiled with Inno Setup. Inno Setup is build/distribution tooling rather than a NuGet runtime dependency of ArsExam. Its copyright and license terms remain governed by the upstream Inno Setup project and are not replaced by the ArsExam EULA.

Project / license information: https://jrsoftware.org/isinfo.php

## Hosted services

### Sentry

The Sentry .NET SDK embedded in ArsExam is an MIT-licensed open-source client library. Use of the hosted Sentry service is separate and governed by Sentry's service terms, privacy documentation and data-processing terms. Remote crash/error delivery is opt-in and restricted by ArsExam to the approved Sentry EU/DE ingest configuration.

### GitHub

GitHub is used for official ArsExam release/update distribution infrastructure. ArsExam does not use GitHub as a user-authentication or password-recovery service.

ArsExam 3.2.0 and 3.2.1 do not use Supabase for password recovery.

## Proprietary ArsExam code vs third-party rights

The original ArsExam application remains proprietary and is governed by the ArsExam EULA. Restrictions applicable to the original ArsExam application do not remove rights granted by the licenses of specific third-party components or rights that applicable mandatory law does not permit to be contractually excluded.

## Release verification requirement

Before publishing a Stable, RC or Beta build, the release procedure must confirm, using automated checks where available and manual review where necessary:

1. direct runtime package IDs and versions are represented in this notice;
2. the resolved package graph has been checked for known vulnerabilities through the configured NuGet audit;
3. newly introduced or materially changed dependencies have been reviewed for license/notice obligations;
4. the SQLite3 Multiple Ciphers/native package provenance and required notices are present in distributed legal materials;
5. this notice matches the runtime components, build/distribution tooling and hosted-service integrations actually enabled in the release.

Where a third-party license requires distribution of its complete license or copyright notice, the corresponding notice must be included with the official ArsExam distribution.

## No endorsement

Names and trademarks of third-party projects/services are used only to identify incorporated components, build tooling or external processors. Their inclusion does not imply endorsement of ArsExam by the respective copyright holders/providers.
