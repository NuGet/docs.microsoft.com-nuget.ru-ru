---
title: "Заметки о выпуске NuGet 2.1 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 2.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.1 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 05cdb898cc674ac7eadb238d41896638d8e3488c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="97757-104">Заметки о выпуске 2.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="97757-104">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="97757-105">[Заметки о выпуске NuGet 2.0](../release-notes/nuget-2.0.md) | [заметки о выпуске NuGet 2.2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="97757-105">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="97757-106">NuGet 2.1 был выпущен 4 октября 2012 г.</span><span class="sxs-lookup"><span data-stu-id="97757-106">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="97757-107">Иерархические Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="97757-107">Hierarchical Nuget.Config</span></span>
<span data-ttu-id="97757-108">NuGet 2.1 обеспечивает большую гибкость в управлении параметры NuGet посредством рекурсивно проходу вверх структура папок поиска `NuGet.Config` файлы и затем построения из набора всех найденных файлов конфигурации.</span><span class="sxs-lookup"><span data-stu-id="97757-108">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="97757-109">Например рассмотрим сценарий, где команды имеет внутренний пакет репозиторий для построения CI другие внутренние зависимости.</span><span class="sxs-lookup"><span data-stu-id="97757-109">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="97757-110">Структура папок для отдельного проекта может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="97757-110">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="97757-111">Кроме того Если восстановление пакета включен для решения, появятся следующую папку:</span><span class="sxs-lookup"><span data-stu-id="97757-111">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="97757-112">Для выполнения команды внутреннего пакета репозитория для всех проектов, в которых работает команда, не сделана доступной для каждого проекта на компьютере, мы создайте новый файл Nuget.Config и поместите его в папку c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="97757-112">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="97757-113">Невозможно до указания папку пакетов на один проект.</span><span class="sxs-lookup"><span data-stu-id="97757-113">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="97757-114">Теперь можно увидеть, что источник был добавлен, выполнив команду «nuget.exe источников» из любой папки под c:\myteam как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="97757-114">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Источники пакетов из родительской конфигурации nuget](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="97757-116">`NuGet.Config`Поиск файлов выполняется в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="97757-116">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="97757-117">Рекурсивные стека из папки проекта к корню</span><span class="sxs-lookup"><span data-stu-id="97757-117">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="97757-118">Глобальный `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="97757-118">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="97757-119">Конфигурации представлены не применяются в *в обратном порядке*, это значит, что на основе выше заказ, глобальные Nuget.Config бы быть применялся первым, следуют обнаруженные файлы Nuget.Config из корневой папки проекта, а затем по `.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="97757-119">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="97757-120">Это особенно важно, если вы используете `<clear/>` элемента для удаления набора элементов из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="97757-120">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="97757-121">Укажите «пакеты» расположение папки</span><span class="sxs-lookup"><span data-stu-id="97757-121">Specify ‘packages’ Folder Location</span></span>
<span data-ttu-id="97757-122">В прошлом NuGet управляемого пакеты решения из папки известных «пакеты» найден в корневой папке решения.</span><span class="sxs-lookup"><span data-stu-id="97757-122">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="97757-123">Группы разработчиков, которые имеют много различные решения, имеющие установить пакеты NuGet это может привести в том же пакете, устанавливаемого в различных местах в файловой системе.</span><span class="sxs-lookup"><span data-stu-id="97757-123">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="97757-124">NuGet 2.1 обеспечивает более детальный контроль над расположение папки пакетов через `repositoryPath` элемент `NuGet.Config` файла.</span><span class="sxs-lookup"><span data-stu-id="97757-124">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="97757-125">Построение в предыдущем примере поддержка иерархической структуры Nuget.Config, предположим, что нам требуется, чтобы все проекты в общем ресурсе C:\myteam\ той же папке пакетов.</span><span class="sxs-lookup"><span data-stu-id="97757-125">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="97757-126">Чтобы сделать это, просто добавьте следующую запись `c:\myteam\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="97757-126">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="97757-127">В этом примере общий `Nuget.Config` файл определяет общие пакеты папку для каждого проекта, созданного под C:\myteam, вне зависимости от глубины.</span><span class="sxs-lookup"><span data-stu-id="97757-127">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="97757-128">Обратите внимание, что при наличии существующей папке пакетов в корне решения необходимо будет удалить его перед NuGet будет помещать пакетов в новое расположение.</span><span class="sxs-lookup"><span data-stu-id="97757-128">Note that if you have an existing packages folder underneath your solution root, you will need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="97757-129">Поддержка переносимой библиотеки</span><span class="sxs-lookup"><span data-stu-id="97757-129">Support for Portable Libraries</span></span>
<span data-ttu-id="97757-130">[Переносимые библиотеки](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) — это функция, впервые появившаяся .NET 4, который позволяет создавать сборки, которые могут работать без изменений на различных платформах Майкрософт, из версий платформы.NET Framework для Silverlight для Windows Phone и Xbox даже 360 (хотя NuGet в настоящее время не поддерживается целевой переносимой библиотеки Xbox).</span><span class="sxs-lookup"><span data-stu-id="97757-130">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="97757-131">Расширив [пакета соглашения](../create-packages/supporting-multiple-target-frameworks.md) для профилей и версии framework NuGet 2.1 теперь поддерживает переносимой библиотеки, позволяя создавать пакеты, имеющие комплексной .NET framework и целевой профиль `lib` папки.</span><span class="sxs-lookup"><span data-stu-id="97757-131">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="97757-132">Например рассмотрим следующие переносимой библиотеки классов доступные целевые платформы.</span><span class="sxs-lookup"><span data-stu-id="97757-132">As an example, consider the following portable class library’s available target platforms.</span></span>

![Диалоговое окно создания переносимой библиотеки](./media/releasenotes-21-plib.png)

<span data-ttu-id="97757-134">После построения библиотеки и команда `nuget.exe pack MyPortableProject.csproj` запускается новый портативный структуру папок пакета в библиотеку можно увидеть, проверив содержимое созданного пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="97757-134">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Макет пакета переносимой библиотеки](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="97757-136">Как видите, соглашение о имя папки переносимой библиотеки соответствует шаблону «переносимой-{framework 1} + {framework n}» где идентификаторы framework выполните существующих [framework имя и версию соглашения](../schema/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="97757-136">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../schema/target-frameworks.md).</span></span> <span data-ttu-id="97757-137">Единственным исключением из соглашения имени и версии можно найти в framework идентификатор, используемый для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="97757-137">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="97757-138">Этот моникер следует использовать имя платформы «wp» (wp7, wp71 или wp8).</span><span class="sxs-lookup"><span data-stu-id="97757-138">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="97757-139">С помощью «wp7 silverlight», например, приведет к ошибку.</span><span class="sxs-lookup"><span data-stu-id="97757-139">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="97757-140">При установке пакета, которая создается на основе этой структуры папок, NuGet теперь правила можно применять его платформа и профиль для нескольких целевых объектов, как указано в имени папки.</span><span class="sxs-lookup"><span data-stu-id="97757-140">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="97757-141">За NuGet правила сопоставления является принцип, что целевые объекты «подробные» будет иметь приоритет над ««частных.</span><span class="sxs-lookup"><span data-stu-id="97757-141">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="97757-142">Это означает, что моникеров, предназначенных для конкретных платформ всегда предпочтительный приоритет переносимой тем если они оба совместимы с проектом.</span><span class="sxs-lookup"><span data-stu-id="97757-142">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="97757-143">Кроме того Если несколько целевых объектов переносимой совместимы с проектом, NuGet, предпочтут тем, где набор платформ, поддерживаемых в «близко расположенные» в проект ссылки на пакет.</span><span class="sxs-lookup"><span data-stu-id="97757-143">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="97757-144">Выбора целевой платформы Windows 8 и Windows Phone 8 проектов</span><span class="sxs-lookup"><span data-stu-id="97757-144">Targeting Windows 8 and Windows Phone 8 Projects</span></span>
<span data-ttu-id="97757-145">В дополнение к Добавление поддержки для нацеливания на проекты переносимых библиотек, NuGet 2.1 предоставляет моникеров новые платформы проектов магазина Windows 8 и Windows Phone 8, а также некоторые новые общие моникеров для магазина Windows и Windows Phone проекты, которые будут Упрощение управления будущими версиями соответствующих платформ.</span><span class="sxs-lookup"><span data-stu-id="97757-145">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="97757-146">Для приложений для магазина Windows 8 идентификаторы выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="97757-146">For Windows 8 Store applications, the identifiers look as follows:</span></span>

|<span data-ttu-id="97757-147">NuGet 2.0 и более ранних версий</span><span class="sxs-lookup"><span data-stu-id="97757-147">NuGet 2.0 and earlier</span></span>|<span data-ttu-id="97757-148">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="97757-148">NuGet 2.1</span></span>|
|----------------|-----------|
|<span data-ttu-id="97757-149">winRT45, .NETCore45</span><span class="sxs-lookup"><span data-stu-id="97757-149">winRT45, .NETCore45</span></span>|<span data-ttu-id="97757-150">Windows, Windows8, win, win8</span><span class="sxs-lookup"><span data-stu-id="97757-150">Windows, Windows8, win, win8</span></span>|

<br/>
<span data-ttu-id="97757-151">Для проектов Windows Phone идентификаторы выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="97757-151">For Windows Phone projects, the identifiers look as follows:</span></span>

|<span data-ttu-id="97757-152">Phone ОС</span><span class="sxs-lookup"><span data-stu-id="97757-152">Phone OS</span></span>|<span data-ttu-id="97757-153">NuGet 2.0 и более ранних версий</span><span class="sxs-lookup"><span data-stu-id="97757-153">NuGet 2.0 and earlier</span></span>|<span data-ttu-id="97757-154">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="97757-154">NuGet 2.1</span></span>
|----------------|-----------|-----------|
|<span data-ttu-id="97757-155">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="97757-155">Windows Phone 7</span></span>|<span data-ttu-id="97757-156">silverlight3 wp</span><span class="sxs-lookup"><span data-stu-id="97757-156">silverlight3-wp</span></span>|<span data-ttu-id="97757-157">wp, wp7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="97757-157">wp, wp7, WindowsPhone, WindowsPhone7</span></span>|
|<span data-ttu-id="97757-158">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="97757-158">Windows Phone 7.5 (Mango)</span></span>|<span data-ttu-id="97757-159">silverilght4-wp71</span><span class="sxs-lookup"><span data-stu-id="97757-159">silverilght4-wp71</span></span>|<span data-ttu-id="97757-160">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="97757-160">wp71, WindowsPhone71</span></span>|
|<span data-ttu-id="97757-161">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="97757-161">Windows Phone 8</span></span>|<span data-ttu-id="97757-162">(не поддерживается)</span><span class="sxs-lookup"><span data-stu-id="97757-162">(not supported)</span></span>|<span data-ttu-id="97757-163">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="97757-163">wp8, WindowsPhone8</span></span>|
<br/>
<span data-ttu-id="97757-164">Все изменения старые имена framework будет продолжать полностью поддерживаются NuGet 2.1.</span><span class="sxs-lookup"><span data-stu-id="97757-164">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="97757-165">Продвижение вперед, новые имена можно использовать как они будут более стабильные будущими версиями соответствующих платформ.</span><span class="sxs-lookup"><span data-stu-id="97757-165">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="97757-166">Новые имена будут *не* быть поддерживается в версиях, предшествовавших 2.1 NuGet, тем не менее, поэтому соответственно планировать время, чтобы переключиться.</span><span class="sxs-lookup"><span data-stu-id="97757-166">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="97757-167">Улучшение поиска в диалоговом окне диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="97757-167">Improved Search in Package Manager Dialog</span></span>
<span data-ttu-id="97757-168">За последние несколько итераций изменения были введены в коллекции NuGet, существенно повышает скорость и релевантности поиска пакета.</span><span class="sxs-lookup"><span data-stu-id="97757-168">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="97757-169">Однако эти усовершенствования были ограничены nuget.org веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="97757-169">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="97757-170">NuGet 2.1 делает Улучшенный поиск возникнуть доступными через диалоговое окно диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="97757-170">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="97757-171">В качестве примера предположим, требуется найти пакет Windows Azure Caching Preview.</span><span class="sxs-lookup"><span data-stu-id="97757-171">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="97757-172">Запрос разумного поиска для этого пакета может быть «Azure Cache».</span><span class="sxs-lookup"><span data-stu-id="97757-172">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="97757-173">В предыдущих версиях диалогового окна диспетчера пакетов нужный пакет будет не даже будут перечислены на первую страницу результатов.</span><span class="sxs-lookup"><span data-stu-id="97757-173">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="97757-174">Однако в NuGet версии 2.1, нужный пакет теперь отображается в верхней части результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="97757-174">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Пакет диспетчера диалоговое окно поиска](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="97757-176">Принудительное обновление пакета</span><span class="sxs-lookup"><span data-stu-id="97757-176">Force Package Update</span></span>
<span data-ttu-id="97757-177">До NuGet 2.1 NuGet пропустить обновление пакета при отсутствии не номер версии высокого уровня.</span><span class="sxs-lookup"><span data-stu-id="97757-177">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="97757-178">Это появился трения в определенных случаях — особенно в случае сборки или CI сценарии, где команды не следует увеличивать номер при каждом построении версии пакета.</span><span class="sxs-lookup"><span data-stu-id="97757-178">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="97757-179">Для принудительного обновления независимо от того, была желаемое поведение.</span><span class="sxs-lookup"><span data-stu-id="97757-179">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="97757-180">NuGet 2.1 решает эту проблему с флагом «переустановить».</span><span class="sxs-lookup"><span data-stu-id="97757-180">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="97757-181">Например предыдущие версии NuGet приведет к появлению следующих при попытке обновить пакет была установлена более новая версия пакета:</span><span class="sxs-lookup"><span data-stu-id="97757-181">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="97757-182">С помощью флага переустановить пакет будет обновляться независимо от того, следует ли имеется более новая версия.</span><span class="sxs-lookup"><span data-stu-id="97757-182">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="97757-183">Другой сценарий, где флаг reinstall оказывается полезным представляет framework требуемой версии.</span><span class="sxs-lookup"><span data-stu-id="97757-183">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="97757-184">При изменении целевой платформы проекта (например, с .NET 4 в .NET 4.5), пакет обновления-переустановить можно обновить ссылки для исправления сборок для всех пакетов NuGet, установленные в проекте.</span><span class="sxs-lookup"><span data-stu-id="97757-184">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="97757-185">Изменение источников пакетов в среде Visual Studio</span><span class="sxs-lookup"><span data-stu-id="97757-185">Edit Package Sources Within Visual Studio</span></span>
<span data-ttu-id="97757-186">В предыдущих версиях NuGet обновление источника пакета в диалоговом окне обозревателя Visual Studio, необходимые для удаления и повторного добавления источника пакета.</span><span class="sxs-lookup"><span data-stu-id="97757-186">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="97757-187">NuGet 2.1 улучшает этот рабочий процесс с помощью поддержки обновления как функции первого класса пользовательского интерфейса конфигурации.</span><span class="sxs-lookup"><span data-stu-id="97757-187">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Диалоговое окно конфигурации диспетчера пакетов](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="97757-189">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="97757-189">Bug Fixes</span></span>
<span data-ttu-id="97757-190">NuGet 2.1 содержит много исправлений ошибок.</span><span class="sxs-lookup"><span data-stu-id="97757-190">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="97757-191">Полный список рабочих элементов исправления в NuGet 2.0 представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="97757-191">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
