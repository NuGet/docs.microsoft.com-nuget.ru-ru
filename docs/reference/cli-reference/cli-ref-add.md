---
title: Команда интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Add
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776093"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="edb5c-103">Команда "Добавить" (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="edb5c-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="edb5c-104">Область **применения**: &bullet; **Поддерживаемые версии** публикации пакетов: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="edb5c-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="edb5c-105">Добавляет указанный пакет в источник пакета, отличный от HTTP (путь к папке или UNC-пути) в иерархическом макете, где папки создаются для идентификатора пакета и номера версии.</span><span class="sxs-lookup"><span data-stu-id="edb5c-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="edb5c-106">Пример:</span><span class="sxs-lookup"><span data-stu-id="edb5c-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="edb5c-107">При восстановлении или обновлении источника пакета иерархическая структура обеспечивает значительно большую производительность.</span><span class="sxs-lookup"><span data-stu-id="edb5c-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="edb5c-108">Чтобы развернуть все файлы в пакете в источнике целевого пакета, используйте `-Expand` параметр.</span><span class="sxs-lookup"><span data-stu-id="edb5c-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="edb5c-109">Это обычно приводит к появлению дополнительных вложенных папок в месте назначения, таких как `tools` и `lib` .</span><span class="sxs-lookup"><span data-stu-id="edb5c-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="edb5c-110">Использование</span><span class="sxs-lookup"><span data-stu-id="edb5c-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="edb5c-111">где `<packagePath>` — это путь к добавляемому пакету, и `<sourcePath>` указывает источник пакета на основе папки, в который будет добавлен пакет.</span><span class="sxs-lookup"><span data-stu-id="edb5c-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="edb5c-112">Источники HTTP не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="edb5c-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="edb5c-113">Варианты</span><span class="sxs-lookup"><span data-stu-id="edb5c-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="edb5c-114">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="edb5c-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="edb5c-115">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="edb5c-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="edb5c-116">Добавляет все файлы пакета в источник пакета.</span><span class="sxs-lookup"><span data-stu-id="edb5c-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="edb5c-117">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="edb5c-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="edb5c-118">Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="edb5c-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="edb5c-119">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="edb5c-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="edb5c-120">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="edb5c-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="edb5c-121">Указывает источник пакета, который представляет собой папку или общий UNC-ресурс, к которому будет добавлен nupkg.</span><span class="sxs-lookup"><span data-stu-id="edb5c-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="edb5c-122">Источники HTTP не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="edb5c-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="edb5c-123">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="edb5c-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="edb5c-124">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="edb5c-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="edb5c-125">Примеры</span><span class="sxs-lookup"><span data-stu-id="edb5c-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
