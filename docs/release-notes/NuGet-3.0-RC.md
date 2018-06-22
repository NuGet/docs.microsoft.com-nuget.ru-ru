---
title: Заметки о выпуске версии-Кандидата NuGet 3.0
description: Заметки о выпуске для RC NuGet 3.0, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 28ac49d9e9071d16d20b24808abb0acaab214ffd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819602"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="ba282-103">Заметки о выпуске версии-Кандидата NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="ba282-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="ba282-104">[Заметки о выпуске бета-версии NuGet 3.0](../release-notes/nuget-3.0-beta.md) | [заметки о выпуске версии-кандидата 2 NuGet 3.0](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="ba282-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="ba282-105">Версия-Кандидат NuGet 3.0 был выпущен 29 апреля 2015 г. с выпуском Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="ba282-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="ba282-106">Этот выпуск содержит ряд важных исправлений, повышение производительности и обновления для поддержки новых платформ.</span><span class="sxs-lookup"><span data-stu-id="ba282-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="ba282-107">Она доступна только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ba282-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="ba282-108">О производительности</span><span class="sxs-lookup"><span data-stu-id="ba282-108">Continued Focus on Performance</span></span>

<span data-ttu-id="ba282-109">Стабильность и производительность запросов NuGet остаются горячей раздела, мы сосредоточены на.</span><span class="sxs-lookup"><span data-stu-id="ba282-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="ba282-110">В этом выпуске необходимо запустить для просмотра операций очень быстрый поиск в NuGet пользовательского интерфейса и веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="ba282-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="ba282-111">Мы отслеживании службу и как использовать службы, чтобы мы могли продолжать для настройки этих операций.</span><span class="sxs-lookup"><span data-stu-id="ba282-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="ba282-112">Значительные устранения проблем</span><span class="sxs-lookup"><span data-stu-id="ba282-112">Significant Issues Resolved</span></span>

<span data-ttu-id="ba282-113">Чтобы стабилизировать клиенты NuGet, была решена много проблем в рамках этого выпуска.</span><span class="sxs-lookup"><span data-stu-id="ba282-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="ba282-114">Ниже приведен лишь краткий перечень некоторые более важные устранения проблем:</span><span class="sxs-lookup"><span data-stu-id="ba282-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="ba282-115">В ходе переименования K framework для ASP.NET 5, были обновлены моникеров платформы для обработки dnx и dnxcore [ссылку](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="ba282-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="ba282-116">Добавлено в справочной документации по ссылкам в пользовательском Интерфейсе Visual Studio [ссылку](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="ba282-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="ba282-117">Лучше обработка сложных ссылок в `.nuspec` со ссылками с разделителями запятыми framework [ссылку](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="ba282-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="ba282-118">Исправлена поддержки японского языка и региональных параметров [ссылку](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="ba282-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="ba282-119">Обновленный клиент, чтобы разрешить проекты ASP.NET 5, чтобы использовать новые конечные точки v3 [ссылку](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="ba282-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="ba282-120">Обновленные лучше дескриптор папку пакеты с системой управления версиями [ссылку](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="ba282-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="ba282-121">Исправлена поддержка вспомогательных пакетов [ссылку](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="ba282-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="ba282-122">Исправлено поддержка специфичная для платформы файлы содержимого [ссылку](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="ba282-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="ba282-123">Пересмотренную видеодрайверов присутствие GitHub</span><span class="sxs-lookup"><span data-stu-id="ba282-123">GitHub presence overhaul</span></span>

<span data-ttu-id="ba282-124">Мы внесли некоторые изменения в наших [источника репозитории кода на GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="ba282-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="ba282-125">При наличии проблем с помощью клиента NuGet Visual Studio, команды Powershell или командной строки исполняемый файл можно войти этих проблем и отслеживать ход выполнения работ в нашем [списка проблем репозитория GitHub домашней](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="ba282-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="ba282-126">Мы отслеживаем проблемы для коллекции на нашем [репозитория GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="ba282-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="ba282-127">Следите за новостями</span><span class="sxs-lookup"><span data-stu-id="ba282-127">Stay Tuned</span></span>

<span data-ttu-id="ba282-128">Пожалуйста, обратите внимание на [наш блог](http://blog.nuget.org) дополнительные хода выполнения и объявления для NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="ba282-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>