---
title: Заметки о выпуске версии NuGet 4.5 RTM
description: Заметки о выпуске для NuGet 4.5 RTM, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432508"
---
# <a name="nuget-45-release-notes"></a>Заметки о выпуске NuGet 4.5

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает в себя [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="summary-whats-new-in-450"></a>Сводка: Новые возможности версии 4.5.0

## <a name="summary-whats-new-in-452"></a>Сводка: Новые возможности версии 4.5.2

* Исправление безопасности: разрешения на файлы, созданные внутри ~/.nuget, слишком открыты [#7673](https://github.com/NuGet/Home/issues/7673)[CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-453"></a>Сводка: Новые возможности версии 4.5.3

* Исправление безопасности: файлы внутри NUPKG могут иметь относительный путь выше каталога NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Известные проблемы

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Проблемы с .NET Standard 2.0, связанные с .NET Framework и NuGet 

Платформа .NET Standard и ее инструментарий были разработаны таким образом, чтобы проекты, предназначенные для .NET Framework 4.6.1, могли использовать пакеты NuGet и проекты, предназначенные для .NET Standard 2.0 или более ранних версий. [В этом документе](https://github.com/dotnet/standard/issues/481) кратко описаны проблемы, связанные с таким сценарием, план их решения, а также обходные пути, которые можно применить в текущем состоянии.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Вы не можете просмотреть, добавить или обновить DotNetCLITools с помощью диспетчера пакетов NuGet.

#### <a name="issue"></a>Проблемы

Диспетчер пакетов NuGet не отображается и не позволяет добавить или обновить DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Обходной путь

DotNetCLIToolReferences нужно изменить вручную в файле проекта.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Изменение требуемой версии .NET Framework может привести к частичному отсутствию данных функции IntelliSense

#### <a name="issue"></a>Проблемы

Если изменить требуемую версию .NET Framework в Visual Studio, вы можете получить неполные данные функции IntelliSense. Это происходит, если использовать PackageReferences в качестве формата диспетчера пакетов. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Обходной путь

Выполните восстановление вручную.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Пакет в проекте .NET Core, который содержит сборку с недопустимой подписью, может инициировать бесконечный цикл восстановления.

#### <a name="issue"></a>Проблемы

Иногда при использовании пакета, содержащего сборку с недопустимой подписью, или при использовании пакета, версия которого задается с помощью параметра DateTime, возникает бесконечный цикл автоматического восстановления пакета [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Обходной путь

Сейчас для этой проблемы не существует обходного решения.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Проблемы, исправленные в рамках NuGet 4.5 RTM

Проблемы, исправленные в NuGet 4.4 RTM, описаны в разделе [Заметки о выпуске NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Функции

- Отключение автоматической отправки пакета символов — [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Ошибки

- [Регрессия] в 15.5p1: Portable0.0 пропускается — [#6105](https://github.com/NuGet/Home/issues/6105)
- Отсутствуют ресурсы в пакетах после восстановления — [#5995](https://github.com/NuGet/Home/issues/5995)
- Поставщики учетных данных подключаемых модулей не работают с URI, содержащими пробелы, — [#5982](https://github.com/NuGet/Home/issues/5982)
- Если не удалось восстановить пакет, ошибка должна присутствовать в выходных данных, даже если включен режим минимальной детализации — [#5658](https://github.com/NuGet/Home/issues/5658)
- dotnet
  - Команда dotnetcore restore на уровне решения не следует ProjectReference, когда для ReferenceOutputAssembly задано значение false, что ведет к случайным сбоям сборки — [#5490](https://github.com/NuGet/Home/issues/5490)
- Автозавершение в PMC неправильно работает с методами объекта — [#4800](https://github.com/NuGet/Home/issues/4800)
- Восстановление nuget.exe завершается с ошибкой при использовании набора инструментов Visual Studio 2015 — [#4713](https://github.com/NuGet/Home/issues/4713)
- Производительность: для создания экземпляра PMC расходуется много ресурсов в Visual Studio 2017 — [#4205](https://github.com/NuGet/Home/issues/4205)
- Медленное получение сведений о зависимостях при низкоскоростном соединении — [#4089](https://github.com/NuGet/Home/issues/4089)
- Команда uninstall-package с параметром -RemoveDependencies завершается ошибкой, если несколько пакетов совместно используют одну зависимость — [#4026](https://github.com/NuGet/Home/issues/4026)
- Финализация NuGet.Core.nupkg для публикации — [#3581](https://github.com/NuGet/Home/issues/3581)
- Пакет NuGet разрешает идентификатор зависимости из имени каталога, когда -IncludeProjectReferences используется для csproj + project.json — [#3566](https://github.com/NuGet/Home/issues/3566)
- Инициализатор типа для "NuGet.ProxyCache" выдал исключение — [#3144](https://github.com/NuGet/Home/issues/3144)
- Проблема с производительностью восстановления NuGet при использовании Kudu — [#3087](https://github.com/NuGet/Home/issues/3087)
- Клиенту пользовательского интерфейса не удается показать ошибки или предупреждения, когда выполняется поиск по большим двоичным объектам регистрации — [#2149](https://github.com/NuGet/Home/issues/2149)
- Команда Get-Packages -Updates создает неправильный запрос — [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Ссылки на проблемы GitHub, исправленные в версии 4.5 RTM

[Список проблем](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
