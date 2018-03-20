---
title: "Пошаговое руководство по восстановлению пакетов NuGet с помощью сборки Team Foundation | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Пошаговое руководство по восстановлению пакетов NuGet с помощью сборки Team Foundation (Team Foundation Server и Visual Studio Team Services)."
keywords: "восстановление пакетов NuGet, NuGet и Team Foundation Server, NuGet и VSTS, системы сборки NuGet, сборка Team Foundation, пользовательские проекты MSBuild, облачная сборка, непрерывная интеграция"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e3ef6e3bcc55705315fcb6ccf3e917963c62250
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/08/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="14edb-104">Настройка восстановления пакетов с помощью сборки Team Foundation</span><span class="sxs-lookup"><span data-stu-id="14edb-104">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="14edb-105">В этой статье приводится подробное пошаговое руководство по восстановлению пакетов в рамках [сборки Team Services](/vsts/build-release/index) как для Git, так и для управления версиями Team Services.</span><span class="sxs-lookup"><span data-stu-id="14edb-105">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="14edb-106">Хотя это руководство относится к сценарию использования Visual Studio Team Services, основные принципы также применимы к другим системам управления версиями и сборки.</span><span class="sxs-lookup"><span data-stu-id="14edb-106">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="14edb-107">Применимо к:</span><span class="sxs-lookup"><span data-stu-id="14edb-107">Applies To:</span></span>

- <span data-ttu-id="14edb-108">пользовательским проектам MSBuild, выполняющимся в любой версии Team Foundation Server;</span><span class="sxs-lookup"><span data-stu-id="14edb-108">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="14edb-109">Team Foundation Server 2012 или более ранней версии;</span><span class="sxs-lookup"><span data-stu-id="14edb-109">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="14edb-110">пользовательским шаблонам процесса сборки Team Foundation, перенесенным в Team Foundation Server 2013 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="14edb-110">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="14edb-111">шаблонам процесса сборки с удаленными возможностями восстановления NuGet.</span><span class="sxs-lookup"><span data-stu-id="14edb-111">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="14edb-112">Если вы используете службы Visual Studio Team Services или сервер Team Foundation Server 2013 с шаблонами процесса сборки, автоматическое восстановление пакетов производится в рамках процесса сборки.</span><span class="sxs-lookup"><span data-stu-id="14edb-112">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="14edb-113">Общий подход</span><span class="sxs-lookup"><span data-stu-id="14edb-113">The general approach</span></span>

<span data-ttu-id="14edb-114">Преимущество использования NuGet в том, что вы можете избежать возврата двоичных файлов в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="14edb-114">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="14edb-115">Это особенно полезно в том случае, если вы применяете [распределенную систему управления версиями](http://en.wikipedia.org/wiki/Distributed_revision_control), такую как GIT, так как в этом случае разработчикам приходится клонировать весь репозиторий, включая полный журнал, прежде чем приступать к работе на локальных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="14edb-115">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="14edb-116">Возврат двоичных файлов может привести к существенному раздуванию репозитория, так как двоичные файлы обычно хранятся без разностного сжатия.</span><span class="sxs-lookup"><span data-stu-id="14edb-116">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="14edb-117">В NuGet уже давно поддерживается [восстановление пакетов](../consume-packages/package-restore.md) в процессе сборки.</span><span class="sxs-lookup"><span data-stu-id="14edb-117">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="14edb-118">В предыдущих реализациях возникала дилемма курицы и яйца в случае, если пакетам необходимо было расширить процесс сборки, так как в NuGet пакеты восстанавливались во время сборки проекта.</span><span class="sxs-lookup"><span data-stu-id="14edb-118">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="14edb-119">Платформа MSBuild не позволяет расширять сборку во время ее выполнения. Кто-то может посчитать это недостатком MSBuild, однако это спорный вопрос.</span><span class="sxs-lookup"><span data-stu-id="14edb-119">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="14edb-120">В зависимости от аспекта, который необходимо расширить, к моменту восстановления пакета регистрировать его может быть уже слишком поздно.</span><span class="sxs-lookup"><span data-stu-id="14edb-120">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="14edb-121">Решением этой проблемы может быть восстановление пакетов на первом этапе процесса сборки.</span><span class="sxs-lookup"><span data-stu-id="14edb-121">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="14edb-122">Если пакеты восстанавливаются перед сборкой кода, вам не нужно возвращать файлы `.targets`.</span><span class="sxs-lookup"><span data-stu-id="14edb-122">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="14edb-123">Пакеты должны быть созданы так, чтобы их можно было загружать в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="14edb-123">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="14edb-124">В противном случае может потребоваться возвращать файлы `.targets`, чтобы другие разработчики могли просто открывать решение, предварительно не восстанавливая пакеты.</span><span class="sxs-lookup"><span data-stu-id="14edb-124">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="14edb-125">В приведенном ниже демонстрационном проекте показано, как настроить сборку таким образом, чтобы папки `packages` и файлы `.targets` не нужно было возвращать.</span><span class="sxs-lookup"><span data-stu-id="14edb-125">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="14edb-126">Кроме того, показано, как настроить автоматическую сборку в Team Foundation Service для этого образца проекта.</span><span class="sxs-lookup"><span data-stu-id="14edb-126">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="14edb-127">Структура репозитория</span><span class="sxs-lookup"><span data-stu-id="14edb-127">Repository structure</span></span>

<span data-ttu-id="14edb-128">Демонстрационный проект представляет собой простую программу командной строки, которая использует аргумент командной строки для запроса Bing.</span><span class="sxs-lookup"><span data-stu-id="14edb-128">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="14edb-129">Он предназначен для платформы .NET Framework 4 и использует многие [пакеты библиотеки BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) и [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="14edb-129">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="14edb-130">Репозиторий имеет следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="14edb-130">The structure of the repository looks as follows:</span></span>

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

<span data-ttu-id="14edb-131">Как вы видите, мы не вернули папку `packages` и файлы `.targets`.</span><span class="sxs-lookup"><span data-stu-id="14edb-131">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="14edb-132">Однако мы вернули файл `nuget.exe`, так как он нужен во время сборки.</span><span class="sxs-lookup"><span data-stu-id="14edb-132">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="14edb-133">Согласно общепринятым соглашениям мы вернули его в общую папку `tools`.</span><span class="sxs-lookup"><span data-stu-id="14edb-133">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="14edb-134">Исходный код находится в папке `src`.</span><span class="sxs-lookup"><span data-stu-id="14edb-134">The source code is under the `src` folder.</span></span> <span data-ttu-id="14edb-135">Хотя в примере используется только одно решение, можно легко представить себе, что эта папка содержит несколько решений.</span><span class="sxs-lookup"><span data-stu-id="14edb-135">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="14edb-136">Пропуск файлов</span><span class="sxs-lookup"><span data-stu-id="14edb-136">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="14edb-137">В клиенте NuGet в настоящее время есть [известная ошибка](https://nuget.codeplex.com/workitem/4072), из-за которой клиент все же добавляет папку `packages` в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="14edb-137">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="14edb-138">Обходным решением является отключение интеграции с системой управления версиями.</span><span class="sxs-lookup"><span data-stu-id="14edb-138">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="14edb-139">Для этого в папке `.nuget`, которая находится в том же каталоге, что и решение, должен быть файл `Nuget.Config `.</span><span class="sxs-lookup"><span data-stu-id="14edb-139">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="14edb-140">Если этой папки еще нет, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="14edb-140">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="14edb-141">В файл [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) добавьте следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="14edb-141">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="14edb-142">Чтобы сообщить системе управления версиями, что мы не намереваемся возвращать папки **пакетов**, мы также добавили файлы игнорирования как для GIT (`.gitignore`), так и для системы управления версиями Team Foundation (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="14edb-142">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="14edb-143">В этих файлах описываются шаблоны файлов, которые не нужно возвращать.</span><span class="sxs-lookup"><span data-stu-id="14edb-143">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="14edb-144">Файл `.gitignore` выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="14edb-144">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages

<span data-ttu-id="14edb-145">Возможности файла `.gitignore` [весьма широки](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="14edb-145">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="14edb-146">Например, если вы не хотите возвращать все содержимое папки `packages`, но хотите вернуть файлы `.targets`, можно вместо этого использовать следующее правило:</span><span class="sxs-lookup"><span data-stu-id="14edb-146">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="14edb-147">При этом исключаются все папки `packages`, но включаются все содержащиеся в них файлы `.targets`.</span><span class="sxs-lookup"><span data-stu-id="14edb-147">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="14edb-148">Кстати, шаблон файлов `.gitignore`, специально предназначенный для потребностей разработчиков Visual Studio, можно найти [здесь](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="14edb-148">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="14edb-149">Система управления версиями Team Foundation поддерживает очень похожий механизм посредством файлов [TFIGNORE](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control).</span><span class="sxs-lookup"><span data-stu-id="14edb-149">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="14edb-150">Синтаксис практически такой же:</span><span class="sxs-lookup"><span data-stu-id="14edb-150">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages

## <a name="buildproj"></a><span data-ttu-id="14edb-151">build.proj</span><span class="sxs-lookup"><span data-stu-id="14edb-151">build.proj</span></span>

<span data-ttu-id="14edb-152">В примере процесс сборки будет достаточно прост.</span><span class="sxs-lookup"><span data-stu-id="14edb-152">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="14edb-153">Мы создадим проект MSBuild, который будет выполнять сборку всех решений, проверяя перед этим, восстановлены ли пакеты.</span><span class="sxs-lookup"><span data-stu-id="14edb-153">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="14edb-154">Этот проект будет иметь три стандартные цели: `Clean`, `Build` и `Rebuild`, а также новую цель `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="14edb-154">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="14edb-155">Цели `Build` и `Rebuild` зависят от `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="14edb-155">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="14edb-156">Таким образом, вы сможете выполнять `Build` и `Rebuild`, будучи уверенными в том, что пакеты восстановлены.</span><span class="sxs-lookup"><span data-stu-id="14edb-156">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="14edb-157">`Clean`, `Build` и `Rebuild` вызывают соответствующую цель MSBuild для всех файлов решения.</span><span class="sxs-lookup"><span data-stu-id="14edb-157">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="14edb-158">Цель `RestorePackages` вызывает программу `nuget.exe` для каждого файла решения.</span><span class="sxs-lookup"><span data-stu-id="14edb-158">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="14edb-159">Для этого применяется [функция пакетной обработки MSBuild](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="14edb-159">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="14edb-160">Результат выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="14edb-160">The result looks as follows:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a><span data-ttu-id="14edb-161">Настройка Team Build</span><span class="sxs-lookup"><span data-stu-id="14edb-161">Configuring Team Build</span></span>

<span data-ttu-id="14edb-162">Team Build предлагает различные шаблоны процессов.</span><span class="sxs-lookup"><span data-stu-id="14edb-162">Team Build offers various process templates.</span></span> <span data-ttu-id="14edb-163">Для этой демонстрации мы используем Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="14edb-163">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="14edb-164">В локальных установках Team Foundation Server процесс очень похож.</span><span class="sxs-lookup"><span data-stu-id="14edb-164">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="14edb-165">Шаблоны Team Build для GIT и системы управления версиями Team Foundation различаются, поэтому дальнейшие действия зависят от того, какую из этих систем вы используете.</span><span class="sxs-lookup"><span data-stu-id="14edb-165">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="14edb-166">В обоих случаях вам просто нужно выбрать build.proj в качестве проекта, сборку которого требуется выполнить.</span><span class="sxs-lookup"><span data-stu-id="14edb-166">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="14edb-167">Сначала рассмотрим шаблон процесса для GIT.</span><span class="sxs-lookup"><span data-stu-id="14edb-167">First, let's look at the process template for git.</span></span> <span data-ttu-id="14edb-168">В шаблоне на основе GIT сборка выбирается с помощью свойства `Solution to build`.</span><span class="sxs-lookup"><span data-stu-id="14edb-168">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Процесс сборки для GIT](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="14edb-170">Имейте в виду, что это свойство указывает на расположение в вашем репозитории.</span><span class="sxs-lookup"><span data-stu-id="14edb-170">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="14edb-171">Так как в нашем случае файл `build.proj` находится в корневой папке, мы просто использовали значение `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="14edb-171">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="14edb-172">Если бы файл сборки находился в папке `tools`, значение было бы `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="14edb-172">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="14edb-173">В шаблоне для системы управления версиями Team Foundation проект выбирается с помощью свойства `Projects`.</span><span class="sxs-lookup"><span data-stu-id="14edb-173">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Процесс сборки для системы управления версиями Team Foundation](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="14edb-175">В отличие от шаблона на основе GIT, система управления версиями Team Foundation поддерживает средство выбора (кнопка с многоточием справа).</span><span class="sxs-lookup"><span data-stu-id="14edb-175">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="14edb-176">Поэтому, чтобы избежать ошибок при вводе, мы рекомендуем воспользоваться им для выбора проекта.</span><span class="sxs-lookup"><span data-stu-id="14edb-176">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
