---
title: Заметки о выпуске NuGet 2.8.2
description: Заметки о выпуске для NuGet 2.8.2, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821334"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="e8574-103">Заметки о выпуске NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="e8574-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="e8574-104">[Заметки о выпуске NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 заметки о выпуске](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="e8574-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="e8574-105">NuGet 2.8.2 был выпущен 22 мая 2014 г.</span><span class="sxs-lookup"><span data-stu-id="e8574-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="e8574-106">Этот выпуск включены только изменения командной строки nuget.exe, NuGet.Server пакета и других пакетах NuGet.</span><span class="sxs-lookup"><span data-stu-id="e8574-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="e8574-107">Выпуск не содержит обновленные расширение Visual Studio или расширения WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="e8574-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="e8574-108">Важные обновления</span><span class="sxs-lookup"><span data-stu-id="e8574-108">Notable Updates</span></span>

<span data-ttu-id="e8574-109">В окне командной строки nuget.exe и NuGet.Server пакета (для резидентных каналы NuGet) были наиболее важные обновления.</span><span class="sxs-lookup"><span data-stu-id="e8574-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="e8574-110">Исправления важных nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e8574-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="e8574-111">NuGet.exe принудительной отправки завершается сбоем и отслеживает повторение попытки</span><span class="sxs-lookup"><span data-stu-id="e8574-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="e8574-112">NuGet.exe принудительной правильно не отправлять Обычная проверка подлинности учетных данных</span><span class="sxs-lookup"><span data-stu-id="e8574-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="e8574-113">NuGet.exe Push не выполните Временное перенаправление</span><span class="sxs-lookup"><span data-stu-id="e8574-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="e8574-114">Исправление ошибки важные NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="e8574-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="e8574-115">Неверное значение IsAbsoluteLatestVersion возвращенных NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="e8574-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="e8574-116">Пакеты обновления</span><span class="sxs-lookup"><span data-stu-id="e8574-116">Packages Updated</span></span>

<span data-ttu-id="e8574-117">Nuget.exe командной строки и NuGet.Server исправления поставляются как обновления пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="e8574-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="e8574-118">Нет других пакетов с 2.8.2 также.</span><span class="sxs-lookup"><span data-stu-id="e8574-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="e8574-119">Ниже приведен перечень обновленные пакеты.</span><span class="sxs-lookup"><span data-stu-id="e8574-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="e8574-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="e8574-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="e8574-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="e8574-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="e8574-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="e8574-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="e8574-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="e8574-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="e8574-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (пакета, не расширения)</span><span class="sxs-lookup"><span data-stu-id="e8574-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="e8574-125">Все изменения</span><span class="sxs-lookup"><span data-stu-id="e8574-125">All Changes</span></span>
<span data-ttu-id="e8574-126">Возникли проблемы 10, в выпуске.</span><span class="sxs-lookup"><span data-stu-id="e8574-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="e8574-127">Полный список рабочих элементов исправления в NuGet 2.8.2, представление [NuGet отслеживания проблем в этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="e8574-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
