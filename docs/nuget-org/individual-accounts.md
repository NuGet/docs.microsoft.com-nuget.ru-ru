---
title: Индивидуальные учетные записи — NuGet.org
description: Для публикации пакетов требуются индивидуальные учетные записи на сайте NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: d032b69f6eb4cbd3687ca60190c15aed9b7a4d79
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323899"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="362b6-103">Индивидуальные учетные записи на NuGet.org</span><span class="sxs-lookup"><span data-stu-id="362b6-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="362b6-104">Чтобы осуществлять публикацию пакетов на сайте NuGet.org и управлять ими, вам необходимо создать индивидуальную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="362b6-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="362b6-105">Сравнение индивидуальных учетных записей и учетных записей организаций</span><span class="sxs-lookup"><span data-stu-id="362b6-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="362b6-106">Ваша индивидуальная (пользовательская) учетная запись является вашим удостоверением на сайте NuGet.org и может являться членом любой организации.</span><span class="sxs-lookup"><span data-stu-id="362b6-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="362b6-107">Пакет может принадлежать учетной записи организации так же, как и индивидуальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="362b6-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="362b6-108">Для потребителей пакета нет никаких различий между индивидуальной учетной записью и учетной записью организации. Обе они отображаются как объекты `owners` для пакета.</span><span class="sxs-lookup"><span data-stu-id="362b6-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="362b6-109">В учетную запись организации могут входить в качестве членов одна или несколько индивидуальных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="362b6-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="362b6-110">Эти члены могут управлять набором пакетов, используя для этого единое удостоверение владельца.</span><span class="sxs-lookup"><span data-stu-id="362b6-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="362b6-111">Добавление новой индивидуальной учетной записи</span><span class="sxs-lookup"><span data-stu-id="362b6-111">Add a new individual account</span></span>

<span data-ttu-id="362b6-112">Чтобы создать учетную запись NuGet.org, нужно иметь личную учетную запись Майкрософт (MSA) или учетную запись Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="362b6-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="362b6-113">Если у вас нет такой учетной записи, можете [создать](https://signup.live.com) ее.</span><span class="sxs-lookup"><span data-stu-id="362b6-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="362b6-114">Если у вас есть учетная запись MSA или AAD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="362b6-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="362b6-115">Перейдите на [страницу входа на сайт NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="362b6-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="362b6-116">Нажмите кнопку **Вход с помощью учетной записи Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="362b6-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="362b6-117">Введите данные своей учетной записи Майкрософт или Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="362b6-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="362b6-118">Щелкните **Да**, чтобы принять разрешения, которые требуется предоставить приложению *NuGet.org*.</span><span class="sxs-lookup"><span data-stu-id="362b6-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Предоставление разрешений приложению NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="362b6-120">Вы будете перенаправлены на сайт *nuget.org* и получите запрос на ввод имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="362b6-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="362b6-121">Укажите имя пользователя в поле ввода.</span><span class="sxs-lookup"><span data-stu-id="362b6-121">Specify the username in the input box.</span></span> <span data-ttu-id="362b6-122">Обратите внимание, что имя пользователя **вводится** с учетом регистра и не может быть изменено позднее.</span><span class="sxs-lookup"><span data-stu-id="362b6-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Ввод имени пользователя в приложении NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="362b6-124">Нажмите кнопку **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="362b6-124">Click the **Register** button.</span></span>

<span data-ttu-id="362b6-125">Теперь у вас есть учетная запись NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="362b6-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="362b6-126">Управлять учетными записями можно на странице [параметров учетной записи](https://www.nuget.org/account).</span><span class="sxs-lookup"><span data-stu-id="362b6-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="362b6-127">Включение двухфакторной проверки подлинности (2FA)</span><span class="sxs-lookup"><span data-stu-id="362b6-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="362b6-128">Двухфакторная проверка подлинности — это дополнительный слой обеспечения безопасности, используемый при входе на веб-сайты или в приложения.</span><span class="sxs-lookup"><span data-stu-id="362b6-128">Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps.</span></span> <span data-ttu-id="362b6-129">При ее использовании необходимо войти в систему с помощью учетной записи Майкрософт и пройти проверку подлинности еще одним способом, который известен или доступен только вам.</span><span class="sxs-lookup"><span data-stu-id="362b6-129">With 2FA, you have to log in with your Microsoft Account (MSA) and provide another form of authentication that only you know or have access to.</span></span> <span data-ttu-id="362b6-130">Чтобы лучше защитить учетную запись, включите двухфакторную проверку подлинности (рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="362b6-130">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="362b6-131">Войдя в учетную запись, откройте профиль и выберите **Включить** в разделе **Учетная запись входа**.</span><span class="sxs-lookup"><span data-stu-id="362b6-131">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![Включение 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="362b6-133">Вы увидите сообщение о том, что при следующем входе в *nuget.org* вам будет предложено ввести дополнительные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="362b6-133">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="362b6-134">Чтобы завершить проверку подлинности, выйдите из учетной записи и снова войдите.</span><span class="sxs-lookup"><span data-stu-id="362b6-134">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="362b6-135">При входе выберите в качестве второй формы проверки подлинности текст или электронное письмо.</span><span class="sxs-lookup"><span data-stu-id="362b6-135">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="362b6-136">Проверьте номер телефона или адрес электронной почты, которые уже связаны с вашей учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="362b6-136">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="362b6-137">Может потребоваться ввести новые номер телефона или адрес электронной почты для своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="362b6-137">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="362b6-138">В таком случае введите необходимые сведения и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="362b6-138">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![Включение двухфакторной проверки подлинности и ввод номера телефона](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="362b6-140">Проверьте свое устройство или учетную запись электронной почты и введите только что отправленный код.</span><span class="sxs-lookup"><span data-stu-id="362b6-140">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![Включение двухфакторной проверки подлинности и ввод кода](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="362b6-142">Выполните дополнительные инструкции, чтобы выполнить двухфакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="362b6-142">Follow any additional instructions to complete Two-factor authentication.</span></span>

> [!Tip]
> <span data-ttu-id="362b6-143">Включение двухфакторной проверки подлинности для учетной записи NuGet.org не влияет на параметры проверки подлинности для других учетных записей или служб, которые связаны с учетной записью Майкрософт, используемой для входа в NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="362b6-143">Enabling 2FA for your NuGet.org account does not impact authentication settings for other accounts or services that may be linked to the Microsoft account you use to login to NuGet.org.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="362b6-144">Удаление учетной записи NuGet.org</span><span class="sxs-lookup"><span data-stu-id="362b6-144">Delete a NuGet.org account</span></span>

<span data-ttu-id="362b6-145">Сведения о дополнительных задачах, связанных с учетной записью, таких как удаление учетной записи NuGet.org, см. в разделе [Управление учетной записью NuGet.org](/nuget/nuget-org/nuget-org-faq#nuget.org-account-management).</span><span class="sxs-lookup"><span data-stu-id="362b6-145">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](/nuget/nuget-org/nuget-org-faq#nuget.org-account-management).</span></span>
