---
title: 3.5 заметки о выпуске версии-Кандидата
description: Заметки о выпуске для NuGet 3.5 RC, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548542"
---
# <a name="nuget-35-rc-release-notes"></a>Заметки о выпуске версии-Кандидата NuGet 3.5

[Заметки о выпуске NuGet 3.5 Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-заметки о выпуске RTM](../release-notes/nuget-3.5-RTM.md)

3,5 выпуск ориентирован на повышение качества и производительности клиенты NuGet. Кроме того, мы уже на подходе несколько функций, таких как поддержка [резервные папки](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) поддержки в `.nuspec` и многое другое.

[Список проблем](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Исправления ошибок

* Происходит сбой установки или восстановления пакета с помощью «пакет содержит несколько `.nuspec` файлы.» - [#3231](https://github.com/NuGet/Home/issues/3231)

* пакет NuGet принудительно добавляет `.tt` файлы в папку content, независимо от того, что - [#3203](https://github.com/NuGet/Home/issues/3203)

* csproj пакет NuGet (с `project.json`) вызывает сбой, если нет packOptions и владельца в файле JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* пакет NuGet для `project.json` игнорирует теги packOptions Сводка, авторы, владельцы д - [#3161](https://github.com/NuGet/Home/issues/3161)

* пакет NuGet игнорирует зависимости в выходных данных `.nuspec` для `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Обновление нескольких пакетов с откатом оставляет проект в поврежденном состоянии - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles при любом не добавляются для проектов netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Невозможно упаковать библиотеки, предназначенные для .net Standard правильно - [#3108](https://github.com/NuGet/Home/issues/3108)

* Файл "->" новый проект "->" происходит сбой проекта библиотеки классов (переносимая) в Visual Studio 2015 и Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Ошибка NuGet — 1.0.0-* не является допустимой строкой версии - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package не отображается, однако работает Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Ошибка при «Install-Package jquery.validation» в dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* При установленной Visual STUDIO 2015 с обновлением 3 на виртуальном СЕРВЕРЕ, используемые NuGet, возникает ошибка версии 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* Пользовательский Интерфейс диспетчера пакетов: не отображает новой версии после обновления пакета- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey в командной строке удаления не чтения/отправляется в 3.5.0 бета-версии - [#3037](https://github.com/NuGet/Home/issues/3037)

* Неправильная строка: стабильный выпуск пакета не должен зависеть предварительной зависимость. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Создание проекта переносимой библиотеки Классов (net46 и windows 10), get исключение NullRef. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Обновления NuGet должен предоставить информационное сообщение, если более поздней версии ограничивается ограничению allowedVersions — [#3013](https://github.com/NuGet/Home/issues/3013)

* Подключаемый модуль учетных данных завершил работу с ошибкой -1 / произошла ошибка при загрузке пакета при использовании поставщиков учетных данных с несколькими источниками - [#2885](https://github.com/NuGet/Home/issues/2885)

* пакет NuGet - Newtonsoft.Json отсутствует зависимость пакета - [#2876](https://github.com/NuGet/Home/issues/2876)

* Ошибка в ExecuteSynchronizedCore на Linux и Mac OS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* VS не поддерживает переменные среды в repositoryPath (nuget.exe делает) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Устранить проблемы со специальными возможностями - [#2745](https://github.com/NuGet/Home/issues/2745)

* Переносимые платформы с дефисами профили, будут отклонены. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Диспетчер пакетов NuGet должны содержаться этого списка параметры в пакетах, подробно не применяется к `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0, происходит сбой обновления с помощью "... дополнительное ограничение определенных в packages.config предотвращает эту операцию." - [#1816](https://github.com/NuGet/Home/issues/1816)

* При установке пакета из локального источника, который не существует вызывает исключение поддельное сообщение - [#1674](https://github.com/NuGet/Home/issues/1674)

* Фильтр «Обновить имеющиеся» показывает обновления, которые нарушают ограничение по версии - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Улучшения производительности

* Производительность: Повысить ContentModel target framework синтаксический разбор - [#3162](https://github.com/NuGet/Home/issues/3162)

* Производительность: Избежать чтения `runtime.json` файлы для восстановления, не имеют идентификаторов RID [#3150](https://github.com/NuGet/Home/issues/3150). На компьютерах, CI восстановление пример, в который длительность 15 секунд для 3 сек сокращена веб-приложение ASP.NET.

* Производительность: Время загрузки консоль диспетчера пакетов init.ps1, возникает [#2956](https://github.com/NuGet/Home/issues/2956). В некоторых случаях из 132s 10s улучшение временных показателей открытия PackageManagerConsole.

* Решайте проблемы с производительностью ReSharper в обновлении NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): на пример проекта, чтобы установить пакеты сокращает время из 140s для 68s.

## <a name="dcrs"></a>Запросы на изменение структуры

* NuGet требуются, чтобы пользователи знали, что обновление или установка в dotnet моникера целевой платформы на основе переносимой библиотеки Классов может привести к ошибкам - [#3138](https://github.com/NuGet/Home/issues/3138)

* Предупреждение bad установку или обновление для проекта с tfm = «dotnet» - [#3137](https://github.com/NuGet/Home/issues/3137)

* Добавление поддержки netcoreapp11 и netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Печать содержимого заголовка NuGet предупреждения на консоль в nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* Используйте атрибут AssemblyMetadata для `.nuspec` маркер замены - [#2851](https://github.com/NuGet/Home/issues/2851)

* Удалите заблокированного свойства из файла блокировки - [#2379](https://github.com/NuGet/Home/issues/2379)

* Пакеты символов никогда не следует использовать при установке или обновить #2807

## <a name="features"></a>Функции

* Поддержка папки резервной пакета - [#2899](https://github.com/NuGet/Home/issues/2899)

* Разрабатывать и реализовывать понятие типа пакета для поддержки пакетов средство — [#2476](https://github.com/NuGet/Home/issues/2476)

* API для получения пути к папке установки глобальных пакетов - [#2403](https://github.com/NuGet/Home/issues/2403)

* Собственные пакеты обновления, поддержка — [#1291](https://github.com/NuGet/Home/issues/1291)
