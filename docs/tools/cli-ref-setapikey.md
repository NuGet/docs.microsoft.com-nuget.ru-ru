---
title: Команды интерфейса командной строки NuGet setapikey
description: Справочник по командам setapikey nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549224"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="18bcd-103">Команда setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="18bcd-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="18bcd-104">**Применяется к:** использование пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="18bcd-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="18bcd-105">Сохраняет ключ API для URL-адрес данного сервера в `NuGet.Config` таким образом, чтобы ничего не нужно вводить для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="18bcd-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="18bcd-106">Использование</span><span class="sxs-lookup"><span data-stu-id="18bcd-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="18bcd-107">где `<source>` идентифицирует сервер и `<key>` ключ или пароль для сохранения.</span><span class="sxs-lookup"><span data-stu-id="18bcd-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="18bcd-108">Если `<source>` является опущен, подразумевается nuget.org.</span><span class="sxs-lookup"><span data-stu-id="18bcd-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="18bcd-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="18bcd-109">Options</span></span>

| <span data-ttu-id="18bcd-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="18bcd-110">Option</span></span> | <span data-ttu-id="18bcd-111">Описание</span><span class="sxs-lookup"><span data-stu-id="18bcd-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="18bcd-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="18bcd-112">ConfigFile</span></span> | <span data-ttu-id="18bcd-113">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="18bcd-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="18bcd-114">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="18bcd-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="18bcd-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="18bcd-115">ForceEnglishOutput</span></span> | <span data-ttu-id="18bcd-116">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="18bcd-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="18bcd-117">Справка</span><span class="sxs-lookup"><span data-stu-id="18bcd-117">Help</span></span> | <span data-ttu-id="18bcd-118">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="18bcd-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="18bcd-119">Неинтерактивная</span><span class="sxs-lookup"><span data-stu-id="18bcd-119">NonInteractive</span></span> | <span data-ttu-id="18bcd-120">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="18bcd-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="18bcd-121">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="18bcd-121">Verbosity</span></span> | <span data-ttu-id="18bcd-122">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="18bcd-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="18bcd-123">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="18bcd-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="18bcd-124">Примеры</span><span class="sxs-lookup"><span data-stu-id="18bcd-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
