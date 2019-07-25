---
title: Устарелый формат project.json NuGet
description: Различные части содержимого с project.json удалены из других разделов документации по NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 8d732e87f01c55bde87da0a2e382fd6d509886a3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317016"
---
# <a name="projectjson-archive"></a>Устарелый формат project.json

Формат управления `project.json` впервые появился в NuGet версии 3.x и использовался с определенными типами проектов. Он был объявлен устаревшим с появлением формата PackageReference, в котором зависимости перечислены непосредственно в файле проекта.

См. также:

- [Справочник по файлу project.json](project-json.md)
- [Impact of project.json when creating packages](project-json-impact.md) (Влияние project.json при создании пакетов)
- [project.json и универсальная платформа Windows](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>Формат управления project.json

*Полное описание см. в статье о [восстановлении пакетов](../what-is-nuget.md).*

В списке форматов управления:

- [`project.json`](project-json.md): *(объявлен устаревшим)* JSON-файл, содержащий список зависимостей проекта, при этом общая схема пакета приведена в связанном файле `project.lock.json`. Этот формат объявлен устаревшим в связи с появлением PackageReference.

## <a name="nuget-restore-on-mono"></a>Восстановление NuGet в Mono

*Полное описание см. в статье об [установке клиентских средств NuGet](../install-nuget-client-tools.md).*

Работает с `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Ограничение версий пакетов при восстановлении

*Полное описание см. в статье о [восстановлении пакетов](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*

- `project.json`: укажите диапазон версий непосредственно с номером версии зависимости. Например:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>Команды интерфейса командной строки NuGet

- `nuget install` не работает с `project.json`.
- `nuget restore`: при применении в проектах, использующих `project.json`, создается файл `project.lock.json` и (если необходимо) `<project>.nuget.props`. (Оба эти файла можно опустить в системе управления версиями.) Аргумент `<projectPath>` может указывать на файл `project.json`. При этом поведение аналогично, как при указании на файл `packages.config` или файл проекта. В порядке приоритета для папок пакета перед использованием `project.json` выполняется поиск в `%userprofile%\.nuget\packages`.
- `nuget update`: в Mono эта команда не работает с проектами, использующими `project.json`.

## <a name="dependency-resolution-with-packagereference"></a>Разрешение зависимостей при использовании PackageReference

*Полное описание см. в разделе о [разрешении зависимостей](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*

Поведение PackageReference также применяется к файлу `project.json`. Команда восстановления NuGet записывает схему зависимостей в файл с именем `project.lock.json`, а также `project.json`.

## <a name="managing-dependency-assets"></a>Управление ресурсами зависимостей

*Полное описание см. в разделе о [разрешении зависимостей](../consume-packages/dependency-resolution.md#managing-dependency-assets).*

При использовании формата `project.json` вы можете управлять тем, какие ресурсы из зависимостей переходят в проект верхнего уровня. Дополнительные сведения см. в [справочнике по файлу project.json](project-json.md).

## <a name="excluding-references"></a>Исключение ссылок

*Полное описание см. в разделе о [разрешении зависимостей](../consume-packages/dependency-resolution.md#excluding-references).*

- `project.json`: добавьте `"exclude" : "all"` в зависимость для пакета PackageC:

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>Устранение ошибок с несовместимостью пакетов

*Полное описание см. в разделе о [разрешении зависимостей](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*

Добавленный метод устранения ошибок:

- **Не рекомендуется**: в качестве временной меры, пока вы сотрудничаете с автором пакетов, проекты, ориентированные на `netcore`, `netstandard` и `netcoreapp`, могут обозначать другие платформы как совместимые, тем самым позволяя использовать пакеты, ориентированные на эти платформы. См. разделы [Оператор imports в project.json](project-json.md#imports) и [Целевой объект restore MSBuild в PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback). Это может привести к непредвиденному поведению, поэтому повторим, что лучше всего устранить проблемы совместимости путем сотрудничества с автором пакетов.

## <a name="target-frameworks"></a>Требуемые версии .NET Framework

*Полное описание см. в статье о [требуемых версиях .NET Framework](../reference/target-frameworks.md).*

- [project.json](project-json.md): узел `frameworks` задает версии платформы, для которых может быть скомпилирован пакет.

## <a name="creating-a-package"></a>Создание пакета

*Полное описание см. в статье о [создании пакета](../create-packages/creating-a-package.md).*

### <a name="setting-a-package-type"></a>Указание типа пакета

С .NET Core 1.x при установке пакета DotnetCliTool среда Visual Studio помещает его в узел `project.json` `tools`, а не `dependencies`.

Типы пакетов заданы в файле `project.json`.

- `project.json`: укажите тип пакета в свойстве `packOptions.packageType` файла JSON:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Добавление целевых объектов и свойств MSBuild

*Полное описание см. в статье о [создании пакетов NuGet для платформы .NET Standard с помощью Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

При использовании `project.json` целевые платформы не добавляются в проект, а предоставляются через файл `project.lock.json`.

### <a name="package-versioning"></a>Управление версиями пакета

*Полное описание см. в статье об [управлении версиями пакета](../reference/package-versioning.md).*

При использовании формата `project.json` NuGet также поддерживает применение нотации с использованием подстановочного знака \* для суффикса номера основной, дополнительной, предварительной версии и версии с исправлением.

### <a name="nugetconfig-reference"></a>Справочник по NuGet.Config

*Полное описание см. в [справочнике по NuGet.Config](../reference/nuget-config-file.md).*

`globalPackagesFolder` применяется только к `project.json`. (Применяется к формату PackageReference.)

### <a name="nuspec-file-reference"></a>Справка по NUSPEC-файлу

*Полное описание см. в [справочнике по NUSPEC-файлу](../reference/nuspec.md).*

Элемент `<contentFiles>` используется вместо `<files>` с файлом `project.json`.

### <a name="package-manager-options-control"></a>Управление параметрами диспетчера пакетов

*Полное описание см. в [справочнике по пользовательскому интерфейсу диспетчера пакетов](../consume-packages/install-use-packages-visual-studio.md).*

В проектах, использующих формат управления `project.json`, отображается только параметр **Показать окно предварительного просмотра**.

### <a name="visual-studio-templates"></a>Шаблоны Visual Studio

*Полное описание см. в статье о [пакетах NuGet в шаблонах Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*

Шаблоны не содержат файл `project.json` и не включают в себя ссылки или содержимое, которое следует добавить при установке пакетов NuGet.