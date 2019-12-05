---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825165"
---
<span data-ttu-id="77c34-101">С помощью команды [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) вы можете восстановить пакеты, включенные в файл проекта (см. [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="77c34-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="77c34-102">При использовании .NET Core версии 2.0 и более поздней автоматическое восстановление доступно с помощью команд `dotnet build` и `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="77c34-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="77c34-103">В версии NuGet 4.0 при этом выполняется тот же код, что и для команды `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="77c34-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="77c34-104">Как и с другими командами CLI `dotnet`, откройте командную строку и перейдите к каталогу, в котором находится файл проекта.</span><span class="sxs-lookup"><span data-stu-id="77c34-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="77c34-105">Восстановление пакета с помощью `dotnet restore`.</span><span class="sxs-lookup"><span data-stu-id="77c34-105">To restore a package using `dotnet restore`:</span></span>

```dotnetcli
dotnet restore 
```