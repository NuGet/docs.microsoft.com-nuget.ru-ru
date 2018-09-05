---
title: Интерфейс командной строки NuGet источники команд
description: Справочник по nuget.exe источники команд
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7ef856f783c8e11cdb40edb0d1c1458730d87262
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548112"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="bf7f3-103">Команда sources (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="bf7f3-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="bf7f3-104">**Применяется к:** использование пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="bf7f3-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="bf7f3-105">Управляет списком источников, расположенных в файле конфигурации области пользователя или указанного файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="bf7f3-106">Файл конфигурации пользователя область находится в `%appdata%\NuGet\NuGet.Config` (Windows) и `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="bf7f3-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="bf7f3-107">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="bf7f3-108">Использование</span><span class="sxs-lookup"><span data-stu-id="bf7f3-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="bf7f3-109">где `<operation>` является одним из *списка, добавления, удаления, включение, отключение* или *обновление*, `<name>` имя источника, и `<source>` является URL-адрес источника.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="bf7f3-110">Параметры</span><span class="sxs-lookup"><span data-stu-id="bf7f3-110">Options</span></span>

| <span data-ttu-id="bf7f3-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="bf7f3-111">Option</span></span> | <span data-ttu-id="bf7f3-112">Описание</span><span class="sxs-lookup"><span data-stu-id="bf7f3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bf7f3-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="bf7f3-113">ConfigFile</span></span> | <span data-ttu-id="bf7f3-114">Чтобы применить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bf7f3-115">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="bf7f3-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="bf7f3-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="bf7f3-116">ForceEnglishOutput</span></span> | <span data-ttu-id="bf7f3-117">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="bf7f3-118">Формат</span><span class="sxs-lookup"><span data-stu-id="bf7f3-118">Format</span></span> | <span data-ttu-id="bf7f3-119">Применяется к `list` действия и может быть `Detailed` (по умолчанию) или `Short`.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="bf7f3-120">Справка</span><span class="sxs-lookup"><span data-stu-id="bf7f3-120">Help</span></span> | <span data-ttu-id="bf7f3-121">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="bf7f3-122">Неинтерактивная</span><span class="sxs-lookup"><span data-stu-id="bf7f3-122">NonInteractive</span></span> | <span data-ttu-id="bf7f3-123">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="bf7f3-124">Пароль</span><span class="sxs-lookup"><span data-stu-id="bf7f3-124">Password</span></span> | <span data-ttu-id="bf7f3-125">Указывает пароль для проверки подлинности с источником.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="bf7f3-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="bf7f3-126">StorePasswordInClearText</span></span> | <span data-ttu-id="bf7f3-127">Указывает, чтобы сохранить пароль в незашифрованном вместо хранения в зашифрованной форме по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="bf7f3-128">UserName</span><span class="sxs-lookup"><span data-stu-id="bf7f3-128">UserName</span></span> | <span data-ttu-id="bf7f3-129">Указывает имя пользователя для проверки подлинности с источником.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="bf7f3-130">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="bf7f3-130">Verbosity</span></span> | <span data-ttu-id="bf7f3-131">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="bf7f3-132">Не забудьте добавить пароль источников, в том же контексте пользователя, как nuget.exe впоследствии будет использоваться для доступа к источнику пакета.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="bf7f3-133">Пароль будет храниться в зашифрованном виде в файле конфигурации и могут быть расшифрованы только в том же контексте пользователя, так как он был зашифрован.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="bf7f3-134">Так что, например при использовании сервера сборки для восстановления пакетов NuGet, который должен быть зашифрован пароль с тем же пользователем Windows, с которой будет выполняться задача сервера сборки.</span><span class="sxs-lookup"><span data-stu-id="bf7f3-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="bf7f3-135">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bf7f3-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="bf7f3-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="bf7f3-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
