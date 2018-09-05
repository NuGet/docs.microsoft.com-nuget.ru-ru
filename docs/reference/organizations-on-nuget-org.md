---
title: Организации на сайте nuget.org
description: Организации на сайте nuget.org помогает управлять пакеты, опубликованные по группе или в группе, среде компании.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551232"
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="a3344-103">Организации на сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="a3344-103">Organization on nuget.org</span></span>

<span data-ttu-id="a3344-104">Организации предоставить предприятиям и проектов с открытым кодом для совместной работы над пакетов с помощью удостоверения единый nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a3344-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="a3344-105">Для потребителя пакета учетная запись организации отображается то же, что учетная запись пользователя на сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a3344-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="a3344-106">Учетные записи пользователей и учетных записей организации</span><span class="sxs-lookup"><span data-stu-id="a3344-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="a3344-107">Учетная запись пользователя является личности на сайте nuget.org и может быть элементом любого количества организаций.</span><span class="sxs-lookup"><span data-stu-id="a3344-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="a3344-108">Пакет может принадлежать к учетной записи организации, как он может принадлежать к учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="a3344-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="a3344-109">Потребители не видят разницы между учетная запись пользователя или учетной записью организации: одновременно появляться в виде пакета `owners`.</span><span class="sxs-lookup"><span data-stu-id="a3344-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="a3344-110">Учетная запись организации имеет один или несколько учетных записей пользователей их членами.</span><span class="sxs-lookup"><span data-stu-id="a3344-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="a3344-111">Эти члены могут управлять набор пакетов, сохраняя одно удостоверение для владельца.</span><span class="sxs-lookup"><span data-stu-id="a3344-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="a3344-112">Добавление новой организации</span><span class="sxs-lookup"><span data-stu-id="a3344-112">Adding a new organization</span></span>

<span data-ttu-id="a3344-113">Чтобы добавить новую организацию, выберите свою учетную запись на сайте nuget.org, а затем выберите **управление организации...**  команды меню:</span><span class="sxs-lookup"><span data-stu-id="a3344-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Пункт меню на сайте nuget.org для организаций Manager](media/org-manage-option.png)

<span data-ttu-id="a3344-115">На следующей странице выберите **добавить новую организацию** кнопки:</span><span class="sxs-lookup"><span data-stu-id="a3344-115">On the next page, select the **Add new organization** button:</span></span>

![Кнопку, чтобы создать новую организацию на сайте nuget.org](media/org-add-new-option.png)

<span data-ttu-id="a3344-117">На следующей странице Укажите организации имя и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="a3344-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="a3344-118">Так как учетные записи организации совместно используют то же пространство имен, как учетные записи пользователей, название организации должны быть разными, от любого другого существующей организации или учетные записи пользователей.</span><span class="sxs-lookup"><span data-stu-id="a3344-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="a3344-119">Адрес электронной почты также должно быть уникальным среди всех учетных записей.</span><span class="sxs-lookup"><span data-stu-id="a3344-119">The email address must also be unique across all accounts.</span></span>

![Добавить новую страницу организации на сайте nuget.org](media/org-add-new-page.png)

<span data-ttu-id="a3344-121">После создания учетной записи организации вы являетесь администратором и могут отправлять пакеты для организации и добавление членов организации.</span><span class="sxs-lookup"><span data-stu-id="a3344-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="a3344-122">Преобразование существующей учетной записи в организации</span><span class="sxs-lookup"><span data-stu-id="a3344-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="a3344-123">Преобразование учетной записи является необратимым: не удалось преобразовать обратно в учетную запись пользователя организации.</span><span class="sxs-lookup"><span data-stu-id="a3344-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="a3344-124">Если вы управляете пакеты в команде с помощью одной учетной записи и хотите преобразовать эту учетную запись в организации, используйте **преобразование вашей учетной записи для организации** параметр **организациям управлять** страницы:</span><span class="sxs-lookup"><span data-stu-id="a3344-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Параметр на сайте nuget.org, чтобы преобразовать существующую учетную запись в организации](media/org-transform-option.png)

<span data-ttu-id="a3344-126">На следующей странице укажите другую учетную запись пользователя назначить в качестве администратора организации, а затем выберите **преобразование**.</span><span class="sxs-lookup"><span data-stu-id="a3344-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Ввести данные для преобразования учетной записи пользователя в организации](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="a3344-128">Управление сотрудникам организации</span><span class="sxs-lookup"><span data-stu-id="a3344-128">Managing organization members</span></span>

<span data-ttu-id="a3344-129">Администратор организации, можно добавить элементы, предоставляя каждый член nuget.org *имя учетной записи пользователя*; нельзя использовать адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="a3344-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="a3344-130">Пометьте каждый член как участник или администратор со следующими разрешениями:</span><span class="sxs-lookup"><span data-stu-id="a3344-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="a3344-131">Разрешение</span><span class="sxs-lookup"><span data-stu-id="a3344-131">Permission</span></span> | <span data-ttu-id="a3344-132">Участник совместной работы</span><span class="sxs-lookup"><span data-stu-id="a3344-132">Collaborator</span></span> | <span data-ttu-id="a3344-133">Администратор</span><span class="sxs-lookup"><span data-stu-id="a3344-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3344-134">Управление пакетами организации</span><span class="sxs-lookup"><span data-stu-id="a3344-134">Manage the organization's packages</span></span><br/><span data-ttu-id="a3344-135">(Отправка новых пакетов, обновить или удалить из списка существующих пакетов)</span><span class="sxs-lookup"><span data-stu-id="a3344-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="a3344-136">Да</span><span class="sxs-lookup"><span data-stu-id="a3344-136">Yes</span></span> | <span data-ttu-id="a3344-137">Да</span><span class="sxs-lookup"><span data-stu-id="a3344-137">Yes</span></span> |
| <span data-ttu-id="a3344-138">Изменение организации метаданных</span><span class="sxs-lookup"><span data-stu-id="a3344-138">Change organization metadata</span></span><br/><span data-ttu-id="a3344-139">(адрес электронной почты, параметры уведомлений)</span><span class="sxs-lookup"><span data-stu-id="a3344-139">(email address, notification settings)</span></span> | <span data-ttu-id="a3344-140">Нет</span><span class="sxs-lookup"><span data-stu-id="a3344-140">No</span></span> | <span data-ttu-id="a3344-141">Да</span><span class="sxs-lookup"><span data-stu-id="a3344-141">Yes</span></span> |
| <span data-ttu-id="a3344-142">Управление членами организации</span><span class="sxs-lookup"><span data-stu-id="a3344-142">Manage organization members</span></span> | <span data-ttu-id="a3344-143">Нет</span><span class="sxs-lookup"><span data-stu-id="a3344-143">No</span></span> | <span data-ttu-id="a3344-144">Да</span><span class="sxs-lookup"><span data-stu-id="a3344-144">Yes</span></span> |
| <span data-ttu-id="a3344-145">Запрос и реакции на запросы co-ownership для организации пакетов</span><span class="sxs-lookup"><span data-stu-id="a3344-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="a3344-146">Нет</span><span class="sxs-lookup"><span data-stu-id="a3344-146">No</span></span> | <span data-ttu-id="a3344-147">Да</span><span class="sxs-lookup"><span data-stu-id="a3344-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="a3344-148">Управление пакетами</span><span class="sxs-lookup"><span data-stu-id="a3344-148">Managing packages</span></span>

<span data-ttu-id="a3344-149">Вы можете просматривать все пакеты для вашей учетной записи и всех организаций, которые вы входите на [управление пакетами](https://www.nuget.org/account/Packages) страницы.</span><span class="sxs-lookup"><span data-stu-id="a3344-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="a3344-150">Чтобы просмотреть пакеты, относящиеся к вашей учетной записи или любой конкретной организации, используйте фильтр учетных записей в верхнем правом углу страницы.</span><span class="sxs-lookup"><span data-stu-id="a3344-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Управление пакетами с фильтром учетной записи](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="a3344-152">Передача пакетов в организации</span><span class="sxs-lookup"><span data-stu-id="a3344-152">Transferring packages to an organization</span></span>
<span data-ttu-id="a3344-153">Если вы хотите перенести некоторые пакеты с только что созданный организацией, это можно сделать, запрашивает учетную запись организации, чтобы осуществлять совместное владение пакета и затем удаление самого себя в качестве владельца.</span><span class="sxs-lookup"><span data-stu-id="a3344-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="a3344-154">Если вы являетесь администратором организации, это подтверждение не обязан принимать владельца.</span><span class="sxs-lookup"><span data-stu-id="a3344-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="a3344-155">Тем не менее если вы являетесь участника совместной работы, добавление организации в качестве владельца требует наличия администраторам принять.</span><span class="sxs-lookup"><span data-stu-id="a3344-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="a3344-156">Публикация пакетов</span><span class="sxs-lookup"><span data-stu-id="a3344-156">Publishing packages</span></span>

<span data-ttu-id="a3344-157">Публикация пакетов для организации, как и публикации пакетов в учетной записи пользователя: непосредственная передача пакета на сайте nuget.org или с помощью принудительной отправки пакета `nuget push` или `dotnet nuget push` команд интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="a3344-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="a3344-158">Загрузка пакета</span><span class="sxs-lookup"><span data-stu-id="a3344-158">Uploading packages</span></span>

<span data-ttu-id="a3344-159">Если вы напрямую отправить новый пакет на [nuget.org передачи](https://www.nuget.org/packages/manage/upload) странице назначается владелец пакета учетной записи пользователя или организации:</span><span class="sxs-lookup"><span data-stu-id="a3344-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Отправка пакета с помощью параметра учетной записи](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="a3344-161">С помощью ключей API</span><span class="sxs-lookup"><span data-stu-id="a3344-161">Using API keys</span></span>

<span data-ttu-id="a3344-162">Для отправки пакета `nuget push` или `dotnet nuget push` команд интерфейса командной строки, необходимо получить ключ API, необходимые для этих команд.</span><span class="sxs-lookup"><span data-stu-id="a3344-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="a3344-163">Дополнительные сведения см. в разделе [Публикация пакета](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="a3344-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="a3344-164">При создании нового ключа API, выберите соответствующую организацию в **владелец пакета** раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="a3344-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="a3344-165">Любой ключ API, создаваемых применима только к выбранным организации:</span><span class="sxs-lookup"><span data-stu-id="a3344-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Ключ API с помощью параметра учетной записи](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="a3344-167">Удаление организации</span><span class="sxs-lookup"><span data-stu-id="a3344-167">Removing an organization</span></span>

<span data-ttu-id="a3344-168">Как пользователю, можно удалить себя из организации, выбрав `X` кнопку показано членство в вашей организации:</span><span class="sxs-lookup"><span data-stu-id="a3344-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Удаление учетной записи пользователя из организации](media/org-remove-self-option.png)

<span data-ttu-id="a3344-170">Администраторы могут удалять любой член из организации, включая других администраторов.</span><span class="sxs-lookup"><span data-stu-id="a3344-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="a3344-171">Если вы являетесь единственным администратором в организации, невозможно удалить себя так же, если не добавить другого члена с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a3344-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="a3344-172">Удаление учетной записи организации</span><span class="sxs-lookup"><span data-stu-id="a3344-172">Deleting an organization account</span></span>

<span data-ttu-id="a3344-173">Эта функция ожидается в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="a3344-173">This feature is coming soon.</span></span>
