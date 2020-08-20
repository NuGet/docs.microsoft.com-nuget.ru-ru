---
title: Вопросы и ответы по NuGet
description: Вопросы и ответы по использованию NuGet в командной строке и в Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 937a0083ca47ba5668059736a7e99f7ca88e8908
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622620"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="a358c-103">Вопросы и ответы по NuGet</span><span class="sxs-lookup"><span data-stu-id="a358c-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="a358c-104">Часто задаваемые вопросы, относящиеся к NuGet.org, например вопросы об учетных записях NuGet.org, см. в разделе [Вопросы и ответы по NuGet.org](../nuget-org/nuget-org-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a358c-104">For frequently-asked questions pertaining to NuGet.org, such as NuGet.org account questions, see [NuGet.org frequently-asked questions](../nuget-org/nuget-org-faq.md).</span></span>

<span data-ttu-id="a358c-105">**Что необходимо для запуска NuGet?**</span><span class="sxs-lookup"><span data-stu-id="a358c-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="a358c-106">Все данные по пользовательскому интерфейсу и средствам командной строки доступны в [руководстве по установке](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="a358c-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="a358c-107">**Поддерживает ли NuGet Mono?**</span><span class="sxs-lookup"><span data-stu-id="a358c-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="a358c-108">Средство командной строки `nuget.exe` выполняет построение и запускается с помощью Mono 3.2 или более поздней версии и поддерживает создание пакетов в Mono.</span><span class="sxs-lookup"><span data-stu-id="a358c-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="a358c-109">Несмотря на то, что `nuget.exe` полностью работает в Windows, в Linux и OS X существуют известные проблемы. См. раздел GitHub, посвященный [проблемам с Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono).</span><span class="sxs-lookup"><span data-stu-id="a358c-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="a358c-110">[Графический клиент](https://github.com/mrward/monodevelop-nuget-addin) доступен в виде надстройки для MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="a358c-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="a358c-111">**Как можно определить, что содержит пакет, и является ли он стабильным и полезным для моего приложения?**</span><span class="sxs-lookup"><span data-stu-id="a358c-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="a358c-112">Основным источником информации о пакете является его страница сведений на веб-сайте nuget.org (или в другом закрытом веб-канале).</span><span class="sxs-lookup"><span data-stu-id="a358c-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="a358c-113">На странице каждого пакета на веб-сайте nuget.org приводится описание проекта, история его версий и статистика использования.</span><span class="sxs-lookup"><span data-stu-id="a358c-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="a358c-114">В разделе **Сведения** на странице пакета также приводится ссылка на веб-сайт проекта, где обычно можно найти много примеров и других документов, с помощью которых можно оценить полезность пакета.</span><span class="sxs-lookup"><span data-stu-id="a358c-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="a358c-115">Дополнительные сведения см. в разделе [Поиск и выбор пакетов](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="a358c-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="a358c-116">NuGet в среде Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a358c-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="a358c-117">**Каким образом обеспечивается поддержка NuGet в различных продуктах Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="a358c-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="a358c-118">Visual Studio для Windows поддерживает [пользовательский интерфейс диспетчера пакетов](../consume-packages/install-use-packages-visual-studio.md) и [консоль диспетчера пакетов](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a358c-118">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="a358c-119">Visual Studio для Mac реализует встроенные возможности NuGet, которые описываются в разделе [Включение пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="a358c-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="a358c-120">Visual Studio Code для всех платформ не поддерживает прямую интеграцию с NuGet.</span><span class="sxs-lookup"><span data-stu-id="a358c-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="a358c-121">Используйте [интерфейс командной строки NuGet](../reference/nuget-exe-cli-reference.md) или [интерфейс командной строки dotnet](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="a358c-121">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="a358c-122">Azure DevOps реализует [шаг построения для восстановления пакетов NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="a358c-122">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="a358c-123">Также вы можете [разместить закрытые веб-каналы NuGet в Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="a358c-123">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="a358c-124">**Как определить точную версию устанавливаемых средств NuGet?**</span><span class="sxs-lookup"><span data-stu-id="a358c-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="a358c-125">В Visual Studio выберите **Справка > О Microsoft Visual Studio** и проверьте версию компонента **Диспетчер пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a358c-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="a358c-126">Также можно запустить консоль диспетчера пакетов (**Сервис > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**) и ввести `$host`, чтобы просмотреть сведения о версии NuGet и другую информацию.</span><span class="sxs-lookup"><span data-stu-id="a358c-126">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="a358c-127">**Какие языки программирования поддерживает NuGet?**</span><span class="sxs-lookup"><span data-stu-id="a358c-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="a358c-128">NuGet обычно работает с языками платформы .NET и предназначен для использования библиотек .NET в проекте.</span><span class="sxs-lookup"><span data-stu-id="a358c-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="a358c-129">Поскольку для проектов некоторых типов также поддерживаются средства автоматизации MSBuild и Visual Studio, в определенной степени также поддерживаются другие проекты и языки.</span><span class="sxs-lookup"><span data-stu-id="a358c-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="a358c-130">Последняя версия NuGet поддерживает C#, Visual Basic, F#, WiX и C++.</span><span class="sxs-lookup"><span data-stu-id="a358c-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="a358c-131">**Какие шаблоны проектов поддерживает NuGet?**</span><span class="sxs-lookup"><span data-stu-id="a358c-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="a358c-132">NuGet обеспечивает полную поддержку множества шаблонов проектов, включая Windows, Интернет, облако, SharePoint, Wix и другие.</span><span class="sxs-lookup"><span data-stu-id="a358c-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="a358c-133">**Как обновить пакеты, которые являются частью шаблонов Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="a358c-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="a358c-134">Перейдите на вкладку **Обновления** в пользовательском интерфейсе диспетчера проектов и выберите **Обновить все** или воспользуйтесь [командой `Update-Package`](../reference/ps-reference/ps-ref-update-package.md) в консоли диспетчера проектов.</span><span class="sxs-lookup"><span data-stu-id="a358c-134">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="a358c-135">Чтобы обновить сам шаблон, необходимо вручную обновить репозиторий шаблонов.</span><span class="sxs-lookup"><span data-stu-id="a358c-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="a358c-136">Дополнительные сведения по этой теме см. в [блоге Ксавье Декостера (Xavier Decoster)](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages).</span><span class="sxs-lookup"><span data-stu-id="a358c-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="a358c-137">Обратите внимание, что все это вы делаете на свой страх и риск, поскольку ручное обновление может привести к повреждению шаблона в том случае, если последние версии всех зависимостей несовместимы друг с другом.</span><span class="sxs-lookup"><span data-stu-id="a358c-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="a358c-138">**Можно ли использовать NuGet вне среды Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="a358c-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="a358c-139">Да. NuGet работает непосредственно из командной строки.</span><span class="sxs-lookup"><span data-stu-id="a358c-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="a358c-140">См. [руководство по установке](../install-nuget-client-tools.md) и [справочник по интерфейсу командной строки](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a358c-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="a358c-141">Командная строка NuGet</span><span class="sxs-lookup"><span data-stu-id="a358c-141">NuGet command line</span></span>

<span data-ttu-id="a358c-142">**Как получить последнюю версию средства командной строки NuGet?**</span><span class="sxs-lookup"><span data-stu-id="a358c-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="a358c-143">См. [руководство по установке](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="a358c-143">See the [Install guide](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="a358c-144">Чтобы проверить текущую установленную версию средства, выполните команду `nuget help`.</span><span class="sxs-lookup"><span data-stu-id="a358c-144">To check the current installed version of the tool, use `nuget help`.</span></span>

<span data-ttu-id="a358c-145">**Для чего нужна лицензия на веб-сайте nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="a358c-145">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="a358c-146">Вы можете распространить nuget.exe в соответствии с условиями лицензии MIT.</span><span class="sxs-lookup"><span data-stu-id="a358c-146">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="a358c-147">Вы несете ответственность за обновление и обслуживание всех распространяемых вами копий nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="a358c-147">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="a358c-148">**Можно ли расширить возможности средства командной строки NuGet?**</span><span class="sxs-lookup"><span data-stu-id="a358c-148">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="a358c-149">Да. Вы можете добавлять в `nuget.exe` собственные команды, как описывается в [статье Роба Рейнолда (Rob Reynold)](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="a358c-149">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="a358c-150">Консоль диспетчера пакетов NuGet (Visual Studio для Windows)</span><span class="sxs-lookup"><span data-stu-id="a358c-150">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="a358c-151">**Как получить доступ к объекту DTE в консоли диспетчера пакетов?**</span><span class="sxs-lookup"><span data-stu-id="a358c-151">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="a358c-152">Объект верхнего уровня в объектной модели автоматизации Visual Studio называется объектом DTE (среда средств разработки).</span><span class="sxs-lookup"><span data-stu-id="a358c-152">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="a358c-153">Этот объект предоставляется консолью с помощью переменной `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="a358c-153">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="a358c-154">Дополнительные сведения см. в разделе [Общие сведения о модели автоматизации](/visualstudio/extensibility/internals/automation-model-overview) в документации по расширению среды Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a358c-154">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="a358c-155">**При попытке привести переменную $DTE к типу DTE2 возникает ошибка: "Не удается преобразовать значение "EnvDTE.DTEClass" типа "EnvDTE.DTEClass" в тип "EnvDTE80.DTE2"". В чем проблема?**</span><span class="sxs-lookup"><span data-stu-id="a358c-155">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="a358c-156">Это известная проблема, связанная с взаимодействием PowerShell с COM-объектом.</span><span class="sxs-lookup"><span data-stu-id="a358c-156">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="a358c-157">Попробуйте выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a358c-157">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="a358c-158">`Get-Interface` — это вспомогательная функция, добавляемая узлом PowerShell NuGet.</span><span class="sxs-lookup"><span data-stu-id="a358c-158">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="a358c-159">Создание и публикация пакетов</span><span class="sxs-lookup"><span data-stu-id="a358c-159">Creating and publishing packages</span></span>

<span data-ttu-id="a358c-160">**Как включить мой пакет в веб-канал?**</span><span class="sxs-lookup"><span data-stu-id="a358c-160">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="a358c-161">См. раздел [Создание и публикация пакетов](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a358c-161">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="a358c-162">**У меня есть несколько версий библиотеки, предназначенных для различных версий платформы .NET Framework. Как построить единый пакет, поддерживающий такую реализацию?**</span><span class="sxs-lookup"><span data-stu-id="a358c-162">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="a358c-163">См. раздел [Поддержка нескольких версий и профилей платформы .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="a358c-163">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="a358c-164">**Как настроить свой собственный репозиторий или веб-канал?**</span><span class="sxs-lookup"><span data-stu-id="a358c-164">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="a358c-165">См. раздел [Общие сведения о размещении пакетов](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="a358c-165">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="a358c-166">**Как выполнить массовую загрузку пакетов в мой веб-канал NuGet?**</span><span class="sxs-lookup"><span data-stu-id="a358c-166">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="a358c-167">См. раздел [Массовая публикация пакетов NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="a358c-167">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="a358c-168">Работа с пакетами</span><span class="sxs-lookup"><span data-stu-id="a358c-168">Working with packages</span></span>

<span data-ttu-id="a358c-169">**Можно ли устанавливать пакеты NuGet без подключения к Интернету?**</span><span class="sxs-lookup"><span data-stu-id="a358c-169">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="a358c-170">Да. См. статью блога Скотта Ханселмана (Scott Hanselman), посвященную [доступу к NuGet при неработающем веб-сайте nuget.org или во время полета на самолете](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="a358c-170">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="a358c-171">**Можно ли устанавливать пакеты в папку, отличную от заданной по умолчанию?**</span><span class="sxs-lookup"><span data-stu-id="a358c-171">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="a358c-172">Задайте параметр [`repositoryPath`](../reference/nuget-config-file.md#config-section) в файле `Nuget.Config`, используя `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="a358c-172">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="a358c-173">**Как избежать добавления папки пакетов NuGet в систему управления версиями?**</span><span class="sxs-lookup"><span data-stu-id="a358c-173">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="a358c-174">Присвойте свойству [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) в файле `Nuget.Config` значение `true`.</span><span class="sxs-lookup"><span data-stu-id="a358c-174">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="a358c-175">Этот ключ работает на уровне решения и поэтому должен добавляться в файл `$(Solutiondir)\.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="a358c-175">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="a358c-176">Если включить восстановление пакета из Visual Studio, этот файл будет создан автоматически.</span><span class="sxs-lookup"><span data-stu-id="a358c-176">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="a358c-177">**Как отключить восстановление пакетов?**</span><span class="sxs-lookup"><span data-stu-id="a358c-177">**How do I turn off package restore?**</span></span>

<span data-ttu-id="a358c-178">См. раздел [Включение и отключение восстановления пакетов](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="a358c-178">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="a358c-179">**Почему при установке локального пакета с удаленными зависимостями возникает ошибка "Не удается разрешить зависимость"?**</span><span class="sxs-lookup"><span data-stu-id="a358c-179">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="a358c-180">При установке локального пакета в проект выберите источник **Все**.</span><span class="sxs-lookup"><span data-stu-id="a358c-180">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="a358c-181">При этом вместо использования одного веб-канала будут объединены все веб-каналы.</span><span class="sxs-lookup"><span data-stu-id="a358c-181">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="a358c-182">Причиной этой ошибки обычно является то, что пользователи локального репозитория часто стремятся избежать случайной установки удаленного пакета из-за требований корпоративной политики.</span><span class="sxs-lookup"><span data-stu-id="a358c-182">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="a358c-183">**У меня есть несколько проектов, расположенных в одной папке. Как использовать отдельные файлы packages.config для каждого проекта?**</span><span class="sxs-lookup"><span data-stu-id="a358c-183">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="a358c-184">В большинстве случаев, когда отдельные проекты располагаются в отдельных папках, это не проблема, поскольку NuGet идентифицирует файлы `packages.config` в каждом проекте.</span><span class="sxs-lookup"><span data-stu-id="a358c-184">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="a358c-185">Если вы работаете с NuGet версии 3.3 или более поздней и размещаете несколько проектов в одной папке, вы можете вставить имя проекта в имена файлов `packages.config`, используя шаблон `packages.{project-name}.config`. NuGet будет использовать этот файл.</span><span class="sxs-lookup"><span data-stu-id="a358c-185">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="a358c-186">Это также не проблема при использовании PackageReference, поскольку каждый файл проекта содержит собственный список зависимостей.</span><span class="sxs-lookup"><span data-stu-id="a358c-186">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="a358c-187">**Я не вижу nuget.org в списке репозиториев. Как вернуть его?**</span><span class="sxs-lookup"><span data-stu-id="a358c-187">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="a358c-188">Добавьте `https://api.nuget.org/v3/index.json` в список источников или</span><span class="sxs-lookup"><span data-stu-id="a358c-188">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="a358c-189">Удалите файл `%appdata%\.nuget\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) и дождитесь, пока NuGet снова создаст его.</span><span class="sxs-lookup"><span data-stu-id="a358c-189">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
