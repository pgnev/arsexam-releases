# ArsExam — Official Releases & Updates

Това repository е **официалният публичен канал за дистрибуция и обновяване** на ArsExam Desktop. Изходният код не се публикува тук.

**Автор и разработчик:** Petko Ganev  
**Поддръжка:** petkoganev@gmail.com  
**Copyright © 2026 Petko Ganev. All rights reserved.**

## Текущ официален статус

| Канал | Версия | Статус |
|---|---:|---|
| **Stable** | **3.7.1** | **CURRENT STABLE — публикуван на 05.09.2026** |
| Previous Stable | 3.6.3 | immutable historical release |
| Test feed | отделен prerelease/testing channel | authoritative: `update/test-manifest.json` |

Авторитетни за инсталираните update канали са `update/stable-manifest.json` и `update/test-manifest.json`.

## ArsExam 3.7.1 Stable

Official release: `v3.7.1`

Основни assets:

- `ArsExam_Setup_3.7.1_win-x64.exe`
- `ArsExam_Update_3.7.1_win-x64.zip`
- `update-manifest.json`

Stable feed `update/stable-manifest.json` е промотиран до **3.7.1**.

### SHA-256

- Setup: `EA3E7CB9D9D24D910A183412A9124015CE92A005FFC4FBDEE3B3018E952856F3`
- Update ZIP: `64B151B2514635C718D72CB6C9ECDD318F6EF1FED539BD72BF3F09F34ABA26B2`

### Release binding

- canonical source repository: `pgnev/arsexam-source`;
- immutable source tag: `v3.7.1`;
- exact tagged source SHA: `7eed9fafbe89cc399f0980856632dfc11637cc88`;
- validated source tree SHA: `882779e4c1b27999547c085b411020a8b0b9e5ad`;
- source merge commit on `main`: `adff78b8d0190a59b42330ecd709a76547dc8da7`;
- exact-tag local release gate: **PASS** — 735/735 tests, 7/7 updater matrix;
- exact-tag Windows/Sentry acceptance: **PASS**;
- hosted exact-tag Actions attempt failed at startup before jobs; the documented exact-tag local fallback was used under release policy.

## Какво включва 3.7.1

3.7.1 е Stable finalization release върху валидирания, но непубликуван 3.7.0 scope. Основният user-facing функционален акцент е checkbox multi-select търсене в банките на Модули 1–3:

- OR вътре в един categorical filter и AND между различни filters;
- Module 1 cumulative properties и master state `Всички свойства`;
- contextual Module 1 themes спрямо union-а на избраните сектори;
- multi-select Difficulty/Status/Discipline/Profile/Topic filters според модула;
- безопасно spacing/layout поведение около `Изчисти`;
- Module 3 new-topic creation изисква точно един selected profile.

3.7.1 също финализира release/documentation consistency: Privacy и Third-party surfaces показват реалната installed version, Setup инсталира само curated end-user documentation, а upgrade cleanup премахва само известни ArsExam source-only документи и запазва чужди/потребителски файлове.

Desktop и Portable използват един и същ валидиран application payload; различават се по deployment/persistent-data режима.

## Code signing

**ArsExam 3.7.1 Stable е публикуван без Authenticode подпис.** Windows може да покаже SmartScreen/Unknown Publisher предупреждение според локалната policy/reputation state. Изтегляйте само от официалния release и проверявайте SHA-256 binding-а от manifest-а.

HTTPS + SHA-256 са transport/integrity controls; те не са Authenticode publisher-identity signing.

## Update behavior

ArsExam е offline-first и проверява за обновления само когато update channel-ът е разрешен и има мрежова свързаност. Update пакетите се приемат само след SHA-256 проверка срещу authoritative manifest.

При временен DNS/transport проблем текущата инсталация трябва да остане работеща и persistent user data да не се променят. Официалният fallback е текущият `ArsExam_Setup_<version>_win-x64.exe` от този repository.

## Privacy и diagnostics

Основните банки, генератори, Recycler, Backup/Restore и Desktop/Portable data workflows работят локално. Crash/error диагностиката е **opt-in** и е изключена по подразбиране. ArsExam не изпраща usage/behavior analytics за използвани екрани, банки или workflow states.

Password recovery е локално чрез Recovery Key; няма universal server-side master password/backdoor.

Подробният текущ contract е в `PRIVACY_POLICY_BG.md`.

## Repository роли

- `pgnev/arsexam-releases` — **единствен официален публичен distribution/update authority**;
- `pgnev/arsexam-source` — private canonical source/development repository;
- `pgnev/arsexam-desktop` — legacy compatibility/history repository и не е current release authority;
- `pgnev/arsexam` — исторически web repository, не текущ Desktop authority.

## Operational check

На ArsExam 3.6.3 Stable → „Провери за обновление“ трябва да предложи **3.7.1**, ако Stable update channel-ът е разрешен и мрежата е достъпна. При временен network отказ приложението трябва да остане на текущата работеща версия без промяна на persistent data.
