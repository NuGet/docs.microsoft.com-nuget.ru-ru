---
title: Заметки о выпуске NuGet 1,5
description: Заметки о выпуске NuGet 1,5, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383353"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="f0295-103">Заметки о выпуске NuGet 1,5</span><span class="sxs-lookup"><span data-stu-id="f0295-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="f0295-104">[Заметки о выпуске nuget 1,4](../release-notes/nuget-1.4.md) | [заметок о выпуске NuGet 1,6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="f0295-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="f0295-105">Версия NuGet 1,5 была выпущена 30 августа 2011.</span><span class="sxs-lookup"><span data-stu-id="f0295-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="f0295-106">Функции</span><span class="sxs-lookup"><span data-stu-id="f0295-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="f0295-107">Шаблоны проектов с предварительно установленными пакетами NuGet</span><span class="sxs-lookup"><span data-stu-id="f0295-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="f0295-108">При создании нового шаблона проекта ASP.NET MVC 3 библиотеки скриптов jQuery, включенные в проект, фактически размещаются в нем при установке пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="f0295-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="f0295-109">Шаблон проекта ASP.NET MVC 3 включает набор пакетов NuGet, которые устанавливаются при вызове шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="f0295-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="f0295-110">Эта возможность включать пакеты NuGet с шаблоном проекта теперь является функцией NuGet, которую _любой_ шаблон проекта теперь может использовать.</span><span class="sxs-lookup"><span data-stu-id="f0295-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="f0295-111">Дополнительные сведения об этой функции см. в этой записи [блога разработчиком этой функции](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0295-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="f0295-112">Явные ссылки на сборки</span><span class="sxs-lookup"><span data-stu-id="f0295-112">Explicit Assembly References</span></span>

<span data-ttu-id="f0295-113">Добавлен новый элемент `<references />`, используемый для явного указания сборок в пакете, на которые следует ссылаться.</span><span class="sxs-lookup"><span data-stu-id="f0295-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="f0295-114">Например, если добавить следующее:</span><span class="sxs-lookup"><span data-stu-id="f0295-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="f0295-115">После этого в соответствующей подпапке [Framework/Profile](../reference/nuspec.md#explicit-assembly-references) в папке `lib` будут ссылаться только на `xunit.dll` и `xunit.extensions.dll`, даже если в папке находятся другие сборки.</span><span class="sxs-lookup"><span data-stu-id="f0295-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="f0295-116">Если этот элемент не указан, применяется обычное поведение, которое предназначено для ссылки на каждую сборку в папке `lib`.</span><span class="sxs-lookup"><span data-stu-id="f0295-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="f0295-117">__Для чего используется эта функция?__</span><span class="sxs-lookup"><span data-stu-id="f0295-117">__What is this feature used for?__</span></span>

<span data-ttu-id="f0295-118">Эта функция поддерживает сборки только во время разработки.</span><span class="sxs-lookup"><span data-stu-id="f0295-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="f0295-119">Например, при использовании контрактов кода сборки контракта должны находиться рядом с сборками среды выполнения, которые они дополняют, чтобы среда Visual Studio могла их найти, но сборки контрактов на самом деле не должны ссылаться на проект и не должны копироваться в папку `bin`.</span><span class="sxs-lookup"><span data-stu-id="f0295-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="f0295-120">Аналогичным образом эту функцию можно использовать для платформ модульного тестирования, таких как XUnit, которые должны располагаться рядом со сборками среды выполнения, но исключены из ссылок проекта.</span><span class="sxs-lookup"><span data-stu-id="f0295-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="f0295-121">Добавлена возможность исключения файлов из файла. nuspec</span><span class="sxs-lookup"><span data-stu-id="f0295-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="f0295-122">Элемент `<file>` в файле `.nuspec` может использоваться для включения определенного файла или набора файлов с помощью подстановочного знака.</span><span class="sxs-lookup"><span data-stu-id="f0295-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="f0295-123">При использовании подстановочного знака не существует способа исключить конкретное подмножество включаемых файлов.</span><span class="sxs-lookup"><span data-stu-id="f0295-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="f0295-124">Например, предположим, что вам нужны все текстовые файлы в папке, кроме определенного.</span><span class="sxs-lookup"><span data-stu-id="f0295-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="f0295-125">Для указания нескольких файлов используйте точку с запятой.</span><span class="sxs-lookup"><span data-stu-id="f0295-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="f0295-126">Или используйте подстановочный знак для исключения набора файлов, например всех файлов резервных копий.</span><span class="sxs-lookup"><span data-stu-id="f0295-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="f0295-127">Удаление пакетов с помощью диалогового окна с запросом на удаление зависимостей</span><span class="sxs-lookup"><span data-stu-id="f0295-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="f0295-128">При удалении пакета с зависимостями запрашивают NuGet, разрешая удаление зависимостей пакета вместе с пакетом.</span><span class="sxs-lookup"><span data-stu-id="f0295-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Удаление зависимых пакетов](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="f0295-130">`Get-Package` улучшение команд</span><span class="sxs-lookup"><span data-stu-id="f0295-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="f0295-131">Команда `Get-Package` теперь поддерживает параметр `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="f0295-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="f0295-132">Поэтому команда</span><span class="sxs-lookup"><span data-stu-id="f0295-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="f0295-133">Выводит список всех пакетов, установленных в Project а.</span><span class="sxs-lookup"><span data-stu-id="f0295-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="f0295-134">Поддержка прокси-серверов, требующих проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f0295-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="f0295-135">При использовании NuGet за прокси-сервером, который требует проверки подлинности, NuGet теперь будет запрашивать учетные данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="f0295-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="f0295-136">Ввод учетных данных позволяет NuGet подключаться к удаленному репозиторию.</span><span class="sxs-lookup"><span data-stu-id="f0295-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="f0295-137">Поддержка репозиториев, требующих проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f0295-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="f0295-138">NuGet теперь поддерживает подключение к [частным репозиториям](../hosting-packages/local-feeds.md) , требующим обычную проверку подлинности или NTLM.</span><span class="sxs-lookup"><span data-stu-id="f0295-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="f0295-139">В следующем выпуске будет добавлена поддержка дайджест-проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f0295-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="f0295-140">Повышение производительности репозитория nuget.org</span><span class="sxs-lookup"><span data-stu-id="f0295-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="f0295-141">Мы внесли несколько улучшений производительности в коллекцию nuget.org, чтобы сделать список пакетов и поиск быстрее.</span><span class="sxs-lookup"><span data-stu-id="f0295-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="f0295-142">Фильтрация проектов диалоговых окон решений</span><span class="sxs-lookup"><span data-stu-id="f0295-142">Solution dialog project filtering</span></span>
<span data-ttu-id="f0295-143">В диалоговом окне уровень решения при запросе на установку устанавливаемых проектов отображаются только проекты, совместимые с выбранным пакетом.</span><span class="sxs-lookup"><span data-stu-id="f0295-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="f0295-144">Заметки о выпуске пакета</span><span class="sxs-lookup"><span data-stu-id="f0295-144">Package Release Notes</span></span>
<span data-ttu-id="f0295-145">Пакеты NuGet теперь включают поддержку заметок о выпуске.</span><span class="sxs-lookup"><span data-stu-id="f0295-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="f0295-146">Заметки о выпуске отображаются только при просмотре _обновлений_ для пакета, поэтому нет смысла добавлять их в первый выпуск.</span><span class="sxs-lookup"><span data-stu-id="f0295-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Заметки о выпуске на вкладке "обновления"](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="f0295-148">Чтобы добавить заметки о выпуске в пакет, используйте новый элемент метаданных `<releaseNotes />` в файле NuSpec.</span><span class="sxs-lookup"><span data-stu-id="f0295-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="f0295-149">nuspec & лтфилес/&gt; улучшения</span><span class="sxs-lookup"><span data-stu-id="f0295-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="f0295-150">Файл `.nuspec` теперь допускает пустой элемент `<files />`, который указывает NuGet. exe не включать какой либо файл в пакет.</span><span class="sxs-lookup"><span data-stu-id="f0295-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="f0295-151">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="f0295-151">Bug Fixes</span></span>
<span data-ttu-id="f0295-152">В NuGet 1,5 было исправлено всего 107 рабочих элементов.</span><span class="sxs-lookup"><span data-stu-id="f0295-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="f0295-153">103 из них были помечены как ошибки.</span><span class="sxs-lookup"><span data-stu-id="f0295-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="f0295-154">Полный список рабочих элементов, исправленных в NuGet 1,5, см. в [этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="f0295-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="f0295-155">Исправлены ошибки, которые следует отметить:</span><span class="sxs-lookup"><span data-stu-id="f0295-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="f0295-156">[Ошибка 1273](http://nuget.codeplex.com/workitem/1273): `packages.config` более понятное управление версиями путем сортировки пакетов в алфавитном порядке и удаления лишних пробелов.</span><span class="sxs-lookup"><span data-stu-id="f0295-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="f0295-157">[Ошибка 844](http://nuget.codeplex.com/workitem/844): Теперь номера версий нормализованы, так что `Install-Package 1.0` работает с пакетом с `1.0.0`версии.</span><span class="sxs-lookup"><span data-stu-id="f0295-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="f0295-158">[Ошибка 1060](http://nuget.codeplex.com/workitem/1060). при создании пакета с помощью NuGet. exe флаг `-Version` переопределяет элемент `<version />`.</span><span class="sxs-lookup"><span data-stu-id="f0295-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
