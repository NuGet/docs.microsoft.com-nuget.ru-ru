---
title: Индивидуальные учетные записи
description: Для публикации пакетов требуются индивидуальные учетные записи на сайте NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: c88b88015bd6d5bae4789765126c0a3dec527e24
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419839"
---
# <a name="individual-accounts"></a><span data-ttu-id="f2b5f-103">Индивидуальные учетные записи</span><span class="sxs-lookup"><span data-stu-id="f2b5f-103">Individual accounts</span></span>

<span data-ttu-id="f2b5f-104">Чтобы осуществлять публикацию пакетов на сайте NuGet.org и управлять ими, вам необходимо создать индивидуальную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="f2b5f-105">Сравнение индивидуальных учетных записей и учетных записей организаций</span><span class="sxs-lookup"><span data-stu-id="f2b5f-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="f2b5f-106">Ваша индивидуальная (пользовательская) учетная запись является вашим удостоверением на сайте NuGet.org и может являться членом любой организации.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="f2b5f-107">Пакет может принадлежать учетной записи организации так же, как и индивидуальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="f2b5f-108">Для потребителей пакета нет никаких различий между индивидуальной учетной записью и учетной записью организации. Обе они отображаются как объекты `owners` для пакета.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="f2b5f-109">В учетную запись организации могут входить в качестве членов одна или несколько индивидуальных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="f2b5f-110">Эти члены могут управлять набором пакетов, используя для этого единое удостоверение владельца.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="f2b5f-111">Добавление новой индивидуальной учетной записи</span><span class="sxs-lookup"><span data-stu-id="f2b5f-111">Add a new individual account</span></span>

<span data-ttu-id="f2b5f-112">Чтобы создать учетную запись NuGet.org, нужно иметь личную учетную запись Майкрософт (MSA) или учетную запись Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="f2b5f-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="f2b5f-113">Если у вас нет такой учетной записи, можете [создать](https://signup.live.com) ее.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="f2b5f-114">Если у вас есть учетная запись MSA или AAD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="f2b5f-115">Перейдите на [страницу входа на сайт NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="f2b5f-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="f2b5f-116">Нажмите кнопку **Вход с помощью учетной записи Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="f2b5f-117">Введите данные своей учетной записи Майкрософт или Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="f2b5f-118">Щелкните **Да**, чтобы принять разрешения, которые требуется предоставить приложению *NuGet.org*.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Предоставление разрешений приложению NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="f2b5f-120">Вы будете перенаправлены на сайт *nuget.org* и получите запрос на ввод имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="f2b5f-121">Укажите имя пользователя в поле ввода.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-121">Specify the username in the input box.</span></span> <span data-ttu-id="f2b5f-122">Обратите внимание, что имя пользователя **вводится** с учетом регистра и не может быть изменено позднее.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Ввод имени пользователя в приложении NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="f2b5f-124">Нажмите кнопку **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-124">Click the **Register** button.</span></span>

<span data-ttu-id="f2b5f-125">Теперь у вас есть учетная запись NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="f2b5f-126">Управлять учетными записями можно на странице [параметров учетной записи](https://www.nuget.org/account).</span><span class="sxs-lookup"><span data-stu-id="f2b5f-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="f2b5f-127">Включение двухфакторной проверки подлинности (2FA)</span><span class="sxs-lookup"><span data-stu-id="f2b5f-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="f2b5f-128">Чтобы лучше защитить учетную запись, включите двухфакторную проверку подлинности (рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="f2b5f-128">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="f2b5f-129">Войдя в учетную запись, откройте профиль и выберите **Включить** в разделе **Учетная запись входа**.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-129">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![Включение 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="f2b5f-131">Вы увидите сообщение о том, что при следующем входе в *nuget.org* вам будет предложено ввести дополнительные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-131">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="f2b5f-132">Чтобы завершить проверку подлинности, выйдите из учетной записи и снова войдите.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-132">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="f2b5f-133">При входе выберите в качестве второй формы проверки подлинности текст или электронное письмо.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-133">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="f2b5f-134">Проверьте номер телефона или адрес электронной почты, которые уже связаны с вашей учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-134">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="f2b5f-135">Может потребоваться ввести новые номер телефона или адрес электронной почты для своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-135">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="f2b5f-136">В таком случае введите необходимые сведения и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-136">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![Включение 2FA](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="f2b5f-138">Проверьте свое устройство или учетную запись электронной почты и введите только что отправленный код.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-138">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![Включение 2FA](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="f2b5f-140">Выполните дополнительные инструкции, чтобы выполнить двухфакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="f2b5f-140">Follow any additional instructions to complete Two-factor authentication.</span></span>
