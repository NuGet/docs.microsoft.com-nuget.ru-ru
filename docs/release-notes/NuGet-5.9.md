---
title: Заметки о выпуске NuGet 5,9
description: Заметки о выпуске NuGet 5,9, включая новые функции, исправления ошибок и DCR.
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 24933ebb51851da2583b03e7fd3e55fade5e8a18
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859537"
---
# <a name="nuget-59-release-notes"></a>Заметки о выпуске NuGet 5,9

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio | Доступно в пакетах SDK для .NET |
|:---|:---|:---|
| [**5.9**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16,9](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> установлен с Visual Studio 2019 с рабочей нагрузкой .NET Core
  
> [!NOTE]
> Для Visual Studio 16,9, MSBuild 16,9 и .NET 5.0.3 + требуется NuGet.exe 5,9 или более поздней версии.

## <a name="summary-whats-new-in-59"></a>Сводка: новые возможности в 5,9

* Добавьте элемент контекстного меню "Обновить" для зависимостей пакетов, который запускает пользовательский интерфейс диспетчера пакетов с предварительно выбранными пакетами для обновления [#10378](https://github.com/NuGet/Home/issues/10378)

    ![Щелкните правой кнопкой мыши пакет "Обновить".](media/releasenotes-59-update.png)

* Отображение запрошенной версии (включая плавающую версию или запрос диапазона версий) в столбце "версия" списка проектов в пользовательском интерфейсе диспетчера пакетов уровня решения — [#9827](https://github.com/NuGet/Home/issues/9827)

    ![Запрошенная версия в пользовательском интерфейсе диспетчера пакетов уровня решения](media/releasenotes-59-requested-version.png)

* Предложения пакета Интелликоде на вкладке просмотра пользовательского интерфейса диспетчера пакетов, выпущенной в виде A/B, [#10053](https://github.com/NuGet/Home/issues/10053)

* Расширение `.nupkg.metadata` файла для включения источника установки — [#10354](https://github.com/NuGet/Home/issues/10354)

* Познакомьтесь с новым свойством MSBuild, чтобы исключить выходные данные сборки для конкретного TFM в задаче Pack — [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**DCR (запрос на изменение структуры):**

* Значок значка "вниз" при установке последней версии пакета не является интуитивно понятным. Старая Зеленая метка была идеальной [#9789](https://github.com/NuGet/Home/issues/9789)

* Уровень детализации отладки NuGet должен указывать, откуда поступил пакет — [#3055](https://github.com/NuGet/Home/issues/3055)

* Пакет NuGet должен перехватывать неверный пропуск точки в номерах версий — [#9215](https://github.com/NuGet/Home/issues/9215)

* [КПВМ] Отключить закрепление центральных транзитивных зависимостей — [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM: ошибка при отсутствии ТПВ- [#9441](https://github.com/NuGet/Home/issues/9441)

* Контенсаш пакета журнала во время восстановления (во время извлечения) — [#10384](https://github.com/NuGet/Home/issues/10384)

* Реализуйте механизм предварительной регистрации для проектов с устаревшими пр., которые вызывают восстановление в решении Open- [#9986](https://github.com/NuGet/Home/issues/9986)

* Рекомендации по пакету NuGet должны работать, если в диспетчере пакетов выбрано более одного источника — [#10433](https://github.com/NuGet/Home/issues/10433)

* При восстановлении с нормальным уровнем подробности записывается источник, из которого восстанавливается пакет, [#10461](https://github.com/NuGet/Home/issues/10461)

**Появились**

* Инужетпаккажефилесервице — получение изображений и внедренных лицензий для Кодеспацес-Connected и standalone- [#10151](https://github.com/NuGet/Home/issues/10151)

* VS OE: Ипрожектметадатаконтекстинфо отсутствует модуль форматирования — [#10079](https://github.com/NuGet/Home/issues/10079)

* [КПВМ-Perf] Сократите сведения, записываемые в Централтранситиведепенденциграупс- [#10002](https://github.com/NuGet/Home/issues/10002)

* Операции восстановления, которые вызываются из-за незагружаемого проекта, регистрируются как данные `NoOp` телеметрии. [#9985](https://github.com/NuGet/Home/issues/9985)

* Значки с определенными цветовыми палетами вызывают сбой пользовательского интерфейса PM VS- [#10037](https://github.com/NuGet/Home/issues/10037)

* [КПВМ-Perf] Уменьшение клона Паккажеспек при добавлении сведений о КПВМ — [#10003](https://github.com/NuGet/Home/issues/10003)

* Интерфейс PM UI — Загрузка значка асинЦифи — [#10009](https://github.com/NuGet/Home/issues/10009)

* Задержка пользовательского интерфейса при загрузке URL-адресов значков в пользовательском интерфейсе PM — [#8505](https://github.com/NuGet/Home/issues/8505)

* Сходство потоков в потоках перекрывающегося и пользовательского интерфейса WPF — [#9161](https://github.com/NuGet/Home/issues/9161)

* Предупреждение о предупреждении NU5128, когда паккастул с targetFramework Alias- [#10097](https://github.com/NuGet/Home/issues/10097)

* Логика OutputPath в целевых объектах пакета в настраиваемой сборке работает неправильно [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE: кэширование экземпляра Исервицеброкер на клиенте- [#10141](https://github.com/NuGet/Home/issues/10141)

* Создание Нужетпрожектактионс для удаления из пользовательского интерфейса PM параллельная операция — [#9956](https://github.com/NuGet/Home/issues/9956)

* Производительность: уменьшение числа Уиделайс в Жетпаккажеспексасинк для устаревших проектов и проектов без поддержки. [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` не отправляет более одного файла [#4393](https://github.com/NuGet/Home/issues/4393)

* Выходные данные упаковываются в 80 символов в macOS при перенаправлении — [#10198](https://github.com/NuGet/Home/issues/10198)

* Сбой восстановления с помощью-source <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)

* netcoreapp 5.0 — Windows не выполняет циклический проход и не анализирует сведения о платформе — [#10177](https://github.com/NuGet/Home/issues/10177)

* Для восстановления пользовательских проектов CPS требуется возможность проекта Ассемблиреференцес. - [#8071](https://github.com/NuGet/Home/issues/8071)

* Проверка существования файла лицензии и значка всегда должна использовать сравнение с учетом регистра — [#9817](https://github.com/NuGet/Home/issues/9817)

* DotnetCLiToolReference восстановления затрудняют причины относительно количества проектов No-Op и уптодатепрожектскаунт- [#10038](https://github.com/NuGet/Home/issues/10038)

* Трудно увидеть поле штриховой линии формата пакета при переходе по вкладке в диалоговом окне "Выбор формата диспетчера пакетов NuGet" в темной теме — [#9729](https://github.com/NuGet/Home/issues/9729)

* Исключить ссылки на транзитивные платформы из `CollectFrameworkReferences`  -  [#10314](https://github.com/NuGet/Home/issues/10314)

* Статические свойства компаратора должны быть идемпотентными- [#10339](https://github.com/NuGet/Home/issues/10339)

* разрешение загрузки внутренних контрактов сборка (исправление RP или получение исключения) — [#9919](https://github.com/NuGet/Home/issues/9919)

* Замена службы Жетсервицеасинк в NuGet. Clients, часть 1 — [#10362](https://github.com/NuGet/Home/issues/10362)

* При установке интерфейса командной строки не следует устанавливать пакеты, отсутствующие в списке — [#7466](https://github.com/NuGet/Home/issues/7466)

* Статическое восстановление графа MSBuild — унннецессари ведение журнала о Мсбуилдстартупдиректори — [#10335](https://github.com/NuGet/Home/issues/10335)

* Зависимости проектов ссылками, помеченные как PrivateAssets, не должны включаться в файл блокировки проверка до даты — [#8565](https://github.com/NuGet/Home/issues/8565)

* Проекты SDK с неправильными данными не показывают ошибки восстановления в VS- [#10406](https://github.com/NuGet/Home/issues/10406)

* NU1004 при восстановлении решения, которое содержит проекты прежних версий и netstandard2 из командной строки с Локкедмоде- [#9623](https://github.com/NuGet/Home/issues/9623)

* Pack включает содержимое, которое переносится через пакеты зависимостей в пакет текущего проекта (только для проектов на основе SDK). [#8867](https://github.com/NuGet/Home/issues/8867)

* Добавление телеметрии для ошибок API расширяемости VS для NuGet — [#10062](https://github.com/NuGet/Home/issues/10062)

* Добавьте Женератерестореграффиле в статическом восстановлении графа, чтобы улучшить отладку.  - [#10365](https://github.com/NuGet/Home/issues/10365)

* Не удается открыть диспетчер пакетов NuGet — [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/экранный диктор не считывает метку "License" для "Apache-2,0" Link- [#10425](https://github.com/NuGet/Home/issues/10425)

* Сообщение в строке состояния "Обновлено" не является большим в VS- [#9402](https://github.com/NuGet/Home/issues/9402)

* packages.config package.lock.jsв использует неправильную целевую платформу — [#10257](https://github.com/NuGet/Home/issues/10257)

* Кодеспацес: исправление данных телеметрии с https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)

* Ошибка NU1004 исчезает при построении решения после включения "Ресторелоккедмоде" — [#8973](https://github.com/NuGet/Home/issues/8973)

* Переход по ПМУИ в обратном направлении должен быть зеркальным направлением вперед — [#10234](https://github.com/NuGet/Home/issues/10234)

* Отладка ПМУИ в экспериментальном экземпляре иногда вызывает InvalidCastException из Солутионвиев в Прожектвиев- [#10416](https://github.com/NuGet/Home/issues/10416)

* Версия по умолчанию — NULL после щелчка устаревшего пакета на вкладке "Обзор" — [#10380](https://github.com/NuGet/Home/issues/10380)

* Диспетчер NuGet в Visual Studio перезагружается после восстановления фокуса — [#4176](https://github.com/NuGet/Home/issues/4176)

* Удаление IPackageSourceProvider2 и связанных типов — [#10098](https://github.com/NuGet/Home/issues/10098)

* Пакет "Намеофпаккаже" несовместим с платформами "ALL" в проекте — [#5127](https://github.com/NuGet/Home/issues/5127)

* Креатеверсионсасинк выполняет ненужные Нужетверсион сравнения — [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet. Client должен заменить using Манажедимажемоникерс на Кновнмоникерс- [#9977](https://github.com/NuGet/Home/issues/9977)

* Нерекомендуемый значок перекрывает версию устаревшего пакета на вкладке Обзор — [#10452](https://github.com/NuGet/Home/issues/10452)

* Обработка ошибок PackageReference NU1604 различается в VS и командной строке (Restore & пользовательский интерфейс диспетчера пакетов) — [#9289](https://github.com/NuGet/Home/issues/9289)

* Кодеспацес: необходимые модули форматирования не зарегистрированы — [#10467](https://github.com/NuGet/Home/issues/10467)

* Удалите net45 как целевую платформу из NuGet. Frameworks — [#10470](https://github.com/NuGet/Home/issues/10470)

* Реализация. Добавьте новые телеметрии для мониторинга событий, связанных с использованием PMC и PowerShell. - [#10142](https://github.com/NuGet/Home/issues/10142)

* В окне Предварительный просмотр изменений отображается только один пакет, если для обновления в пользовательском интерфейсе диспетчера пакетов доступно несколько пакетов, [#10483](https://github.com/NuGet/Home/issues/10483)

* При упаковке проектов с нацеливанием на проект необходимо создать пустые группы Фрамеворкреференцес. [#10218](https://github.com/NuGet/Home/issues/10218)

* Трудно увидеть, что флажок пакет на вкладке "обновления" имеет вид штриховой линии при переходе по вкладке "синий/синий" (дополнительный контраст)/Лигхт Themes — [#8963](https://github.com/NuGet/Home/issues/8963)

* Флажки вкладок обновления не работают с программами чтения с экрана- [#10449](https://github.com/NuGet/Home/issues/10449)

* Обновление в ПМУИ приводит к тому, что ссылка на объект не задается экземпляром объекта — [#9882](https://github.com/NuGet/Home/issues/9882)

* Реализация. Добавьте новые телеметрии для отслеживания событий, связанных с использованием диспетчера ресурсов PMC и PowerShell. - [#10478](https://github.com/NuGet/Home/issues/10478)

* Ошибка копирования и вставки в V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)

* Исправление Нужетпаккажефилесервице. Используйте, используя для уничтожения MemoryStream — [#10503](https://github.com/NuGet/Home/issues/10503)


**[Список всех проблем, исправленных в этом выпуске — 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[Список фиксаций в этом выпуске — 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>Материалы сообщества

Благодарим всех участников, которые помогли сделать эту версию NuGet более Awesome!

|Куда|Вытягивание|Проблемы|
|----|----|----|
[омажид](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | Ошибка копирования и вставки в V2FeedPackageInfo- [#10480](https://github.com/NuGet/Home/issues/10480)
[Марцин — кристианк](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | Отсутствие тестов для случая, когда на пакеты имеется ссылка с помощью атрибута PrivateAssets = "ALL" — [#10397](https://github.com/NuGet/Home/issues/10397)
[Марцин — кристианк](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | Добавление поддержки для отправки нескольких пакетов — [#4393](https://github.com/NuGet/Home/issues/4393)
[Марцин — кристианк](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | Сборка библиотек NuGet не работает, если подписание сборки отключено — [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | Очистка сопутствующих документов — [#10399](https://github.com/NuGet/Home/issues/10399)
[пасожендавид](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | Проверка существования файла лицензии и значка всегда должна использовать сравнение с учетом регистра — [#9817](https://github.com/NuGet/Home/issues/9817)
[камперсау](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | Используйте Битмапкреатеоптионс. Игнореколорпрофиле для решения проблемы с WPF при использовании Декодепикселвидс- [#10037](https://github.com/NuGet/Home/issues/10037)
[бжоркстромм](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | Ссылка Windows SDK 10 разорвана в NuGet. Пошаговое руководством по публикации клиента — [#10099](https://github.com/NuGet/Home/issues/10099)
[бжоркстромм](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | Относительные ссылки разбиваются в NuGet. Пошаговое руководств по отладке клиента — [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | Улучшение тестовой основы и связанного кода — [#9996](https://github.com/NuGet/Home/issues/9996)
[ролфбжарне](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | Выходные данные упаковываются в 80 символов в macOS при перенаправлении — [#10198](https://github.com/NuGet/Home/issues/10198)
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | Сделайте NuGet. PackageManagement доступным в качестве пакета .NET Standard — [#6150](https://github.com/NuGet/Home/issues/6150)
[анипик](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | Познакомьтесь с новым свойством MSBuild, чтобы исключить выходные данные сборки для конкретного TFM в задаче Pack — [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="feedback-welcome"></a>Добро пожаловать на отзыв

Ваши отзывы очень важны для нас.  Если в этом выпуске возникли какие либо проблемы, ознакомьтесь с нашими [проблемами в GitHub](https://github.com/NuGet/Home/issues) и [сообществом разработчиков Visual Studio](https://developercommunity.visualstudio.com/) за существующими проблемами.  При возникновении новых проблем в NuGet сообщите о [проблемах GitHub](https://github.com/NuGet/Home/issues/new).
Чтобы получить общие сведения о проблемах с NuGet, сообщите нам об этом с помощью параметра [сообщить о проблеме](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) в ИЗБРАННОЙ среде IDE в разделе **Справка > сообщить о проблеме**.
