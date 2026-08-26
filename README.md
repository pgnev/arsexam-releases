# ArsExam — Official Releases & Updates

Това repository е **официалният публичен канал за дистрибуция и обновяване** на ArsExam Desktop.

**ArsExam** е Windows настолен софтуер за управление на дигитални ресурси, свързани с Държавен зрелостен изпит по Теория на професията **„Музикално изкуство“**.

**Автор и разработчик:** Petko Ganev  
**Поддръжка:** petkoganev@gmail.com  
**Copyright © 2026 Petko Ganev. All rights reserved.**

> Тук се публикуват само официални дистрибуционни материали. Това **не е** source-code repository и не предоставя open-source лиценз за оригиналния ArsExam код.

## Текущ официален статус

| Канал | Версия | Статус |
|---|---:|---|
| **Stable** | **3.1.1** | текущо публикувано официално Stable издание |
| **Test** | **3.1.0-rc.9** | исторически Test prerelease, към който все още сочи Test feed-ът |

Авторитетни за текущо публикуваните версии са:

- `update/stable-manifest.json`
- `update/test-manifest.json`

Branch, PR, CI build или private candidate не е официален release. Версия 3.1.1 е публикувана след exact-source validation, immutable `v3.1.1` release и умишлена Stable feed promotion чрез canonical public publisher.

## Инсталиране

Официалният ArsExam Setup поддържа **clean install**. Не е необходимо потребителят първо да инсталира 3.1.0, за да използва 3.1.1.

Единният Setup предлага:

- **Desktop** — per-user инсталация с отделни application и persistent-data папки;
- **Portable** — самостоятелна portable структура за папка/USB носител.

При upgrade **3.1.0 → 3.1.1** се използва пълният Setup, защото release-ът съдържа и Launcher/deployment-owned промени. Това е upgrade requirement, а не prerequisite за clean install.

## Какво носи ArsExam 3.1.1

Следните функции са част от **ArsExam 3.1.1 Stable**:

### Offline-first и локална сигурност

- основната работа с профил, банки, генератори, import/export, Backup/Restore и Desktop↔Portable Transfer остава локална;
- профилната парола не се записва plaintext и използва versioned salted PBKDF2-HMAC-SHA256 verification;
- 3.1.0 password hashes остават съвместими и могат да бъдат надградени след успешен login;
- основната SQLite база използва защитен SQLCipher-capable encrypted data path чрез local security envelope/key hierarchy;
- профилната парола не е директният database encryption key.

### Recovery Key

- забравена парола се възстановява локално чрез Recovery Key;
- няма Supabase recovery e-mail, Request ID или support-code backend;
- има един активен Recovery Key за профила;
- успешното password recovery обезсилва използвания ключ и генерира нов независим Recovery Key;
- authenticated replacement на Recovery Key изисква текущата профилна парола;
- Recovery Key не се пази като възстановимо plaintext копие от ArsExam.

### Protected Backup и Restore

- ръчните Backup-и използват защитен `.arsexam-backup` формат;
- всеки Backup има собствен AE-BK номер и собствена автоматично генерирана Backup парола;
- Backup password-ът е отделен от profile password и Recovery Key;
- encrypted Backup Registry пази metadata и owner credentials за собствените Backup-и;
- потребителските действия за показване/копиране/експортиране на Backup password изискват current-password step-up;
- Safety Backups защитават rollback преди рискови операции;
- normal data Restore не възстановява стар profile password/Recovery Key security state.

### Desktop ↔ Portable Transfer

3.1.1 добавя защитен Transfer между Desktop и Portable ArsExam, работещи на един и същ Windows компютър, като Portable е на свързан USB носител:

- Transfer ID + временен Transfer code;
- локална IPC/Named Pipes координация и USB presence/heartbeat;
- 30-минутен source-side session lifetime;
- bounded wrong-code attempts/cooldown;
- encrypted authenticated transfer package;
- full staging/validation преди active-data mutation;
- Safety Backup + rollback/recovery journal;
- финален SUCCESS/ACK преди приложението да покаже, че USB може да бъде изваден безопасно.

### Регистри

- Backup Registry;
- Transfer Registry без plaintext Transfer-code history;
- Import Registry с read-only operational history.

### UI корекции

- коригирано показване на текста „дигитални ресурси“ при Windows scaling;
- DPI/work-area handling за редакторите на Модул 2 — първа и втора част;
- preventive work-area coverage за редакторите на Модул 1 и Модул 3.

### Важна storage граница

Криптираната SQLite база **не означава**, че standalone файловете в `Media` са индивидуално криптирани при покой. За чувствителен removable storage използвайте и подходяща Windows/storage защита, например BitLocker/BitLocker To Go.

## Интернет функции

Core работата на ArsExam е offline-first. Интернет се използва само за ясно отделени функции според конкретната release версия:

- проверка/изтегляне на официални обновления от GitHub;
- opt-in crash/error диагностика чрез Sentry EU/DE, когато е активирана.

3.1.1 няма online password-recovery backend и няма usage/behavior analytics.

## Update канали

Stable:

```text
https://raw.githubusercontent.com/pgnev/arsexam-releases/main/update/stable-manifest.json
```

Test:

```text
https://raw.githubusercontent.com/pgnev/arsexam-releases/main/update/test-manifest.json
```

Stable и Test са отделни канали. Test е opt-in и не трябва тихо да подменя Stable policy.

Update trust не се основава само на URL: pipeline-ът валидира version/channel contract, HTTPS delivery, package shape, SHA-256 и applicable deployment requirements преди activation.

## Release integrity и provenance

Официалните публични releases се произвеждат от private canonical source чрез контролиран Windows validation/publisher pipeline.

Public publisher проверява:

- source workflow/run identity;
- exact source SHA;
- version/tag relationship;
- immutable release context;
- Setup/update assets;
- SHA-256 binding;
- anti-downgrade feed promotion.

Публикуваните release assets се третират като immutable. Корекция се публикува с нов version/tag, а не чрез тихо подменяне на съществуващи bytes.

## Code signing

Не се твърди Authenticode signing, освен когато exact release evidence действително го доказва. ArsExam 3.1.1 Stable е публикуван unsigned по действащата проектна policy.

За unsigned Stable използвайте само официалния release в `pgnev/arsexam-releases`; Setup/update hashes са обвързани с release manifest-а чрез SHA-256. HTTPS/SHA-256 осигуряват transport/integrity проверки, но не са равнозначни на Authenticode publisher identity.

## Repository purpose

Този repository е ограничен до публична release инфраструктура:

- Windows Setup и update packages;
- Stable/Test manifests;
- release notes/checksums;
- публични legal/privacy/support/security notices;
- compatibility metadata за поддържани ArsExam клиенти.

Тук не трябва да се публикуват source code, private development artifacts, credentials, signing material, diagnostic events или user/examination data.

## Licensing

ArsExam е **proprietary software**. Официалните binaries се използват съгласно ArsExam End User License Agreement (EULA).

Публичното GitHub repository не поставя ArsExam под MIT, GPL, Apache или друг open-source лиценз. Third-party компонентите запазват собствените си лицензи и notices.

Публични документи:

- `LICENSE.md`
- `COPYRIGHT.md`
- `EULA_BG.txt`
- `PRIVACY_POLICY_BG.md`
- `THIRD_PARTY_NOTICES.md`
- `SECURITY.md`
- `SUPPORT.md`

## Privacy

Нормална update проверка не качва в това repository въпросни банки, отговори, generated documents, Media, local databases, Recovery Keys, Backup passwords или Transfer codes.

Privacy behavior е version-specific. Публичната Privacy Policy и документите, включени в конкретен release, трябва да съответстват на реалното поведение на тази release версия.

## Security и support

Поддръжка: **petkoganev@gmail.com**.

Не изпращайте по e-mail profile passwords, Recovery Keys, Backup passwords, Transfer codes, цели бази данни или ненужно изпитно съдържание.

Security проблеми следва да се докладват частно; не публикувайте exploitable details в публичен GitHub issue. Вижте `SECURITY.md`.

## Repository роли

- `pgnev/arsexam-releases` — **официален публичен distribution/update authority**;
- `pgnev/arsexam-source` — private canonical source/development repository;
- `pgnev/arsexam-desktop` — legacy compatibility repository, не независим release authority.

## Publication rule

Release asset, tag или manifest е официален само когато е публикуван чрез контролирания ArsExam release процес и съответният channel manifest е умишлено promoted.
