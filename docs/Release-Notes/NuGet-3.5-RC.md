---
title: 3.5 заметки о выпуске версии-Кандидата
description: Заметки о выпуске для RC NuGet 3.5, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d620a8b8d97f9a52cb2bc93a91eb393130a42898
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-35-rc-release-notes"></a>Заметки о выпуске версии-Кандидата NuGet 3.5

[Заметки о выпуске бета 2 3.5 NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM заметки о выпуске](../release-notes/nuget-3.5-RTM.md)

3.5 выпуск предназначен для повышения качества и производительности клиентах NuGet. Кроме того, мы доставленные несколько функций, таких как поддержка [резервной папки](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) поддержки в `.nuspec` и многое другое.

[Список проблем](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Исправления ошибок

* Сбой установки или восстановления пакета с «пакет содержит несколько `.nuspec` файлы.» - [#3231](https://github.com/NuGet/Home/issues/3231)

* пакет NuGet принудительно добавляет `.tt` файлы в папку контента, независимо от того, что - [#3203](https://github.com/NuGet/Home/issues/3203)

* csproj пакет NuGet (с `project.json`) аварийно завершает работу при наличии не packOptions и владельцем в файле JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* пакет NuGet для `project.json` игнорирует теги packOptions Сводка, авторов, владельцев и т. д - [#3161](https://github.com/NuGet/Home/issues/3161)

* пакет NuGet не учитывает зависимости в выходных данных `.nuspec` для `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Обновление нескольких пакетов с помощью отката оставляет проект в поврежденном состоянии - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles при выполнении любого не добавляются для проектов моникеров netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Невозможно упаковать библиотеки, предназначенные для .net Standard правильно - [#3108](https://github.com/NuGet/Home/issues/3108)

* Файл -> Новый проект библиотеки классов (переносимая) проекта завершается с ошибкой VS2015 и Dev15 - "->" [#3094](https://github.com/NuGet/Home/issues/3094)

* Ошибка nuGet - 1.0.0-* не является допустимой строкой версии - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package не отображается, однако works Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Ошибка при «Install-Package jquery.validation» на dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* При установленной VS 2015 с обновлением 3 на виртуальном СЕРВЕРЕ, используемые NuGet, возникает ошибка версии 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* Пакет пользовательского интерфейса диспетчера: не отображает новые версии после обновления пакета- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey в командной строке удаления не чтения и отправляется в 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Неправильная строка: стабильный выпуск пакета не должен зависеть предварительной зависимостей. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Создание проекта PCL (net46 и windows 10) get NullRef исключение. - [#3014](https://github.com/NuGet/Home/issues/3014)

* NuGet обновления должен предоставить информационное сообщение, когда более поздняя версия ограничен ограничением значение allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Подключаемый модуль учетных данных завершился с ошибкой -1 / Ошибка загрузки пакета при использовании поставщиков учетных данных с несколькими источниками - [#2885](https://github.com/NuGet/Home/issues/2885)

* пакет NuGet - зависимость пакета отсутствует Newtonsoft.Json - [#2876](https://github.com/NuGet/Home/issues/2876)

* Ошибка в ExecuteSynchronizedCore на Linux или MacOS + моно - [#2860](https://github.com/NuGet/Home/issues/2860)

* VS не поддерживает переменные среды в repositoryPath (nuget.exe делает) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Устранение проблемы доступа - [#2745](https://github.com/NuGet/Home/issues/2745)

* Переносимый платформы с дефисами профилей, отклоняются. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Диспетчер пакетов NuGet должны содержаться этого списка параметры в пакетах, подробно не применяется к `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 при попытке установить "дополнительное ограничение... определенные в packages.config предотвращает эту операцию." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Установка пакета из локального источника, не существует вызывает поддельное сообщение — [#1674](https://github.com/NuGet/Home/issues/1674)

* «Обновление тупные» отображаются обновления, которые нарушают ограничения версии - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Улучшения производительности

* Производительность: Повысить ContentModel target framework синтаксический разбор - [#3162](https://github.com/NuGet/Home/issues/3162)

* Производительность: Избегайте чтения `runtime.json` файлы для восстановления, которые не имеют идентификаторов RID [#3150](https://github.com/NuGet/Home/issues/3150). На компьютерах CI восстановление образец веб-приложения ASP.NET сжать через 15 секунд для 3 сек.

* Производительность: Время загрузки консоль диспетчера пакетов init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956). В некоторых случаях 132s десятках Повышение времени, чтобы открыть PackageManagerConsole.

* Устранить проблемы с производительностью ReSharper в обновлении NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): В образец проекта, чтобы установить пакеты сокращает время из 140s для 68s.

## <a name="dcrs"></a>Запросы на изменение структуры

* NuGet необходимо сообщить пользователям, обновление или установка в tfm dotnet, в основе PCL может привести к ошибкам - [#3138](https://github.com/NuGet/Home/issues/3138)

* Предупреждать неправильный установку или обновление для проекта с tfm = «dotnet» - [#3137](https://github.com/NuGet/Home/issues/3137)

* Добавление поддержки netcoreapp11 и netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Печать содержимого заголовка NuGet предупреждения на консоль в nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* Использование атрибута AssemblyMetadata для `.nuspec` токен замены - [#2851](https://github.com/NuGet/Home/issues/2851)

* Удалите свойство заблокированные из файла блокировки - [#2379](https://github.com/NuGet/Home/issues/2379)

* Пакеты символов никогда не следует использовать в установку или обновление #2807

## <a name="features"></a>Функции

* Поддержка пакета резервной папки - [#2899](https://github.com/NuGet/Home/issues/2899)

* Разрабатывать и реализовывать понятие типа пакета для поддержки пакетов средство - [#2476](https://github.com/NuGet/Home/issues/2476)

* API-Интерфейс для получения пути к папке глобального пакетов - [#2403](https://github.com/NuGet/Home/issues/2403)

* Поддержка - обновлений пакетов машинного кода [#1291](https://github.com/NuGet/Home/issues/1291)
