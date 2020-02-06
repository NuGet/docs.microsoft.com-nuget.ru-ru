---
title: Поддержка длинного пути CLI NuGet
description: Справочник по поддержке длинных путей в NuGet. exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 9b5a97d963eab7fbbde4aefae1c9b1a8bfcdeb11
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036959"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="08f53-103">Поддержка длинных путей (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="08f53-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="08f53-104">Область **применения:** все &bullet; **Поддерживаемые версии:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="08f53-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="08f53-105">NuGet. exe 4,8 и более поздних версий поддерживают длинные пути для файлов и каталогов в таких сценариях, как Pack, Restore, install и большинство других сценариев, которым требуются пути к файлам.</span><span class="sxs-lookup"><span data-stu-id="08f53-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="08f53-106">Требуемая операционная система</span><span class="sxs-lookup"><span data-stu-id="08f53-106">Required Operating System</span></span>

-   <span data-ttu-id="08f53-107">Windows 10 (версия 1607 или более поздняя)</span><span class="sxs-lookup"><span data-stu-id="08f53-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="08f53-108">Windows 10 (июль 2015 выпуск или 1511) при обновлении .NET Framework до версии 4.6.2 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="08f53-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="08f53-109">Windows Server 2016 (все версии)</span><span class="sxs-lookup"><span data-stu-id="08f53-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="08f53-110">Включить "длинные пути Win32" групповая политика</span><span class="sxs-lookup"><span data-stu-id="08f53-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="08f53-111">Необходимо включить поддержку длинных путей в этих системах, задав групповую политику.</span><span class="sxs-lookup"><span data-stu-id="08f53-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="08f53-112">Шаги:</span><span class="sxs-lookup"><span data-stu-id="08f53-112">Steps:</span></span>
1. <span data-ttu-id="08f53-113">Запустите **Групповая политика редактор** , введите "изменить групповую политику" на панели поиска для запуска или выполните команду gpedit. msc в команде Run (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="08f53-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="08f53-114">В **редактор локальных групповых политик**установите флажок "Политика локального компьютера/Конфигурация компьютера/Административные шаблоны/все параметры/включить длинные пути Win32".</span><span class="sxs-lookup"><span data-stu-id="08f53-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Политика длинных путей](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="08f53-116">Включение поддержки длинных путей другими средствами NuGet</span><span class="sxs-lookup"><span data-stu-id="08f53-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="08f53-117">DotNet CLI поддерживает длинные пути независимо от операционной системы или версии.</span><span class="sxs-lookup"><span data-stu-id="08f53-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="08f53-118">Visual Studio или `msbuild -t:restore` пока не поддерживает длинные пути.</span><span class="sxs-lookup"><span data-stu-id="08f53-118">Visual Studio or `msbuild -t:restore` does not yet support long paths.</span></span>
> -   <span data-ttu-id="08f53-119">Программное обеспечение, использующее библиотеки NuGet для выполнения восстановления и других команд, будет поддерживать длинные пути в тех же системах, где работает NuGet. exe, если они также устанавливают `longPathAware` в манифесте Windows и настраивают `UseLegacyPathHandling` для `false` с помощью App. config. [Дополнительные сведения](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="08f53-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set `longPathAware` in their windows manifest and configure `UseLegacyPathHandling` to `false` via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

