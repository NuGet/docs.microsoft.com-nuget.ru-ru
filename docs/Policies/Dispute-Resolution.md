---
title: "Разрешение споров в отношении имен пакетов NuGet | Документация Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Процесс разрешения споров в связи с фирменной символикой и товарными знаками, а также других конфликтных ситуаций между издателями пакетов NuGet."
keywords: "споры в связи с пакетами NuGet, разрешения споров в связи с NuGet, процесс разрешения споров"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 589fe4e7d2b05f3d589dcc70e78e7199d7e717c8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="a91ee-104">Разрешение споров в отношении имен пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="a91ee-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="a91ee-105">В этой статье представлен рекомендованный процесс разрешения споров, возникающих у участников сообщества с другими издателями NuGet.</span><span class="sxs-lookup"><span data-stu-id="a91ee-105">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="a91ee-106">Например, предположим, что компания Northwind Traders создает систему CRM, для которой она предоставляет драйверы клиента в виде файла MSI, доступного для скачивания на веб-сайте компании.</span><span class="sxs-lookup"><span data-stu-id="a91ee-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="a91ee-107">Анна, независимый разработчик, хочет упростить использование клиентской библиотеки Northwind и преобразует ее в пакет NuGet с именем `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="a91ee-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="a91ee-108">Позднее компания Northwind решает предоставить собственный официальный пакет NuGet со своей клиентской библиотекой и поэтому желает оспорить право собственности Анны на имя пакета.</span><span class="sxs-lookup"><span data-stu-id="a91ee-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="a91ee-109">В этой ситуации у Анны, очевидно, не было плохих намерений. Она хотела помочь пользователям продукта Northwind и потратила на это свои усилия и время.</span><span class="sxs-lookup"><span data-stu-id="a91ee-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="a91ee-110">В то же время компания Northwind является законным владельцем имени Northwind.</span><span class="sxs-lookup"><span data-stu-id="a91ee-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="a91ee-111">Следуя описанной ниже процедуре, компания Northwind и Анна могут совместно выработать приемлемое решение, так как обе стороны заинтересованы в помощи сообществу разработчиков.</span><span class="sxs-lookup"><span data-stu-id="a91ee-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="a91ee-112">Участие команды NuGet, как правило, не требуется. Такие ситуации лучше всего урегулировать самим сторонам спора.</span><span class="sxs-lookup"><span data-stu-id="a91ee-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="a91ee-113">До сих пор практически все споры, которые доводились до сведения команды NuGet, урегулировались без вынесения решения этой командой.</span><span class="sxs-lookup"><span data-stu-id="a91ee-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>

## <a name="process"></a><span data-ttu-id="a91ee-114">Процесс</span><span class="sxs-lookup"><span data-stu-id="a91ee-114">Process</span></span>

1. <span data-ttu-id="a91ee-115">Свяжитесь с владельцами пакета, в отношении которого возник спор, с помощью ссылки **Contact Owners** (Связаться с владельцами) на странице со сведениями о пакете.</span><span class="sxs-lookup"><span data-stu-id="a91ee-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="a91ee-116">Опишите проблему прямо, но вежливо.</span><span class="sxs-lookup"><span data-stu-id="a91ee-116">Explain your issue in a kind and direct manner.</span></span>
1. <span data-ttu-id="a91ee-117">Отправьте копию сообщения на адрес [support@nuget.org](mailto:support@nuget.org), чтобы поставить команду NuGet и .NET Foundation в известность о вашем споре.</span><span class="sxs-lookup"><span data-stu-id="a91ee-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
1. <span data-ttu-id="a91ee-118">Если через 30 дней спор не будет разрешен, отправьте повторное уведомление на адрес [support@nuget.org](mailto:support@nuget.org).</span><span class="sxs-lookup"><span data-stu-id="a91ee-118">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="a91ee-119">Служба поддержки nuget.org рассмотрит проблему и постарается урегулировать спор совместно с обеими сторонами.</span><span class="sxs-lookup"><span data-stu-id="a91ee-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
