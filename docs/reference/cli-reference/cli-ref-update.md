---
title: Команда обновления интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323652"
---
# <a name="update-command-nuget-cli"></a>команда Update (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** для использования пакетов: все

При этом все пакеты в проекте, использующем файл `packages.config`, обновляются до последней доступной версии. Рекомендуется выполнить [инструкцию RESTORE](cli-ref-restore.md) перед запуском `update` . (Чтобы обновить отдельный пакет, используйте [`nuget install`](cli-ref-install.md) без указания номера версии. в этом случае NuGet устанавливает последнюю версию.)

Примечание. не `update` работает с интерфейсом командной строки, работающим под управлением Mono (Mac OSX или Linux) или при использовании формата PackageReference.

`update`Команда также обновляет ссылки на сборки в файле проекта при условии, что эти ссылки уже существуют. Если обновленный пакет содержит добавленную сборку, Новая ссылка *не* добавляется. Для новых зависимостей пакетов также не добавляются ссылки на сборки. Чтобы включить эти операции в состав обновления, обновите пакет в Visual Studio с помощью пользовательского интерфейса диспетчера пакетов или консоли диспетчера пакетов.

Эту команду также можно использовать для обновления nuget.exe, используя флаг *-Self* .

## <a name="usage"></a>Использование

```cli
nuget update <configPath> [options]
```

где `<configPath>` определяет либо `packages.config` файл решения, либо список зависимостей проекта.

## <a name="options"></a>Параметры

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  Указывает версию пакетов зависимостей для использования, которая может быть одной из следующих:<br/><ul><li>*Самый низкий* (по умолчанию): самая низкая версия</li><li>*Хигхестпатч*: версия с наименьшим основным, наименьшим незначительным, самым высоким исправлением</li><li>*Хигхестминор*: версия с наименьшим основным, наибольшим незначительным, самым высоким исправлением</li><li>*Наибольшее*: самая высокая версия</li><li>*Ignore*: пакеты зависимостей не будут использоваться</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Указывает действие по умолчанию, если файл из пакета уже существует в целевом проекте. Установите значение `Overwrite` , чтобы всегда перезаписывать файлы. Задайте для значение `Ignore` , чтобы пропустить файлы.

  `PromptUser`Действие, используемое по умолчанию, запрашивает каждый конфликтующий файл, если не `OverwriteAll` `IgnoreAll` указан параметр или, который будет применяться ко всем оставшимся файлам.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-Id`**

  Указывает список идентификаторов пакетов для обновления.

- **`-MSBuildPath`**

  *(4.0 +)* Указывает путь MSBuild для использования с командой, который имеет приоритет над `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Указывает версию MSBuild, которая будет использоваться с этой командой. Поддерживаемые значения: 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. По умолчанию в пути выбирается MSBuild, в противном случае — по умолчанию — самая высокая установленная версия MSBuild.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-PreRelease`**

  Разрешает обновление до предварительных версий. Этот флаг не требуется при обновлении уже установленных пакетов предварительной версии.

- **`-RepositoryPath`**

  Указывает локальную папку, в которую устанавливаются пакеты.

- **`-Safe`**

  Указывает, что будут установлены только обновления с самой высокой версией в той же основной и дополнительной версии, что и установленный пакет.

- **`-Self`**

  Обновления `nuget.exe` до последней версии. `-Source` можно использовать, но все остальные аргументы игнорируются. Если источник не указан, проверяет наличие `nuget.org` обновлений независимо от `NuGet.Config` параметров.

- **`-Source`**

  Указывает список источников пакетов (в виде URL-адресов), используемых для обновлений. Если этот параметр не указан, команда использует источники, предоставленные в файлах конфигурации, см. раздел [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

- **`-Version`**

  При использовании с одним ИДЕНТИФИКАТОРом пакета указывает версию пакета для обновления.

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
