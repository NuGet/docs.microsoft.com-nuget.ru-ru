---
title: NuGet 2.6.1 для WebMatrix заметки
description: Заметки о выпуске для NuGet 2.6.1 для WebMatrix, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550321"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="369da-103">NuGet 2.6.1 для WebMatrix заметки</span><span class="sxs-lookup"><span data-stu-id="369da-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="369da-104">[Заметки о выпуске NuGet 2.6](../release-notes/nuget-2.6.md) | [заметки о выпуске NuGet 2.7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="369da-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="369da-105">Команда NuGet выпустила обновленную расширение диспетчера пакетов NuGet для WebMatrix 26 марта 2014 г.</span><span class="sxs-lookup"><span data-stu-id="369da-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="369da-106">Это обновление можно установить из [коллекции расширений WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) , выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="369da-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="369da-107">Откройте WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="369da-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="369da-108">Щелкните значок расширения в «Главная» ленты</span><span class="sxs-lookup"><span data-stu-id="369da-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="369da-109">Выберите вкладку "обновления"</span><span class="sxs-lookup"><span data-stu-id="369da-109">Select the Updates tab</span></span>
1. <span data-ttu-id="369da-110">Щелкните, чтобы обновить диспетчер пакетов NuGet для 2.6.1</span><span class="sxs-lookup"><span data-stu-id="369da-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="369da-111">Закройте и перезапустите WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="369da-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="369da-112">Существенные изменения</span><span class="sxs-lookup"><span data-stu-id="369da-112">Notable Changes</span></span>

<span data-ttu-id="369da-113">Это расширение обновления адреса двух крупнейших проблем пользователей испытывают много пакетов NuGet в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="369da-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="369da-114">Первая ошибка NuGet схемы версии и второй имела место ошибка, что приводит к пустой библиотеки DLL в `bin` папку.</span><span class="sxs-lookup"><span data-stu-id="369da-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="369da-115">Ошибка версии NuGet схемы</span><span class="sxs-lookup"><span data-stu-id="369da-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="369da-116">С момента выпуска WebMatrix 3, были введены новые функции в NuGet, который требуется новая версия схемы для пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="369da-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="369da-117">При попытке управлять пакетами NuGet в веб-сайт, эти новые пакеты может привести к ошибкам, которые вы видите в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="369da-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Произошла ошибка.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="369da-121">Этот последний выпуск обеспечивает совместимость с новейшие пакеты NuGet, предотвращая появление этой ошибки.</span><span class="sxs-lookup"><span data-stu-id="369da-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="369da-122">Теперь можно устанавливать новые версии пакетов, включая Microsoft.AspNet.WebPages в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="369da-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="369da-123">Некоторые из этих пакетов использовать возможности NuGet, такие как [преобразования XDT конфигурации](../release-notes/nuget-2.6.md#xdt), который не поддерживается в WebMatrix, до сих пор.</span><span class="sxs-lookup"><span data-stu-id="369da-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="369da-124">Пустой библиотеки DLL в папку bin</span><span class="sxs-lookup"><span data-stu-id="369da-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="369da-125">Некоторые пользователи сообщили, после установки NuGet упаковывает в WebMatrix, включают библиотеки DLL, которые копируются в контейнер, который show библиотеки DLL в `bin` папке с файлами (нулевой) байт.</span><span class="sxs-lookup"><span data-stu-id="369da-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="369da-126">Это приводит к сбою приложения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="369da-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="369da-127">[Эта проблема](https://nuget.codeplex.com/workitem/4060) теперь устранена.</span><span class="sxs-lookup"><span data-stu-id="369da-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="369da-128">Другие последние улучшения</span><span class="sxs-lookup"><span data-stu-id="369da-128">Other Recent Improvements</span></span>

<span data-ttu-id="369da-129">После выпуска диспетчера пакета NuGet 2.8 для Visual Studio, мы также выпустили диспетчер пакетов NuGet 2.5.0 для WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="369da-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="369da-130">Хотя об этом говорилось в [заметки о выпуске NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), мы не упомянул конкретный новые возможности обновления, представленные.</span><span class="sxs-lookup"><span data-stu-id="369da-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="369da-131">Обновить все</span><span class="sxs-lookup"><span data-stu-id="369da-131">Update All</span></span>

<span data-ttu-id="369da-132">Теперь вы можете обновить все пакеты веб сайта за один шаг.</span><span class="sxs-lookup"><span data-stu-id="369da-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="369da-133">При открытии расширения NuGet в WebMatrix, см. список всех пакетов в коллекции, они установлены, а те обновления, доступные.</span><span class="sxs-lookup"><span data-stu-id="369da-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="369da-134">Ранее каждый пакет пришлось бы обновлять по отдельности, но теперь есть полезные кнопку «Обновить все», которая отображается на вкладке "обновления".</span><span class="sxs-lookup"><span data-stu-id="369da-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Нажмите кнопку Обновить все, чтобы обновить все пакеты с использованием доступных обновлений](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="369da-136">Перезаписать существующие файлы</span><span class="sxs-lookup"><span data-stu-id="369da-136">Overwrite Existing Files</span></span>

<span data-ttu-id="369da-137">При установке пакетов, содержащих файлы, которые уже существуют в веб-сайт, NuGet всегда просто игнорируется эти файлы (оставляя существующие файлы отдельно).</span><span class="sxs-lookup"><span data-stu-id="369da-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="369da-138">Это может привести к впечатление, что пакет был установлен или неправильно обновлены, когда на самом деле это не было.</span><span class="sxs-lookup"><span data-stu-id="369da-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="369da-139">NuGet теперь выдаст запрос на перезапись файлов.</span><span class="sxs-lookup"><span data-stu-id="369da-139">NuGet will now prompt for files to be overwritten.</span></span>

![Разрешение конфликтов файлов](./media/NuGet-2.8/webmatrix-overwrite-file.png)
