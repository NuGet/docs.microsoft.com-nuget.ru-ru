---
title: Справочник по файлу NuGet packages.config | Документы Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: В проектах некоторых типов в файле packages.config содержится список пакетов NuGet, используемых в проекте.
keywords: файл NuGet packages.config, ссылки на пакеты NuGet, зависимости NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 38d4724d25476d372a936cb8ebf08e2b53fcf9f4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="24c36-104">Справочник по файлу packages.config</span><span class="sxs-lookup"><span data-stu-id="24c36-104">packages.config reference</span></span>

<span data-ttu-id="24c36-105">Файл `packages.config` используется в проектах некоторых типов для ведения списка пакетов, на которые ссылается проект.</span><span class="sxs-lookup"><span data-stu-id="24c36-105">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="24c36-106">Это позволяет NuGet легко восстанавливать зависимости проекта при переносе проекта на другой компьютер, например сервер сборки, без всех этих пакетов.</span><span class="sxs-lookup"><span data-stu-id="24c36-106">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="24c36-107">Схема</span><span class="sxs-lookup"><span data-stu-id="24c36-107">Schema</span></span>

<span data-ttu-id="24c36-108">Схема проста: после стандартного заголовка XML находится единственный узел `<packages>`, который содержит один или несколько элементов `<package>` (по одному на каждую ссылку).</span><span class="sxs-lookup"><span data-stu-id="24c36-108">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="24c36-109">Каждый элемент `<package>` может иметь указанные ниже атрибуты.</span><span class="sxs-lookup"><span data-stu-id="24c36-109">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="24c36-110">Атрибут</span><span class="sxs-lookup"><span data-stu-id="24c36-110">Attribute</span></span> | <span data-ttu-id="24c36-111">Обязательно</span><span class="sxs-lookup"><span data-stu-id="24c36-111">Required</span></span> | <span data-ttu-id="24c36-112">Описание</span><span class="sxs-lookup"><span data-stu-id="24c36-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24c36-113">идентификатор</span><span class="sxs-lookup"><span data-stu-id="24c36-113">id</span></span> | <span data-ttu-id="24c36-114">Да</span><span class="sxs-lookup"><span data-stu-id="24c36-114">Yes</span></span> | <span data-ttu-id="24c36-115">Идентификатор пакета, например Newtonsoft.json или Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="24c36-115">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="24c36-116">version</span><span class="sxs-lookup"><span data-stu-id="24c36-116">version</span></span> | <span data-ttu-id="24c36-117">Да</span><span class="sxs-lookup"><span data-stu-id="24c36-117">Yes</span></span> | <span data-ttu-id="24c36-118">Точная версия устанавливаемого пакета, например 3.1.1 или 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="24c36-118">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="24c36-119">Строка версии должна содержать по крайней мере три числа. Четвертое число и суффикс предварительной версии являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="24c36-119">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="24c36-120">Диапазоны не допускаются.</span><span class="sxs-lookup"><span data-stu-id="24c36-120">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="24c36-121">targetFramework</span><span class="sxs-lookup"><span data-stu-id="24c36-121">targetFramework</span></span> | <span data-ttu-id="24c36-122">Нет</span><span class="sxs-lookup"><span data-stu-id="24c36-122">No</span></span> | <span data-ttu-id="24c36-123">[Моникер целевой платформы (TFM)](target-frameworks.md), применяемый при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="24c36-123">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="24c36-124">При установке пакета первоначально задается целевая платформа проекта.</span><span class="sxs-lookup"><span data-stu-id="24c36-124">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="24c36-125">В результате элементы `<package>` могут иметь разные моникеры целевых платформ.</span><span class="sxs-lookup"><span data-stu-id="24c36-125">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="24c36-126">Например, если вы создаете проект для .NET 4.5.2, устанавливаемые на этом этапе пакеты будут использовать моникер целевой платформы net452.</span><span class="sxs-lookup"><span data-stu-id="24c36-126">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="24c36-127">Если в дальнейшем целевая платформа проекта будет изменена на .NET 4.6 и будут добавлены дополнительные пакеты, они начнут использовать моникер целевой платформы net46.</span><span class="sxs-lookup"><span data-stu-id="24c36-127">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="24c36-128">В случае несоответствия целевой платформы проекта и значений атрибутов `targetFramework` будут выдаваться предупреждения. В этом случае вы можете переустановить нужные пакеты.</span><span class="sxs-lookup"><span data-stu-id="24c36-128">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="24c36-129">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="24c36-129">allowedVersions</span></span> | <span data-ttu-id="24c36-130">Нет</span><span class="sxs-lookup"><span data-stu-id="24c36-130">No</span></span> | <span data-ttu-id="24c36-131">Допустимый диапазон версий пакета, применяемый во время обновления пакета (см. раздел [Ограничение версий для обновления](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)).</span><span class="sxs-lookup"><span data-stu-id="24c36-131">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="24c36-132">*Не* влияет на то, какой пакет устанавливается во время операции установки или восстановления.</span><span class="sxs-lookup"><span data-stu-id="24c36-132">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="24c36-133">Синтаксис см. в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="24c36-133">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="24c36-134">В пользовательском интерфейсе диспетчера пакетов также отключаются все версии за пределами допустимого диапазона.</span><span class="sxs-lookup"><span data-stu-id="24c36-134">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="24c36-135">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="24c36-135">developmentDependency</span></span> | <span data-ttu-id="24c36-136">Нет</span><span class="sxs-lookup"><span data-stu-id="24c36-136">No</span></span> | <span data-ttu-id="24c36-137">Если проект-потребитель сам создает пакет NuGet, присвоение значения `true` этому атрибуту зависимости предотвращает включение пакета при создании пакета-потребителя.</span><span class="sxs-lookup"><span data-stu-id="24c36-137">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="24c36-138">Значение по умолчанию — `false`.</span><span class="sxs-lookup"><span data-stu-id="24c36-138">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="24c36-139">Примеры</span><span class="sxs-lookup"><span data-stu-id="24c36-139">Examples</span></span>

<span data-ttu-id="24c36-140">Следующий файл `packages.config` содержит ссылки на две зависимости:</span><span class="sxs-lookup"><span data-stu-id="24c36-140">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="24c36-141">Приведенный ниже файл `packages.config` содержит ссылки на девять пакетов, однако пакет `Microsoft.Net.Compilers` не будет включен при выполнении сборки пакета-потребителя из-за атрибута `developmentDependency`.</span><span class="sxs-lookup"><span data-stu-id="24c36-141">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="24c36-142">Кроме того, в ссылке на пакет Newtonsoft.Json обновление ограничивается версиями 8.x и 9.x.</span><span class="sxs-lookup"><span data-stu-id="24c36-142">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
