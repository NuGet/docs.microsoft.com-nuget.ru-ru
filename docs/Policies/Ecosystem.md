---
title: "Общие сведения об экосистеме NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 8971dcf5-1d05-46e1-adf2-ce0f55521a49
description: "Полноценный набор ресурсов в экосистеме NuGet, включая источники NuGet, проекты NuGet сторонних поставщиков, служебные программы и учебные материалы."
keywords: "экосистема NuGet, проекты NuGet сторонних поставщиков, открытый исходный код NuGet, служебные программы NuGet, учебные материалы NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: de64cf96595825b7c1bf2e235e370f5a95c64096
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="an-overview-of-the-nuget-ecosystem"></a><span data-ttu-id="edd65-104">Общие сведения об экосистеме NuGet</span><span class="sxs-lookup"><span data-stu-id="edd65-104">An overview of the NuGet ecosystem</span></span>

<span data-ttu-id="edd65-105">С момента своего появления в 2010 году NuGet позволил значительно улучшить и автоматизировать различные аспекты процессов разработки.</span><span class="sxs-lookup"><span data-stu-id="edd65-105">Since it's introduction in 2010, NuGet has presented a great opportunity to improve and automate different aspects of the development processes.</span></span>

<span data-ttu-id="edd65-106">Так как NuGet представляет собой проект с открытым исходным кодом, регулируемый [свободной лицензией Apache версии 2](http://choosealicense.com/licenses/apache/), он может использоваться в других проектах, а организации могут реализовывать его поддержку в своих продуктах.</span><span class="sxs-lookup"><span data-stu-id="edd65-106">Because NuGet is open source under a permissive [Apache v2 license](http://choosealicense.com/licenses/apache/), other projects can leverage NuGet and companies can build support for it in their products.</span></span> <span data-ttu-id="edd65-107">Как для проектов с открытым кодом, так и для разработки корпоративных приложений NuGet и другие основанные на нем приложения предоставляют обширную экосистему средств для улучшения процесса разработки программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="edd65-107">Whether for open-source projects or enterprise application development, NuGet and other applications built on and around NuGet provide a broad ecosystem of tools for improving your software development process.</span></span>

<span data-ttu-id="edd65-108">Все эти проекты продвигаются вперед благодаря вкладу разработчиков.</span><span class="sxs-lookup"><span data-stu-id="edd65-108">All of these projects are able to innovate because of developer contributions.</span></span> <span data-ttu-id="edd65-109">Если вы работаете над NuGet, внесите вклад и в эти проекты, по мере возможности сообщая о дефектах, делясь идеями по улучшению продукта, оставляя отзывы, составляя документацию и дополняя код.</span><span class="sxs-lookup"><span data-stu-id="edd65-109">Just as you contribute to NuGet itself, also make contribution to these projects by reporting defects and new feature ideas, providing feedback, writing documentation, and contributing code where possible.</span></span>

## <a name="net-foundation-projects"></a><span data-ttu-id="edd65-110">Проекты .NET Foundation</span><span class="sxs-lookup"><span data-stu-id="edd65-110">.NET Foundation projects</span></span>

<span data-ttu-id="edd65-111">NuGet предоставляет бесплатную систему управления пакетами с открытым исходным кодом для платформы разработки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="edd65-111">NuGet provides a free, open source package management system for the Microsoft development platform.</span></span> <span data-ttu-id="edd65-112">Она состоит из нескольких клиентских средств, а также набора служб, составляющих [официальную коллекцию NuGet](http://www.nuget.org).</span><span class="sxs-lookup"><span data-stu-id="edd65-112">It consists of a few client tools as well as the set of services that comprise the [official NuGet Gallery](http://www.nuget.org).</span></span> <span data-ttu-id="edd65-113">Вместе они образуют проект NuGet, управляемый [.NET Foundation](http://www.dotnetfoundation.org/).</span><span class="sxs-lookup"><span data-stu-id="edd65-113">Combined, these form the NuGet project which is governed by the [.NET Foundation](http://www.dotnetfoundation.org/).</span></span>

<span data-ttu-id="edd65-114">Организация NuGet имеет различные репозитории на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="edd65-114">The NuGet Organization contains various repositories on GitHub.</span></span> <span data-ttu-id="edd65-115">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) предоставляет общие сведения о всех репозиториях и том, где можно найти различные компоненты NuGet.</span><span class="sxs-lookup"><span data-stu-id="edd65-115">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) gives an overview of all the repositories and where to find the various NuGet components.</span></span>

## <a name="microsoft-projects"></a><span data-ttu-id="edd65-116">Проекты Майкрософт</span><span class="sxs-lookup"><span data-stu-id="edd65-116">Microsoft projects</span></span>

<span data-ttu-id="edd65-117">Корпорация Майкрософт внесла значительный вклад в разработку NuGet.</span><span class="sxs-lookup"><span data-stu-id="edd65-117">Microsoft has contributed extensively to the development of NuGet.</span></span> <span data-ttu-id="edd65-118">Все внесенные сотрудниками корпорации Майкрософт дополнения также имеют открытый исходный код и переданы в дар (включая авторские права) .NET Foundation.</span><span class="sxs-lookup"><span data-stu-id="edd65-118">All contributions made by Microsoft employees are also open source and are donated (including copyrights) to the .NET Foundation.</span></span>

## <a name="non-microsoft-projects"></a><span data-ttu-id="edd65-119">Сторонние проекты</span><span class="sxs-lookup"><span data-stu-id="edd65-119">Non-Microsoft projects</span></span>

<span data-ttu-id="edd65-120">Значительный вклад в экосистему NuGet внесли многие люди и организации.</span><span class="sxs-lookup"><span data-stu-id="edd65-120">Many other individuals and companies have made significant contributions to the NuGet ecosystem.</span></span> <span data-ttu-id="edd65-121">Каждый из перечисленных здесь проектов может иметь не такие условия лицензии, как основные компоненты NuGet, поэтому перед использованием убедитесь, что эти условия приемлемы для вас:</span><span class="sxs-lookup"><span data-stu-id="edd65-121">Each project listed here may have a different license than the core NuGet components, so confirm that the license terms are acceptable prior to use:</span></span>

* [<span data-ttu-id="edd65-122">AppVeyor CI</span><span class="sxs-lookup"><span data-stu-id="edd65-122">AppVeyor CI</span></span>](https://www.appveyor.com/)
* [<span data-ttu-id="edd65-123">Artifactory</span><span class="sxs-lookup"><span data-stu-id="edd65-123">Artifactory</span></span>](https://www.jfrog.com/artifactory/)
* [<span data-ttu-id="edd65-124">BoxStarter</span><span class="sxs-lookup"><span data-stu-id="edd65-124">BoxStarter</span></span>](http://boxstarter.org/)
* [<span data-ttu-id="edd65-125">Chocolatey</span><span class="sxs-lookup"><span data-stu-id="edd65-125">Chocolatey</span></span>](https://chocolatey.org/)
* [<span data-ttu-id="edd65-126">CoApp</span><span class="sxs-lookup"><span data-stu-id="edd65-126">CoApp</span></span>](http://coapp.org/)
* [<span data-ttu-id="edd65-127">JetBrains ReSharper</span><span class="sxs-lookup"><span data-stu-id="edd65-127">JetBrains ReSharper</span></span>](https://resharper-plugins.jetbrains.com/)
* [<span data-ttu-id="edd65-128">JetBrains TeamCity</span><span class="sxs-lookup"><span data-stu-id="edd65-128">JetBrains TeamCity</span></span>](https://www.jetbrains.com/teamcity/)
* [<span data-ttu-id="edd65-129">Klondike</span><span class="sxs-lookup"><span data-stu-id="edd65-129">Klondike</span></span>](https://github.com/themotleyfool/Klondike)
* [<span data-ttu-id="edd65-130">MinimalNugetServer</span><span class="sxs-lookup"><span data-stu-id="edd65-130">MinimalNugetServer</span></span>](https://github.com/TanukiSharp/MinimalNugetServer)
* [<span data-ttu-id="edd65-131">MyGet (или NuGet-as-a-service)</span><span class="sxs-lookup"><span data-stu-id="edd65-131">MyGet (or NuGet-as-a-service)</span></span>](http://www.myget.org/)
* [<span data-ttu-id="edd65-132">NuGet Package Explorer</span><span class="sxs-lookup"><span data-stu-id="edd65-132">NuGet Package Explorer</span></span>](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
* [<span data-ttu-id="edd65-133">NuGet Server</span><span class="sxs-lookup"><span data-stu-id="edd65-133">NuGet Server</span></span>](http://nugetserver.net/)
* [<span data-ttu-id="edd65-134">OctopusDeploy</span><span class="sxs-lookup"><span data-stu-id="edd65-134">OctopusDeploy</span></span>](https://octopus.com/)
* [<span data-ttu-id="edd65-135">Paket</span><span class="sxs-lookup"><span data-stu-id="edd65-135">Paket</span></span>](https://fsprojects.github.io/Paket/)
* [<span data-ttu-id="edd65-136">ProGet (Inedo)</span><span class="sxs-lookup"><span data-stu-id="edd65-136">ProGet (Inedo)</span></span>](http://inedo.com/proget)
* [<span data-ttu-id="edd65-137">scriptcs</span><span class="sxs-lookup"><span data-stu-id="edd65-137">scriptcs</span></span>](http://scriptcs.net/)
* [<span data-ttu-id="edd65-138">SharpDevelop</span><span class="sxs-lookup"><span data-stu-id="edd65-138">SharpDevelop</span></span>](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
* [<span data-ttu-id="edd65-139">Sonatype Nexus</span><span class="sxs-lookup"><span data-stu-id="edd65-139">Sonatype Nexus</span></span>](http://www.sonatype.com/nexus-repository-sonatype)
* [<span data-ttu-id="edd65-140">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="edd65-140">SymbolSource</span></span>](http://www.symbolsource.org/Public)
* [<span data-ttu-id="edd65-141">Xamarin и MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="edd65-141">Xamarin and MonoDevelop</span></span>](https://github.com/mrward/monodevelop-nuget-addin)


## <a name="other-nuget-based-utilities"></a><span data-ttu-id="edd65-142">Другие служебные программы на основе NuGet</span><span class="sxs-lookup"><span data-stu-id="edd65-142">Other NuGet-based utilities</span></span>

<span data-ttu-id="edd65-143">Эти средства и служебные программы основаны на NuGet:</span><span class="sxs-lookup"><span data-stu-id="edd65-143">These are tools and utilities built on NuGet:</span></span>

* <span data-ttu-id="edd65-144">[Glimpse Extensions](http://getglimpse.com/Packages) (подключаемые модули являются пакетами)</span><span class="sxs-lookup"><span data-stu-id="edd65-144">[Glimpse Extensions](http://getglimpse.com/Packages) (plug-ins are packages)</span></span>
* [<span data-ttu-id="edd65-145">NuGetMustHaves.com</span><span class="sxs-lookup"><span data-stu-id="edd65-145">NuGetMustHaves.com</span></span>](http://nugetmusthaves.com/)
* <span data-ttu-id="edd65-146">[Orchard](http://www.orchardproject.net/) (модули CMS получены из веб-канала NuGet версии v1, размещенного в коллекции Orchard Gallery)</span><span class="sxs-lookup"><span data-stu-id="edd65-146">[Orchard](http://www.orchardproject.net/) (CMS modules are fetched from a v1 NuGet feed hosted in the Orchard Gallery)</span></span>
* [<span data-ttu-id="edd65-147">Реализация сервера NuGet на языке Java</span><span class="sxs-lookup"><span data-stu-id="edd65-147">Java implementation of NuGet Server</span></span>](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
* <span data-ttu-id="edd65-148">[NuGetLatest](https://twitter.com/NuGetLatest) (бот в Twitter, публикующий данные о новых пакетах)</span><span class="sxs-lookup"><span data-stu-id="edd65-148">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting new package publications)</span></span>
* <span data-ttu-id="edd65-149">[DefinitelyTyped](http://definitelytyped.org/) ([автоматическая](https://github.com/DefinitelyTyped/NugetAutomation/) публикация определений типа TypeScript [в NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span><span class="sxs-lookup"><span data-stu-id="edd65-149">[DefinitelyTyped](http://definitelytyped.org/) ([Automatic](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [Definitions published to NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span></span>

## <a name="training-materials-and-references"></a><span data-ttu-id="edd65-150">Учебные материалы и справочники</span><span class="sxs-lookup"><span data-stu-id="edd65-150">Training materials and references</span></span>

<span data-ttu-id="edd65-151">Внедрение нового инструмента или технологии обычно требуют времени на изучение.</span><span class="sxs-lookup"><span data-stu-id="edd65-151">Using a new tool or technology usually comes with a learning curve.</span></span> <span data-ttu-id="edd65-152">К счастью, с NuGet дело обстоит совсем не так.</span><span class="sxs-lookup"><span data-stu-id="edd65-152">Luckily for you, NuGet has no steep learning curve it all!</span></span> <span data-ttu-id="edd65-153">Фактически, любой человек может быстро [приступить к использованию пакетов](../quickstart/use-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="edd65-153">In fact, anyone can [get started consuming packages](../quickstart/use-a-package.md) quickly.</span></span>

<span data-ttu-id="edd65-154">Однако для создания пакетов, особенно хорошего качества, с сопутствующим кодом NuGet в рамках автоматических процессов сборки и развертывания вам потребуется уделить немного больше времени изучению следующих ресурсов:</span><span class="sxs-lookup"><span data-stu-id="edd65-154">That said, authoring packages–and especially good packages–along with  embracing NuGet in automated build and deployment processes, requires spending a little more time with the following resources:</span></span>

- [<span data-ttu-id="edd65-155">Блог по NuGet</span><span class="sxs-lookup"><span data-stu-id="edd65-155">NuGet Blog</span></span>](http://blog.nuget.org/)
- [<span data-ttu-id="edd65-156">Команда разработчиков NuGet в Twitter, @nuget</span><span class="sxs-lookup"><span data-stu-id="edd65-156">NuGet team on Twitter, @nuget</span></span>](http://twitter.com/nuget)
- <span data-ttu-id="edd65-157">Книги:</span><span class="sxs-lookup"><span data-stu-id="edd65-157">Books:</span></span>
    * [<span data-ttu-id="edd65-158">Apress Pro NuGet</span><span class="sxs-lookup"><span data-stu-id="edd65-158">Apress Pro NuGet</span></span>](http://bit.ly/ProNuGet)
    * [<span data-ttu-id="edd65-159">NuGet 2 Essentials</span><span class="sxs-lookup"><span data-stu-id="edd65-159">NuGet 2 Essentials</span></span>](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a><span data-ttu-id="edd65-160">Документация для отдельных пакетов</span><span class="sxs-lookup"><span data-stu-id="edd65-160">Documentation for individual packages</span></span>

<span data-ttu-id="edd65-161">[NuDoq](http://nudoq.org) обеспечивает простой доступ, обновления и документацию для пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="edd65-161">[NuDoq](http://nudoq.org) provides straightforward access and updates and documentation for NuGet packages.</span></span>

<span data-ttu-id="edd65-162">NuDoq регулярно опрашивает сервер коллекции nuget.org на наличие последних обновлений пакетов, распаковывает и обрабатывает файлы документации библиотек и соответствующим образом обновляет сайт.</span><span class="sxs-lookup"><span data-stu-id="edd65-162">NuDoq regularly polls the nuget.org gallery server for the latest package updates, unpacks and processes the library documentation files, and updates the site accordingly.</span></span>

## <a name="adding-your-project"></a><span data-ttu-id="edd65-163">Добавление своего проекта</span><span class="sxs-lookup"><span data-stu-id="edd65-163">Adding your project</span></span>

<span data-ttu-id="edd65-164">Если у вас есть проект экосистемы NuGet, который может стать ценным дополнением для этой страницы, отправьте запрос на вытягивание с изменением на эту страницу.</span><span class="sxs-lookup"><span data-stu-id="edd65-164">If you have a NuGet ecosystem project that would be a valuable addition to this page, please  submit a pull request with an edit to this page.</span></span>
