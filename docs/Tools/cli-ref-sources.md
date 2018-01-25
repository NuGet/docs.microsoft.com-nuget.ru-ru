---
title: "Команда источники NuGet CLI | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по nuget.exe источники команды"
keywords: "NuGet источники ссылки, источники команды"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c1cd909c0c35d52f0269d267367669df46f9db55
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="7ef17-104">Команда источников (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7ef17-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="7ef17-105">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="7ef17-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7ef17-106">Управляет списком источников, расположенных в `%AppData%\NuGet\NuGet.Config` или указанного файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7ef17-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="7ef17-107">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="7ef17-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="7ef17-108">Использование</span><span class="sxs-lookup"><span data-stu-id="7ef17-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="7ef17-109">где `<operation>` является одним из *списка, добавления, удаления, включение, отключение* или *обновление*, `<name>` имя источника, и `<source>` является URL-адрес источника.</span><span class="sxs-lookup"><span data-stu-id="7ef17-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="7ef17-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="7ef17-110">Options</span></span>

| <span data-ttu-id="7ef17-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="7ef17-111">Option</span></span> | <span data-ttu-id="7ef17-112">Описание:</span><span class="sxs-lookup"><span data-stu-id="7ef17-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7ef17-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7ef17-113">ConfigFile</span></span> | <span data-ttu-id="7ef17-114">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="7ef17-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7ef17-115">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="7ef17-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="7ef17-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7ef17-116">ForceEnglishOutput</span></span> | <span data-ttu-id="7ef17-117">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="7ef17-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7ef17-118">Формат</span><span class="sxs-lookup"><span data-stu-id="7ef17-118">Format</span></span> | <span data-ttu-id="7ef17-119">Применяется к `list` действия и может быть `Detailed` (по умолчанию) или `Short`.</span><span class="sxs-lookup"><span data-stu-id="7ef17-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="7ef17-120">Справка</span><span class="sxs-lookup"><span data-stu-id="7ef17-120">Help</span></span> | <span data-ttu-id="7ef17-121">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="7ef17-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="7ef17-122">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="7ef17-122">NonInteractive</span></span> | <span data-ttu-id="7ef17-123">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="7ef17-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7ef17-124">Пароль</span><span class="sxs-lookup"><span data-stu-id="7ef17-124">Password</span></span> | <span data-ttu-id="7ef17-125">Указывает пароль для проверки подлинности с источником.</span><span class="sxs-lookup"><span data-stu-id="7ef17-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="7ef17-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="7ef17-126">StorePasswordInClearText</span></span> | <span data-ttu-id="7ef17-127">Указывает, чтобы сохранить пароль в незашифрованном вместо поведения по умолчанию хранение в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="7ef17-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="7ef17-128">UserName</span><span class="sxs-lookup"><span data-stu-id="7ef17-128">UserName</span></span> | <span data-ttu-id="7ef17-129">Указывает имя пользователя для проверки подлинности с источником.</span><span class="sxs-lookup"><span data-stu-id="7ef17-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="7ef17-130">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="7ef17-130">Verbosity</span></span> | <span data-ttu-id="7ef17-131">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="7ef17-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="7ef17-132">Убедитесь в том, что добавление источников в один и тот же контекст пользователя пароль как nuget.exe впоследствии будет использоваться для доступа к источнику пакета.</span><span class="sxs-lookup"><span data-stu-id="7ef17-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="7ef17-133">Пароль будет сохранен в файле конфигурации зашифрованы и могут быть расшифрованы только в том же контексте пользователя, он был зашифрован.</span><span class="sxs-lookup"><span data-stu-id="7ef17-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="7ef17-134">Так, например при использовании сервера сборки для восстановления пакетов NuGet, который должен быть зашифрован пароль с тем же пользователем Windows, под которой будет выполняться задача построения сервера.</span><span class="sxs-lookup"><span data-stu-id="7ef17-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="7ef17-135">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7ef17-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7ef17-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="7ef17-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
