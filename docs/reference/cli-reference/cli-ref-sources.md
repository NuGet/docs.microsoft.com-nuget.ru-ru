---
title: Команда NuGet CLI Sources Command
description: Справочник по команде NuGet. exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327601"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="1a32f-103">Команда sources (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1a32f-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="1a32f-104">Область **применения:** использование пакетов, публикация &bullet; **поддерживаемых версий:** все</span><span class="sxs-lookup"><span data-stu-id="1a32f-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1a32f-105">Управляет списком источников, расположенных в файле конфигурации пользовательской области или в указанном файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1a32f-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="1a32f-106">Файл конфигурации пользовательской области находится в папке `%appdata%\NuGet\NuGet.Config` (Windows) и `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1a32f-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="1a32f-107">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="1a32f-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="1a32f-108">Использование</span><span class="sxs-lookup"><span data-stu-id="1a32f-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="1a32f-109">Если `<operation>` один из *списков, добавить, удалить, включить, отключить* или *Обновить*, `<name>` — это имя источника, а `<source>` — URL-адрес источника.</span><span class="sxs-lookup"><span data-stu-id="1a32f-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="1a32f-110">В каждый момент времени можно обрабатывать только один источник.</span><span class="sxs-lookup"><span data-stu-id="1a32f-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="1a32f-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="1a32f-111">Options</span></span>

| <span data-ttu-id="1a32f-112">Параметр</span><span class="sxs-lookup"><span data-stu-id="1a32f-112">Option</span></span> | <span data-ttu-id="1a32f-113">Описание</span><span class="sxs-lookup"><span data-stu-id="1a32f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a32f-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1a32f-114">ConfigFile</span></span> | <span data-ttu-id="1a32f-115">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="1a32f-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1a32f-116">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1a32f-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1a32f-117">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="1a32f-117">ForceEnglishOutput</span></span> | <span data-ttu-id="1a32f-118">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="1a32f-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1a32f-119">Формат</span><span class="sxs-lookup"><span data-stu-id="1a32f-119">Format</span></span> | <span data-ttu-id="1a32f-120">Применяется к `list` действию и может быть `Detailed` (по умолчанию) или `Short`.</span><span class="sxs-lookup"><span data-stu-id="1a32f-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="1a32f-121">Help</span><span class="sxs-lookup"><span data-stu-id="1a32f-121">Help</span></span> | <span data-ttu-id="1a32f-122">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="1a32f-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="1a32f-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1a32f-123">NonInteractive</span></span> | <span data-ttu-id="1a32f-124">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="1a32f-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1a32f-125">Пароль</span><span class="sxs-lookup"><span data-stu-id="1a32f-125">Password</span></span> | <span data-ttu-id="1a32f-126">Указывает пароль для проверки подлинности в источнике.</span><span class="sxs-lookup"><span data-stu-id="1a32f-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="1a32f-127">сторепассвординклеартекст</span><span class="sxs-lookup"><span data-stu-id="1a32f-127">StorePasswordInClearText</span></span> | <span data-ttu-id="1a32f-128">Указывает, что пароль следует хранить в незашифрованном тексте, а не в стандартном способе хранения зашифрованной формы.</span><span class="sxs-lookup"><span data-stu-id="1a32f-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="1a32f-129">UserName</span><span class="sxs-lookup"><span data-stu-id="1a32f-129">UserName</span></span> | <span data-ttu-id="1a32f-130">Указывает имя пользователя для проверки подлинности в источнике.</span><span class="sxs-lookup"><span data-stu-id="1a32f-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="1a32f-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="1a32f-131">Verbosity</span></span> | <span data-ttu-id="1a32f-132">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="1a32f-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="1a32f-133">Не забудьте добавить пароль источников в том же контексте пользователя, что и NuGet. exe позднее используется для доступа к источнику пакета.</span><span class="sxs-lookup"><span data-stu-id="1a32f-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="1a32f-134">Пароль будет сохранен в зашифрованном виде в файле конфигурации и может быть расшифрован только в том же контексте пользователя, в котором он был зашифрован.</span><span class="sxs-lookup"><span data-stu-id="1a32f-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="1a32f-135">Например, при использовании сервера сборки для восстановления пакетов NuGet пароль должен быть зашифрован с помощью того же пользователя Windows, под которым будет выполняться задача сервера сборки.</span><span class="sxs-lookup"><span data-stu-id="1a32f-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="1a32f-136">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1a32f-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1a32f-137">Примеры</span><span class="sxs-lookup"><span data-stu-id="1a32f-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
