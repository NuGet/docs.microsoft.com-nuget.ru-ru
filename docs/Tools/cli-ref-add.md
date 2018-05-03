---
title: Команда add NuGet CLI
description: Справочник по nuget.exe Добавление команды
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a4201a321ffe0f7fb61f4e98012a1a2d7d8fda4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="f76ad-103">Добавьте команду (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f76ad-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="f76ad-104">**Применяется к**: пакета публикации &bullet; **поддерживаемые версии**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="f76ad-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="f76ad-105">Добавляет источник пакетов не HTTP (папка или UNC-путь) в иерархическом виде, в которой будут созданы папки для пакета идентификатор и номер версии указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="f76ad-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="f76ad-106">Пример:</span><span class="sxs-lookup"><span data-stu-id="f76ad-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="f76ad-107">При восстановлении или обновлении к источнику пакета, в иерархическом виде предоставляет значительно повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="f76ad-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="f76ad-108">Чтобы развернуть все файлы в пакете в целевой источник пакета, используйте `-Expand` переключения.</span><span class="sxs-lookup"><span data-stu-id="f76ad-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="f76ad-109">Это обычно приводит дополнительные вложенные папки отображаются в месте назначения, такие как `tools` и `lib`.</span><span class="sxs-lookup"><span data-stu-id="f76ad-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="f76ad-110">Использование</span><span class="sxs-lookup"><span data-stu-id="f76ad-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="f76ad-111">где `<packagePath>` является путем к пакету, чтобы добавить, и `<sourcePath>` указывает источник пакета на основе папок, в которую будет добавляться пакета.</span><span class="sxs-lookup"><span data-stu-id="f76ad-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="f76ad-112">Источники HTTP не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="f76ad-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="f76ad-113">Параметры</span><span class="sxs-lookup"><span data-stu-id="f76ad-113">Options</span></span>

| <span data-ttu-id="f76ad-114">Параметр</span><span class="sxs-lookup"><span data-stu-id="f76ad-114">Option</span></span> | <span data-ttu-id="f76ad-115">Описание</span><span class="sxs-lookup"><span data-stu-id="f76ad-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f76ad-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f76ad-116">ConfigFile</span></span> | <span data-ttu-id="f76ad-117">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="f76ad-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f76ad-118">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="f76ad-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f76ad-119">Expand</span><span class="sxs-lookup"><span data-stu-id="f76ad-119">Expand</span></span> | <span data-ttu-id="f76ad-120">Добавляет все файлы в пакете источника пакета.</span><span class="sxs-lookup"><span data-stu-id="f76ad-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="f76ad-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f76ad-121">ForceEnglishOutput</span></span> | <span data-ttu-id="f76ad-122">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="f76ad-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f76ad-123">Справка</span><span class="sxs-lookup"><span data-stu-id="f76ad-123">Help</span></span> | <span data-ttu-id="f76ad-124">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="f76ad-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="f76ad-125">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="f76ad-125">NonInteractive</span></span> | <span data-ttu-id="f76ad-126">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="f76ad-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f76ad-127">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="f76ad-127">Verbosity</span></span> | <span data-ttu-id="f76ad-128">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="f76ad-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f76ad-129">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f76ad-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f76ad-130">Примеры</span><span class="sxs-lookup"><span data-stu-id="f76ad-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
