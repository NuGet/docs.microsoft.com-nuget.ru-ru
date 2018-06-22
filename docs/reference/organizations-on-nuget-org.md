---
title: Организации на nuget.org
description: Организации на nuget.org помогает управлять пакетами, для публикации по группе или в команде среды организации.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449582"
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="ad788-103">Организации на nuget.org</span><span class="sxs-lookup"><span data-stu-id="ad788-103">Organization on nuget.org</span></span>

<span data-ttu-id="ad788-104">Организации предоставить предприятия и проектов с открытым кодом для совместной работы над пакетов с помощью удостоверения одной nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ad788-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="ad788-105">Для объекта-получателя пакета учетной записи организации отображается то же, что учетная запись пользователя на nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ad788-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="ad788-106">Учетные записи пользователей и учетные записи организации</span><span class="sxs-lookup"><span data-stu-id="ad788-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="ad788-107">Учетная запись пользователя является nuget.org учетных данных и может входить любое количество организаций.</span><span class="sxs-lookup"><span data-stu-id="ad788-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="ad788-108">Пакет может принадлежать к учетной записи организации, как он может принадлежать учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="ad788-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="ad788-109">Потребители пакетов не видят разницы между учетной записью пользователя или учетной записи организации: одновременно появляться в виде пакета `owners`.</span><span class="sxs-lookup"><span data-stu-id="ad788-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="ad788-110">Учетная запись организации имеет один или несколько учетных записей пользователей, что его члены.</span><span class="sxs-lookup"><span data-stu-id="ad788-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="ad788-111">Эти элементы можно управлять набор пакетов, сохраняя единое удостоверение для владения.</span><span class="sxs-lookup"><span data-stu-id="ad788-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="ad788-112">Добавление новой организации</span><span class="sxs-lookup"><span data-stu-id="ad788-112">Adding a new organization</span></span>

<span data-ttu-id="ad788-113">Чтобы добавить новую организацию, выберите свою учетную запись на nuget.org, а затем выберите **организациям управлять...**  команды меню:</span><span class="sxs-lookup"><span data-stu-id="ad788-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Параметр меню на nuget.org для диспетчера организаций](media/org-manage-option.png)

<span data-ttu-id="ad788-115">На следующей странице выберите **Добавление новой организации** кнопки:</span><span class="sxs-lookup"><span data-stu-id="ad788-115">On the next page, select the **Add new organization** button:</span></span>

![Чтобы создать новую организацию на nuget.org](media/org-add-new-option.png)

<span data-ttu-id="ad788-117">На следующей странице Укажите организации имя и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="ad788-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="ad788-118">Поскольку учетные записи организации имеют то же пространство имен, как учетные записи пользователей, название организации должен отличаться от любой существующей организации или учетные записи пользователей.</span><span class="sxs-lookup"><span data-stu-id="ad788-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="ad788-119">Адрес электронной почты также должен быть уникальным для всех учетных записей.</span><span class="sxs-lookup"><span data-stu-id="ad788-119">The email address must also be unique across all accounts.</span></span>

![Добавить новую страницу организации на nuget.org](media/org-add-new-page.png)

<span data-ttu-id="ad788-121">После создания учетной записи организации, Администраторы и можно отправить пакеты для организации и добавить члены организации.</span><span class="sxs-lookup"><span data-stu-id="ad788-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="ad788-122">Преобразование существующей учетной записи в организации</span><span class="sxs-lookup"><span data-stu-id="ad788-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="ad788-123">Учетная запись преобразования является необратимым: не удалось преобразовать обратно в учетную запись пользователя организации.</span><span class="sxs-lookup"><span data-stu-id="ad788-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="ad788-124">Если управляете пакеты в команде с помощью одной учетной записи пользователя и для преобразования этой учетной записи в организации, используйте **преобразования вашей учетной записи для каждой организации** параметр **организациям управлять** страницы:</span><span class="sxs-lookup"><span data-stu-id="ad788-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Параметр nuget.org для преобразования существующей учетной записи в организации](media/org-transform-option.png)

<span data-ttu-id="ad788-126">На следующей странице укажите другую учетную запись пользователя для назначения в качестве администратора организации, а затем выберите **преобразования**.</span><span class="sxs-lookup"><span data-stu-id="ad788-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Ввод данных для преобразования учетной записи пользователя в организации](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="ad788-128">Управление членами организации</span><span class="sxs-lookup"><span data-stu-id="ad788-128">Managing organization members</span></span>

<span data-ttu-id="ad788-129">Как администратор организации, можно добавлять участников, предоставляя каждого члена nuget.org *имя учетной записи пользователя*; нельзя использовать адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="ad788-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="ad788-130">Пометьте каждый член участника совместной работы или администратор со следующими разрешениями:</span><span class="sxs-lookup"><span data-stu-id="ad788-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="ad788-131">Разрешение</span><span class="sxs-lookup"><span data-stu-id="ad788-131">Permission</span></span> | <span data-ttu-id="ad788-132">Участника совместной работы</span><span class="sxs-lookup"><span data-stu-id="ad788-132">Collaborator</span></span> | <span data-ttu-id="ad788-133">Администратор</span><span class="sxs-lookup"><span data-stu-id="ad788-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad788-134">Управление пакетами организации</span><span class="sxs-lookup"><span data-stu-id="ad788-134">Manage the organization's packages</span></span><br/><span data-ttu-id="ad788-135">(отправить новые пакеты, обновления или исключить существующих пакетов)</span><span class="sxs-lookup"><span data-stu-id="ad788-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="ad788-136">Да</span><span class="sxs-lookup"><span data-stu-id="ad788-136">Yes</span></span> | <span data-ttu-id="ad788-137">Да</span><span class="sxs-lookup"><span data-stu-id="ad788-137">Yes</span></span> |
| <span data-ttu-id="ad788-138">Изменение метаданных организации</span><span class="sxs-lookup"><span data-stu-id="ad788-138">Change organization metadata</span></span><br/><span data-ttu-id="ad788-139">(адрес электронной почты, параметры уведомлений)</span><span class="sxs-lookup"><span data-stu-id="ad788-139">(email address, notification settings)</span></span> | <span data-ttu-id="ad788-140">Нет</span><span class="sxs-lookup"><span data-stu-id="ad788-140">No</span></span> | <span data-ttu-id="ad788-141">Да</span><span class="sxs-lookup"><span data-stu-id="ad788-141">Yes</span></span> |
| <span data-ttu-id="ad788-142">Управление членами организации</span><span class="sxs-lookup"><span data-stu-id="ad788-142">Manage organization members</span></span> | <span data-ttu-id="ad788-143">Нет</span><span class="sxs-lookup"><span data-stu-id="ad788-143">No</span></span> | <span data-ttu-id="ad788-144">Да</span><span class="sxs-lookup"><span data-stu-id="ad788-144">Yes</span></span> |
| <span data-ttu-id="ad788-145">Запрос или реагировать на запросы co-ownership для организации пакетов</span><span class="sxs-lookup"><span data-stu-id="ad788-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="ad788-146">Нет</span><span class="sxs-lookup"><span data-stu-id="ad788-146">No</span></span> | <span data-ttu-id="ad788-147">Да</span><span class="sxs-lookup"><span data-stu-id="ad788-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="ad788-148">Управление пакетами</span><span class="sxs-lookup"><span data-stu-id="ad788-148">Managing packages</span></span>

<span data-ttu-id="ad788-149">Можно просмотреть все пакеты в вашей учетной записи и все организации, которых вы являетесь участником на [управление пакетами](https://www.nuget.org/account/Packages) страницы.</span><span class="sxs-lookup"><span data-stu-id="ad788-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="ad788-150">Для просмотра пакетов, относящиеся к вашей учетной записи или любой конкретной организации, используйте фильтр учетные записи в верхнем правом углу страницы.</span><span class="sxs-lookup"><span data-stu-id="ad788-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Управление пакетами с фильтром учетной записи](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="ad788-152">Передача пакетов в организации</span><span class="sxs-lookup"><span data-stu-id="ad788-152">Transferring packages to an organization</span></span>
<span data-ttu-id="ad788-153">Если вы хотите перенести некоторые из своих пакетов к только что созданный организации, это можно сделать путем запроса учетная запись организации, чтобы осуществлять совместное владение пакета и затем удаление самого себя как владелец.</span><span class="sxs-lookup"><span data-stu-id="ad788-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="ad788-154">Если вы являетесь администратором организации, нет подтверждение не требуется принимать права владения.</span><span class="sxs-lookup"><span data-stu-id="ad788-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="ad788-155">Тем не менее если участника совместной работы, добавление организации в качестве владельца требует наличия администраторам принимать права владения.</span><span class="sxs-lookup"><span data-stu-id="ad788-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="ad788-156">Публикация пакетов</span><span class="sxs-lookup"><span data-stu-id="ad788-156">Publishing packages</span></span>

<span data-ttu-id="ad788-157">Публикация пакетов для каждой организации, как публикация пакетов с учетной записью пользователя: загрузка пакета nuget.org напрямую или с помощью принудительной отправки пакета `nuget push` или `dotnet nuget push` команды CLI.</span><span class="sxs-lookup"><span data-stu-id="ad788-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="ad788-158">Передача пакетов</span><span class="sxs-lookup"><span data-stu-id="ad788-158">Uploading packages</span></span>

<span data-ttu-id="ad788-159">Если вы непосредственно отправьте новый пакет на [nuget.org передачи](https://www.nuget.org/packages/manage/upload) страницы, назначаемые владелец пакета учетной записи пользователя или организации:</span><span class="sxs-lookup"><span data-stu-id="ad788-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Отправить пакет с помощью параметра учетной записи](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="ad788-161">Использование ключей API</span><span class="sxs-lookup"><span data-stu-id="ad788-161">Using API keys</span></span>

<span data-ttu-id="ad788-162">Для принудительной отправки пакета `nuget push` или `dotnet nuget push` команд CLI, необходимо получить ключ API, необходимые для этих команд.</span><span class="sxs-lookup"><span data-stu-id="ad788-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="ad788-163">Дополнительные сведения см. в разделе [Публикация пакета](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="ad788-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="ad788-164">При создании нового ключа API, выберите соответствующий организации в **владельца пакета** раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="ad788-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="ad788-165">Любой ключ API, создаваемых применима только к выбранным организации:</span><span class="sxs-lookup"><span data-stu-id="ad788-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Ключ API с учетной записью](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="ad788-167">Удаление организации</span><span class="sxs-lookup"><span data-stu-id="ad788-167">Removing an organization</span></span>

<span data-ttu-id="ad788-168">Как пользователь, можно удалить себя из организации, выбрав `X` кнопок, членство в вашей организации:</span><span class="sxs-lookup"><span data-stu-id="ad788-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Удаление учетной записи пользователя в организации](media/org-remove-self-option.png)

<span data-ttu-id="ad788-170">Администраторы могут удалять любой член из организации, включая других администраторов.</span><span class="sxs-lookup"><span data-stu-id="ad788-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="ad788-171">Если вы являетесь единственным администратором в организации, нельзя удалить себя, если не добавить члена с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ad788-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="ad788-172">Удаление учетной записи организации</span><span class="sxs-lookup"><span data-stu-id="ad788-172">Deleting an organization account</span></span>

<span data-ttu-id="ad788-173">Эта возможность скоро будет.</span><span class="sxs-lookup"><span data-stu-id="ad788-173">This feature is coming soon.</span></span>
