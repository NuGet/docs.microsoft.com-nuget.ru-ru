---
title: Индивидуальные учетные записи
description: Для публикации пакетов требуются индивидуальные учетные записи на сайте NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427139"
---
# <a name="individual-accounts"></a><span data-ttu-id="38ca7-103">Индивидуальные учетные записи</span><span class="sxs-lookup"><span data-stu-id="38ca7-103">Individual accounts</span></span>

<span data-ttu-id="38ca7-104">Чтобы осуществлять публикацию пакетов на сайте NuGet.org и управлять ими, вам необходимо создать индивидуальную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="38ca7-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="38ca7-105">Сравнение индивидуальных учетных записей и учетных записей организаций</span><span class="sxs-lookup"><span data-stu-id="38ca7-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="38ca7-106">Ваша индивидуальная (пользовательская) учетная запись является вашим удостоверением на сайте NuGet.org и может являться членом любой организации.</span><span class="sxs-lookup"><span data-stu-id="38ca7-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="38ca7-107">Пакет может принадлежать учетной записи организации так же, как и индивидуальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="38ca7-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="38ca7-108">Для потребителей пакета нет никаких различий между индивидуальной учетной записью и учетной записью организации. Обе они отображаются как объекты `owners` для пакета.</span><span class="sxs-lookup"><span data-stu-id="38ca7-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="38ca7-109">В учетную запись организации могут входить в качестве членов одна или несколько индивидуальных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="38ca7-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="38ca7-110">Эти члены могут управлять набором пакетов, используя для этого единое удостоверение владельца.</span><span class="sxs-lookup"><span data-stu-id="38ca7-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="38ca7-111">Добавление новой индивидуальной учетной записи</span><span class="sxs-lookup"><span data-stu-id="38ca7-111">Add a new individual account</span></span>

<span data-ttu-id="38ca7-112">Чтобы создать учетную запись NuGet.org, нужно иметь личную учетную запись Майкрософт (MSA) или учетную запись Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="38ca7-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="38ca7-113">Если у вас нет такой учетной записи, можете [создать](https://signup.live.com) ее.</span><span class="sxs-lookup"><span data-stu-id="38ca7-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="38ca7-114">Если у вас есть учетная запись MSA или AAD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="38ca7-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="38ca7-115">Перейдите на [страницу входа на сайт NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="38ca7-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="38ca7-116">Нажмите кнопку **Вход с помощью учетной записи Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="38ca7-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="38ca7-117">Введите данные своей учетной записи Майкрософт или Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="38ca7-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="38ca7-118">Щелкните **Да**, чтобы принять разрешения, которые требуется предоставить приложению *NuGet.org*.</span><span class="sxs-lookup"><span data-stu-id="38ca7-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Предоставление разрешений приложению NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="38ca7-120">Вы будете перенаправлены на сайт *nuget.org* и получите запрос на ввод имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="38ca7-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="38ca7-121">Укажите имя пользователя в поле ввода.</span><span class="sxs-lookup"><span data-stu-id="38ca7-121">Specify the username in the input box.</span></span> <span data-ttu-id="38ca7-122">Обратите внимание, что имя пользователя **вводится** с учетом регистра и не может быть изменено позднее.</span><span class="sxs-lookup"><span data-stu-id="38ca7-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Ввод имени пользователя в приложении NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="38ca7-124">Нажмите кнопку **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="38ca7-124">Click the **Register** button.</span></span>

<span data-ttu-id="38ca7-125">Теперь у вас есть учетная запись NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="38ca7-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="38ca7-126">Управлять учетными записями можно на странице [параметров учетной записи](https://www.nuget.org/account).</span><span class="sxs-lookup"><span data-stu-id="38ca7-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
