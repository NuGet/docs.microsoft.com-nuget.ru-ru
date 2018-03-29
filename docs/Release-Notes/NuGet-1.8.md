---
title: Заметки о выпуске NuGet 1.8 | Документы Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Заметки о выпуске для NuGet 1.8, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
keywords: NuGet 1.8 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b94382f79143cac6bd5deccb5e5253ba8c6f60ec
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="a7dd6-104">Заметки о выпуске 1,8 NuGet</span><span class="sxs-lookup"><span data-stu-id="a7dd6-104">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="a7dd6-105">[Заметки о выпуске NuGet 1.7](../release-notes/nuget-1.7.md) | [заметки о выпуске NuGet 2.0](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="a7dd6-105">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="a7dd6-106">NuGet 1.8 был выпущен 23 мая 2012 г.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-106">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="a7dd6-107">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="a7dd6-107">Known Installation Issue</span></span>
<span data-ttu-id="a7dd6-108">Если вы используете VS 2010 с пакетом обновления 1, вы можете столкнуться ошибка установки при попытке обновить NuGet, если у вас установлена более ранняя версия.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="a7dd6-109">Достаточно просто удалить NuGet, а затем установить его из библиотеки расширения VS.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="a7dd6-110">В разделе [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Дополнительные сведения или [перейдите непосредственно на исправление VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="a7dd6-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="a7dd6-111">Примечание: Если Visual Studio не позволяют удалить расширение (кнопка удаления отключена), скорее всего, необходимо перезапустить Visual Studio, используя «Запуск от имени администратора».</span><span class="sxs-lookup"><span data-stu-id="a7dd6-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="a7dd6-112">NuGet 1.8 несовместим с Windows XP, опубликованные исправления</span><span class="sxs-lookup"><span data-stu-id="a7dd6-112">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="a7dd6-113">Вскоре после выпуска NuGet 1.8, мы узнали, что изменение шифрования в 1.8 было передано пользователей в Windows XP.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-113">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="a7dd6-114">Поскольку корпорация Майкрософт выпустила исправление, устраняющее эту проблему.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-114">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="a7dd6-115">Обновляя NuGet через коллекцию расширения Visual Studio, появляется это исправление.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-115">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="a7dd6-116">Возможности</span><span class="sxs-lookup"><span data-stu-id="a7dd6-116">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="a7dd6-117">Вспомогательные пакеты для локализованных ресурсов</span><span class="sxs-lookup"><span data-stu-id="a7dd6-117">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="a7dd6-118">NuGet 1.8 теперь поддерживает возможность создания отдельных пакетов для локализованных ресурсов, схожие с возможностями вспомогательные сборки платформы .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-118">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="a7dd6-119">Вспомогательные пакет создается таким же образом, как пакет NuGet с добавлением нескольких соглашения:</span><span class="sxs-lookup"><span data-stu-id="a7dd6-119">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="a7dd6-120">Имя и идентификатор пакета вспомогательных следует включить суффикс, соответствующий одному из стандартных [языка и региональных параметров строки, используемые в .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span><span class="sxs-lookup"><span data-stu-id="a7dd6-120">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span></span>
* <span data-ttu-id="a7dd6-121">В его `.nuspec` файла, вспомогательные пакета необходимо определить элемент языка с такой же строки языка и региональных параметров, используемых в идентификатор</span><span class="sxs-lookup"><span data-stu-id="a7dd6-121">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="a7dd6-122">Вспомогательные пакета необходимо определить зависимости в его `.nuspec` файл, чтобы его основных компонентов пакета, который является просто пакет с тем же Идентификатором минус суффикс языка.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-122">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="a7dd6-123">Базовый пакет должен быть доступны в репозитории для успешной установки.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-123">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="a7dd6-124">Чтобы установить пакет с локализованными ресурсами, разработчик явным образом выбирает локализованного пакета из репозитория.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-124">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="a7dd6-125">В настоящее галереи NuGet не предоставляет никакого специальной обработки, чтобы вспомогательные пакеты.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-125">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![Диалоговое окно диспетчера пакетов с локализованные pacakges](./media/dlg-w-loc-packs.png)

<span data-ttu-id="a7dd6-127">Так как пакет вспомогательных перечислены зависимости для его базовый пакет, основные и вспомогательные пакеты переносятся в папке пакеты NuGet и установлены.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-127">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![Локализованные пакеты в папке пакеты](./media/fldr-loc-packs.png)

<span data-ttu-id="a7dd6-129">Кроме того во время установки пакета вспомогательных NuGet также распознает соглашение об именовании строку языка и региональных параметров и затем копирует сборку локализованный ресурс в правильный вложенную папку в базовый пакет, чтобы его можно извлечь в .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-129">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![Папка ядра пакета с папкой скопированный ресурс](./media/fldr-copied-loc.png)

<span data-ttu-id="a7dd6-131">Один существующую ошибку, необходимо отметить вспомогательные пакеты заключается в том, что NuGet не локализованные ресурсы для `bin` папки для проектов веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-131">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="a7dd6-132">Эта проблема будет исправлена в следующем выпуске NuGet.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-132">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="a7dd6-133">Полный пример, демонстрирующий, как создать и использовать вспомогательные пакеты, в разделе [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).</span><span class="sxs-lookup"><span data-stu-id="a7dd6-133">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="a7dd6-134">Согласие восстановления пакета</span><span class="sxs-lookup"><span data-stu-id="a7dd6-134">Package Restore Consent</span></span>
<span data-ttu-id="a7dd6-135">В NuGet 1.8 мы упорядочивается подготовительную работу для поддержки важное ограничение при восстановлении пакета для защиты конфиденциальности пользователей.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-135">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="a7dd6-136">Это ограничение требует, что разработчики проекты и решения, использующие восстановление пакета явное согласие на восстановлении пакета должна online для загрузки пакетов из источников настроенный пакет.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-136">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="a7dd6-137">Для предоставления этого согласия 2 способами.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-137">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="a7dd6-138">Первый можно найти в диалоговом пакета диспетчера конфигурации, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-138">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="a7dd6-139">Этот метод в основном предназначен для машин разработчика.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-139">This method is primarily intended for developer machines.</span></span>

![Диалоговое окно конфигурации диспетчера пакетов](./media/pr-consent-configdlg.png)

<span data-ttu-id="a7dd6-141">Второй метод — задать среду переменной «EnableNuGetPackageRestore» значение «true».</span><span class="sxs-lookup"><span data-stu-id="a7dd6-141">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="a7dd6-142">Этот метод предназначен для автоматической компьютерах, таких как серверы CI или сборки.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-142">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="a7dd6-143">Теперь как уже говорилось выше, мы только расположения основу для этой функции в NuGet 1.8.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-143">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="a7dd6-144">На практике это означает, пока мы добавили всю логику, чтобы включить этот компонент, его применения в настоящее время не в этой версии.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-144">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="a7dd6-145">Будет включена, однако в следующем выпуске NuGet, поэтому мы хотели бы сообщить вам о его как можно быстрее, чтобы соответствующим образом настроить сред и поэтому не изменится при ограничение согласия.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-145">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="a7dd6-146">Дополнительные сведения см. в разделе [в блоге группы](http://blog.nuget.org/20120518/package-restore-and-consent.html) эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-146">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="a7dd6-147">Повышение производительности NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="a7dd6-147">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="a7dd6-148">Изменяя команду установки, чтобы загрузить и установить пакеты в параллельном режиме, NuGet 1.8 переводит ускоряется к nuget.exe — и при восстановлении пакета расширения.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-148">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="a7dd6-149">Высокий уровень уровня тестирование показывает, что для установки 6-пакетов в проект улучшится, около 35% NuGet 1.8.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-149">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="a7dd6-150">При увеличении числа пакетов до 25 дает прирост производительности составляет около 60%.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-150">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a7dd6-151">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="a7dd6-151">Bug Fixes</span></span>
<span data-ttu-id="a7dd6-152">NuGet 1.8 включает довольно много исправлений ошибок с акцентом на консоли диспетчера пакетов и восстановление рабочего процесса пакета, особенно в отношении пакета восстановления согласия и интеграции, Windows 8 Express.</span><span class="sxs-lookup"><span data-stu-id="a7dd6-152">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="a7dd6-153">Полный список рабочих элементов исправления в NuGet 1.8 представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="a7dd6-153">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
