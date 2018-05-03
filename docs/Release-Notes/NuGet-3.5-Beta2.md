---
title: 3.5 заметки о выпуске бета-версия 2
description: Заметки о выпуске, включая известные проблемы, исправленные ошибки, добавленные функции и DCR второй бета-версии 3.5 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08bbae00a3e63c2a1ff42d5cc04981eb02966850
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-35-beta2-release-notes"></a>Заметки о выпуске NuGet 3.5 бета-версия 2

[Заметки о выпуске 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md) | [заметки о выпуске 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 бета-версии 2 RTM был выпущен для Visual Studio 2013 и nuget.exe 27 июня 2016 г.

[Полный журнал изменений](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Список проблем](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Исправления ошибок

* Обновленные возвращается сообщение об отсутствия поддержки decrpytion пароль в .NET Core для прошедших проверку подлинности веб-каналов - [#2942](https://github.com/NuGet/Home/issues/2942)

* Консоль диспетчера пакетов Get-Package завершается сбоем, если открыт проект .NET Core - [#2932](https://github.com/NuGet/Home/issues/2932)

* Исправьте неправильной обработкой 403 в команде принудительной NuGet [#2910](https://github.com/NuGet/Home/issues/2910)

* Устранение проблем в удаление пакетов в решении, привязанный к системе управления версиями TFS при disableSourceControlIntegration задано значение true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Исправьте пакет обновления в пакеты не целевой учетной записи - [#2724](https://github.com/NuGet/Home/issues/2724)

* Позволяет задать уровень ведения журнала для диспетчера пакетов Nuget действия пользовательского интерфейса — уровень детализации MSBuild [#2705](https://github.com/NuGet/Home/issues/2705)

* Исправление конфигурации NuGet — недопустимый ошибка в проекты веб-сайтов - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* Устранение проблемы пакета из `.csproj` при включенных файлов содержимого - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource в `NuGetDefaults.Config` (`ProgramData\NuGet`) не работает — [#2653](https://github.com/NuGet/Home/issues/2653)

* Устранить проблему в выпуске Nuget 3.4.3 - значение не может быть null для создания пакета - [#2648](https://github.com/NuGet/Home/issues/2648)

* Восстановление использует сохраненные учетные данные из Nuget.Config для веб-каналов VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* Производительность - исправление чрезмерного выделения в код версии сравнение - [#2632](https://github.com/NuGet/Home/issues/2632)

* Устранение проблем, когда несколько экземпляров nuget.exe пытается установить тот же пакет параллельно - [#2628](https://github.com/NuGet/Home/issues/2628)

* Производительность - кэша сведений о зависимостях для нескольких проектов операций - [#2619](https://github.com/NuGet/Home/issues/2619)

* Исправьте проблему там, где пакет источники добавлены из параметров при пустом - исходного списка [#2617](https://github.com/NuGet/Home/issues/2617)

* Устранение ошибки Misleading при попытке установить пакет, который зависит от роли внешних разработки - [#2594](https://github.com/NuGet/Home/issues/2594)

* Установка пакета в консоли PackageManager с параметр «All» пытается первого источника - [#2557](https://github.com/NuGet/Home/issues/2557)

* Устранение проблем с пакетами, файлы со временем записи в будущем (моно) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Отображение исключений при сбое поиск проектов в команду update - [#2418](https://github.com/NuGet/Home/issues/2418)

* Содержимое пакета не является правильно восстановить при установке пакета из nuget v3.3 + веб-канала с аргументом - NoCache Если пакет содержит `.nupkg` файлы - [#2354](https://github.com/NuGet/Home/issues/2354)

* Устраните проблему с пакетом установки (все источники), если отсутствует пакет из источника 1 - [#2322](https://github.com/NuGet/Home/issues/2322)

* Установить блоки, если один источник отказывает в авторизации - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` диапазон, должны переопределять версия - IncludeReferencedProjects - версии [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 при попытке установить "дополнительное ограничение... определенные в packages.config предотвращает эту операцию." - [#1816](https://github.com/NuGet/Home/issues/1816)

* NuGet.exe обновления удаляет строгое имя сборки и атрибут Private. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Устранение проблем с относительным путем к файлу для «DefaultPushSource» - [#1746](https://github.com/NuGet/Home/issues/1746)

* Улучшения сообщений о сбое обновления Сопоставитель - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Возможности и изменения в поведении

* Принудительная, NuGet.exe не работает параметр времени ожидания - [#2785](https://github.com/NuGet/Home/issues/2785)

* не позволяет создавать восстановления NuGet.exe `.props` и `.targets` файлы для `.nuproj` проекты (Регрессия в v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Требуется API для сравнения платформы с imports - расширяемости [#2633](https://github.com/NuGet/Home/issues/2633)

* Скрыть параметры зависимостей при использовании `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Распечатать заголовок версии nuget.exe в подробные выходные данные - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet необходимо добавить поддержку /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)