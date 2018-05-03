---
title: Команда setapikey NuGet CLI
description: Справочник по командной setapikey nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 968e22f32e51659590a6fe1e881bf5a9792a1331
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="574d8-103">Команда setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="574d8-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="574d8-104">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="574d8-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="574d8-105">Сохраняет ключ API для URL-адрес данного сервера в `NuGet.Config` , чтобы его не нужно вводить для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="574d8-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="574d8-106">Использование</span><span class="sxs-lookup"><span data-stu-id="574d8-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="574d8-107">где `<source>` определяет сервер и `<key>` ключа или пароля для сохранения.</span><span class="sxs-lookup"><span data-stu-id="574d8-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="574d8-108">Если `<source>` — этот параметр опущен, подразумевается nuget.org.</span><span class="sxs-lookup"><span data-stu-id="574d8-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="574d8-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="574d8-109">Options</span></span>

| <span data-ttu-id="574d8-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="574d8-110">Option</span></span> | <span data-ttu-id="574d8-111">Описание</span><span class="sxs-lookup"><span data-stu-id="574d8-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="574d8-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="574d8-112">ConfigFile</span></span> | <span data-ttu-id="574d8-113">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="574d8-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="574d8-114">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="574d8-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="574d8-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="574d8-115">ForceEnglishOutput</span></span> | <span data-ttu-id="574d8-116">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="574d8-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="574d8-117">Справка</span><span class="sxs-lookup"><span data-stu-id="574d8-117">Help</span></span> | <span data-ttu-id="574d8-118">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="574d8-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="574d8-119">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="574d8-119">NonInteractive</span></span> | <span data-ttu-id="574d8-120">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="574d8-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="574d8-121">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="574d8-121">Verbosity</span></span> | <span data-ttu-id="574d8-122">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="574d8-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="574d8-123">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="574d8-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="574d8-124">Примеры</span><span class="sxs-lookup"><span data-stu-id="574d8-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
