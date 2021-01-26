---
title: Заметки о выпуске NuGet 2,1
description: Заметки о выпуске NuGet 2,1, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777025"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="a38ce-103">Заметки о выпуске NuGet 2,1</span><span class="sxs-lookup"><span data-stu-id="a38ce-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="a38ce-104">[Заметки о](../release-notes/nuget-2.0.md)  |  выпуске NuGet 2,0 [Заметки о выпуске NuGet 2,2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="a38ce-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="a38ce-105">Версия NuGet 2,1 была выпущена 4 октября 2012 г.</span><span class="sxs-lookup"><span data-stu-id="a38ce-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="a38ce-106">Иерархическая Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="a38ce-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="a38ce-107">NuGet 2,1 предоставляет большую гибкость в управлении параметрами NuGet с помощью рекурсивного прохода по структуре папок для поиска `NuGet.Config` файлов и последующей сборки конфигурации из набора всех найденных файлов.</span><span class="sxs-lookup"><span data-stu-id="a38ce-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="a38ce-108">В качестве примера рассмотрим ситуацию, когда у команды есть внутренний репозиторий пакетов для CI-сборок других внутренних зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a38ce-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="a38ce-109">Структура папок для отдельного проекта может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a38ce-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="a38ce-110">Кроме того, если для решения включено восстановление пакетов, будет также существовать Следующая папка:</span><span class="sxs-lookup"><span data-stu-id="a38ce-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="a38ce-111">Чтобы обеспечить доступность внутреннего репозитория пакетов для всех проектов, над которыми работает команда, не делая ее доступной для каждого проекта на компьютере, можно создать новый файл Nuget.Config и поместить его в папку к:\митеам.</span><span class="sxs-lookup"><span data-stu-id="a38ce-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="a38ce-112">Для каждого проекта невозможно выполнить конкретную папку пакетов.</span><span class="sxs-lookup"><span data-stu-id="a38ce-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="a38ce-113">Теперь можно увидеть, что источник добавлен, запустив команду "nuget.exe источники" из любой папки под к:\митеам, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="a38ce-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Источники пакетов из родительской конфигурации NuGet](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="a38ce-115">`NuGet.Config` Поиск файлов выполняется в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="a38ce-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="a38ce-116">Рекурсивный обход из папки проекта в корневую папку</span><span class="sxs-lookup"><span data-stu-id="a38ce-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="a38ce-117">Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )</span><span class="sxs-lookup"><span data-stu-id="a38ce-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="a38ce-118">Конфигурации применяются в *обратном порядке*, то есть в соответствии с приведенным выше порядком, сначала применяется Глобальная Nuget.Config, а затем обнаруженные Nuget.Config файлы из корневой папки в папку проекта, а затем `.nuget\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="a38ce-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="a38ce-119">Это особенно важно, если вы используете `<clear/>` элемент для удаления набора элементов из конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a38ce-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="a38ce-120">Укажите расположение папки "Packages"</span><span class="sxs-lookup"><span data-stu-id="a38ce-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="a38ce-121">В прошлом NuGet управляет пакетами решения из известной папки Packages, найденной в корневой папке решения.</span><span class="sxs-lookup"><span data-stu-id="a38ce-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="a38ce-122">Для команд разработчиков, имеющих множество различных решений, на которых установлены пакеты NuGet, это может привести к установке одного и того же пакета во многих разных местах файловой системы.</span><span class="sxs-lookup"><span data-stu-id="a38ce-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="a38ce-123">NuGet 2,1 обеспечивает более детальный контроль расположения папки Packages с помощью `repositoryPath` элемента в `NuGet.Config` файле.</span><span class="sxs-lookup"><span data-stu-id="a38ce-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="a38ce-124">Основываясь на предыдущем примере поддержки иерархических Nuget.Config, предположим, что нам нужно, чтобы все проекты в К:\митеам\ использовали одну и ту же папку пакетов.</span><span class="sxs-lookup"><span data-stu-id="a38ce-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="a38ce-125">Для этого просто добавьте следующую запись в `c:\myteam\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="a38ce-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="a38ce-126">В этом примере общий `Nuget.Config` файл указывает общую папку пакетов для каждого проекта, созданного под к:\митеам, независимо от глубины.</span><span class="sxs-lookup"><span data-stu-id="a38ce-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="a38ce-127">Обратите внимание, что если у вас есть папка Packages под корнем решения, необходимо удалить ее, прежде чем NuGet поместит пакеты в новое расположение.</span><span class="sxs-lookup"><span data-stu-id="a38ce-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="a38ce-128">Поддержка переносимых библиотек</span><span class="sxs-lookup"><span data-stu-id="a38ce-128">Support for Portable Libraries</span></span>

<span data-ttu-id="a38ce-129">[Переносимые библиотеки](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) — это функция, впервые появившаяся в .NET 4, которая позволяет создавать сборки, которые могут работать без изменений на разных платформах Майкрософт, от версий The.NET Framework до Silverlight для Windows Phone и даже Xbox 360 (хотя в настоящее время NuGet не поддерживает целевой объект переносимой библиотеки Xbox).</span><span class="sxs-lookup"><span data-stu-id="a38ce-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="a38ce-130">Расширяя [соглашения о пакетах](../create-packages/supporting-multiple-target-frameworks.md) для версий и профилей платформы, NuGet 2,1 теперь поддерживает переносимые библиотеки, позволяя создавать пакеты с составными папками платформы и целевого профиля `lib` .</span><span class="sxs-lookup"><span data-stu-id="a38ce-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="a38ce-131">В качестве примера рассмотрим следующие доступные целевые платформы переносимой библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="a38ce-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Диалоговое окно создания переносимой библиотеки](./media/releasenotes-21-plib.png)

<span data-ttu-id="a38ce-133">После сборки библиотеки и `nuget.exe pack MyPortableProject.csproj` выполнения команды можно просмотреть новую структуру папок пакета переносимой библиотеки, изучив содержимое созданного пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="a38ce-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Макет переносимого пакета библиотеки](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="a38ce-135">Как видите, соглашение о имени папки переносимой библиотеки соответствует шаблону "Portable-{Framework 1} + {Framework n}", где идентификаторы платформы соответствуют [соглашениям о существующем имени и версии платформы](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="a38ce-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="a38ce-136">Одно исключение из соглашений об имени и версии находится в идентификаторе платформы, используемом для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a38ce-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="a38ce-137">В этом моникере следует использовать имя платформы "WP" (WP7, wp71 или WP8).</span><span class="sxs-lookup"><span data-stu-id="a38ce-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="a38ce-138">Например, использование "Silverlight-WP7" приведет к ошибке.</span><span class="sxs-lookup"><span data-stu-id="a38ce-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="a38ce-139">При установке пакета, созданного из этой структуры папок, NuGet теперь может применять свои платформы и правила профилей к нескольким целевым объектам, как указано в имени папки.</span><span class="sxs-lookup"><span data-stu-id="a38ce-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="a38ce-140">Правила сопоставления NuGet являются принципом того, что "более конкретные" целевые объекты имеют приоритет над "менее конкретными".</span><span class="sxs-lookup"><span data-stu-id="a38ce-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="a38ce-141">Это означает, что моникеры, предназначенные для конкретной платформы, всегда будут предпочтительнее, чем переносимые, если они совместимы с проектом.</span><span class="sxs-lookup"><span data-stu-id="a38ce-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="a38ce-142">Кроме того, если несколько переносимых целевых объектов совместимы с проектом, NuGet будет предпочитать, что набор поддерживаемых платформ является ближайшим к проекту, ссылающимся на пакет.</span><span class="sxs-lookup"><span data-stu-id="a38ce-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="a38ce-143">Нацеливание на проекты Windows 8 и Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="a38ce-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="a38ce-144">Помимо добавления поддержки для проектов с переносимыми библиотеками, NuGet 2,1 предоставляет новые моникеры платформы для Магазина Windows 8 и Windows Phone 8, а также некоторые новые общие моникеры для проектов Магазина Windows и Windows Phone, которые проще всего управлять в будущих версиях соответствующих платформ.</span><span class="sxs-lookup"><span data-stu-id="a38ce-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="a38ce-145">Для приложений Магазина Windows 8 идентификаторы выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a38ce-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="a38ce-146">NuGet 2,0 и более ранних версий</span><span class="sxs-lookup"><span data-stu-id="a38ce-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="a38ce-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="a38ce-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="a38ce-148">winRT45, . NETCore45</span><span class="sxs-lookup"><span data-stu-id="a38ce-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="a38ce-149">Windows, Windows8, Win, Win8</span><span class="sxs-lookup"><span data-stu-id="a38ce-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="a38ce-150">Для проектов Windows Phone идентификаторы выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a38ce-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="a38ce-151">Телефонная ОС</span><span class="sxs-lookup"><span data-stu-id="a38ce-151">Phone OS</span></span> | <span data-ttu-id="a38ce-152">NuGet 2,0 и более ранних версий</span><span class="sxs-lookup"><span data-stu-id="a38ce-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="a38ce-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="a38ce-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a38ce-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="a38ce-154">Windows Phone 7</span></span> | <span data-ttu-id="a38ce-155">Silverlight3-WP</span><span class="sxs-lookup"><span data-stu-id="a38ce-155">silverlight3-wp</span></span> | <span data-ttu-id="a38ce-156">WP, WP7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="a38ce-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="a38ce-157">Windows Phone 7,5 (с)</span><span class="sxs-lookup"><span data-stu-id="a38ce-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="a38ce-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="a38ce-158">silverlight4-wp71</span></span> | <span data-ttu-id="a38ce-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="a38ce-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="a38ce-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="a38ce-160">Windows Phone 8</span></span> | <span data-ttu-id="a38ce-161">(Не поддерживается)</span><span class="sxs-lookup"><span data-stu-id="a38ce-161">(not supported)</span></span> | <span data-ttu-id="a38ce-162">WP8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="a38ce-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="a38ce-163">Во всех перечисленных выше изменениях старые имена платформ будут по прежнему поддерживаться в NuGet 2,1.</span><span class="sxs-lookup"><span data-stu-id="a38ce-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="a38ce-164">При перемещении вперед используются новые имена, так как они будут более стабильными в будущих версиях соответствующих платформ.</span><span class="sxs-lookup"><span data-stu-id="a38ce-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="a38ce-165">Новые имена *не* будут поддерживаться в версиях NuGet до 2,1, поэтому необходимо соответствующим образом спланировать, когда следует использовать параметр.</span><span class="sxs-lookup"><span data-stu-id="a38ce-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="a38ce-166">Улучшенный поиск в диалоговом окне диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="a38ce-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="a38ce-167">За последние несколько итераций появились изменения в коллекции NuGet, которые значительно улучшили скорость и релевантность поиска пакетов.</span><span class="sxs-lookup"><span data-stu-id="a38ce-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="a38ce-168">Однако эти улучшения были ограничены веб-сайтом nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a38ce-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="a38ce-169">NuGet 2,1 делает Улучшенный интерфейс поиска доступным в диалоговом окне диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="a38ce-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="a38ce-170">В качестве примера представьте, что вы хотели бы найти пакет предварительной версии Windows Azure Caching.</span><span class="sxs-lookup"><span data-stu-id="a38ce-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="a38ce-171">Разумный поисковый запрос для этого пакета может быть "кэшем Azure".</span><span class="sxs-lookup"><span data-stu-id="a38ce-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="a38ce-172">В предыдущих версиях диалогового окна Диспетчер пакетов нужный пакет даже не был указан на первой странице результатов.</span><span class="sxs-lookup"><span data-stu-id="a38ce-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="a38ce-173">Однако в NuGet 2,1 требуемый пакет теперь отображается в верхней части результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="a38ce-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Поиск в диалоговом окне диспетчера пакетов](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="a38ce-175">Принудительное обновление пакета</span><span class="sxs-lookup"><span data-stu-id="a38ce-175">Force Package Update</span></span>

<span data-ttu-id="a38ce-176">До NuGet 2,1 NuGet пропустит обновление пакета, если не был задан старший номер версии.</span><span class="sxs-lookup"><span data-stu-id="a38ce-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="a38ce-177">Это сделало трение для определенных сценариев, особенно в случае сценариев сборки или CI, в которых команде не нужно увеличивать номер версии пакета при каждой сборке.</span><span class="sxs-lookup"><span data-stu-id="a38ce-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="a38ce-178">Требуемое поведение заключается в принудительном обновлении без учета.</span><span class="sxs-lookup"><span data-stu-id="a38ce-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="a38ce-179">NuGet 2,1 обращается к этому параметру с флагом "REINSTALL".</span><span class="sxs-lookup"><span data-stu-id="a38ce-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="a38ce-180">Например, предыдущие версии NuGet приведут к следующим результатам при попытке обновить пакет, для которого не была установлена более поздняя версия пакета:</span><span class="sxs-lookup"><span data-stu-id="a38ce-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="a38ce-181">При использовании флага переустановки пакет будет обновлен независимо от наличия более новой версии.</span><span class="sxs-lookup"><span data-stu-id="a38ce-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="a38ce-182">Другой сценарий, в котором флаг переустановки подтверждает преимущества, заключается в том, что платформа перенацелена на платформу.</span><span class="sxs-lookup"><span data-stu-id="a38ce-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="a38ce-183">При изменении целевой платформы проекта (например, с .NET 4 на .NET 4,5) Update-Package-REINSTALL может обновить ссылки на правильные сборки для всех пакетов NuGet, установленных в проекте.</span><span class="sxs-lookup"><span data-stu-id="a38ce-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="a38ce-184">Изменение источников пакетов в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a38ce-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="a38ce-185">В предыдущих версиях NuGet обновление источника пакета в диалоговом окне "Параметры Visual Studio" требовало удаления и повторного добавления источника пакета.</span><span class="sxs-lookup"><span data-stu-id="a38ce-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="a38ce-186">NuGet 2,1 улучшает этот рабочий процесс, поддерживая обновление как функцию первого класса пользовательского интерфейса конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a38ce-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Диалоговое окно настройки диспетчера пакетов](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="a38ce-188">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="a38ce-188">Bug Fixes</span></span>

<span data-ttu-id="a38ce-189">NuGet 2,1 включает множество исправлений ошибок.</span><span class="sxs-lookup"><span data-stu-id="a38ce-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="a38ce-190">Полный список рабочих элементов, исправленных в NuGet 2,0, см. в [этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="a38ce-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
