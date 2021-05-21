---
title: Файл сведений о пакете на NuGet.org
description: Подробное описание того, как отображаются файлы сведений на NuGet.org и что делать при возникновении проблем.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902230"
---
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="bbaae-103">Файл сведений о пакете на NuGet.org</span><span class="sxs-lookup"><span data-stu-id="bbaae-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="bbaae-104">[Добавьте в пакет NuGet файл сведений](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile), чтобы предоставить пользователям более детальные сведения о пакете.</span><span class="sxs-lookup"><span data-stu-id="bbaae-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="bbaae-105">Скорее всего, это один из первых элементов, которые пользователи увидят при просмотре страницы сведений о пакете на NuGet.org. Он очень важен для создания хорошего впечатления!</span><span class="sxs-lookup"><span data-stu-id="bbaae-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbaae-106">NuGet.org поддерживает только файлы сведений в формате [Markdown](https://daringfireball.net/projects/markdown/) и изображения из ограниченного набора доменов.</span><span class="sxs-lookup"><span data-stu-id="bbaae-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="bbaae-107">Ознакомьтесь с [разрешенными доменами для изображений](#allowed-domains-for-images-and-badges) и [поддерживаемыми функциями Markdown](#supported-markdown-features), чтобы убедиться, что файл сведений правильно отображается на NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="bbaae-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="bbaae-108">Что необходимо включить в файл сведений?</span><span class="sxs-lookup"><span data-stu-id="bbaae-108">What should my readme include?</span></span>

<span data-ttu-id="bbaae-109">Рассмотрите возможность включения следующих элементов в файл сведений:</span><span class="sxs-lookup"><span data-stu-id="bbaae-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="bbaae-110">Общие сведения о том, что представляет собой пакет, и какие проблемы он решает.</span><span class="sxs-lookup"><span data-stu-id="bbaae-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="bbaae-111">Инструкции по началу работы с пакетом и особые требования (при наличии).</span><span class="sxs-lookup"><span data-stu-id="bbaae-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="bbaae-112">Ссылки на более подробную документацию, если она не включена в сам файл сведений.</span><span class="sxs-lookup"><span data-stu-id="bbaae-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="bbaae-113">По крайней мере несколько фрагментов кода, примеров или изображений.</span><span class="sxs-lookup"><span data-stu-id="bbaae-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="bbaae-114">Где и как оставить отзыв, например ссылка на проблемы проекта, Twitter, средство отслеживания ошибок или другую платформу.</span><span class="sxs-lookup"><span data-stu-id="bbaae-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="bbaae-115">Как помочь разработке, если применимо.</span><span class="sxs-lookup"><span data-stu-id="bbaae-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="bbaae-116">Учтите, что качественные файлы сведений бывают самых разных форматов, форм и размеров.</span><span class="sxs-lookup"><span data-stu-id="bbaae-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="bbaae-117">Если у вас уже есть пакет, доступный на NuGet.org, вероятно, у вас есть `readme.md` или другой файл документации в репозитории, который будет отличным дополнением к странице сведений на NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="bbaae-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="bbaae-118">Предварительный просмотр файла сведений</span><span class="sxs-lookup"><span data-stu-id="bbaae-118">Preview your readme</span></span>

<span data-ttu-id="bbaae-119">Чтобы просмотреть файл сведений перед его публикацией на NuGet.org, отправьте пакет с помощью [веб-портала отправки пакетов на NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) и прокрутите вниз до раздела Readme File (Файл сведений) на странице предварительного просмотра метаданных.</span><span class="sxs-lookup"><span data-stu-id="bbaae-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="bbaae-120">Должно отобразиться примерно следующее:</span><span class="sxs-lookup"><span data-stu-id="bbaae-120">It should look something like this:</span></span>

![Предварительный просмотр файла сведений](media\readme-upload-preview.PNG)

<span data-ttu-id="bbaae-122">Рекомендуем воспользоваться предварительным просмотром и проверить файл сведений, чтобы обеспечить соответствие требованиям к [изображениям](#allowed-domains-for-images-and-badges) и [форматированию](#supported-markdown-features). Это поможет произвести отличное первое впечатление на потенциальных пользователей!</span><span class="sxs-lookup"><span data-stu-id="bbaae-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="bbaae-123">Чтобы исправить ошибки в файле сведений о пакете после его публикации на NuGet.org, необходимо отправить обновленную версию пакета с исправлением.</span><span class="sxs-lookup"><span data-stu-id="bbaae-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="bbaae-124">Если вы сразу убедитесь, что все выглядит хорошо, то сможете сэкономить время.</span><span class="sxs-lookup"><span data-stu-id="bbaae-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="bbaae-125">Разрешенные домены для изображений и эмблем</span><span class="sxs-lookup"><span data-stu-id="bbaae-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="bbaae-126">По соображениям безопасности и конфиденциальности NuGet.org поддерживает только ограниченный набор доменов, из которых можно отображать изображения и эмблемы на доверенных узлах.</span><span class="sxs-lookup"><span data-stu-id="bbaae-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="bbaae-127">NuGet.org позволяет отображать все изображения, в том числе эмблемы, из следующих доверенных доменов:</span><span class="sxs-lookup"><span data-stu-id="bbaae-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="bbaae-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-128">api.bintray.com</span></span>
* <span data-ttu-id="bbaae-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-129">api.codacy.com</span></span>
* <span data-ttu-id="bbaae-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-130">api.codeclimate.com</span></span>
* <span data-ttu-id="bbaae-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-131">api.dependabot.com</span></span>
* <span data-ttu-id="bbaae-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-132">api.travis-ci.com</span></span>
* <span data-ttu-id="bbaae-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="bbaae-133">api.travis-ci.org</span></span>
* <span data-ttu-id="bbaae-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="bbaae-134">app.fossa.io</span></span>
* <span data-ttu-id="bbaae-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="bbaae-135">badge.fury.io</span></span>
* <span data-ttu-id="bbaae-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="bbaae-136">badgen.net</span></span>
* <span data-ttu-id="bbaae-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="bbaae-137">badges.gitter.im</span></span>
* <span data-ttu-id="bbaae-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-138">bettercodehub.com</span></span>
* <span data-ttu-id="bbaae-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="bbaae-139">buildstats.info</span></span>
* <span data-ttu-id="bbaae-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="bbaae-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-141">ci.appveyor.com</span></span>
* <span data-ttu-id="bbaae-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-142">circleci.com</span></span>
* <span data-ttu-id="bbaae-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="bbaae-143">codecov.io</span></span>
* <span data-ttu-id="bbaae-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="bbaae-144">codefactor.io</span></span>
* <span data-ttu-id="bbaae-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="bbaae-145">coveralls.io</span></span>
* <span data-ttu-id="bbaae-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-146">dev.azure.com</span></span>
* <span data-ttu-id="bbaae-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="bbaae-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="bbaae-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-148">gitlab.com</span></span>
* <span data-ttu-id="bbaae-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="bbaae-149">img.shields.io</span></span>
* <span data-ttu-id="bbaae-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-150">isitmaintained.com</span></span>
* <span data-ttu-id="bbaae-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-151">opencollective.com</span></span>
* <span data-ttu-id="bbaae-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-152">raw.github.com</span></span>
* <span data-ttu-id="bbaae-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="bbaae-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="bbaae-154">snyk.io</span></span>
* <span data-ttu-id="bbaae-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="bbaae-155">sonarcloud.io</span></span>
* <span data-ttu-id="bbaae-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="bbaae-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="bbaae-157">Если вы считаете, что в список разрешений нужно добавить домен, вы можете [сообщить о проблеме](https://github.com/NuGet/NuGetGallery/issues), и она будет рассмотрена нашей командой специалистов по обеспечению конфиденциальности и безопасности.</span><span class="sxs-lookup"><span data-stu-id="bbaae-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="bbaae-158">Изображения с относительными локальными путями и изображения, размещенные в неподдерживаемых доменах, не будут отображаться. На странице предварительного просмотра файла сведений о пакете будет предупреждение, которое смогут увидеть только владельцы пакета.</span><span class="sxs-lookup"><span data-stu-id="bbaae-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="bbaae-159">Поддерживаемые возможности Markdown</span><span class="sxs-lookup"><span data-stu-id="bbaae-159">Supported Markdown features</span></span>
<span data-ttu-id="bbaae-160">[Markdown](https://daringfireball.net/projects/markdown/) — это облегченный язык разметки с синтаксисом форматирования обычного текста.</span><span class="sxs-lookup"><span data-stu-id="bbaae-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="bbaae-161">Файл сведений на NuGet.org поддерживает совместимый с [CommonMark](https://commonmark.org/) язык Markdown, на основе подсистемы анализа [Markdig](https://github.com/lunet-io/markdig).</span><span class="sxs-lookup"><span data-stu-id="bbaae-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="bbaae-162">В настоящее время NuGet.org поддерживает следующие возможности Markdown:</span><span class="sxs-lookup"><span data-stu-id="bbaae-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="bbaae-163">Заголовки</span><span class="sxs-lookup"><span data-stu-id="bbaae-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="bbaae-164">Изображения</span><span class="sxs-lookup"><span data-stu-id="bbaae-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="bbaae-165">Дополнительное выделение текста</span><span class="sxs-lookup"><span data-stu-id="bbaae-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="bbaae-166">Списки</span><span class="sxs-lookup"><span data-stu-id="bbaae-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="bbaae-167">Ссылки</span><span class="sxs-lookup"><span data-stu-id="bbaae-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="bbaae-168">Цитаты</span><span class="sxs-lookup"><span data-stu-id="bbaae-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="bbaae-169">Обратная косая черта в качестве escape-символа</span><span class="sxs-lookup"><span data-stu-id="bbaae-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="bbaae-170">Диапазоны кода</span><span class="sxs-lookup"><span data-stu-id="bbaae-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="bbaae-171">Списки задач</span><span class="sxs-lookup"><span data-stu-id="bbaae-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="bbaae-172">Таблицы</span><span class="sxs-lookup"><span data-stu-id="bbaae-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="bbaae-173">Эмодзи</span><span class="sxs-lookup"><span data-stu-id="bbaae-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="bbaae-174">Автоматические ссылки</span><span class="sxs-lookup"><span data-stu-id="bbaae-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

