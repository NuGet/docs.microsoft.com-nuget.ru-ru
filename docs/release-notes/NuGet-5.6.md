---
title: Заметки о выпуске NuGet 5,6
description: Заметки о выпуске NuGet 5,6, включая новые функции, исправления ошибок и DCR.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727809"
---
# <a name="nuget-56-release-notes"></a>Заметки о выпуске NuGet 5,6

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio| Доступно в пакетах SDK для .NET|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16.6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core

## <a name="summary-whats-new-in-56"></a>Сводка: новые возможности в 5,6

* Поддержка предварительных пакетов с плавающими версиями. `Version="*-*"`, `Version="1.*-*"` и аналогичные данные с плавающей запятой до последних версий, включая предварительные версии, в пределах указанного диапазона — [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>Исправления в этом выпуске

**Появились**

* `nuget push *.nupkg`завершается ошибкой, если снупкг не существует — [#8148](https://github.com/NuGet/Home/issues/8148)

* И несколько других путей кода, не зависящие от языкового стандарта. Использование RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)

* Производительность: спецификация разгрузки для выгруженных сценариев проекта не должна быть создана в предварительном восстановлении — [#8793](https://github.com/NuGet/Home/issues/8793)

* Восстановление: повышение производительности с помощью кэширования схемы зависимости решений — [#9201](https://github.com/NuGet/Home/issues/9201)

* Пользовательский интерфейс PM не работает для проектов стилей SDK после установки пакета с помощью консоли PM [#9203](https://github.com/NuGet/Home/issues/9203)

* Не удается отобразить внедренный значок в пользовательском интерфейсе PM с локальным веб-каналом пакетов — в зависимости от/VS \- [#9225](https://github.com/NuGet/Home/issues/9225)

* Нужетверсион. Трипарсестрикт () должен возвращать значение false, если не удается выполнить синтаксический анализ — [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`Справка для `-source` , должен предлагать использование имени источника, а не исходного URL-адреса — [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`создает неверное имя источника пакета по умолчанию — [#9277](https://github.com/NuGet/Home/issues/9277)

* Средство чтения с экрана не объявляет о поиске... сообщение при переключении вкладок — [#9307](https://github.com/NuGet/Home/issues/9307)

* Специальные возможности: цвет прямоугольника с фокусом недоступен на вкладках пользовательского интерфейса в темной теме — [#9336](https://github.com/NuGet/Home/issues/9336)

* не удается восстановить NuGet. exe 5,5 с помощью MSBuild 14 или более [#9458](https://github.com/NuGet/Home/issues/9458)

* Не регистрировать время миллисекунд в сообщениях о восстановлении — [#8977](https://github.com/NuGet/Home/issues/8977)

* Сделать Иаутпутконсоле асинхронным — [#9268](https://github.com/NuGet/Home/issues/9268)

* На некоторых языках и региональных параметрах, отличных от английского, отработка версий MSBuild работает плохо. [#9322](https://github.com/NuGet/Home/issues/9322)

* Отсутствует формат по умолчанию для `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Perf: Рестореоператионлогжер имеет ненужное сходство потоков — [#9288](https://github.com/NuGet/Home/issues/9288)

* Автоматическое создание документов для `dotnet nuget` команд — [#9146](https://github.com/NuGet/Home/issues/9146)

* Уровень детализации по умолчанию не должен сообщать о восстановлении NOOP для каждого проекта [#8792](https://github.com/NuGet/Home/issues/8792)

* `-DependencyVersion`Параметр поддержки для `NuGet.exe update` , аналогично команде Install [#7694](https://github.com/NuGet/Home/issues/7694)


**DCR**

* Добавление начальной поддержки для целевой платформы NET 5.0 — [#9584](https://github.com/NuGet/Home/issues/9584)

* Сортировка пакетов по ИДЕНТИФИКАТОРу на вкладке "обновления" пользовательского интерфейса PM — [#9278](https://github.com/NuGet/Home/issues/9278)


**[Список всех проблем, исправленных в этом выпуске — 5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
