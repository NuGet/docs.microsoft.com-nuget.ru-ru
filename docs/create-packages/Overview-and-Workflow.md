---
title: Общие сведения о создании пакетов NuGet и соответствующем рабочем процессе
description: Общие сведения о процессе создания и публикации пакетов NuGet со ссылками на отдельные части процесса.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: a9dd4439f2aa72424187eaa2d9555d5af0e7843d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="package-creation-workflow"></a><span data-ttu-id="f282b-103">Рабочий процесс создания пакета</span><span class="sxs-lookup"><span data-stu-id="f282b-103">Package creation workflow</span></span>

<span data-ttu-id="f282b-104">Создание пакета начинается с получения скомпилированного кода (обычно это сборки .NET), который требуется упаковать и предоставить для общего доступа посредством открытой коллекции на веб-сайте nuget.org или закрытой коллекции в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="f282b-104">Creating a package starts with the compiled code (typically .NET assemblies) that you want to package and share with others, either through the public nuget.org gallery or a private gallery within your organization.</span></span> <span data-ttu-id="f282b-105">Пакет также может включать дополнительные файлы, в том числе файл сведений, который отображается при установке пакета, а также преобразования в определенные файлы проекта.</span><span class="sxs-lookup"><span data-stu-id="f282b-105">The package can also include additional files such as a readme that is displayed when the package is installed, and can include transformations to certain project files.</span></span>

<span data-ttu-id="f282b-106">Кроме того, пакет может также использоваться только для извлечения других зависимостей и не содержать собственного кода.</span><span class="sxs-lookup"><span data-stu-id="f282b-106">A package can also serve to only pull in any number of other dependencies, without containing any code of its own.</span></span> <span data-ttu-id="f282b-107">Такой способ подходит для распространения пакетов SDK, которые состоят из нескольких независимых пакетов.</span><span class="sxs-lookup"><span data-stu-id="f282b-107">Such a package is a convenient way to deliver an SDK that's composed of multiple independent packages.</span></span> <span data-ttu-id="f282b-108">В других случаях пакет может содержать только файлы символов (`.pdb`), которые используются при отладке.</span><span class="sxs-lookup"><span data-stu-id="f282b-108">In other cases, a package may contain only symbol (`.pdb`) files to aid debugging.</span></span>

> [!Note]
> <span data-ttu-id="f282b-109">При создании пакета, который будет использоваться другими разработчиками, важно понимать, что они будут зависеть от вашей работы.</span><span class="sxs-lookup"><span data-stu-id="f282b-109">When you create a package for use by other developers, it's important to understand that they are taking a dependency on your work.</span></span> <span data-ttu-id="f282b-110">Таким образом, создавая и публикуя пакет, вы также должны обеспечивать исправление ошибок и внесение других обновлений либо, как минимум, предоставление доступа к открытому исходному коду пакета, чтобы его могли обслуживать другие пользователи.</span><span class="sxs-lookup"><span data-stu-id="f282b-110">As such, creating and publishing a package also implies a commitment to fixing bugs and making other updates, or at the very least making the package available as open source so others can help to maintain it.</span></span>

<span data-ttu-id="f282b-111">В любом случае создание пакета начинается с определения включаемых в него сборок и других файлов.</span><span class="sxs-lookup"><span data-stu-id="f282b-111">Whatever the case, creating a package begins with deciding which assemblies and other files to package.</span></span> <span data-ttu-id="f282b-112">Затем следует создать файл манифеста (`.nuspec`), в котором описывается содержимое пакета, а также приводятся его идентификатор, номер версии, сведения об авторских правах, свойства и целевые объекты MSBuild и многое другое.</span><span class="sxs-lookup"><span data-stu-id="f282b-112">You then create a manifest file, referred to as a `.nuspec` file, to describe the package's contents along with its identifier, version number, copyright information, MSBuild props and targets, and much more.</span></span>

<span data-ttu-id="f282b-113">После того как вы подготовили все необходимые файлы в соответствующих папках и создали файл `.nuspec`, следует использовать команду `nuget pack` (или [назначение пакета MSBuild](../reference/msbuild-targets.md)) для объединения всех этих элементов в файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="f282b-113">When you've prepared all the necessary files in the appropriate folders and have created the appropriate `.nuspec` file, you then use the `nuget pack` command (or the [MSBuild pack target](../reference/msbuild-targets.md)) to put everything together into a `.nupkg` file.</span></span> <span data-ttu-id="f282b-114">После этого вы будете готовы развернуть пакет на любом узле, где он будет доступен другим разработчикам.</span><span class="sxs-lookup"><span data-stu-id="f282b-114">You're then ready to deploy the package to whatever host makes it available to other developers.</span></span>

> [!Tip]
> <span data-ttu-id="f282b-115">Пакет NuGet с расширением `.nupkg` представляет собой обычный ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="f282b-115">A NuGet package with the `.nupkg` extension is simply a ZIP file.</span></span> <span data-ttu-id="f282b-116">Чтобы просмотреть содержимое любого такого пакета, достаточно изменить его расширение на `.zip` и развернуть обычным способом.</span><span class="sxs-lookup"><span data-stu-id="f282b-116">To easily examine any package's contents, change the extension to `.zip` and expand its contents as usual.</span></span> <span data-ttu-id="f282b-117">Не забудьте изменить расширение на `.nupkg` перед загрузкой пакета на узел.</span><span class="sxs-lookup"><span data-stu-id="f282b-117">Just be sure to change the extension back to `.nupkg` before attempting to upload it to a host.</span></span>

<span data-ttu-id="f282b-118">Общее описание и начальные сведения о процессе создания см. в разделе [Создание пакета](../create-packages/creating-a-package.md), где приводятся пошаговые инструкции по выполнению общих для всех пакетов действий.</span><span class="sxs-lookup"><span data-stu-id="f282b-118">To learn and understand the creation process, start with [Creating a package](../create-packages/creating-a-package.md) which guides you through the core processes common to all packages.</span></span>

<span data-ttu-id="f282b-119">На этом этапе можно рассмотреть различные варианты работы с пакетом:</span><span class="sxs-lookup"><span data-stu-id="f282b-119">From there, you can consider a number of other options for your package:</span></span>

- <span data-ttu-id="f282b-120">[Поддержка нескольких целевых платформ](../create-packages/supporting-multiple-target-frameworks.md). В этом разделе описывается создание пакета с несколькими вариантами для различных платформ .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f282b-120">[Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md) describes how to create a package with multiple variants for different .NET Frameworks.</span></span>
- <span data-ttu-id="f282b-121">[Создание локализованных пакетов](../create-packages/creating-localized-packages.md). В этом разделе описывается структура пакета с несколькими языковыми ресурсами, а также порядок использования отдельных локализованных вспомогательных пакетов.</span><span class="sxs-lookup"><span data-stu-id="f282b-121">[Creating Localized Packages](../create-packages/creating-localized-packages.md) describes how to structure a package with multiple language resources and how to use separate localized satellite packages.</span></span>
- <span data-ttu-id="f282b-122">[Предварительные версии пакетов](../create-packages/prerelease-packages.md). В этом разделе демонстрируется порядок выпуска альфа, бета-версий и версий-кандидатов пакетов для заинтересованных в них клиентов.</span><span class="sxs-lookup"><span data-stu-id="f282b-122">[Pre-release Packages](../create-packages/prerelease-packages.md) demonstrates how to release alpha, beta, and rc packages to those customers who are interested.</span></span>
- <span data-ttu-id="f282b-123">[Преобразования файлов исходного кода и конфигурации](../create-packages/source-and-config-file-transformations.md). В этом разделе описывается, как выполнить одностороннюю замену маркера в файлах, которые добавляются в проект, а также изменить файлы `web.config` и `app.config`, используя параметры, которые отменяются при удалении пакета.</span><span class="sxs-lookup"><span data-stu-id="f282b-123">[Source and Config File Transformations](../create-packages/source-and-config-file-transformations.md) describes how you can do both one-way token replacements in files that are added to a project, and modify `web.config` and `app.config` with settings that are also backed out when the package is uninstalled.</span></span>
- <span data-ttu-id="f282b-124">[Пакеты символов](../create-packages/symbol-packages.md). В этом разделе приводятся указания по реализации символов для библиотеки, благодаря которым клиенты смогут пошагово выполнять ваш код во время отладки.</span><span class="sxs-lookup"><span data-stu-id="f282b-124">[Symbol Packages](../create-packages/symbol-packages.md) offers guidance for supplying symbols for your library that allow consumers to step into your code while debugging.</span></span>
- <span data-ttu-id="f282b-125">[Управление версиями пакетов](../reference/package-versioning.md). В этом разделе описывается порядок определения точных версий, которые допускаются для зависимостей (другие пакеты, используемые вашим пакетом).</span><span class="sxs-lookup"><span data-stu-id="f282b-125">[Package versioning](../reference/package-versioning.md) discusses how to identify the exact versions that you allow for your dependencies (other packages that you consume from your package).</span></span>
- <span data-ttu-id="f282b-126">[Собственные пакеты](../create-packages/native-packages.md). В этом разделе описывается порядок создания пакета для потребителей C++.</span><span class="sxs-lookup"><span data-stu-id="f282b-126">[Native Packages](../create-packages/native-packages.md) describes the process for creating a package for C++ consumers.</span></span>
- <span data-ttu-id="f282b-127">[Подписывание пакетов](../create-packages/sign-a-package.md). Этот раздел описывает добавление цифровой подписи для пакета.</span><span class="sxs-lookup"><span data-stu-id="f282b-127">[Signing Packages](../create-packages/sign-a-package.md) describes the process for adding a digital signature to a package.</span></span>

<span data-ttu-id="f282b-128">Если вы готовы опубликовать пакет на веб-сайте nuget.org, выполните простой процесс, описываемый в разделе [Публикация пакета](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f282b-128">When you're then ready to publish a package to nuget.org, follow the simple process in [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="f282b-129">Если вы хотите использовать вместо nuget.org закрытый веб-канал, ознакомьтесь с разделом [Общие сведения о размещении пакетов](../hosting-packages/overview.md)</span><span class="sxs-lookup"><span data-stu-id="f282b-129">If you want to use a private feed instead of nuget.org, see the [Hosting Packages Overview](../hosting-packages/overview.md)</span></span>