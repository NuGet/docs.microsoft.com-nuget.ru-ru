---
title: Команда сетапикэй интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe сетапикэй
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383973"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="2e445-103">Команда сетапикэй (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="2e445-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="2e445-104">Область **применения:** использование пакетов, публикация &bullet; **Поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="2e445-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2e445-105">Сохраняет ключ API для указанного URL-адреса сервера в `NuGet.Config`, чтобы его не нужно было указывать для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="2e445-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="2e445-106">Метрики</span><span class="sxs-lookup"><span data-stu-id="2e445-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="2e445-107">где `<source>` идентифицирует сервер, а `<key>` — ключ или пароль для сохранения.</span><span class="sxs-lookup"><span data-stu-id="2e445-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="2e445-108">Если `<source>` опущен, предполагается nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2e445-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

> [!NOTE]
> <span data-ttu-id="2e445-109">Ключ API не используется для проверки подлинности в частном веб-канале.</span><span class="sxs-lookup"><span data-stu-id="2e445-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="2e445-110">Инструкции по управлению учетными данными для проверки подлинности в источнике см. в разделе [`nuget sources`](../cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="2e445-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>

## <a name="options"></a><span data-ttu-id="2e445-111">Options</span><span class="sxs-lookup"><span data-stu-id="2e445-111">Options</span></span>

| <span data-ttu-id="2e445-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="2e445-112">Option</span></span> | <span data-ttu-id="2e445-113">Описание</span><span class="sxs-lookup"><span data-stu-id="2e445-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e445-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2e445-114">ConfigFile</span></span> | <span data-ttu-id="2e445-115">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="2e445-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2e445-116">Если не указано, используется `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="2e445-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2e445-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2e445-117">ForceEnglishOutput</span></span> | <span data-ttu-id="2e445-118">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="2e445-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2e445-119">Справка</span><span class="sxs-lookup"><span data-stu-id="2e445-119">Help</span></span> | <span data-ttu-id="2e445-120">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="2e445-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="2e445-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2e445-121">NonInteractive</span></span> | <span data-ttu-id="2e445-122">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="2e445-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2e445-123">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="2e445-123">Verbosity</span></span> | <span data-ttu-id="2e445-124">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="2e445-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2e445-125">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2e445-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2e445-126">Примеры</span><span class="sxs-lookup"><span data-stu-id="2e445-126">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
