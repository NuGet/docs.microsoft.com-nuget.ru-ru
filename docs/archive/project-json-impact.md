---
title: Влияние project.json на авторов пакетов NuGet | Документы Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Сведения о том, как реализация project.json в NuGet 3.x влияет на авторов пакетов, например неподдерживаемые функции, содержимое и формат пакетов.
keywords: NuGet и project.json, влияние project.json, аспекты создания пакетов, функции project.json
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6e8af98504a2866106e84943989aeb91f2e9c1fb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="b4540-104">Влияние project.json при создании пакетов</span><span class="sxs-lookup"><span data-stu-id="b4540-104">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="b4540-105">Это содержимое является устаревшим.</span><span class="sxs-lookup"><span data-stu-id="b4540-105">This content is deprecated.</span></span> <span data-ttu-id="b4540-106">Проекты должны использовать формат `packages.config` или PackageReference.</span><span class="sxs-lookup"><span data-stu-id="b4540-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="b4540-107">Система `project.json`, используемая в NuGet 3+, влияет на авторов пакетов несколькими разными способами, описанными в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="b4540-107">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="b4540-108">Изменения, затрагивающие использование существующих пакетов</span><span class="sxs-lookup"><span data-stu-id="b4540-108">Changes affecting existing packages usage</span></span>

<span data-ttu-id="b4540-109">Традиционные пакеты NuGet поддерживают набор функций, которые не переносятся в транзитивный мир.</span><span class="sxs-lookup"><span data-stu-id="b4540-109">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="b4540-110">Скрипты установки и удаления игнорируются</span><span class="sxs-lookup"><span data-stu-id="b4540-110">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="b4540-111">В модели транзитивного восстановления, описанной в разделе [Разрешение зависимостей](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), отсутствует понятие "время установки пакета".</span><span class="sxs-lookup"><span data-stu-id="b4540-111">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="b4540-112">Пакет присутствует или отсутствует, но не существует никакого согласованного процесса, реализуемого при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="b4540-112">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="b4540-113">Кроме того, скрипты установки поддерживались только в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4540-113">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="b4540-114">Другим интегрированным средам разработки для поддержки таких скриптов пришлось имитировать API расширяемости Visual Studio, а в распространенных редакторах и программах командной строки такая поддержка отсутствовала.</span><span class="sxs-lookup"><span data-stu-id="b4540-114">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="b4540-115">Преобразования содержимого не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b4540-115">Content transforms are not supported</span></span>

<span data-ttu-id="b4540-116">Подобно скриптам установки, преобразования запускаются при установке пакета и обычно не являются идемпотентными.</span><span class="sxs-lookup"><span data-stu-id="b4540-116">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="b4540-117">Так как времени установки больше нет, XDT Transform и другие аналогичные компоненты не поддерживаются и игнорируются при использовании такого пакета в транзитивном сценарии.</span><span class="sxs-lookup"><span data-stu-id="b4540-117">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="b4540-118">Content</span><span class="sxs-lookup"><span data-stu-id="b4540-118">Content</span></span>

<span data-ttu-id="b4540-119">К традиционным пакетам NuGet прилагаются файлы содержимого, например файлы исходного кода и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b4540-119">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="b4540-120">Обычно они используются в двух сценариях:</span><span class="sxs-lookup"><span data-stu-id="b4540-120">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="b4540-121">Начальные файлы помещаются в проект, чтобы пользователь мог изменить их позднее.</span><span class="sxs-lookup"><span data-stu-id="b4540-121">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="b4540-122">Типичным примером являются файлы конфигурации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b4540-122">The common example is default configuration files.</span></span>

1. <span data-ttu-id="b4540-123">Файлы содержимого сопровождают сборки, установленные в проекте.</span><span class="sxs-lookup"><span data-stu-id="b4540-123">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="b4540-124">В качестве примера здесь можно привести изображение логотипа, используемое в сборке.</span><span class="sxs-lookup"><span data-stu-id="b4540-124">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="b4540-125">Поддержка содержимого сейчас отключена по тем же причинам, что и скрипты и преобразования, но мы ведем работу в этом направлении.</span><span class="sxs-lookup"><span data-stu-id="b4540-125">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="b4540-126">Файлы содержимого по-прежнему можно переносить внутри пакетов. Сейчас они игнорируются, однако конечный пользователь по-прежнему может скопировать их в нужное место.</span><span class="sxs-lookup"><span data-stu-id="b4540-126">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="b4540-127">Вы можете просмотреть одно из предложений по возвращению файлов содержимого и отследить ход его реализации: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="b4540-127">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="b4540-128">Влияние на авторов пакетов</span><span class="sxs-lookup"><span data-stu-id="b4540-128">Impact for package authors</span></span>

<span data-ttu-id="b4540-129">Пакетам с указанными выше функциями придется использовать другой механизм.</span><span class="sxs-lookup"><span data-stu-id="b4540-129">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="b4540-130">В общем случае наиболее удобным механизмом являются целевые объекты и свойства MSBuild, которые полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b4540-130">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="b4540-131">Система сборки может использовать другие соглашения в пакете.</span><span class="sxs-lookup"><span data-stu-id="b4540-131">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="b4540-132">Именно так обеспечивается поддержка целевых объектов MSBuild, а также анализаторов Roslyn.</span><span class="sxs-lookup"><span data-stu-id="b4540-132">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="b4540-133">Можно создавать пакеты, поддерживающие целевые объекты и анализаторы для сценариев `packages.config` и `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b4540-133">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="b4540-134">Пакеты, которые пытаются изменить проект для упрощения запуска, обычно функционируют лишь в ограниченном наборе сценариев, и вместо этого им следует предоставлять файл сведений или указания по использованию пакета.</span><span class="sxs-lookup"><span data-stu-id="b4540-134">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="b4540-135">Большинству существующих пакетов не потребуется использовать описанный ниже формат пакета.</span><span class="sxs-lookup"><span data-stu-id="b4540-135">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="b4540-136">Этот формат позволяет использовать собственное содержимое в привилегированном сценарии.</span><span class="sxs-lookup"><span data-stu-id="b4540-136">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="b4540-137">Это означает, что управляемые сборки, зависящие от приближенных к оборудованию реализаций, предоставляют двоичные реализации наряду с управляемыми сборками в зависимости от целевой платформы.</span><span class="sxs-lookup"><span data-stu-id="b4540-137">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="b4540-138">Например, эту технологию использует пакет System.IO.Compression.</span><span class="sxs-lookup"><span data-stu-id="b4540-138">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="b4540-139">Таким образом, если описанные выше функции не являются обязательными, мы рекомендуем использовать существующий формат пакета, так как описанный здесь формат поддерживается только NuGet 3.x+.</span><span class="sxs-lookup"><span data-stu-id="b4540-139">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="b4540-140">Создание пакетов, одновременно подходящих для сценариев `packages.config` и `project.json`, возможно при помощи оболочек совместимости, но часто проще структурировать пакеты традиционным образом, не прибегая к указанным выше нерекомендуемым функциям.</span><span class="sxs-lookup"><span data-stu-id="b4540-140">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="b4540-141">Формат пакета 3.x</span><span class="sxs-lookup"><span data-stu-id="b4540-141">3.x package format</span></span>

<span data-ttu-id="b4540-142">Формат пакета 3.x предоставляет несколько дополнительных функций по сравнению с форматом NuGet 2.x:</span><span class="sxs-lookup"><span data-stu-id="b4540-142">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="b4540-143">Определение базовой сборки, используемой для компиляции, и набора сборок реализации, используемых во время выполнения на разных платформах и устройствах.</span><span class="sxs-lookup"><span data-stu-id="b4540-143">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="b4540-144">Это позволяет вам воспользоваться преимуществами API для конкретной платформы, а также предоставляет потребителям общую контактную зону.</span><span class="sxs-lookup"><span data-stu-id="b4540-144">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="b4540-145">В частности, это упрощает написание промежуточных переносимых библиотек.</span><span class="sxs-lookup"><span data-stu-id="b4540-145">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="b4540-146">Позволяет пакетам выполнять сводку по платформам, например операционным системам или архитектуре ЦП.</span><span class="sxs-lookup"><span data-stu-id="b4540-146">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="b4540-147">Обеспечивает разделение реализаций для конкретной платформы по дополнительным пакетам.</span><span class="sxs-lookup"><span data-stu-id="b4540-147">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="b4540-148">Поддержка собственных зависимостей в качестве привилегированного компонента.</span><span class="sxs-lookup"><span data-stu-id="b4540-148">Support Native dependencies as a first class citizen.</span></span>
