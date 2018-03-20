---
title: "Вопросы и ответы | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/11/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Вопросы и ответы по использованию NuGet в командной строке и в Visual Studio, а также по работе с коллекцией NuGet."
keywords: "вопросы и ответы по NuGet, вопросы и ответы, распространенные проблемы, версии NuGet, версии пакетов"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3782fe5dcf8df002d99446aa7548a6eacc62211c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="8b207-104">Вопросы и ответы по NuGet</span><span class="sxs-lookup"><span data-stu-id="8b207-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="8b207-105">**Что необходимо для запуска NuGet?**</span><span class="sxs-lookup"><span data-stu-id="8b207-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="8b207-106">Все данные по пользовательскому интерфейсу и средствам командной строки доступны в [руководстве по установке](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="8b207-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="8b207-107">**Поддерживает ли NuGet Mono?**</span><span class="sxs-lookup"><span data-stu-id="8b207-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="8b207-108">Средство командной строки `nuget.exe` выполняет построение и запускается с помощью Mono 3.2 или более поздней версии и поддерживает создание пакетов в Mono.</span><span class="sxs-lookup"><span data-stu-id="8b207-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="8b207-109">Несмотря на то, что `nuget.exe` полностью работает в Windows, в Linux и OS X существуют известные проблемы. См. раздел GitHub, посвященный [проблемам с Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono).</span><span class="sxs-lookup"><span data-stu-id="8b207-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="8b207-110">[Графический клиент](https://github.com/mrward/monodevelop-nuget-addin) доступен в виде надстройки для MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="8b207-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="8b207-111">**Как можно определить, что содержит пакет, и является ли он стабильным и полезным для моего приложения?**</span><span class="sxs-lookup"><span data-stu-id="8b207-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="8b207-112">Основным источником информации о пакете является его страница сведений на веб-сайте nuget.org (или в другом закрытом веб-канале).</span><span class="sxs-lookup"><span data-stu-id="8b207-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="8b207-113">На странице каждого пакета на веб-сайте nuget.org приводится описание проекта, история его версий и статистика использования.</span><span class="sxs-lookup"><span data-stu-id="8b207-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="8b207-114">В разделе **Сведения** на странице пакета также приводится ссылка на веб-сайт проекта, где обычно можно найти много примеров и других документов, с помощью которых можно оценить полезность пакета.</span><span class="sxs-lookup"><span data-stu-id="8b207-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="8b207-115">Дополнительные сведения см. в разделе [Поиск и выбор пакетов](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="8b207-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="8b207-116">NuGet в среде Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8b207-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="8b207-117">**Каким образом обеспечивается поддержка NuGet в различных продуктах Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="8b207-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="8b207-118">Visual Studio для Windows поддерживает [пользовательский интерфейс диспетчера пакетов](../tools/package-manager-ui.md) и [консоль диспетчера пакетов](../tools/package-manager-console.md).</span><span class="sxs-lookup"><span data-stu-id="8b207-118">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="8b207-119">Visual Studio для Mac реализует встроенные возможности NuGet, которые описываются в разделе [Включение пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="8b207-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="8b207-120">Visual Studio Code для всех платформ не поддерживает прямую интеграцию с NuGet.</span><span class="sxs-lookup"><span data-stu-id="8b207-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="8b207-121">Используйте [интерфейс командной строки NuGet](../tools/nuget-exe-cli-reference.md) или [интерфейс командной строки dotnet](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="8b207-121">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="8b207-122">Visual Studio Team Services реализует [шаг построения для восстановления пакетов NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="8b207-122">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="8b207-123">Также вы можете [разместить закрытые веб-каналы NuGet в Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="8b207-123">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="8b207-124">**Как определить точную версию устанавливаемых средств NuGet?**</span><span class="sxs-lookup"><span data-stu-id="8b207-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="8b207-125">В Visual Studio выберите **Справка > О Microsoft Visual Studio** и проверьте версию компонента **Диспетчер пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8b207-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="8b207-126">Также можно запустить консоль диспетчера пакетов (**Сервис > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**) и ввести `$host`, чтобы просмотреть сведения о версии NuGet и другую информацию.</span><span class="sxs-lookup"><span data-stu-id="8b207-126">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="8b207-127">**Какие языки программирования поддерживает NuGet?**</span><span class="sxs-lookup"><span data-stu-id="8b207-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="8b207-128">NuGet обычно работает с языками платформы .NET и предназначен для использования библиотек .NET в проекте.</span><span class="sxs-lookup"><span data-stu-id="8b207-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="8b207-129">Поскольку для проектов некоторых типов также поддерживаются средства автоматизации MSBuild и Visual Studio, в определенной степени также поддерживаются другие проекты и языки.</span><span class="sxs-lookup"><span data-stu-id="8b207-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="8b207-130">Последняя версия NuGet поддерживает C#, Visual Basic, F#, WiX и C++.</span><span class="sxs-lookup"><span data-stu-id="8b207-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="8b207-131">**Какие шаблоны проектов поддерживает NuGet?**</span><span class="sxs-lookup"><span data-stu-id="8b207-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="8b207-132">NuGet обеспечивает полную поддержку множества шаблонов проектов, включая Windows, Интернет, облако, SharePoint, Wix и другие.</span><span class="sxs-lookup"><span data-stu-id="8b207-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="8b207-133">**Как обновить пакеты, которые являются частью шаблонов Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="8b207-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="8b207-134">Перейдите на вкладку **Обновления** в пользовательском интерфейсе диспетчера проектов и выберите **Обновить все** или воспользуйтесь [командой `Update-Package`](../tools/ps-ref-update-package.md) в консоли диспетчера проектов.</span><span class="sxs-lookup"><span data-stu-id="8b207-134">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="8b207-135">Чтобы обновить сам шаблон, необходимо вручную обновить репозиторий шаблонов.</span><span class="sxs-lookup"><span data-stu-id="8b207-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="8b207-136">Дополнительные сведения по этой теме см. в [блоге Ксавье Декостера (Xavier Decoster)](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages).</span><span class="sxs-lookup"><span data-stu-id="8b207-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="8b207-137">Обратите внимание, что все это вы делаете на свой страх и риск, поскольку ручное обновление может привести к повреждению шаблона в том случае, если последние версии всех зависимостей несовместимы друг с другом.</span><span class="sxs-lookup"><span data-stu-id="8b207-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="8b207-138">**Можно ли использовать NuGet вне среды Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="8b207-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="8b207-139">Да. NuGet работает непосредственно из командной строки.</span><span class="sxs-lookup"><span data-stu-id="8b207-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="8b207-140">См. [руководство по установке](../install-nuget-client-tools.md) и [справочник по интерфейсу командной строки](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8b207-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="8b207-141">Командная строка NuGet</span><span class="sxs-lookup"><span data-stu-id="8b207-141">NuGet command line</span></span>

<span data-ttu-id="8b207-142">**Как получить последнюю версию средства командной строки NuGet?**</span><span class="sxs-lookup"><span data-stu-id="8b207-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="8b207-143">См. [руководство по установке](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="8b207-143">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="8b207-144">**Для чего нужна лицензия на веб-сайте nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="8b207-144">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="8b207-145">Вы можете распространить nuget.exe в соответствии с условиями лицензии MIT.</span><span class="sxs-lookup"><span data-stu-id="8b207-145">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="8b207-146">Вы несете ответственность за обновление и обслуживание всех распространяемых вами копий nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="8b207-146">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="8b207-147">**Можно ли расширить возможности средства командной строки NuGet?**</span><span class="sxs-lookup"><span data-stu-id="8b207-147">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="8b207-148">Да. Вы можете добавлять в `nuget.exe` собственные команды, как описывается в [статье Роба Рейнолда (Rob Reynold)](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b207-148">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="8b207-149">Консоль диспетчера пакетов NuGet (Visual Studio для Windows)</span><span class="sxs-lookup"><span data-stu-id="8b207-149">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="8b207-150">**Как получить доступ к объекту DTE в консоли диспетчера пакетов?**</span><span class="sxs-lookup"><span data-stu-id="8b207-150">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="8b207-151">Объект верхнего уровня в объектной модели автоматизации Visual Studio называется объектом DTE (среда средств разработки).</span><span class="sxs-lookup"><span data-stu-id="8b207-151">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="8b207-152">Этот объект предоставляется консолью с помощью переменной `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="8b207-152">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="8b207-153">Дополнительные сведения см. в разделе [Общие сведения о модели автоматизации](/visualstudio/extensibility/internals/automation-model-overview) в документации по расширению среды Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b207-153">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="8b207-154">**При попытке привести переменную $DTE к типу DTE2 возникает ошибка: "Не удается преобразовать значение "EnvDTE.DTEClass" типа "EnvDTE.DTEClass" в тип "EnvDTE80.DTE2"". В чем проблема?**</span><span class="sxs-lookup"><span data-stu-id="8b207-154">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="8b207-155">Это известная проблема, связанная с взаимодействием PowerShell с COM-объектом.</span><span class="sxs-lookup"><span data-stu-id="8b207-155">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="8b207-156">Попробуйте выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8b207-156">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="8b207-157">`Get-Interface` — это вспомогательная функция, добавляемая узлом PowerShell NuGet.</span><span class="sxs-lookup"><span data-stu-id="8b207-157">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="8b207-158">Создание и публикация пакетов</span><span class="sxs-lookup"><span data-stu-id="8b207-158">Creating and publishing packages</span></span>

<span data-ttu-id="8b207-159">**Как включить мой пакет в веб-канал?**</span><span class="sxs-lookup"><span data-stu-id="8b207-159">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="8b207-160">См. раздел [Создание и публикация пакетов](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="8b207-160">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="8b207-161">**У меня есть несколько версий библиотеки, предназначенных для различных версий платформы .NET Framework. Как построить единый пакет, поддерживающий такую реализацию?**</span><span class="sxs-lookup"><span data-stu-id="8b207-161">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="8b207-162">См. раздел [Поддержка нескольких версий и профилей платформы .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="8b207-162">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="8b207-163">**Как настроить свой собственный репозиторий или веб-канал?**</span><span class="sxs-lookup"><span data-stu-id="8b207-163">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="8b207-164">См. раздел [Общие сведения о размещении пакетов](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="8b207-164">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="8b207-165">**Как выполнить массовую загрузку пакетов в мой веб-канал NuGet?**</span><span class="sxs-lookup"><span data-stu-id="8b207-165">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="8b207-166">См. раздел [Массовая публикация пакетов NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="8b207-166">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="8b207-167">Работа с пакетами</span><span class="sxs-lookup"><span data-stu-id="8b207-167">Working with packages</span></span>

<span data-ttu-id="8b207-168">**В чем разница между пакетами уровня проекта и уровня решения?**</span><span class="sxs-lookup"><span data-stu-id="8b207-168">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="8b207-169">Пакет уровня решения (NuGet версии 3.x или более поздней) устанавливается в решении только один раз и после этого доступен для всех проектов решения.</span><span class="sxs-lookup"><span data-stu-id="8b207-169">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="8b207-170">Пакет уровня проекта устанавливается в каждом проекте, который его использует.</span><span class="sxs-lookup"><span data-stu-id="8b207-170">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="8b207-171">Пакет уровня решения также может устанавливать новые команды, которые могут вызываться из консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="8b207-171">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="8b207-172">**Можно ли устанавливать пакеты NuGet без подключения к Интернету?**</span><span class="sxs-lookup"><span data-stu-id="8b207-172">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="8b207-173">Да. См. статью блога Скотта Ханселмана (Scott Hanselman), посвященную [доступу к NuGet при неработающем веб-сайте nuget.org или во время полета на самолете](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="8b207-173">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="8b207-174">**Можно ли устанавливать пакеты в папку, отличную от заданной по умолчанию?**</span><span class="sxs-lookup"><span data-stu-id="8b207-174">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="8b207-175">Задайте параметр [`repositoryPath`](../reference/nuget-config-file.md#config-section) в файле `Nuget.Config`, используя `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="8b207-175">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="8b207-176">**Как избежать добавления папки пакетов NuGet в систему управления версиями?**</span><span class="sxs-lookup"><span data-stu-id="8b207-176">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="8b207-177">Присвойте свойству [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) в файле `Nuget.Config` значение `true`.</span><span class="sxs-lookup"><span data-stu-id="8b207-177">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="8b207-178">Этот ключ работает на уровне решения и поэтому должен добавляться в файл `$(Solutiondir)\.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="8b207-178">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="8b207-179">Если включить восстановление пакета из Visual Studio, этот файл будет создан автоматически.</span><span class="sxs-lookup"><span data-stu-id="8b207-179">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="8b207-180">**Как отключить восстановление пакетов?**</span><span class="sxs-lookup"><span data-stu-id="8b207-180">**How do I turn off package restore?**</span></span>

<span data-ttu-id="8b207-181">См. раздел [Включение и отключение восстановления пакетов](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="8b207-181">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="8b207-182">**Почему при установке локального пакета с удаленными зависимостями возникает ошибка "Не удается разрешить зависимость"?**</span><span class="sxs-lookup"><span data-stu-id="8b207-182">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="8b207-183">При установке локального пакета в проект выберите источник **Все**.</span><span class="sxs-lookup"><span data-stu-id="8b207-183">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="8b207-184">При этом вместо использования одного веб-канала будут объединены все веб-каналы.</span><span class="sxs-lookup"><span data-stu-id="8b207-184">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="8b207-185">Причиной этой ошибки обычно является то, что пользователи локального репозитория часто стремятся избежать случайной установки удаленного пакета из-за требований корпоративной политики.</span><span class="sxs-lookup"><span data-stu-id="8b207-185">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="8b207-186">**У меня есть несколько проектов, расположенных в одной папке. Как использовать отдельные файлы packages.config для каждого проекта?**</span><span class="sxs-lookup"><span data-stu-id="8b207-186">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="8b207-187">В большинстве случаев, когда отдельные проекты располагаются в отдельных папках, это не проблема, поскольку NuGet идентифицирует файлы `packages.config` в каждом проекте.</span><span class="sxs-lookup"><span data-stu-id="8b207-187">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="8b207-188">Если вы работаете с NuGet версии 3.3 или более поздней и размещаете несколько проектов в одной папке, вы можете вставить имя проекта в имена файлов `packages.config`, используя шаблон `packages.{project-name}.config`. NuGet будет использовать этот файл.</span><span class="sxs-lookup"><span data-stu-id="8b207-188">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="8b207-189">Это также не проблема при использовании PackageReference, поскольку каждый файл проекта содержит собственный список зависимостей.</span><span class="sxs-lookup"><span data-stu-id="8b207-189">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="8b207-190">**Я не вижу nuget.org в списке репозиториев. Как вернуть его?**</span><span class="sxs-lookup"><span data-stu-id="8b207-190">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="8b207-191">Добавьте `https://api.nuget.org/v3/index.json` в список источников или</span><span class="sxs-lookup"><span data-stu-id="8b207-191">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="8b207-192">Удалите файл `%appdata%\.nuget\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) и дождитесь, пока NuGet снова создаст его.</span><span class="sxs-lookup"><span data-stu-id="8b207-192">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>

<span data-ttu-id="8b207-193">**Какие условия лицензирования применяются по умолчанию, если для пакета не указаны никакие сведения о лицензии?**</span><span class="sxs-lookup"><span data-stu-id="8b207-193">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="8b207-194">В отношении каждого пакета действуют входящие в него условия.</span><span class="sxs-lookup"><span data-stu-id="8b207-194">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="8b207-195">Прежде чем получать доступ к пакетам, скачивать или получать их, необходимо ознакомиться с соответствующими условиями.</span><span class="sxs-lookup"><span data-stu-id="8b207-195">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="8b207-196">Воспользуйтесь ссылкой **Сведения о лицензии** на странице пакета на веб-сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8b207-196">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="8b207-197">Если для пакета не заданы условия лицензии, следует обратиться непосредственно к владельцу пакета **по ссылке для связи с владельцем** на странице пакета на веб-сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8b207-197">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="8b207-198">Корпорация Майкрософт не предоставляет вам лицензию на какую-либо интеллектуальную собственность сторонних поставщиков пакетов и не несет ответственность за сведения, предоставляемые третьими лицами.</span><span class="sxs-lookup"><span data-stu-id="8b207-198">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="8b207-199">Управление владельцами пакетов на веб-сайте nuget.org</span><span class="sxs-lookup"><span data-stu-id="8b207-199">Managing packages on nuget.org</span></span>

<span data-ttu-id="8b207-200">**Можно ли изменить метаданные пакета после его загрузки? Почему для изменений метаданных пакета требуется редактировать файл nuspec и отправлять новый пакет?**</span><span class="sxs-lookup"><span data-stu-id="8b207-200">**Can I edit package metadata after it's been uploaded? Why do you require editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="8b207-201">NuGet требует, чтобы все пакеты были подписаны.</span><span class="sxs-lookup"><span data-stu-id="8b207-201">NuGet requires all packages to be signed.</span></span> <span data-ttu-id="8b207-202">Основополагающим принципом подписывания является то, что содержимое подписанного пакета, включая файл nuspec, является неизменным.</span><span class="sxs-lookup"><span data-stu-id="8b207-202">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="8b207-203">При редактировании метаданных пакета изменяется файл nuspec, в результате чего существующие подписи становятся недействительными.</span><span class="sxs-lookup"><span data-stu-id="8b207-203">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="8b207-204">Мы рекомендуем изменить существующие рабочие процессы таким образом, чтобы после создания пакета не требовалось редактирование его метаданных.</span><span class="sxs-lookup"><span data-stu-id="8b207-204">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="8b207-205">Обратите внимание, что перечисленные в пакете зависимости создаются автоматически на основании самого пакета и не могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="8b207-205">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="8b207-206">Кроме того, загрузка пакета на веб-сайт [staging.nuget.org](http://staging.nuget.org) позволяет легко протестировать и проверить пакет, не публикуя его в общедоступной коллекции.</span><span class="sxs-lookup"><span data-stu-id="8b207-206">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="8b207-207">**Можно ли зарезервировать имена для пакетов, которые будут опубликованы в будущем?**</span><span class="sxs-lookup"><span data-stu-id="8b207-207">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="8b207-208">Да.</span><span class="sxs-lookup"><span data-stu-id="8b207-208">Yes.</span></span> <span data-ttu-id="8b207-209">Вы можете зарезервировать идентификаторы пакетов на веб-сайте [nuget.org](https://www.nuget.org/), запросив префикс идентификатора пакета для своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="8b207-209">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="8b207-210">Чтобы запросить префикс идентификатора пакета, следуйте инструкциям в [документации](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span><span class="sxs-lookup"><span data-stu-id="8b207-210">In order to request a package ID prefix, follow the instructions in the [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="8b207-211">**Как заявить о правах владельца пакетов?**</span><span class="sxs-lookup"><span data-stu-id="8b207-211">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="8b207-212">См. раздел [Управление владельцами пакетов на веб-сайте nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="8b207-212">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="8b207-213">**Что делать с владельцем пакета, который нарушает условия лицензии на мое программное обеспечение?**</span><span class="sxs-lookup"><span data-stu-id="8b207-213">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="8b207-214">В рамках сообщества NuGet мы пропагандируем тесное сотрудничество по вопросам разрешения любых разногласий, которые могут возникать между владельцами пакетов и другого программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="8b207-214">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="8b207-215">Прежде чем обращаться к администраторам nuget.org, мы рекомендуем воспользоваться [процессом разрешения споров](../policies/dispute-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="8b207-215">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="8b207-216">**Рекомендуется ли загружать тестовые пакеты на веб-сайт nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="8b207-216">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="8b207-217">В целях тестирования вы можете использовать веб-сайт [staging.nuget.org](http://staging.nuget.org) или альтернативные общедоступные серверы NuGet, такие как [myget.org](https://myget.org) или [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="8b207-217">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="8b207-218">Обратите внимание, что загруженные на веб-сайт staging.nuget.org пакеты могут не сохраняться.</span><span class="sxs-lookup"><span data-stu-id="8b207-218">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="8b207-219">См. раздел [Прощание с предварительной версией](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="8b207-219">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="8b207-220">**Каков максимальный размер пакетов, загружаемых на веб-сайт nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="8b207-220">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="8b207-221">На веб-сайт nuget.org можно загружать пакеты размером до 250 МБ, однако мы рекомендуем по возможности не создавать пакеты размером более 1 МБ и использовать зависимости для установления связей между пакетами.</span><span class="sxs-lookup"><span data-stu-id="8b207-221">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="8b207-222">Чтобы избежать конфликтов, рекомендуется включать в пакет только одну сборку.</span><span class="sxs-lookup"><span data-stu-id="8b207-222">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="8b207-223">NuGet использует для скачивания пакетов протокол HTTP, поэтому для крупных пакетов повышается вероятность сбоев при установке.</span><span class="sxs-lookup"><span data-stu-id="8b207-223">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="8b207-224">Вы можете использовать общие зависимости между несколькими пакетами, уменьшая общий размер скачиваемых клиентами пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="8b207-224">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="8b207-225">В большинстве случаев зависимости являются статическими и никогда не изменяются.</span><span class="sxs-lookup"><span data-stu-id="8b207-225">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="8b207-226">При исправлении ошибок в коде обновление зависимостей может не требоваться.</span><span class="sxs-lookup"><span data-stu-id="8b207-226">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="8b207-227">Если вы объединяете зависимости в пакет, в конечном итоге вам придется каждый раз выполнять повторную доставку пакетов большого размера.</span><span class="sxs-lookup"><span data-stu-id="8b207-227">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="8b207-228">Разбивая пакеты NuGet на взаимосвязанные зависимости, вы реализуете более детализированный процесс обновления пакетов для клиентов.</span><span class="sxs-lookup"><span data-stu-id="8b207-228">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="8b207-229">Отсутствие доступа к nuget.org</span><span class="sxs-lookup"><span data-stu-id="8b207-229">nuget.org not accessible</span></span>

<span data-ttu-id="8b207-230">**Почему я не могу скачать пакеты с веб-сайта nuget.org или загрузить их на него?**</span><span class="sxs-lookup"><span data-stu-id="8b207-230">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="8b207-231">Во-первых, убедитесь, что вы используете последние версии NuGet.</span><span class="sxs-lookup"><span data-stu-id="8b207-231">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="8b207-232">Если при работе такой версии продолжают возникать ошибки, [обратитесь в службу поддержки](https://www.nuget.org/policies/Contact) и предоставьте нам дополнительные сведения для устранения неполадок, в том числе следующие:</span><span class="sxs-lookup"><span data-stu-id="8b207-232">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="8b207-233">Версия NuGet, которую вы используете</span><span class="sxs-lookup"><span data-stu-id="8b207-233">The version of NuGet you're using</span></span>
- <span data-ttu-id="8b207-234">Источники пакетов, которые вы используете</span><span class="sxs-lookup"><span data-stu-id="8b207-234">The package sources you're using</span></span>
- <span data-ttu-id="8b207-235">Журнал восстановления с подробным уровнем детализации</span><span class="sxs-lookup"><span data-stu-id="8b207-235">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="8b207-236">Данные трассировки MTR или Fiddler (см. ниже)</span><span class="sxs-lookup"><span data-stu-id="8b207-236">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="8b207-237">Ваш географический регион</span><span class="sxs-lookup"><span data-stu-id="8b207-237">Your geographical area</span></span>
- <span data-ttu-id="8b207-238">Версия вашей операционной системы</span><span class="sxs-lookup"><span data-stu-id="8b207-238">Your operating system version</span></span>
- <span data-ttu-id="8b207-239">Конфигурация компьютера (ЦП, сетевые компоненты, жесткий диск)</span><span class="sxs-lookup"><span data-stu-id="8b207-239">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="8b207-240">Сведения об установке компьютера за прокси-сервером или брандмауэром</span><span class="sxs-lookup"><span data-stu-id="8b207-240">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="8b207-241">Установленные на компьютере версии платформы .NET</span><span class="sxs-lookup"><span data-stu-id="8b207-241">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="8b207-242">Версии кроссплатформенных средств, таких как интерфейс командной строки .NET или DNU, которые вы используете</span><span class="sxs-lookup"><span data-stu-id="8b207-242">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="8b207-243">*Получение трассировки MTR:*</span><span class="sxs-lookup"><span data-stu-id="8b207-243">*To capture MTR:*</span></span>

- <span data-ttu-id="8b207-244">Скачайте WinMTR из [http://winmtr.net/download/](http://winmtr.net/).</span><span class="sxs-lookup"><span data-stu-id="8b207-244">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="8b207-245">Введите имя узла `api.nuget.org` и щелкните **Пуск**.</span><span class="sxs-lookup"><span data-stu-id="8b207-245">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="8b207-246">Дождитесь, пока значение в столбце **Отправлено** превысит 100.</span><span class="sxs-lookup"><span data-stu-id="8b207-246">Wait until the **Sent** column is >= 100.</span></span>

    ![Получение трассировки MTR](media/mtr.png)

- <span data-ttu-id="8b207-248">Скопируйте текст в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="8b207-248">Copy text to clipboard.</span></span>

<span data-ttu-id="8b207-249">*Получение трассировки Fiddler:*</span><span class="sxs-lookup"><span data-stu-id="8b207-249">*To capture Fiddler:*</span></span>

- <span data-ttu-id="8b207-250">Установите последнюю версию [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="8b207-250">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="8b207-251">Запустите Fiddler и отключите запись трафика в меню **Файл > Запись трафика**.</span><span class="sxs-lookup"><span data-stu-id="8b207-251">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="8b207-252">Удалите все сеансы (выделите все элементы в списке и нажмите клавишу **Delete**).</span><span class="sxs-lookup"><span data-stu-id="8b207-252">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="8b207-253">Настройте Fiddler для записи трафика HTTPS, установив флажок **Расшифровывать трафик HTTPS** на вкладке **HTTPS** в меню **Сервис > Параметры Fiddler...**</span><span class="sxs-lookup"><span data-stu-id="8b207-253">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="8b207-254">Закройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8b207-254">Close Visual Studio.</span></span>
- <span data-ttu-id="8b207-255">Включите меню **Файл > Запись трафика**.</span><span class="sxs-lookup"><span data-stu-id="8b207-255">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="8b207-256">Запустите исполняемый файл Visual Studio или nuget.exe и выполните действия, которые не получились ранее.</span><span class="sxs-lookup"><span data-stu-id="8b207-256">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="8b207-257">Трафик, сформированный этими действиями, будет показан в Fiddler.</span><span class="sxs-lookup"><span data-stu-id="8b207-257">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="8b207-258">После выполнения нужных действий выберите **Файл > Сохранить > Все сеансы**, чтобы сохранить записанные сеансы.</span><span class="sxs-lookup"><span data-stu-id="8b207-258">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="8b207-259">Примечание. Для маршрутизации трафика NuGet через Fiddler может потребоваться присвоить переменной среды `HTTP_PROXY` значение `http://127.0.0.1:8888`.</span><span class="sxs-lookup"><span data-stu-id="8b207-259">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="8b207-260">Если этот способ не помогает, попробуйте советы, приведенные в этой [статье на веб-сайте StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="8b207-260">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="8b207-261">**Каковы конечные точки API для nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="8b207-261">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="8b207-262">Версия 3: `https://api.nuget.org/v3/index.json` Версия 2: `https://www.nuget.org/api/v2/` (Обратите внимание, что все API версии 2 не рекомендуются к использованию и не работают с NuGet 4 или более поздних версий.)</span><span class="sxs-lookup"><span data-stu-id="8b207-262">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
