# ArsExam 4.1.1 — technical reference

Reviewed 12 October 2026. This describes the 4.1.1 source and package behavior. Publication and completed QA are recorded separately in [channel status](DOCS_FRESHNESS.md) and [release qualification](QA-REPORT-4.1.1.md).

## Release channels and identity

The private canonical source is `pgnev/arsexam-source`. The public GitHub Setup/Update authority is `pgnev/arsexam-releases`, its latest non-draft/non-prerelease release and `update/stable-manifest.json`. Microsoft Store product `9PM6RKFN28HK` uses separate MSIX submissions and Store-managed updates. A Store upload, certification, a source merge or a local package does not promote the GitHub Stable channel.

Desktop and Launcher version is 4.1.1; assembly/file version is 4.1.1.0. Exact builds embed `4.1.1+<full source commit>` in ProductVersion. Protected payloads rename selected private implementation metadata while preserving WPF and serialized contracts. Protection does not provide publisher authentication. Release SHA-256 and Authenticode status are checked independently on the final bytes. Existing repository policy permits unsigned releases with explicit disclosure; a QA certificate must never be represented as a trusted publisher certificate.

GitHub distribution is self-contained Windows x64, with a unified Inno Setup installer for Desktop and Portable and a versioned update ZIP. `requiresInstaller=true` directs supported upgrades through Setup. Node, Python and a separately installed .NET runtime are not end-user requirements. Node/workerd, .NET SDK 10, Obfuscar, Inno Setup and Windows SDK/WACK are build or qualification tools.

## Local data and updates

WPF runs local bank, generator, Recycler/import, Word/Excel and Backup/Restore workflows. Protected SQLite, profile security and recovery data are separate from versioned executable payloads. Application updates preserve user Data, Media, Import, Export and Backup folders. Setup refreshes owned user documentation. Portable transfer and backup restore move permitted data; neither grants a license to an additional device.

Launcher verifies update identity, channel and hash, activates the target version and waits for a startup health acknowledgement. Failure enters the documented rollback path. A healthy-launch probe and regression matrix do not replace installing the exact final Setup in an isolated target or verifying the corresponding installed documents.

## Request, activation and recovery

The production request endpoint is `https://arsexam.com/api/license/request`. Before sending HTTP, 4.1.1 saves the original request JSON, request ID and a 256-bit retry credential in DPAPI-protected local state. Recovery reuses that committed identity and body. It must not duplicate a request or overwrite an unrelated request. Corrupt state fails closed.

An individual license permits one named device; an institutional license permits up to two named devices. New licenses normally last 12 months. The UI warns 30 days before expiry. The 7-day grace period applies only to an otherwise valid signed license and cannot override a confirmed revocation. ECDSA-P256-SHA256 license signatures are distinct from Windows Authenticode signatures.

After an activation response or client persistence is lost, recovery may return the same previously redeemed signed license only for matching authenticated request, code and device, valid dates and a non-revoked server registry. Owner edits that change applicant or institution identity invalidate stale issuance. Local application startup, periodic online validation and the protected license state enforce the device/date/revocation policy. An offline device learns a new server revocation at its next successful online check; immediate worldwide offline blocking is not claimed.

## Owner records, erasure and revocation

The ordinary Delete action handles eligible unissued applications. Issued signed rights use the separate **Revoke all licenses** action with digest/revision confirmation. Optional erasure removes the applicant record while a minimized digest ledger and immutable Owner audit preserve revocation proof and prevent erased PII from being recreated through import/retry. SQL migrations 0020 and 0021 are additive. Production database work requires evidence about the actual schema and retained records; running release QA does not authorize resetting D1.

## Optional emails and essential notices

Optional request/expiry emails default OFF and require explicit opt-in and address verification. The Desktop provides verification, status and opt-out controls. Completion, errors and button state return through the WPF dispatcher. Brevo acceptance, delivery webhook evidence and independent inbox receipt are different events.

Revocation can reserve one essential service notice independently of voluntary reminders. The server verifies the original service address and committed group revocation before the normal erasure trigger. The recipient is AES-256-GCM encrypted in an outbox; after the single provider attempt the address is scrubbed, leaving minimized HMAC delivery evidence. An ambiguous provider result is not automatically retried. Expired reserved/handoff envelopes are scrubbed after 24 hours. A provider failure cannot prevent license revocation. No activation keys, license signatures or device identifiers are included in the service notice.

Notifications use cron `*/15 * * * *`; bounded cleanup uses `17 3 * * *`. Brevo transport uses `redirect: 'manual'`; redirects are not accepted as successful delivery and credentials are not forwarded automatically. Live production flags, cron and secret bindings must be read from Cloudflare; checked-in defaults alone do not prove deployment state.

## Privacy, diagnostics and support

Crash/error diagnostics default OFF, use explicit consent 4.0 and the configured Sentry Germany ingest endpoint, and do not add behavioral usage analytics. Local diagnostics are bounded; events without valid consent are not saved for later sending. Launcher has no independent remote diagnostics client. Public service privacy is [arsexam.com/privacy](https://arsexam.com/privacy); installed legal texts apply to the package being used.

Support is `support@arsexam.com`. Do not include profile passwords, Recovery Keys, backup passwords, activation/retry credentials, full databases or unnecessary exam/personal content in support messages.

## Required qualification evidence

Run full Release build with warnings as errors, NuGet audit, full .NET and Node regressions, isolated real workerd/D1 acceptance, protected JSON/DPAPI probes, protected startup and updater rollback checks. Then qualify exact MSIX with WACK and Store baseline upgrades, and exact Setup with clean Desktop/Portable installation and supported Setup upgrades. Record source commit/tree, tool versions, exact hashes, installed ProductVersion, data/license preservation, installed document comparisons, signing state, skipped tests and any unresolved gate. A synthetic Sandbox signature qualifies deployment behavior only, not Microsoft Store signing or final certification.

Before publishing, read the actual Partner Center status. Upload GitHub assets and promote Stable only after required gates pass. Use local Windows/RDC tools; no paid GitHub Actions are needed. Historical QA may help reproduce a test but must not be relabeled as acceptance of a different commit or package.
