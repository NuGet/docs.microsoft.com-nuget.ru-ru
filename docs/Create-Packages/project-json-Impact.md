---
title: "Влияние project.json на авторов пакетов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 983485df-9375-4827-b58b-70065320ee37
description: "Сведения о том, как реализация project.json в NuGet 3.x влияет на авторов пакетов, например неподдерживаемые функции, содержимое и формат пакетов."
keywords: "NuGet и project.json, влияние project.json, аспекты создания пакетов, функции project.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 93a4e9f9cb57c8acbe516a957e01b801bac0e116
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="6c680-104">Влияние project.json при создании пакетов</span><span class="sxs-lookup"><span data-stu-id="6c680-104">Impact of project.json when creating packages</span></span>

<span data-ttu-id="6c680-105">Система `project.json`, используемая в NuGet 3+, влияет на авторов пакетов несколькими разными способами, описанными в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="6c680-105">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="6c680-106">Изменения, затрагивающие использование существующих пакетов</span><span class="sxs-lookup"><span data-stu-id="6c680-106">Changes affecting existing packages usage</span></span>

<span data-ttu-id="6c680-107">Традиционные пакеты NuGet поддерживают набор функций, которые не переносятся в транзитивный мир.</span><span class="sxs-lookup"><span data-stu-id="6c680-107">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="6c680-108">Скрипты установки и удаления игнорируются</span><span class="sxs-lookup"><span data-stu-id="6c680-108">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="6c680-109">В модели транзитивного восстановления, описанной в разделе [Разрешение зависимостей](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference-and-projectjson), отсутствует понятие "время установки пакета".</span><span class="sxs-lookup"><span data-stu-id="6c680-109">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference-and-projectjson), does not have a concept of "package install time".</span></span> <span data-ttu-id="6c680-110">Пакет присутствует или отсутствует, но не существует никакого согласованного процесса, реализуемого при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="6c680-110">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="6c680-111">Кроме того, скрипты установки поддерживались только в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c680-111">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="6c680-112">Другим интегрированным средам разработки для поддержки таких скриптов пришлось имитировать API расширяемости Visual Studio, а в распространенных редакторах и программах командной строки такая поддержка отсутствовала.</span><span class="sxs-lookup"><span data-stu-id="6c680-112">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="6c680-113">Преобразования содержимого не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="6c680-113">Content transforms are not supported.</span></span>

<span data-ttu-id="6c680-114">Подобно скриптам установки, преобразования запускаются при установке пакета и обычно не являются идемпотентными.</span><span class="sxs-lookup"><span data-stu-id="6c680-114">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="6c680-115">Так как времени установки больше нет, XDT Transform и другие аналогичные компоненты не поддерживаются и игнорируются при использовании такого пакета в транзитивном сценарии.</span><span class="sxs-lookup"><span data-stu-id="6c680-115">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>


### <a name="content"></a><span data-ttu-id="6c680-116">Content</span><span class="sxs-lookup"><span data-stu-id="6c680-116">Content</span></span>

<span data-ttu-id="6c680-117">К традиционным пакетам NuGet прилагаются файлы содержимого, например файлы исходного кода и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6c680-117">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="6c680-118">Обычно они используются в двух сценариях:</span><span class="sxs-lookup"><span data-stu-id="6c680-118">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="6c680-119">Начальные файлы помещаются в проект, чтобы пользователь мог изменить их позднее.</span><span class="sxs-lookup"><span data-stu-id="6c680-119">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="6c680-120">Типичным примером являются файлы конфигурации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6c680-120">The common example is default configuration files.</span></span>

2. <span data-ttu-id="6c680-121">Файлы содержимого сопровождают сборки, установленные в проекте.</span><span class="sxs-lookup"><span data-stu-id="6c680-121">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="6c680-122">В качестве примера здесь можно привести изображение логотипа, используемое в сборке.</span><span class="sxs-lookup"><span data-stu-id="6c680-122">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="6c680-123">Поддержка содержимого сейчас отключена по тем же причинам, что и скрипты и преобразования, но мы ведем работу в этом направлении.</span><span class="sxs-lookup"><span data-stu-id="6c680-123">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="6c680-124">Файлы содержимого по-прежнему можно переносить внутри пакетов. Сейчас они игнорируются, однако конечный пользователь по-прежнему может скопировать их в нужное место.</span><span class="sxs-lookup"><span data-stu-id="6c680-124">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="6c680-125">Вы можете просмотреть одно из предложений по возвращению файлов содержимого и отследить ход его реализации: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="6c680-125">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="6c680-126">Влияние на авторов пакетов</span><span class="sxs-lookup"><span data-stu-id="6c680-126">Impact for package authors</span></span>

<span data-ttu-id="6c680-127">Пакетам с указанными выше функциями придется использовать другой механизм.</span><span class="sxs-lookup"><span data-stu-id="6c680-127">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="6c680-128">В общем случае наиболее удобным механизмом являются целевые объекты и свойства MSBuild, которые полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="6c680-128">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="6c680-129">Система сборки может использовать другие соглашения в пакете.</span><span class="sxs-lookup"><span data-stu-id="6c680-129">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="6c680-130">Именно так обеспечивается поддержка целевых объектов MSBuild, а также анализаторов Roslyn.</span><span class="sxs-lookup"><span data-stu-id="6c680-130">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="6c680-131">Можно создавать пакеты, поддерживающие целевые объекты и анализаторы для сценариев `packages.config` и `project.json`.</span><span class="sxs-lookup"><span data-stu-id="6c680-131">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="6c680-132">Пакеты, которые пытаются изменить проект для упрощения запуска, обычно функционируют лишь в ограниченном наборе сценариев, и вместо этого им следует предоставлять файл сведений или указания по использованию пакета.</span><span class="sxs-lookup"><span data-stu-id="6c680-132">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="6c680-133">Большинству существующих пакетов не потребуется использовать описанный ниже формат пакета.</span><span class="sxs-lookup"><span data-stu-id="6c680-133">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="6c680-134">Этот формат позволяет использовать собственное содержимое в привилегированном сценарии.</span><span class="sxs-lookup"><span data-stu-id="6c680-134">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="6c680-135">Это означает, что управляемые сборки, зависящие от приближенных к оборудованию реализаций, предоставляют двоичные реализации наряду с управляемыми сборками в зависимости от целевой платформы.</span><span class="sxs-lookup"><span data-stu-id="6c680-135">This means that managed assemblies depending on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="6c680-136">Например, эту технологию использует пакет System.IO.Compression.</span><span class="sxs-lookup"><span data-stu-id="6c680-136">For example System.IO.Compression package is utilizing this technology.</span></span> [<span data-ttu-id="6c680-137">https://www.nuget.org/packages/System.IO.Compression</span><span class="sxs-lookup"><span data-stu-id="6c680-137">https://www.nuget.org/packages/System.IO.Compression</span></span>](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="6c680-138">Таким образом, если описанные выше функции не являются обязательными, мы рекомендуем использовать существующий формат пакета, так как описанный здесь формат поддерживается только NuGet 3.x+.</span><span class="sxs-lookup"><span data-stu-id="6c680-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="6c680-139">Можно было бы создать пакеты, работающие как для сценариев `packages.config`, так и для сценариев `project.json`, с помощью создания оболочки совместимости, однако часто бывает проще структурировать пакет традиционным образом, не прибегая к указанным выше нерекомендуемым функциям.</span><span class="sxs-lookup"><span data-stu-id="6c680-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it is often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>


## <a name="3x-package-format"></a><span data-ttu-id="6c680-140">Формат пакета 3.x</span><span class="sxs-lookup"><span data-stu-id="6c680-140">3.x package format</span></span>  ##

<span data-ttu-id="6c680-141">Формат пакета 3.x предоставляет несколько дополнительных функций по сравнению с форматом NuGet 2.x:</span><span class="sxs-lookup"><span data-stu-id="6c680-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="6c680-142">Определение базовой сборки, используемой для компиляции, и набора сборок реализации, используемых во время выполнения на разных платформах и устройствах.</span><span class="sxs-lookup"><span data-stu-id="6c680-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="6c680-143">Это позволяет вам воспользоваться преимуществами API для конкретной платформы, а также предоставляет потребителям общую контактную зону.</span><span class="sxs-lookup"><span data-stu-id="6c680-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="6c680-144">В частности, это упрощает написание промежуточных переносимых библиотек.</span><span class="sxs-lookup"><span data-stu-id="6c680-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

2. <span data-ttu-id="6c680-145">Позволяет пакетам выполнять сводку по платформам, например операционным системам или архитектуре ЦП.</span><span class="sxs-lookup"><span data-stu-id="6c680-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

3. <span data-ttu-id="6c680-146">Обеспечивает разделение реализаций для конкретной платформы по дополнительным пакетам.</span><span class="sxs-lookup"><span data-stu-id="6c680-146">Allows for separation of platform specific implementations to companion packages.</span></span>

4. <span data-ttu-id="6c680-147">Поддержка собственных зависимостей в качестве привилегированного компонента.</span><span class="sxs-lookup"><span data-stu-id="6c680-147">Support Native dependencies as a first class citizen.</span></span>