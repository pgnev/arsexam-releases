# ArsExam — Official Releases & Updates

Това repository е **официалният публичен канал за дистрибуция и обновяване** на ArsExam Desktop.

**ArsExam** е Windows настолен софтуер за управление на дигитални ресурси, свързани с Държавен зрелостен изпит по Теория на професията **„Музикално изкуство“**.

**Автор и разработчик:** Petko Ganev  
**Поддръжка:** petkoganev@gmail.com  
**Copyright © 2026 Petko Ganev. All rights reserved.**

> Тук се публикуват официалните Windows binaries, update packages, manifests и публични правни/security notices. Това **не е** source-code repository и публичната му видимост не предоставя open-source лиценз върху оригиналния ArsExam код.

## Текущ официален статус

| Канал | Версия | Статус |
|---|---:|---|
| **Stable** | **3.2.1** | текущо официално Stable издание |
| **Test** | **3.2.0** | няма активен prerelease; каналът остава върху последния умишлено promoted Test manifest |

Авторитетни за каналите са `update/stable-manifest.json` и `update/test-manifest.json`.

Branch, PR, CI build или private candidate не е официален release. Съществуващите Stable release assets не се подменят тихо; корекция се публикува с нова version/tag линия.

## ArsExam 3.2.1 Stable

ArsExam 3.2.1 е hotfix издание върху 3.2.x линията. То запазва offline-first архитектурата и добавя корекции за:

- управление на staged/import пакети върху защитената локална база без plaintext SQLite bypass;
- редактиране и изтриване на staged записи/пакети без `SQLite Error 26: file is not a database`;
- безопасно Desktop uninstall почистване на launcher/update-owned program files;
- защита на чужди/немаркирани `versions` директории при custom install path;
- version ownership marker без UTF-8 BOM за надеждно разпознаване от installer/uninstaller логиката.

### Offline-first и защитено локално хранилище

Основната работа с профил, изпитни банки, генератори, import/export, Backup/Restore и Desktop↔Portable Transfer остава локална.

- plaintext профилната парола не се съхранява;
- локалната автентикация използва versioned salted PBKDF2-HMAC-SHA256 verification;
- основната SQLite база използва криптиран SQLite3 Multiple Ciphers connection path след отключване на local security envelope;
- профилната парола не е директният database-encryption key;
- purpose-separated keys се използват за database, Backup Registry, Transfer Registry и Recovery Key vault.

### Recovery Key

Възстановяването на забравена парола е **локално**. ArsExam 3.2.1 не използва Supabase, recovery e-mail, Request ID, support code или универсален server-side/master key.

Recovery Key е single-use при успешно password recovery; използваният ключ и старата парола стават невалидни, генерира се нов ключ, а при нови 3.2+ профили активният ключ може да бъде пазен в **AES-256-GCM encrypted profile-bound vault** и след проверка с текущата профилна парола да бъде показан, копиран, повторно записан като TXT и отпечатан/запазен като PDF.

### Protected Backup / Restore / Transfer

Ръчните Backup-и използват защитен `.arsexam-backup` формат с отделен Backup номер и отделна Backup парола. Restore поддържа preview, Merge/„Допълни“, Safe Replace/„Замени безопасно“, Safety Backup и rollback при failure. Desktop↔Portable Transfer използва отделен Transfer ID/code, authenticated encrypted package, staging/validation и rollback/recovery механизъм.

### Crash/error диагностика

Crash/error диагностиката е **opt-in** и е изключена по подразбиране. ArsExam не изпраща usage/behavior analytics за използвани екрани, банки или функции.

При включена диагностика local history е ограничена до **20** минимизирани отчета за не повече от **30 дни**. Remote delivery е възможен само към одобрения Sentry EU/DE host pattern `*.ingest.de.sentry.io` и само при валидно текущо потребителско съгласие.

### Важна storage граница

Криптираната SQLite база **не означава**, че standalone файловете в `Media` са индивидуално криптирани при покой. При чувствителен removable storage използвайте и подходяща Windows/storage защита, например BitLocker/BitLocker To Go.

## Инсталиране и обновления

Официалният ArsExam Setup поддържа **clean install** и предлага Desktop или Portable режим. Не са необходими Python, Node.js, Microsoft Access или предварително инсталиран .NET Runtime.

Update flow валидира официалния HTTPS source, version/channel contract, package shape и SHA-256 преди activation и използва versioned deployment/launcher health-check/rollback механизъм.

### Code signing

Не се твърди Authenticode signing, освен когато exact release evidence действително го доказва. ArsExam 3.2.1 Stable е публикуван unsigned по действащата release policy; изтегляйте го само от официалния release и проверявайте manifest/SHA-256 binding-а.

## Release integrity и provenance

Официалните releases се произвеждат от private canonical source чрез контролиран Windows validation/publisher pipeline. Public publisher проверява exact source SHA, version/tag relationship, immutable release context, Setup/update assets и SHA-256 binding преди feed promotion.

Публикуваните Stable bytes се третират като immutable. Поправка на 3.2.1 трябва да бъде нова версия, а не тихо заменен `v3.2.1` asset.

## Licensing, privacy, security и support

ArsExam е **proprietary software**. Официалните binaries се използват съгласно EULA. Освен доколкото приложимото императивно право изрично допуска друго, не се предоставя право за обратно инженерство, декомпилация, дизасемблиране, реконструиране на изходен код, заобикаляне на технически защити или създаване на производни версии на оригиналното приложение. Third-party компонентите запазват собствените си лицензи и предоставените от тях права.

Публични документи:

- `LICENSE.md`
- `COPYRIGHT.md`
- `EULA_BG.txt`
- `PRIVACY_POLICY_BG.md`
- `THIRD_PARTY_NOTICES.md`
- `SECURITY.md`
- `SUPPORT.md`

Не изпращайте по e-mail profile passwords, Recovery Keys, Backup passwords, Transfer codes, цели бази или ненужно изпитно съдържание. Security проблеми се докладват частно на **petkoganev@gmail.com**.

## Repository роли

- `pgnev/arsexam-releases` — **официален публичен distribution/update authority**;
- `pgnev/arsexam-source` — private canonical source/development repository;
- `pgnev/arsexam-desktop` — legacy compatibility repository, не независим release authority;
- `pgnev/arsexam` — исторически web repository, не текущ Desktop authority.

## Publication rule

Release asset, tag или manifest е официален само когато е публикуван чрез контролирания ArsExam release процес и съответният channel manifest е умишлено promoted.
