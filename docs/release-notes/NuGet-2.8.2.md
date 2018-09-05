---
title: Заметки о выпуске NuGet 2.8.2
description: Заметки о выпуске для NuGet 2.8.2, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551152"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="314a0-103">Заметки о выпуске NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="314a0-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="314a0-104">[Заметки о выпуске NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [заметки о выпуске NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="314a0-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="314a0-105">NuGet 2.8.2 было выпущено 22 мая 2014 г.</span><span class="sxs-lookup"><span data-stu-id="314a0-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="314a0-106">Этот выпуск включены только изменения командной строки nuget.exe, пакета NuGet.Server и других пакетах NuGet.</span><span class="sxs-lookup"><span data-stu-id="314a0-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="314a0-107">Выпуск не включала обновленные расширение Visual Studio или WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="314a0-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="314a0-108">Важные обновления</span><span class="sxs-lookup"><span data-stu-id="314a0-108">Notable Updates</span></span>

<span data-ttu-id="314a0-109">Наиболее важные обновления были в командной строки nuget.exe и пакета NuGet.Server (для резидентных веб-каналов NuGet).</span><span class="sxs-lookup"><span data-stu-id="314a0-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="314a0-110">Nuget.exe важные исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="314a0-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="314a0-111">NuGet.exe Push-уведомлений, завершается ошибкой и отслеживает повторная попытка</span><span class="sxs-lookup"><span data-stu-id="314a0-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="314a0-112">NuGet.exe Push-уведомлений не отправляет учетные данные обычной проверки подлинности правильно</span><span class="sxs-lookup"><span data-stu-id="314a0-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="314a0-113">NuGet.exe Push-уведомлений не следуйте Временное перенаправление</span><span class="sxs-lookup"><span data-stu-id="314a0-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="314a0-114">Исправление ошибки важные NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="314a0-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="314a0-115">Неверное значение IsAbsoluteLatestVersion, возвращенный NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="314a0-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="314a0-116">Пакеты обновлены</span><span class="sxs-lookup"><span data-stu-id="314a0-116">Packages Updated</span></span>

<span data-ttu-id="314a0-117">Командной строки nuget.exe и NuGet.Server исправления поставляются как обновлений пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="314a0-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="314a0-118">Произошли другие пакеты, обновляется также 2.8.2.</span><span class="sxs-lookup"><span data-stu-id="314a0-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="314a0-119">Ниже приведен список обновленных пакетов:</span><span class="sxs-lookup"><span data-stu-id="314a0-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="314a0-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="314a0-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="314a0-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="314a0-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="314a0-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="314a0-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="314a0-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="314a0-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="314a0-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (пакета, не расширения)</span><span class="sxs-lookup"><span data-stu-id="314a0-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="314a0-125">Все изменения</span><span class="sxs-lookup"><span data-stu-id="314a0-125">All Changes</span></span>
<span data-ttu-id="314a0-126">Возникли 10 ошибок, устраненных в выпуске.</span><span class="sxs-lookup"><span data-stu-id="314a0-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="314a0-127">Полный список рабочих элементов исправленные в NuGet 2.8.2, пожалуйста представление [Issue Tracker NuGet для этого выпуска](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="314a0-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
