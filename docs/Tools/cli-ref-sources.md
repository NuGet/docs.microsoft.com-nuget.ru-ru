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
ms.openlocfilehash: 52c46dba168e7395d50cb8d8f9775839389e614c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="56818-104">Команда источников (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="56818-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="56818-105">**Применяется к:** потребления пакета, публикация &bullet; **поддерживаемые версии:** все</span><span class="sxs-lookup"><span data-stu-id="56818-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="56818-106">Управляет списком источников, расположенных в `%AppData%\NuGet\NuGet.Config` или указанного файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="56818-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

## <a name="usage"></a><span data-ttu-id="56818-107">Использование</span><span class="sxs-lookup"><span data-stu-id="56818-107">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="56818-108">где `<operation>` является одним из *списка, добавления, удаления, включение, отключение* или *обновление*, `<name>` имя источника, и `<source>` является URL-адрес источника.</span><span class="sxs-lookup"><span data-stu-id="56818-108">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>


## <a name="options"></a><span data-ttu-id="56818-109">Параметры</span><span class="sxs-lookup"><span data-stu-id="56818-109">Options</span></span>

| <span data-ttu-id="56818-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="56818-110">Option</span></span> | <span data-ttu-id="56818-111">Описание</span><span class="sxs-lookup"><span data-stu-id="56818-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="56818-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="56818-112">ConfigFile</span></span> | <span data-ttu-id="56818-113">*(2.5 +)*  NuGet файла конфигурации для применения.</span><span class="sxs-lookup"><span data-stu-id="56818-113">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="56818-114">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="56818-114">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="56818-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="56818-115">ForceEnglishOutput</span></span> | <span data-ttu-id="56818-116">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="56818-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="56818-117">Формат</span><span class="sxs-lookup"><span data-stu-id="56818-117">Format</span></span> | <span data-ttu-id="56818-118">Применяется к `list` действия и может быть `Detailed` (по умолчанию) или `Short`.</span><span class="sxs-lookup"><span data-stu-id="56818-118">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="56818-119">Справка</span><span class="sxs-lookup"><span data-stu-id="56818-119">Help</span></span> | <span data-ttu-id="56818-120">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="56818-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="56818-121">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="56818-121">NonInteractive</span></span> | <span data-ttu-id="56818-122">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="56818-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="56818-123">Пароль</span><span class="sxs-lookup"><span data-stu-id="56818-123">Password</span></span> | <span data-ttu-id="56818-124">Указывает пароль для проверки подлинности с источником.</span><span class="sxs-lookup"><span data-stu-id="56818-124">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="56818-125">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="56818-125">StorePasswordInClearText</span></span> | <span data-ttu-id="56818-126">Указывает, чтобы сохранить пароль в незашифрованном вместо поведения по умолчанию хранение в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="56818-126">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="56818-127">UserName</span><span class="sxs-lookup"><span data-stu-id="56818-127">UserName</span></span> | <span data-ttu-id="56818-128">Указывает имя пользователя для проверки подлинности с источником.</span><span class="sxs-lookup"><span data-stu-id="56818-128">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="56818-129">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="56818-129">Verbosity</span></span> | <span data-ttu-id="56818-130">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="56818-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="56818-131">Убедитесь в том, что добавление источников в один и тот же контекст пользователя пароль как nuget.exe впоследствии будет использоваться для доступа к источнику пакета.</span><span class="sxs-lookup"><span data-stu-id="56818-131">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="56818-132">Пароль будет сохранен в файле конфигурации зашифрованы и могут быть расшифрованы только в том же контексте пользователя, он был зашифрован.</span><span class="sxs-lookup"><span data-stu-id="56818-132">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="56818-133">Так, например при использовании сервера сборки для восстановления пакетов NuGet, который должен быть зашифрован пароль с тем же пользователем Windows, под которой будет выполняться задача построения сервера.</span><span class="sxs-lookup"><span data-stu-id="56818-133">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="56818-134">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="56818-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="56818-135">Примеры</span><span class="sxs-lookup"><span data-stu-id="56818-135">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
