---
title: Создание локализованного пакета NuGet
description: Сведения о двух способах создать локализованные пакеты NuGet, включив все сборки в один пакет или опубликовав отдельные сборки.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: cb3f8a9df66f259b130996822f102c27636d5d2c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774753"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="cdcda-103">Создание локализованных пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="cdcda-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="cdcda-104">Существует два способа создать локализованные версии библиотеки:</span><span class="sxs-lookup"><span data-stu-id="cdcda-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="cdcda-105">Включить все локализованные сборки ресурсов в один пакет.</span><span class="sxs-lookup"><span data-stu-id="cdcda-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="cdcda-106">Создать отдельные локализованные вспомогательные пакеты, следуя строгому набору соглашений.</span><span class="sxs-lookup"><span data-stu-id="cdcda-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="cdcda-107">Оба метода имеют преимущества и недостатки, описанные в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="cdcda-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="cdcda-108">Локализованные сборки ресурсов в одном пакете</span><span class="sxs-lookup"><span data-stu-id="cdcda-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="cdcda-109">Включение локализованных сборок ресурсов в один пакет обычно является самым простым подходом.</span><span class="sxs-lookup"><span data-stu-id="cdcda-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="cdcda-110">Для этого создайте внутри `lib` папки для поддерживаемого языка, отличного от используемого по умолчанию в пакете (предполагается, что это en-us).</span><span class="sxs-lookup"><span data-stu-id="cdcda-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="cdcda-111">В эти папки можно поместить сборки ресурсов и локализованные XML-файлы IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="cdcda-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="cdcda-112">Например, следующая структура папок поддерживает немецкий (de), итальянский (it), японский (ja), русский (ru), китайский (упрощенное письмо) (zh-Hans) и китайский (традиционное письмо) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="cdcda-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

```
lib
└───net40
    │   Contoso.Utilities.dll
    │   Contoso.Utilities.xml
    │
    ├───de
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───it
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───ja
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───ru
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    ├───zh-Hans
    │       Contoso.Utilities.resources.dll
    │       Contoso.Utilities.xml
    │
    └───zh-Hant
            Contoso.Utilities.resources.dll
            Contoso.Utilities.xml
```

<span data-ttu-id="cdcda-113">Видно, что все языки указаны под папкой целевой платформы `net40`.</span><span class="sxs-lookup"><span data-stu-id="cdcda-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="cdcda-114">Если вы [обеспечиваете поддержку нескольких платформ](../create-packages/supporting-multiple-target-frameworks.md), то в `lib` у вас есть папка для каждого из вариантов.</span><span class="sxs-lookup"><span data-stu-id="cdcda-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="cdcda-115">Разместив все эти папки, сошлитесь на все файлы в `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="cdcda-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="cdcda-116">Одним из примеров пакета, использующего этот подход, является [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="cdcda-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="cdcda-117">Преимущества и недостатки (локализованные сборки ресурсов)</span><span class="sxs-lookup"><span data-stu-id="cdcda-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="cdcda-118">Объединение всех языков в одном пакете имеет несколько недостатков:</span><span class="sxs-lookup"><span data-stu-id="cdcda-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="cdcda-119">**Общие метаданные**. Так как пакет NuGet может содержать только один файл `.nuspec`, вы можете предоставить метаданные лишь для одного языка.</span><span class="sxs-lookup"><span data-stu-id="cdcda-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="cdcda-120">То есть NuGet не представляет поддержку локализованных метаданных.</span><span class="sxs-lookup"><span data-stu-id="cdcda-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="cdcda-121">**Размер пакета**. В зависимости от числа поддерживаемых языков библиотека может стать довольно большой, что замедляет установку и восстановление пакета.</span><span class="sxs-lookup"><span data-stu-id="cdcda-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="cdcda-122">**Одновременные выпуски**. Объединение локализованных файлов в один пакет требует выпускать все ресурсы в этом пакете одновременно, то есть вы не сможете выпустить каждую локализацию отдельно.</span><span class="sxs-lookup"><span data-stu-id="cdcda-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="cdcda-123">Кроме того, при обновлении любой из локализаций требуется новая версия для всего пакета.</span><span class="sxs-lookup"><span data-stu-id="cdcda-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="cdcda-124">Однако оно имеет и некоторые преимущества:</span><span class="sxs-lookup"><span data-stu-id="cdcda-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="cdcda-125">**Простота**. Потребители пакета получают все поддерживаемые языки за одну установку вместо того, чтобы устанавливать каждый язык отдельно.</span><span class="sxs-lookup"><span data-stu-id="cdcda-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="cdcda-126">Отдельный пакет также легче найти на сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cdcda-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="cdcda-127">**Связанные версии**. Так как все сборки ресурсов находятся в том же пакете, что и основная сборка, они имеют одинаковый номер версии и не могут быть ошибочно разделены.</span><span class="sxs-lookup"><span data-stu-id="cdcda-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="cdcda-128">Локализованные вспомогательные пакеты</span><span class="sxs-lookup"><span data-stu-id="cdcda-128">Localized satellite packages</span></span>

<span data-ttu-id="cdcda-129">По аналогии с тем, как .NET Framework поддерживает вспомогательные сборки, этот метод разделяет локализованные ресурсы и XML-файлы IntelliSense на вспомогательные пакеты.</span><span class="sxs-lookup"><span data-stu-id="cdcda-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="cdcda-130">Для этого ваш основной пакет использует соглашение об именовании `{identifier}.{version}.nupkg` и содержит сборку для языка по умолчанию (например, en-US).</span><span class="sxs-lookup"><span data-stu-id="cdcda-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="cdcda-131">Например, `ContosoUtilities.1.0.0.nupkg` будет содержать следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="cdcda-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

```
lib
└───net40
        ContosoUtilities.dll
        ContosoUtilities.xml
```

<span data-ttu-id="cdcda-132">Вспомогательная сборка затем использует соглашение об именовании `{identifier}.{language}.{version}.nupkg`, например `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="cdcda-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="cdcda-133">Идентификатор **должен** точно совпадать с идентификатором основного пакета.</span><span class="sxs-lookup"><span data-stu-id="cdcda-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="cdcda-134">Так как это отдельный пакет, он имеет свой собственный файл `.nuspec`, содержащий локализованные метаданные.</span><span class="sxs-lookup"><span data-stu-id="cdcda-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="cdcda-135">Помните, что язык в `.nuspec` **должен** соответствовать используемому в имени файла.</span><span class="sxs-lookup"><span data-stu-id="cdcda-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="cdcda-136">Вспомогательная сборка также **должна** объявить точную версию основного пакета в качестве зависимости с помощью нотации версии [] \(см. раздел [Управления версиями пакетов](../concepts/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="cdcda-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../concepts/package-versioning.md)).</span></span> <span data-ttu-id="cdcda-137">Например, `ContosoUtilities.de.1.0.0.nupkg` должен объявить о зависимости от `ContosoUtilities.1.0.0.nupkg` с помощью нотации `[1.0.0]`.</span><span class="sxs-lookup"><span data-stu-id="cdcda-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="cdcda-138">Конечно же, вспомогательный пакет может иметь не такой номер версии, как основной пакет.</span><span class="sxs-lookup"><span data-stu-id="cdcda-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="cdcda-139">Структура вспомогательного пакета должна содержать сборку ресурсов и XML-файл IntelliSense во вложенной папке, соответствующей значению `{language}` в имени файла пакета:</span><span class="sxs-lookup"><span data-stu-id="cdcda-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

```
lib
└───net40
    └───de
            ContosoUtilities.resources.dll
            ContosoUtilities.xml
```

<span data-ttu-id="cdcda-140">**Примечание**. Если не требуются конкретные язык и региональные параметры, такие как `ja-JP`, всегда используйте идентификатор языка более высокого уровня, такой как `ja`.</span><span class="sxs-lookup"><span data-stu-id="cdcda-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="cdcda-141">Во вспомогательной сборке NuGet распознает **только** файлы в папке, соответствующей `{language}` в имени файла.</span><span class="sxs-lookup"><span data-stu-id="cdcda-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="cdcda-142">Другие атрибуты игнорируются.</span><span class="sxs-lookup"><span data-stu-id="cdcda-142">All others are ignored.</span></span>

<span data-ttu-id="cdcda-143">При соблюдении всех этих соглашений NuGet распознает пакет в качестве вспомогательного и установит локализованные файлы в папку `lib` основного пакета, как если бы они были объединены изначально.</span><span class="sxs-lookup"><span data-stu-id="cdcda-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="cdcda-144">При удалении вспомогательного пакета удаляются и его файлы из этой папки.</span><span class="sxs-lookup"><span data-stu-id="cdcda-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="cdcda-145">Таким образом вы можете создать дополнительные вспомогательные сборки для каждого поддерживаемого языка.</span><span class="sxs-lookup"><span data-stu-id="cdcda-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="cdcda-146">Например, изучите набор пакетов MVC ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="cdcda-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="cdcda-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (основной английский язык)</span><span class="sxs-lookup"><span data-stu-id="cdcda-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="cdcda-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (немецкий)</span><span class="sxs-lookup"><span data-stu-id="cdcda-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="cdcda-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (японский)</span><span class="sxs-lookup"><span data-stu-id="cdcda-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="cdcda-150">[Microsoft.AspNet.Mvc.zh Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (китайский (упрощенное письмо))</span><span class="sxs-lookup"><span data-stu-id="cdcda-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="cdcda-151">[Microsoft.AspNet.Mvc.zh Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (китайский (традиционное письмо))</span><span class="sxs-lookup"><span data-stu-id="cdcda-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="cdcda-152">Сводка по необходимым соглашениям</span><span class="sxs-lookup"><span data-stu-id="cdcda-152">Summary of required conventions</span></span>

- <span data-ttu-id="cdcda-153">Основной пакет должен иметь имя `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="cdcda-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="cdcda-154">Вспомогательный пакет должен иметь имя `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="cdcda-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="cdcda-155">Вспомогательный пакет `.nuspec` должен указать свой язык в соответствии с именем файла.</span><span class="sxs-lookup"><span data-stu-id="cdcda-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="cdcda-156">Вспомогательный пакет должен объявить о зависимости от точной версии основного пакета с помощью нотации [] в своем файле `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="cdcda-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="cdcda-157">Диапазоны не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="cdcda-157">Ranges are not supported.</span></span>
- <span data-ttu-id="cdcda-158">Вспомогательный пакет должен поместить файлы в папку `lib\[{framework}\]{language}`, точно соответствующую `{language}` в имени файла.</span><span class="sxs-lookup"><span data-stu-id="cdcda-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="cdcda-159">Преимущества и недостатки (вспомогательные пакеты)</span><span class="sxs-lookup"><span data-stu-id="cdcda-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="cdcda-160">Использование вспомогательных пакетов дает несколько преимуществ:</span><span class="sxs-lookup"><span data-stu-id="cdcda-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="cdcda-161">**Размер пакета**. Место, занимаемое основным пакетом, сведено к минимуму, и потребители несут лишь затраты для каждого из нужных им языков.</span><span class="sxs-lookup"><span data-stu-id="cdcda-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="cdcda-162">**Отдельные метаданные**. Каждый вспомогательный пакет имеет свой собственный файл `.nuspec` и, следовательно, собственные локализованные метаданные.</span><span class="sxs-lookup"><span data-stu-id="cdcda-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="cdcda-163">Это позволяет некоторым потребителям проще находить пакеты при поиске по локализованным условиям на сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cdcda-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="cdcda-164">**Несвязанные выпуски**. Вспомогательные сборки можно выпускать в течение некоторого периода, а не все одновременно, что позволяет распределить усилия по локализации.</span><span class="sxs-lookup"><span data-stu-id="cdcda-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="cdcda-165">Однако вспомогательные пакеты имеют и определенные недостатки:</span><span class="sxs-lookup"><span data-stu-id="cdcda-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="cdcda-166">**Беспорядок**. Вместо одного пакета вы получаете несколько, что может привести к загромождению результатов поиска на сайте nuget.org и длинному списку ссылок в проекте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cdcda-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="cdcda-167">**Строгие соглашения**.</span><span class="sxs-lookup"><span data-stu-id="cdcda-167">**Strict conventions**.</span></span> <span data-ttu-id="cdcda-168">Вспомогательные пакеты должны точно соответствовать соглашениям, в противном случае локализованные версии не будут приняты должным образом.</span><span class="sxs-lookup"><span data-stu-id="cdcda-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="cdcda-169">**Управление версиями**. Каждый вспомогательный пакет должен иметь зависимость по точной версии от основного пакета.</span><span class="sxs-lookup"><span data-stu-id="cdcda-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="cdcda-170">Это означает, что при обновлении основного пакета может потребоваться обновление всех вспомогательных пакетов, даже если ресурсы не изменились.</span><span class="sxs-lookup"><span data-stu-id="cdcda-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
