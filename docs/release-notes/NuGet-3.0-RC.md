---
title: Заметки о выпуске для версии-КАНДИДАТа NuGet 3,0
description: Заметки о выпуске для версии-КАНДИДАТа NuGet 3,0, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776568"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="4e0cd-103">Заметки о выпуске для версии-КАНДИДАТа NuGet 3,0</span><span class="sxs-lookup"><span data-stu-id="4e0cd-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="4e0cd-104">[Заметки о](../release-notes/nuget-3.0-beta.md)  |  бета-версии NuGet 3,0 [Заметки о выпуске NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="4e0cd-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="4e0cd-105">Версия-кандидат NuGet 3,0 была выпущена 29 апреля 2015 с версией-КАНДИДАТом Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="4e0cd-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="4e0cd-106">В этом выпуске имеется ряд важных исправлений ошибок, улучшений производительности и обновлений для поддержки новых платформ.</span><span class="sxs-lookup"><span data-stu-id="4e0cd-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="4e0cd-107">Он доступен только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="4e0cd-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="4e0cd-108">Постоянное внимание на производительности</span><span class="sxs-lookup"><span data-stu-id="4e0cd-108">Continued Focus on Performance</span></span>

<span data-ttu-id="4e0cd-109">Стабильность и производительность запросов NuGet по-прежнему представляют собой горячую тему, на которую мы уделимся.</span><span class="sxs-lookup"><span data-stu-id="4e0cd-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="4e0cd-110">В этом выпуске вы должны начать видеть очень быстрые операции поиска в пользовательском интерфейсе NuGet и на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="4e0cd-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="4e0cd-111">Мы отслеживаем службу и используем службу, чтобы мы могли продолжить настройку этих операций.</span><span class="sxs-lookup"><span data-stu-id="4e0cd-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="4e0cd-112">Существенные проблемы устранены</span><span class="sxs-lookup"><span data-stu-id="4e0cd-112">Significant Issues Resolved</span></span>

<span data-ttu-id="4e0cd-113">Чтобы стабилизировать клиенты NuGet, мы разрешили многие проблемы в рамках этого выпуска.</span><span class="sxs-lookup"><span data-stu-id="4e0cd-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="4e0cd-114">Вот краткий список некоторых из наиболее важных проблем, которые решаются:</span><span class="sxs-lookup"><span data-stu-id="4e0cd-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="4e0cd-115">В рамках переименования K Framework для ASP.NET 5 моникеры платформы были обновлены для работы со [ссылками](https://github.com/NuGet/Home/issues/215) DNX и днкскоре</span><span class="sxs-lookup"><span data-stu-id="4e0cd-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="4e0cd-116">Добавлена справочная документация [по ссылкам в пользовательском](https://github.com/NuGet/Home/issues/232) интерфейсе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e0cd-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="4e0cd-117">Улучшенная обработка сложных ссылок в `.nuspec` с помощью [ссылки](https://github.com/NuGet/Home/issues/276) на структуру ссылок в среде с разделителями-запятыми</span><span class="sxs-lookup"><span data-stu-id="4e0cd-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="4e0cd-118">Исправлена поддержка [ссылки](https://github.com/NuGet/Home/issues/253) на японские языки и региональные параметры</span><span class="sxs-lookup"><span data-stu-id="4e0cd-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="4e0cd-119">Обновленный клиент, позволяющий проектам ASP.NET 5 использовать новую [ссылку](https://github.com/NuGet/Home/issues/219) v3 Endpoints</span><span class="sxs-lookup"><span data-stu-id="4e0cd-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="4e0cd-120">Обновлено для более эффективной работы с папкой пакетов с помощью [ссылки](https://github.com/NuGet/Home/issues/56) системы управления версиями</span><span class="sxs-lookup"><span data-stu-id="4e0cd-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="4e0cd-121">Исправлена поддержка [ссылки](https://github.com/NuGet/Home/issues/17) на вспомогательные пакеты</span><span class="sxs-lookup"><span data-stu-id="4e0cd-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="4e0cd-122">Исправлена поддержка [ссылки](https://github.com/NuGet/Home/issues/18) на файлы содержимого, относящиеся к платформе</span><span class="sxs-lookup"><span data-stu-id="4e0cd-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="4e0cd-123">Ремонт присутствия GitHub</span><span class="sxs-lookup"><span data-stu-id="4e0cd-123">GitHub presence overhaul</span></span>

<span data-ttu-id="4e0cd-124">Мы внесли некоторые изменения в [репозитории исходного кода на сайте GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="4e0cd-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="4e0cd-125">Если у вас возникли проблемы с клиентом NuGet для Visual Studio, командами PowerShell или исполняемым файлом командной строки, вы можете зарегистрировать эти проблемы и отслеживать ход их выполнения в [списке проблем в домашнем репозитории GitHub](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="4e0cd-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="4e0cd-126">Мы отслеживаем проблемы для коллекции в нашем [репозитории GitHub нужетгаллери](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="4e0cd-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="4e0cd-127">Оставайтесь в курсе</span><span class="sxs-lookup"><span data-stu-id="4e0cd-127">Stay Tuned</span></span>

<span data-ttu-id="4e0cd-128">Следите за [нашим блогом](http://blog.nuget.org) , чтобы получить дополнительные сведения о ходе и объявлениях для NuGet 3,0!</span><span class="sxs-lookup"><span data-stu-id="4e0cd-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>