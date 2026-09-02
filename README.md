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
| **Stable** | **3.6.2** | **CURRENT STABLE — публикуван на 02.09.2026** |
| Previous Stable | 3.6.1 | immutable historical release |
| Test feed | отделен prerelease/testing channel | authoritative: `update/test-manifest.json` |

Авторитетни за инсталираните update канали са `update/stable-manifest.json` и `update/test-manifest.json`.

## ArsExam 3.6.2 Stable

Official release: `v3.6.2`

Основни assets:

- `ArsExam_Setup_3.6.2_win-x64.exe`
- `ArsExam_Update_3.6.2_win-x64.zip`
- `update-manifest.json`

Stable feed е `update/stable-manifest.json` на branch `main` и е промотиран до **3.6.2**.

### Какво се променя в 3.6.2

- единен шестстепенен workflow vocabulary в банки, редактори, Import/Approval и Quick Preview;
- съвместимост за Rejected/Excluded към потребителския статус „Отхвърлен“;
- fail-closed generator eligibility и синхронизация на staged archive/outcome/batch;
- общ Generator Readiness diagnostics слой за Module 1, Module 2 и Module 3;
- контекстна помощ за K/C/S/L/D, активната методика, expert override и module-specific правила;
- difficulty диапазоните и labels се извеждат от активната методика вместо от hard-coded граници;
- permanent WPF snapshot matrix: 8 критични изгледа × 5 viewport/DPI сценария = 40 render проверки.

## Release integrity — ArsExam 3.6.2

Canonical source binding:

- source repository: `pgnev/arsexam-source`;
- tag: `v3.6.2`;
- source/merge SHA: `1b52a37a186535435160fa19a6c4f92199687e9c`;
- validated release tree SHA: `a96986932a527f72d0d0a54031588966081c3f5f`;
- exact-tag Windows Release #1117: **SUCCESS**;
- exact-tag Upgrade Matrix #540: **SUCCESS**;
- exact-tag UI Snapshots #73: **SUCCESS**;
- Public Distribution #711: **SUCCESS**.

### SHA-256 — ArsExam 3.6.2

- Setup: `A5D4A81500307059171E49624BAB061CBA281BFFF5CAA7E6C2E802BA90BF80A6`
- Update ZIP: `B8F46EC121D5BBA08627CCBBDDC124080EB20655887309F63E54B88B102DC051`

Проверявайте актуалния `stable-manifest.json` и release assets като authoritative source за download URLs и hashes.

## Code signing

**ArsExam 3.6.2 Stable е публикуван без Authenticode подпис.** Windows може да покаже SmartScreen/Unknown Publisher предупреждение според локалната policy/reputation state. Изтегляйте само от официалния `pgnev/arsexam-releases` release и използвайте SHA-256 binding-а от manifest-а.

HTTPS + SHA-256 са transport/integrity controls; те не са Authenticode publisher-identity signing.

За следващите версии се оценява publicly trusted code-signing механизъм (Microsoft Artifact Signing или публично доверен CA сертификат) с CI/CD интеграция. До вземане и прилагане на това решение текущата unsigned policy остава изрично описана.

## Update behavior

ArsExam е offline-first и проверява за обновления само когато update channel-ът е разрешен и има мрежова свързаност. Update пакетите се приемат само след SHA-256 проверка срещу authoritative manifest.

При временен DNS/transport проблем текущата инсталация трябва да остане работеща и потребителските данни не трябва да се променят. Официалният fallback при невъзможност за автоматично обновяване е директно изтегляне и стартиране на текущия `ArsExam_Setup_<version>_win-x64.exe` от официалния release.

## Privacy и diagnostics

ArsExam е **offline-first**. Основните банки, генератори, Recycler, Backup/Restore и Desktop/Portable data workflows работят локално.

Crash/error диагностиката е **opt-in** и е изключена по подразбиране. ArsExam не изпраща usage/behavior analytics за използвани екрани, банки или workflow states.

Password recovery е локално чрез Recovery Key; ArsExam не използва server-side master password/backdoor.

## Repository роли

- `pgnev/arsexam-releases` — **единствен официален публичен distribution/update authority**;
- `pgnev/arsexam-source` — private canonical source/development repository; metadata-only source release markers;
- `pgnev/arsexam-desktop` — retired legacy repository; не е current release authority и се пази само докато бъде решена legacy update compatibility policy;
- `pgnev/arsexam` — исторически web repository, не текущ Desktop authority.

## Operational check

На реална машина с ArsExam 3.6.1 Stable → „Провери за обновление“ трябва да предложи **3.6.2**. При временен DNS/transport отказ приложението трябва да остане на текущата работеща версия без промяна на persistent data; след възстановяване на мрежата проверката/изтеглянето може да бъде повторено.
