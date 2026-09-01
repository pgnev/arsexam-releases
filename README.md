# ArsExam — Official Releases & Updates

Това repository е **официалният публичен канал за дистрибуция и обновяване** на ArsExam Desktop.

**ArsExam** е Windows настолен софтуер за управление на дигитални ресурси, свързани с Държавен зрелостен изпит по Теория на професията **„Музикално изкуство“**.

**Автор и разработчик:** Petko Ganev  
**Поддръжка:** petkoganev@gmail.com  
**Copyright © 2026 Petko Ganev. All rights reserved.**

> Тук се публикуват официалните Windows binaries, update packages, manifests и публични правни/security notices. Това **не е** source-code repository.

## Текущ официален статус

| Канал | Версия | Статус |
|---|---:|---|
| **Stable** | **3.5.2** | **CURRENT STABLE — публикуван на 01.09.2026** |
| Previous Stable | 3.5.1 | immutable historical release |
| Test feed | 3.2.0 | отделен prerelease/testing channel |

Авторитетни за инсталираните update канали са `update/stable-manifest.json` и `update/test-manifest.json`.

## ArsExam 3.5.2 Stable

Official release: `v3.5.2`

Основни assets:

- `ArsExam_Setup_3.5.2_win-x64.exe`
- `ArsExam_Update_3.5.2_win-x64.zip`
- `update-manifest.json`

Stable feed е `update/stable-manifest.json` на branch `main` и е промотиран до **3.5.2** с `requiresInstaller=true`.

### Какво се променя в 3.5.2

- Module 1 Recycler пази каноничното 30-въпросно секторно разпределение и блокира известните грешни semantic reroutes;
- тематично разпознаване покрива `Секвенции` и `Старинна сюита`;
- linked Harmony workflow е Leader-first, техническите group ID стойности са автоматични, а staged Leader selector-ът вижда текущия пакет;
- исторически Harmony групи с 3+ Followers се пазят цели, но са generator-ineligible вместо да се реже произволен subset;
- Module 2.1 възстановява fragmented official answer keys по source question number и fail-closed provenance;
- Module 2.2 забранява answer-key pages като task-media source и възстановява task-local Theory/Harmony нотни crop-ове от реалната изпитна страница;
- Module 1/Import DataGrid колоните имат четими начални ширини, но отново могат свободно да се стесняват/разширяват от потребителя;
- главният прозорец след login се отваря максимизиран.

## Release integrity — ArsExam 3.5.2

Canonical source binding:

- source repository: `pgnev/arsexam-source`;
- tag: `v3.5.2`;
- source SHA: `7514d16bf7b5bafac90bdfbf5bf55c365afe6a9e`;
- validated acceptance tree SHA: `f16f0f38a479473e34ce2628d3f081e4ad8f4dcd` — tree-identical release content;
- exact-tag Windows Release #1004: **SUCCESS**;
- fresh exact-tag Upgrade Matrix #472: **SUCCESS**;
- Stable Release Orchestrator #1: **SUCCESS**.

### SHA-256 — ArsExam 3.5.2

- Setup: `E0CFCB65CC7E36E61FAACB7C42D41CA8955ED21F1D573CA010ECE92A1DC62ED5`
- Update ZIP: `47045CF537555D43A7A7B410CE55ECF248DF5F26881602CF61F0E5ECB2E75E50`

Проверявайте актуалния `stable-manifest.json` и release assets като authoritative source за download URLs и hashes.

## Code signing

**ArsExam 3.5.2 Stable е публикуван без Authenticode подпис.** Windows може да покаже SmartScreen/Unknown Publisher предупреждение според локалната policy/reputation state. Изтегляйте само от официалния `pgnev/arsexam-releases` release и използвайте SHA-256 binding-а от manifest-а.

HTTPS + SHA-256 са transport/integrity controls; те не са Authenticode publisher-identity signing.

## Update behavior

ArsExam 3.5.2 е full-Setup release (`requiresInstaller=true`). Инсталиран ArsExam 3.5.1 на Stable channel трябва да открие 3.5.2 и да премине по поддържания installer/update path, като persistent user data остане непокътнат.

Ако automatic update UX не завърши успешно, официалният fallback е директно изтегляне и стартиране на `ArsExam_Setup_3.5.2_win-x64.exe` от release `v3.5.2`.

## Privacy и diagnostics

ArsExam е **offline-first**. Основните банки, генератори, Recycler, Backup/Restore и Desktop/Portable data workflows работят локално.

Crash/error диагностиката е **opt-in** и е изключена по подразбиране. ArsExam не изпраща usage/behavior analytics за използвани екрани, банки или workflow states.

Password recovery е локално чрез Recovery Key; ArsExam 3.5.x не използва server-side master password/backdoor.

## Repository роли

- `pgnev/arsexam-releases` — **единствен официален публичен distribution/update authority**;
- `pgnev/arsexam-source` — private canonical source/development repository; metadata-only source release markers;
- `pgnev/arsexam-desktop` — retired legacy repository; ArsExam 3.5.x няма runtime/update fallback към него;
- `pgnev/arsexam` — исторически web repository, не текущ Desktop authority.

## Текущ operational check

На реална машина с ArsExam 3.5.1: Stable → „Провери за обновление“ трябва да предложи **3.5.2**. След upgrade се проверяват persistent data, Module 1 classification, linked Harmony workflow, M2.1 answer keys, M2.2 notation visuals, DataGrid resize и maximized startup.
