---
title: "Команда add NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по nuget.exe Добавление команды"
keywords: "NuGet добавить ссылку, добавьте команду пакета"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70c86f8d240bd308224f6b7887b630cc1e953bf8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="5d04b-104">Добавьте команду (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5d04b-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="5d04b-105">**Применяется к**: пакета публикации &bullet; **поддерживаемые версии**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="5d04b-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="5d04b-106">Добавляет источник пакетов не HTTP (папка или UNC-путь) в иерархическом виде, в которой будут созданы папки для пакета идентификатор и номер версии указанного пакета.</span><span class="sxs-lookup"><span data-stu-id="5d04b-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="5d04b-107">Пример:</span><span class="sxs-lookup"><span data-stu-id="5d04b-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="5d04b-108">При восстановлении или обновлении к источнику пакета, в иерархическом виде предоставляет значительно повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="5d04b-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="5d04b-109">Чтобы развернуть все файлы в пакете в целевой источник пакета, используйте `-Expand` переключения.</span><span class="sxs-lookup"><span data-stu-id="5d04b-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="5d04b-110">Это обычно приводит дополнительные вложенные папки отображаются в месте назначения, такие как `tools` и `lib`.</span><span class="sxs-lookup"><span data-stu-id="5d04b-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="5d04b-111">Использование</span><span class="sxs-lookup"><span data-stu-id="5d04b-111">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="5d04b-112">где `<packagePath>` является путем к пакету, чтобы добавить, и `<sourcePath>` указывает источник пакета на основе папок, в которую будет добавляться пакета.</span><span class="sxs-lookup"><span data-stu-id="5d04b-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="5d04b-113">Источники HTTP не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="5d04b-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="5d04b-114">Параметры</span><span class="sxs-lookup"><span data-stu-id="5d04b-114">Options</span></span>

| <span data-ttu-id="5d04b-115">Параметр</span><span class="sxs-lookup"><span data-stu-id="5d04b-115">Option</span></span> | <span data-ttu-id="5d04b-116">Описание:</span><span class="sxs-lookup"><span data-stu-id="5d04b-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5d04b-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5d04b-117">ConfigFile</span></span> | <span data-ttu-id="5d04b-118">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="5d04b-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5d04b-119">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="5d04b-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span>| 
| <span data-ttu-id="5d04b-120">Expand</span><span class="sxs-lookup"><span data-stu-id="5d04b-120">Expand</span></span> | <span data-ttu-id="5d04b-121">Добавляет все файлы в пакете источника пакета.</span><span class="sxs-lookup"><span data-stu-id="5d04b-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="5d04b-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5d04b-122">ForceEnglishOutput</span></span> | <span data-ttu-id="5d04b-123">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="5d04b-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5d04b-124">Справка</span><span class="sxs-lookup"><span data-stu-id="5d04b-124">Help</span></span> | <span data-ttu-id="5d04b-125">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="5d04b-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="5d04b-126">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="5d04b-126">NonInteractive</span></span> | <span data-ttu-id="5d04b-127">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="5d04b-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5d04b-128">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="5d04b-128">Verbosity</span></span> | <span data-ttu-id="5d04b-129">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="5d04b-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5d04b-130">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5d04b-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5d04b-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="5d04b-131">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
