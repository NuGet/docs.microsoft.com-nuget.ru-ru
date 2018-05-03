---
title: NuGet 2.6.1 заметки о выпуске WebMatrix
description: Заметки о выпуске для NuGet 2.6.1 для WebMatrix, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3d767788d348553cbb5cb82c6f70aac1894628c3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="cbf08-103">NuGet 2.6.1 заметки о выпуске WebMatrix</span><span class="sxs-lookup"><span data-stu-id="cbf08-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="cbf08-104">[Заметки о выпуске NuGet 2.6](../release-notes/nuget-2.6.md) | [заметки о выпуске NuGet 2.7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="cbf08-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="cbf08-105">Команды NuGet выпущен обновленный расширение диспетчера пакетов NuGet для WebMatrix 26 марта 2014 г.</span><span class="sxs-lookup"><span data-stu-id="cbf08-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="cbf08-106">Это обновление можно установить из [галереи расширений WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cbf08-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="cbf08-107">Откройте WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="cbf08-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="cbf08-108">Щелкните значок расширения в ленты "Главная"</span><span class="sxs-lookup"><span data-stu-id="cbf08-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="cbf08-109">Выберите вкладку "обновления"</span><span class="sxs-lookup"><span data-stu-id="cbf08-109">Select the Updates tab</span></span>
1. <span data-ttu-id="cbf08-110">Щелкните, чтобы обновить диспетчер пакетов NuGet для 2.6.1</span><span class="sxs-lookup"><span data-stu-id="cbf08-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="cbf08-111">Закройте и перезапустите WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="cbf08-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="cbf08-112">Существенные изменения</span><span class="sxs-lookup"><span data-stu-id="cbf08-112">Notable Changes</span></span>

<span data-ttu-id="cbf08-113">Это расширение обновление устраняет двух крупнейших проблем пользователей столкнулись много пакетов NuGet в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="cbf08-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="cbf08-114">Первый — ошибки NuGet версии схемы, а второй — ошибки, вызывающие пустой библиотек DLL в `bin` папки.</span><span class="sxs-lookup"><span data-stu-id="cbf08-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="cbf08-115">Ошибка, связанная с версией схемы NuGet</span><span class="sxs-lookup"><span data-stu-id="cbf08-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="cbf08-116">Со времени выпуска WebMatrix 3, были введены новые функции в NuGet, требуется новая версия схемы для пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="cbf08-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="cbf08-117">При попытке управлять пакетами NuGet на веб-сайте, эти новые пакеты может привести к ошибкам, которые можно увидеть в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="cbf08-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Произошла ошибка.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="cbf08-121">Этот последний выпуск обеспечивает совместимость с последние пакеты NuGet, предотвращает возникновение этой ошибки.</span><span class="sxs-lookup"><span data-stu-id="cbf08-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="cbf08-122">Новые версии пакетов, включая Microsoft.AspNet.WebPages теперь могут устанавливаться в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="cbf08-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="cbf08-123">Некоторые из этих пакетов были с помощью NuGet функции например [преобразования XDT конфигурации](../release-notes/nuget-2.6.md#xdt), который не поддерживается в WebMatrix до этого момента.</span><span class="sxs-lookup"><span data-stu-id="cbf08-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="cbf08-124">Пустой библиотек DLL в папке bin</span><span class="sxs-lookup"><span data-stu-id="cbf08-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="cbf08-125">Некоторые пользователи сообщали о, установка NuGet упаковывает в WebMatrix, включают DLL-библиотеки, которые копируются ячейки, которая для отображения DLL-библиотеки в `bin` папке с файлами нулевым байтом.</span><span class="sxs-lookup"><span data-stu-id="cbf08-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="cbf08-126">Это нарушает логику приложения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="cbf08-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="cbf08-127">[Эта проблема](https://nuget.codeplex.com/workitem/4060) теперь исправлена.</span><span class="sxs-lookup"><span data-stu-id="cbf08-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="cbf08-128">Другие усовершенствования последних</span><span class="sxs-lookup"><span data-stu-id="cbf08-128">Other Recent Improvements</span></span>

<span data-ttu-id="cbf08-129">Диспетчер пакетов NuGet 2.8 на момент выпуска для Visual Studio, кроме того, выпущен диспетчер пакетов NuGet 2.5.0 для WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="cbf08-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="cbf08-130">При этом говорилось в [заметки о выпуске NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), мы не ссылаются на конкретный новые возможности, появившиеся обновления.</span><span class="sxs-lookup"><span data-stu-id="cbf08-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="cbf08-131">Обновить все</span><span class="sxs-lookup"><span data-stu-id="cbf08-131">Update All</span></span>

<span data-ttu-id="cbf08-132">Теперь можно обновить все пакеты веб-сайта за один шаг.</span><span class="sxs-lookup"><span data-stu-id="cbf08-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="cbf08-133">При открытии расширение NuGet в WebMatrix вы см. список всех пакетов в коллекции, они установлены и те, которые имеют доступные обновления.</span><span class="sxs-lookup"><span data-stu-id="cbf08-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="cbf08-134">Ранее каждый пакет будет необходимо обновить по отдельности, но теперь является полезным «Обновить все» кнопку, которая отображается на вкладке «обновления».</span><span class="sxs-lookup"><span data-stu-id="cbf08-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Нажмите кнопку Обновить все, чтобы обновить все пакеты с использованием доступных обновлений](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="cbf08-136">Перезапись существующих файлов</span><span class="sxs-lookup"><span data-stu-id="cbf08-136">Overwrite Existing Files</span></span>

<span data-ttu-id="cbf08-137">При установке пакетов, содержащих файлы, которые уже существуют в веб-сайте, NuGet всегда просто игнорируется этих файлов (Если оставить существующие файлы отдельно).</span><span class="sxs-lookup"><span data-stu-id="cbf08-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="cbf08-138">Это может привести к впечатление, что пакет был установлен или неправильно обновлены, когда на самом деле это не было.</span><span class="sxs-lookup"><span data-stu-id="cbf08-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="cbf08-139">NuGet теперь выдаст запрос на перезапись файлов.</span><span class="sxs-lookup"><span data-stu-id="cbf08-139">NuGet will now prompt for files to be overwritten.</span></span>

![Разрешение конфликтов файлов](./media/NuGet-2.8/webmatrix-overwrite-file.png)
