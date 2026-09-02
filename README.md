# ArsExam — Official Releases & Updates

Това repository е **официалният публичен канал за дистрибуция и обновяване** на ArsExam Desktop. Изходният код не се публикува тук.

**Автор и разработчик:** Petko Ganev  
**Поддръжка:** petkoganev@gmail.com  
**Copyright © 2026 Petko Ganev. All rights reserved.**

## Текущ официален статус

| Канал | Версия | Статус |
|---|---:|---|
| **Stable** | **3.6.3** | **CURRENT STABLE — публикуван на 03.09.2026** |
| Previous Stable | 3.6.2 | immutable historical release |
| Test feed | отделен prerelease/testing channel | authoritative: `update/test-manifest.json` |

Авторитетни за инсталираните update канали са `update/stable-manifest.json` и `update/test-manifest.json`.

## ArsExam 3.6.3 Stable

Official release: `v3.6.3`

Основни assets:

- `ArsExam_Setup_3.6.3_win-x64.exe`
- `ArsExam_Update_3.6.3_win-x64.zip`
- `update-manifest.json`

Stable feed `update/stable-manifest.json` е промотиран до **3.6.3**.

### SHA-256

- Setup: `8C611D1A32A0835D3DCC07F3F327E874871F948D3D2C74A7C02C24030B5509DB`
- Update ZIP: `3BA2E518D63F648C46E23658765041BD320365767D4637A523171246AAFCCA49`

### Release binding

- canonical source repository: `pgnev/arsexam-source`;
- immutable source tag: `v3.6.3`;
- source/merge SHA: `ff852752ea802ae9e72046b9bd76d40a87a0a179`;
- validated source tree SHA: `b7735f3284a3980ff781737ce7496e483368b159`;
- exact-tag Upgrade Matrix #555: **SUCCESS**;
- exact-tag Windows Release #1196: **SUCCESS**;
- Public Distribution #793: **SUCCESS**.

## Какво включва 3.6.3

3.6.3 е corrective hardening release върху 3.6.2. Включва по-устойчив updater с bounded retry/fallback и задължителна SHA-256 проверка, fail-closed обработка на повредени security envelope данни, diagnostics consent 4.0 с ограничен store-and-forward cache, локален Launcher incident bridge, по-безопасни user-facing technical errors и release-time protection на реалния single-file payload преди bundling.

Desktop и Portable използват един и същ валидиран application payload; различават се по deployment/persistent-data режима.

## Code signing

**ArsExam 3.6.3 Stable е публикуван без Authenticode подпис.** Windows може да покаже SmartScreen/Unknown Publisher предупреждение според локалната policy/reputation state. Изтегляйте само от официалния release и проверявайте SHA-256 binding-а от manifest-а.

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

На ArsExam 3.6.2 Stable → „Провери за обновление“ трябва да предложи **3.6.3**, ако Stable update channel-ът е разрешен и мрежата е достъпна. При временен network отказ приложението трябва да остане на текущата работеща версия без промяна на persistent data.
