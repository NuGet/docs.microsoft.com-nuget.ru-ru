---
title: Разрешение зависимостей для пакетов NuGet
description: Сведения о процессе разрешения зависимостей для пакета NuGet и их установки в NuGet 2.x и NuGet 3.x+.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: bfe6e348fa9a8f5df7f28509098260128920c528
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="how-nuget-resolves-package-dependencies"></a><span data-ttu-id="1eb48-103">Принципы разрешения зависимостей пакетов в NuGet</span><span class="sxs-lookup"><span data-stu-id="1eb48-103">How NuGet resolves package dependencies</span></span>

<span data-ttu-id="1eb48-104">При любой установке или переустановке пакета, включая установку в рамках процесса [восстановления](../consume-packages/package-restore.md), NuGet также устанавливает все дополнительные пакеты, от которых зависит этот первый пакет.</span><span class="sxs-lookup"><span data-stu-id="1eb48-104">Any time a package is installed or reinstalled, which includes being installed as part of a [restore](../consume-packages/package-restore.md) process, NuGet also installs any additional packages on which that first package depends.</span></span>

<span data-ttu-id="1eb48-105">Эти прямые зависимости также могут иметь собственные зависимости, уходящие на произвольную глубину.</span><span class="sxs-lookup"><span data-stu-id="1eb48-105">Those immediate dependencies might then also have dependencies on their own, which can continue to an arbitrary depth.</span></span> <span data-ttu-id="1eb48-106">В результате образуется так называемая *схема зависимостей*, описывающая связи между пакетами на всех уровнях.</span><span class="sxs-lookup"><span data-stu-id="1eb48-106">This produces what's called a *dependency graph* that describes the relationships between packages at all levels.</span></span>

<span data-ttu-id="1eb48-107">Если несколько пакетов имеют одинаковую зависимость, один идентификатор пакета может отображаться на графе несколько раз, возможно, с другими ограничениями по версиям.</span><span class="sxs-lookup"><span data-stu-id="1eb48-107">When multiple packages have the same dependency, then the same package ID can appear in the graph multiple times, potentially with different version constraints.</span></span> <span data-ttu-id="1eb48-108">Однако в проекте можно использовать только одну версию заданного пакета, поэтому NuGet нужно выбрать подходящую версию.</span><span class="sxs-lookup"><span data-stu-id="1eb48-108">However, only one version of a given package can be used in a project, so NuGet must choose which version is used.</span></span> <span data-ttu-id="1eb48-109">Конкретная процедура зависит от используемого формата управления пакетами.</span><span class="sxs-lookup"><span data-stu-id="1eb48-109">The exact process depends on the package management format being used.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="1eb48-110">Разрешение зависимостей при использовании PackageReference</span><span class="sxs-lookup"><span data-stu-id="1eb48-110">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="1eb48-111">При установке пакетов в проекты с использованием формата PackageReference, NuGet добавляет ссылки на плоскую схему пакета в соответствующий файл и разрешает конфликты заранее.</span><span class="sxs-lookup"><span data-stu-id="1eb48-111">When installing packages into projects using the PackageReference format, NuGet adds references to a flat package graph in the appropriate file and resolves conflicts ahead of time.</span></span> <span data-ttu-id="1eb48-112">Этот процесс называется *транзитивным восстановлением*.</span><span class="sxs-lookup"><span data-stu-id="1eb48-112">This process is referred to as *transitive restore*.</span></span> <span data-ttu-id="1eb48-113">В этом случае переустановка или восстановление пакетов представляют собой скачивание пакетов, указанных на графе, в результате чего сборки выполняются быстрее и более предсказуемо.</span><span class="sxs-lookup"><span data-stu-id="1eb48-113">Reinstalling or restoring packages is then a process of downloading the packages listed in the graph, resulting in faster and more predictable builds.</span></span> <span data-ttu-id="1eb48-114">Вы также можете воспользоваться преимуществами групповых версий, таких как 2.8. \*, избавившись от ресурсоемких и подверженных ошибкам вызовов `nuget update` на клиентских компьютерах и серверах сборки.</span><span class="sxs-lookup"><span data-stu-id="1eb48-114">You can also take advantage of wildcard (floating) versions, such as 2.8.\*, avoiding expensive and error prone calls to `nuget update` on the client machines and build servers.</span></span>

<span data-ttu-id="1eb48-115">Когда перед сборкой выполняется процесс восстановления NuGet, он сначала устраняет зависимости в памяти, а затем записывает полученную схему в файл с именем `project.assets.json` в папке `obj` проекта с использованием PackageReference.</span><span class="sxs-lookup"><span data-stu-id="1eb48-115">When the NuGet restore process runs prior to a build, it resolves dependencies first in memory, then writes the resulting graph to a file called `project.assets.json` in the `obj` folder of a project using PackageReference.</span></span> <span data-ttu-id="1eb48-116">После этого MSBuild считывает этот файл и преобразует его в набор папок, где можно найти потенциальные ссылки, а затем добавляет их в дерево проектов в памяти.</span><span class="sxs-lookup"><span data-stu-id="1eb48-116">MSBuild then reads this file and translates it into a set of folders where potential references can be found, and then adds them to the project tree in memory.</span></span>

<span data-ttu-id="1eb48-117">Файл блокировки является временным, поэтому добавлять его в систему управления исходным кодом не нужно.</span><span class="sxs-lookup"><span data-stu-id="1eb48-117">The lock file is temporary and should not be added to source control.</span></span> <span data-ttu-id="1eb48-118">Он указан по умолчанию в `.gitignore` и `.tfignore`.</span><span class="sxs-lookup"><span data-stu-id="1eb48-118">It's listed by default in both `.gitignore` and `.tfignore`.</span></span> <span data-ttu-id="1eb48-119">См. раздел [Пакеты и система управления версиями](packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="1eb48-119">See [Packages and source control](packages-and-source-control.md).</span></span>

### <a name="dependency-resolution-rules"></a><span data-ttu-id="1eb48-120">Правила разрешения зависимостей</span><span class="sxs-lookup"><span data-stu-id="1eb48-120">Dependency resolution rules</span></span>

<span data-ttu-id="1eb48-121">Для разрешения зависимостей транзитивное восстановление применяет четыре основных правила: минимально приемлемая версия, групповые версии, ближайшее совпадение и родственные зависимости.</span><span class="sxs-lookup"><span data-stu-id="1eb48-121">Transitive restore applies four main rules to resolve dependencies: lowest applicable version, floating versions, nearest-wins, and cousin dependencies.</span></span>

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a><span data-ttu-id="1eb48-122">Минимально приемлемая версия</span><span class="sxs-lookup"><span data-stu-id="1eb48-122">Lowest applicable version</span></span>

<span data-ttu-id="1eb48-123">Правило минимально приемлемой версии восстанавливает наименьшую версию пакета, определяемую его зависимостями.</span><span class="sxs-lookup"><span data-stu-id="1eb48-123">The lowest applicable version rule restores the lowest possible version of a package as defined by its dependencies.</span></span> <span data-ttu-id="1eb48-124">Она также применяется к зависимостям для приложения и библиотеки классов, если только та не объявлена как [групповая](#floating-versions).</span><span class="sxs-lookup"><span data-stu-id="1eb48-124">It also applies to dependencies on the application or the class library unless declared as [floating](#floating-versions).</span></span>

<span data-ttu-id="1eb48-125">Например, на следующем рисунке 1.0-beta считается ниже, чем 1.0, поэтому NuGet выбирает версию 1.0:</span><span class="sxs-lookup"><span data-stu-id="1eb48-125">In the following figure, for example, 1.0-beta is considered lower than 1.0 so NuGet chooses the 1.0 version:</span></span>

![Выбор минимально приемлемой версии](media/projectJson-dependency-1.png)

<span data-ttu-id="1eb48-127">На следующем рисунке версия 2.1 недоступна в веб-канале, но так как ограничение по версии имеет значение >= 2.1, NuGet выбирает следующую наименьшую версию, которую может найти, в данном случае это 2.2:</span><span class="sxs-lookup"><span data-stu-id="1eb48-127">In the next figure, version 2.1 is not available on the feed but because the version constraint is >= 2.1 NuGet picks the next lowest version it can find, in this case 2.2:</span></span>

![Выбор следующей наименьшей версии из доступных в веб-канале](media/projectJson-dependency-2.png)

<span data-ttu-id="1eb48-129">Если приложение указывает точный номер версии, например 1.2, который недоступен в веб-канале, NuGet завершается с ошибкой при попытке установить или восстановить этот пакет:</span><span class="sxs-lookup"><span data-stu-id="1eb48-129">When an application specifies an exact version number, such as 1.2, that is not available on the feed, NuGet fails with an error when attempting to install or restore the package:</span></span>

![NuGet выдает ошибку, если точная версия пакета недоступна](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a><span data-ttu-id="1eb48-131">Групповые версии</span><span class="sxs-lookup"><span data-stu-id="1eb48-131">Floating (wildcard) versions</span></span>

<span data-ttu-id="1eb48-132">Групповая версия зависимости указывается с помощью подстановочного знака \*, например 6.0.\*.</span><span class="sxs-lookup"><span data-stu-id="1eb48-132">A floating or wildcard dependency version is specified with the \* wildcard, as with 6.0.\*.</span></span> <span data-ttu-id="1eb48-133">Такая запись версии указывает, что нужно использовать самую последнюю версию 6.0.x. Если указано 4.\*, нужно использовать последнюю версию 4.x.</span><span class="sxs-lookup"><span data-stu-id="1eb48-133">This version specification says "use the latest 6.0.x version"; 4.\* means "use the latest 4.x version."</span></span> <span data-ttu-id="1eb48-134">Использование подстановочного знака позволяет последовательно дорабатывать пакет зависимостей без внесения изменений в использующее его приложение (или пакет).</span><span class="sxs-lookup"><span data-stu-id="1eb48-134">Using a wildcard allows a dependency package to continue evolving without requiring a change to the consuming application (or package).</span></span>

<span data-ttu-id="1eb48-135">При наличии подстановочного знака NuGet разрешает самую новую версию пакета, соответствующую заданному шаблону. Например, при значении 6.0.\* используется самая новая версия пакета, начинающаяся с 6.0:</span><span class="sxs-lookup"><span data-stu-id="1eb48-135">When using a wildcard, NuGet resolves the highest version of a package that matches the version pattern, for example 6.0.\* gets the highest version of a package that starts with 6.0:</span></span>

![Выбор версии 6.0.1, когда запрошена групповая версия 6.0.\*](media/projectJson-dependency-4.png)

> [!Note]
> <span data-ttu-id="1eb48-137">Сведения о работе групповых и предварительных версий см. в разделе [Управление версиями пакетов](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="1eb48-137">For information on the behavior of wildcards and pre-release versions, see [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a><span data-ttu-id="1eb48-138">Ближайшее совпадение</span><span class="sxs-lookup"><span data-stu-id="1eb48-138">Nearest wins</span></span>

<span data-ttu-id="1eb48-139">Если граф пакетов для приложения содержит разные версии одного пакета, NuGet выбирает пакет, который находится ближе всего к приложению на графе, и игнорирует остальные.</span><span class="sxs-lookup"><span data-stu-id="1eb48-139">When the package graph for an application contains different versions of the same package, NuGet chooses the package that's closest to the application in the graph and ignores all others.</span></span> <span data-ttu-id="1eb48-140">Такое поведение позволяет приложению переопределить любую конкретную версию пакета на графе зависимостей.</span><span class="sxs-lookup"><span data-stu-id="1eb48-140">This behavior allows an application to override any particular package version in the dependency graph.</span></span>

<span data-ttu-id="1eb48-141">В следующем примере приложение зависит непосредственно от пакета B с ограничением по версии >=2.0.</span><span class="sxs-lookup"><span data-stu-id="1eb48-141">In the example below, the application depends directly on Package B with a version constraint of >=2.0.</span></span> <span data-ttu-id="1eb48-142">Кроме того, приложение зависит от пакета A, который, в свою очередь, зависит от пакета B, но с ограничением >=1.0.</span><span class="sxs-lookup"><span data-stu-id="1eb48-142">The application also depends on Package A which in turn also depends on Package B, but with a >=1.0 constraint.</span></span> <span data-ttu-id="1eb48-143">Так как в графе зависимость от версии 2.0 пакета B находится ближе всего к приложению, используется эта версия:</span><span class="sxs-lookup"><span data-stu-id="1eb48-143">Because the dependency on Package B 2.0 is nearer to the application in the graph, that version is used:</span></span>

![Приложение, использующее правило ближайшего совпадения](media/projectJson-dependency-5.png)

>[!Warning]
> <span data-ttu-id="1eb48-145">Правило ближайшего совпадения может привести к понижению версии пакета, что способно нарушить другие зависимости на графе.</span><span class="sxs-lookup"><span data-stu-id="1eb48-145">The Nearest Wins rule can result in a downgrade of the package version, thus potentially breaking other dependencies in the graph.</span></span> <span data-ttu-id="1eb48-146">Поэтому при использовании данного правила выдается предупреждение для пользователя.</span><span class="sxs-lookup"><span data-stu-id="1eb48-146">Hence this rule is applied with a warning to alert the user.</span></span>

<span data-ttu-id="1eb48-147">Кроме того, это правило также эффективнее работает с крупным графом зависимостей (например, как в случае с пакетами BCL), так как после пропуска заданной зависимости NuGet также игнорирует все оставшиеся зависимости в этой ветви графа.</span><span class="sxs-lookup"><span data-stu-id="1eb48-147">This rule also results in greater efficiency with a large dependency graph (such as those with the BCL packages) because once a given dependency is ignored, NuGet also ignores all remaining dependencies on that branch of the graph.</span></span> <span data-ttu-id="1eb48-148">На следующей схеме из-за использования версии 2.0 пакета C NuGet игнорирует все ветви графа, относящиеся к более старой версии пакета C:</span><span class="sxs-lookup"><span data-stu-id="1eb48-148">In the diagram below, for example, because Package C 2.0 is used, NuGet ignores any branches in the graph that refer to an older version of Package C:</span></span>

![Если NuGet игнорирует пакет на графе, он пропускает всю эту ветвь](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a><span data-ttu-id="1eb48-150">Родственные зависимости</span><span class="sxs-lookup"><span data-stu-id="1eb48-150">Cousin dependencies</span></span>

<span data-ttu-id="1eb48-151">Когда на графе разные версии пакета находятся на одинаковом удалении от приложения, NuGet использует самую раннюю версию, удовлетворяющую всем требованиям к версии (как в случае с правилами [минимально приемлемой версии](#lowest-applicable-version) и [групповых версий](#floating-versions)).</span><span class="sxs-lookup"><span data-stu-id="1eb48-151">When different package versions are referred to at the same distance in the graph from the application, NuGet uses the lowest version that satisfies all version requirements (as with the [lowest applicable version](#lowest-applicable-version) and [floating versions](#floating-versions) rules).</span></span> <span data-ttu-id="1eb48-152">Например, на рисунке ниже версия 2.0 пакета B удовлетворяет другому ограничению версии >=1.0 и поэтому используется:</span><span class="sxs-lookup"><span data-stu-id="1eb48-152">In the image below, for example, version 2.0 of Package B satisfies the other >=1.0 constraint, and is thus used:</span></span>

![Разрешение родственных зависимостей с помощью наиболее ранней версии, удовлетворяющей всем ограничениям](media/projectJson-dependency-7.png)

<span data-ttu-id="1eb48-154">В некоторых случаях удовлетворить все требования к версии невозможно.</span><span class="sxs-lookup"><span data-stu-id="1eb48-154">In some cases, it's not possible to meet all version requirements.</span></span> <span data-ttu-id="1eb48-155">Как показано ниже, если пакету A требуется именно версия 1.0 пакета B, а пакету C требуется пакет B версии >=2.0, то NuGet не может разрешить эти зависимости и выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="1eb48-155">As shown below, if Package A requires exactly Package B 1.0 and Package C requires Package B >=2.0, then NuGet cannot resolve the dependencies and gives an error.</span></span>

![Неразрешаемые зависимости из-за потребности в точной версии](media/projectJson-dependency-8.png)

<span data-ttu-id="1eb48-157">В таких ситуациях потребителю верхнего уровня (приложение или пакет) следует добавить собственную прямую зависимость от пакета B, чтобы применялось правило [ближайшего совпадения](#nearest-wins).</span><span class="sxs-lookup"><span data-stu-id="1eb48-157">In these situations, the top-level consumer (the application or package) should add its own direct dependency on Package B so that the [Nearest Wins](#nearest-wins) rule applies.</span></span>

## <a name="dependency-resolution-with-packagesconfig"></a><span data-ttu-id="1eb48-158">Разрешение зависимостей для packages.config</span><span class="sxs-lookup"><span data-stu-id="1eb48-158">Dependency resolution with packages.config</span></span>

<span data-ttu-id="1eb48-159">При использовании `packages.config` зависимости проекта записываются в `packages.config` в виде плоского списка.</span><span class="sxs-lookup"><span data-stu-id="1eb48-159">With `packages.config`, a project's dependencies are written to `packages.config` as a flat list.</span></span> <span data-ttu-id="1eb48-160">Все зависимости этих пакетов также записываются в тот же список.</span><span class="sxs-lookup"><span data-stu-id="1eb48-160">Any dependencies of those packages are also written in the same list.</span></span> <span data-ttu-id="1eb48-161">При установке пакетов NuGet также может изменить файл `.csproj`, `app.config`, `web.config` и другие отдельные файлы.</span><span class="sxs-lookup"><span data-stu-id="1eb48-161">When packages are installed, NuGet might also modify the `.csproj` file, `app.config`, `web.config`, and other individual files.</span></span>

<span data-ttu-id="1eb48-162">При использовании `packages.config` NuGet пытается разрешить конфликты зависимостей во время установки каждого отдельного пакета.</span><span class="sxs-lookup"><span data-stu-id="1eb48-162">With `packages.config`, NuGet attempts to resolve dependency conflicts during the installation of each individual package.</span></span> <span data-ttu-id="1eb48-163">Таким образом, если устанавливается пакет A, зависящий от пакета B, а пакет B уже указан в `packages.config` в качестве зависимости для чего-то еще, NuGet сравнивает запрошенные версии пакета B и пытается найти ту из них, которая соответствует всем ограничениям по версиям.</span><span class="sxs-lookup"><span data-stu-id="1eb48-163">That is, if Package A is being installed and depends on Package B, and Package B is already listed in `packages.config` as a dependency of something else, NuGet compares the versions of Package B being requested and attempts to find a version that satisfies all version constraints.</span></span> <span data-ttu-id="1eb48-164">В частности, NuGet выбирает более низкую версию *основной_номер.дополнительный_номер*, которая удовлетворяет зависимостям.</span><span class="sxs-lookup"><span data-stu-id="1eb48-164">Specifically, NuGet selects the lower *major.minor* version that satisfies dependencies.</span></span>

<span data-ttu-id="1eb48-165">По умолчанию NuGet 2.8 ищет самую раннюю версию исправления (см. [заметки о выпуске NuGet 2.8](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)).</span><span class="sxs-lookup"><span data-stu-id="1eb48-165">By default, NuGet 2.8 looks for the lowest patch version (see [NuGet 2.8 release notes](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)).</span></span> <span data-ttu-id="1eb48-166">Вы можете управлять этим параметром с помощью атрибута `DependencyVersion` в `Nuget.Config` и параметра `-DependencyVersion` в командной строке.</span><span class="sxs-lookup"><span data-stu-id="1eb48-166">You can control this setting through the `DependencyVersion` attribute in `Nuget.Config` and the `-DependencyVersion` switch on the command line.</span></span>  

<span data-ttu-id="1eb48-167">Для более крупных графов процесс разрешения зависимостей `packages.config` усложняется.</span><span class="sxs-lookup"><span data-stu-id="1eb48-167">The `packages.config` process for resolving dependencies gets complicated for larger dependency graphs.</span></span> <span data-ttu-id="1eb48-168">При каждой новой установке пакета требуется обход всего графа, а также повышается вероятность конфликтов версий.</span><span class="sxs-lookup"><span data-stu-id="1eb48-168">Each new package installation requires a traversal of the whole graph and raises the chance for version conflicts.</span></span> <span data-ttu-id="1eb48-169">При возникновении конфликта установка останавливается, оставляя проект в неопределенном состоянии, что особенно касается потенциальных изменений в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="1eb48-169">When a conflict occurs, installation is stopped, leaving the project in an indeterminate state, especially with potential modifications to the project file itself.</span></span> <span data-ttu-id="1eb48-170">Эта проблема не актуальна при использовании других форматов управления пакетами.</span><span class="sxs-lookup"><span data-stu-id="1eb48-170">This is not an issue when using other package management formats.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="1eb48-171">Управление ресурсами зависимостей</span><span class="sxs-lookup"><span data-stu-id="1eb48-171">Managing dependency assets</span></span>

<span data-ttu-id="1eb48-172">При использовании формата PackageReference вы можете управлять тем, какие ресурсы из зависимостей переходят в проект верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="1eb48-172">When using the PackageReference format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="1eb48-173">Дополнительные сведения см. в разделе [Управление ресурсами зависимости](package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="1eb48-173">For details, see [PackageReference](package-references-in-project-files.md#controlling-dependency-assets).</span></span>

<span data-ttu-id="1eb48-174">Если проект верхнего уровня сам является пакетом, вы также можете управлять этим переходом, используя атрибуты `include` и `exclude` для зависимостей, перечисленных в файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="1eb48-174">When the top-level project is itself a package, you also have control over this flow by using the `include` and `exclude` attributes with dependencies listed in the `.nuspec` file.</span></span> <span data-ttu-id="1eb48-175">См. подраздел "Зависимости" в разделе [Справочник по файлам NUSPEC](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="1eb48-175">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="1eb48-176">Исключение ссылок</span><span class="sxs-lookup"><span data-stu-id="1eb48-176">Excluding references</span></span>

<span data-ttu-id="1eb48-177">Существуют сценарии, когда проект может ссылаться на сборки с одинаковым именем несколько раз, что вызывает ошибки времени разработки и времени сборки.</span><span class="sxs-lookup"><span data-stu-id="1eb48-177">There are scenarios in which assemblies with the same name might be referenced more than once in a project, producing design-time and build-time errors.</span></span> <span data-ttu-id="1eb48-178">Рассмотрим проект, который содержит настраиваемую версию `C.dll` и ссылается на пакет C, который также содержит `C.dll`.</span><span class="sxs-lookup"><span data-stu-id="1eb48-178">Consider a project that contains a custom version of `C.dll`, and references Package C that also contains `C.dll`.</span></span> <span data-ttu-id="1eb48-179">В то же время проект зависит от пакета B, который, в свою очередь, зависит от пакета C и `C.dll`.</span><span class="sxs-lookup"><span data-stu-id="1eb48-179">At the same time, the project also depends on Package B which also depends on Package C and `C.dll`.</span></span> <span data-ttu-id="1eb48-180">В результате NuGet не может определить, какую `C.dll` использовать. Однако вы не можете просто удалить зависимость проекта от пакета C, так как от него зависит и пакет B.</span><span class="sxs-lookup"><span data-stu-id="1eb48-180">As a result, NuGet can't determine which `C.dll` to use, but you can't just remove the project's dependency on Package C because Package B also depends on it.</span></span>

<span data-ttu-id="1eb48-181">Чтобы разрешить эту ситуацию, нужно напрямую сослаться на нужную `C.dll` (или использовать другой пакет с правильной ссылкой) и затем добавить зависимость от пакета C, которая исключает все его ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1eb48-181">To resolve this, you must directly reference the `C.dll` you want (or use another package that references the right one), and then add a dependency on Package C that excludes all its assets.</span></span> <span data-ttu-id="1eb48-182">Это делается следующим образом в зависимости от используемого формата управления пакетами:</span><span class="sxs-lookup"><span data-stu-id="1eb48-182">This is done as follows depending on the package management format in use:</span></span>

- <span data-ttu-id="1eb48-183">[PackageReference](../consume-packages/package-references-in-project-files.md): добавьте `Exclude="All"` в зависимость:</span><span class="sxs-lookup"><span data-stu-id="1eb48-183">[PackageReference](../consume-packages/package-references-in-project-files.md): add `Exclude="All"` in the dependency:</span></span>

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- <span data-ttu-id="1eb48-184">`packages.config`: удалите ссылку на пакет PackageC из файла `.csproj`, чтобы он ссылался только на нужную версию `C.dll`.</span><span class="sxs-lookup"><span data-stu-id="1eb48-184">`packages.config`: remove the reference to PackageC from the `.csproj` file so that it references only the version of `C.dll` that you want.</span></span>
    
## <a name="dependency-updates-during-package-install"></a><span data-ttu-id="1eb48-185">Обновление зависимостей при установке пакета</span><span class="sxs-lookup"><span data-stu-id="1eb48-185">Dependency updates during package install</span></span> 

<span data-ttu-id="1eb48-186">Если версия зависимости уже удовлетворена, зависимость не обновляется при установке других пакетов.</span><span class="sxs-lookup"><span data-stu-id="1eb48-186">If a dependency version is already satisfied, the dependency isn't updated during other package installations.</span></span> <span data-ttu-id="1eb48-187">Например, рассмотрим пакет A, который зависит от пакета B и указывает номер версии 1.0.</span><span class="sxs-lookup"><span data-stu-id="1eb48-187">For example, consider package A that depends on package B and specifies 1.0 for the version number.</span></span> <span data-ttu-id="1eb48-188">Исходный репозиторий содержит версии 1.0, 1.1 и 1.2 пакета B. Если установить пакет A в проекте, который уже содержит версию 1.0 пакета B, то пакет B версии 1.0 все еще будет использоваться, так как это удовлетворяет ограничение по версии.</span><span class="sxs-lookup"><span data-stu-id="1eb48-188">The source repository contains versions 1.0, 1.1, and 1.2 of package B. If A is installed in a project that already contains B version 1.0, then B 1.0 remains in use because it satisfies the version constraint.</span></span> <span data-ttu-id="1eb48-189">Однако если бы пакет A запрашивал для пакета B версию 1.1 или более позднюю, был бы установлен пакет B версии 1.2.</span><span class="sxs-lookup"><span data-stu-id="1eb48-189">However, if package A had requests version 1.1 or higher of B, then B 1.2 would be installed.</span></span> 

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="1eb48-190">Устранение ошибок с несовместимостью пакетов</span><span class="sxs-lookup"><span data-stu-id="1eb48-190">Resolving incompatible package errors</span></span>

<span data-ttu-id="1eb48-191">При операции восстановления пакета вы можете увидеть ошибку "One or more packages are not compatible" (Один или несколько пакетов несовместимы) или сообщение о несовместимости пакета с целевой платформой проекта.</span><span class="sxs-lookup"><span data-stu-id="1eb48-191">During a package restore operation, you may see the error "One or more packages are not compatible..." or that a package "is not compatible" with the project's target framework.</span></span>

<span data-ttu-id="1eb48-192">Эта ошибка возникает, когда один или несколько пакетов, на которые ссылается ваш проект, не сообщают о поддержке целевой платформы проекта. В результате пакет не содержит подходящую библиотеку DLL в своей папке `lib` для целевой платформы, совместимой с этим проектом.</span><span class="sxs-lookup"><span data-stu-id="1eb48-192">This error occurs when one or more of the packages referenced in your project do not indicate that they support the project's target framework; that is, the package does not contain a suitable DLL in its `lib` folder for a target framework that is compatible with the project.</span></span> <span data-ttu-id="1eb48-193">(Список см. в разделе [Целевые платформы](../reference/target-frameworks.md).)</span><span class="sxs-lookup"><span data-stu-id="1eb48-193">(See [Target frameworks](../reference/target-frameworks.md) for a list.)</span></span> 

<span data-ttu-id="1eb48-194">Например, если проект предназначен для `netstandard1.6` и вы пытаетесь установить пакет, содержащий библиотеки DLL, только в папках `lib\net20` и `\lib\net45`, то для пакета и, возможно, его зависимостей могут отображаться следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="1eb48-194">For example, if a project targets `netstandard1.6` and you attempt to install a package that contains DLLs in only the `lib\net20` and `\lib\net45` folders, then you see messages like the following for the package and possibly its dependents:</span></span>

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

<span data-ttu-id="1eb48-195">Для устранения этих проблем совместимости выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="1eb48-195">To resolve incompatibilities, do one of the following:</span></span>

- <span data-ttu-id="1eb48-196">Переориентируйте проект на платформу, которая поддерживается нужными вам пакетами.</span><span class="sxs-lookup"><span data-stu-id="1eb48-196">Retarget your project to a framework that is supported by the packages you want to use.</span></span>
- <span data-ttu-id="1eb48-197">Обратитесь к автору пакетов и помогите ему добавить поддержку для выбранной вами платформы.</span><span class="sxs-lookup"><span data-stu-id="1eb48-197">Contact the author of the packages and work with them to add support for your chosen framework.</span></span> <span data-ttu-id="1eb48-198">Для этого на каждой странице с описанием пакета на сайте [nuget.org](https://www.nuget.org/) предусмотрена ссылка **Contact Owners** (Связаться с владельцами).</span><span class="sxs-lookup"><span data-stu-id="1eb48-198">Each package listing page on [nuget.org](https://www.nuget.org/) has a **Contact Owners** link for this purpose.</span></span>
