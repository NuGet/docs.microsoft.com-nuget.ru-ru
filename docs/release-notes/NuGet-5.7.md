---
title: Заметки о выпуске NuGet 5,7
description: Заметки о выпуске NuGet 5,7, включая новые функции, исправления ошибок и DCR.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364156"
---
# <a name="nuget-57-release-notes"></a>Заметки о выпуске NuGet 5,7

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio | Доступно в пакетах SDK для .NET |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> установлен с Visual Studio 2019 с рабочей нагрузкой .NET Core

## <a name="summary-whats-new-in-57"></a>Сводка: новые возможности в 5,7

### <a name="features-added-in-this-release"></a>Функции, добавленные в этом выпуске

* Добавлена поддержка внешних псевдонимов для ссылок на пакеты NuGet — [#4989](https://github.com/NuGet/Home/issues/4989)

* Быстро переключаться между установленными и обновленными вкладками, позволяя им совместно использовать источник данных и сокращать ресфрешинг- [#8294](https://github.com/NuGet/Home/issues/8294)

* Сделайте восстановление быстрее, вызвав API-интерфейсы статических графов MSBuild (dotnet.exe) — [#9644](https://github.com/NuGet/Home/issues/9644)

* Добавлено частичное восстановление Visual Studio для проектов PackageReference (без-op + +) — [#9513](https://github.com/NuGet/Home/issues/9513)

* Пользовательский интерфейс диспетчера пакетов Visual Studio аварийно завершит работу при поиске неправильного поведения источников пакетов, которые возвращают больше запрошенного количества результатов на HTTP-запрос. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Добавлена интеграция сведений PackageVersion для проектов стилей, отличных от SDK, в VS Restore- [#9236](https://github.com/NuGet/Home/issues/9236)

* Добавлена поддержка nuget.exe обновления `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* Добавлена поддержка нескольких файлов конфигурации в каталоге%Аппдата%\нужет — [#9394](https://github.com/NuGet/Home/issues/9394)

* Детерминистиксаурцепасс теперь получает исходные пакеты NuGet для учетной [#9431](https://github.com/NuGet/Home/issues/9431)

* Добавлен API расширяемости Инужетпрожектсервице. Жетинсталледпаккажесасинк — [#9702](https://github.com/NuGet/Home/issues/9702)

* Добавлен API взаимодействия для перечисления резервных папок без необходимости решения или проекта — [#9395](https://github.com/NuGet/Home/issues/9395)

* Добавлен `latest` параметр для `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Появились**

* При восстановлении с помощью команды DotNet CLI при запуске подключаемых модулей учетных данных Попробуйте использовать CLI DotNet в системном пути, если `DOTNET_HOST_PATH`  переменная среды не определена. - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe спецификация создает тег авторского права с жестко запрограммированным текстом, а не `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe выдает исключение "авторы должны" во время упаковки файла CSPROJ, игнорируя заполнители и атрибуты AssemblyInfo, если имя сборки изменено — [#4234](https://github.com/NuGet/Home/issues/4234)

* HttpRequestMessage многократно используется несколько раз, которое не поддерживается в Соккесттфандлер- [#8661](https://github.com/NuGet/Home/issues/8661)

* NuGet. index 5.6.0 Preview 3 и более поздних версий использует другой маркер открытого ключа — [#9481](https://github.com/NuGet/Home/issues/9481)

* Соблюдайте Треатварнингсасеррорс во время создания пакета NuGet — [#7404](https://github.com/NuGet/Home/issues/7404)

* [КПВМ] Ложное понижение уровня пакета для нескольких проектов P2P — [#9549](https://github.com/NuGet/Home/issues/9549)

* Вкладка "Обзор" не отображается по левому краю поля поиска [#9559](https://github.com/NuGet/Home/issues/9559)

* Установленная версия не согласуется со значком "внедренный" в пользовательском интерфейсе уровня решения по одному идентификатору пакета с несколькими установленными версиями — [#9321](https://github.com/NuGet/Home/issues/9321)

* Утечка: PartCreationPolicy (CreationPolicy. unshareed) NuGet. Солутионрестореманажер. Рестореоператионлогжер- [#9595](https://github.com/NuGet/Home/issues/9595)

* Избегайте чтения файла ресурсов при восстановлении без операций — [#9693](https://github.com/NuGet/Home/issues/9693)

* NuGet. Protocol не поддерживает получение количества Скачиваний версии из поиска [#9086](https://github.com/NuGet/Home/issues/9086)

* Повышение производительности памяти PackageMetadataResourceV3 путем уменьшения JObject зависимостей — [#9719](https://github.com/NuGet/Home/issues/9719)

**Запросы на изменение структуры:**

* Подавляет `<owners>` элемент при избыточном [#5134](https://github.com/NuGet/Home/issues/5134)

* Вести журнал Интервалтраккерс как события ETW — [#9593](https://github.com/NuGet/Home/issues/9593)

* Добавлено информационное сообщение о восстановлении для информирования пользователей КПВМ о том, что эта функция находится на этапе предварительной версии [#9340](https://github.com/NuGet/Home/issues/9340)

* Заполнение обозреватель решений пакетных и проектных зависимостей из файла ресурсов — [#9580](https://github.com/NuGet/Home/issues/9580)

* Вкладка "установленные пакеты" не должна разбивать список пакетов на страницы [#6995](https://github.com/NuGet/Home/issues/6995)

**[Список всех проблем, исправленных в этом выпуске — 5,7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Материалы сообщества

Благодарим всех участников, которые помогли сделать эту версию NuGet более Awesome!

|Куда|Вытягивание|Проблемы|
|----|----|----|
|[камперсау](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet. Protocol не поддерживает получение количества Скачиваний версии из поиска [#9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage многократно используется несколько раз, которое не поддерживается в Соккесттфандлер- [#8661](https://github.com/NuGet/Home/issues/8661)|
|[Джозеф Муссер (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|Подавляет `<owners>` элемент при избыточном [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Володимир Школка (Блаккгад)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet не может выполнить восстановление из источников HTTPS, для которых требуются сертификаты клиентов. [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Унгуреану (Серзок)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|Хттпсаурцеаусентикатионхандлер SemaphoreSlim для будущего тестирования — [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Суннер (Суннжек)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe спецификация создает тег авторского права с жестко запрограммированным текстом, а не `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Оливиер Спинелли (Оливиер-Спинелли)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|При восстановлении с помощью команды DotNet CLI при запуске подключаемых модулей учетных данных Попробуйте использовать CLI DotNet в системном пути, если `DOTNET_HOST_PATH`  переменная среды не определена. - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[гойзанг](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|Добавлен `latest` параметр для `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)|
