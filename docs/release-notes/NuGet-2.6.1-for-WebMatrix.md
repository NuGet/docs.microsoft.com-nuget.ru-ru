---
title: Заметки о выпуске NuGet 2.6.1 для WebMatrix
description: Заметки о выпуске NuGet 2.6.1 для WebMatrix, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780425"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="7b06e-103">Заметки о выпуске NuGet 2.6.1 для WebMatrix</span><span class="sxs-lookup"><span data-stu-id="7b06e-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="7b06e-104">[Заметки о](../release-notes/nuget-2.6.md)  |  выпуске NuGet 2,6 [Заметки о выпуске NuGet 2,7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="7b06e-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="7b06e-105">Группа NuGet выпустила обновленное расширение диспетчера пакетов NuGet для WebMatrix 26 марта 2014.</span><span class="sxs-lookup"><span data-stu-id="7b06e-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="7b06e-106">Это обновление можно установить из [коллекции расширений WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) , выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7b06e-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="7b06e-107">Открыть WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="7b06e-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="7b06e-108">Щелкните значок расширения на ленте Главная.</span><span class="sxs-lookup"><span data-stu-id="7b06e-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="7b06e-109">Выберите вкладку обновления.</span><span class="sxs-lookup"><span data-stu-id="7b06e-109">Select the Updates tab</span></span>
1. <span data-ttu-id="7b06e-110">Щелкните, чтобы обновить диспетчер пакетов NuGet до 2.6.1</span><span class="sxs-lookup"><span data-stu-id="7b06e-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="7b06e-111">Закрытие и перезапуск WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="7b06e-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="7b06e-112">Важные изменения</span><span class="sxs-lookup"><span data-stu-id="7b06e-112">Notable Changes</span></span>

<span data-ttu-id="7b06e-113">Это обновление расширения устраняет две из крупнейших проблем, с которыми сталкиваются пользователи при использовании пакетов NuGet в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7b06e-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="7b06e-114">Первая из них была ошибкой версии схемы NuGet, а вторая — ошибкой для DLL-библиотек с нулевым байтом в `bin` папке.</span><span class="sxs-lookup"><span data-stu-id="7b06e-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="7b06e-115">Ошибка версии схемы NuGet</span><span class="sxs-lookup"><span data-stu-id="7b06e-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="7b06e-116">После выпуска WebMatrix 3 в NuGet появились новые функции, для которых требуется новая версия схемы для пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="7b06e-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="7b06e-117">При попытке управления пакетами NuGet на веб-сайте эти новые пакеты могут привести к ошибкам, отображаемым в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7b06e-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Произошла ошибка.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="7b06e-121">Этот последний выпуск обеспечивает совместимость с новейшими пакетами NuGet, предотвращая возникновение этой ошибки.</span><span class="sxs-lookup"><span data-stu-id="7b06e-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="7b06e-122">Новые версии пакетов, включая Microsoft. AspNet. веб-страницы, теперь можно установить в WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7b06e-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="7b06e-123">Некоторые из этих пакетов использовали такие функции NuGet, как [преобразования конфигурации xdt](../release-notes/nuget-2.6.md#xdt), которые не поддерживались в WebMatrix до настоящего момента.</span><span class="sxs-lookup"><span data-stu-id="7b06e-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="7b06e-124">Zero-Byte библиотеки DLL в папке bin</span><span class="sxs-lookup"><span data-stu-id="7b06e-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="7b06e-125">Некоторые пользователи сообщили, что после установки пакетов NuGet в WebMatrix, включающих библиотеки DLL, скопированные в папку bin, библиотеки DLL отображаются в `bin` папке как 0-байтовые файлы.</span><span class="sxs-lookup"><span data-stu-id="7b06e-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="7b06e-126">Это прерывает работу приложения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="7b06e-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="7b06e-127">Теперь [Эта проблема](https://nuget.codeplex.com/workitem/4060) исправлена.</span><span class="sxs-lookup"><span data-stu-id="7b06e-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="7b06e-128">Другие последние улучшения</span><span class="sxs-lookup"><span data-stu-id="7b06e-128">Other Recent Improvements</span></span>

<span data-ttu-id="7b06e-129">Когда диспетчер пакетов NuGet 2,8 был выпущен для Visual Studio, мы также выпустили диспетчер пакетов NuGet 2.5.0 для WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7b06e-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="7b06e-130">Хотя это было сказано в [заметках о выпуске NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), мы не говорили о новых возможностях, которые появились в обновлении.</span><span class="sxs-lookup"><span data-stu-id="7b06e-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="7b06e-131">Обновить все</span><span class="sxs-lookup"><span data-stu-id="7b06e-131">Update All</span></span>

<span data-ttu-id="7b06e-132">Теперь вы можете обновить все пакеты веб-сайта за один шаг!</span><span class="sxs-lookup"><span data-stu-id="7b06e-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="7b06e-133">При открытии расширения NuGet в WebMatrix отображается список всех пакетов в коллекции, установленных, а также доступные обновления.</span><span class="sxs-lookup"><span data-stu-id="7b06e-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="7b06e-134">Ранее каждый пакет должен быть обновлен по отдельности, но теперь есть полезная кнопка "обновить все", которая отображается на вкладке "обновления".</span><span class="sxs-lookup"><span data-stu-id="7b06e-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Щелкните Обновить все, чтобы обновить все пакеты с доступными обновлениями](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="7b06e-136">Перезаписать существующие файлы</span><span class="sxs-lookup"><span data-stu-id="7b06e-136">Overwrite Existing Files</span></span>

<span data-ttu-id="7b06e-137">При установке пакетов, содержащих файлы, которые уже существуют на веб-сайте, NuGet всегда проигнорировал эти файлы без вмешательства пользователя (при этом только существующие файлы).</span><span class="sxs-lookup"><span data-stu-id="7b06e-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="7b06e-138">Это может привести к тому, что пакет был установлен или правильно обновлен, если на самом деле он был недоступен.</span><span class="sxs-lookup"><span data-stu-id="7b06e-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="7b06e-139">NuGet теперь будет запрашивать перезапись файлов.</span><span class="sxs-lookup"><span data-stu-id="7b06e-139">NuGet will now prompt for files to be overwritten.</span></span>

![Разрешение конфликтов файлов](./media/NuGet-2.8/webmatrix-overwrite-file.png)
