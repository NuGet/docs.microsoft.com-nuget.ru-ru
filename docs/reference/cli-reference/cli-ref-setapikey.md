---
title: Команда сетапикэй интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe сетапикэй
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327611"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="e87b2-103">Команда сетапикэй (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="e87b2-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="e87b2-104">Область **применения:** использование пакетов, публикация &bullet; **поддерживаемых версий:** все</span><span class="sxs-lookup"><span data-stu-id="e87b2-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e87b2-105">Сохраняет ключ API для данного URL-адреса сервера в `NuGet.Config` , чтобы его не нужно было указывать для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="e87b2-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="e87b2-106">Использование</span><span class="sxs-lookup"><span data-stu-id="e87b2-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="e87b2-107">где `<source>` идентифицирует сервер, а `<key>` — ключ или пароль для сохранения.</span><span class="sxs-lookup"><span data-stu-id="e87b2-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="e87b2-108">Если `<source>` аргумент не указан, предполагается NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="e87b2-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="e87b2-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="e87b2-109">Options</span></span>

| <span data-ttu-id="e87b2-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="e87b2-110">Option</span></span> | <span data-ttu-id="e87b2-111">Описание</span><span class="sxs-lookup"><span data-stu-id="e87b2-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e87b2-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e87b2-112">ConfigFile</span></span> | <span data-ttu-id="e87b2-113">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="e87b2-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e87b2-114">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="e87b2-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e87b2-115">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="e87b2-115">ForceEnglishOutput</span></span> | <span data-ttu-id="e87b2-116">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="e87b2-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e87b2-117">Help</span><span class="sxs-lookup"><span data-stu-id="e87b2-117">Help</span></span> | <span data-ttu-id="e87b2-118">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="e87b2-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="e87b2-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e87b2-119">NonInteractive</span></span> | <span data-ttu-id="e87b2-120">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="e87b2-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e87b2-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="e87b2-121">Verbosity</span></span> | <span data-ttu-id="e87b2-122">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="e87b2-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e87b2-123">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e87b2-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e87b2-124">Примеры</span><span class="sxs-lookup"><span data-stu-id="e87b2-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
