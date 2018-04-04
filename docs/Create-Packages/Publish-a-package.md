---
title: Публикация пакета NuGet | Документы Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Подробные инструкции по публикации пакета NuGet на веб-сайте nuget.org или в закрытых веб-каналах, а также по управлению владением пакетом nuget.org.
keywords: публикация пакета NuGet, владение пакетом NuGet, публикация на веб-сайте nuget.org, закрытые веб-каналы NuGet
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 68db25276297353fab03258adecd9169149dbe51
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="publishing-packages"></a><span data-ttu-id="21ad1-104">Публикация пакетов</span><span class="sxs-lookup"><span data-stu-id="21ad1-104">Publishing packages</span></span>

<span data-ttu-id="21ad1-105">После создания пакета и получения файла `.nukpg` его можно легко опубликовать для других разработчиков на общедоступных или закрытых ресурсах:</span><span class="sxs-lookup"><span data-stu-id="21ad1-105">Once you have created a package and have your `.nukpg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="21ad1-106">Открытые пакеты публикуются для других разработчиков на глобальном веб-сайте [nuget.org](https://www.nuget.org/packages/manage/upload), как описывается в этой статье (требуется NuGet 4.1.0+).</span><span class="sxs-lookup"><span data-stu-id="21ad1-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="21ad1-107">Закрытые пакеты публикуются только для команд или организаций путем размещения на общем файловом ресурсе, закрытом сервере NuGet, в [среде управления пакетами Visual Studio Team Services](https://www.visualstudio.com/docs/package/nuget/publish) или стороннем репозитории, таком как myget, ProGet, Nexus Repository или Artifactory.</span><span class="sxs-lookup"><span data-stu-id="21ad1-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="21ad1-108">Дополнительные сведения см. в разделе [Общее сведения о размещении пакетов](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="21ad1-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="21ad1-109">В этой статье описывается публикация на веб-сайте nuget.org. Сведения о публикации в Visual Studio Team Services см. в [этой статье](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="21ad1-109">This article covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="21ad1-110">Публикация на веб-сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="21ad1-110">Publish to nuget.org</span></span>

<span data-ttu-id="21ad1-111">Сначала необходимо войти на сайт nuget.org под учетной записью Майкрософт, с помощью которой на нем необходимо зарегистрироваться. Вы также можете войти с помощью учетной записи nuget.org, созданной в предыдущих версиях портала.</span><span class="sxs-lookup"><span data-stu-id="21ad1-111">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![Местоположение входа в NuGet](media/publish_NuGetSignIn.png)

<span data-ttu-id="21ad1-113">Далее можно отправить пакет через веб-портал nuget.org, выполнить принудительную отправку на веб-сайт nuget.org из командной строки (требуется `nuget.exe` 4.1.0 или более поздней версии) или опубликовать в рамках процесса непрерывной интеграции и развертывания через Visual Studio Team Services, как описывается в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="21ad1-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="21ad1-114">Веб-портал. Использование вкладки Upload Package (Отправить пакет) на сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="21ad1-114">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="21ad1-115">В верхнем меню сайта nuget.org выберите **Upload** (Передать) и перейдите к расположению пакета.</span><span class="sxs-lookup"><span data-stu-id="21ad1-115">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Передача пакета на сайт nuget.org](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="21ad1-117">На сайте nuget.org отображается, доступно ли имя пакета.</span><span class="sxs-lookup"><span data-stu-id="21ad1-117">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="21ad1-118">Если нет, необходимо изменить идентификатор пакета в проекте, перестроить его и попробовать отправить еще раз.</span><span class="sxs-lookup"><span data-stu-id="21ad1-118">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="21ad1-119">Если имя пакета доступно, на сайте nuget.org откроется раздел **Verify** (Проверка), в котором можно просмотреть метаданные из манифеста пакета.</span><span class="sxs-lookup"><span data-stu-id="21ad1-119">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="21ad1-120">Чтобы изменить метаданные, измените проект (файл проекта или файл`.nuspec`), перестройте его, повторно создайте пакет и загрузите еще раз.</span><span class="sxs-lookup"><span data-stu-id="21ad1-120">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="21ad1-121">В разделе **Import Documentation** (Импортировать документацию) вы можете вставить файл Markdown, добавить URL-адреса документов или передать файл документации.</span><span class="sxs-lookup"><span data-stu-id="21ad1-121">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="21ad1-122">После введения всех сведений нажмите кнопку **Submit** (Отправить).</span><span class="sxs-lookup"><span data-stu-id="21ad1-122">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="21ad1-123">Командная строка</span><span class="sxs-lookup"><span data-stu-id="21ad1-123">Command line</span></span>

<span data-ttu-id="21ad1-124">Для принудительной отправки пакетов на веб-сайт nuget.org необходимо использовать [nuget.exe версии 4.1.0 или более поздней](https://www.nuget.org/downloads), где реализуются требуемые [протоколы NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="21ad1-124">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="21ad1-125">Вам также потребуется ключ API, который создается на сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="21ad1-125">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="21ad1-126">Создание ключей API</span><span class="sxs-lookup"><span data-stu-id="21ad1-126">Create API keys</span></span>

[!INCLUDE[publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="21ad1-127">Публикация с помощью команды dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="21ad1-127">Publish with dotnet nuget push</span></span>

[!INCLUDE[publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="21ad1-128">Публикация с помощью команды nuget push</span><span class="sxs-lookup"><span data-stu-id="21ad1-128">Publish with nuget push</span></span>

1. <span data-ttu-id="21ad1-129">В окне командной строки выполните следующую команду, заменив `<your_API_key>` ключом, полученным на сайте nuget.org:</span><span class="sxs-lookup"><span data-stu-id="21ad1-129">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="21ad1-130">Эта команда сохраняет ключ API в конфигурации NuGet. Это действие нужно повторить еще раз на том же компьютере.</span><span class="sxs-lookup"><span data-stu-id="21ad1-130">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="21ad1-131">Выполните принудительную отправку в коллекцию NuGet с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="21ad1-131">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

### <a name="package-validation-and-indexing"></a><span data-ttu-id="21ad1-132">Проверка и индексирование пакета</span><span class="sxs-lookup"><span data-stu-id="21ad1-132">Package validation and indexing</span></span>

<span data-ttu-id="21ad1-133">Пакеты, передаваемые на веб-сайт nuget.org, проходят несколько проверок, например проверку на вирусы.</span><span class="sxs-lookup"><span data-stu-id="21ad1-133">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="21ad1-134">(Все пакеты на сайте nuget.org периодически сканируются.)</span><span class="sxs-lookup"><span data-stu-id="21ad1-134">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="21ad1-135">.</span><span class="sxs-lookup"><span data-stu-id="21ad1-135">.</span></span> <span data-ttu-id="21ad1-136">После того как пакет пройдет все проверки, он будет индексирован и появится в результатах поиска спустя некоторое время.</span><span class="sxs-lookup"><span data-stu-id="21ad1-136">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="21ad1-137">По завершении индексирования вы получите по электронной почте подтверждение о том, что пакет был успешно опубликован.</span><span class="sxs-lookup"><span data-stu-id="21ad1-137">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="21ad1-138">Если пакет не проходит проверку, на странице сведений о пакете отображается соответствующее уведомление об ошибке и вы также получите сообщение электронной почты с уведомлением.</span><span class="sxs-lookup"><span data-stu-id="21ad1-138">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="21ad1-139">Проверка и индексирование пакета обычно занимает около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="21ad1-139">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="21ad1-140">Если публикация пакета занимает больше времени, перейдите на веб-сайт [status.nuget.org](https://status.nuget.org/) и убедитесь, что портал nuget.org работает.</span><span class="sxs-lookup"><span data-stu-id="21ad1-140">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="21ad1-141">Если все системы исправны, но пакет не был опубликован в течение часа, войдите на веб-сайт nuget.org и свяжитесь с нами по ссылке "Связаться со службой поддержки" на странице пакета.</span><span class="sxs-lookup"><span data-stu-id="21ad1-141">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="21ad1-142">Чтобы просмотреть состояние пакета, на сайте nuget.org под именем учетной записи выберите **Manage packages** (Управление пакетами). После завершения проверки появится сообщение с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="21ad1-142">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="21ad1-143">Обратите внимание, что пакет индексируется и будет появляться в результатах поиска для других пользователей спустя определенное время. В этот период на странице вашего пакета будет отображаться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="21ad1-143">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Сообщение о том, что пакет не опубликовано](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="21ad1-145">Visual Studio Team Services (непрерывная интеграция и развертывание)</span><span class="sxs-lookup"><span data-stu-id="21ad1-145">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="21ad1-146">Если вы отправляете пакеты на веб-сайт nuget.org с использованием Visual Studio Team Services в рамках процесса непрерывной интеграции и развертывания, необходимо использовать `nuget.exe` 4.1 или более поздней версии в задачах NuGet.</span><span class="sxs-lookup"><span data-stu-id="21ad1-146">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="21ad1-147">Дополнительные сведения см. в разделе [Использование последней версии NuGet в сборках](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (блог Microsoft DevOps).</span><span class="sxs-lookup"><span data-stu-id="21ad1-147">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="21ad1-148">Управление владельцами пакетов на веб-сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="21ad1-148">Managing package owners on nuget.org</span></span>

<span data-ttu-id="21ad1-149">Несмотря на то, что в файле `.nuspec` каждого пакета NuGet определены авторы пакета, в коллекции nuget.org эти метаданные не используются для определения владельцев.</span><span class="sxs-lookup"><span data-stu-id="21ad1-149">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="21ad1-150">Вместо этого веб-сайт nuget.org назначает первичные права владения пользователю, который публикует пакет.</span><span class="sxs-lookup"><span data-stu-id="21ad1-150">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="21ad1-151">Это может быть выполнивший вход в систему пользователь, который отправил пакет через пользовательский интерфейс nuget.org, или пользователь, чей ключ API использовался в команде `nuget SetApiKey` или `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="21ad1-151">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="21ad1-152">Все владельцы пакета имеют полные разрешения на него, в том числе на добавление и удаление других владельцев, а также на публикацию обновлений.</span><span class="sxs-lookup"><span data-stu-id="21ad1-152">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="21ad1-153">Чтобы изменить владельца пакета, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="21ad1-153">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="21ad1-154">Войдите на веб-сайт nuget.org, используя учетную запись текущего владельца пакета.</span><span class="sxs-lookup"><span data-stu-id="21ad1-154">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="21ad1-155">Выберите имя учетной записи, щелкните **Manage packages** (Управление пакетами) и разверните узел **Published Packages** (Опубликованные пакеты).</span><span class="sxs-lookup"><span data-stu-id="21ad1-155">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="21ad1-156">Выберите пакет, которым требуется управлять, а затем в правой части выберите **Manage owners** (Управление владельцами).</span><span class="sxs-lookup"><span data-stu-id="21ad1-156">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="21ad1-157">В этом разделе можно выполнить разные действия:</span><span class="sxs-lookup"><span data-stu-id="21ad1-157">From here you have several options:</span></span>

1. <span data-ttu-id="21ad1-158">Удалите любого владельца из раздела **Current Owners** (Текущие владельцы).</span><span class="sxs-lookup"><span data-stu-id="21ad1-158">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="21ad1-159">Добавьте владельца в разделе **Add Owner** (Добавление владельца). Для этого введите имя пользователя, сообщение и нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="21ad1-159">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="21ad1-160">После этого новому совладельцу будет отправлено сообщение электронной почты со ссылкой для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="21ad1-160">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="21ad1-161">После подтверждения этот пользователь получит полные права доступа для добавления и удаления владельцев.</span><span class="sxs-lookup"><span data-stu-id="21ad1-161">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="21ad1-162">(До подтверждения в разделе **Current Owners** (Текущие владельцы) для этого пользователя будет отображаться уведомление об ожидании утверждения.)</span><span class="sxs-lookup"><span data-stu-id="21ad1-162">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="21ad1-163">Чтобы передать права владельца (например, в случае смены владельца или публикации с использованием неверной учетной записи), добавьте нового владельца и после получения подтверждения от него попросите удалить вашего пользователя из списка.</span><span class="sxs-lookup"><span data-stu-id="21ad1-163">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="21ad1-164">Чтобы назначить права владения компании или группе, создайте учетную запись на веб-сайте nuget.org с использованием псевдонима электронной почты, который пересылается соответствующим членам группы.</span><span class="sxs-lookup"><span data-stu-id="21ad1-164">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="21ad1-165">Например, многие пакеты ASP.NET корпорации Майкрософт находятся в совместном владении учетных записей [microsoft](http://nuget.org/profiles/microsoft) и [aspnet](http://nuget.org/profiles/aspnet), которые представляют собой подобные псевдонимы.</span><span class="sxs-lookup"><span data-stu-id="21ad1-165">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="21ad1-166">Восстановление прав владения пакетом</span><span class="sxs-lookup"><span data-stu-id="21ad1-166">Recovering package ownership</span></span>

<span data-ttu-id="21ad1-167">В некоторых случаях у пакета может отсутствовать активный владелец.</span><span class="sxs-lookup"><span data-stu-id="21ad1-167">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="21ad1-168">Например, исходный владелец может покинуть компанию, которая создает пакет, могут быть утрачены учетные данные nuget.org или из-за предыдущих ошибок в коллекции пакет может остаться без владельца.</span><span class="sxs-lookup"><span data-stu-id="21ad1-168">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="21ad1-169">Если вы являетесь полноправным владельцем пакета и хотите восстановить права владения, воспользуйтесь [формой для связи](https://www.nuget.org/policies/Contact) на веб-сайте nuget.org и опишите вашу ситуацию сотруднику NuGet.</span><span class="sxs-lookup"><span data-stu-id="21ad1-169">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="21ad1-170">После этого мы проверим ваши права владения пакетом, в том числе попытаемся найти существующего владельца по URL-адресу проекта пакета, через Twitter по электронной почте или другими способами.</span><span class="sxs-lookup"><span data-stu-id="21ad1-170">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="21ad1-171">Если эти способы не помогут, мы пришлем вам новое приглашение стать владельцем.</span><span class="sxs-lookup"><span data-stu-id="21ad1-171">But if all else fails, we can send you a new invite to become an owner.</span></span>
