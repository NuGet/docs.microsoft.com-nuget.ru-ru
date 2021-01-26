---
title: Заметки о выпуске 2.8.2 NuGet
description: Заметки о выпуске NuGet 2.8.2, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780367"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="1b84e-103">Заметки о выпуске 2.8.2 NuGet</span><span class="sxs-lookup"><span data-stu-id="1b84e-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="1b84e-104">[Заметки о](../release-notes/nuget-2.8.1.md)  |  выпуске 2.8.1 NuGet [Заметки о выпуске 2.8.3 NuGet](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="1b84e-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="1b84e-105">2.8.2 NuGet выпущен 22 мая, 2014.</span><span class="sxs-lookup"><span data-stu-id="1b84e-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="1b84e-106">Этот выпуск включал только изменения в командной строке nuget.exe, пакете NuGet. Server и других пакетах NuGet.</span><span class="sxs-lookup"><span data-stu-id="1b84e-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="1b84e-107">Выпуск не включал в себя обновленное расширение Visual Studio или расширение WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="1b84e-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="1b84e-108">Важные обновления</span><span class="sxs-lookup"><span data-stu-id="1b84e-108">Notable Updates</span></span>

<span data-ttu-id="1b84e-109">Наиболее важные обновления находились в командной строке nuget.exe и пакете NuGet. Server (для самостоятельно размещенных веб-каналов NuGet).</span><span class="sxs-lookup"><span data-stu-id="1b84e-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="1b84e-110">Важные исправления ошибок nuget.exe</span><span class="sxs-lookup"><span data-stu-id="1b84e-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="1b84e-111"> Сбой принудительной отправкиnuget.exe и повторная попытка</span><span class="sxs-lookup"><span data-stu-id="1b84e-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="1b84e-112">nuget.exe принудительная отправка неправильно отправляет учетные данные обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="1b84e-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="1b84e-113">nuget.exe push-уведомления не подчиняются временному перенаправлению</span><span class="sxs-lookup"><span data-stu-id="1b84e-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="1b84e-114">Важное исправление ошибки NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="1b84e-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="1b84e-115">Неверное значение Исабсолутелатестверсион, возвращенное NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="1b84e-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="1b84e-116">Пакеты обновлены</span><span class="sxs-lookup"><span data-stu-id="1b84e-116">Packages Updated</span></span>

<span data-ttu-id="1b84e-117">Исправления командной строки nuget.exe и NuGet. Server поставляются как обновления пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="1b84e-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="1b84e-118">Существуют и другие пакеты, обновленные с помощью 2.8.2.</span><span class="sxs-lookup"><span data-stu-id="1b84e-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="1b84e-119">Ниже приведен список обновленных пакетов.</span><span class="sxs-lookup"><span data-stu-id="1b84e-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="1b84e-120">NuGet. Core</span><span class="sxs-lookup"><span data-stu-id="1b84e-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="1b84e-121">NuGet. CommandLine</span><span class="sxs-lookup"><span data-stu-id="1b84e-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="1b84e-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="1b84e-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="1b84e-123">NuGet. Build</span><span class="sxs-lookup"><span data-stu-id="1b84e-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="1b84e-124">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (пакет, а не расширение)</span><span class="sxs-lookup"><span data-stu-id="1b84e-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="1b84e-125">Все изменения</span><span class="sxs-lookup"><span data-stu-id="1b84e-125">All Changes</span></span>
<span data-ttu-id="1b84e-126">В выпуске было решено 10 проблем.</span><span class="sxs-lookup"><span data-stu-id="1b84e-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="1b84e-127">Полный список рабочих элементов, исправленных в NuGet 2.8.2, см. в [этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="1b84e-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
