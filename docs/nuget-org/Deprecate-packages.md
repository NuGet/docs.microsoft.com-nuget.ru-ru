---
title: Объявление пакетов нерекомендуемыми на веб-сайте NuGet.org
description: Подробное описание процесса объявления пакетов нерекомендуемыми и отображения этих сведений в клиентах
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096886"
---
# <a name="deprecating-packages"></a><span data-ttu-id="83daf-103">Объявление пакетов нерекомендуемыми</span><span class="sxs-lookup"><span data-stu-id="83daf-103">Deprecating packages</span></span>

<span data-ttu-id="83daf-104">Пакет можно объявить нерекомендуемым в случае прекращения его поддержки или перевода потребителей на использование другого пакета.</span><span class="sxs-lookup"><span data-stu-id="83daf-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="83daf-105">Процедура объявления пакета нерекомендуемым отличается от **удаления пакета из списка**.</span><span class="sxs-lookup"><span data-stu-id="83daf-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="83daf-106">При **удалении пакета из списка** становится невозможным его обнаружение, так как он будет скрыт в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="83daf-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="83daf-107">При **объявлении пакета нерекомендуемым** существующие потребители пакета могут определять его установку или использование в проектах.</span><span class="sxs-lookup"><span data-stu-id="83daf-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="83daf-108">Кроме того, они могут узнать причину такого объявления и ознакомиться с альтернативным пакетом, предлагаемым его издателем.</span><span class="sxs-lookup"><span data-stu-id="83daf-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="83daf-109">Пакет, объявляемый нерекомендуемым, не удаляется из списка.</span><span class="sxs-lookup"><span data-stu-id="83daf-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="83daf-110">Издатель может и удалить пакет из списка, и объявить его нерекомендуемым.</span><span class="sxs-lookup"><span data-stu-id="83daf-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="83daf-111">Процесс объявления пакета нерекомендуемым</span><span class="sxs-lookup"><span data-stu-id="83daf-111">Deprecation workflow</span></span>
1. <span data-ttu-id="83daf-112">Чтобы объявить пакет нерекомендуемым, перейдите в раздел **Управление пакетами** и выберите **Объявить нерекомендуемым**.</span><span class="sxs-lookup"><span data-stu-id="83daf-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Переход к параметру объявления пакета нерекомендуемым](media/deprecation-select-option.png)

2. <span data-ttu-id="83daf-114">Выберите версию, которую нужно объявить нерекомендуемой.</span><span class="sxs-lookup"><span data-stu-id="83daf-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="83daf-115">Чтобы объявить нерекомендуемыми все версии, выберите параметр **Выбрать все версии**.</span><span class="sxs-lookup"><span data-stu-id="83daf-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Выбор версий пакета, объявляемых нерекомендуемыми](media/deprecation-select-version.png)

3. <span data-ttu-id="83daf-117">Выберите причину объявления пакета нерекомендуемым.</span><span class="sxs-lookup"><span data-stu-id="83daf-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="83daf-118">Если пакет больше не поддерживается, выберите параметр **Устаревший**.</span><span class="sxs-lookup"><span data-stu-id="83daf-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="83daf-119">Если в конкретной версии присутствует критическая ошибка, выберите параметр **содержит критические ошибки**.</span><span class="sxs-lookup"><span data-stu-id="83daf-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="83daf-120">Для любой другой причины выберите **Другое**.</span><span class="sxs-lookup"><span data-stu-id="83daf-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="83daf-121">Издатель всегда может указать альтернативный рекомендуемый пакет (и версию) и добавить настраиваемое сообщение для владельцев.</span><span class="sxs-lookup"><span data-stu-id="83daf-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Выбор причин для рекомендации альтернативного пакета и добавление настраиваемого сообщения](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="83daf-123">Настраиваемые сообщения отображаются только на сайте nuget.org. Из клиентов они не выводятся.</span><span class="sxs-lookup"><span data-stu-id="83daf-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="83daf-124">Сейчас настраиваемые сообщения недоступны в таких клиентах, как `dotnet.exe` и диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="83daf-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="83daf-125">Клиентский интерфейс для нерекомендуемых пакетов</span><span class="sxs-lookup"><span data-stu-id="83daf-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="83daf-126">После того как пакет объявляется нерекомендуемым, его потребители будут уведомлены об этом следующими способами (в зависимости от используемого клиента).</span><span class="sxs-lookup"><span data-stu-id="83daf-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="83daf-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="83daf-127">Visual Studio</span></span> 
<span data-ttu-id="83daf-128">*Доступно начиная с Visual Studio 2019 версии 16.3*</span><span class="sxs-lookup"><span data-stu-id="83daf-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="83daf-129">В Visual Studio предупреждение об использовании нерекомендуемого пакета выводится на вкладке `Installed`. В нем указывается пакет и приводятся сведения об объявлении его нерекомендуемым (включая причину этого объявления и альтернативный пакет, который можно использовать вместо него, если таковой имеется).</span><span class="sxs-lookup"><span data-stu-id="83daf-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Нерекомендуемые пакеты на вкладке "Установленные" диспетчера пакетов в Visual Studio](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="83daf-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="83daf-131">dotnet.exe</span></span>
<span data-ttu-id="83daf-132">*Доступно начиная с пакета SDK для .NET 3.0*</span><span class="sxs-lookup"><span data-stu-id="83daf-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="83daf-133">Если вы используете dotnet.exe, в папке решения или проекта можно выполнить команду `dotnet list package --deprecated` для получения списка нерекомендуемых пакетов и сведений об объявлении их нерекомендуемыми.</span><span class="sxs-lookup"><span data-stu-id="83daf-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
