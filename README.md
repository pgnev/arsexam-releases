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
| **Stable** | **3.2.0** | текущо официално Stable издание |
| **Test** | **3.2.0** | временно синхронизиран със Stable; няма активен prerelease |

Авторитетни за каналите са `update/stable-manifest.json` и `update/test-manifest.json`.

Branch, PR, CI build или private candidate не е официален release. Съществуващите Stable release assets не се подменят тихо; корекция се публикува с нова version/tag линия.

## Инсталиране

Официалният ArsExam Setup поддържа **clean install** и предлага:

- **Desktop** — per-user Windows инсталация с отделни program и persistent-data папки;
- **Portable** — самостоятелна структура за избрана папка/USB носител.

Не са необходими Python, Node.js, Microsoft Access или предварително инсталиран .NET Runtime. Word/Excel са нужни само за външно отваряне/редактиране на съответните генерирани документи.

## ArsExam 3.2.0

### Offline-first и защитено локално хранилище

Основната работа с профил, изпитни банки, генератори, import/export, Backup/Restore и Desktop↔Portable Transfer остава локална.

- plaintext профилната парола не се съхранява;
- локалната автентикация използва versioned salted PBKDF2-HMAC-SHA256 verification;
- основната SQLite база използва SQLCipher-capable encrypted connection path след отключване на local security envelope;
- профилната парола не е директният database-encryption key;
- purpose-separated keys се използват за database, Backup Registry, Transfer Registry и Recovery Key vault.

### Recovery Key — 3.2

Възстановяването на забравена парола е **локално**. ArsExam 3.2.0 не използва Supabase, recovery e-mail, Request ID, support code или универсален server-side/master key.

Recovery Key:

- се генерира локално;
- е single-use при успешно password recovery;
- използваният ключ и старата парола стават невалидни след успешна ротация;
- генерира се нов Recovery Key;
- при нови 3.2+ профили активният ключ има и **AES-256-GCM encrypted profile-bound vault**;
- след проверка с текущата профилна парола може да бъде показан, копиран, повторно записан като TXT и отпечатан/запазен като PDF;
- не е Backup password и не е Transfer code.

При профил, създаден от по-стара версия без Recovery Key vault, старият ключ не може да бъде реконструиран от verifier-а; при известна текуща парола потребителят може безопасно да го замени с нов.

### Protected Backup / Backup Registry / Restore

Ръчните Backup-и използват защитен `.arsexam-backup` формат с отделен Backup номер и отделна Backup парола.

Backup Registry поддържа търсене, дата, extended multi-selection, preview, изтриване на ръчни Backup-и и защитено показване/експорт на owner credentials. Чувствителните действия използват една step-up проверка с текущата профилна парола за отворения Registry прозорец.

Restore започва от registry-style chooser и поддържа:

- preview преди mutation;
- **Merge / „Допълни“** — добавя липсващи записи без тихо презаписване на конфликтни файлове;
- **Safe Replace / „Замени безопасно“** — създава Safety Backup преди подмяна;
- автоматичен rollback при failure след започнала mutation;
- външен Backup с неговата собствена Backup парола.

Data-only Restore не връща стара профилна парола или стар Recovery Key.

### Desktop ↔ Portable Transfer

Защитеният Transfer между Desktop и Portable на един Windows компютър използва отделен Transfer ID, временен Transfer code, local IPC/heartbeat, encrypted authenticated package, staging/validation, Safety Backup и rollback/recovery journal. Transfer code не се пази в историята като plaintext credential.

### Crash/error диагностика

Crash/error diagnostics са **OFF по подразбиране** и се активират само с opt-in. ArsExam 3.2.0 не изпраща usage/behavior analytics за използвани екрани, банки или функции.

Remote crash/error delivery е възможно само при валидно конфигуриран Sentry EU/DE канал и текущо потребителско съгласие. Приложението използва ограничен allow-list payload и не добавя профилна парола, Recovery Key, Backup passwords, Transfer codes, question-bank content, Media, screenshots или clipboard.

### Важна storage граница

Криптираната SQLite база **не означава**, че standalone файловете в `Media` са индивидуално криптирани при покой. При чувствителен removable storage използвайте и подходяща Windows/storage защита, например BitLocker/BitLocker To Go.

## Обновления

ArsExam използва официалната GitHub release/update инфраструктура. Update flow валидира HTTPS source, version/channel contract, package shape и SHA-256 преди activation и използва versioned deployment/launcher health-check/rollback механизъм.

При настройка **„Автоматично — проверка на 12 часа“** проверката се извършва на 12-часов интервал. Липсата на интернет не блокира основната offline работа.

### Code signing

Не се твърди Authenticode signing, освен когато exact release evidence действително го доказва. ArsExam 3.2.0 Stable е публикуван unsigned по действащата release policy; изтегляйте го само от официалния release тук и проверявайте manifest/SHA-256 binding-а.

## Release integrity и provenance

Официалните releases се произвеждат от private canonical source чрез контролиран Windows validation/publisher pipeline. Public publisher проверява source workflow/run identity, exact source SHA, version/tag relationship, release context, Setup/update assets и SHA-256 binding преди feed promotion.

Публикуваните release bytes се третират като immutable. Поправка на 3.2.0 трябва да бъде нова версия, а не тихо заменен `v3.2.0` asset.

## Licensing, privacy, security и support

ArsExam е **proprietary software**. Официалните binaries се използват съгласно EULA. Third-party компонентите запазват собствените си лицензи.

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
- `pgnev/arsexam-desktop` — legacy compatibility repository, не независим release authority.

## Publication rule

Release asset, tag или manifest е официален само когато е публикуван чрез контролирания ArsExam release процес и съответният channel manifest е умишлено promoted.
