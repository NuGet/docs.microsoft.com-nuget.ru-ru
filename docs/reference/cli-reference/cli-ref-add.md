---
title: Команда интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe Add
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327861"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="f1aff-103">Команда add (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f1aff-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="f1aff-104">Область применения: **Поддерживаемые версии** **для**публикации &bullet; пакетов: 3.3+</span><span class="sxs-lookup"><span data-stu-id="f1aff-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="f1aff-105">Добавляет указанный пакет в источник пакета, отличный от HTTP (путь к папке или UNC-пути) в иерархическом макете, где папки создаются для идентификатора пакета и номера версии.</span><span class="sxs-lookup"><span data-stu-id="f1aff-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="f1aff-106">Например:</span><span class="sxs-lookup"><span data-stu-id="f1aff-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="f1aff-107">При восстановлении или обновлении источника пакета иерархическая структура обеспечивает значительно большую производительность.</span><span class="sxs-lookup"><span data-stu-id="f1aff-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="f1aff-108">Чтобы развернуть все файлы в пакете в источнике целевого пакета, используйте `-Expand` параметр.</span><span class="sxs-lookup"><span data-stu-id="f1aff-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="f1aff-109">Это обычно приводит к появлению дополнительных вложенных папок в месте назначения, таких `tools` как `lib`и.</span><span class="sxs-lookup"><span data-stu-id="f1aff-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="f1aff-110">Использование</span><span class="sxs-lookup"><span data-stu-id="f1aff-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="f1aff-111">где `<packagePath>` — это путь к добавляемому пакету, и `<sourcePath>` указывает источник пакета на основе папки, в который будет добавлен пакет.</span><span class="sxs-lookup"><span data-stu-id="f1aff-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="f1aff-112">Источники HTTP не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="f1aff-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="f1aff-113">Параметры</span><span class="sxs-lookup"><span data-stu-id="f1aff-113">Options</span></span>

| <span data-ttu-id="f1aff-114">Параметр</span><span class="sxs-lookup"><span data-stu-id="f1aff-114">Option</span></span> | <span data-ttu-id="f1aff-115">Описание</span><span class="sxs-lookup"><span data-stu-id="f1aff-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1aff-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f1aff-116">ConfigFile</span></span> | <span data-ttu-id="f1aff-117">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="f1aff-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f1aff-118">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f1aff-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f1aff-119">Expand</span><span class="sxs-lookup"><span data-stu-id="f1aff-119">Expand</span></span> | <span data-ttu-id="f1aff-120">Добавляет все файлы пакета в источник пакета.</span><span class="sxs-lookup"><span data-stu-id="f1aff-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="f1aff-121">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="f1aff-121">ForceEnglishOutput</span></span> | <span data-ttu-id="f1aff-122">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="f1aff-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f1aff-123">Help</span><span class="sxs-lookup"><span data-stu-id="f1aff-123">Help</span></span> | <span data-ttu-id="f1aff-124">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="f1aff-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="f1aff-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f1aff-125">NonInteractive</span></span> | <span data-ttu-id="f1aff-126">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="f1aff-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f1aff-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f1aff-127">Verbosity</span></span> | <span data-ttu-id="f1aff-128">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="f1aff-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f1aff-129">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f1aff-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f1aff-130">Примеры</span><span class="sxs-lookup"><span data-stu-id="f1aff-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
