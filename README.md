# ArsExam Desktop — официални версии, изтегляне и описание на програмата

**ArsExam Desktop** е native Windows, offline-first система за управление на дигитални ресурси, свързани с Държавния зрелостен изпит по Теория на професията **„Музикално изкуство“**.

Това repository — **`pgnev/arsexam-releases`** — е единственият официален публичен канал за:

- ArsExam Setup файлове;
- application update пакети;
- Stable/Test update manifests;
- immutable public release assets;
- публични release notes и integrity информация.

Изходният код **не се публикува тук**.

**Автор и разработчик:** Petko Ganev  
**Поддръжка:** petkoganev@gmail.com  
**Copyright © 2026 Petko Ganev. All rights reserved.**

> [!IMPORTANT]
> Изтегляйте ArsExam само от официалните Releases в това repository. Не приемайте binary от друг repository, mirror, чат или произволен file-sharing източник като официална версия само защото носи ArsExam име или икона.

---

# 1. Какво е ArsExam

ArsExam е специализирано Desktop приложение за целия локален жизнен цикъл на изпитното съдържание:

```mermaid
flowchart LR
    A[Нови или исторически материали] --> B[Recycler / Import]
    B --> C[Преглед и структуриране]
    C --> D[Workflow / Approval]
    D --> E[Официални банки]
    E --> F[Generator eligibility]
    F --> G[Генератори]
    G --> H[Генерирани варианти]
    H --> I[Word / Excel / Export]

    E --> J[Protected Backup]
    J --> K[Restore / Recovery]
```

Програмата е създадена така, че автоматизацията да подпомага експерта, но да не замества човешката преценка с догадка. Когато key, Media, provenance или структура са нееднозначни, съдържанието остава за преглед вместо да бъде автоматично „поправено“ по несигурен начин.

---

# 2. За кого е предназначена

ArsExam е предназначена за преподаватели, експерти, автори и редактори, които:

- поддържат изпитни банки;
- редактират въпроси и задачи;
- анализират исторически изпитни материали;
- изграждат и проверяват изпитни варианти;
- работят с нотни примери, изображения и аудио;
- трябва да пазят работните данни локално и да разполагат с надежден Backup/Restore механизъм.

---

# 3. Основни функции

## 3.1. Банки за трите изпитни модула

ArsExam поддържа структурирано съдържание за:

- **Модул 1** — въпроси с отговори, теми, сектори, свойства, Media, difficulty и generator rules;
- **Модул 2.1** — комплексни задачи с главни въпроси/подвъпроси, точки, key и приложими Media;
- **Модул 2.2** — отворени/практически задачи, включително Теория, Хармония и Музикални форми / анализ;
- **Модул 3** — теми, профили, номер на тема и workflow/generator state.

## 3.2. Workflow

Потребителските работни статуси са:

1. **Чернова**;
2. **За преглед**;
3. **За одобрение**;
4. **Одобрен**;
5. **Отхвърлен**;
6. **Архивиран**.

Важно: **„Одобрен“ не означава автоматично „Допустим за генератор“**. Generator eligibility се проверява отделно чрез модулните structural правила.

## 3.3. Генератори

### Модул 1

Генераторът създава точно **30 въпроса**:

| Група | Брой |
|---|---:|
| Слухови | 4 |
| Теория | 6 |
| Хармония | 7 |
| Музикални форми / анализ | 6 |
| История на музиката | 7 |
| **Общо** | **30** |

Прилагат се candidate availability, topic/structure правила, shuffle на въпросите и независимо shuffle на отговорите с запазване на верния answer mapping.

### Модул 2

Генераторите използват само structurally valid, approved и generator-eligible задачи и прилагат необходимия точков/структурен contract.

### Модул 3

Използва profile/topic generator workflow и отделни правила от числовата difficulty методология на Модул 1/2.

## 3.4. Multi-select търсене

Банките използват checkbox multi-select филтри:

- OR вътре в един categorical filter;
- AND между различни filters;
- contextual Module 1 themes;
- cumulative Module 1 properties;
- Difficulty/Status/Discipline/Profile/Topic filters според модула.

## 3.5. Difficulty methodology

ArsExam поддържа versioned difficulty methodologies, automatic explainable assessment и отделен expert override.

Модул 1/2 generator difficulty choices са concrete bands:

- **Лесно**;
- **Средно**;
- **Трудно**.

## 3.6. Recycler

Recycler обработва исторически и нови source материали и ги превръща в reviewable structured content.

Поддържаният модел включва:

- цели изпитни документи;
- смесени документи;
- самостоятелни tasks/fragments;
- key/criteria fragments;
- нотни/графични материали;
- audio;
- local OCR/layout extraction при приложимите източници.

Критичен принцип е **no silent drop**: неразпознат или нееднозначен материал трябва да остане видим чрез review state/evidence/outcome, а не да изчезне.

## 3.7. Import / Approval

Външното съдържание преминава през staging, validation, review и explicit workflow решение преди да стане official bank content.

Manual Media/association действие не auto-approve-ва съдържанието и не включва generator eligibility автоматично.

## 3.8. Media

ArsExam работи с локални:

- изображения;
- notation/score материали;
- аудио.

Missing/conflicting/ambiguous Media остава review-gated.

## 3.9. Word и Excel

- DOCX output се създава чрез Open XML;
- XLSX import/export използва ClosedXML;
- Microsoft Word/Excel не са runtime requirement за самото генериране/обработване на файловете.

## 3.10. Bank Quality

Инструментите за качество могат да подпомагат откриване и контролирана обработка на:

- duplicates;
- key conflicts;
- structural defects;
- missing Media;
- archive/merge/remove решения.

Destructive operations използват приложим preview/confirmation/audit/Safety Backup contract.

---

# 4. Offline-first работа

Основните функции работят локално и не изискват постоянен internet:

- локален профил и вход;
- банки;
- генератори;
- Recycler;
- Import/Approval;
- Word/Excel;
- Backup/Restore;
- Desktop/Portable data workflows.

Интернет се използва за:

1. официална проверка/изтегляне на update;
2. доброволна opt-in crash/error диагностика, когато е включена.

Няма задължителен cloud account за normal bank/generator workflow.

---

# 5. Desktop и Portable

## Desktop

Desktop installation държи versioned application binaries отделно от persistent user data.

## Portable

Portable режимът позволява пренасяне на приложението и неговия portable data root между поддържани Windows x64 компютри.

Типичните persistent категории включват:

- `Data`;
- `Media`;
- `Import`;
- `Export`;
- `Backup`;
- `Templates`;
- `Documentation`.

> [!CAUTION]
> Portable storage не означава автоматично, че всеки Media файл е индивидуално криптиран. При чувствителен removable носител използвайте подходяща OS/storage защита.

---

# 6. Локална сигурност

ArsExam използва локален защитен профилен/storage модел.

Основни принципи:

- plaintext profile password не се съхранява;
- profile password не е директно database encryption key;
- local security envelope/master-key state отделя authentication от data encryption;
- няма universal server-side master password/backdoor.

## Recovery Key

Recovery Key е локален single-use forgotten-password credential.

Той:

- не съдържа паролата;
- не е Backup password;
- не е transfer code;
- след успешно recovery се инвалидира и се издава нов.

---

# 7. Backup и Restore

ArsExam използва защитен `.arsexam-backup` формат.

Backup credential е отделен от profile password и Recovery Key.

```mermaid
flowchart LR
    A[Manual Backup] --> B[Authenticated protected package]
    B --> C{Restore}
    C -- Replace --> D[Safety Backup -> Replace]
    C -- Merge --> E[Safety Backup -> Conservative Merge]
    D --> F[Validation]
    E --> F
    F -- Failure --> G[Rollback attempt]
    F -- Success --> H[Completed]
```

### Replace

Заменя приложимото work state след validation и Safety Backup.

### Merge

Добавя допустимото incoming content консервативно, като пази current target state за съществуващи записи и блокира конфликтни methodology/file definitions преди mutation.

---

# 8. Актуализации

ArsExam използва официалните manifests в това repository.

```mermaid
flowchart LR
    A[Official manifest] --> B[HTTPS download]
    B --> C[Version + channel + SHA-256 validation]
    C --> D[Versioned deployment / Setup]
    D --> E[Launcher health check]
    E -- PASS --> F[Нова active версия]
    E -- FAIL --> G[Rollback към healthy версия]
```

Потребителските `Data/Media/Import/Export/Backup` не са normal application update payload.

Подробно описание: [`update/README.md`](update/README.md).

---

# 9. Privacy и diagnostics

Crash/error diagnostics са:

- OFF по подразбиране;
- opt-in;
- без usage/behavior analytics;
- ограничени до минимизиран technical payload според consent contract-а.

Основните банки, генератори, Recycler и Backup/Restore не изискват remote diagnostics.

---

# 10. Системни изисквания

Официалната native Desktop линия е предназначена за:

- Windows 10 / Windows 11;
- x64 архитектура.

Self-contained distribution не изисква предварително инсталиран .NET Runtime.

Няма runtime зависимост от Python, Node.js, npm, Microsoft Access, browser или localhost server.

---

# 11. Текущ официален статус

| Канал | Версия | Статус |
|---|---:|---|
| **Stable** | **3.9.1** | **CURRENT STABLE — публикуван на 12.09.2026; authority: `update/stable-manifest.json` + официалния `v3.9.1` release** |
| Previous Stable | 3.9.0 | immutable historical release |
| Withdrawn | 3.8.0 | **WITHDRAWN / DO NOT INSTALL — production startup health acceptance failed; assets се пазят само за audit/history** |
| Test | 3.9.0-rc.2 | текущият `update/test-manifest.json`; prerelease/testing channel, не е Stable |

Machine-readable update authority са:

- `update/stable-manifest.json`;
- `update/test-manifest.json`.

`3.8.2`, `3.8.1` и `3.7.1` остават по-ранни исторически Stable releases. Публичният current Stable статус не се определя от README самостоятелно, а от съгласуването на Stable manifest, latest non-draft/non-prerelease release и immutable source identity.

---

## ArsExam 3.9.1 — CURRENT STABLE

Официален release: **`v3.9.1`**  
Публикуван: **12.09.2026, 19:30:36 UTC**

Основни assets:

- `ArsExam_Setup_3.9.1_win-x64.exe`;
- `ArsExam_Update_3.9.1_win-x64.zip`.

### SHA-256

- Setup: `634A702F0AB6C7FB010F3D55C15D542ABC490CB2C863B153B51BEC68DE14B1D8`
- Update ZIP: `94F413E8E6BC1E60A9D5413907F7E1F361F735C98CF3C514B5222A933CBE30E9`

### Source/release binding

- canonical source: `pgnev/arsexam-source`;
- immutable source tag: `v3.9.1`;
- exact tagged source commit: `6ba036ae5faf8bdd0aa06bb45e9dd405e48b7629`;
- exact source tree: `a8216aa68c07b8f75c8723a5cca07b92ee382a44`;
- exact-tag Windows qualification: PASS;
- full regression and Module 1 solver stress: included in Stable qualification;
- WPF validation: **84/84 PASS**;
- Stable manifest / public release / asset SHA-256 reconciliation: PASS;
- Authenticode signing: **NO — intentionally unsigned**.

---

## ArsExam 3.8.0 — WITHDRAWN

Официалният release `v3.8.0` се пази immutable за audit/history, но **не е текущ Stable и не трябва да бъде инсталиран или използван като update target**.

> [!CAUTION]
> При реална Windows startup acceptance версия 3.8.0 не създаде изисквания launcher health acknowledgement в допустимия прозорец. ArsExam Launcher правилно задейства automatic rollback към предишната healthy версия и възстанови резервното копие на данните. Историческият failure остава част от release provenance; текущият Stable authority вече е **3.9.1**.

Исторически assets:

- `ArsExam_Setup_3.8.0_win-x64.exe`;
- `ArsExam_Update_3.8.0_win-x64.zip`;
- `update-manifest.json`.

### SHA-256

- Setup: `116AE12099572FDE26D4E406043E7316355A7B787F0945A23D18A5401C211380`
- Update ZIP: `2DC6DA5F12861CC4874EE40EA92F856B1FDCD40672D9F1D2902949DA28696C4F`

### Source/release binding

- canonical source: `pgnev/arsexam-source`;
- immutable source tag: `v3.8.0`;
- tagged source SHA: `01edd1aaa88a6ce650a5250d73e5479356b783ac`;
- validated Stable candidate SHA: `6e2891987479edd81ee7133f2e5c426bbdb10ae5`;
- regression suite: **746 passed / 0 failed / 0 skipped**;
- update stage/verify: **PASS**;
- production startup health acceptance: **FAIL — automatic rollback observed on Windows**.

---

# 12. ArsExam 3.9.0 — Previous Stable

Официален historical release: **`v3.9.0`**

Основни assets:

- `ArsExam_Setup_3.9.0_win-x64.exe`;
- `ArsExam_Update_3.9.0_win-x64.zip`.

## SHA-256

- Setup: `DF77E7B1729A57C07E8E9D0A3996E7FB3D772199E4BD3047602760593EC75A58`
- Update ZIP: `ACE473F3819A7E5CF9F58A8EE6A9882AC62CADDA2FDFE7BA54D257C0AE823F28`

## Source/release binding

- canonical source: `pgnev/arsexam-source`;
- immutable source tag: `v3.9.0`;
- exact tagged source commit: `ecbfba285593d4b72c20e5f2c04643f5c51d16d4`;
- exact source tree: `426c850725aea10ab9f72e1fc61fa3f6d7daab61`;
- Authenticode signing: **NO**.

3.9.0 остава immutable historical release evidence и не е current Stable след публикуването на 3.9.1.

---

# 13. Какво включва 3.9.1

ArsExam 3.9.1 е bounded maintenance update върху 3.9.0. Той запазва установеното exam/data поведение и добавя:

- завършен user-safe error handling contract;
- по-ясни и безопасни error/reference съобщения без изтичане на чувствителни exception details;
- release-pipeline reliability hardening за owner-local qualification/publication;
- exact-tag квалификация, пълна updater/rollback matrix и повторна manual acceptance върху публикуваните bytes.

Всички публикувани 3.9.1 binaries са обвързани с immutable `v3.9.1` source tag и authoritative SHA-256 стойности.

---

# 14. Code signing — важно за Windows предупрежденията

**ArsExam 3.9.1 Stable е публикуван без Authenticode подпис.**

Поради това Windows/SmartScreen може да покаже предупреждение като **Unknown Publisher**, в зависимост от локалната policy и reputation state.

Това трябва да се различава от integrity проверката:

- HTTPS защитава transport path-а;
- SHA-256 позволява сравнение с authoritative release hash;
- Authenticode удостоверява publisher identity чрез code-signing certificate.

За 3.9.1 третият механизъм не е наличен. Signing state винаги е release-specific и не трябва да се предполага за бъдещи версии.

---

# 15. Как да изтеглите безопасно

1. Отворете официалната секция **Releases** на `pgnev/arsexam-releases`.
2. Използвайте версията, посочена в `update/stable-manifest.json` като текущ Stable.
3. За нормална инсталация използвайте съответния `ArsExam_Setup_<version>_win-x64.exe`.
4. При необходимост сравнете SHA-256 с публикуваните authoritative данни.
5. Не инсталирайте release, който е маркиран като Withdrawn, дори assets да са запазени за audit/history.
6. Не заменяйте ръчно persistent `Data`/`Backup` директории с файлове от непознат source.

За проверка на SHA-256 на текущия Stable в PowerShell:

```powershell
Get-FileHash .\ArsExam_Setup_3.9.1_win-x64.exe -Algorithm SHA256
```

Очакван SHA-256 за официалния 3.9.1 Setup:

```text
634A702F0AB6C7FB010F3D55C15D542ABC490CB2C863B153B51BEC68DE14B1D8
```

---

# 16. Какво да направите при update/network проблем

При временен network failure:

- текущата working installation трябва да остане работеща;
- persistent user data не трябва да се променят;
- може да повторите update check по-късно;
- официалният fallback е Setup asset-ът от текущия Stable release в това repository.

Не изтривайте ръчно локалните банки или Backup файлове само защото update check е неуспешен.

---

# 17. Repository роли

- **`pgnev/arsexam-releases`** — единствен официален публичен binary/update authority;
- `pgnev/arsexam-source` — private canonical source/development repository;
- legacy/historical repositories не са текущият Desktop release authority.

Публикуваните release assets са immutable по release policy. Ако след публикация бъде открит дефект, корекцията трябва да бъде публикувана с **нова версия**, а не чрез тиха подмяна на стария binary.

---

# 18. Поддръжка

За техническа поддръжка:

**petkoganev@gmail.com**

Не изпращайте по email:

- profile password;
- Recovery Key;
- Backup password;
- transfer code;
- цели databases или ненужни изпитни/лични данни.

Споделяйте само минималната информация, необходима за диагностика.

---

# 19. Най-важното накратко

> **ArsExam Desktop е локална професионална система за изпитни банки, Recycler/Import, approval workflow, генератори, Word/Excel обмен и защитено Backup/Restore. Това repository е единственият официален публичен източник за неговите binaries и update manifests. Текущият Stable е ArsExam 3.9.1.**

## Граница на съдържанието

Софтуерът ArsExam не съдържа, не разпространява и не предоставя достъп до служебно, поверително или защитено съдържание, свързано с ДЗИ по Теория на професията „Музикално изкуство“. Програмата представлява единствено софтуерен инструмент за създаване, редактиране, организиране и управление на съдържание, въведено или създадено от надлежно оторизирани потребители.

Публично разпространяваният изпълним софтуер не включва база данни с реални служебни изпитни материали, задачи, отговори или други защитени данни.
