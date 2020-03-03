---
title: Команда сетапикэй интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe сетапикэй
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231231"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="36cb1-103">Команда сетапикэй (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="36cb1-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="36cb1-104">Область **применения:** использование пакетов, публикация &bullet; **Поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="36cb1-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="36cb1-105">Сохраняет ключ API для указанного URL-адреса сервера в `NuGet.Config`, чтобы его не нужно было указывать для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="36cb1-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="36cb1-106">Использование</span><span class="sxs-lookup"><span data-stu-id="36cb1-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="36cb1-107">где `<source>` идентифицирует сервер, а `<key>` — ключ для сохранения.</span><span class="sxs-lookup"><span data-stu-id="36cb1-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="36cb1-108">Если `<source>` опущен, предполагается nuget.org.</span><span class="sxs-lookup"><span data-stu-id="36cb1-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="36cb1-109">Ключ API не используется для проверки подлинности в частном веб-канале.</span><span class="sxs-lookup"><span data-stu-id="36cb1-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="36cb1-110">Инструкции по управлению учетными данными для проверки подлинности в источнике см. в разделе [`nuget sources`](../cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="36cb1-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="36cb1-111">Ключи API можно получить с отдельных серверов NuGet.</span><span class="sxs-lookup"><span data-stu-id="36cb1-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="36cb1-112">Чтобы создать Апикэйс для nuget.org и управлять им, см. [раздел Publish-API-Key](../../quickstart/includes/publish-api-key.md) .</span><span class="sxs-lookup"><span data-stu-id="36cb1-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="36cb1-113">Параметры</span><span class="sxs-lookup"><span data-stu-id="36cb1-113">Options</span></span>

| <span data-ttu-id="36cb1-114">Параметр</span><span class="sxs-lookup"><span data-stu-id="36cb1-114">Option</span></span> | <span data-ttu-id="36cb1-115">Описание</span><span class="sxs-lookup"><span data-stu-id="36cb1-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36cb1-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="36cb1-116">ConfigFile</span></span> | <span data-ttu-id="36cb1-117">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="36cb1-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="36cb1-118">Если не указано, используется `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="36cb1-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="36cb1-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="36cb1-119">ForceEnglishOutput</span></span> | <span data-ttu-id="36cb1-120">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="36cb1-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="36cb1-121">Справка</span><span class="sxs-lookup"><span data-stu-id="36cb1-121">Help</span></span> | <span data-ttu-id="36cb1-122">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="36cb1-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="36cb1-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="36cb1-123">NonInteractive</span></span> | <span data-ttu-id="36cb1-124">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="36cb1-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="36cb1-125">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="36cb1-125">Verbosity</span></span> | <span data-ttu-id="36cb1-126">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="36cb1-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="36cb1-127">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="36cb1-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="36cb1-128">Примеры</span><span class="sxs-lookup"><span data-stu-id="36cb1-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
