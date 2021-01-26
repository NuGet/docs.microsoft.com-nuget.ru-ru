---
title: Заметки о выпуске 3,5 бета
description: Заметки о выпуске для бета-версии 2 NuGet 3,5, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776396"
---
# <a name="nuget-35-beta2-release-notes"></a>Заметки о выпуске NuGet 3,5 для версии 2

[NuGet 3,5 — заметки о](../release-notes/nuget-3.5-Beta.md)  |  выпуске бета-версии [NuGet 3,5 — заметки о выпуске RC](../release-notes/nuget-3.5-RC.md)

Бета-версия 2 пакета NuGet 3,5 RTM была выпущена 27 июня 2016 для Visual Studio 2013 и nuget.exe

[Полный журнал изменений](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Список проблем](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Исправления ошибок

* В .NET Core для веб-каналов, прошедших проверку подлинности, изменено сообщение об ошибке с нехваткой поддержки декрпитион паролей. [#2942](https://github.com/NuGet/Home/issues/2942)

* Get-Package консоли диспетчера пакетов завершается сбоем, если проект .NET Core открыт, [#2932](https://github.com/NuGet/Home/issues/2932)

* Исправление неправильной обработки 403 в команде NuGet Push [#2910](https://github.com/NuGet/Home/issues/2910)

* Устранение проблем при удалении пакетов в решении, привязанном к системе управления версиями TFS, если Дисаблесаурцеконтролинтегратион имеет значение true- [#2739](https://github.com/NuGet/Home/issues/2739)

* Исправление обновления пакета для учета нецелевых пакетов — [#2724](https://github.com/NuGet/Home/issues/2724)

* Используйте уровень детализации MSBuild, чтобы задать уровень ведения журнала для действий пользовательского интерфейса диспетчера пакетов NuGet — [#2705](https://github.com/NuGet/Home/issues/2705)

* Исправление ошибки конфигурации NuGet недопустимо в проектах веб-сайтов — Visual Studio 2015 VSIX (v 3.4.3) — [#2667](https://github.com/NuGet/Home/issues/2667)

* Устранение проблем с пакетами в `.csproj` случае включения файлов содержимого [#2658](https://github.com/NuGet/Home/issues/2658)

* Дефаултпушсаурце в `NuGetDefaults.Config` ( `ProgramData\NuGet` ) не работает — [#2653](https://github.com/NuGet/Home/issues/2653)

* Исправление проблемы в выпуске NuGet 3.4.3. значение не может быть null при создании пакета — [#2648](https://github.com/NuGet/Home/issues/2648)

* Инструкция RESTORE использует сохраненные учетные данные из Nuget.Config для веб-каналов VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)

* Производительность — устранение чрезмерного выделения памяти в версии компарсион Code — [#2632](https://github.com/NuGet/Home/issues/2632)

* Устранение проблем, возникающих, когда несколько экземпляров nuget.exe пытаются установить один и тот же пакет параллельно [#2628](https://github.com/NuGet/Home/issues/2628)

* Сведения о зависимостях кэша производительности для операций с несколькими проектами [#2619](https://github.com/NuGet/Home/issues/2619)

* Устранена проблема, из-за которой невозможно добавить источники пакетов из параметров, если исходный список пуст — [#2617](https://github.com/NuGet/Home/issues/2617)

* Исправьте ошибочную ошибку при попытке установить пакет, зависящий от интерфейсов времени разработки, [#2594](https://github.com/NuGet/Home/issues/2594)

* Установка пакета из консоли PackageManager с параметром "ALL" пытается только первый источник — [#2557](https://github.com/NuGet/Home/issues/2557)

* Устранение проблем с пакетами, имеющими файлы со временем записи в будущем (моно) — [#2518](https://github.com/NuGet/Home/issues/2518)

* Отображать исключение при сбое поиска проектов в команде Update [#2418](https://github.com/NuGet/Home/issues/2418)

* Содержимое пакета не восстанавливается надлежащим образом при установке пакета из канала NuGet v 3.3 + с аргументом-with, если пакет содержит `.nupkg` файлы — [#2354](https://github.com/NuGet/Home/issues/2354)

* Устранить проблему с установкой пакета (все источники), если пакет отсутствует в 1 Источник — [#2322](https://github.com/NuGet/Home/issues/2322)

* Установка блокируется, если один источник не проходит авторизацию [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` диапазон версий должен переопределять Инклудереференцедпрожектс Version- [#1983](https://github.com/NuGet/Home/issues/1983)

* Сбой обновления 3.3.0 NuGet с "дополнительным ограничением... определено в packages.config не разрешает эту операцию. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe обновление удаляет строгое имя сборки и частный атрибут. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Устранение проблем с относительным путем к файлу для "Дефаултпушсаурце" — [#1746](https://github.com/NuGet/Home/issues/1746)

* Улучшение сообщений об ошибках распознавателя обновлений — [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Изменения в возможностях и работе

* nuget.exe параметр времени ожидания push-уведомлений не работает [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exeное восстановление не создает `.props` и `.targets` файлы для `.nuproj` проектов (регрессия в v 3.4.3.855) — [#2711](https://github.com/NuGet/Home/issues/2711)

* Требуется API расширяемости для сравнения платформ с Imports- [#2633](https://github.com/NuGet/Home/issues/2633)

* Скрывать параметры зависимости при использовании `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Вывод заголовка nuget.exe версии в подробных выходных данных — [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet должен добавить поддержку для/рунтимес/{Рид}/нативеассетс/{ТКСМ}/- [#2782](https://github.com/NuGet/Home/issues/2782)