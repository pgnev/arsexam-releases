# ArsExam — Official Releases & Updates

Това repository е **официалният публичен канал за дистрибуция и обновяване** на ArsExam Desktop.

**ArsExam** е Windows настолен софтуер за управление на дигитални ресурси, свързани с Държавен зрелостен изпит по Теория на професията **„Музикално изкуство“**.

**Автор и разработчик:** Petko Ganev  
**Поддръжка:** petkoganev@gmail.com  
**Copyright © 2026 Petko Ganev. All rights reserved.**

> Тук се публикуват официалните Windows binaries, update packages, manifests и публични правни/security notices. Това **не е** source-code repository и публичната му видимост не предоставя open-source лиценз върху оригиналния ArsExam код.

## Текущ официален статус

| Линия | Версия | Статус |
|---|---:|---|
| **Stable** | **3.5.0** | текущото официално Stable издание, публикувано на 31.08.2026 |
| **Development candidate** | **3.5.1** | **NOT RELEASED** — активен private-source acceptance candidate; няма публикувани 3.5.1 binaries/tag/feed |
| **Test feed** | **3.2.0** | няма активен 3.5.1 prerelease; manifest-ът не се променя само заради development branch |

Авторитетни за инсталираните update канали са `update/stable-manifest.json` и `update/test-manifest.json`.

Branch, PR, CI build или private candidate не е официален release. Публикуваните Stable assets не се подменят тихо; корекция се публикува с нов version/tag след отделно приемане.

## ArsExam 3.5.1 — development / acceptance candidate

**3.5.1 все още не е публичен release.** Тази секция описва текущата разработвана patch линия, за да няма разминаване между public distribution документацията и canonical source roadmap-а.

Текущият 3.5.1 candidate е maintenance/UX/Recycler correctness patch върху 3.5.0 и включва:

- по-пълно управление на versioned difficulty methodologies — създаване, версиране, редактиране, защитено multi-delete и K/C/S/L/D легенда;
- независимо разгъване на top-level sidebar секциите;
- по-компактен и потребителски ориентиран Module 1 bank/generator UX;
- DataGrid header hardening: кратките колони в Module 1 и Import използват гарантирани четими ширини, вместо да се смачкват/пренасят по средата на дума;
- Module 2.1 Recycler: dedicated official answer key има приоритет над по-нискоавторитетни embedded/director варианти; общият `Ключ / критерий` се изгражда четимо от разчетените подвъпроси;
- Module 2.2 Recycler: task-local PDF visual recovery за Theory/Harmony, включително bare task-number anchors и review-gated crop fallback, когато няма отделен embedded image/score region;
- updater cleanup: 3.5.1 използва само manifest-и от `pgnev/arsexam-releases`; legacy fallback към `pgnev/arsexam-desktop` е премахнат от candidate source.

Преди 3.5.1 да стане Stable са задължителни нов exact-head Windows build/test/Setup, upgrade matrix, реален преглед на засегнатите Recycler/UI сценарии и изрично owner разрешение за merge/tag/public release.

**Не са разрешени към този момент:** `v3.5.1` release, 3.5.1 binaries в този repository или Stable manifest promotion.

## ArsExam 3.5.0 Stable

ArsExam 3.5.0 въвежда работния модел за проследимо съдържание и generator eligibility, разширен Recycler/import review, versioned difficulty methodology, Bulgarian-first UX и schema-v8 Backup/Restore hardening.

### Workflow и generator eligibility

ArsExam 3.5 отделя **наличието на запис в работната банка** от **правото му да участва в генератор**.

Поддържаните workflow състояния са:

- Чернова;
- За преглед;
- Готов за одобрение;
- Одобрен;
- Изключен;
- Архивиран.

`generator_eligible` е отделно състояние. Само approved + otherwise eligible съдържание може да премине generator candidate gates за Module 1, Module 2 и Module 3.

### Recycler / import — без silent drop

Всеки анализиран/staged запис трябва да остане видим чрез workflow state или explicit final outcome.

3.5 включва:

- per-record import outcomes;
- staged workflow lifecycle;
- status/attention filters и provenance search;
- multi-select и bulk actions;
- source/key/media inspector;
- видими unassigned media candidates;
- explicit expert-only manual media assignment.

Manual media assignment не одобрява автоматично запис и не включва generator eligibility.

### Versioned difficulty methodology

Schema v8 включва versioned difficulty methodologies и content difficulty assessments.

Фабричната **ArsExam Standard 1.0** е защитена. Поддържат се user copies/versions, preview-before-apply recalculation и запазване на expert overrides и причините им.

### Backup / Restore / recovery compatibility

Data-only Backup snapshot v2 пази:

- bank content и generated tests;
- Module 1 composition/linked metadata;
- workflow state и generator eligibility;
- difficulty methodology versions;
- automatic/expert difficulty assessments и rationale.

Data-only Backup **не възстановява** стара profile password/hash, Recovery Key/security envelope, Backup Registry secret vault, diagnostics/update settings или import-history credentials.

Legacy snapshot v1 остава четим чрез compatibility reconstruction на липсващия schema-v8 companion state.

### Desktop и Portable

Официалният Setup предлага Desktop и Portable режим.

- Desktop използва versioned program payload и отделен persistent user-data root.
- Portable държи приложението и данните в избрания portable root и няма Windows uninstaller.
- Поддържаният updater пази persistent user data и използва versioned activation/health/rollback contract.

## Изтегляне на ArsExam 3.5.0

Официалният release е `v3.5.0` в този repository.

Основни assets:

- `ArsExam_Setup_3.5.0_win-x64.exe`
- `ArsExam_Update_3.5.0_win-x64.zip`
- `update-manifest.json`

Stable feed е `update/stable-manifest.json` на branch `main`.

## Release integrity — ArsExam 3.5.0

Официалният 3.5.0 release е произведен от private canonical source чрез контролирания release pipeline.

Final source/tag binding:

- source repository: `pgnev/arsexam-source`;
- tag: `v3.5.0`;
- source SHA: `6adc5a17f79f2396ca9eb4c5aa855d0c8841aa17`;
- exact-tag Windows Release #916: SUCCESS;
- test suite: **602 passed / 0 failed / 0 skipped**;
- Public Distribution #511: SUCCESS.

### SHA-256 — ArsExam 3.5.0

- Setup: `3992DF6F5281B83D14ED439FDBABC900C6FD682917146F38142341FC96649C00`
- Update ZIP: `E3718996792CF2616C4C59C4D8CCB719CD58EA58DA477EFC8E954E5F676CDF34`

Проверявайте актуалния `stable-manifest.json` и release assets като authoritative source за download URLs и hashes.

## Code signing

**ArsExam 3.5.0 Stable е публикуван без Authenticode подпис.**

Windows може да покаже SmartScreen/Unknown Publisher предупреждение според локалната policy/reputation state. Изтегляйте само от официалния `pgnev/arsexam-releases` release и използвайте SHA-256 binding-а от manifest-а.

HTTPS + SHA-256 са transport/integrity controls; те не са Authenticode publisher-identity signing.

Състоянието на подписването за бъдеща 3.5.1 се определя само от нейното собствено final exact-release evidence, ако версията бъде одобрена за публикуване.

## Privacy и diagnostics

ArsExam е **offline-first**. Основните банки, генератори, Recycler, Backup/Restore и Desktop/Portable data workflows работят локално.

Crash/error диагностиката е **opt-in** и е изключена по подразбиране. ArsExam не изпраща usage/behavior analytics за използвани екрани, банки или workflow states.

Password recovery е локално чрез Recovery Key; ArsExam 3.5.x не използва Supabase, recovery e-mail, Request ID или support-issued reset code за password recovery.

## Licensing, privacy, security и support

ArsExam е **proprietary software**. Официалните binaries се използват съгласно EULA. Third-party компонентите запазват собствените си лицензи и предоставените от тях права.

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

- `pgnev/arsexam-releases` — **единствен официален публичен distribution/update authority**;
- `pgnev/arsexam-source` — private canonical source/development repository;
- `pgnev/arsexam-desktop` — retired legacy compatibility repository; 3.5.1 candidate няма runtime update fallback към него и то може да бъде decommissioned след final dependency audit;
- `pgnev/arsexam` — исторически web repository, не текущ Desktop authority.

## Publication rule

Release asset, tag или manifest е официален само когато е публикуван чрез контролирания ArsExam release процес и съответният channel manifest е умишлено promoted. Development описание на 3.5.1 в този README **не е release и не променя Stable 3.5.0**.
