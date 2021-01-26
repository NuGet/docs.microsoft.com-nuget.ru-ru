---
title: Команда восстановления интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Restore
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780036"
---
# <a name="restore-command-nuget-cli"></a>команда Restore (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** для использования пакетов: 2.7 +

Скачивает и устанавливает все пакеты, отсутствующие в `packages` папке. При использовании с NuGet 4.0 + и форматом PackageReference при необходимости создает `<project>.nuget.props` файл в `obj` папке. (Файл можно опустить из системы управления версиями.)

В Mac OSX и Linux с интерфейсом командной строки в Mono восстановление пакетов с помощью PackageReference не поддерживается.

## <a name="usage"></a>Использование

```cli
nuget restore <projectPath> [options]
```

где `<projectPath>` указывает расположение решения или `packages.config` файла. Подробные сведения о поведении см. в разделе [Примечания](#remarks) ниже.

## <a name="options"></a>Варианты

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-DirectDownload`**

  *(4.0 +)* Скачивает пакеты напрямую, не заполняя кэши двоичными файлами или метаданными.

- **`-DisableParallelProcessing`**

   Отключает восстановление нескольких пакетов параллельно.

- **`-FallbackSource`**

  *(3.2 +)* Список источников пакетов, используемых в качестве резервных при условии, что пакет не найден в основном источнике или по умолчанию. Используйте точку с запятой для разделения записей списка.

- **`-Force`**

  В проектах на основе PackageReference принудительно разрешаются все зависимости, даже если последнее восстановление прошло успешно. Установка этого флага аналогична удалению `project.assets.json` файла. Это не позволяет обходить HTTP-кэш.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-ForceEvaluate`**

  Принудительно применяет восстановление, чтобы повторно рассчитать все зависимости, если файл блокировки уже существует.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-LockFilePath`**

  Расположение выходных данных для записи файла блокировки проекта. По умолчанию используется значение `PROJECT_ROOT\packages.lock.json`.

- **`-LockedMode`**

  Не разрешать обновление файла блокировки проекта.

- **`-MSBuildPath`**

   *(4.0 +)* Указывает путь MSBuild для использования с командой, который имеет приоритет над `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Указывает версию MSBuild, которая будет использоваться с этой командой. Поддерживаемые значения: 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. По умолчанию в пути выбирается MSBuild, в противном случае — по умолчанию — самая высокая установленная версия MSBuild.

- **`-NoCache`**

  Предотвращает использование кэшированных пакетов NuGet. См. раздел [Управление глобальными пакетами и папками кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-OutputDirectory`**

  Указывает папку, в которой устанавливаются пакеты. Если папка не указана, используется текущая папка. Требуется при восстановлении с `packages.config` файлом, если не `PackagesDirectory` `SolutionDirectory` используется или.

- **`-PackageSaveMode`**

  Указывает типы файлов, которые необходимо сохранить после установки пакета: один из `nuspec` , `nupkg` или `nuspec;nupkg` .

- **`-PackagesDirectory`**

  Эквивалентно `OutputDirectory`. Требуется при восстановлении с `packages.config` файлом, если не `OutputDirectory` `SolutionDirectory` используется или.

- **`-Project2ProjectTimeOut`**

  Время ожидания в секундах для разрешения ссылок между проектами.

- **`-Recursive`**

  *(4.0 +)* Восстанавливает все проекты ссылок для проектов UWP и .NET Core. Не применяется к проектам с помощью `packages.config` .

- **`-RequireConsent`**

  Проверяет, что восстановление пакетов включено перед загрузкой и установкой пакетов. Дополнительные сведения см. в разделе [восстановление пакетов](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Указывает папку решения. Недопустимый при восстановлении пакетов для решения. Требуется при восстановлении с `packages.config` файлом, если не `PackagesDirectory` `OutputDirectory` используется или.

- **`-Source`**

  Указывает список источников пакетов (в виде URL-адресов), используемых для восстановления. Если этот параметр не указан, команда использует источники, предоставленные в файлах конфигурации, см. раздел [Настройка поведения NuGet](../../consume-packages/configuring-nuget-behavior.md). Используйте точку с запятой для разделения записей списка.

- **`-UseLockFile`**

  Включает создание файла блокировки проекта и использование этого файла при восстановлении.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="remarks"></a>Remarks

Команда Restore выполняет следующие действия.

1. Определите режим работы команды Restore.

   | Тип файла projectPath | Поведение |
   | --- | --- |
   | Решение (папка) | NuGet ищет `.sln` файл и использует его, если он найден; в противном случае выдает ошибку. `(SolutionDir)\.nuget` используется в качестве начальной папки. |
   | Файл `.sln` | Восстановление пакетов, идентифицируемых решением; выдает ошибку, если `-SolutionDirectory` используется. `$(SolutionDir)\.nuget` используется в качестве начальной папки. |
   | `packages.config` или файл проекта | Восстановление пакетов, перечисленных в файле, разрешение и установку зависимостей. |
   | Другой тип файла | Предполагается, что файл является `.sln` файлом, как показано выше. Если это не решение, NuGet выдает ошибку. |
   | (не указано projectPath) | <ul><li>NuGet ищет файлы решений в текущей папке. Если найден один файл, то он используется для восстановления пакетов. Если найдено несколько решений, NuGet выдает ошибку.</li><li>Если файлы решения отсутствуют, NuGet ищет `packages.config` и использует их для восстановления пакетов.</li><li>Если решение или `packages.config` файл не найдены, NuGet выдает ошибку.</ul> |

2. Определите папку Packages, используя следующий порядок приоритета (NuGet выдает ошибку, если ни одна из этих папок не найдена):

    - Папка, указанная в параметре `-PackagesDirectory` .
    - `repositoryPath`Значение в`Nuget.Config`
    - Папка, указанная с помощью `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. При восстановлении пакетов для решения NuGet выполняет следующие действия:
    - Загружает файл решения.
    - Восстанавливает пакеты уровня решения, перечисленные в `$(SolutionDir)\.nuget\packages.config` `packages` папке.
    - Восстановление пакетов, перечисленных в `$(ProjectDir)\packages.config` папке, в `packages` папку. Для каждого указанного пакета восстановите пакет параллельно, если `-DisableParallelProcessing` не указано иное.

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
