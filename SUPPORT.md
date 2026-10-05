# Поддръжка на ArsExam

Revision: 2 October 2026 — ArsExam 3.9.8 Stable

## Official contact

**petkoganev@gmail.com**

За обичайни въпроси за продукта използвайте вградената команда **Помощ → Свържете се с поддръжката**, когато е налична.

## Current supported public line

The current official Stable release is **ArsExam 3.9.8**. The authoritative current-version source is `update/stable-manifest.json` together with the latest non-draft, non-prerelease public release in this repository.

ArsExam 3.9.8 is intentionally **not Authenticode-signed** under the current release evidence; download only from the official release and verify SHA-256 against the Stable manifest/release metadata.

**ArsExam 3.8.0 remains WITHDRAWN / DO NOT INSTALL.** ArsExam 3.9.6, 3.9.5 and 3.9.4 are previous Stable releases and remain immutable historical release evidence.

## What to include

A useful support request should contain only the minimum information necessary:

- ArsExam version and distribution mode (Desktop/Portable);
- a short problem description;
- exact reproduction steps;
- the exact user-facing error text, when relevant;
- affected module/workflow state, when relevant;
- a minimal privacy-safe diagnostic/support bundle only when relevant and intentionally attached.

При проблеми с обновяване посочете също изходната версия, целевата версия и видимия етап на грешката, когато е известен. Do not send raw credentials or complete databases merely to diagnose an update problem.

## Do not send

Do **not** send by ordinary e-mail plaintext profile passwords, Recovery Keys, Backup passwords, Transfer codes, complete databases/full Backup archives, confidential examination content that is not strictly required, signing material, API keys or unrelated personal data.

Поддръжката никога не трябва да изисква старата Ви парола в открит вид, Recovery Key, парола за Backup или Transfer code.

## Лицензиране и активация за изданията с актуализирания механизъм

След инсталиране първоначалната активация изисква интернет връзка. Потребителят подава заявка за лиценз до поддръжката и след одобрение активира съответното устройство.

- индивидуален лиценз — 1 устройство;
- институционален лиценз — до 2 устройства.

След успешната активация основната работа с ArsExam остава локална и не изисква постоянна интернет връзка. Интернет връзка може да се използва и за официални обновления, доброволна диагностика при сривове и грешки и доброволна кореспонденция с поддръжката.

При проблем със заявката за лиценз посочете версията на ArsExam, вида на лиценза и показаното съобщение за грешка. Не изпращайте профилна парола, ключ за възстановяване, парола за резервно копие, код за прехвърляне или други ненужни чувствителни данни.

## Password recovery

Forgotten-password recovery is **local** and uses the active Recovery Key. ArsExam does not use recovery e-mail enrollment, support-issued reset codes or a universal server-side/master password.

After successful recovery, the used Recovery Key becomes invalid and a new independent Recovery Key is generated.

## Generator / workflow assistance

Generator eligibility is a separate fail-closed condition and should not be inferred solely from a visible workflow state. When reporting generator-readiness issues include the module, selected difficulty band, active methodology where visible, relevant theme/topic and the readiness explanation shown by ArsExam.

For Module 1 listening topics, availability depends on approved, generator-eligible questions in the selected difficulty band; a draft/unapproved record alone is not sufficient. In ArsExam 3.9.8 the four mandatory listening-topic indicators reflect actual candidate availability and are not manually toggled.

## Bank search / Bank Quality assistance

ArsExam 3.9.8 retains checkbox multi-select bank filters in Modules 1–3. OR applies inside one categorical filter and AND applies across different filters; Module 1 properties are cumulative/AND. If reporting a filter issue, include the module and the exact selected filters, but do not send confidential bank content unless strictly necessary.

For Bank Quality edit/repair issues include the visible issue class, the attempted action and the fail-closed validation message. Do not bypass review gates by editing databases directly.

## Backup / Restore assistance

A Backup password is specific to its Backup and is not interchangeable with the profile password or Recovery Key. Data-only Backup does not restore an old profile password/hash, Recovery Key/security envelope, Backup Registry secret vault or diagnostics/update settings.

When reporting Backup/Restore problems include Backup identifier, operation type (Preview/Merge/Replace), visible status/error text and ArsExam version, but not the secret credentials themselves.

## Desktop / Portable / Microsoft Store assistance

Desktop program files normally live under `%LOCALAPPDATA%\Programs\ArsExam`, while persistent user data lives separately under `%LOCALAPPDATA%\ArsExam`. Portable mode uses its selected portable root and does not create a Windows uninstaller.

Supported updater and migration paths are designed to preserve persistent work data. Microsoft Store builds use Store-managed updates and do not use the Desktop/Portable ArsExamLauncher self-update path.

## Помощ при обновяване

Current Stable feed: `update/stable-manifest.json`; it resolves to **3.9.8** with `requiresInstaller=true`.

Official 3.9.8 assets:

- `ArsExam_Setup_3.9.8_win-x64.exe` — SHA-256 `347F6DFD219BCE068842AAADEFF1D1BB45BA3A69FC6D5D0193301F76F9DB8CE9`;
- `ArsExam_Update_3.9.8_win-x64.zip` — SHA-256 `1281663254B73124BC80F482B72E45ED978538794BC834D42B241EB93E774C78`.

Ако автоматичното обновяване се провали поради временен проблем с DNS или мрежовата връзка, текущата инсталация трябва да остане непроменена. Опитайте отново след възстановяване на връзката или използвайте официалния инсталатор от това хранилище.

The current Test feed is separate and currently resolves to **3.9.2-rc.2**. It is a prerelease/testing channel and must not be treated as Stable authority.

## Диагностика при сривове и грешки

Диагностиката при сривове и грешки е изключена по подразбиране и се включва само по желание на потребителя. ArsExam 3.9.8 uses diagnostics consent 4.0 and does not send usage/behavior analytics. When enabled/configured, minimized remote delivery is restricted to the approved Sentry EU/DE ingest configuration. See `PRIVACY_POLICY_BG.md` for the current contract.

## Сигурност и лицензиране

Suspected vulnerabilities should be reported privately with subject `ArsExam security report`; see `SECURITY.md`.

ArsExam is proprietary software. Licensing questions should refer to the EULA, `LICENSE.md` and `COPYRIGHT.md`. Applicable mandatory-law and third-party-license rights are preserved.

## Достъпност на поддръжката

Support is provided according to available capacity and is not a guaranteed service-level agreement unless explicitly agreed in writing.
