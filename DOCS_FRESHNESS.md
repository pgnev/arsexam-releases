# Documentation freshness

Release documentation must stay synchronized with the authoritative Stable feed and latest public release. CI should fail publication when documented Stable version, asset names, or SHA-256 values drift from `update/stable-manifest.json` or `/releases/latest`.

## Independent Microsoft Store candidate status (12 October 2026)

The Windows Store submission for **ArsExam 4.1.1.0** is recorded in [STORE-RELEASE-NOTES-4.1.1.md](STORE-RELEASE-NOTES-4.1.1.md). This is **not** a GitHub Stable release, is not the asset behind `/releases/latest`, and must not change either signed update manifest or their published SHA-256 digests.

The last verified GitHub Stable Setup and Update remain **4.0.0** until separately published assets and the verified distribution workflow establish a new GitHub Stable release. Microsoft Store certification and GitHub binary publication are independently controlled processes.

Online licencing is server-managed and may be updated independently of the Store MSIX. The technical revocation-notification changes were qualified and deployed on 12 October 2026; this documentation describes their scope without declaring the Store package released.
