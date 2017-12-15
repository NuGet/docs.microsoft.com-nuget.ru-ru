---
title: "Команда восстановления NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Справочник по команде восстановления nuget.exe"
keywords: "NuGet восстановления ссылок, пакеты команды restore"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a>Команда RESTORE (NuGet CLI)

**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 2.7 +

NuGet 2.7 +: Загружает и устанавливает все пакеты, отсутствующие на `packages` папки.

NuGet 3.3 + с проектами с помощью `project.json`: приводит к возникновению ошибки `project.lock.json` файла и `<project>.nuget.props` файла, при необходимости. (Можно опустить оба файла из системы управления версиями.)

NuGet 4.0 + с проектом, в какой пакет включаются ссылки на файл проекта напрямую: приводит к возникновению ошибки `<project>.nuget.props` файла, при необходимости в `obj` папки. (Можно опустить файл из системы управления версиями.)

В Mac OSX и Linux с CLI на моно восстановление пакетов не поддерживается в формате PackageReference.

## <a name="usage"></a>Использование

```
nuget restore <projectPath> [options]
```

где `<projectPath>` указывает расположение решения, `packages.config` файл, или `project.json` файла. В разделе [примечания](#remarks) ниже поведения подробности.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
| DirectDownload | *(4.0 +)*  Загружает пакеты непосредственно, без заполнения кэши с двоичные файлы и метаданные. |
| DisableParallelProcessing | Отключает восстановление нескольких пакетов в параллельном режиме. |
| FallbackSource | *(3.2 +)*  Список источников пакетов для использования как в случае ошибки в случае, если пакет не найден в основной или источник по умолчанию. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| MSBuildPath | *(4.0 +)*  Указывает путь к MSBuild для команды, переназначает `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Указывает версию MSBuild для использования с помощью этой команды. Поддерживаемые значения: 4, 12, 14, 15. По умолчанию выбирается MSBuild в пути в противном случае по умолчанию наибольшую установленную версию MSBuild. |
| NoCache | Запрещает NuGet с помощью пакетов из кэшей локального компьютера. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Выходной каталог | Указывает папку, в которой устанавливаются пакеты. Если папка не указана, используется текущая папка. |
| PackageSaveMode | Указывает типы файлов для сохранения после установки пакета: один из `nuspec`, `nupkg`, или `nuspec;nupkg`. |
| Пакетыструктура | Эквивалентно `OutputDirectory`. |
| Project2ProjectTimeOut | Время ожидания в секундах для разрешения ссылок проекта на проект. |
| Рекурсивные | *(4.0 +)*  Восстанавливает все ссылки на проекты для проектов UWP и .NET Core. Не применяется для проектов с помощью `packages.config`. |
| RequireConsent | Восстановление пакетов проверяет, включена ли перед загрузкой и установкой пакетов. Дополнительные сведения см. в разделе [восстановление пакетов](../consume-packages/package-restore.md). |
| SolutionDirectory | Указывает папку решения. Не является допустимым при восстановлении пакетами для решения. |
| Исходный код | Указывает список источников пакетов (в виде URL-адреса) для восстановления. Если не указано, команда использует источники, предоставляемые в файлах конфигурации см. в разделе [NuGet Настройка поведения](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Уровень детализации |> указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="remarks"></a>Примечания

Команда восстановления выполняет следующие действия:

1. Определите режим работы команды restore.
    Тип файла projectPath | Поведение
    | --- | --- |
    Решения (папка) | Ищет NuGet `.sln` файл и используется, если элемент найден; в противном случае он приводит к ошибке. `(SolutionDir)\.nuget`используются в качестве начальной папки.
    `.sln`файл | Восстановление пакетов, определенных для этого решения; выдает ошибку, если `-SolutionDirectory` используется. `$(SolutionDir)\.nuget`используются в качестве начальной папки.
    `packages.config`, `project.json`, или файл проекта | Восстановите пакеты, перечисленные в файле, разрешения и установка зависимостей.
    Другие типы файлов | Файл считается `.sln` файл, что и выше; Если не решение, дает NuGet произошла ошибка.
    (projectPath не указан) | — NuGet ищет файлы решения в текущей папке. Если найден один файл, что один используется для восстановления пакетов; Если обнаружены несколько решений, NuGet сообщает об ошибке.
    |-Если отсутствуют файлы решений, NuGet ищет `packages.config` или `project.json` и использует эти данные для восстановления пакетов.
    |-Если отсутствует файл решения `packages.config`, или `project.json` найден, NuGet выдает ошибку.

1. Определите «пакеты», используя следующий порядок приоритета (NuGet выдает ошибку, если найден ни один из этих папок):

    - `%userprofile%\.nuget\packages` Значение в `project.json`.
    - Папка, указанная с `-PackagesDirectory`.
    - `repositoryPath` Значение в`Nuget.Config`
    - Папка, указанная с`-SolutionDirectory`
    - `$(SolutionDir)\packages`

1. При восстановлении пакетами для решения, NuGet выполняет следующие задачи.
    - Загружает файл решения.
    - Восстанавливает уровня пакеты решения, перечисленные в `$(SolutionDir)\.nuget\packages.config` в `packages` папки.
    - Восстановить пакеты, перечисленные в `$(ProjectDir)\packages.config` в `packages` папки. Для каждого указанного пакета, восстановление пакета в параллельном режиме, если `-DisableParallelProcessing` указано.

## <a name="examples"></a>Примеры

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
