---
title: Пакеты NuGet и система управления версиями
description: Вопросы, касающиеся обработки пакетов NuGet в системах управления версиями и исходным кодом, а также пропуска пакетов с TFVC и GIT.
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: fa3ec6992002224c9fb56a53aee9096e6d2c6fbb
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901672"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="9e1c7-103">Пропуск пакетов NuGet в системах управления исходным кодом</span><span class="sxs-lookup"><span data-stu-id="9e1c7-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="9e1c7-104">Разработчики обычно пропускают пакеты NuGet из своих репозиториев управления исходным кодом и вместо этого полагаются на [восстановление пакетов](package-restore.md) для переустановки зависимостей проекта перед сборкой.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="9e1c7-105">К причинам использования восстановления пакетов относятся следующие:</span><span class="sxs-lookup"><span data-stu-id="9e1c7-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="9e1c7-106">Распределенные системы управления версиями, такие как Git, включают полные копии каждой версии каждого файла в репозитории.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="9e1c7-107">Часто обновляемые двоичные файлы приводят к значительному раздуванию и увеличивают время, необходимое для клонирования репозитория.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="9e1c7-108">При включении пакетов в репозиторий разработчики должны добавлять ссылки непосредственно на содержимое пакета на диске, а не ссылаться на пакеты с помощью NuGet, что может привести к наличию в проекте жестко заданных путей.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="9e1c7-109">Становится все труднее очистить решение от неиспользуемых папок пакетов, так как при этом нужно не удалить используемые папки пакетов.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="9e1c7-110">Опуская пакеты, вы обеспечиваете четкие границы владения между вашим кодом и чужими пакетами, от которых вы зависите.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="9e1c7-111">Многие пакеты NuGet уже находятся в их собственных репозиториях управления исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="9e1c7-112">Несмотря на то, что NuGet восстанавливает пакеты по умолчанию, чтобы пропустить некоторые из них, а именно папки `packages` в проекте, в системе управления исходным кодом требуется выполнить некоторые операции вручную, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="9e1c7-113">Пропуск пакетов в Git</span><span class="sxs-lookup"><span data-stu-id="9e1c7-113">Omitting packages with Git</span></span>

<span data-ttu-id="9e1c7-114">Используйте файл [.gitignore ](https://git-scm.com/docs/gitignore), чтобы игнорировать пакеты NuGet (`.nupkg`) `packages` папки и `project.assets.json`, среди прочего.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="9e1c7-115">Для справки см. [ образец `.gitignore` для проектов Visual Studio ](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span><span class="sxs-lookup"><span data-stu-id="9e1c7-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="9e1c7-116">Далее приведены важные части файла `.gitignore`:</span><span class="sxs-lookup"><span data-stu-id="9e1c7-116">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="9e1c7-117">Пропуск пакетов в системе управления версиями Team Foundation</span><span class="sxs-lookup"><span data-stu-id="9e1c7-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="9e1c7-118">По возможности выполните эти инструкции *перед* добавлением проекта в систему управления исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="9e1c7-119">В противном случае вручную удалите папку `packages` из репозитория и верните это изменение, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="9e1c7-120">Отключение интеграции системы управления исходным кодом с TFVC для выбранных файлов:</span><span class="sxs-lookup"><span data-stu-id="9e1c7-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="9e1c7-121">Создайте папку с именем `.nuget` в папке решения (где находится файл `.sln`).</span><span class="sxs-lookup"><span data-stu-id="9e1c7-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="9e1c7-122">Совет. Чтобы создать эту папку в проводнике Windows, используйте имя `.nuget.` *с* конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="9e1c7-123">В этой папке создайте файл с именем `NuGet.Config` и откройте его для редактирования.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="9e1c7-124">Добавьте хотя бы следующий текст, где параметр [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) предписывает Visual Studio пропустить все содержимое папки `packages`:</span><span class="sxs-lookup"><span data-stu-id="9e1c7-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="9e1c7-125">Если вы используете TFS 2010 или более ранней версии, замаскируйте папку `packages` в сопоставлениях рабочей области.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="9e1c7-126">В TFS 2012 или более поздней версии либо в Visual Studio Team Services создайте файл `.tfignore`, как описано в статье о [добавлении файлов на сервер](/vsts/tfvc/add-files-server?view=vsts#tfignore&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="9e1c7-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [Add Files to the Server](/vsts/tfvc/add-files-server?view=vsts#tfignore&preserve-view=true).</span></span> <span data-ttu-id="9e1c7-127">Включите в этот файл приведенное ниже содержимое, чтобы явно игнорировать изменения в папке `\packages` на уровне репозитория и нескольких других промежуточных файлах.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="9e1c7-128">(Вы можете создать файл в проводнике Windows, используя имя `.tfignore.` с конечной точкой, но сначала вам может потребоваться отключить параметр "Hide known file extensions" (Скрыть известные расширения файлов).)</span><span class="sxs-lookup"><span data-stu-id="9e1c7-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="9e1c7-129">Добавьте `NuGet.Config` и `.tfignore` в систему управления исходным кодом и верните изменения.</span><span class="sxs-lookup"><span data-stu-id="9e1c7-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
