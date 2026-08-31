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
| **Stable** | **3.5.0** | текущото официално Stable издание, публикувано на 31.08.2026 |
| **Test** | **3.2.0** | няма активен prerelease; Test manifest остава върху последната умишлено promoted версия |

Авторитетни за каналите са `update/stable-manifest.json` и `update/test-manifest.json`.

ArsExam 3.3.0 е предходният public Stable. Версия 3.4.0 не беше публикувана отделно; приетата ѝ функционалност е включена в 3.5.0.

Branch, PR, CI build или private candidate не е официален release. Публикуваните Stable assets не се подменят тихо; корекция се публикува с нов version/tag.

## ArsExam 3.5.0 Stable

ArsExam 3.5.0 въвежда новия работен модел за проследимо съдържание и generator eligibility, разширен Recycler/import review, versioned difficulty methodology, Bulgarian-first UX и schema-v8 Backup/Restore hardening.

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

Официалният release е:

`https://github.com/pgnev/arsexam-releases/releases/tag/v3.5.0`

Основни assets:

- `ArsExam_Setup_3.5.0_win-x64.exe`
- `ArsExam_Update_3.5.0_win-x64.zip`
- `update-manifest.json`

Stable feed:

`https://raw.githubusercontent.com/pgnev/arsexam-releases/main/update/stable-manifest.json`

## Release integrity

Официалният 3.5.0 release е произведен от private canonical source чрез контролирания release pipeline.

Final source/tag binding:

- source repository: `pgnev/arsexam-source`;
- tag: `v3.5.0`;
- source SHA: `6adc5a17f79f2396ca9eb4c5aa855d0c8841aa17`;
- exact-tag Windows Release #916: SUCCESS;
- test suite: **602 passed / 0 failed / 0 skipped**;
- Public Distribution #511: SUCCESS.

Публичният publisher проверява exact tag/source SHA, immutable release context, Setup/update assets и SHA-256 binding преди Stable feed promotion.

### SHA-256 — ArsExam 3.5.0

- Setup: `3992DF6F5281B83D14ED439FDBABC900C6FD682917146F38142341FC96649C00`
- Update ZIP: `E3718996792CF2616C4C59C4D8CCB719CD58EA58DA477EFC8E954E5F676CDF34`

Проверявайте актуалния `stable-manifest.json` и release assets като authoritative source за download URLs и hashes.

## Code signing

**ArsExam 3.5.0 Stable е публикуван без Authenticode подпис.**

Windows може да покаже SmartScreen/Unknown Publisher предупреждение според локалната policy/reputation state. Изтегляйте само от официалния `pgnev/arsexam-releases` release и използвайте SHA-256 binding-а от manifest-а.

HTTPS + SHA-256 са transport/integrity controls; те не са Authenticode publisher-identity signing.

## Privacy и diagnostics

ArsExam е **offline-first**. Основните банки, генератори, Recycler, Backup/Restore и Desktop/Portable data workflows работят локално.

Crash/error диагностиката е **opt-in** и е изключена по подразбиране. ArsExam не изпраща usage/behavior analytics за използвани екрани, банки или workflow states.

При включена remote diagnostics production ingest е ограничен до одобрения Sentry EU/DE host pattern `*.ingest.de.sentry.io` и изисква текущо съгласие.

Password recovery е локално чрез Recovery Key; ArsExam 3.5.0 не използва Supabase, recovery e-mail, Request ID или support-issued reset code за password recovery.

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

- `pgnev/arsexam-releases` — **официален публичен distribution/update authority**;
- `pgnev/arsexam-source` — private canonical source/development repository;
- `pgnev/arsexam-desktop` — legacy compatibility repository, не независим release authority;
- `pgnev/arsexam` — исторически web repository, не текущ Desktop authority.

## Publication rule

Release asset, tag или manifest е официален само когато е публикуван чрез контролирания ArsExam release процес и съответният channel manifest е умишлено promoted.
