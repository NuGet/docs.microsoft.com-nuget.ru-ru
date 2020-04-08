---
title: Создание пакетов, содержащих сборки COM-взаимодействия
description: Здесь объясняется, как создавать пакеты, содержащие сборки COM-взаимодействия
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: de164b136a1636b89f674b8626613094fc53e04c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "75385576"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>Создание пакетов NuGet, содержащих сборки COM-взаимодействия

Пакеты, содержащие сборки COM-взаимодействия, должны включать в себя соответствующий [файл целей](creating-a-package.md#include-msbuild-props-and-targets-in-a-package), чтобы в проекты были добавлены правильные метаданные `EmbedInteropTypes` в формате PackageReference. По умолчанию метаданные `EmbedInteropTypes` всегда имеют значение false для всех сборок при использовании PackageReference, поэтому файл целей добавляет эти метаданные явным образом. Во избежание конфликтов имя цели должно быть уникальным. В идеале следует использовать сочетание имен пакета и внедряемой сборки, заменив им элемент `{InteropAssemblyName}` в приведенном ниже примере. (Пример см. также на странице [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop).)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Имейте в виду, что при использовании формата управления `packages.config` добавление ссылок на сборки из пакетов приводит к тому, что NuGet и Visual Studio проверяют наличие сборок COM-взаимодействия и присваивают свойству `EmbedInteropTypes` в файле проекта значение true. В этом случае целевые объекты переопределяются.

Кроме того, по умолчанию [ресурсы сборки не передаются транзитивно](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Пакеты, созданные описанным здесь способом, работают иначе, если они извлекаются в качестве транзитивной зависимости из проекта в ссылку на проект. Пользователь пакета может разрешить их передачу, изменив значение PrivateAssets по умолчанию так, чтобы сборка не включалась.

<a name="creating-the-package"></a>