---
title: 3.5 заметки о выпуске бета-версия 2
description: Заметки о выпуске для NuGet 3.5 Beta 2, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551995"
---
# <a name="nuget-35-beta2-release-notes"></a>Заметки о выпуске NuGet 3.5 Beta2

[Заметки о выпуске бета-версии 3.5 NuGet](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC заметки.](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM был выпущен 27 июня 2016 г. для Visual Studio 2013 и nuget.exe

[Полный журнал изменений](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Список проблем](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Исправления ошибок

* Обновленные возвращается сообщение об отсутствие поддержки decrpytion пароль в .NET Core для каналы с проверкой подлинности - [#2942](https://github.com/NuGet/Home/issues/2942)

* Консоль диспетчера пакетов Get-Package завершается неудачей, если открыт проект .NET Core - [#2932](https://github.com/NuGet/Home/issues/2932)

* Устраните 403 неправильной обработкой в команда NuGet push [#2910](https://github.com/NuGet/Home/issues/2910)

* Устранить проблемы при удалении пакетов в решении, привязывается к системе управления версиями TFS, в случае, когда disableSourceControlIntegration задано значение true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Исправление пакета обновления с весовым коэффициентом пакеты без целевой учетной записи - [#2724](https://github.com/NuGet/Home/issues/2724)

* Уровень детализации MSBuild используется для задания уровня ведения журнала для диспетчера пакетов Nuget действий пользовательского интерфейса - [#2705](https://github.com/NuGet/Home/issues/2705)

* Исправление конфигурации NuGet — недопустимый ошибки в проектах веб-сайта — VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* Устранить проблемы с пакетами из `.csproj` Если файлы содержимого включаются - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource в `NuGetDefaults.Config` (`ProgramData\NuGet`) не работает — [#2653](https://github.com/NuGet/Home/issues/2653)

* Проблема устранена в выпуске Nuget 3.4.3 - значение не может иметь значение null, если при создании пакета - [#2648](https://github.com/NuGet/Home/issues/2648)

* Восстановление использует сохраненные учетные данные из Nuget.Config для веб-каналов VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* Производительность - исправление чрезмерное выделение ресурсов в код версии сравнение - [#2632](https://github.com/NuGet/Home/issues/2632)

* Устранение проблем, когда несколько экземпляров nuget.exe пытается установить тот же пакет в параллельном режиме - [#2628](https://github.com/NuGet/Home/issues/2628)

* Производительность - кэша сведений о зависимостях для нескольких проектов operations - [#2619](https://github.com/NuGet/Home/issues/2619)

* Устранить проблему там, где не удается выполнить пакет источников добавляться из параметров при пустом - исходного списка [#2617](https://github.com/NuGet/Home/issues/2617)

* Исправить Дезориентирующие ошибка при попытке установить пакет, который зависит от времени разработки интерфейсов - [#2594](https://github.com/NuGet/Home/issues/2594)

* Установка пакета из консоли PackageManager с параметром «All» пытается только первый источник - [#2557](https://github.com/NuGet/Home/issues/2557)

* Устранение проблем с пакетами, файлы которых со временем записи в будущем (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Отобразить исключение при возникновении сбоя поиск проектов в команду update - [#2418](https://github.com/NuGet/Home/issues/2418)

* Содержимое пакета не восстанавливается правильно при установке пакета из nuget версии 3.3 + веб-канала с аргументом - NoCache Если пакет содержит `.nupkg` файлы — [#2354](https://github.com/NuGet/Home/issues/2354)

* Устранена проблема с пакет установки (всех источников), если отсутствует пакет из источника 1 - [#2322](https://github.com/NuGet/Home/issues/2322)

* Установить блоки, если один источник отказывает в авторизации - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` диапазон должен переопределить - IncludeReferencedProjects version — версия [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0, происходит сбой обновления с помощью "... дополнительное ограничение определенных в packages.config предотвращает эту операцию." - [#1816](https://github.com/NuGet/Home/issues/1816)

* NuGet.exe обновления удаляет строгое имя сборки и закрытый атрибут. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Устранение проблем с относительный путь к файлу для «DefaultPushSource» - [#1746](https://github.com/NuGet/Home/issues/1746)

* Улучшения сообщений о сбое обновления Сопоставитель - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Функции и изменения в поведении

* NuGet.exe push - параметр времени ожидания не работает — [#2785](https://github.com/NuGet/Home/issues/2785)

* NuGet.exe restore не создает `.props` и `.targets` файлы для `.nuproj` проектов (Регрессия в v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Требуется расширяемости API для сравнения платформ с imports - [#2633](https://github.com/NuGet/Home/issues/2633)

* Скрыть параметры зависимости при использовании `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Вывод заголовка версии nuget.exe в подробные выходные данные — [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet должны обеспечить поддержку для /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)