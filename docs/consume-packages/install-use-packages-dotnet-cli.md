---
title: Установка пакетов NuGet и управление ими с использованием CLI dotnet
description: Инструкции по использованию CLI dotnet для работы с пакетами NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825156"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="49617-103">Установка пакетов и управление ими с использованием CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="49617-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="49617-104">С помощью средства CLI вы можете легко устанавливаться, удалять и обновлять пакеты NuGet в проектах и решениях.</span><span class="sxs-lookup"><span data-stu-id="49617-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="49617-105">Оно работает в Windows, Mac OS X и Linux.</span><span class="sxs-lookup"><span data-stu-id="49617-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="49617-106">Средство CLI dotnet предназначено для использования в проектах .NET Core и .NET Standard (проекты в стиле пакета SDK), а также в любых других проектах в стиле пакета SDK (например, в тех, которые нацелены на платформу .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="49617-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="49617-107">Дополнительные сведения см. в статье [Атрибут SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="49617-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="49617-108">В этой статье описываются общие принципы использования некоторых распространенных команд CLI dotnet.</span><span class="sxs-lookup"><span data-stu-id="49617-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="49617-109">Для большинства из этих команд средство CLI ищет файл проекта в текущем каталоге, кроме случаев, когда файл проекта задан в самой команде (с помощью необязательного параметра).</span><span class="sxs-lookup"><span data-stu-id="49617-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="49617-110">Полный список доступных команд и аргументов см. в статье [Средства интерфейса командной строки (CLI) .NET Core](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="49617-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49617-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="49617-111">Prerequisites</span></span>

- <span data-ttu-id="49617-112">[Пакет SDK для .NET Core](https://www.microsoft.com/net/download/), который предоставляет программу командной строки `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="49617-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="49617-113">Начиная с версии Visual Studio 2017, средство CLI dotnet автоматически устанавливается вместе с любыми рабочими нагрузками, связанными с .NET Core.</span><span class="sxs-lookup"><span data-stu-id="49617-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="49617-114">Установка пакета</span><span class="sxs-lookup"><span data-stu-id="49617-114">Install a package</span></span>

<span data-ttu-id="49617-115">Команда [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) добавляет в файл проекта ссылку на пакет, после чего выполняет команду `dotnet restore` для установки пакета.</span><span class="sxs-lookup"><span data-stu-id="49617-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="49617-116">Откройте командную строку и перейдите в каталог, в котором находится файл проекта.</span><span class="sxs-lookup"><span data-stu-id="49617-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="49617-117">Выполните следующую команду для установки пакета Nuget:</span><span class="sxs-lookup"><span data-stu-id="49617-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="49617-118">Например, чтобы установить пакет `Newtonsoft.Json`, выполните следующую команду</span><span class="sxs-lookup"><span data-stu-id="49617-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="49617-119">После выполнения команды проверьте файл проекта и убедитесь, что пакет был установлен.</span><span class="sxs-lookup"><span data-stu-id="49617-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="49617-120">Для этого можно открыть файл `.csproj` и проверить добавленную в него ссылку:</span><span class="sxs-lookup"><span data-stu-id="49617-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="49617-121">Установка определенной версии пакета</span><span class="sxs-lookup"><span data-stu-id="49617-121">Install a specific version of a package</span></span>

<span data-ttu-id="49617-122">Если версия пакета не указана, NuGet установит его последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="49617-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="49617-123">Также вы можете выполнить команду [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), чтобы установить определенную версию пакета Nuget:</span><span class="sxs-lookup"><span data-stu-id="49617-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="49617-124">Например, чтобы добавить версию 12.0.1 пакета `Newtonsoft.Json`, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="49617-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="49617-125">Вывод списка ссылок на пакеты</span><span class="sxs-lookup"><span data-stu-id="49617-125">List package references</span></span>

<span data-ttu-id="49617-126">Чтобы просмотреть список ссылок на пакеты для проекта, воспользуйтесь командой [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="49617-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="49617-127">Удаление пакета</span><span class="sxs-lookup"><span data-stu-id="49617-127">Remove a package</span></span>

<span data-ttu-id="49617-128">Чтобы удалить ссылку на пакет из файла проекта, воспользуйтесь командой [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="49617-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="49617-129">Например, чтобы удалить пакет `Newtonsoft.Json`, выполните следующую команду</span><span class="sxs-lookup"><span data-stu-id="49617-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="49617-130">Обновление пакета</span><span class="sxs-lookup"><span data-stu-id="49617-130">Update a package</span></span>

<span data-ttu-id="49617-131">При выполнении команды `dotnet add package` NuGet устанавливает последнюю версию пакета, кроме случаев, когда версия задается с помощью параметра `-v`.</span><span class="sxs-lookup"><span data-stu-id="49617-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="49617-132">Восстановление пакетов</span><span class="sxs-lookup"><span data-stu-id="49617-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
