---
title: "Заметки о выпуске NuGet 2.8.2 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "Заметки о выпуске для NuGet 2.8.2, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.8.2 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="87859-104">Заметки о выпуске NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="87859-104">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="87859-105">[Заметки о выпуске NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 заметки о выпуске](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="87859-105">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="87859-106">NuGet 2.8.2 был выпущен 22 мая 2014 г.</span><span class="sxs-lookup"><span data-stu-id="87859-106">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="87859-107">Этот выпуск включены только изменения командной строки nuget.exe, NuGet.Server пакета и других пакетах NuGet.</span><span class="sxs-lookup"><span data-stu-id="87859-107">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="87859-108">Выпуск не содержит обновленные расширение Visual Studio или расширения WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="87859-108">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="87859-109">Важные обновления</span><span class="sxs-lookup"><span data-stu-id="87859-109">Notable Updates</span></span>

<span data-ttu-id="87859-110">В окне командной строки nuget.exe и NuGet.Server пакета (для резидентных каналы NuGet) были наиболее важные обновления.</span><span class="sxs-lookup"><span data-stu-id="87859-110">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="87859-111">Исправления важных nuget.exe</span><span class="sxs-lookup"><span data-stu-id="87859-111">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="87859-112">NuGet.exe принудительной отправки завершается сбоем и отслеживает повторение попытки</span><span class="sxs-lookup"><span data-stu-id="87859-112">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="87859-113">NuGet.exe принудительной правильно не отправлять Обычная проверка подлинности учетных данных</span><span class="sxs-lookup"><span data-stu-id="87859-113">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="87859-114">NuGet.exe Push не выполните Временное перенаправление</span><span class="sxs-lookup"><span data-stu-id="87859-114">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="87859-115">Исправление ошибки важные NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="87859-115">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="87859-116">Неверное значение IsAbsoluteLatestVersion возвращенных NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="87859-116">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="87859-117">Пакеты обновления</span><span class="sxs-lookup"><span data-stu-id="87859-117">Packages Updated</span></span>

<span data-ttu-id="87859-118">Nuget.exe командной строки и NuGet.Server исправления поставляются как обновления пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="87859-118">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="87859-119">Нет других пакетов с 2.8.2 также.</span><span class="sxs-lookup"><span data-stu-id="87859-119">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="87859-120">Ниже приведен перечень обновленные пакеты.</span><span class="sxs-lookup"><span data-stu-id="87859-120">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="87859-121">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="87859-121">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="87859-122">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="87859-122">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="87859-123">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="87859-123">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="87859-124">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="87859-124">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="87859-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (пакета, не расширения)</span><span class="sxs-lookup"><span data-stu-id="87859-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="87859-126">Все изменения</span><span class="sxs-lookup"><span data-stu-id="87859-126">All Changes</span></span>
<span data-ttu-id="87859-127">Возникли проблемы 10, в выпуске.</span><span class="sxs-lookup"><span data-stu-id="87859-127">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="87859-128">Полный список рабочих элементов исправления в NuGet 2.8.2, представление [NuGet отслеживания проблем в этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="87859-128">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
