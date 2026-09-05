# Политика за поверителност — ArsExam Desktop

Редакция: 05.09.2026 г. — ArsExam Desktop 3.7.1 Stable
В сила от: публичното публикуване на ArsExam 3.7.1 Stable

Тази политика описва действащия privacy/consent contract на **ArsExam Desktop 3.7.1 Stable**, включително diagnostics consent 4.0, bounded Sentry store-and-forward delivery и локалния Launcher update/rollback incident bridge. Инсталираното приложение version-bind-ва bundled копието към действително инсталираната версия; този публичен файл е release-specific snapshot за 3.7.1.

## 1. Администратор и контакт

За личните данни, които действително достигат до автора чрез доброволна crash/error диагностика или пряка кореспонденция с поддръжката, администратор е:

**Петко Ганев**  
Контакт по въпроси за поверителност и поддръжка: **petkoganev@gmail.com**

ArsExam Desktop е **offline-first** приложение. Основните работни данни се съхраняват локално и по принцип не достигат до автора.

Когато училище, организация или друго лице въвежда лични данни на трети лица в локални банки, документи, Media или Backup-и, то самостоятелно отговаря за правното основание, минимизацията, достъпа, сроковете за съхранение и останалите си задължения за това съдържание.

## 2. Данни, които остават локално

В зависимост от използваните функции ArsExam може да съхранява на устройството:

- локален профил: име, e-mail за контакт, институция/дирекция, телефон и настройки;
- salted/versioned password-verifier/hash данни; plaintext профилната парола не се записва;
- local security-envelope state и wrapped/verifier материали за криптираното хранилище и Recovery Key механизма;
- encrypted profile-bound Recovery Key vault, когато е наличен за профила;
- въпросни банки, задачи, теми, answer keys и generated tests;
- schema-v8 workflow status и generator eligibility за official-bank content;
- versioned difficulty methodologies, automatic assessments, rationale и expert overrides;
- Recycler/import staging, review context, outcome information и operation history според използваната функция;
- Atomic Recycler source snapshots и provenance/evidence данни, включително приложими source/file/page/region и SHA-256 идентификатори;
- изображения, аудио и други `Media` файлове;
- import/export файлове;
- защитени Manual Backup-и и вътрешни Safety Backup-и;
- криптиран Backup Registry, включително локално защитени owner Backup credentials;
- Transfer Registry/history без plaintext Transfer codes;
- update settings/cache;
- локален technical log;
- diagnostics consent/settings и, когато функцията е включена, ограничена локална история на минимизирани diagnostic reports;
- при update/activation/startup-health/rollback проблем — ограничен локален `LauncherIncidents` journal с минимизирани технически полета.

Тези работни данни не се изпращат автоматично до автора като част от нормалната offline работа.

Профилният e-mail е **контактна информация**, а не online recovery identity. Забравена парола се възстановява локално чрез Recovery Key и не създава e-mail recovery request към външен backend.

### Recycler, import и workflow state

Recycler/import review работи локално върху предоставените от потребителя материали. Source document, key, OCR/Media evidence, Atomic snapshots и staged review context могат да съдържат изпитно или друго работно съдържание.

ArsExam пази explicit per-record workflow/outcome information, за да не изчезват анализирани записи без видим резултат. Atomic Recycler може да създава локални content-addressed source snapshots в `Data\RecyclerWorkspace\atomic-sources`, така че pending review да не зависи от оригиналния USB/външен път. Тези snapshots са локална operational/provenance функция; не са remote analytics.

Локалният Windows OCR, използван от Recycler за поддържаните изображения, не изпраща source images към cloud OCR услуга като част от описания Recycler path.

## 3. Защита на локалното хранилище

ArsExam използва application-level encryption за основната SQLite база и отделни защитени локални registry/security файлове.

Профилната парола не е директният database-encryption key. ArsExam използва local key hierarchy и purpose-separated derivation/wrapping за различните защитени функции.

### Важна граница

Standalone файловете в локалните `Media` папки и Recycler source snapshots **не трябва да се считат за индивидуално криптирани при покой само защото SQLite базата е криптирана**. При чувствителни removable devices използвайте подходящи Windows/storage controls, например BitLocker/BitLocker To Go, когато рискът го изисква.

Ръчните `.arsexam-backup` архиви и защитените transfer packages използват собствено authenticated encryption и не са обикновени plaintext ZIP архиви.

Application-level encryption не защитава от malware/keylogger или процес с достатъчни права, който вече контролира отключена ArsExam/Windows сесия.

## 4. Recovery Key и забравена парола

Функцията **„Забравена парола?“** работи локално. Текущият ArsExam Desktop client не използва Supabase, recovery e-mail, Request ID, support code или друг online control plane за password recovery.

Recovery Key:

- се генерира локално;
- е един активен ключ за профила;
- е single-use при успешно password recovery;
- след успешно използване става невалиден и се генерира нов ключ;
- не се изпраща на автора, GitHub или Sentry;
- не е Backup password и не е Transfer code.

Когато профилът поддържа encrypted profile-bound Recovery Key vault, след successful step-up authentication с текущата профилна парола ArsExam може да покаже активния Recovery Key и да позволи повторно копиране/export/print.

Ако потребителят изгуби едновременно профилната си парола и валидния Recovery Key, авторът няма универсален server-side/master-key механизъм за отключване на профила.

## 5. Ръчни Backup-и, Backup Registry и Restore

Manual Backup е local protected `.arsexam-backup` archive. Всеки Backup има собствен Backup number и cryptographically generated Backup password.

Backup password е отделна от profile password и Recovery Key. За Backup-и, създадени от текущия профил, ArsExam може да пази recoverable копие в **криптиран локален Backup Registry**, за да позволи последващо reveal/copy/export след step-up authentication.

### Data-only Backup v2

Backup snapshot v2 пази work data, включително official-bank schema-v8 workflow/generator-eligibility и difficulty methodology/assessment state, необходими за коректно Restore на текущото работно съдържание.

Data-only Backup **не възстановява като стара security identity**:

- profile password/hash;
- Recovery Key/security envelope;
- Backup Registry secret vault;
- diagnostics/update settings;
- import-history credentials.

Import batch history не е част от този data-only semantic contract; когато се възстановява workflow state, `source_batch_id` не се пренася като dangling operational reference.

Restore поддържа Preview, Merge/„Допълни“ и Safe Replace/„Замени безопасно“. Преди mutating Restore се създава Safety Backup. Merge запазва current target active methodology и existing-record companion state; conflicting same-ID/version methodology definition се блокира преди mutation.

Legacy v1 data-only snapshots остават четими, но липсващата schema-v8 provenance се реконструира по compatibility rules; ArsExam не твърди, че старият формат е съдържал данни, които исторически не е записвал.

## 6. Desktop / Portable data movement

Desktop и Portable data movement е локална функция и не използва GitHub update feed като transport за user work data.

Защитеният Transfer между Desktop и Portable използва отделен Transfer ID, временен Transfer code, local staging/validation, Safety Backup и rollback/recovery mechanics според съответния workflow. Transfer code не се записва в историята като plaintext credential.

Поддържаният direct Portable→Desktop import path копира persistent work categories след Safety Backup и не внася device-local UpdateCache/Diagnostics от source Portable data root. Schema-v8 workflow/difficulty state се пренася като част от SQLite work data.

## 7. Crash/error диагностика

Crash/error диагностиката е **opt-in** и е изключена по подразбиране. ArsExam не събира отделна usage/behavior analytics телеметрия за това кои екрани, банки, workflow states или функции използвате.

Diagnostics consent **4.0** обхваща две строго минимизирани категории:

1. приложни crash/error/test diagnostic events;
2. Launcher update/activation/startup-health/rollback incidents, които първо се записват само локално и никога не се изпращат директно от Launcher.

За приложни грешки допустимият allow-listed набор е ограничен до технически полета като report ID/UTC time, application version/distribution mode, общ OS/runtime context, exception type и sanitized stack trace.

За Launcher incident-и допустимият набор е още по-тесен: incident ID/UTC time, безопасни current/target version стойности, stage (`apply`, `activate`, `health-check`, `rollback`), deployment mode, failure class/outcome, rollback attempted/succeeded и sanitized exception **type only**, когато е наличен.

Launcher **няма Sentry SDK, HTTP client или друг remote diagnostics endpoint**. Той може само best-effort да запише bounded local journal entry. Desktop може да приеме такъв incident в нормалния diagnostics pipeline само ако:

- валидно consent 4.0 за Sentry EU е било активно в момента на възникване; и
- същото валидно текущо съгласие е активно при последващото Desktop ingestion.

Incident, възникнал без валидно occurrence-time consent, се изтрива при compatible Desktop startup и **не се пази за бъдещо opt-in**. Така бъдещо включване на диагностиката не разрешава ретроактивно изпращане на стари събития.

ArsExam **не добавя като предназначен remote diagnostic payload**:

- име/e-mail/телефон/институция от локалния профил;
- profile password/hash;
- Recovery Key;
- Backup passwords;
- Transfer codes;
- въпроси, answers, keys или bank/workflow content;
- database или Backup/Transfer packages;
- images/audio/screenshots/clipboard;
- filesystem paths;
- package/download URLs;
- SHA/hash стойности;
- PID, command line или други process internals;
- raw exception message/data.

При валидно текущо съгласие ArsExam може да пази до **20** локални минимизирани diagnostic reports за не повече от **30 дни**. Sentry SDK store-and-forward cache-ът също е bounded до 20 items. Launcher incident journal-ът е отделен local-only bridge, bounded до **20** entries, **8 KiB** на entry и **30 дни** retention.

При временна липса на връзка вече минимизиран и consent-eligible Sentry event може да остане в bounded local Sentry cache и да бъде изпратен по-късно, ако съгласието продължава да е валидно. При изключване или invalid/stale consent бъдещото remote изпращане се прекратява; local diagnostic history и Sentry cache се purge-ват според приложната логика.

Remote delivery е възможно само ако конкретният build е конфигуриран с валиден **Sentry EU/DE** ingest channel и потребителят е дал изрично текущо съгласие. Production ingest е ограничен до host pattern `*.ingest.de.sentry.io`.

Доставчик на Sentry е Functional Software, Inc. Standard network data, включително IP адресът на връзката, могат технически да бъдат обработени от доставчика/инфраструктурата, дори ArsExam да не добавя IP като поле в event-а.

Информация за Sentry:

- Privacy: https://sentry.io/privacy/
- Data Processing Addendum: https://sentry.io/legal/dpa/
- Subprocessors: https://sentry.io/legal/subprocessors/

Правното основание за доброволната crash/error диагностика е **съгласие** по чл. 6, § 1, б. „а“ GDPR, когато GDPR е приложим. Consent 3.0 или по-старо съгласие не се интерпретира автоматично като consent 4.0; потребителят трябва изрично да включи и запази диагностиката отново под актуалното disclosure. Съгласието може да бъде оттеглено чрез изключване на функцията за бъдещо изпращане.

## 8. Официални обновления

ArsExam може да използва internet за проверка и изтегляне на official updates от public GitHub release/update infrastructure.

При настройка **„Автоматично — проверка на 12 часа“** потребителският update-check cadence е 12 часа.

Update request-ът не включва question-bank content, workflow/difficulty content, Recovery Key, Backup passwords, Transfer codes или local profile като приложен payload. Както при всяка HTTPS връзка, GitHub и network infrastructure могат технически да обработят IP address, date/time и standard request metadata според собствените си policies.

Official public distribution/update repository е `pgnev/arsexam-releases`. `pgnev/arsexam-desktop` може да остане legacy read-only compatibility endpoint за supported older clients, но не е current release authority.

## 9. Поддръжка и e-mail кореспонденция

Ако доброволно изпратите e-mail до support, авторът може да обработи e-mail address/name, съдържанието на request-а, date/time, standard mail metadata и файловете, които Вие сами сте решили да приложите.

Не изпращайте profile passwords, Recovery Keys, Backup passwords, Transfer codes, цели databases, protected Backup-и или ненужни лични/изпитни данни по ordinary e-mail.

Support correspondence се пази само доколкото е необходима за обработване на случая и последваща техническа справка, по правило до **12 месеца след последната съществена кореспонденция**, освен ако по-дълъг срок е необходим по закон или за установяване, упражняване или защита на правни претенции.

## 10. Външни получатели и международна обработка

В зависимост от използваната network функция външни providers могат да бъдат:

- **GitHub** — official update manifests/releases и update downloads;
- **Sentry EU/DE** — само при explicit opt-in remote diagnostics и valid configured release;
- e-mail providers на страните — при доброволна support correspondence.

ArsExam Desktop **не използва Supabase за password recovery**.

Външните providers могат да използват инфраструктура в различни държави според собствените си договорни/privacy mechanisms. ArsExam не гарантира, че всяка standard network metadata operation остава физически само в България/ЕИП, когато provider не предоставя такава гаранция.

## 11. Срокове и изтриване

Local work data, Backups, registries и settings остават под user control и се пазят до deletion/uninstall/cleanup според съответната функция.

Pending Atomic Recycler source snapshots могат да бъдат задържани, докато staged пакет ги реферира. Orphan snapshot cleanup се извършва само когато няма pending reference и fail-closed проверките позволяват безопасно изтриване.

Local diagnostic history и Sentry cache са bounded до 20 items според съответния формат и се управляват от diagnostics consent/settings. Launcher incident journal-ът е bounded до 20 entries и 30 дни; malformed/oversized/stale material се отхвърля fail-closed.

Support correspondence се пази според необходимостта за конкретния случай и описания ориентировъчен срок.

## 12. Права на субектите на данни

Когато авторът действително обработва Ваши personal data и GDPR е приложим, според конкретния случай можете да имате право на информация/access, correction, deletion, restriction, objection, portability и withdrawal of consent за processing, основана на consent.

За искания: **petkoganev@gmail.com**.

Ако считате, че приложимите правила са нарушени, можете да подадете complaint до компетентния supervisory authority, включително Комисията за защита на личните данни в Република България, когато тя е компетентна.

## 13. Данни на ученици и други трети лица

ArsExam не използва public update/support/diagnostics channels с цел да събира изпитното съдържание или personal data, които user въвежда в local banks/documents/Media.

Потребителят или организацията, която определя съдържанието на локалните материали, носи собствена отговорност за legal basis, minimization, access и retention на данни на ученици/други трети лица.

## 14. Версионност на политиката

Този публичен policy snapshot е обвързан с **ArsExam 3.7.1 Stable**. Инсталираното приложение version-bind-ва bundled policy към действително инсталираната версия, а публичният Stable статус се определя от официалния public release/update authority.

Вече публикуваните release-specific policy/assets остават immutable historical evidence. При бъдеща промяна на privacy/consent contract-а се създава нова редакция и се минава приложимият legal/privacy review и release gate, без ретроактивно пренаписване на старите публични binaries/assets.
