---
title: Определение формата проекта
description: Описание способов определения формата проекта
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488483"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="4909e-103">Определение формата проекта</span><span class="sxs-lookup"><span data-stu-id="4909e-103">Identify the project format</span></span>

<span data-ttu-id="4909e-104">NuGet работает со всеми проектами .NET.</span><span class="sxs-lookup"><span data-stu-id="4909e-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="4909e-105">Но формат проекта (в стиле пакета SDK или не в стиле пакета SDK) определяет некоторые средства и методы, которые необходимо применять для использования и создания пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="4909e-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="4909e-106">В проектах в стиле пакета SDK используется атрибут [пакета SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="4909e-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="4909e-107">Важно указать тип проекта, так как методы и средства, применяемые для использования и создания пакетов NuGet, зависят от формата проекта.</span><span class="sxs-lookup"><span data-stu-id="4909e-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="4909e-108">Для проектов не в стиле пакета SDK методы и средства зависят также от того, преобразован ли проект в формат `PackageReference`.</span><span class="sxs-lookup"><span data-stu-id="4909e-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="4909e-109">Стиль проекта не зависит от метода, используемого для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="4909e-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="4909e-110">В следующей таблице представлен формат проекта по умолчанию и связанный с ним инструмент CLI, используемый при создании проекта с помощью Visual Studio 2017 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="4909e-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="4909e-111">Проект&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="4909e-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="4909e-112">Формат проекта по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4909e-112">Default project format</span></span> | <span data-ttu-id="4909e-113">Средство CLI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="4909e-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="4909e-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="4909e-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="4909e-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="4909e-115">.NET Standard</span></span> | <span data-ttu-id="4909e-116">Стиль пакета SDK</span><span class="sxs-lookup"><span data-stu-id="4909e-116">SDK-style</span></span> | [<span data-ttu-id="4909e-117">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="4909e-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="4909e-118">Проекты, созданные в версиях, которые выпущены до Visual Studio 2017, разработаны не в стиле пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="4909e-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="4909e-119">Используйте CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="4909e-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="4909e-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="4909e-120">.NET Core</span></span> | <span data-ttu-id="4909e-121">Стиль пакета SDK</span><span class="sxs-lookup"><span data-stu-id="4909e-121">SDK-style</span></span> | [<span data-ttu-id="4909e-122">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="4909e-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="4909e-123">Проекты, созданные в версиях, которые выпущены до Visual Studio 2017, разработаны не в стиле пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="4909e-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="4909e-124">Используйте CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="4909e-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="4909e-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4909e-125">.NET Framework</span></span> | <span data-ttu-id="4909e-126">Проекты не в стиле пакета SDK</span><span class="sxs-lookup"><span data-stu-id="4909e-126">Non-SDK-style</span></span> | [<span data-ttu-id="4909e-127">Интерфейс командной строки nuget.exe</span><span class="sxs-lookup"><span data-stu-id="4909e-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="4909e-128">Проекты .NET Framework, созданные с помощью других методов, можно преобразовать в стиль пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="4909e-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="4909e-129">Для этого воспользуйтесь [CLI dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="4909e-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="4909e-130">[Перенесенный](../consume-packages/migrate-packages-config-to-package-reference.md) проект .NET</span><span class="sxs-lookup"><span data-stu-id="4909e-130">[Migrated](../consume-packages/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="4909e-131">Проекты не в стиле пакета SDK</span><span class="sxs-lookup"><span data-stu-id="4909e-131">Non-SDK-style</span></span>| <span data-ttu-id="4909e-132">Создавайте пакеты с помощью [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="4909e-132">To create packages, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="4909e-133">Для создания пакетов рекомендуем использовать `msbuild -t:pack`.</span><span class="sxs-lookup"><span data-stu-id="4909e-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="4909e-134">Для других целей используйте [CLI dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="4909e-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="4909e-135">Перенесенные проекты не разработаны не в стиле SDK.</span><span class="sxs-lookup"><span data-stu-id="4909e-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="4909e-136">Проверка формата проекта</span><span class="sxs-lookup"><span data-stu-id="4909e-136">Check the project format</span></span>

<span data-ttu-id="4909e-137">Если вы не знаете, разработан ли проект в стиле пакета SDK, найдите атрибут SDK в элементе `<Project>` в файле проекта (для C# это файл \*.csproj).</span><span class="sxs-lookup"><span data-stu-id="4909e-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="4909e-138">Если такой атрибут есть, проект разработан в стиле пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="4909e-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="4909e-139">Проверка формата проекта в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4909e-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="4909e-140">При работе в Visual Studio можно быстро проверить формат проекта с помощью одного из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="4909e-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="4909e-141">В обозревателе решений щелкните проект правой кнопкой мыши и выберите команду **изменения имя_проекта.csproj**.</span><span class="sxs-lookup"><span data-stu-id="4909e-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="4909e-142">Этот параметр доступен для проектов, использующих атрибут стиля пакета SDK, только в версиях начиная с Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4909e-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="4909e-143">При использовании других версий применяйте другой метод.</span><span class="sxs-lookup"><span data-stu-id="4909e-143">Otherwise, use the other method.</span></span>

   ![Изменение файла проекта](media/edit-project-file.png)

   <span data-ttu-id="4909e-145">В файле проекта в стиле SDK отображается [атрибут пакета SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="4909e-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="4909e-146">В меню **Проект** выберите команду **Выгрузить проект** (или щелкните проект правой кнопкой мыши и выберите команду **Выгрузить проект**).</span><span class="sxs-lookup"><span data-stu-id="4909e-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="4909e-147">В файле этого проекта не будет отображаться атрибут пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="4909e-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="4909e-148">Значит, проект разработан не в стиле пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="4909e-148">It is not an SDK-style project.</span></span>

   ![Выгрузка проекта](media/unload-project.png)

   <span data-ttu-id="4909e-150">Затем щелкните правой кнопкой мыши выгруженный проект и выберите команду **изменения имя_проекта. csproj.**</span><span class="sxs-lookup"><span data-stu-id="4909e-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="4909e-151">См. также раздел</span><span class="sxs-lookup"><span data-stu-id="4909e-151">See also</span></span>

- [<span data-ttu-id="4909e-152">Создание пакетов .NET Standard с помощью CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="4909e-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="4909e-153">Создание пакетов .NET Standard с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4909e-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="4909e-154">Создание и публикация пакета .NET Framework (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4909e-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="4909e-155">Объекты pack и restore NuGet в качестве целевых объектов MSBuild</span><span class="sxs-lookup"><span data-stu-id="4909e-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
