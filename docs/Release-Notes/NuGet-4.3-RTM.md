---
title: "Заметки о выпуске NuGet 4.3 RTM | Документы Майкрософт"
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: da3bf363-4d9d-446c-b91d-41c4cf6e16a1
description: "Заметки о выпуске для NuGet 4.3 RTM, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры."
keywords: "заметки о выпуске NuGet 4.3 RTM, исправления ошибок, известные проблемы, добавленные функции и запросы на изменение структуры"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: d237c4a29d8a76bba10ff9bb641f2e06329c07a6
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="43-rtm-release-notes"></a>Заметки о выпуске версии 4.3 RTM

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает в себя NuGet 4.3 RTM, который добавляет поддержку новых сценариев, таких как .NET Standard 2.0/.NET Core 2.0, содержит множество исправлений, а также повышает производительность. Кроме того, этот выпуск привносит несколько усовершенствований, таких как поддержка семантического версионирования 2.0.0, интеграция ошибок и предупреждений NuGet в MSBuild и многое другое.

## <a name="known-issues"></a>Известные проблемы

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>Восстановление NuGet может в некоторых случаях считать отключенные источники пакетов включенными.

#### <a name="issue"></a>Проблема.
Следующие методы восстановления в командной строке обрабатывают отключенные источники пакетов как включенные. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (с использованием файла dotnet.exe, поставляемого с VS или пакетом SDK для NetCore 2.0.0)

#### <a name="workaround"></a>Инструкции по решению:
1. Используйте Visual Studio (2017 15.3 или более поздней версии) либо NuGet.exe (4.3.0 или более поздней версии)
1. Удалите отключенный источник и продолжите использовать msbuild или dotnet.exe.
1. Вы можете использовать для своего решения параметр Clear в NuGet.config, а затем задать необходимые для этого решения источники.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>При использовании консоли диспетчера пакетов клавиша ВВОД может не работать

#### <a name="issue"></a>Проблема.
Периодически клавиша ВВОД не работает в консоли диспетчера пакетов. В этом случае проверьте ход исправления и укажите дополнительные сведения для воспроизведения ошибки. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Решение
Перезапустите Visual Studio и откройте консоль управления пакетами перед тем, как открыть решение. Кроме того, попробуйте удалить файл `project.lock.json` и выполнить восстановление еще раз.

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Невозможно просмотреть, добавить или обновить DotNetCLITools с помощью диспетчера пакетов Nuget

#### <a name="issue"></a>Проблема.
Диспетчер пакетов NuGet не отображается и не позволяет добавить или обновить DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Решение
DotNetCLIToolReferences нужно изменить вручную в файле проекта.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Изменение требуемой версии .NET Framework может привести к частичному отсутствию данных функции IntelliSense

#### <a name="issue"></a>Проблема.
Если изменить требуемую версию .NET Framework в Visual Studio, вы можете получить неполные данные функции IntelliSense. Это происходит, если использовать PackageReferences в качестве формата диспетчера пакетов. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Решение
Выполните восстановление вручную.


## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Проблемы, исправленные в рамках NuGet 4.3 RTM

Проблемы, исправленные в NuGet 4.0 RTM, описаны в разделе [Заметки о выпуске NuGet 4.0 RTM](../release-notes/nuget-4.0-RTM.md)

**Функция:**

* Улучшение производительности восстановления NuGet: реализация оптимизированного NoOp для восстановлений из командной строки и VS — [#5080](https://github.com/NuGet/Home/issues/5080)

* NET Core 2.0: интерфейс командной строки VS/Dotnet должен запускаться с использованием имеющейся функциональности NuGet: резервные папки — [#4939](https://github.com/NuGet/Home/issues/4939)

* NET Core 2.0: разрешение пользователям пропускать определенные предупреждения о восстановлении (или повышать их до ошибки) — [#4898](https://github.com/NuGet/Home/issues/4898)

* NET Core 2.0: локализованные сборки в интерфейсе командной строки — [#4896](https://github.com/NuGet/Home/issues/4896)

* NET Core 2.0: регистрация всех предупреждений/ошибок в файле ресурсов (включая PackageTargetFallback) — [#4895](https://github.com/NuGet/Home/issues/4895)

* Включение поддержки TFM: NetStandard2.0, Tizen — [#4892](https://github.com/NuGet/Home/issues/4892)

* Уменьшение числа проектов NuGet.Core и NuGet.Client (а, соответственно, и библиотек DLL) — [#2446](https://github.com/NuGet/Home/issues/2446)

* Добавление возможности помечать предупреждения и ошибки NuGet — [#2395](https://github.com/NuGet/Home/issues/2395)


**Ошибка:**

* msbuild /t:pack завершается с ошибкой "Параметр "DevelopmentDependency" не поддерживается задачей "PackTask"" — [#5584](https://github.com/NuGet/Home/issues/5584)

* Структура каталогов для файлов содержимого становится плоской, если не добавлять разделитель каталогов Windows в конце PackagePath — [#4795](https://github.com/NuGet/Home/issues/4795)

* Проекты NetCore не поддерживают настройку в качестве developmentDependency — [#4694](https://github.com/NuGet/Home/issues/4694)

* RestoreManagerPackage загружается синхронно, что привело к блокировке потока пользовательского интерфейса и взаимоблокировке VS — [#4679](https://github.com/NuGet/Home/issues/4679)

* Команда dotnet Restore (и, соответственно, msbuild /t:restore) пропускает проекты с явной зависимостью от проекта решения — [#4578](https://github.com/NuGet/Home/issues/4578)

* Если решение имеет ссылки, указывающие на один и тот же проект, написанный с разным регистром, восстановление может не работать. Это также влияет на различные относительные пути без различий в регистре — [#4574](https://github.com/NuGet/Home/issues/4574)

* Исполняемые файлы, восстановленные из пакетов NuGet, больше невозможно выполнить с помощью .NET Core 2.0 — [#4424](https://github.com/NuGet/Home/issues/4424)

* NuGet.exe поглощает сведения об исключении при синтаксическом анализе файла решения — [#4411](https://github.com/NuGet/Home/issues/4411)

* Пакет помещает файлы содержимого в неправильное расположение, если ContentTargetFolders содержит пути, заканчивающиеся на "/" в Windows — [#4407](https://github.com/NuGet/Home/issues/4407)

* Не удается восстановить DotNetCliToolReference для пакета инструментов, ориентированного на netcoreapp1.1 — [#4396](https://github.com/NuGet/Home/issues/4396)

* Интерфейс командной строки обновления NuGet оставляет старое условие версии пакета в файле проекта (C++) — [#2449](https://github.com/NuGet/Home/issues/2449)

**Запрос на изменение структуры:**

* Read DotnetCliToolTargetFramework из номинации CPS — [#5397](https://github.com/NuGet/Home/issues/5397)

* Проверка TPMinV должна работать для UWP в стиле pj — [#4763](https://github.com/NuGet/Home/issues/4763)

* Улучшение описания пользовательского интерфейса для пакетов с автоссылками — [#4471](https://github.com/NuGet/Home/issues/4471)

* Функция восстановления NuGet выбирает ресурсы компиляции из раздела времени выполнения. - [#4207](https://github.com/NuGet/Home/issues/4207)

* Помещение диагностики зависимостей в файл блокировок — [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="link-to-github-issues-fixed-in-43-rtm"></a>Ссылка на проблемы GitHub, исправленные в версии 4.3 RTM

[Список проблем](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")