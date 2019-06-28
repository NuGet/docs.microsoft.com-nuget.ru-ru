---
title: Команда восстановления NuGet CLI
description: Справочник по командам восстановление nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d7a4188de4fb6f812ca19e7f9e302a5a133c58b
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425970"
---
# <a name="restore-command-nuget-cli"></a>Команда RESTORE (NuGet CLI)

**Применяется к:** упаковать потребления &bullet; **поддерживаемые версии:** 2.7+

Загружает и устанавливает все пакеты, отсутствующие на `packages` папки. При использовании NuGet 4.0 + и формата PackageReference, приводит к возникновению ошибки `<project>.nuget.props` файл, при необходимости в `obj` папку. (Можно опустить файл из системы управления версиями.)

В Mac OSX и Linux с помощью интерфейса командной строки в Mono восстановление пакетов не поддерживается с PackageReference.

## <a name="usage"></a>Использование

```cli
nuget restore <projectPath> [options]
```

где `<projectPath>` указывает расположение решения или `packages.config` файл. См. в разделе ["Примечания"](#remarks) ниже поведения сведения.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Чтобы применить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| DirectDownload | *(4.0 и более поздние)*  Загружает пакеты непосредственно, без заполнения кэши с двоичные файлы и метаданные. |
| DisableParallelProcessing | Отключает восстановление нескольких пакетов в параллельном режиме. |
| FallbackSource | *(3.2 и более поздние)*  Список источников пакетов для использования в качестве в случае ошибки в случае, если пакет не найден в первичном или источник по умолчанию. |
| ForceEnglishOutput | *(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Help | Отображает справку для команды. |
| MSBuildPath | *(4.0 и более поздние)*  Указывает путь к MSBuild для использования с командой, имеют приоритет перед `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 и более поздние)*  Указывает версию MSBuild для использования с помощью следующей команды. Поддерживаемые значения: 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9. По умолчанию выбирается MSBuild в пути в противном случае по умолчанию установленных самую новую версию MSBuild. |
| NoCache | Запрещает использовать кэшированные пакеты NuGet. См. в разделе [управление папкой установки глобальных пакетов и папками кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Подавление для пользователя данные или подтверждения. |
| OutputDirectory | Указывает папку, в которой устанавливаются пакеты. Если папка не указана, используется текущая папка. Требуется, если восстановление с помощью `packages.config` файла `PackagesDirectory` или `SolutionDirectory` используется.|
| Использованием PackageSaveMode | Указывает типы файлов для сохранения после установки пакета: один из `nuspec`, `nupkg`, или `nuspec;nupkg`. |
| Пакетыструктура | Эквивалентно `OutputDirectory`. Требуется, если восстановление с помощью `packages.config` файла `OutputDirectory` или `SolutionDirectory` используется. |
| Project2ProjectTimeOut | Время ожидания в секундах для разрешения ссылок проекта на проект. |
| Рекурсивные | *(4.0 и более поздние)*  Восстанавливает все ссылки на проекты для проектов UWP и .NET Core. Не применяется в проектах с помощью `packages.config`. |
| RequireConsent | При восстановлении пакетов проверяет, включена ли перед загрузкой и установкой пакетов. Дополнительные сведения см. в разделе [восстановление пакета](../consume-packages/package-restore.md). |
| SolutionDirectory | Указывает папку решения. Не является допустимым при восстановлении пакетов для решения. Требуется, если восстановление с помощью `packages.config` файла `PackagesDirectory` или `OutputDirectory` используется. |
| Source | Указывает список источников пакетов (в качестве URL-адреса) для восстановления. Если не указано, команда использует эти источники, в файлах конфигурации, см. в разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

Также см. в разделе [переменные среды](cli-ref-environment-variables.md)

## <a name="remarks"></a>Примечания

Команда восстановления выполняет следующие действия:

1. Определите режим работы команды restore.

   | Тип файла projectPath | Поведение |
   | --- | --- |
   | Решения (папка) | NuGet ищет `.sln` файл и используется, если элемент найден; в противном случае выдает ошибку. `(SolutionDir)\.nuget` используется в качестве начальной папки. |
   | `.sln` Файл | Восстановите пакеты, идентифицируемый решения; выдает ошибку, если `-SolutionDirectory` используется. `$(SolutionDir)\.nuget` используется в качестве начальной папки. |
   | `packages.config` или файл проекта | Восстановите пакеты, перечисленные в файле, разрешение и установку зависимостей. |
   | Другие типы файлов | Файл считается `.sln` файл, как описано выше; Если это не решение, NuGet дает ошибку. |
   | (projectPath не указан) | <ul><li>NuGet ищет файлы решения в текущей папке. При обнаружении одного файла, что один используется для восстановления пакетов; Если обнаружены несколько решений, NuGet выдает ошибку.</li><li>Если нет файлов решения, NuGet ищет `packages.config` и использует его для восстановления пакетов.</li><li>Если ни одно решение или `packages.config` файл найден, NuGet выдает ошибку.</ul> |

2. Определите папку пакетов, используя следующий порядок приоритета (NuGet выдает ошибку при обнаружении ни один из этих папок):

    - Папка, указанная с `-PackagesDirectory`.
    - `repositoryPath` Значение в `Nuget.Config`
    - Папка, указанная с помощью `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. При восстановлении пакетов для решения, NuGet выполняет следующее:
    - Загружает файл решения.
    - Восстанавливает пакеты уровня решения, перечисленные в `$(SolutionDir)\.nuget\packages.config` в `packages` папку.
    - Восстановить пакеты, перечисленные в `$(ProjectDir)\packages.config` в `packages` папку. Для каждого пакета, указанного, восстановить этот пакет в параллельном режиме, если не `-DisableParallelProcessing` указан.

## <a name="examples"></a>Примеры

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
