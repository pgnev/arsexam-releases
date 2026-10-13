# ArsExam 4.1.2 — release QA, 12 октомври 2026

## Обхват и provenance

Source repository: private pgnev/arsexam-source.
Immutable source tag: v4.1.2.
Exact source commit: 7b3710377fbce8288b1488877e6a28b7ed2c3999.
Промяна: поправена е невъзможността да се отвори прозорецът за поддръжка преди активация (PR #270), интегрирана за 4.1.2 чрез PR #271.

## Проверки на изходния код

- Node регресии: 312 успешно, 0 грешки. Допълнителният точен .NET Support/Consent набор премина 6/6.
- .NET регресия: 1577 успешно, 0 грешки, 2 условно пропуснати (изискват отделна квалификационна среда). Допълнително специалният тест за техническия лимит на генератора беше изпълнен отделно с `ARSEXAM_RUN_QUALIFICATION_STRESS=1`: 1/1 PASS. Остава един условен Worker/D1 тест без отделна среда. В предварителен прогон е отчетен един нестабилен timing тест; при повторението цялата регресия премина и отделното повторение беше успешно.
- Защитен Windows Release за exact source: 17 PASS врати до инсталатора. Първоначалният процес бе прекъснат по време на Inno Setup; компилацията на Setup бе повторена успешно и изходът проверен независимо. Полученият композитен отчет съдържа 19 проверки, като изрично обозначава прекъсването. Не се представя като един непрекъснат прогон.
- Updater/rollback матрица: 7 PASS сценария от release лога.

## Артефакти

| Файл | Размер | SHA-256 |
|---|---:|---|
| ArsExam_Setup_4.1.2_win-x64.exe | 84 793 033 bytes | 0FDB942B1E4EC000A13F600B0E5519BF3D2570781F0F66F5CDE8136E597CA18D |
| ArsExam_Update_4.1.2_win-x64.zip | 74 956 643 bytes | CDEB7F22D7CA8FC32655432BA42E70E528F68CE869AC47BCBF8D4264A601FF87 |
| ArsExam_Store_4.1.2.0_x64.msix (отделен Store кандидат) | 78 204 135 bytes | 3812598F0ED3DC2A03FF89B543561B3ED0B4033B3D276D67417B7285967FECCF |

GitHub Setup/Desktop/Launcher са Authenticode NotSigned. За Store е изграден отделен защитен неподписан MSIX. Той не е доказателство за Microsoft certification или Store публикация.

## Изолирани Windows Sandbox инсталации

- Clean Desktop и Portable: PASS; инсталация, reinstall, exact hash/document inventory, стартиране до екрана за активация и нормално затваряне.
- Setup 3.9.8 → 4.1.2: PASS за Desktop/Portable, синтетични постоянни папки и rollback версия.
- Setup 4.1.1 → 4.1.2: PASS за Desktop/Portable, синтетични постоянни папки и rollback версия.
- Използвани са синтетични потребителски файлове, не реални бази и потребителски лицензи.

## WACK

**WACK PASS — независима проверка:** общ резултат PASS, partialRun FALSE, WACK exit 0, 24 теста; 23 PASS и 1 незадължителен FAIL (`Blocked executables`, индекс 88). Няма задължителни неуспешни тестове. Седемте компонента на SDK са инсталирани успешно в офлайн Sandbox. Оригинален XML SHA-256: `0F228D9D4DBA8BECE59CCF581DFA0DFF266B2374CD1EAC9CAD83282890DED99D`. Независимият проверяващ отчита `WACK_QA_PASS`, като проверява и точния MSIX/source SHA; временният тестов сертификат съществува само в Sandbox и не е издателски подпис.

## Microsoft Store MSIX — реални изолирани обновявания

- **4.1.1.0 → 4.1.2.0: PASS.** Инсталиран е базовият MSIX, след това новият кандидат със същото package family; синтетичните Data/Media/Licensing файлове са запазени. Пакетираното приложение се стартира и завършва нормално с exit code 0.
- **3.9.8.0 → 4.1.2.0: PASS.** Същата реална инсталация, проверка на постоянните синтетични файлове, стартиране и нормално приключване с exit code 0.
- Двата теста са изпълнени в чиста Windows Sandbox, с изключена мрежа и временен сертификат само в госта. Това не доказва действителна Store сертификация или че Microsoft е подписал пакета.

## Protected GUI acceptance — PASS (exact 4.1.2 binary)

The final protected `ArsExam.exe` from the 4.1.2 build, SHA-256 `0D680C2244DE1B8075A584C4CBF5B0DF3BD9637A63D5B8F4A0F1DAA26CE7DDC9`, ProductVersion `4.1.2+7b3710377fbce8288b1488877e6a28b7ed2c3999`, was executed as an isolated **Portable QA copy on UNISOL**, without an issued license or customer database.

**PASS:** real Activation → Privacy policy → Contact support modal route; real diagnostic preview opened and closed; Create ZIP generated one 1,271-byte local archive with exactly `README.txt`, `support-summary.txt` and `recent-crash-reports.txt` (SHA-256 `42A465AB7A8BFE6133062496F35A8D8838F091DAFCEEC1C7FF118349165A5C16`). All dialogs closed normally; the application exited with process code `0`. The log confirms completed managed cleanup and contains no ERROR/FATAL entry. Diagnostics consent remained disabled, and no Sentry cache, test license or test database was created.

The first UI harness could not discover nested WPF modal windows because it inspected only top-level UI Automation elements. The corrected acceptance enumerated nested Windows. This final acceptance is **not a network-isolated Sandbox test**; no external diagnostic submission was initiated, but network traffic was not independently captured. Full local evidence: `exact-protected-support-412-result.json` and source/evidence report bundle.

## Публикация и независима верификация

**GITHUB STABLE ПУБЛИКУВАН И НЕЗАВИСИМО ПОТВЪРДЕН — 13.10.2026 г., 06:25:20 Europe/Sofia / 2026-10-13T03:25:20Z.** Официален non-draft/non-prerelease Release: https://github.com/pgnev/arsexam-releases/releases/tag/v4.1.2. Публичният `update/stable-manifest.json`, immutable private source tag `v4.1.2` и `Documentation/CURRENT_STABLE.json` са преминали cross-authority audit с PASS. Двата файла — Setup (84 793 033 байта) и Update ZIP (74 956 643 байта) — са свалени повторно от GitHub и изчислените върху изтеглените байтове SHA-256 хешове съвпадат с посочените по-горе. Публичната документация е актуализирана чрез PR #17; частният регистър на изданието — чрез source PR #272. **Microsoft Store 4.1.2.0 не е подаден или сертифициран с тази операция** и изисква отделно подаване през Partner Center.

## Поверителност и лицензи

Диагностиката остава изключена по подразбиране. Поправката не включва автоматично изпращане на отчети. В тази QA работа не са извършени Cloudflare deployments, нови отнемания или записи в продукционната D1.

Пълните сурови доказателства и автоматизираните проверяващи скриптове се пазят в локалната QA работна директория на издателя. Публичният отчет не включва лични файлови пътища или инсталационни идентификатори.
