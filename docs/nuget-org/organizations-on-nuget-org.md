---
title: Ваша организация на сайте NuGet.org
description: С помощью организаций на сайте NuGet.org вы можете управлять пакетами, публикуемыми группой или командой в среде компании.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427079"
---
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="f9dc3-103">Ваша организация на сайте NuGet.org</span><span class="sxs-lookup"><span data-stu-id="f9dc3-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="f9dc3-104">Благодаря организациям компании и проекты с открытым исходным кодом могут совместно работать с пакетами, используя одно удостоверение на сайте NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="f9dc3-105">Потребитель пакета видит учетную запись организации так же, как и существующую пользовательскую учетную запись на сайте NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="f9dc3-106">Сравнение учетных записей организаций и индивидуальных учетных записей</span><span class="sxs-lookup"><span data-stu-id="f9dc3-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="f9dc3-107">В учетную запись организации могут входить в качестве членов одна или несколько индивидуальных (пользовательских) учетных записей.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="f9dc3-108">Эти члены могут управлять набором пакетов, используя для этого единое удостоверение владельца.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="f9dc3-109">Ваша индивидуальная учетная запись является вашим удостоверением на сайте NuGet.org и может являться членом любой организации.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="f9dc3-110">Пакет может принадлежать учетной записи организации так же, как и индивидуальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="f9dc3-111">Для потребителей пакета нет никаких различий между индивидуальной учетной записью и учетной записью организации. Обе они отображаются как объекты `owners` для пакета.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="f9dc3-112">Добавление новой организации</span><span class="sxs-lookup"><span data-stu-id="f9dc3-112">Adding a new organization</span></span>

<span data-ttu-id="f9dc3-113">Чтобы добавить организацию, выберите свою учетную запись на сайте NuGet.org, после чего щелкните команду **Управление организациями** в меню:</span><span class="sxs-lookup"><span data-stu-id="f9dc3-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![Команда меню для управления организациями на сайте NuGet.org](media/org-manage-option.png)

<span data-ttu-id="f9dc3-115">На следующей странице нажмите кнопку **Добавить новую организацию**.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-115">On the next page, select the **Add new organization** button:</span></span>

![Кнопка для создания новой организации на сайте NuGet.org](media/org-add-new-option.png)

<span data-ttu-id="f9dc3-117">На следующей странице укажите название и адрес электронной почты организации.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="f9dc3-118">Поскольку учетные записи организаций и пользователей находятся в одном пространстве имен, название организации не может совпадать с названиями других организаций и именами пользователей.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="f9dc3-119">Адрес электронной почты также должен быть уникальным на уровне всех учетных записей.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-119">The email address must also be unique across all accounts.</span></span>

![Страница добавления организации на сайте NuGet.org](media/org-add-new-page.png)

<span data-ttu-id="f9dc3-121">После создания учетной записи организации вы получаете права ее администратора и можете отправлять пакеты от имени организации, а также добавлять в нее членов.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="f9dc3-122">Преобразование существующей учетной записи в организацию</span><span class="sxs-lookup"><span data-stu-id="f9dc3-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="f9dc3-123">Преобразование учетной записи является необратимой операцией. Это значит, что вернуть учетную запись организации на уровень пользовательской не получится.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="f9dc3-124">Если вы управляете пакетами в составе команды с использованием одной учетной записи пользователя и хотите преобразовать ее в учетную запись организации, используйте параметр **Преобразовать учетную запись в организацию** на странице **Управление организациями**:</span><span class="sxs-lookup"><span data-stu-id="f9dc3-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Параметр сайта NuGet.org, позволяющий преобразовать существующую учетную запись в учетную запись организации](media/org-transform-option.png)

<span data-ttu-id="f9dc3-126">На следующей странице укажите другую учетную запись пользователя, который будет назначен администратором организации, после чего щелкните **Преобразовать**.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Ввод информации для преобразования учетной записи пользователя в организацию](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="f9dc3-128">Управление членами организации</span><span class="sxs-lookup"><span data-stu-id="f9dc3-128">Managing organization members</span></span>

<span data-ttu-id="f9dc3-129">Администратор организации может добавлять членов, указывая *учетные записи пользователей* на сайте NuGet.org. Адреса электронной почты для этой цели использовать нельзя.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="f9dc3-130">Далее каждому члену назначаются права участника совместной работы или администратора со следующими разрешениями:</span><span class="sxs-lookup"><span data-stu-id="f9dc3-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="f9dc3-131">Разрешение</span><span class="sxs-lookup"><span data-stu-id="f9dc3-131">Permission</span></span> | <span data-ttu-id="f9dc3-132">Участник совместной работы</span><span class="sxs-lookup"><span data-stu-id="f9dc3-132">Collaborator</span></span> | <span data-ttu-id="f9dc3-133">Администратор</span><span class="sxs-lookup"><span data-stu-id="f9dc3-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9dc3-134">Управление пакетами организации</span><span class="sxs-lookup"><span data-stu-id="f9dc3-134">Manage the organization's packages</span></span><br/><span data-ttu-id="f9dc3-135">(отправка новых пакетов, а также обновление или удаление из списка существующих пакетов)</span><span class="sxs-lookup"><span data-stu-id="f9dc3-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="f9dc3-136">Yes</span><span class="sxs-lookup"><span data-stu-id="f9dc3-136">Yes</span></span> | <span data-ttu-id="f9dc3-137">Yes</span><span class="sxs-lookup"><span data-stu-id="f9dc3-137">Yes</span></span> |
| <span data-ttu-id="f9dc3-138">Изменение метаданных организации</span><span class="sxs-lookup"><span data-stu-id="f9dc3-138">Change organization metadata</span></span><br/><span data-ttu-id="f9dc3-139">(адрес электронной почты, параметры уведомлений)</span><span class="sxs-lookup"><span data-stu-id="f9dc3-139">(email address, notification settings)</span></span> | <span data-ttu-id="f9dc3-140">Нет </span><span class="sxs-lookup"><span data-stu-id="f9dc3-140">No</span></span> | <span data-ttu-id="f9dc3-141">Yes</span><span class="sxs-lookup"><span data-stu-id="f9dc3-141">Yes</span></span> |
| <span data-ttu-id="f9dc3-142">Управление членами организации</span><span class="sxs-lookup"><span data-stu-id="f9dc3-142">Manage organization members</span></span> | <span data-ttu-id="f9dc3-143">Нет </span><span class="sxs-lookup"><span data-stu-id="f9dc3-143">No</span></span> | <span data-ttu-id="f9dc3-144">Yes</span><span class="sxs-lookup"><span data-stu-id="f9dc3-144">Yes</span></span> |
| <span data-ttu-id="f9dc3-145">Отправка запросов или выполнение действий в ответ на запросы на совместное владение в отношении пакетов организации</span><span class="sxs-lookup"><span data-stu-id="f9dc3-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="f9dc3-146">Нет </span><span class="sxs-lookup"><span data-stu-id="f9dc3-146">No</span></span> | <span data-ttu-id="f9dc3-147">Yes</span><span class="sxs-lookup"><span data-stu-id="f9dc3-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="f9dc3-148">Управление пакетами</span><span class="sxs-lookup"><span data-stu-id="f9dc3-148">Managing packages</span></span>

<span data-ttu-id="f9dc3-149">На странице [Управление пакетами](https://www.nuget.org/account/Packages) вы можете просмотреть все пакеты своей учетной записи и всех организаций, членом которых вы являетесь.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="f9dc3-150">Чтобы просмотреть пакеты, относящиеся к вашей учетной записи или любой конкретной организации, используйте фильтр учетных записей, расположенный в верхнем правом углу страницы.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Управление пакетами с использованием фильтра учетных записей](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="f9dc3-152">Перенос пакетов в организацию</span><span class="sxs-lookup"><span data-stu-id="f9dc3-152">Transferring packages to an organization</span></span>
<span data-ttu-id="f9dc3-153">Чтобы перенести некоторые пакеты в созданную организацию, направьте в учетную запись организации запрос на совместное владение пакетами и затем отзовите право владения у своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="f9dc3-154">Если вы являетесь администратором организации, подтверждать получение права владения не требуется.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="f9dc3-155">Тем не менее, если вы являетесь участником совместной работы и добавляете организацию в качестве владельца, один из администраторов должен принять право владения.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="f9dc3-156">Публикация пакетов</span><span class="sxs-lookup"><span data-stu-id="f9dc3-156">Publishing packages</span></span>

<span data-ttu-id="f9dc3-157">Публикация пакетов в учетной записи организации осуществляется так же, как и для учетной записи пользователя. Для этого достаточно загрузить пакет непосредственно на сайт NuGet.org или отправить его с помощью команд CLI `nuget push` или `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="f9dc3-158">Загрузка пакетов</span><span class="sxs-lookup"><span data-stu-id="f9dc3-158">Uploading packages</span></span>

<span data-ttu-id="f9dc3-159">Если вы загружаете новый пакет непосредственно на страницу [Загрузка](https://www.nuget.org/packages/manage/upload) сайта NuGet.org, необходимо присвоить право владения пакетом учетной записи пользователя или организации:</span><span class="sxs-lookup"><span data-stu-id="f9dc3-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Загрузка пакета с использованием параметра учетной записи](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="f9dc3-161">Использование ключей API</span><span class="sxs-lookup"><span data-stu-id="f9dc3-161">Using API keys</span></span>

<span data-ttu-id="f9dc3-162">Чтобы отправить пакет с помощью команды CLI `nuget push` или `dotnet nuget push`, необходимо получить используемый этими командами ключ API.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="f9dc3-163">Дополнительные сведения см. в статье [Публикация пакета](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="f9dc3-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="f9dc3-164">При создании нового ключа API выберите соответствующую организацию в раскрывающемся списке **Владелец пакета**.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="f9dc3-165">Любой создаваемый ключ API будет применяться только для выбранной организации.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Ключ API с параметром учетной записи](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="f9dc3-167">Удаление организации</span><span class="sxs-lookup"><span data-stu-id="f9dc3-167">Removing an organization</span></span>

<span data-ttu-id="f9dc3-168">Пользователь может удалить из организации свою учетную запись, нажав кнопку **X** в разделе членства в организации:</span><span class="sxs-lookup"><span data-stu-id="f9dc3-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![Удаление учетной записи пользователя из организации](media/org-remove-self-option.png)

<span data-ttu-id="f9dc3-170">Администратор может удалить любого члена организации, в том числе и другого администратора.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="f9dc3-171">Если вы являетесь единственным администратором организации, вы не сможете удалить свою учетную запись до тех пор, пока в качестве администратора не будет добавлен другой член.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="f9dc3-172">Удаление учетной записи организации</span><span class="sxs-lookup"><span data-stu-id="f9dc3-172">Deleting an organization account</span></span>

<span data-ttu-id="f9dc3-173">Чтобы удалить учетную запись организации, нажмите кнопку **Удалить** на странице организации.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![Удаление организации](media/org-delete-option.png)

<span data-ttu-id="f9dc3-175">Чтобы окончательно удалить организацию, подтвердите эту операцию с помощью кнопки **Удалить организацию**.</span><span class="sxs-lookup"><span data-stu-id="f9dc3-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
