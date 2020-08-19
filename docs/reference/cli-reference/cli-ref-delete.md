---
title: Команда удаления интерфейса командной строки NuGet
description: Ссылка на команду nuget.exe Delete
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622867"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="07e48-103">команда Delete (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="07e48-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="07e48-104">Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: все</span><span class="sxs-lookup"><span data-stu-id="07e48-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="07e48-105">Удаляет пакет из источника пакета или выводит из него список.</span><span class="sxs-lookup"><span data-stu-id="07e48-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="07e48-106">Для nuget.org команда Delete удаляет [из списка пакет](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="07e48-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="07e48-107">Использование</span><span class="sxs-lookup"><span data-stu-id="07e48-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="07e48-108">где `<packageID>` и `<packageVersion>` выявление точного пакета, который нужно удалить или отменить из списка.</span><span class="sxs-lookup"><span data-stu-id="07e48-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="07e48-109">Точное поведение зависит от источника.</span><span class="sxs-lookup"><span data-stu-id="07e48-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="07e48-110">Например, для локальных папок пакет удаляется. для nuget.org пакет не входит в список.</span><span class="sxs-lookup"><span data-stu-id="07e48-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="07e48-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="07e48-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="07e48-112">Ключ API для целевого репозитория.</span><span class="sxs-lookup"><span data-stu-id="07e48-112">The API key for the target repository.</span></span> <span data-ttu-id="07e48-113">Если он отсутствует, используется указанный в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="07e48-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="07e48-114">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="07e48-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="07e48-115">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="07e48-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="07e48-116">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="07e48-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="07e48-117">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="07e48-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="07e48-118">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="07e48-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="07e48-119">Не выводить запрос при удалении.</span><span class="sxs-lookup"><span data-stu-id="07e48-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="07e48-120">**`-NoServiceEndpoint`** Не добавляет "API/v2/Packages" к исходному URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="07e48-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="07e48-121">Определяет URL-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="07e48-121">Specifies the server URL.</span></span> <span data-ttu-id="07e48-122">URL-адрес для nuget.org — `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="07e48-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="07e48-123">Для частных веб-каналов замените имя узла, например, *% HostName%/API/V3*.</span><span class="sxs-lookup"><span data-stu-id="07e48-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="07e48-124">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="07e48-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="07e48-125">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="07e48-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="07e48-126">Примеры</span><span class="sxs-lookup"><span data-stu-id="07e48-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
