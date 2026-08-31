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
| **Stable** | **3.5.1** | **CURRENT STABLE — публикуван на 31.08.2026** |
| Previous Stable | 3.5.0 | immutable historical release |
| Test feed | 3.2.0 | отделен prerelease/testing channel |

Авторитетни за инсталираните update канали са `update/stable-manifest.json` и `update/test-manifest.json`.

## ArsExam 3.5.1 Stable

Official release: `v3.5.1`

Основни assets:

- `ArsExam_Setup_3.5.1_win-x64.exe`
- `ArsExam_Update_3.5.1_win-x64.zip`
- `update-manifest.json`

Stable feed е `update/stable-manifest.json` на branch `main` и е промотиран до **3.5.1** с `requiresInstaller=true`.

### Какво се променя в 3.5.1

- по-пълно управление на versioned difficulty methodologies — създаване, версиране, редактиране, защитено transactional multi-delete и K/C/S/L/D легенда;
- независимо разгъване на top-level sidebar секциите;
- по-компактен и потребителски ориентиран Module 1 bank/generator UX;
- четими DataGrid headers/widths в Module 1 и Import;
- Module 2.1 Recycler: dedicated official answer key има приоритет над по-нискоавторитетни embedded/director варианти и общият `Ключ / критерий` се изгражда четимо;
- Module 2.2 Recycler: task-local PDF visual recovery за Theory/Harmony, включително bare task-number anchors и review-gated crop fallback;
- updater cleanup: ArsExam 3.5.1 използва manifest-и само от `pgnev/arsexam-releases`; legacy runtime fallback към `pgnev/arsexam-desktop` е премахнат.

## Release integrity — ArsExam 3.5.1

Canonical source release binding:

- source repository: `pgnev/arsexam-source`;
- tag: `v3.5.1`;
- source SHA: `9346397b12aef3a38543e9503d3827a27fa5f481`;
- exact-tag Windows Release #953: **SUCCESS**;
- fresh exact-tag Upgrade Matrix #423: **SUCCESS**;
- Stable Release Orchestrator #6: **SUCCESS**.

### SHA-256 — ArsExam 3.5.1

- Setup: `AB7C6D54C642FA317C69800E2A634E86EBA5E2B61BBFB713E3BB016E15E5AA80`
- Update ZIP: `A547D49109C0E74B7B0F888D0DAD583F0197D2A9ABB85EA98F8F1238FF067FF7`

Проверявайте актуалния `stable-manifest.json` и release assets като authoritative source за download URLs и hashes.

## Code signing

**ArsExam 3.5.1 Stable е публикуван без Authenticode подпис.**

Windows може да покаже SmartScreen/Unknown Publisher предупреждение според локалната policy/reputation state. Изтегляйте само от официалния `pgnev/arsexam-releases` release и използвайте SHA-256 binding-а от manifest-а.

HTTPS + SHA-256 са transport/integrity controls; те не са Authenticode publisher-identity signing.

## Update behavior

ArsExam 3.5.1 е full-Setup release (`requiresInstaller=true`). Инсталиран ArsExam 3.5.0 на Stable channel трябва да открие 3.5.1 и да премине по поддържания installer/update path, като persistent user data остане непокътнат.

Ако automatic update UX не завърши успешно, официалният fallback за потребителя е директно изтегляне и стартиране на `ArsExam_Setup_3.5.1_win-x64.exe` от release `v3.5.1`.

## ArsExam 3.5.0

3.5.0 остава предишен immutable Stable. Неговите assets и tag не се заменят или променят.

Final source/tag binding:

- tag `v3.5.0`;
- source SHA `6adc5a17f79f2396ca9eb4c5aa855d0c8841aa17`;
- exact-tag Windows Release #916 — SUCCESS;
- 602 passed / 0 failed / 0 skipped;
- Public Distribution #511 — SUCCESS.

## Privacy и diagnostics

ArsExam е **offline-first**. Основните банки, генератори, Recycler, Backup/Restore и Desktop/Portable data workflows работят локално.

Crash/error диагностиката е **opt-in** и е изключена по подразбиране. ArsExam не изпраща usage/behavior analytics за използвани екрани, банки или workflow states.

Password recovery е локално чрез Recovery Key; ArsExam 3.5.x не използва server-side master password/backdoor.

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
- `pgnev/arsexam-source` — private canonical source/development repository; съдържа metadata-only release marker за текущия Stable;
- `pgnev/arsexam-desktop` — retired legacy repository; ArsExam 3.5.1 няма runtime/update fallback към него;
- `pgnev/arsexam` — исторически web repository, не текущ Desktop authority.

## Следващ operational check

След release 3.5.1 остава реалният Windows rollout test: upgrade от инсталиран 3.5.0 до Stable 3.5.1 и проверка, че persistent data и засегнатите Module 1 / Import / M2.1 / M2.2 сценарии са коректни.

След успешен реален rollout и при липса на legacy потребители retired `pgnev/arsexam-desktop` може да бъде окончателно премахнат.
