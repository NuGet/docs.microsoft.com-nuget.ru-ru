---
title: Команда setapikey NuGet CLI | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Справочник по командной setapikey nuget.exe
keywords: Справочник по setapikey NuGet, команда setapikey
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 696ccf9df5af487d3bf75925c1c1e0d1d1bf7f7b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="34c3b-104">Команда setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="34c3b-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="34c3b-105">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="34c3b-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="34c3b-106">Сохраняет ключ API для URL-адрес данного сервера в `NuGet.Config` , чтобы его не нужно вводить для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="34c3b-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="34c3b-107">Использование</span><span class="sxs-lookup"><span data-stu-id="34c3b-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="34c3b-108">где `<source>` определяет сервер и `<key>` ключа или пароля для сохранения.</span><span class="sxs-lookup"><span data-stu-id="34c3b-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="34c3b-109">Если `<source>` — этот параметр опущен, подразумевается nuget.org.</span><span class="sxs-lookup"><span data-stu-id="34c3b-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="34c3b-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="34c3b-110">Options</span></span>

| <span data-ttu-id="34c3b-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="34c3b-111">Option</span></span> | <span data-ttu-id="34c3b-112">Описание</span><span class="sxs-lookup"><span data-stu-id="34c3b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="34c3b-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="34c3b-113">ConfigFile</span></span> | <span data-ttu-id="34c3b-114">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="34c3b-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="34c3b-115">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="34c3b-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="34c3b-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="34c3b-116">ForceEnglishOutput</span></span> | <span data-ttu-id="34c3b-117">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="34c3b-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="34c3b-118">Справка</span><span class="sxs-lookup"><span data-stu-id="34c3b-118">Help</span></span> | <span data-ttu-id="34c3b-119">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="34c3b-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="34c3b-120">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="34c3b-120">NonInteractive</span></span> | <span data-ttu-id="34c3b-121">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="34c3b-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="34c3b-122">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="34c3b-122">Verbosity</span></span> | <span data-ttu-id="34c3b-123">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="34c3b-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="34c3b-124">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="34c3b-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="34c3b-125">Примеры</span><span class="sxs-lookup"><span data-stu-id="34c3b-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
