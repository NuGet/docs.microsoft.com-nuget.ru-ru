---
title: "Команда источники NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Справочник по nuget.exe источники команды"
keywords: "NuGet источники ссылки, источники команды"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2eca8557840c467a60f5f708efe242cd83609164
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="a86ae-104">Команда источников (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a86ae-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="a86ae-105">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="a86ae-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a86ae-106">Управляет списком источников, расположенных в `%AppData%\NuGet\NuGet.Config` или указанного файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a86ae-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="a86ae-107">Обратите внимание, что URL-адрес источника для nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="a86ae-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="a86ae-108">Использование</span><span class="sxs-lookup"><span data-stu-id="a86ae-108">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="a86ae-109">где `<operation>` является одним из *списка, добавления, удаления, включение, отключение* или *обновление*, `<name>` имя источника, и `<source>` является URL-адрес источника.</span><span class="sxs-lookup"><span data-stu-id="a86ae-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="a86ae-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="a86ae-110">Options</span></span>

| <span data-ttu-id="a86ae-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="a86ae-111">Option</span></span> | <span data-ttu-id="a86ae-112">Описание:</span><span class="sxs-lookup"><span data-stu-id="a86ae-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a86ae-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a86ae-113">ConfigFile</span></span> | <span data-ttu-id="a86ae-114">*(2.5 +)*  NuGet файла конфигурации для применения.</span><span class="sxs-lookup"><span data-stu-id="a86ae-114">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="a86ae-115">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="a86ae-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a86ae-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a86ae-116">ForceEnglishOutput</span></span> | <span data-ttu-id="a86ae-117">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="a86ae-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a86ae-118">Формат</span><span class="sxs-lookup"><span data-stu-id="a86ae-118">Format</span></span> | <span data-ttu-id="a86ae-119">Применяется к `list` действия и может быть `Detailed` (по умолчанию) или `Short`.</span><span class="sxs-lookup"><span data-stu-id="a86ae-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="a86ae-120">Справка</span><span class="sxs-lookup"><span data-stu-id="a86ae-120">Help</span></span> | <span data-ttu-id="a86ae-121">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="a86ae-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="a86ae-122">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="a86ae-122">NonInteractive</span></span> | <span data-ttu-id="a86ae-123">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="a86ae-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a86ae-124">Пароль</span><span class="sxs-lookup"><span data-stu-id="a86ae-124">Password</span></span> | <span data-ttu-id="a86ae-125">Указывает пароль для проверки подлинности с источником.</span><span class="sxs-lookup"><span data-stu-id="a86ae-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="a86ae-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="a86ae-126">StorePasswordInClearText</span></span> | <span data-ttu-id="a86ae-127">Указывает, чтобы сохранить пароль в незашифрованном вместо поведения по умолчанию хранение в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="a86ae-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="a86ae-128">UserName</span><span class="sxs-lookup"><span data-stu-id="a86ae-128">UserName</span></span> | <span data-ttu-id="a86ae-129">Указывает имя пользователя для проверки подлинности с источником.</span><span class="sxs-lookup"><span data-stu-id="a86ae-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="a86ae-130">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="a86ae-130">Verbosity</span></span> | <span data-ttu-id="a86ae-131">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="a86ae-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="a86ae-132">Убедитесь в том, что добавление источников в один и тот же контекст пользователя пароль как nuget.exe впоследствии будет использоваться для доступа к источнику пакета.</span><span class="sxs-lookup"><span data-stu-id="a86ae-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="a86ae-133">Пароль будет сохранен в файле конфигурации зашифрованы и могут быть расшифрованы только в том же контексте пользователя, он был зашифрован.</span><span class="sxs-lookup"><span data-stu-id="a86ae-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="a86ae-134">Так, например при использовании сервера сборки для восстановления пакетов NuGet, который должен быть зашифрован пароль с тем же пользователем Windows, под которой будет выполняться задача построения сервера.</span><span class="sxs-lookup"><span data-stu-id="a86ae-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="a86ae-135">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a86ae-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a86ae-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="a86ae-136">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
