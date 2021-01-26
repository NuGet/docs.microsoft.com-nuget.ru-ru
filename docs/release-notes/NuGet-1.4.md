---
title: Заметки о выпуске NuGet 1,4
description: Заметки о выпуске NuGet 1,4, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777142"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="76222-103">Заметки о выпуске NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="76222-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="76222-104">[Заметки о](../release-notes/nuget-1.3.md)  |  выпуске NuGet 1,3 [Заметки о выпуске NuGet 1,5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="76222-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="76222-105">NuGet 1,4 был выпущен 17 июня 2011 г.</span><span class="sxs-lookup"><span data-stu-id="76222-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="76222-106">Компоненты</span><span class="sxs-lookup"><span data-stu-id="76222-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="76222-107">Улучшения Update-Package</span><span class="sxs-lookup"><span data-stu-id="76222-107">Update-Package improvements</span></span>
<span data-ttu-id="76222-108">В NuGet 1,4 введено множество улучшений команды Update-Package, что упрощает обеспечение сохранения пакетов в одной версии в нескольких проектах в решении.</span><span class="sxs-lookup"><span data-stu-id="76222-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="76222-109">Например, при обновлении пакета до последней версии очень часто требуется, чтобы все проекты с установленным пакетом были обновлены до тех же верисион.</span><span class="sxs-lookup"><span data-stu-id="76222-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="76222-110">`Update-Package`Теперь команда упрощает следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="76222-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="76222-111">Обновление всех пакетов в одном проекте</span><span class="sxs-lookup"><span data-stu-id="76222-111">Update all packages in a single project</span></span>

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="76222-112">Обновление пакета во всех проектах</span><span class="sxs-lookup"><span data-stu-id="76222-112">Update a package in all projects</span></span>

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="76222-113">Обновить все пакеты во всех проектах</span><span class="sxs-lookup"><span data-stu-id="76222-113">Update all packages in all projects</span></span>

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="76222-114">Выполнение "безопасного" обновления для всех пакетов</span><span class="sxs-lookup"><span data-stu-id="76222-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="76222-115">`-Safe`Флаг ограничивает обновление только версиями с одним и тем же основным и вспомогательным компонентом версии.</span><span class="sxs-lookup"><span data-stu-id="76222-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="76222-116">Например, если установлена версия пакета 1.0.0, а в веб-канале доступны версии 1.0.1, 1.0.2 и 1,1, `-Safe` флаг обновляет пакет до версии 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="76222-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="76222-117">При обновлении без `-Safe` флага пакет будет обновлен до последней версии 1,1.</span><span class="sxs-lookup"><span data-stu-id="76222-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="76222-118">Управление пакетами на уровне решения</span><span class="sxs-lookup"><span data-stu-id="76222-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="76222-119">До NuGet 1,4 Установка пакета в несколько проектов была утомительной с помощью диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="76222-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="76222-120">Он требовал запуска диалогового окна один раз для каждого проекта.</span><span class="sxs-lookup"><span data-stu-id="76222-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="76222-121">NuGet 1,4 добавляет поддержку установки, удаления и обновления пакетов в нескольких проектах одновременно.</span><span class="sxs-lookup"><span data-stu-id="76222-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="76222-122">Просто запустите компонент, щелкнув правой кнопкой мыши решение и выбрав пункт **Управление пакетами NuGet** .</span><span class="sxs-lookup"><span data-stu-id="76222-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Диалоговое окно "Управление пакетами NuGet" на уровне решения](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="76222-124">Обратите внимание, что в заголовке диалогового окна отображается имя решения, а не имя проекта.</span><span class="sxs-lookup"><span data-stu-id="76222-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="76222-125">Операции с пакетами теперь предоставляют список флажков со списком проектов, к которым должна применяться операция.</span><span class="sxs-lookup"><span data-stu-id="76222-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Управление пакетами NuGet выбор проекта](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="76222-127">Дополнительные сведения см. в разделе об [управлении пакетами для решения](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="76222-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="76222-128">Ограничение обновлений до разрешенных версий</span><span class="sxs-lookup"><span data-stu-id="76222-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="76222-129">По умолчанию при выполнении `Update-Package` команды в пакете (или обновлении пакета с помощью диалогового окна) он будет обновлен до последней версии в веб-канале.</span><span class="sxs-lookup"><span data-stu-id="76222-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="76222-130">Благодаря новой поддержке обновления всех пакетов могут возникнуть ситуации, в которых необходимо заблокировать пакет для определенного диапазона версий.</span><span class="sxs-lookup"><span data-stu-id="76222-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="76222-131">Например, вы можете заранее понять, что приложение будет работать только с версией 2. \* пакета, но не 3,0 и выше.</span><span class="sxs-lookup"><span data-stu-id="76222-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="76222-132">Чтобы предотвратить случайное обновление пакета до 3, NuGet 1,4 добавляет поддержку ограничения диапазона версий, до которого можно обновить пакеты, вручную редактируя `packages.config` файл с помощью нового `allowedVersions` атрибута.</span><span class="sxs-lookup"><span data-stu-id="76222-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="76222-133">Например, в следующем примере показано, как заблокировать `SomePackage` пакет с диапазоном версий 2,0-3,0 (эксклюзивный).</span><span class="sxs-lookup"><span data-stu-id="76222-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="76222-134">`allowedVersions`Атрибут принимает значения, используя [Формат диапазона версий](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="76222-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="76222-135">Обратите внимание, что в 1,4 Блокировка пакета в определенном диапазоне версий должна быть вручную изменена.</span><span class="sxs-lookup"><span data-stu-id="76222-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="76222-136">В NuGet 1,5 мы планируем добавить поддержку для размещения этого диапазона с помощью `Install-Package` команды.</span><span class="sxs-lookup"><span data-stu-id="76222-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="76222-137">Визуализатор пакетов</span><span class="sxs-lookup"><span data-stu-id="76222-137">Package Visualizer</span></span>
<span data-ttu-id="76222-138">Новый Визуализатор пакетов, запущенный с помощью   ->  команды меню Визуализатор пакета **диспетчера пакетов библиотеки** инструментов  ->   , позволяет легко визуализировать все проекты и их зависимости пакетов в рамках решения.</span><span class="sxs-lookup"><span data-stu-id="76222-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="76222-139">_**Важное замечание.** Эта функция использует преимущества поддержки DGML в Visual Studio. Создание визуализации поддерживается только в Visual Studio Ultimate. Просмотр DGML-схемы поддерживается только в Visual Studio Premium и более поздних версиях._</span><span class="sxs-lookup"><span data-stu-id="76222-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Визуализатор пакетов](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="76222-141">Автоматическая проверка обновлений для диалогового окна NuGet</span><span class="sxs-lookup"><span data-stu-id="76222-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="76222-142">Некоторые версии NuGet представляют новые функции, представленные в `.nuspec` файле, которые не распознаются более старыми версиями диалогового окна NuGet.</span><span class="sxs-lookup"><span data-stu-id="76222-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="76222-143">Одним из примеров является введение в NuGet 1,4 для [указания сборок платформы](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="76222-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="76222-144">Поэтому важно использовать последнюю версию NuGet, чтобы вы могли использовать пакеты, используя преимущества новейших функций.</span><span class="sxs-lookup"><span data-stu-id="76222-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="76222-145">Чтобы сделать обновления для NuGet более видимыми, диалоговое окно NuGet содержит логику, которая выделит, когда доступна более новая версия.</span><span class="sxs-lookup"><span data-stu-id="76222-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="76222-146">_**Примечание**. Проверка выполняется только в том случае, если в текущем сеансе выбрана вкладка "в **сети** "._</span><span class="sxs-lookup"><span data-stu-id="76222-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Диалоговое окно управления пакетами NuGet с доступной новой версией](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="76222-148">Чтобы отключить автоматическую проверку обновлений, перейдите в диалоговое окно Параметры NuGet и снимите флажок **автоматически проверять наличие обновлений**.</span><span class="sxs-lookup"><span data-stu-id="76222-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Параметры NuGet](./media/nuget-settings.png)

<span data-ttu-id="76222-150">Эта функция на самом деле была добавлена в NuGet 1,3, но она не будет видима, разумеется, пока не станет доступной обновление 1,3, например NuGet 1,4.</span><span class="sxs-lookup"><span data-stu-id="76222-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="76222-151">Усовершенствования диалогового окна диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="76222-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="76222-152">**Улучшенные имена меню**: параметры меню для запуска диалогового окна были переименованы для ясности.</span><span class="sxs-lookup"><span data-stu-id="76222-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="76222-153">Теперь команда меню **управляет пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="76222-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="76222-154">**Область сведений показывает дату последнего обновления**. в диалоговом окне NuGet отображается дата последнего обновления в области сведений для пакета, если выбрана вкладка "в **сети** " или " **обновления** ".</span><span class="sxs-lookup"><span data-stu-id="76222-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="76222-155">**Список отображаемых тегов**. в диалоговом окне NuGet отображаются теги.</span><span class="sxs-lookup"><span data-stu-id="76222-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="76222-156">Усовершенствования PowerShell</span><span class="sxs-lookup"><span data-stu-id="76222-156">Powershell Improvements</span></span>
* <span data-ttu-id="76222-157">**Подписанные скрипты PowerShell**. NuGet включает подписанные сценарии PowerShell, которые позволяют использовать более узкие среды.</span><span class="sxs-lookup"><span data-stu-id="76222-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="76222-158">**Поддержка запросов**. консоль диспетчера пакетов теперь поддерживает запросы с помощью `$host.ui.Prompt` `$host.ui.PromptForChoice` команд и.</span><span class="sxs-lookup"><span data-stu-id="76222-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="76222-159">**Имена источников пакетов**. Указание имени источника пакета поддерживается при указании источника пакета с помощью `-Source` флага.</span><span class="sxs-lookup"><span data-stu-id="76222-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="76222-160">nuget.exe улучшения командной строки</span><span class="sxs-lookup"><span data-stu-id="76222-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="76222-161">**Пользовательские команды NuGet**. nuget.exe расширяются с помощью пользовательских команд, использующих MEF.</span><span class="sxs-lookup"><span data-stu-id="76222-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="76222-162">**Более простой рабочий процесс для создания пакетов символов**. `-Symbols` флаг можно применить к стандартной структуре папок на основе соглашения, создающей пакет символов, только включая исходный файл и `.pdb` файлы в папке.</span><span class="sxs-lookup"><span data-stu-id="76222-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="76222-163">**Указание нескольких источников**. `NuGet install` команда поддерживает указание нескольких источников, используя точку с запятой в качестве разделителя или `-Source` несколько раз.</span><span class="sxs-lookup"><span data-stu-id="76222-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="76222-164">**Поддержка проверки подлинности прокси-сервера**. NuGet 1,4 добавляет поддержку запроса учетных данных пользователя при использовании NuGet за прокси-сервером, требующем проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="76222-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="76222-165">**Критическое изменениеnuget.exe обновления**. `-Self` флаг теперь требуется для обновления nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="76222-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="76222-166">`nuget.exe Update` Теперь принимает путь к `packages.config` файлу и пытается обновить пакеты.</span><span class="sxs-lookup"><span data-stu-id="76222-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="76222-167">Обратите внимание, что это обновление ограничено тем, что оно не будет: \* \* обновление, Добавление и удаление содержимого в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="76222-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="76222-168">\* \* Запуск скриптов PowerShell в пакете.</span><span class="sxs-lookup"><span data-stu-id="76222-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="76222-169">Поддержка сервера NuGet для отправки пакетов с помощью nuget.exe</span><span class="sxs-lookup"><span data-stu-id="76222-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="76222-170">NuGet предоставляет простой способ размещения [упрощенного веб-репозитория NuGet](../hosting-packages/nuget-server.md) через `NuGet.Server` пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="76222-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="76222-171">В NuGet 1,4 Облегченный сервер поддерживает принудительную отправку и удаление пакетов с помощью nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="76222-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="76222-172">Последняя версия `NuGet.Server` добавляет новый объект `appSetting` с именем `apiKey` .</span><span class="sxs-lookup"><span data-stu-id="76222-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="76222-173">Если ключ не указан или оставлен пустым, отправка пакетов в веб-канал отключается.</span><span class="sxs-lookup"><span data-stu-id="76222-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="76222-174">Установка значения apiKey (в идеале надежный пароль) позволяет принудительно передавать пакеты с помощью nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="76222-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="76222-175">Поддержка средств Windows Phoneного выпуска</span><span class="sxs-lookup"><span data-stu-id="76222-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="76222-176">Теперь NuGet поддерживается в версии-кандидате средств Windows Phone Tools для системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="76222-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="76222-177">В настоящее время средства Windows Phone не поддерживают диспетчер расширений Visual Studio, поэтому для установки NuGet для Windows Phone инструментов может потребоваться Скачать и запустить VSIX вручную.</span><span class="sxs-lookup"><span data-stu-id="76222-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="76222-178">Чтобы удалить NuGet для Windows Phone инструментов, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="76222-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a><span data-ttu-id="76222-179">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="76222-179">Bug Fixes</span></span>
<span data-ttu-id="76222-180">В NuGet 1,4 было исправлено всего 88 рабочих элементов.</span><span class="sxs-lookup"><span data-stu-id="76222-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="76222-181">71 из них были помечены как ошибки.</span><span class="sxs-lookup"><span data-stu-id="76222-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="76222-182">Полный список рабочих элементов, исправленных в NuGet 1,4, см. в [этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="76222-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="76222-183">Исправлены ошибки, которые следует отметить:</span><span class="sxs-lookup"><span data-stu-id="76222-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="76222-184">[Ошибка 603](http://nuget.codeplex.com/workitem/603). зависимости пакета в разных репозиториях разрешаются правильно при указании определенного источника пакета.</span><span class="sxs-lookup"><span data-stu-id="76222-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="76222-185">[Ошибка 1036](http://nuget.codeplex.com/workitem/1036): Добавление `NuGet Pack SomeProject.csproj` события после сборки больше не приводит к бесконечному циклу.</span><span class="sxs-lookup"><span data-stu-id="76222-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="76222-186">[Ошибка 961](http://nuget.codeplex.com/workitem/961): `-Source` флаг поддерживает относительные пути.</span><span class="sxs-lookup"><span data-stu-id="76222-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="76222-187">Обновление NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="76222-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="76222-188">Вскоре после выпуска NuGet 1,4 мы обнаружили несколько проблем, которые были важны для исправления.</span><span class="sxs-lookup"><span data-stu-id="76222-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="76222-189">Номер версии этого обновления для 1,4 — 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="76222-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="76222-190">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="76222-190">Bug Fixes</span></span>
* <span data-ttu-id="76222-191">[Проблема 1220](http://nuget.codeplex.com/workitem/1220): Update-Package не выполняется `install.ps1` / `uninstall.ps1` во всех проектах, если имеется более одного проекта</span><span class="sxs-lookup"><span data-stu-id="76222-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="76222-192">[Ошибка 1156](http://nuget.codeplex.com/workitem/1156): Диспетчер пакетов консолей в W2K3/XP (если не установлена оболочка PowerShell 2)</span><span class="sxs-lookup"><span data-stu-id="76222-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
