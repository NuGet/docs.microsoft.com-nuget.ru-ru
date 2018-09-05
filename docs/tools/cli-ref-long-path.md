---
title: Поддержка длинных путей интерфейса командной строки NuGet
description: Справочник по nuget.exe поддержка длинных путей
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547830"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="45c47-103">Поддержка длинных путей (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="45c47-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="45c47-104">**Применяется к:** все &bullet; **поддерживаемые версии:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="45c47-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="45c47-105">NuGet.exe 4.8 и более поздних версий поддержка длинные пути для файлов и каталогов для сценариев, такие как пакет, восстановления, установки и в большинстве других ситуаций, требующих пути к файлам.</span><span class="sxs-lookup"><span data-stu-id="45c47-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="45c47-106">Требуемая операционная система</span><span class="sxs-lookup"><span data-stu-id="45c47-106">Required Operating System</span></span>

-   <span data-ttu-id="45c47-107">Windows 10 (версия 1607 или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="45c47-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="45c47-108">Windows 10 (июль 2015 г. выпуск или версия 1511) при обновлении .NET Framework до версии 4.6.2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="45c47-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="45c47-109">Windows Server 2016 (все версии)</span><span class="sxs-lookup"><span data-stu-id="45c47-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="45c47-110">Включение групповой политики «Длинные пути Win32»</span><span class="sxs-lookup"><span data-stu-id="45c47-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="45c47-111">Необходимо включить поддержку длинных путей в этих системах, задав групповой политики.</span><span class="sxs-lookup"><span data-stu-id="45c47-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="45c47-112">Шаги:</span><span class="sxs-lookup"><span data-stu-id="45c47-112">Steps:</span></span>
1. <span data-ttu-id="45c47-113">Запустите **групповыми политиками** - введите «Изменение групповой политики» в строке поиска начала или выполните команду «gpedit.msc» из команды «выполнить» (Windows-R).</span><span class="sxs-lookup"><span data-stu-id="45c47-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="45c47-114">В **редактор локальных групповых политик**, включите «локального компьютера Policy/Computer Configuration/Administrative шаблоны/длинные пути все параметры и включение Win32».</span><span class="sxs-lookup"><span data-stu-id="45c47-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Политика длинных путей](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="45c47-116">Включение других средств NuGet для поддержки длинных путей</span><span class="sxs-lookup"><span data-stu-id="45c47-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="45c47-117">Интерфейс командной строки DotNet поддерживает длинные пути, независимо от операционной системы и версии.</span><span class="sxs-lookup"><span data-stu-id="45c47-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="45c47-118">Visual Studio или msbuild/t: RESTORE не поддерживает длинные пути.</span><span class="sxs-lookup"><span data-stu-id="45c47-118">Visual Studio or msbuild /t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="45c47-119">Программное обеспечение, которое использует NuGet библиотеки для выполнения восстановления и других команд будет поддерживать длинные пути на тех же системах работает NuGet.exe, если они также задать longPathAware в окнах своих манифеста Настройка UseLegacyPathHandling значение false с помощью файла App.Config [ Дополнительные сведения см. в разделе](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="45c47-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

