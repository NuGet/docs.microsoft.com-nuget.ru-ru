---
title: Заметки о выпуске 1,5 NuGet
description: Заметки о выпуске для NuGet 1.5, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f2f7ebe718ce943faa31b7e19395eead8726648
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821347"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="84943-103">Заметки о выпуске 1,5 NuGet</span><span class="sxs-lookup"><span data-stu-id="84943-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="84943-104">[Заметки о выпуске NuGet 1.4](../release-notes/nuget-1.4.md) | [NuGet 1.6 заметки о выпуске](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="84943-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="84943-105">NuGet 1.5 был выпущен 30 августа 2011 г.</span><span class="sxs-lookup"><span data-stu-id="84943-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="84943-106">Функции</span><span class="sxs-lookup"><span data-stu-id="84943-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="84943-107">Шаблоны проектов с помощью NuGet предустановленных пакетов</span><span class="sxs-lookup"><span data-stu-id="84943-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="84943-108">При создании нового шаблона проекта ASP.NET MVC 3, библиотеки скриптов jQuery, включенный в проект фактически размещенные Установка пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="84943-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="84943-109">Шаблон проекта ASP.NET MVC 3 включает набор пакеты NuGet, которые устанавливаются при вызове шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="84943-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="84943-110">Эта возможность включить пакеты NuGet с помощью шаблона проекта теперь является функцией NuGet, _любой_ шаблон проекта теперь могут воспользоваться преимуществами.</span><span class="sxs-lookup"><span data-stu-id="84943-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="84943-111">Дополнительные сведения об этой возможности прочитать этот [записи блога от разработчика компонента](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="84943-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="84943-112">Ссылки на сборки, явные</span><span class="sxs-lookup"><span data-stu-id="84943-112">Explicit Assembly References</span></span>

<span data-ttu-id="84943-113">Добавлен новый `<references />` элемент используется, чтобы явно указать какие сборки в пакет, должна быть ссылка.</span><span class="sxs-lookup"><span data-stu-id="84943-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="84943-114">Например, добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="84943-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="84943-115">Затем только `xunit.dll` и `xunit.extensions.dll` будет ссылаться из соответствующих [вложенную папку framework или профиль](../reference/nuspec.md#explicit-assembly-references) из `lib` папки даже при наличии других сборок в папке.</span><span class="sxs-lookup"><span data-stu-id="84943-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="84943-116">Если этот элемент указан, то применяется обычным поведением, являющееся ссылаться каждая сборка в `lib` папки.</span><span class="sxs-lookup"><span data-stu-id="84943-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="84943-117">__Для чего используется этот компонент?__</span><span class="sxs-lookup"><span data-stu-id="84943-117">__What is this feature used for?__</span></span>

<span data-ttu-id="84943-118">Эта функция поддерживает только сборки времени разработки.</span><span class="sxs-lookup"><span data-stu-id="84943-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="84943-119">Например при использовании контрактов для кода, сборки контракта должны быть рядом с сборки среды выполнения, которые они расширяют, чтобы их можно было найти Visual Studio, но сборки контракт фактически не должны ссылаться в проекте и не будут скопированы в `bin` папки.</span><span class="sxs-lookup"><span data-stu-id="84943-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="84943-120">Аналогичным образом компонент может использоваться для для платформ модульного тестирования, например XUnit, которой требуется ее средств сборки рядом сборки среды выполнения, но исключаются из ссылки на проект.</span><span class="sxs-lookup"><span data-stu-id="84943-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="84943-121">Добавлена возможность исключить файлы в .nuspec</span><span class="sxs-lookup"><span data-stu-id="84943-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="84943-122">`<file>` Элемент в пределах `.nuspec` файл может использоваться для включения определенного файла или набора файлов, с помощью подстановочного знака.</span><span class="sxs-lookup"><span data-stu-id="84943-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="84943-123">При использовании подстановочного знака, нет возможности для исключения подмножества включенные файлы.</span><span class="sxs-lookup"><span data-stu-id="84943-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="84943-124">Например предположим, требуется, чтобы все текстовые файлы из папки, за исключением одну из них.</span><span class="sxs-lookup"><span data-stu-id="84943-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="84943-125">Чтобы указать несколько файлов, используйте точку с запятой.</span><span class="sxs-lookup"><span data-stu-id="84943-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="84943-126">Или набор файлов, например все файлы резервных копий с помощью подстановочного знака</span><span class="sxs-lookup"><span data-stu-id="84943-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="84943-127">Удаление пакетов, используя диалоговое окно предлагает для удаления зависимостей</span><span class="sxs-lookup"><span data-stu-id="84943-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="84943-128">При удалении пакета с зависимостями, предлагает NuGet, позволяя удаления зависимостей пакета вместе с пакетом.</span><span class="sxs-lookup"><span data-stu-id="84943-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Удаление зависимых пакетов](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="84943-130">`Get-Package` Команда улучшения</span><span class="sxs-lookup"><span data-stu-id="84943-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="84943-131">`Get-Package` Команда теперь поддерживает `-ProjectName` параметра.</span><span class="sxs-lookup"><span data-stu-id="84943-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="84943-132">Поэтому команда</span><span class="sxs-lookup"><span data-stu-id="84943-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="84943-133">будут перечислены все пакеты, установленные в проекте A.</span><span class="sxs-lookup"><span data-stu-id="84943-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="84943-134">Поддержка прокси-серверы, требующие проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="84943-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="84943-135">При использовании NuGet через прокси, который требует проверки подлинности, NuGet теперь предложит ввести учетные данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="84943-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="84943-136">Ввод учетных данных позволяет NuGet для подключения к удаленному репозиторию.</span><span class="sxs-lookup"><span data-stu-id="84943-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="84943-137">Поддержка репозиториев, требующих проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="84943-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="84943-138">NuGet теперь поддерживает подключение к [частных репозиториев](../hosting-packages/local-feeds.md) , требуется обычная или проверка подлинности NTLM.</span><span class="sxs-lookup"><span data-stu-id="84943-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="84943-139">Поддержка для дайджест-проверка подлинности будет добавлена в будущем выпуске.</span><span class="sxs-lookup"><span data-stu-id="84943-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="84943-140">Повышение производительности в репозиторий nuget.org</span><span class="sxs-lookup"><span data-stu-id="84943-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="84943-141">Мы внесли несколько изменений для повышения производительности галерею nuget.org, чтобы сделать пакет со списком быстрого и поиска.</span><span class="sxs-lookup"><span data-stu-id="84943-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="84943-142">Фильтрация проекта решения диалогового окна</span><span class="sxs-lookup"><span data-stu-id="84943-142">Solution dialog project filtering</span></span>
<span data-ttu-id="84943-143">В диалоговом уровне решения при выполнении запроса, для каких проектов для установки мы отображаются только проекты, которые совместимы с выбранным пакетом.</span><span class="sxs-lookup"><span data-stu-id="84943-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="84943-144">Заметки о выпуске пакета</span><span class="sxs-lookup"><span data-stu-id="84943-144">Package Release Notes</span></span>
<span data-ttu-id="84943-145">Пакеты NuGet теперь включают поддержку заметки о выпуске.</span><span class="sxs-lookup"><span data-stu-id="84943-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="84943-146">Заметки о выпуске Показывать только копирование при просмотре _обновления_ для пакета, поэтому он не имеет смысла для добавления в первом выпуске.</span><span class="sxs-lookup"><span data-stu-id="84943-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Заметки о выпуске обновления вкладке](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="84943-148">Чтобы добавить заметки о выпуске для пакета, используйте новый `<releaseNotes />` элемент метаданных в NuSpec-файла.</span><span class="sxs-lookup"><span data-stu-id="84943-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="84943-149">.nuspec & ltfiles /&gt; улучшения</span><span class="sxs-lookup"><span data-stu-id="84943-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="84943-150">`.nuspec` Файл теперь позволяет пустой `<files />` элемент, который сообщает nuget.exe не, чтобы включить все файлы в пакете.</span><span class="sxs-lookup"><span data-stu-id="84943-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="84943-151">Исправления ошибок</span><span class="sxs-lookup"><span data-stu-id="84943-151">Bug Fixes</span></span>
<span data-ttu-id="84943-152">NuGet 1.5 было всего 107 рабочие элементы фиксированной.</span><span class="sxs-lookup"><span data-stu-id="84943-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="84943-153">103 те из них были помечены как ошибки.</span><span class="sxs-lookup"><span data-stu-id="84943-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="84943-154">Полный список рабочих элементов исправления в 1,5 NuGet представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="84943-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="84943-155">Исправления следует отметить:</span><span class="sxs-lookup"><span data-stu-id="84943-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="84943-156">[Проблема 1273](http://nuget.codeplex.com/workitem/1273): внесенные `packages.config` Дополнительные системы управления версиями, понятное сортировкой пакеты в алфавитном порядке и удаления лишних пробелов.</span><span class="sxs-lookup"><span data-stu-id="84943-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="84943-157">[Проблема 844](http://nuget.codeplex.com/workitem/844): теперь нормализуются номера версий, чтобы `Install-Package 1.0` работает на пакет с версией `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="84943-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="84943-158">[Проблема 1060](http://nuget.codeplex.com/workitem/1060): при создании пакета с помощью nuget.exe, `-Version` флаг переопределения `<version />` элемента.</span><span class="sxs-lookup"><span data-stu-id="84943-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
