---
title: Заметки о выпуске версии-Кандидата NuGet 3.0
description: Заметки о выпуске для NuGet 3.0 RC, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551723"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="bccae-103">Заметки о выпуске версии-Кандидата NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="bccae-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="bccae-104">[Заметки о выпуске бета-версия NuGet 3.0](../release-notes/nuget-3.0-beta.md) | [заметки о выпуске NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="bccae-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="bccae-105">NuGet 3.0 RC было выпущено 29 апреля 2015 г. с выпуском Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="bccae-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="bccae-106">Этот выпуск содержит ряд важных исправлений, повышение производительности и обновления для поддержки новых платформ.</span><span class="sxs-lookup"><span data-stu-id="bccae-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="bccae-107">Он доступен только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="bccae-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="bccae-108">Не теряя производительности</span><span class="sxs-lookup"><span data-stu-id="bccae-108">Continued Focus on Performance</span></span>

<span data-ttu-id="bccae-109">Стабильность и производительность запросов NuGet продолжать пристальное внимание, мы сосредоточились на.</span><span class="sxs-lookup"><span data-stu-id="bccae-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="bccae-110">В этом выпуске должны начать появляться операций очень быстрого поиска в веб-сайт и пользовательский Интерфейс NuGet.</span><span class="sxs-lookup"><span data-stu-id="bccae-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="bccae-111">Мы выполним мониторинг службы и как использовать службы таким образом, мы можете продолжить изменять эти операции.</span><span class="sxs-lookup"><span data-stu-id="bccae-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="bccae-112">Значительные проблемы решены</span><span class="sxs-lookup"><span data-stu-id="bccae-112">Significant Issues Resolved</span></span>

<span data-ttu-id="bccae-113">Чтобы стабилизировать клиенты NuGet, в этом выпуске устранен многих проблем.</span><span class="sxs-lookup"><span data-stu-id="bccae-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="bccae-114">Ниже приведен лишь краткий перечень некоторые из более важных проблем, устраненных:</span><span class="sxs-lookup"><span data-stu-id="bccae-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="bccae-115">В процессе переименования платформы K для ASP.NET 5, моникеры платформ были обновлены для обработки dnx и dnxcore [ссылку](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="bccae-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="bccae-116">Добавить справочную документацию по ссылкам в пользовательском Интерфейсе Visual Studio [ссылку](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="bccae-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="bccae-117">Более эффективная обработка сложных ссылок в `.nuspec` с помощью ссылки на платформу с разделителями запятыми [ссылку](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="bccae-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="bccae-118">Исправлена поддержка японский языки и региональные параметры [ссылку](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="bccae-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="bccae-119">Обновленный клиент, чтобы разрешить проектов ASP.NET 5 использовать новые конечные точки v3 [ссылку](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="bccae-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="bccae-120">Обновленные лучше дескриптор папку пакетов с системой управления версиями [ссылку](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="bccae-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="bccae-121">Исправлена поддержка вспомогательные пакеты [ссылку](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="bccae-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="bccae-122">Исправлена поддержка файлы содержимого для определенных платформ [ссылку](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="bccae-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="bccae-123">Наличие пересмотренную GitHub</span><span class="sxs-lookup"><span data-stu-id="bccae-123">GitHub presence overhaul</span></span>

<span data-ttu-id="bccae-124">Мы внесли некоторые изменения, чтобы наши [репозитории исходного кода на GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="bccae-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="bccae-125">Если у вас возникли проблемы с помощью клиента NuGet для Visual Studio, команды Powershell или командной строки исполняемый файл можно войти эти проблемы и отслеживать ход их выполнения на наших [список проблем в репозитории GitHub домашней](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="bccae-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="bccae-126">Мы отслеживаем проблемы для коллекции в наших [репозитория GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="bccae-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="bccae-127">Следите за новостями</span><span class="sxs-lookup"><span data-stu-id="bccae-127">Stay Tuned</span></span>

<span data-ttu-id="bccae-128">Пожалуйста, обратите внимание на [наш блог](http://blog.nuget.org) дополнительные ход выполнения и объявления для NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="bccae-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>