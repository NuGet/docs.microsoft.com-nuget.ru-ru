---
title: Заметки о выпуске 2.1 NuGet
description: Заметки о выпуске для NuGet 2.1, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548601"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="14eb0-103">Заметки о выпуске 2.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="14eb0-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="14eb0-104">[Заметки о выпуске NuGet 2.0](../release-notes/nuget-2.0.md) | [заметки о выпуске NuGet 2.2](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="14eb0-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="14eb0-105">NuGet 2.1 была выпущена 4 октября 2012 г.</span><span class="sxs-lookup"><span data-stu-id="14eb0-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="14eb0-106">Иерархические Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="14eb0-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="14eb0-107">NuGet 2.1 обеспечивает большую гибкость в управлении параметры NuGet посредством рекурсивно проходу вверх структуру папок, ищете `NuGet.Config` файлы, а затем построить из набора всех найденных файлов конфигурации.</span><span class="sxs-lookup"><span data-stu-id="14eb0-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="14eb0-108">Например рассмотрим ситуацию, где предусмотрела репозиторием внутреннего пакета для сборок непрерывной Интеграции других внутренних зависимостей.</span><span class="sxs-lookup"><span data-stu-id="14eb0-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="14eb0-109">Структура папок для отдельного проекта может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="14eb0-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="14eb0-110">Кроме того Если включается восстановление пакетов для решения, будет также существовать следующую папку:</span><span class="sxs-lookup"><span data-stu-id="14eb0-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="14eb0-111">Чтобы у команды внутреннего пакета репозиторий доступен для всех проектов, которые группа работает, а не делая его доступным для каждого проекта на компьютере, мы можно создать новый файл Nuget.Config и поместить его в папке c:\myteam.</span><span class="sxs-lookup"><span data-stu-id="14eb0-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="14eb0-112">Не существует способа для указания папки пакетов для проекта.</span><span class="sxs-lookup"><span data-stu-id="14eb0-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="14eb0-113">Теперь мы видим, что источник был добавлен с помощью команды «nuget.exe источники» из любой папки под c:\myteam как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="14eb0-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Источники пакетов из родительской конфигурации nuget](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="14eb0-115">`NuGet.Config` Поиск файлов выполняется в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="14eb0-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="14eb0-116">Рекурсивные стека из папки проекта к корню</span><span class="sxs-lookup"><span data-stu-id="14eb0-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="14eb0-117">Глобальный `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="14eb0-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="14eb0-118">Конфигурации находятся не в *обратный порядок*, основаны на порядок выше это означает, что глобальный файл Nuget.Config будет быть применяется первой, следуют обнаруженным файлам Nuget.Config из корневого каталога в папку проекта, по `.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="14eb0-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="14eb0-119">Это особенно важно в том случае, если вы используете `<clear/>` элемента, удаляемого набора элементов из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="14eb0-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="14eb0-120">Укажите «пакеты» расположение папки</span><span class="sxs-lookup"><span data-stu-id="14eb0-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="14eb0-121">В прошлом NuGet управляемого решения пакеты из папки известных «пакеты» найден в корневой папке решения.</span><span class="sxs-lookup"><span data-stu-id="14eb0-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="14eb0-122">Для групп разработчиков, имеющих множество различных решений, которые установлены пакеты NuGet это может привести в том же пакете, устанавливаемого в различных местах в файловой системе.</span><span class="sxs-lookup"><span data-stu-id="14eb0-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="14eb0-123">NuGet 2.1 обеспечивает более детальный контроль над расположение папки с пакетами с помощью `repositoryPath` элемент `NuGet.Config` файла.</span><span class="sxs-lookup"><span data-stu-id="14eb0-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="14eb0-124">Основываясь на предыдущем примере поддержка иерархической структуры Nuget.Config, предполагается, что нам требуется отправить все проекты в общем ресурсе C:\myteam\ той же папке пакетов.</span><span class="sxs-lookup"><span data-stu-id="14eb0-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="14eb0-125">Для этого просто добавьте следующую запись `c:\myteam\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="14eb0-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="14eb0-126">В этом примере общий `Nuget.Config` файл указывает папку Общие пакеты для каждого проекта, созданного под C:\myteam, независимо от глубины.</span><span class="sxs-lookup"><span data-stu-id="14eb0-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="14eb0-127">Обратите внимание, что при наличии существующей папке, в пакеты под корневом каталоге решения, необходимо удалить его, прежде чем NuGet разместит пакеты в новом расположении.</span><span class="sxs-lookup"><span data-stu-id="14eb0-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="14eb0-128">Поддержка переносимых библиотек</span><span class="sxs-lookup"><span data-stu-id="14eb0-128">Support for Portable Libraries</span></span>

<span data-ttu-id="14eb0-129">[Переносимые библиотеки](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) — это функция, впервые представленный в .NET 4, который позволяет создавать сборки, которые могут работать без внесения изменений на разных платформах Microsoft, созданных в версиях платформы.NET Framework для Silverlight для Windows Phone и даже Xbox 360 (хотя в настоящее время NuGet не поддерживает целевой переносимой библиотеки Xbox).</span><span class="sxs-lookup"><span data-stu-id="14eb0-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="14eb0-130">Путем расширения [упаковать соглашения](../create-packages/supporting-multiple-target-frameworks.md) для профилей и framework версии NuGet 2.1 теперь поддерживает переносимые библиотеки, позволяя создавать пакеты, которые имеют составное framework и целевой профиль `lib` папки.</span><span class="sxs-lookup"><span data-stu-id="14eb0-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="14eb0-131">Например рассмотрим следующие переносимой библиотеки классов доступных платформ.</span><span class="sxs-lookup"><span data-stu-id="14eb0-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Диалоговое окно создания переносимой библиотеки](./media/releasenotes-21-plib.png)

<span data-ttu-id="14eb0-133">После сборки библиотеки и команда `nuget.exe pack MyPortableProject.csproj` запускается новый портативный структуру папок пакета библиотеки можно увидеть, проверив содержимое созданного пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="14eb0-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Макет пакета переносимой библиотеки](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="14eb0-135">Как вы видите, соглашение переносимой библиотеки папки имя соответствует шаблону «переносимой-{framework 1} + {framework n}» где идентификаторов платформы выполните существующий [соглашения об имени и версии framework](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="14eb0-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="14eb0-136">Единственным исключением из соглашения об имени и версии можно найти в framework идентификатор, используемый для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="14eb0-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="14eb0-137">Данный моникер следует использовать имя платформы «wp» (wp7, wp71 или wp8).</span><span class="sxs-lookup"><span data-stu-id="14eb0-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="14eb0-138">Например, с помощью «silverlight-wp7» приведет к ошибкой.</span><span class="sxs-lookup"><span data-stu-id="14eb0-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="14eb0-139">При установке пакета, созданный на основе этой структуры папок, NuGet теперь правила можно применять его framework и профиль для нескольких целевых объектов, как указано в имени папки.</span><span class="sxs-lookup"><span data-stu-id="14eb0-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="14eb0-140">За правил сопоставления NuGet — это принцип, что целевые объекты «подробные» будет иметь приоритет над «менее конкретными».</span><span class="sxs-lookup"><span data-stu-id="14eb0-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="14eb0-141">Это означает, что моникеров, предназначенных для определенной платформы будет всегда будет предпочтительнее переносимых из них, если они оба совместимы с проектом.</span><span class="sxs-lookup"><span data-stu-id="14eb0-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="14eb0-142">Кроме того Если несколько целевых объектов, переносимых совместимы с проектом, NuGet предпочтут той, где набор платформ, поддерживаемых «близко расположенные» в проект ссылки на пакет.</span><span class="sxs-lookup"><span data-stu-id="14eb0-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="14eb0-143">Предназначенных для Windows 8 и Windows Phone 8 проектов</span><span class="sxs-lookup"><span data-stu-id="14eb0-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="14eb0-144">Помимо добавления поддержки для нацеливания на проекты переносимых библиотек, NuGet 2.1 обеспечивает новый моникеры платформ для проектов Windows 8 Store и Windows Phone 8, а также некоторые новые общие моникеры для Windows Store и проекты Windows Phone, которые будут проще управлять в будущих версиях для соответствующих платформ.</span><span class="sxs-lookup"><span data-stu-id="14eb0-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="14eb0-145">Для приложений Windows 8 Store идентификаторы выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="14eb0-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="14eb0-146">NuGet 2.0 и более ранних версий</span><span class="sxs-lookup"><span data-stu-id="14eb0-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="14eb0-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="14eb0-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="14eb0-148">winRT45. NETCore45</span><span class="sxs-lookup"><span data-stu-id="14eb0-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="14eb0-149">Windows, Windows8, win, win8</span><span class="sxs-lookup"><span data-stu-id="14eb0-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="14eb0-150">Для проектов Windows Phone идентификаторы выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="14eb0-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="14eb0-151">Phone OS</span><span class="sxs-lookup"><span data-stu-id="14eb0-151">Phone OS</span></span> | <span data-ttu-id="14eb0-152">NuGet 2.0 и более ранних версий</span><span class="sxs-lookup"><span data-stu-id="14eb0-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="14eb0-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="14eb0-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="14eb0-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="14eb0-154">Windows Phone 7</span></span> | <span data-ttu-id="14eb0-155">silverlight3 wp</span><span class="sxs-lookup"><span data-stu-id="14eb0-155">silverlight3-wp</span></span> | <span data-ttu-id="14eb0-156">WP, WindowsPhone7 wp7, WindowsPhone,</span><span class="sxs-lookup"><span data-stu-id="14eb0-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="14eb0-157">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="14eb0-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="14eb0-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="14eb0-158">silverlight4-wp71</span></span> | <span data-ttu-id="14eb0-159">wp71 WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="14eb0-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="14eb0-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="14eb0-160">Windows Phone 8</span></span> | <span data-ttu-id="14eb0-161">(не поддерживается)</span><span class="sxs-lookup"><span data-stu-id="14eb0-161">(not supported)</span></span> | <span data-ttu-id="14eb0-162">wp8 WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="14eb0-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="14eb0-163">Во всех указанных выше изменений старые имена framework будет продолжать полностью поддерживаются NuGet 2.1.</span><span class="sxs-lookup"><span data-stu-id="14eb0-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="14eb0-164">В дальнейшем новые имена можно использовать как и стабильнее будущими версиями для соответствующих платформ.</span><span class="sxs-lookup"><span data-stu-id="14eb0-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="14eb0-165">Новые имена будут *не* быть поддерживается в версиях NuGet до 2.1, тем не менее, поэтому планируйте сеансы момента, когда нужно переключить.</span><span class="sxs-lookup"><span data-stu-id="14eb0-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="14eb0-166">Улучшенный поиск в диалоговом окне диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="14eb0-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="14eb0-167">За последние несколько итераций изменения, появившиеся в коллекцию NuGet, который значительно улучшена скорость и релевантности поиска пакета.</span><span class="sxs-lookup"><span data-stu-id="14eb0-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="14eb0-168">Тем не менее эти усовершенствования были ограничены веб-сайт nuget.org.</span><span class="sxs-lookup"><span data-stu-id="14eb0-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="14eb0-169">NuGet 2.1 предоставляет улучшенные возможности поиска посредством диалогового окна диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="14eb0-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="14eb0-170">В качестве примера предположим, что вы хотите найти пакет Windows Azure Caching Preview.</span><span class="sxs-lookup"><span data-stu-id="14eb0-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="14eb0-171">Разумный поисковый запрос для этого пакета может быть «Azure Cache».</span><span class="sxs-lookup"><span data-stu-id="14eb0-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="14eb0-172">В предыдущих версиях диалоговое окно диспетчера пакетов требуемому пакету бы даже отсутствовать на первой странице результатов.</span><span class="sxs-lookup"><span data-stu-id="14eb0-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="14eb0-173">Тем не менее в NuGet 2.1, нужного пакета теперь отображается в верхней части результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="14eb0-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Поиск диалоговое окно диспетчера пакетов](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="14eb0-175">Принудительное обновление пакета</span><span class="sxs-lookup"><span data-stu-id="14eb0-175">Force Package Update</span></span>

<span data-ttu-id="14eb0-176">До NuGet 2.1, NuGet пропустить обновление пакета при отсутствии не номером версии высокого уровня.</span><span class="sxs-lookup"><span data-stu-id="14eb0-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="14eb0-177">Это вызывает трудностей для определенных сценариев — особенно в случае построения или сценариях непрерывной Интеграции, где команда не хотели увеличить число при каждой сборке версию пакета.</span><span class="sxs-lookup"><span data-stu-id="14eb0-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="14eb0-178">Принудительно выполнить обновление, независимо от того, было требуемое поведение.</span><span class="sxs-lookup"><span data-stu-id="14eb0-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="14eb0-179">NuGet 2.1 решает эту проблему с флагом «переустановить».</span><span class="sxs-lookup"><span data-stu-id="14eb0-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="14eb0-180">Например предыдущие версии NuGet приведет следующие при попытке обновить пакет, который не имеет более новая версия пакета:</span><span class="sxs-lookup"><span data-stu-id="14eb0-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="14eb0-181">С флагом переустановить пакет будет обновляться независимо от того, следует ли более новая версия.</span><span class="sxs-lookup"><span data-stu-id="14eb0-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="14eb0-182">Еще один сценарий, которого флаг reinstall подтверждает полезно — это повторно нацеливание на платформу.</span><span class="sxs-lookup"><span data-stu-id="14eb0-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="14eb0-183">При изменении целевой платформы проекта (например, в .NET 4-.NET 4.5), Update-Package-переустановить можно обновить ссылки на верные сборки для всех пакетов NuGet, установленные в проекте.</span><span class="sxs-lookup"><span data-stu-id="14eb0-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="14eb0-184">Изменить источники пакетов в среде Visual Studio</span><span class="sxs-lookup"><span data-stu-id="14eb0-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="14eb0-185">В предыдущих версиях NuGet обновление источника пакета из в диалоговом окне Visual Studio параметры, необходимые для удаления и повторного добавления источника пакета.</span><span class="sxs-lookup"><span data-stu-id="14eb0-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="14eb0-186">NuGet 2.1 улучшает этот рабочий процесс, поддерживая обновление как функции первого класса пользовательского интерфейса конфигурации.</span><span class="sxs-lookup"><span data-stu-id="14eb0-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Диалоговое окно настройки диспетчера пакетов](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="14eb0-188">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="14eb0-188">Bug Fixes</span></span>

<span data-ttu-id="14eb0-189">NuGet 2.1 включает множество исправлений ошибок.</span><span class="sxs-lookup"><span data-stu-id="14eb0-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="14eb0-190">Полный список рабочих элементов исправленные в NuGet 2.0 обратитесь представление [Issue Tracker NuGet для этого выпуска](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="14eb0-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
