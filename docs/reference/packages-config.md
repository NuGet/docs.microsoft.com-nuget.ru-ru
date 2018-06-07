---
title: Ссылка на файл packages.config NuGet
description: В проектах некоторых типов в файле packages.config содержится список пакетов NuGet, используемых в проекте.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 2019ce5961a8237fbda855cd7d5b42948808be3a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817841"
---
# <a name="packagesconfig-reference"></a>Справочник по файлу packages.config

Файл `packages.config` используется в проектах некоторых типов для ведения списка пакетов, на которые ссылается проект. Это позволяет NuGet легко восстанавливать зависимости проекта при переносе проекта на другой компьютер, например сервер сборки, без всех этих пакетов.

При использовании `packages.config` обычно находится в корне проекта. Автоматически создается при первой операции NuGet запускается, но можно также создать вручную перед выполнением каких-либо команд, таких как `nuget restore`.

Проекты, использующие [PackageReference](../consume-packages/Package-References-in-Project-Files.md) используют `packages.config`.

## <a name="schema"></a>Схема

Схема проста: после стандартного заголовка XML находится единственный узел `<packages>`, который содержит один или несколько элементов `<package>` (по одному на каждую ссылку). Каждый элемент `<package>` может иметь указанные ниже атрибуты.

| Атрибут | Обязательно | Описание: |
| --- | --- | --- |
| id | Да | Идентификатор пакета, например Newtonsoft.json или Microsoft.AspNet.Mvc. | 
| version | Да | Точная версия устанавливаемого пакета, например 3.1.1 или 4.2.5.11-beta. Строка версии должна содержать по крайней мере три числа. Четвертое число и суффикс предварительной версии являются необязательными. Диапазоны не допускаются. | 
| targetFramework | Нет | [Моникер целевой платформы (TFM)](target-frameworks.md), применяемый при установке пакета. При установке пакета первоначально задается целевая платформа проекта. В результате элементы `<package>` могут иметь разные моникеры целевых платформ. Например, если вы создаете проект для .NET 4.5.2, устанавливаемые на этом этапе пакеты будут использовать моникер целевой платформы net452. Если в дальнейшем целевая платформа проекта будет изменена на .NET 4.6 и будут добавлены дополнительные пакеты, они начнут использовать моникер целевой платформы net46. В случае несоответствия целевой платформы проекта и значений атрибутов `targetFramework` будут выдаваться предупреждения. В этом случае вы можете переустановить нужные пакеты. | 
| allowedVersions | Нет | Допустимый диапазон версий пакета, применяемый во время обновления пакета (см. раздел [Ограничение версий для обновления](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)). *Не* влияет на то, какой пакет устанавливается во время операции установки или восстановления. Синтаксис см. в разделе [Управление версиями пакета](../reference/package-versioning.md#version-ranges-and-wildcards). В пользовательском интерфейсе диспетчера пакетов также отключаются все версии за пределами допустимого диапазона. | 
| developmentDependency | Нет | Если проект-потребитель сам создает пакет NuGet, присвоение значения `true` этому атрибуту зависимости предотвращает включение пакета при создании пакета-потребителя. Значение по умолчанию — `false`. | 

## <a name="examples"></a>Примеры

Следующий файл `packages.config` содержит ссылки на две зависимости:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Приведенный ниже файл `packages.config` содержит ссылки на девять пакетов, однако пакет `Microsoft.Net.Compilers` не будет включен при выполнении сборки пакета-потребителя из-за атрибута `developmentDependency`. Кроме того, в ссылке на пакет Newtonsoft.Json обновление ограничивается версиями 8.x и 9.x.

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
