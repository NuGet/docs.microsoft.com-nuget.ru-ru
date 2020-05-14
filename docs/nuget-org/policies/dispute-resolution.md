---
title: Разрешение споров в отношении имен пакетов NuGet
description: Процесс разрешения споров в связи с фирменной символикой и товарными знаками, а также других конфликтных ситуаций между издателями пакетов NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 7e725d8114cde3de189dc3a648bc5a6c0b0e785b
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367951"
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="5bfec-103">Разрешение споров в отношении имен пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="5bfec-103">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="5bfec-104">В этой статье представлен рекомендованный процесс разрешения споров, возникающих у участников сообщества с другими издателями NuGet.</span><span class="sxs-lookup"><span data-stu-id="5bfec-104">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="5bfec-105">Например, предположим, что компания Northwind Traders создает систему CRM, для которой она предоставляет драйверы клиента в виде файла MSI, доступного для скачивания на веб-сайте компании.</span><span class="sxs-lookup"><span data-stu-id="5bfec-105">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="5bfec-106">Анна, независимый разработчик, хочет упростить использование клиентской библиотеки Northwind и преобразует ее в пакет NuGet с именем `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="5bfec-106">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="5bfec-107">Позднее компания Northwind решает предоставить собственный официальный пакет NuGet со своей клиентской библиотекой и поэтому желает оспорить право собственности Анны на имя пакета.</span><span class="sxs-lookup"><span data-stu-id="5bfec-107">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="5bfec-108">В этой ситуации у Анны, очевидно, не было плохих намерений. Она хотела помочь пользователям продукта Northwind и потратила на это свои усилия и время.</span><span class="sxs-lookup"><span data-stu-id="5bfec-108">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="5bfec-109">В то же время компания Northwind является законным владельцем имени Northwind.</span><span class="sxs-lookup"><span data-stu-id="5bfec-109">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="5bfec-110">Следуя описанной ниже процедуре, компания Northwind и Анна могут совместно выработать приемлемое решение, так как обе стороны заинтересованы в помощи сообществу разработчиков.</span><span class="sxs-lookup"><span data-stu-id="5bfec-110">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="5bfec-111">Участие команды NuGet, как правило, не требуется. Такие ситуации лучше всего урегулировать самим сторонам спора.</span><span class="sxs-lookup"><span data-stu-id="5bfec-111">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span>

## <a name="process"></a><span data-ttu-id="5bfec-112">Процесс</span><span class="sxs-lookup"><span data-stu-id="5bfec-112">Process</span></span>

1. <span data-ttu-id="5bfec-113">Свяжитесь с владельцами пакета, в отношении которого возник спор, с помощью ссылки **Contact Owners** (Связаться с владельцами) на странице со сведениями о пакете.</span><span class="sxs-lookup"><span data-stu-id="5bfec-113">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="5bfec-114">Опишите проблему прямо, но вежливо.</span><span class="sxs-lookup"><span data-stu-id="5bfec-114">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="5bfec-115">Отправьте копию сообщения на адрес [support@nuget.org](mailto:support@nuget.org), чтобы поставить команду NuGet и .NET Foundation в известность о вашем споре.</span><span class="sxs-lookup"><span data-stu-id="5bfec-115">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="5bfec-116">Если через 30 дней спор не будет разрешен, отправьте повторное уведомление на адрес [support@nuget.org](mailto:support@nuget.org).</span><span class="sxs-lookup"><span data-stu-id="5bfec-116">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="5bfec-117">Служба поддержки nuget.org рассмотрит проблему и постарается урегулировать спор совместно с обеими сторонами.</span><span class="sxs-lookup"><span data-stu-id="5bfec-117">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
