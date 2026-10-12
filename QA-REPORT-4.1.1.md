# ArsExam 4.1.1 — QA отчет, Work, 12 октомври 2026

Квалифицирани са конкретните финални файлове, описани по-долу. Реалната GitHub публикация и независимо повторно изтеглените Setup/Update са потвърдени. Microsoft Store е отделен канал.

**Допълнение след публикацията:** потвърден е дефект в маршрута активация → Privacy → Support. Предпубликационните проверки по-долу не са включвали тази команда. Публикуваните 4.1.1 файлове съдържат дефекта; отделно провереният кандидат с поправка още не е публикуван. Записаните PASS резултати се отнасят до описания им обхват.

## Изходен код и артефакти

- Частен източник: `pgnev/arsexam-source`.
- Квалифициран commit: `38a2e0c74b83b869058244b5a133fae8397e0eb0`.
- Tree: `5b2e7b0c9218171c58aab975c06d610f04c0465c`.
- Source tag: `v4.1.1`, потвърдени еднакви local/remote commit и принадлежност към main след merge на [PR #268](https://github.com/pgnev/arsexam-source/pull/268).
- ProductVersion: `4.1.1+38a2e0c74b83b869058244b5a133fae8397e0eb0`; FileVersion/MSIX version: `4.1.1.0`.
- Прегледани начални main версии: source `d1bf1d7e51ccb9466cb598eb7056f8ef42c3390f`, public releases `9ccef2793a3b02519000c1a0945fa9e0f5d52985`.

| Файл | SHA-256 |
|---|---|
| ArsExam_Setup_4.1.1_win-x64.exe | A1FA607CAC04794E17A8B5A1977E907955416A902065B61FC11164D672159DF1 |
| ArsExam_Update_4.1.1_win-x64.zip | 32CEBC650F755C90FD965A60495DD589CF239F5EFFC74D0B8C4DAD33E538F80D |
| ArsExam_Store_4.1.1.0_x64.msix — локален QA файл, неподаден в Store | 2B8D94B25EB5DCF25FCB4C97EC8B6D11E06D6379B4D88E353960F06E323CC4A4 |
| ArsExam.exe от GitHub payload | 26A9BC06C6145B326C78C52BAC48DEE9EF344C8E75A77DE606BD13E333C0725E |
| ArsExamLauncher.exe | BCE3FD6B48496384A0188C647D78BF8842812C12BC68C0ECF8DBEBD5A95EF749 |

Release build е изпълнен за точния commit преди създаването на tag. След всички тестове immutable local/remote tag и main ancestry са проверени срещу същия commit и същите непроменени package bytes. Tagging не е използвано за преизграждане или подмяна на квалифицираните файлове. Това е локална exact-commit квалификация; не се твърди GitHub Actions PASS или изпълнен canonical exact-tag rebuild.

## Подписване

Setup, Desktop и Launcher имат действителен Authenticode статус **NotSigned**. Съществуващата release политика допуска изрично обозначено неподписано издание. HTTPS/SHA-256 удостоверяват целостта и не са издателски подпис. ECDSA подписите на лицензите са отделен механизъм.

MSIX входът остава unsigned и непроменен. За WACK и Store upgrade само копия в изолирания Sandbox са подписани с временен QA сертификат. Host trust не е променян. **Подпис на Microsoft Store/доверен издателски подпис не е валидиран чрез тези тестове.** Не е закупуван сертификат.

## Реално изпълнени проверки

| Проверка | Резултат и обхват |
|---|---|
| Release pipeline | 19/19 PASS; warnings as errors, 0 warnings/0 errors; restore, актуален NuGet vulnerability audit, protected Desktop/Launcher, JSON/DPAPI probes, startup health, ZIP shape и updater/rollback matrix. |
| Пълна .NET регресия за финалния commit | 1572 passed, 0 failed, 2 conditional skips. |
| Допълнителен solver stress | 1 passed, 0 failed, 0 skipped на финалния commit. |
| Реален local Worker/D1 + Windows HTTP/DPAPI/revocation | 1 passed, 0 failed, 0 skipped; подписан синтетичен лиценз, активен статус, изрично отнемане, блокиране след restart/offline. |
| Финални Node регресии | 312 passed, 0 failed, 0 skipped. |
| Реален изолиран workerd/D1 | Essential revocation 8; retained Owner rights/audit 10; notifications 9; service drafts CRUD 18; applicant handoff 24 проверки PASS. Изпълнени преди последната корекция само на документи; равенството на целия licensing module tree с финалния commit е проверено. |
| WACK за точния финален MSIX | **Overall PASS, partial FALSE**, exit 0; 23/24 теста PASS, 0 задължителни грешки, 1 незадължителна грешка: **Blocked executables**, index 88. Независим reviewer свърза XML, точния MSIX SHA-256, ProductVersion и 7 реално инсталирани SDK компонента. |
| Чист Desktop Setup | PASS; точни Desktop/Launcher bytes, реален activation-window launch и нормален exit 0; прочетени/сравнени 22 инсталирани документа. |
| Чист Portable Setup | PASS; точни bytes, реален launch и exit 0; прочетени/сравнени 24 документа, правилен Portable marker, без uninstaller. |
| Desktop 3.9.8 → 4.1.1 и reinstall | PASS; реални Setup операции, Data/Media/Import/Export/Backup/Licensing синтетични файлове и чужд root файл запазени; rollback версия 3.9.8 запазена; реален launch/exit 0. |
| Portable 3.9.8 → 4.1.1 и reinstall | PASS със същите byte/hash, preservation, rollback и launch/exit проверки. |
| Store 3.9.8.0 → 4.1.1.0 | PASS; реално deployment, launch, нормален close/exit 0; синтетични Data/Media/Licensing bytes запазени; точен кандидат. |
| Store 4.1.0.0 → 4.1.1.0 | PASS със същите проверки. 4.1.0 е предходен Store кандидат; не се твърди публичен GitHub 4.1.0 Setup baseline. |
| Sentry EU | Един синтетичен manual-diagnostic от действителния protected MSIX модул в изолиран QA host е потвърден независимо в authenticated Sentry UI: event `a7065cc71b024b5a8da06afa758d5cee`, release `4.1.1+38a2e0c74b83b869058244b5a133fae8397e0eb0`, context `arsexam-411-work-qualification-3fbbf998f50248298cb92ca0abd41de1`, без exception message/stack и с 0 users. Default OFF, consent и opt-out/премахване на local reports/cache PASS. Това не е изпратен диагностичен тест през native application UI. |

Инсталационните сценарии проверяват синтетични постоянни файлове и лицензна папка; не се представят за активация с реален лиценз или за тест върху клиентска база. Криптографската политика и реалните HTTP/DPAPI/отнемане са проверени отделно. Main Desktop/Launcher/Licensing source tree съвпада с по-рано квалифицирания `406d4624...`; неговите стари GUI отчети остават исторически, а не acceptance на новите bytes.

Raw baseline Setup 3.9.8 SHA-256: `347F6DFD219BCE068842AAADEFF1D1BB45BA3A69FC6D5D0193301F76F9DB8CE9`. Baseline MSIX 3.9.8.0: `5DAEBA3E31C7E5EA9E2BFF44EFB361D01F2A9E6BA30435C893435C72F63264F3`. Baseline MSIX 4.1.0.0: `9E0D81085A67A6585F712082AC74AF2F87C57FBC1385BF2F5E45B9238381725B`.

## Дефект в поддръжката, потвърден след публикацията

На 12.10.2026 г. реалният Store лог показа `NullReferenceException` в `SupportWindow..ctor` при активация → Политика за поверителност → Връзка с поддръжката. `App.Diagnostics`, diagnostics settings и update settings се създават след лицензния gate, а старият конструктор ги ползва преди това. Същият дефект е потвърден в source на GitHub 4.1.1. За контакт при тази грешка използвайте **support@arsexam.com** директно, без изискване за Support ID или ZIP.

Поправката в частния [source PR #270](https://github.com/pgnev/arsexam-source/pull/270) използва локални настройки преди създаването на нормалните услуги, без стартиране на транспорт или промяна на съгласието. Прозорецът и ZIP отчитат само съгласие за текущата версия на consent и съответния delivery target. Точно проверен implementation commit: `f31a4c3d1730f7336d1402edee300959adbaa02d`, tree `3c8eaea55b49fafe55e3485fc6ac627a4881e1ea`.

| Отделна проверка на поправката | Реален резултат |
|---|---|
| Нов реален WPF window regression преди поправката | FAIL със същия constructor null reference |
| Consent-target regression преди поправката | 2 FAIL / 2 PASS |
| Фокусирани support тестове след поправката | 9 PASS, 0 FAIL, 0 SKIP |
| Пълна .NET Release регресия | 1577 PASS, 0 FAIL, 2 съществуващи conditional skips; общо 1579 |
| Protected Release кандидат | Obfuscar 2.2.50, bundle/protected input проверен; ProductVersion `4.1.1+f31a4c3d1730f7336d1402edee300959adbaa02d` |
| Реален UI преди активация | Privacy → Support, диагностичен Preview и създаване на локален ZIP PASS |
| Затваряне и локално състояние | Нормално затваряне, completed managed cleanup/base.OnExit, процесът приключи; consent OFF, без Sentry cache или нов ERROR; числовият exit code не беше достъпен |

SHA-256 на непубликувания кандидат `ArsExam.exe`: `020B6CA183495947995D64D71455A7B2C5AC4671B47B31824ACB79C3A0A7E45C`; 187469722 bytes. Реалният UI ZIP съдържа само `README.txt`, `recent-crash-reports.txt`, `support-summary.txt`; неговият SHA-256 е `F2A41F6EED70DF3B24A341937DC0C5849F4C86B903A03CE019A2480495DF1BDC`.

Тези резултати принадлежат на **непубликувания кандидат**, отделно от квалифицираните 4.1.1 bytes от `38a2e0c…`. Те не означават обновена Store инсталация или ново преминаване на WACK, Setup/upgrade matrix, Node/Worker регресии и двата conditional теста. Restore използва кеширани пакети с изключен NuGet audit; не се твърди нов dependency security audit. Не е изпращана заявка/имейл или променяна продукционна D1. Подробният [source correction QA](https://github.com/pgnev/arsexam-source/blob/fix/preactivation-support-20261012/Documentation/ARSEXAM_PREACTIVATION_SUPPORT_FIX_QA_20261012.md) изисква достъп до частното хранилище.

## Partner Center и продукционна услуга

Partner Center е прочетен и повторно обновен преди GitHub публикацията: продукт `9PM6RKFN28HK`, Submission 3 **In certification**, Publishing **Not started**, held until Publish now. Активната Submission 2 показва `ArsExam_Store_3.9.8.0_x64.msix`. Не е променяно подаването, не е качван новият QA MSIX и не е натискан Publish now. GitHub release не е доказателство за Store сертификация/публикация.

Read-only Cloudflare проверка: Worker `edbd0c64-1324-4e7a-95e3-7c7715442a4a` на 100% трафик, 13 secret bindings, cron `*/15 * * * *` и `17 3 * * *`, миграции 0020/0021. D1: 4 заявки, 3 entitlement записа, 1 служебно известие и 1 delivery event; status delivered, оставащ email cipher 0 bytes. Проверените заявки отчетоха **rows_written=0, changed_db=false**. Не са правени deployments, D1 writes/destructive операции, нови отнемания или Brevo имейли.

## Поправени несъответствия и запазена история

Release prerequisite е сверена с support@arsexam.com. README, START_HERE, user/Recycler/update ръководства, EULA и пакетната privacy политика са синхронизирани към 4.1.1 и съществуващия одобрен текст за служебни известия. Runtime-bound privacy/third-party templates остават версията на действителното приложение; онлайн документите се публикуват с конкретна версия.

Първият документационен прогон имаше един FAIL за променена формулировка в START_HERE; формулировката е поправена и финалният пълен прогон е PASS. Кандидатът `6c77d80d...` и неговите хешове са superseded след откриване на остарели пакетни документи. Старите резултати са запазени отделно и не са използвани като финални release bytes.

Изпълнението е на наличния Windows компютър UNISOL и отделни Windows Sandbox сесии с изключена мрежа за deployment/WACK. Няма платени GitHub Actions, workflow dispatch, нова платена услуга или покупка. Raw evidence е запазено локално; публичният отчет съдържа минимизирани резултати и идентификатори.

## Публикация и authority

Транзакцията за GitHub v4.1.1 е завършена след горните PASS проверки; действителното издание, assets и Stable manifest са прочетени независимо след нея.

### Потвърдена GitHub публикация

[ArsExam v4.1.1](https://github.com/pgnev/arsexam-releases/releases/tag/v4.1.1) е публикувано на **12.10.2026 г., 09:44:08 Europe/Sofia** / 2026-10-12T06:44:08Z, non-draft и non-prerelease. GitHub asset digests и действителният Stable manifest съвпадат с финалните хешове, версията, URLs, requiresInstaller=true, minimum 3.0.1 и publishedAtUtc. Независимото повторно изтегляне е описано по-долу; post-publication документните промени не променят квалифицираните package bytes.

### Независимо повторно изтегляне

След публикацията двата действителни GitHub assets са изтеглени в нова локална директория и хеширани повторно: Setup **84 800 417 bytes**, SHA-256 A1FA607CAC04794E17A8B5A1977E907955416A902065B61FC11164D672159DF1; Update ZIP **74 956 125 bytes**, SHA-256 32CEBC650F755C90FD965A60495DD589CF239F5EFFC74D0B8C4DAD33E538F80D. И двата съвпадат с квалифицираните локални files и GitHub digests. Подробните source/public документационни промени са отделна post-publication metadata операция и не изменят tag или assets.
### Документно съгласуване и независим authority audit

Публичните README, legal/support/update документи, техническа справка, release notes и QA отчет са слети с [PR #14](https://github.com/pgnev/arsexam-releases/pull/14), merge commit `abce4f92553c424dc9cc92b4c7f8b0e4cf4a9f4b`. Release notes са прочетени след metadata update и съвпадат с пълните бележки, с абсолютни публични QA/manifest връзки.

`Validate-PublicStableReconciliation.ps1` PASS за действителните 5 public docs, 3 source release-bound docs, 14 version-neutral authority docs и unversioned roadmap. Първият post-publication прогон откри остарял current Stable 4.0.0 ред в roadmap; редът и старият fixed release-identity contract са актуализирани. Целевите post-publication документационни/authority .NET тестове: **35 passed, 0 failed, 0 skipped**. Тези промени са само в документи и release-identity тест; runtime/tag/package bytes не се променят.

`Test-ArsExamPublicReleaseAuthority.ps1` PASS, Mutation NONE: действителното latest release е v4.1.1; immutable source tag/commit/tree, canonical Stable blob `685070ef59f14d903730a8998bba350c3bc1a1b2`, publishedAtUtc, asset URLs/digests и checked-in CURRENT_STABLE са съгласувани.

[Source v4.1.1 metadata-only marker](https://github.com/pgnev/arsexam-source/releases/tag/v4.1.1) е независимо потвърден с direct API: non-draft/non-prerelease, **0 binary assets**, точен source tag и връзка към public release. Скриптът създаде marker, но непосредственото list-based readback първоначално върна not-found; оригиналният log е запазен, а следващата независима direct API проверка и cross-authority audit потвърдиха действителния marker.

### Последна промяна в Partner Center след GitHub публикацията

Проверено повторно на 12.10.2026 г., 07:17 UTC / 10:17 Europe/Sofia: Submission 3 е **Ready to publish** и е преминала сертификацията; пакетът е **ArsExam_Store_4.1.1.0_x64.msix**, x64, 74.6 MB. Publishing е **Not started**, задържано до Publish now. Store presence остава Submission 2 с пакет 3.9.8.0. Новият локален QA MSIX не е качван; съответствие на SHA-256 на вече подадения пакет с новия QA MSIX не е доказано. Не е натискан Publish now.

Проверени са и двата пакета през Manage packages и детайлите на Submission 3. Това е действителен certification резултат на вече подадения пакет; не променя обхвата на exact-byte локалната QA квалификация и не е Store publication.


Source post-publication документацията и CURRENT_STABLE са слети с [PR #269](https://github.com/pgnev/arsexam-source/pull/269), merge commit `fe443e8707fc3c7e90ed428ee16f0caaba9ef184`. Qualified source commit/tag остава `38a2e0c74b83b869058244b5a133fae8397e0eb0`; documentation main commit не е преизграден или представян като release bytes.
