---
title: "Команда setapikey NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по командной setapikey nuget.exe"
keywords: "Справочник по setapikey NuGet, команда setapikey"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ca6caddbf1404bcaa1ca068c9556f7cf0c651947
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="81838-104">Команда setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="81838-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="81838-105">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="81838-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="81838-106">Сохраняет ключ API для URL-адрес данного сервера в `NuGet.Config` , чтобы его не нужно вводить для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="81838-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="81838-107">Использование</span><span class="sxs-lookup"><span data-stu-id="81838-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="81838-108">где `<source>` определяет сервер и `<key>` ключа или пароля для сохранения.</span><span class="sxs-lookup"><span data-stu-id="81838-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="81838-109">Если `<source>` — этот параметр опущен, подразумевается nuget.org.</span><span class="sxs-lookup"><span data-stu-id="81838-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="81838-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="81838-110">Options</span></span>

| <span data-ttu-id="81838-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="81838-111">Option</span></span> | <span data-ttu-id="81838-112">Описание:</span><span class="sxs-lookup"><span data-stu-id="81838-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="81838-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="81838-113">ConfigFile</span></span> | <span data-ttu-id="81838-114">Файл конфигурации NuGet для изменения.</span><span class="sxs-lookup"><span data-stu-id="81838-114">The NuGet configuration file to modify.</span></span> <span data-ttu-id="81838-115">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="81838-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="81838-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="81838-116">ForceEnglishOutput</span></span> | <span data-ttu-id="81838-117">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="81838-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="81838-118">Справка</span><span class="sxs-lookup"><span data-stu-id="81838-118">Help</span></span> | <span data-ttu-id="81838-119">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="81838-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="81838-120">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="81838-120">NonInteractive</span></span> | <span data-ttu-id="81838-121">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="81838-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="81838-122">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="81838-122">Verbosity</span></span> | <span data-ttu-id="81838-123">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="81838-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="81838-124">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="81838-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="81838-125">Примеры</span><span class="sxs-lookup"><span data-stu-id="81838-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
