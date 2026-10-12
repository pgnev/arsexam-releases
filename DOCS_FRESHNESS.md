# Documentation freshness

Release documentation must stay synchronized with the authoritative Stable feed and latest public release. CI should fail publication when documented Stable version, asset names, or SHA-256 values drift from `update/stable-manifest.json` or `/releases/latest`.

## Independent Microsoft Store candidate status (12 October 2026)

The Windows Store submission for **ArsExam 4.1.1.0** is recorded in [STORE-RELEASE-NOTES-4.1.1.md](STORE-RELEASE-NOTES-4.1.1.md). This is **not** a GitHub Stable release, is not the asset behind `/releases/latest`, and must not change either signed update manifest or their published SHA-256 digests.

The last verified GitHub Stable Setup and Update remain **4.0.0** until separately published assets and the verified distribution workflow establish a new GitHub Stable release. Microsoft Store certification and GitHub binary publication are independently controlled processes.

Online licencing is server-managed and may be updated independently of the Store MSIX. The technical revocation-notification changes were qualified and deployed on 12 October 2026; this documentation describes their scope without declaring the Store package released.


## Independent Stable authority check — 12 October 2026

- The latest **non-draft, non-prerelease** GitHub release is [v4.0.0](https://github.com/pgnev/arsexam-releases/releases/tag/v4.0.0). No public GitHub v4.1.1 installer or update ZIP was present during this check.
- The release assets' GitHub-reported SHA-256 digests match \`update/stable-manifest.json\`: Setup \`F65A7561CB280D791E9754396E094D18586C643B78D387BC5F5BECB499EFA8CA\`; Update ZIP \`52B9374020E0DBF77C825EFDF415A0E2268107F490E5F6CBD6A335E8F9C510CB\`.
- Both Stable and Test manifests continue to reference 4.0.0. Test is **not** a separate 4.1.1 prerelease feed.
- ArsExam 4.1.1 source changes are merged in the **private** \`pgnev/arsexam-source/main\` (PR #266 and #267). Source integration and Cloudflare licensing deployment do not qualify a Windows Setup, Store MSIX, or update package. The Microsoft Store status must be independently checked in Partner Center.
- Do not change distribution manifests or publicly declare v4.1.1 until exact-package Windows installation, upgrade, security, and asset-integrity checks are complete.
