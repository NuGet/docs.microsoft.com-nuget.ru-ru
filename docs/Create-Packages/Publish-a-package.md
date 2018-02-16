---
title: "Публикация пакета NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/05/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Подробные инструкции по публикации пакета NuGet на веб-сайте nuget.org или в закрытых веб-каналах, а также по управлению владением пакетом nuget.org."
keywords: "публикация пакета NuGet, владение пакетом NuGet, публикация на веб-сайте nuget.org, закрытые веб-каналы NuGet"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 610b20831b17ca5c1bae07546fde6eff3e2e43cc
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/14/2018
---
# <a name="publishing-packages"></a><span data-ttu-id="37a87-104">Публикация пакетов</span><span class="sxs-lookup"><span data-stu-id="37a87-104">Publishing packages</span></span>

<span data-ttu-id="37a87-105">После создания пакета и получения файла `.nukpg` его можно легко опубликовать для других разработчиков на общедоступных или закрытых ресурсах:</span><span class="sxs-lookup"><span data-stu-id="37a87-105">Once you have created a package and have your `.nukpg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="37a87-106">Открытые пакеты публикуются для других разработчиков на глобальном веб-сайте [nuget.org](https://www.nuget.org/packages/manage/upload), как описывается в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="37a87-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this topic.</span></span>
- <span data-ttu-id="37a87-107">Закрытые пакеты публикуются только для команд или организаций путем размещения на общем файловом ресурсе, закрытом сервере NuGet, в [среде управления пакетами Visual Studio Team Services](https://www.visualstudio.com/docs/package/nuget/publish) или стороннем репозитории, таком как myget, ProGet, Nexus Repository или Artifactory.</span><span class="sxs-lookup"><span data-stu-id="37a87-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="37a87-108">Дополнительные сведения см. в разделе [Общее сведения о размещении пакетов](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="37a87-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="37a87-109">В этом разделе описывается публикация на веб-сайте nuget.org. Сведения о публикации в Visual Studio Team Services см. в разделе [Управление пакетами](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="37a87-109">This topic covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="37a87-110">Публикация на веб-сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="37a87-110">Publish to nuget.org</span></span>

<span data-ttu-id="37a87-111">Для публикации на веб-сайте nuget.org необходимо [зарегистрировать бесплатную учетную запись](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) или войти в существующую:</span><span class="sxs-lookup"><span data-stu-id="37a87-111">For nuget.org, you must first [register for a free account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or sign in if already registered:</span></span>

![Место регистрации и входа в NuGet](media/publish_NuGetSignIn.png)

<span data-ttu-id="37a87-113">Далее можно отправить пакет через веб-портал nuget.org, выполнить принудительную отправку на веб-сайт nuget.org из командной строки (требуется `nuget.exe` 4.1.0 или более поздней версии) или опубликовать в рамках процесса непрерывной интеграции и развертывания через Visual Studio Team Services, как описывается в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="37a87-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="37a87-114">Веб-портал. Использование вкладки Upload Package (Отправить пакет) на сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="37a87-114">Web portal: use the Upload Package tab on nuget.org</span></span>

![Отправка пакета с помощью диспетчера пакетов NuGet](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a><span data-ttu-id="37a87-116">Командная строка</span><span class="sxs-lookup"><span data-stu-id="37a87-116">Command line</span></span>

> [!Important]
> <span data-ttu-id="37a87-117">Для принудительной отправки пакетов на веб-сайт nuget.org необходимо использовать [nuget.exe версии 4.1.0 или более поздней](https://www.nuget.org/downloads), где реализуются требуемые [протоколы NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="37a87-117">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="37a87-118">Щелкните свое имя пользователя, чтобы перейти к параметрам учетной записи.</span><span class="sxs-lookup"><span data-stu-id="37a87-118">Click on your user name to navigate to your account settings.</span></span>
1. <span data-ttu-id="37a87-119">В разделе **Ключ API** щелкните **Копировать в буфер обмена**, чтобы получить ключ доступа, который потребуется в интерфейсе командной строки:</span><span class="sxs-lookup"><span data-stu-id="37a87-119">Under **API Key**, click **copy to clipboard** to retrieve the access key you need in the CLI:</span></span>

    ![Копирование ключа API из параметров учетной записи](media/publish_APIKey.png)

1. <span data-ttu-id="37a87-121">В командной строке выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37a87-121">At a command prompt, run the following command:</span></span>

    ```cli
    nuget setApiKey Your-API-Key
    ```

    <span data-ttu-id="37a87-122">Ключ API будет сохранен на компьютере, поэтому вам не потребуется выполнять этот шаг снова на том же компьютере.</span><span class="sxs-lookup"><span data-stu-id="37a87-122">This stores your API key on the machine so that you need not do this step again on the same machine.</span></span>

1. <span data-ttu-id="37a87-123">Выполните принудительную отправку в коллекцию NuGet с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="37a87-123">Push your package to NuGet Gallery using the command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="37a87-124">Перед публикацией все пакеты, загружаемые на веб-сайт nuget.org, проверяются на вирусы и в случае обнаружения вирусов отклоняются.</span><span class="sxs-lookup"><span data-stu-id="37a87-124">Before being made public, all packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="37a87-125">Кроме того, периодическую проверку проходят все пакеты, представленные на веб-сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="37a87-125">All packages listed on nuget.org are also scanned periodically.</span></span>

1. <span data-ttu-id="37a87-126">В своей учетной записи на веб-сайте nuget.org щелкните **Manage my packages** (Управление моими пакетами), чтобы просмотреть только что опубликованный вами пакет. Кроме того, вы получите подтверждение по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="37a87-126">In your account on nuget.org, click **Manage my packages** to see the one that you just published; you also receive a confirmation email.</span></span> <span data-ttu-id="37a87-127">Обратите внимание, что пакет индексируется и будет появляться в результатах поиска для других пользователей спустя определенное время. В этот период на странице вашего пакета будет отображаться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="37a87-127">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

    ![Сообщение о том, что пакет не индексирован](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a><span data-ttu-id="37a87-129">Проверка и индексирование пакета</span><span class="sxs-lookup"><span data-stu-id="37a87-129">Package validation and indexing</span></span>

<span data-ttu-id="37a87-130">Пакеты, передаваемые на веб-сайт NuGet.org, проходят несколько проверок.</span><span class="sxs-lookup"><span data-stu-id="37a87-130">Packages pushed to NuGet.org undergo several validations.</span></span> <span data-ttu-id="37a87-131">После того как пакет пройдет все проверки, он будет индексирован и появится в результатах поиска спустя некоторое время.</span><span class="sxs-lookup"><span data-stu-id="37a87-131">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="37a87-132">По завершении индексирования вы получите по электронной почте подтверждение о том, что пакет был успешно опубликован.</span><span class="sxs-lookup"><span data-stu-id="37a87-132">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="37a87-133">Если пакет не проходит проверку, на странице сведений о пакете отображается соответствующее уведомление об ошибке и вы также получите сообщение электронной почты с уведомлением.</span><span class="sxs-lookup"><span data-stu-id="37a87-133">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="37a87-134">Проверка и индексирование пакета обычно занимает около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="37a87-134">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="37a87-135">Если публикация пакета занимает больше времени, перейдите на веб-сайт [status.nuget.org](https://status.nuget.org/) и убедитесь, что портал NuGet.org работает.</span><span class="sxs-lookup"><span data-stu-id="37a87-135">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="37a87-136">Если все системы исправны, но пакет не был опубликован в течение часа, войдите на веб-сайт NuGet.org и свяжитесь с нами по ссылке "Связаться со службой поддержки" на странице пакета.</span><span class="sxs-lookup"><span data-stu-id="37a87-136">If all systems are operational and the package hasn't been successfully published within an hour, please login to NuGet.org and contact us using the Contact Support link on the package page.</span></span>

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="37a87-137">Visual Studio Team Services (непрерывная интеграция и развертывание)</span><span class="sxs-lookup"><span data-stu-id="37a87-137">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="37a87-138">Если вы отправляете пакеты на веб-сайт nuget.org с использованием Visual Studio Team Services в рамках процесса непрерывной интеграции и развертывания, необходимо использовать `nuget.exe` 4.1 или более поздней версии в задачах NuGet.</span><span class="sxs-lookup"><span data-stu-id="37a87-138">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="37a87-139">Дополнительные сведения см. в разделе [Использование последней версии NuGet в сборках](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (блог Microsoft DevOps).</span><span class="sxs-lookup"><span data-stu-id="37a87-139">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="37a87-140">Управление владельцами пакетов на веб-сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="37a87-140">Managing package owners on nuget.org</span></span>

<span data-ttu-id="37a87-141">Несмотря на то, что в файле `.nuspec` каждого пакета NuGet определены авторы пакета, в коллекции nuget.org эти метаданные не используются для определения владельцев.</span><span class="sxs-lookup"><span data-stu-id="37a87-141">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="37a87-142">Вместо этого веб-сайт nuget.org назначает первичные права владения пользователю, который публикует пакет.</span><span class="sxs-lookup"><span data-stu-id="37a87-142">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="37a87-143">Это может быть выполнивший вход в систему пользователь, который отправил пакет через пользовательский интерфейс nuget.org, или пользователь, чей ключ API использовался в команде `nuget SetApiKey` или `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="37a87-143">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="37a87-144">Все владельцы пакета имеют полные разрешения на него, в том числе на добавление и удаление других владельцев, а также на публикацию обновлений.</span><span class="sxs-lookup"><span data-stu-id="37a87-144">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="37a87-145">Чтобы изменить владельца пакета, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="37a87-145">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="37a87-146">Войдите на веб-сайт nuget.org, используя учетную запись текущего владельца пакета.</span><span class="sxs-lookup"><span data-stu-id="37a87-146">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="37a87-147">Щелкните свое имя пользователя, выберите **Управление моими пакетами** и затем щелкните нужный пакет.</span><span class="sxs-lookup"><span data-stu-id="37a87-147">Click on your username, then on **Manage my packages**, then on the package you want to manage.</span></span>
1. <span data-ttu-id="37a87-148">Щелкните ссылку **Управление владельцами** слева.</span><span class="sxs-lookup"><span data-stu-id="37a87-148">Click the **Manage owners** link on the left side.</span></span>

<span data-ttu-id="37a87-149">В этом разделе можно выполнить разные действия:</span><span class="sxs-lookup"><span data-stu-id="37a87-149">From here you have several options:</span></span>

1. <span data-ttu-id="37a87-150">Чтобы добавить владельца, введите имя соответствующей учетной записи NuGet и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="37a87-150">To add an owner, enter their NuGet account name and click **Add**.</span></span> <span data-ttu-id="37a87-151">После этого новому совладельцу будет отправлено сообщение электронной почты со ссылкой для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="37a87-151">This sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="37a87-152">После подтверждения этот пользователь получит полные права доступа для добавления и удаления владельцев.</span><span class="sxs-lookup"><span data-stu-id="37a87-152">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="37a87-153">(Пока не будет выполнено подтверждение, на странице **Управление владельцами** для этого пользователя будет отображаться уведомление об ожидании утверждения.)</span><span class="sxs-lookup"><span data-stu-id="37a87-153">(Until confirmed, the **Manage owners** page indicates "pending approval" for that person).</span></span>
1. <span data-ttu-id="37a87-154">Чтобы удалить владельца, щелкните его имя на странице **Управление владельцами** и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="37a87-154">To remove an owner, select their name on the **Manage owners** and click **Remove**.</span></span>
1. <span data-ttu-id="37a87-155">Чтобы передать права владельца (например, в случае смены владельца или публикации с использованием неверной учетной записи), добавьте нового владельца и после получения подтверждения от него попросите удалить вашего пользователя из списка.</span><span class="sxs-lookup"><span data-stu-id="37a87-155">To transfer ownership (as when ownership changes or a package was published under the wrong account), simply add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="37a87-156">Чтобы назначить права владения компании или группе, создайте учетную запись на веб-сайте nuget.org с использованием псевдонима электронной почты, который пересылается соответствующим членам группы.</span><span class="sxs-lookup"><span data-stu-id="37a87-156">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="37a87-157">Например, многие пакеты ASP.NET корпорации Майкрософт находятся в совместном владении учетных записей [microsoft](http://nuget.org/profiles/microsoft) и [aspnet](http://nuget.org/profiles/aspnet), которые представляют собой подобные псевдонимы.</span><span class="sxs-lookup"><span data-stu-id="37a87-157">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="37a87-158">Восстановление прав владения пакетом</span><span class="sxs-lookup"><span data-stu-id="37a87-158">Recovering package ownership</span></span>

<span data-ttu-id="37a87-159">В некоторых случаях у пакета может отсутствовать активный владелец.</span><span class="sxs-lookup"><span data-stu-id="37a87-159">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="37a87-160">Например, исходный владелец может покинуть компанию, которая создает пакет, могут быть утрачены учетные данные nuget.org или из-за предыдущих ошибок в коллекции пакет может остаться без владельца.</span><span class="sxs-lookup"><span data-stu-id="37a87-160">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="37a87-161">Если вы являетесь полноправным владельцем пакета и хотите восстановить права владения, воспользуйтесь [формой для связи](https://www.nuget.org/policies/Contact) на веб-сайте nuget.org и опишите вашу ситуацию сотруднику NuGet.</span><span class="sxs-lookup"><span data-stu-id="37a87-161">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="37a87-162">После этого мы проверим ваши права владения пакетом, в том числе попытаемся найти существующего владельца по URL-адресу проекта пакета, через Twitter по электронной почте или другими способами.</span><span class="sxs-lookup"><span data-stu-id="37a87-162">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="37a87-163">Если эти способы не помогут, мы пришлем вам новое приглашение стать владельцем.</span><span class="sxs-lookup"><span data-stu-id="37a87-163">But if all else fails, we can send you a new invite to become an owner.</span></span>
