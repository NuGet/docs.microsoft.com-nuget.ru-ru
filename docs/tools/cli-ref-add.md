---
title: Интерфейс командной строки NuGet добавьте команду
description: Справочник по nuget.exe добавьте команду
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545838"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="43376-103">Команда add (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="43376-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="43376-104">**Применяется к**: Упаковка публикации &bullet; **поддерживаемые версии**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="43376-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="43376-105">Добавляет указанный пакет источник пакетов, отличные от HTTP (папка или UNC-путь) в виде иерархического представления, при котором создаются папки, для номера идентификатора и версии пакета.</span><span class="sxs-lookup"><span data-stu-id="43376-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="43376-106">Пример:</span><span class="sxs-lookup"><span data-stu-id="43376-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="43376-107">При восстановлении или обновлении в источнике пакета, иерархического представления обеспечивает значительно более высокую производительность.</span><span class="sxs-lookup"><span data-stu-id="43376-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="43376-108">Чтобы развернуть все файлы в пакете к источнику пакета назначения, используйте `-Expand` переключения.</span><span class="sxs-lookup"><span data-stu-id="43376-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="43376-109">Это обычно приводит появление в месте назначения, такие как дополнительные подпапки `tools` и `lib`.</span><span class="sxs-lookup"><span data-stu-id="43376-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="43376-110">Использование</span><span class="sxs-lookup"><span data-stu-id="43376-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="43376-111">где `<packagePath>` — это путь к пакету, чтобы добавить, и `<sourcePath>` указывает источник пакетов на основе папки, в которую будут добавлены пакета.</span><span class="sxs-lookup"><span data-stu-id="43376-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="43376-112">HTTP-источники не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="43376-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="43376-113">Параметры</span><span class="sxs-lookup"><span data-stu-id="43376-113">Options</span></span>

| <span data-ttu-id="43376-114">Параметр</span><span class="sxs-lookup"><span data-stu-id="43376-114">Option</span></span> | <span data-ttu-id="43376-115">Описание</span><span class="sxs-lookup"><span data-stu-id="43376-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="43376-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="43376-116">ConfigFile</span></span> | <span data-ttu-id="43376-117">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="43376-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="43376-118">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="43376-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="43376-119">Expand</span><span class="sxs-lookup"><span data-stu-id="43376-119">Expand</span></span> | <span data-ttu-id="43376-120">Добавляет все файлы в пакете к источнику пакета.</span><span class="sxs-lookup"><span data-stu-id="43376-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="43376-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="43376-121">ForceEnglishOutput</span></span> | <span data-ttu-id="43376-122">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="43376-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="43376-123">Справка</span><span class="sxs-lookup"><span data-stu-id="43376-123">Help</span></span> | <span data-ttu-id="43376-124">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="43376-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="43376-125">Неинтерактивная</span><span class="sxs-lookup"><span data-stu-id="43376-125">NonInteractive</span></span> | <span data-ttu-id="43376-126">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="43376-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="43376-127">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="43376-127">Verbosity</span></span> | <span data-ttu-id="43376-128">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="43376-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="43376-129">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="43376-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="43376-130">Примеры</span><span class="sxs-lookup"><span data-stu-id="43376-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
