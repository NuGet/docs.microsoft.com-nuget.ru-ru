---
title: Команда NuGet CLI Sources Command
description: Справочник по команде nuget.exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622594"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="5257b-103">Команда "источники" (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="5257b-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="5257b-104">Область **применения:** использование пакетов, публикация &bullet; **поддерживаемых версий:** все</span><span class="sxs-lookup"><span data-stu-id="5257b-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5257b-105">Управляет списком источников, расположенных в файле конфигурации пользовательской области или в указанном файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5257b-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="5257b-106">Файл конфигурации пользовательской области находится в папке `%appdata%\NuGet\NuGet.Config` (Windows) и `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5257b-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="5257b-107">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="5257b-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="5257b-108">Использование</span><span class="sxs-lookup"><span data-stu-id="5257b-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="5257b-109">Если `<operation>` один из *списков, добавить, удалить, включить, отключить* или *Обновить*, `<name>` — это имя источника, а `<source>` — URL-адрес источника.</span><span class="sxs-lookup"><span data-stu-id="5257b-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="5257b-110">В каждый момент времени можно обрабатывать только один источник.</span><span class="sxs-lookup"><span data-stu-id="5257b-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="5257b-111">Параметры</span><span class="sxs-lookup"><span data-stu-id="5257b-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="5257b-112">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="5257b-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5257b-113">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5257b-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="5257b-114">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="5257b-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="5257b-115">Применяется к `list` действию и может быть `Detailed` (по умолчанию) или `Short` .</span><span class="sxs-lookup"><span data-stu-id="5257b-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="5257b-116">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="5257b-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="5257b-117">Имя источника.</span><span class="sxs-lookup"><span data-stu-id="5257b-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="5257b-118">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="5257b-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="5257b-119">Указывает пароль для проверки подлинности в источнике.</span><span class="sxs-lookup"><span data-stu-id="5257b-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="5257b-120">Путь к источнику пакетов.</span><span class="sxs-lookup"><span data-stu-id="5257b-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="5257b-121">Указывает, что пароль следует хранить в незашифрованном тексте, а не в стандартном способе хранения зашифрованной формы.</span><span class="sxs-lookup"><span data-stu-id="5257b-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="5257b-122">Указывает имя пользователя для проверки подлинности в источнике.</span><span class="sxs-lookup"><span data-stu-id="5257b-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="5257b-123">Разделенный запятыми список допустимых типов проверки подлинности для этого источника.</span><span class="sxs-lookup"><span data-stu-id="5257b-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="5257b-124">По умолчанию все типы проверки подлинности являются допустимыми.</span><span class="sxs-lookup"><span data-stu-id="5257b-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="5257b-125">Например, `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="5257b-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="5257b-126">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="5257b-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="5257b-127">Не забудьте добавить пароль исходного кода в том же контексте пользователя, что и nuget.exe позже используется для доступа к источнику пакета.</span><span class="sxs-lookup"><span data-stu-id="5257b-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="5257b-128">Пароль будет сохранен в зашифрованном виде в файле конфигурации и может быть расшифрован только в том же контексте пользователя, в котором он был зашифрован.</span><span class="sxs-lookup"><span data-stu-id="5257b-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="5257b-129">Например, при использовании сервера сборки для восстановления пакетов NuGet пароль должен быть зашифрован с помощью того же пользователя Windows, под которым будет выполняться задача сервера сборки.</span><span class="sxs-lookup"><span data-stu-id="5257b-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="5257b-130">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5257b-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5257b-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="5257b-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
