# Политика за поверителност — ArsExam Desktop

Редакция: 03.09.2026 г. — ArsExam 3.6.3 Stable  
В сила от: публичното публикуване на ArsExam 3.6.3 Stable

Тази редакция описва действащия privacy/consent contract на **ArsExam 3.6.3 Stable**, включително diagnostics consent 4.0, bounded Sentry store-and-forward delivery и локалния Launcher update/rollback incident bridge. Историческите version-specific assets не се променят ретроактивно.

## 1. Администратор и контакт

За личните данни, които действително достигат до автора чрез доброволна crash/error диагностика или пряка кореспонденция с поддръжката, администратор е:

**Петко Ганев**  
Контакт по въпроси за поверителност и поддръжка: **petkoganev@gmail.com**

ArsExam Desktop е **offline-first** приложение. Основните работни данни се съхраняват локално и по принцип не достигат до автора.

Когато училище, организация или друго лице въвежда лични данни на трети лица в локални банки, документи, Media или Backup-и, то самостоятелно отговаря за правното основание, минимизацията, достъпа, сроковете за съхранение и останалите си задължения за това съдържание.

## 2. Данни, които остават локално

В зависимост от използваните функции ArsExam може да съхранява на устройството:

- локален профил и настройки;
- salted/versioned password-verifier/hash данни; plaintext профилната парола не се записва;
- local security-envelope state и материали за Recovery Key механизма;
- въпросни банки, задачи, теми, answer keys и generated tests;
- workflow/generator-eligibility и difficulty methodology/assessment state;
- Recycler/import staging, review context, operation history и local provenance/source snapshots;
- изображения, аудио и други `Media` файлове;
- import/export файлове;
- защитени Manual Backup-и и вътрешни Safety Backup-и;
- криптиран Backup Registry и Transfer Registry/history без plaintext Transfer codes;
- update settings/cache;
- локален technical log;
- diagnostics consent/settings и ограничена локална история на минимизирани diagnostic reports;
- при update/activation/startup-health/rollback проблем — bounded local `LauncherIncidents` journal с минимизирани технически полета.

Тези работни данни не се изпращат автоматично до автора като част от нормалната offline работа.

Профилният e-mail е контактна информация, а не online recovery identity. Забравена парола се възстановява локално чрез Recovery Key.

## 3. Защита на локалното хранилище

ArsExam използва application-level encryption за основната SQLite база и отделни защитени локални registry/security файлове. Профилната парола не е директният database-encryption key.

Standalone файловете в `Media` и Recycler source snapshots **не трябва да се считат за индивидуално криптирани при покой** само защото SQLite базата е криптирана. При чувствителни removable devices използвайте подходящи Windows/storage controls, например BitLocker/BitLocker To Go, когато рискът го изисква.

Ръчните `.arsexam-backup` архиви и защитените transfer packages използват собствено authenticated encryption. Нито една защита при покой не предпазва от malware/keylogger или достатъчно привилегирован достъп до вече отключена сесия.

## 4. Recovery Key и забравена парола

Функцията „Забравена парола?“ работи локално. ArsExam 3.6.3 не използва recovery e-mail backend, Request ID, support-issued reset code или universal server-side/master-key bypass.

Recovery Key:

- се генерира локално;
- е един активен ключ за профила;
- е single-use при успешно password recovery;
- след успешно използване става невалиден и се генерира нов ключ;
- не се изпраща на автора, GitHub или Sentry;
- не е Backup password и не е Transfer code.

Ако потребителят изгуби едновременно профилната си парола и валидния Recovery Key, авторът няма универсален механизъм за отключване на профила.

## 5. Backup / Restore и Desktop / Portable

Manual Backup е local protected `.arsexam-backup` archive със собствен Backup identity/password. Backup password е отделна от profile password и Recovery Key.

Data-only Backup не възстановява стара security identity като profile password/hash, Recovery Key/security envelope или Backup Registry secret vault. Mutating Restore създава Safety Backup преди промяна и поддържа rollback semantics.

Desktop/Portable transfer е локален data workflow и е отделен от GitHub update channel. Защитеният Transfer използва отделен Transfer ID/temporary code и не пази plaintext Transfer code в историята.

## 6. Crash/error диагностика — diagnostics consent 4.0

Crash/error диагностиката е **opt-in** и е изключена по подразбиране. ArsExam не събира отделна usage/behavior analytics телеметрия за това кои екрани, банки, workflow states или функции използвате.

Diagnostics consent **4.0** обхваща две строго минимизирани категории:

1. приложни crash/error/test diagnostic events;
2. Launcher update/activation/startup-health/rollback incidents, които първо се записват само локално и никога не се изпращат директно от Launcher.

За приложни грешки допустимият allow-listed набор е ограничен до технически полета като report ID/UTC time, application version/distribution mode, общ OS/runtime context, exception type и sanitized stack trace.

За Launcher incident-и допустимият набор е още по-тесен: incident ID/UTC time, безопасни current/target version стойности, stage (`apply`, `activate`, `health-check`, `rollback`), deployment mode, failure class/outcome, rollback attempted/succeeded и sanitized exception **type only**, когато е наличен.

Launcher **няма Sentry SDK и не изпраща incident-и директно към remote diagnostics endpoint**. Той може само best-effort да запише bounded local journal entry. Desktop може да приеме такъв incident в diagnostics pipeline само ако:

- валидно consent 4.0 е било активно в момента на възникване; и
- същото валидно текущо съгласие е активно при последващото Desktop ingestion.

Incident, възникнал без валидно occurrence-time consent, не става допустим за бъдещо изпращане само защото потребителят по-късно е включил диагностиката.

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

При временна липса на връзка вече минимизиран и consent-eligible Sentry event може да остане в bounded local cache и да бъде изпратен по-късно, ако съгласието продължава да е валидно. При изключване/невалидно съгласие бъдещото remote изпращане се прекратява и локалните diagnostics/cache данни се purge-ват според приложната логика.

Remote delivery е възможно само ако конкретният build е конфигуриран с валиден **Sentry EU/DE** ingest channel и потребителят е дал изрично текущо съгласие. Production ingest е ограничен до host pattern `*.ingest.de.sentry.io`.

Доставчик на Sentry е Functional Software, Inc. Standard network data, включително IP адресът на връзката, могат технически да бъдат обработени от доставчика/инфраструктурата, дори ArsExam да не добавя IP като event поле.

Информация за Sentry:

- Privacy: https://sentry.io/privacy/
- Data Processing Addendum: https://sentry.io/legal/dpa/
- Subprocessors: https://sentry.io/legal/subprocessors/

Правното основание за доброволната crash/error диагностика е **съгласие** по чл. 6, § 1, б. „а“ GDPR, когато GDPR е приложим. Съгласието може да бъде оттеглено чрез изключване на функцията за бъдещо изпращане.

## 7. Официални обновления

ArsExam може да използва internet за проверка и изтегляне на official updates от public GitHub release/update infrastructure. Official public distribution/update repository е `pgnev/arsexam-releases`.

Update request-ът не включва question-bank content, Recovery Key, Backup passwords, Transfer codes или local profile като приложен payload. Както при всяка HTTPS връзка, GitHub и network infrastructure могат технически да обработят IP address, date/time и standard request metadata според собствените си policies.

Update пакетите се приемат само след SHA-256 verification срещу authoritative Stable manifest.

## 8. Поддръжка и e-mail кореспонденция

Ако доброволно изпратите e-mail до support, авторът може да обработи e-mail address/name, съдържанието на request-а, date/time, standard mail metadata и файловете, които Вие сами сте решили да приложите.

Не изпращайте profile passwords, Recovery Keys, Backup passwords, Transfer codes, цели databases, protected Backup-и или ненужни лични/изпитни данни по ordinary e-mail.

Support correspondence се пази само доколкото е необходима за обработване на случая и последваща техническа справка, по правило до **12 месеца след последната съществена кореспонденция**, освен ако по-дълъг срок е необходим по закон или за установяване, упражняване или защита на правни претенции.

## 9. Права на субектите на данни

Когато GDPR е приложим и авторът е администратор на данните, можете да поискате достъп, коригиране, изтриване, ограничаване, възражение или преносимост, когато съответното право е приложимо. Можете да оттеглите consent за бъдеща diagnostics delivery чрез изключване на функцията.

За въпроси и искания: **petkoganev@gmail.com**. Имате право и на жалба до компетентния надзорен орган, включително Комисията за защита на личните данни, когато тя е компетентна.

## 10. Промени в политиката

Ново официално издание може да съдържа актуализирана политика, когато техническото поведение или правните обстоятелства го изискват. Съществени промени в remote diagnostics/consent contract-а не следва да се прилагат ретроактивно без необходимото ново съгласие.
