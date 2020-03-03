---
title: Справочник по файлу пакетов NuGet. config
description: В проектах некоторых типов в файле packages.config содержится список пакетов NuGet, используемых в проекте.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 3665989d35d7362b30a106cf6b4ed0210619efee
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230583"
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="0fc7b-103">Справочник по файлу packages.config</span><span class="sxs-lookup"><span data-stu-id="0fc7b-103">packages.config reference</span></span>

<span data-ttu-id="0fc7b-104">Файл `packages.config` используется в проектах некоторых типов для ведения списка пакетов, на которые ссылается проект.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="0fc7b-105">Это позволяет NuGet легко восстанавливать зависимости проекта при переносе проекта на другой компьютер, например сервер сборки, без всех этих пакетов.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="0fc7b-106">При использовании `packages.config` обычно находится в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="0fc7b-107">Она автоматически создается при выполнении первой операции NuGet, но ее также можно создать вручную перед выполнением любой команды, например `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="0fc7b-108">Проекты, использующие [PackageReference](../consume-packages/Package-References-in-Project-Files.md) , не используют `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="0fc7b-109">Схема</span><span class="sxs-lookup"><span data-stu-id="0fc7b-109">Schema</span></span>

<span data-ttu-id="0fc7b-110">Схема проста: после стандартного заголовка XML находится единственный узел `<packages>`, который содержит один или несколько элементов `<package>` (по одному на каждую ссылку).</span><span class="sxs-lookup"><span data-stu-id="0fc7b-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="0fc7b-111">Каждый элемент `<package>` может иметь указанные ниже атрибуты.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="0fc7b-112">Атрибут</span><span class="sxs-lookup"><span data-stu-id="0fc7b-112">Attribute</span></span> | <span data-ttu-id="0fc7b-113">Обязательно</span><span class="sxs-lookup"><span data-stu-id="0fc7b-113">Required</span></span> | <span data-ttu-id="0fc7b-114">Описание</span><span class="sxs-lookup"><span data-stu-id="0fc7b-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0fc7b-115">id</span><span class="sxs-lookup"><span data-stu-id="0fc7b-115">id</span></span> | <span data-ttu-id="0fc7b-116">Да</span><span class="sxs-lookup"><span data-stu-id="0fc7b-116">Yes</span></span> | <span data-ttu-id="0fc7b-117">Идентификатор пакета, например Newtonsoft.json или Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="0fc7b-118">version</span><span class="sxs-lookup"><span data-stu-id="0fc7b-118">version</span></span> | <span data-ttu-id="0fc7b-119">Да</span><span class="sxs-lookup"><span data-stu-id="0fc7b-119">Yes</span></span> | <span data-ttu-id="0fc7b-120">Точная версия устанавливаемого пакета, например 3.1.1 или 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="0fc7b-121">Строка версии должна содержать по крайней мере три числа. Четвертое число и суффикс предварительной версии являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="0fc7b-122">Диапазоны не допускаются.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="0fc7b-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="0fc7b-123">targetFramework</span></span> | <span data-ttu-id="0fc7b-124">Нет</span><span class="sxs-lookup"><span data-stu-id="0fc7b-124">No</span></span> | <span data-ttu-id="0fc7b-125">[Моникер целевой платформы (TFM)](target-frameworks.md), применяемый при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="0fc7b-126">При установке пакета первоначально задается целевая платформа проекта.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="0fc7b-127">В результате элементы `<package>` могут иметь разные моникеры целевых платформ.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="0fc7b-128">Например, если вы создаете проект для .NET 4.5.2, устанавливаемые на этом этапе пакеты будут использовать моникер целевой платформы net452.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="0fc7b-129">Если в дальнейшем целевая платформа проекта будет изменена на .NET 4.6 и будут добавлены дополнительные пакеты, они начнут использовать моникер целевой платформы net46.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="0fc7b-130">В случае несоответствия целевой платформы проекта и значений атрибутов `targetFramework` будут выдаваться предупреждения. В этом случае вы можете переустановить нужные пакеты.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="0fc7b-131">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="0fc7b-131">allowedVersions</span></span> | <span data-ttu-id="0fc7b-132">Нет</span><span class="sxs-lookup"><span data-stu-id="0fc7b-132">No</span></span> | <span data-ttu-id="0fc7b-133">Допустимый диапазон версий пакета, применяемый во время обновления пакета (см. раздел [Ограничение версий для обновления](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)).</span><span class="sxs-lookup"><span data-stu-id="0fc7b-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="0fc7b-134">*Не* влияет на то, какой пакет устанавливается во время операции установки или восстановления.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="0fc7b-135">Синтаксис см. в разделе [Управление версиями пакета](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="0fc7b-135">See [Package versioning](../concepts/package-versioning.md#version-ranges) for syntax.</span></span> <span data-ttu-id="0fc7b-136">В пользовательском интерфейсе диспетчера пакетов также отключаются все версии за пределами допустимого диапазона.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="0fc7b-137">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="0fc7b-137">developmentDependency</span></span> | <span data-ttu-id="0fc7b-138">Нет</span><span class="sxs-lookup"><span data-stu-id="0fc7b-138">No</span></span> | <span data-ttu-id="0fc7b-139">Если проект-потребитель сам создает пакет NuGet, присвоение значения `true` этому атрибуту зависимости предотвращает включение пакета при создании пакета-потребителя.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="0fc7b-140">Значение по умолчанию — `false`.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="0fc7b-141">Примеры</span><span class="sxs-lookup"><span data-stu-id="0fc7b-141">Examples</span></span>

<span data-ttu-id="0fc7b-142">Следующий файл `packages.config` содержит ссылки на две зависимости:</span><span class="sxs-lookup"><span data-stu-id="0fc7b-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="0fc7b-143">Приведенный ниже файл `packages.config` содержит ссылки на девять пакетов, однако пакет `Microsoft.Net.Compilers` не будет включен при выполнении сборки пакета-потребителя из-за атрибута `developmentDependency`.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="0fc7b-144">Кроме того, в ссылке на пакет Newtonsoft.Json обновление ограничивается версиями 8.x и 9.x.</span><span class="sxs-lookup"><span data-stu-id="0fc7b-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
