---
title: Заметки о выпуске 3,5 RC
description: Заметки о выпуске для версии-КАНДИДАТа NuGet 3,5, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780202"
---
# <a name="nuget-35-rc-release-notes"></a>Заметки о выпуске для версии-КАНДИДАТа NuGet 3,5

[Заметка о выпуске NuGet 3,5 — бета-версия](../release-notes/nuget-3.5-Beta2.md)  |  [Заметки о выпуске NuGet 3,5-RTM](../release-notes/nuget-3.5-RTM.md)

выпуск 3,5 предназначен для повышения качества и производительности клиентов NuGet. Кроме того, мы отгрузили несколько функций, таких как поддержка [резервных папок](https://github.com/NuGet/Home/issues/2899), поддержка [PackageType](https://github.com/NuGet/Home/issues/2476) в `.nuspec` и многое другое.

[Список проблем](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Исправления ошибок

* Установка или восстановление пакета завершается ошибкой с "пакет содержит несколько `.nuspec` файлов". - [#3231](https://github.com/NuGet/Home/issues/3231)

* пакет NuGet принудительно добавляет `.tt` файлы в папку содержимого независимо от того, что [#3203](https://github.com/NuGet/Home/issues/3203)

* `project.json`Если в JSON-файле нет паккоптионс и владельца, то пакет NuGet Pack CSPROJ (с) завершается сбоем. [#3180](https://github.com/NuGet/Home/issues/3180)

* пакет NuGet для `project.json` игнорирует теги паккоптионс, такие как Summary, authors, Owners и т. д. [#3161](https://github.com/NuGet/Home/issues/3161)

* пакет NuGet игнорирует зависимости в выходных данных `.nuspec` для `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Обновление нескольких пакетов с помощью отката оставляет проект в неработающем состоянии — [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles не добавляются для проектов netstandard — [#3118](https://github.com/NuGet/Home/issues/3118)

* Не удалось правильно упаковать библиотеку .NET Standard, [#3108](https://github.com/NuGet/Home/issues/3108)

* Файл-> создание проекта > библиотеки классов (переносимые) в VS2015 и Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* Ошибка NuGet-1.0.0-* не является допустимой строкой версии — [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package не удается отобразить, но Install-Package Works — [#3068](https://github.com/NuGet/Home/issues/3068)

* Ошибка при выполнении установки-пакета jQuery. Validation на dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* При установке VS 2015 с обновлением 3 на VS, использующем NuGet версии 3.5.0, возникает ошибка. [#3053](https://github.com/NuGet/Home/issues/3053)

* Пользовательский интерфейс диспетчера пакетов: не отображает новую версию после обновления пакета [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey при удалении Командная строка не считывается и не отправляется в 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Неправильная строка: стабильный выпуск пакета не должен иметь предварительную зависимость. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Создание исключения для получения Нуллреф проекта PCL (net46 и Windows 10). - [#3014](https://github.com/NuGet/Home/issues/3014)

* Обновление NuGet должно предоставлять информативное сообщение, если более поздняя версия ограничена ограничением Алловедверсионс- [#3013](https://github.com/NuGet/Home/issues/3013)

* Подключаемый модуль учетных данных завершил работу с ошибкой 1/ошибка при скачивании пакета при использовании поставщиков учетных данных с несколькими источниками [#2885](https://github.com/NuGet/Home/issues/2885)

* пакет NuGet-отсутствует Newtonsoft.Jsдля зависимости пакета — [#2876](https://github.com/NuGet/Home/issues/2876)

* Ошибка в Ексекутесинчронизедкоре в Linux/MacOS + Mono- [#2860](https://github.com/NuGet/Home/issues/2860)

* VS не поддерживает переменные среды в Репоситорипас (nuget.exe) — [#2763](https://github.com/NuGet/Home/issues/2763)

* Устранение проблем с специальными возможностями — [#2745](https://github.com/NuGet/Home/issues/2745)

* Переносные платформы с профилем переноса переносов отклоняются. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Диспетчер пакетов NuGet должен очистить, что список параметров в сведениях о пакетах не применяется к `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Сбой обновления 3.3.0 NuGet с "дополнительным ограничением... определено в packages.config не разрешает эту операцию. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* При установке пакета из локального источника, который не существует, выдается фиктивное сообщение — [#1674](https://github.com/NuGet/Home/issues/1674)

* Фильтр "доступные для обновления" показывает обновления, нарушающие ограничение версии — [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Повышение производительности

* Производительность: улучшение анализа целевой платформы ContentModel — [#3162](https://github.com/NuGet/Home/issues/3162)

* Производительность. Избегайте чтения `runtime.json` файлов для восстановления, не имеющих [#3150](https://github.com/NuGet/Home/issues/3150)RID. На виртуальных машинах восстановление примера веб-приложения ASP.NET с интервалом от более 15 секунд до 3 секунд.

* Производительность: [#2956](https://github.com/NuGet/Home/issues/2956)время загрузки консоли диспетчера пакетов init.ps1. Время на открытие Паккажеманажерконсоле в некоторых случаях от 132s до 10.

* Устранение проблем с производительностью в обновлении NuGet — [#3044](https://github.com/NuGet/Home/issues/3044): в образце проекта время, затрачиваемое на установку пакетов, уменьшенных с 140S до 68S.

## <a name="dcrs"></a>Запросы на изменение структуры

* NuGet должен уведомить пользователей о том, что обновление или установка в PCL TFM на основе библиотеки, может вызвать проблемы. [#3138](https://github.com/NuGet/Home/issues/3138)

* Предупреждать о неправильной установке или обновлении для проекта w/TFM = "DotNet" — [#3137](https://github.com/NuGet/Home/issues/3137)

* Добавление поддержки netcoreapp11 и netstandard17 — [#2998](https://github.com/NuGet/Home/issues/2998)

* Печать содержимого заголовка NuGet-Warning в консоли в nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)

* Использование атрибута AssemblyMetadata для `.nuspec` замены токенов — [#2851](https://github.com/NuGet/Home/issues/2851)

* Удалите свойство locked из файла блокировки — [#2379](https://github.com/NuGet/Home/issues/2379)

* Пакеты символов никогда не следует использовать при установке или обновлении #2807

## <a name="features"></a>Компоненты

* Поддержка резервных папок пакетов — [#2899](https://github.com/NuGet/Home/issues/2899)

* Разработайте и реализуйте понятие типа пакета для поддержки пакетов средств — [#2476](https://github.com/NuGet/Home/issues/2476)

* API для получения пути к папке глобальных пакетов — [#2403](https://github.com/NuGet/Home/issues/2403)

* Поддержка обновления собственных пакетов — [#1291](https://github.com/NuGet/Home/issues/1291)
