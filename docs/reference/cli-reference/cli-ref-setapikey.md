---
title: Команда сетапикэй интерфейса командной строки NuGet
description: Справочник по команде nuget.exe сетапикэй
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622815"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="3e33b-103">Команда сетапикэй (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="3e33b-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="3e33b-104">Область **применения:** использование пакетов, публикация &bullet; **поддерживаемых версий:** все</span><span class="sxs-lookup"><span data-stu-id="3e33b-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3e33b-105">Сохраняет ключ API для данного URL-адреса сервера в, `NuGet.Config` чтобы его не нужно было указывать для последующих команд.</span><span class="sxs-lookup"><span data-stu-id="3e33b-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="3e33b-106">Использование</span><span class="sxs-lookup"><span data-stu-id="3e33b-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="3e33b-107">где `<source>` идентифицирует сервер и `<key>` является ключом для сохранения.</span><span class="sxs-lookup"><span data-stu-id="3e33b-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="3e33b-108">Если `<source>` аргумент не указан, предполагается NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="3e33b-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="3e33b-109">Ключ API не используется для проверки подлинности в частном веб-канале.</span><span class="sxs-lookup"><span data-stu-id="3e33b-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="3e33b-110">Инструкции по управлению учетными данными для проверки подлинности в источнике см [ `nuget sources` . в разделе](../cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="3e33b-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="3e33b-111">Ключи API можно получить с отдельных серверов NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e33b-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="3e33b-112">Чтобы создать Апикэйс для nuget.org и управлять им, обратитесь к [разделу Получение API-ключа](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) .</span><span class="sxs-lookup"><span data-stu-id="3e33b-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="3e33b-113">Параметры</span><span class="sxs-lookup"><span data-stu-id="3e33b-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="3e33b-114">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="3e33b-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3e33b-115">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="3e33b-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="3e33b-116">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="3e33b-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="3e33b-117">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="3e33b-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="3e33b-118">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="3e33b-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="3e33b-119">URL-адрес сервера, на котором действителен ключ API.</span><span class="sxs-lookup"><span data-stu-id="3e33b-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="3e33b-120">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="3e33b-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="3e33b-121">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3e33b-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3e33b-122">Примеры</span><span class="sxs-lookup"><span data-stu-id="3e33b-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
