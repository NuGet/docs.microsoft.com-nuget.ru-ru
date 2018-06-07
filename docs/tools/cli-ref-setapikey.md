---
title: Команда setapikey NuGet CLI
description: Справочник по командной setapikey nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817688"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="42929-103">Команда setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="42929-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="42929-104">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="42929-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="42929-105">Сохраняет ключ API для URL-адрес данного сервера в `NuGet.Config` , чтобы его не нужно вводить для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="42929-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="42929-106">Использование</span><span class="sxs-lookup"><span data-stu-id="42929-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="42929-107">где `<source>` определяет сервер и `<key>` ключа или пароля для сохранения.</span><span class="sxs-lookup"><span data-stu-id="42929-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="42929-108">Если `<source>` — этот параметр опущен, подразумевается nuget.org.</span><span class="sxs-lookup"><span data-stu-id="42929-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="42929-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="42929-109">Options</span></span>

| <span data-ttu-id="42929-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="42929-110">Option</span></span> | <span data-ttu-id="42929-111">Описание:</span><span class="sxs-lookup"><span data-stu-id="42929-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="42929-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="42929-112">ConfigFile</span></span> | <span data-ttu-id="42929-113">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="42929-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="42929-114">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="42929-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="42929-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="42929-115">ForceEnglishOutput</span></span> | <span data-ttu-id="42929-116">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="42929-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="42929-117">Справка</span><span class="sxs-lookup"><span data-stu-id="42929-117">Help</span></span> | <span data-ttu-id="42929-118">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="42929-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="42929-119">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="42929-119">NonInteractive</span></span> | <span data-ttu-id="42929-120">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="42929-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="42929-121">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="42929-121">Verbosity</span></span> | <span data-ttu-id="42929-122">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="42929-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="42929-123">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="42929-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="42929-124">Примеры</span><span class="sxs-lookup"><span data-stu-id="42929-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
