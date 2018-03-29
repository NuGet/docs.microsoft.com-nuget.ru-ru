---
title: Команда источники NuGet CLI | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Справочник по nuget.exe источники команды
keywords: NuGet источники ссылки, источники команды
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f682a5209556ec6741473ccf2648e8f38bb568b9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="172c4-104">Команда источников (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="172c4-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="172c4-105">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="172c4-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="172c4-106">Управляет списком источников, расположенных в файле конфигурации области пользователя или указанного файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="172c4-106">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="172c4-107">Файл конфигурации области пользователя находится в `%appdata%\NuGet\NuGet.Config` (Windows) и `~/.nuget/NuGet/NuGet.Config` (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="172c4-107">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="172c4-108">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="172c4-108">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="172c4-109">Использование</span><span class="sxs-lookup"><span data-stu-id="172c4-109">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="172c4-110">где `<operation>` является одним из *списка, добавления, удаления, включение, отключение* или *обновление*, `<name>` имя источника, и `<source>` является URL-адрес источника.</span><span class="sxs-lookup"><span data-stu-id="172c4-110">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="172c4-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="172c4-111">Options</span></span>

| <span data-ttu-id="172c4-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="172c4-112">Option</span></span> | <span data-ttu-id="172c4-113">Описание</span><span class="sxs-lookup"><span data-stu-id="172c4-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="172c4-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="172c4-114">ConfigFile</span></span> | <span data-ttu-id="172c4-115">Файл конфигурации NuGet вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="172c4-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="172c4-116">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="172c4-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="172c4-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="172c4-117">ForceEnglishOutput</span></span> | <span data-ttu-id="172c4-118">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="172c4-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="172c4-119">Формат</span><span class="sxs-lookup"><span data-stu-id="172c4-119">Format</span></span> | <span data-ttu-id="172c4-120">Применяется к `list` действия и может быть `Detailed` (по умолчанию) или `Short`.</span><span class="sxs-lookup"><span data-stu-id="172c4-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="172c4-121">Справка</span><span class="sxs-lookup"><span data-stu-id="172c4-121">Help</span></span> | <span data-ttu-id="172c4-122">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="172c4-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="172c4-123">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="172c4-123">NonInteractive</span></span> | <span data-ttu-id="172c4-124">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="172c4-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="172c4-125">Пароль</span><span class="sxs-lookup"><span data-stu-id="172c4-125">Password</span></span> | <span data-ttu-id="172c4-126">Указывает пароль для проверки подлинности с источником.</span><span class="sxs-lookup"><span data-stu-id="172c4-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="172c4-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="172c4-127">StorePasswordInClearText</span></span> | <span data-ttu-id="172c4-128">Указывает, чтобы сохранить пароль в незашифрованном вместо поведения по умолчанию хранение в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="172c4-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="172c4-129">UserName</span><span class="sxs-lookup"><span data-stu-id="172c4-129">UserName</span></span> | <span data-ttu-id="172c4-130">Указывает имя пользователя для проверки подлинности с источником.</span><span class="sxs-lookup"><span data-stu-id="172c4-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="172c4-131">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="172c4-131">Verbosity</span></span> | <span data-ttu-id="172c4-132">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="172c4-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="172c4-133">Убедитесь в том, что добавление источников в один и тот же контекст пользователя пароль как nuget.exe впоследствии будет использоваться для доступа к источнику пакета.</span><span class="sxs-lookup"><span data-stu-id="172c4-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="172c4-134">Пароль будет сохранен в файле конфигурации зашифрованы и могут быть расшифрованы только в том же контексте пользователя, он был зашифрован.</span><span class="sxs-lookup"><span data-stu-id="172c4-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="172c4-135">Так, например при использовании сервера сборки для восстановления пакетов NuGet, который должен быть зашифрован пароль с тем же пользователем Windows, под которой будет выполняться задача построения сервера.</span><span class="sxs-lookup"><span data-stu-id="172c4-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="172c4-136">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="172c4-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="172c4-137">Примеры</span><span class="sxs-lookup"><span data-stu-id="172c4-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
