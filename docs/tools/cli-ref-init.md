---
title: Команды интерфейса командной строки NuGet init
description: Справочник по командам init nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551414"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="0b411-103">команда init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0b411-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="0b411-104">**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="0b411-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="0b411-105">Копирует все пакеты из папки на жестком диске в папку назначения, с помощью иерархического представления, как описано для [добавьте команду](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="0b411-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="0b411-106">То есть с помощью `init` равнозначно использованию `add` на каждый пакет в папке.</span><span class="sxs-lookup"><span data-stu-id="0b411-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="0b411-107">Как и в `add`, назначением должна быть локальная папка или UNC-пути; Репозиториями пакетов HTTP, например nuget.org или частные серверы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="0b411-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="0b411-108">Использование</span><span class="sxs-lookup"><span data-stu-id="0b411-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="0b411-109">где `<source>` — это папка, содержащая пакеты и `<destination>` — это локальная папка или путь UNC, в который копируются пакеты.</span><span class="sxs-lookup"><span data-stu-id="0b411-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="0b411-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="0b411-110">Options</span></span>

| <span data-ttu-id="0b411-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="0b411-111">Option</span></span> | <span data-ttu-id="0b411-112">Описание</span><span class="sxs-lookup"><span data-stu-id="0b411-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0b411-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0b411-113">ConfigFile</span></span> | <span data-ttu-id="0b411-114">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="0b411-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0b411-115">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="0b411-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0b411-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0b411-116">ForceEnglishOutput</span></span> | <span data-ttu-id="0b411-117">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="0b411-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0b411-118">Expand</span><span class="sxs-lookup"><span data-stu-id="0b411-118">Expand</span></span> | <span data-ttu-id="0b411-119">Добавляет все файлы в каждом пакете, который добавляется к источнику пакета; Совпадение с кодом `-Expand` с `add` команды.</span><span class="sxs-lookup"><span data-stu-id="0b411-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="0b411-120">Справка</span><span class="sxs-lookup"><span data-stu-id="0b411-120">Help</span></span> | <span data-ttu-id="0b411-121">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="0b411-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="0b411-122">Неинтерактивная</span><span class="sxs-lookup"><span data-stu-id="0b411-122">NonInteractive</span></span> | <span data-ttu-id="0b411-123">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="0b411-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0b411-124">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="0b411-124">Verbosity</span></span> | <span data-ttu-id="0b411-125">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="0b411-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0b411-126">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0b411-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0b411-127">Примеры</span><span class="sxs-lookup"><span data-stu-id="0b411-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
