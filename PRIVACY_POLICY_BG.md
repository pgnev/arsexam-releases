# Политика за поверителност — ArsExam Desktop

Редакция: 31.08.2026 г. — ArsExam 3.5.0 Stable
В сила от: публичното публикуване на ArsExam 3.5.0

Тази редакция описва техническото поведение на ArsExam 3.5.0 Stable и се доставя с официалния Setup.

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
- Recycler/import staging, review context и operation history според използваната функция;
- изображения, аудио и други `Media` файлове;
- import/export файлове;
- защитени Manual Backup-и и вътрешни Safety Backup-и;
- криптиран Backup Registry, включително локално защитени owner Backup credentials;
- Transfer Registry/history без plaintext Transfer codes;
- update settings/cache;
- локален technical log;
- diagnostics consent/settings и, когато функцията е включена, ограничена локална история на минимизирани diagnostic reports.

Тези работни данни не се изпращат автоматично до автора като част от нормалната offline работа.

Профилният e-mail е **контактна информация**, а не online recovery identity. Забравена парола се възстановява локално чрез Recovery Key и не създава e-mail recovery request към външен backend.

### Recycler, import и workflow state

Recycler/import review работи локално върху предоставените от потребителя материали. Source document, key, OCR/Media evidence и staged review context могат да съдържат изпитно или друго работно съдържание.

ArsExam 3.5 пази explicit per-record workflow/outcome information, за да не изчезват анализирани записи без видим резултат. Това е локална operational traceability функция; не е remote analytics.

Локалният Windows OCR, използван от Recycler за поддържаните изображения, не изпраща source images към cloud OCR услуга като част от описания Recycler path.

## 3. Защита на локалното хранилище

ArsExam използва application-level encryption за основната SQLite база и отделни защитени локални registry/security файлове.

Профилната парола не е директният database-encryption key. ArsExam използва local key hierarchy и purpose-separated derivation/wrapping за различните защитени функции.

### Важна граница

Standalone файловете в локалните `Media` папки **не трябва да се считат за индивидуално криптирани при покой само защото SQLite базата е криптирана**. При чувствителни removable devices използвайте подходящи Windows/storage controls, например BitLocker/BitLocker To Go, когато рискът го изисква.

Ръчните `.arsexam-backup` архиви и защитените transfer packages използват собствено authenticated encryption и не са обикновени plaintext ZIP архиви.

Application-level encryption не защитава от malware/keylogger или процес с достатъчни права, който вече контролира отключена ArsExam/Windows сесия.

## 4. Recovery Key и забравена парола

Функцията **„Забравена парола?“** работи локално. Текущият ArsExam 3.5 client не използва Supabase, recovery e-mail, Request ID, support code или друг online control plane за password recovery.

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

### Data-only Backup v2 в ArsExam 3.5

Backup snapshot v2 пази work data, включително official-bank schema-v8 workflow/generator-eligibility и difficulty methodology/assessment state, необходими за коректно Restore на 3.5 работното съдържание.

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

При включена диагностика ArsExam може да създава минимизиран report при необработена грешка, crash или изрично стартиран test diagnostic event.

Допустимият allow-listed набор е ограничен до технически полета като report ID/UTC time, application version/distribution mode, общ OS/runtime context, exception type и sanitized stack trace.

ArsExam **не добавя като предназначен remote diagnostic payload**:

- име/e-mail/телефон/институция от локалния профил;
- profile password/hash;
- Recovery Key;
- Backup passwords;
- Transfer codes;
- въпроси, answers, keys или bank/workflow content;
- database или Backup/Transfer packages;
- images/audio/screenshots/clipboard.

При валидно текущо съгласие ArsExam може да пази до **20** локални минимизирани diagnostic reports за не повече от **30 дни**. При изключване на функцията бъдещото remote изпращане се прекратява и локалната minimized history се управлява според приложната retention логика.

Remote delivery е възможно само ако конкретният build е конфигуриран с валиден **Sentry EU/DE** ingest channel и потребителят е дал изрично съгласие. Production ingest е ограничен до host pattern `*.ingest.de.sentry.io`.

Доставчик на Sentry е Functional Software, Inc. Standard network data, включително IP адресът на връзката, могат технически да бъдат обработени от доставчика/инфраструктурата, дори ArsExam да не добавя IP като поле в event-а.

Информация за Sentry:

- Privacy: https://sentry.io/privacy/
- Data Processing Addendum: https://sentry.io/legal/dpa/
- Subprocessors: https://sentry.io/legal/subprocessors/

Правното основание за доброволната crash/error диагностика е **съгласие** по чл. 6, § 1, б. „а“ GDPR, когато GDPR е приложим. Съгласието може да бъде оттеглено чрез изключване на функцията за бъдещо изпращане.

## 8. Официални обновления

ArsExam може да използва internet за проверка и изтегляне на official updates от public GitHub release/update infrastructure.

При настройка **„Автоматично — проверка на 12 часа“** потребителският update-check cadence е 12 часа.

Update request-ът не включва question-bank content, workflow/difficulty content, Recovery Key, Backup passwords, Transfer codes или local profile като приложен payload. Както при всяка HTTPS връзка, GitHub и network infrastructure могат технически да обработят IP address, date/time и standard request metadata според собствените си policies.

Official public distribution/update repository е `pgnev/arsexam-releases`. `pgnev/arsexam-desktop` може да остане legacy read-only compatibility fallback за supported older clients, но не е current release authority.

## 9. Поддръжка и e-mail кореспонденция

Ако доброволно изпратите e-mail до support, авторът може да обработи e-mail address/name, съдържанието на request-а, date/time, standard mail metadata и файловете, които Вие сами сте решили да приложите.

Не изпращайте profile passwords, Recovery Keys, Backup passwords, Transfer codes, цели databases, protected Backup-и или ненужни лични/изпитни данни по ordinary e-mail.

Support correspondence се пази само доколкото е необходима за обработване на случая и последваща техническа справка, по правило до **12 месеца след последната съществена кореспонденция**, освен ако по-дълъг срок е необходим по закон или за установяване, упражняване или защита на правни претенции.

## 10. Външни получатели и международна обработка

В зависимост от използваната network функция външни providers могат да бъдат:

- **GitHub** — official update manifests/releases и update downloads;
- **Sentry EU/DE** — само при explicit opt-in remote diagnostics и valid configured release;
- e-mail providers на страните — при доброволна support correspondence.

ArsExam 3.5 **не използва Supabase за password recovery**.

Външните providers могат да използват инфраструктура в различни държави според собствените си договорни/privacy mechanisms. ArsExam не гарантира, че всяка standard network metadata operation остава физически само в България/ЕИП, когато provider не предоставя такава гаранция.

## 11. Срокове и изтриване

Local work data, Backups, registries и settings остават под user control и се пазят до deletion/uninstall/cleanup според съответната функция.

Local diagnostic history е ограничена до до 20 minimized reports и до 30 дни според diagnostics consent/settings.

Support correspondence се пази според необходимостта за конкретния случай и описания ориентировъчен срок.

## 12. Права на субектите на данни

Когато авторът действително обработва Ваши personal data и GDPR е приложим, според конкретния случай можете да имате право на информация/access, correction, deletion, restriction, objection, portability и withdrawal of consent за processing, основана на consent.

За искания: **petkoganev@gmail.com**.

Ако считате, че приложимите правила са нарушени, можете да подадете complaint до компетентния supervisory authority, включително Комисията за защита на личните данни в Република България, когато тя е компетентна.

## 13. Данни на ученици и други трети лица

ArsExam не използва public update/support/diagnostics channels с цел да събира изпитното съдържание или personal data, които user въвежда в local banks/documents/Media.

Потребителят или организацията, която определя съдържанието на локалните материали, носи собствена отговорност за legal basis, minimization, access и retention на данни на ученици/други трети лица.

## 14. Версионност на политиката

Тази редакция е технически синхронизирана с **ArsExam 3.5.0 Stable** към 31.08.2026 г. и е проверена срещу exact release source и Setup legal-document contract.

Release-specific policy, доставена с конкретен Setup, остава част от release evidence за тази версия.
