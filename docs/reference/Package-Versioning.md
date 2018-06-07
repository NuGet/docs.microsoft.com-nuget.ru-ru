---
title: Справочник по версии пакета NuGet
description: Точные сведения о задании номера версий и диапазонов для других пакетов, от которого зависит от пакета NuGet и установка зависимостей.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: db529a4aa92f0f0bce0b52b21d2a01bf973d01f2
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817601"
---
# <a name="package-versioning"></a>Управление версиями пакета

Конкретный пакет всегда называется его идентификатором пакета и точный номер версии. Например [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org имеет несколько десятков определенные пакеты, доступные, начиная с версии *4.1.10311* до версии *6.1.3 размещается* (последняя стабильная выпуск) и широкий набор предварительных версий, например *6.2.0-beta1*.

При создании пакета, можно назначить определенный номер версии с суффиксом дополнительный текст предварительного выпуска. При использовании пакетов, с другой стороны, можно указать точный номер версии или диапазон допустимых версий.

В этом разделе.

- [Основные сведения о версии](#version-basics) включая суффиксы предварительного выпуска.
- [Диапазон версий и подстановочные знаки](#version-ranges-and-wildcards)
- [Номера нормализованную версию](#normalized-version-numbers)

## <a name="version-basics"></a>Основные сведения о версии

Определенный номер версии указывается в формате *основной.дополнительный.исправление [-суффикс]*, где компоненты имеют следующий смысл:

- *Основные*: критические изменения
- *Дополнительный номер*: новые возможности, но обратная совместимость
- *Исправление для*: исправления ошибок, связанных в обратной совместимости
- *-Суффикс* (необязательно): дефис следуют за строкой, указывающей на этапе предварительной версии (следующие [семантического управления версиями или SemVer 1.0 соглашение о](http://semver.org/spec/v1.0.0.html)).

**Примеры:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> NuGet.org отклоняет все отправка пакета не обеспечивает точный номер версии. Версия должна быть указана в `.nuspec` или файл проекта используется для создания пакета.

### <a name="pre-release-versions"></a>Предварительные версии

Технической точки зрения автору пакета можно использовать любую строку как суффикс для обозначения предварительной версии, как NuGet считает любую версию такого предварительного выпуска и делает без других интерпретации. То есть NuGet отображает полную версию строки в пользовательском Интерфейсе, независимо от участвует, оставляя Любая обработка значение суффикса потребителю.

С другой стороны, разработчики пакетов в целом следовать распознаваемым соглашения об именовании:

- `-alpha`: Альфа-версии, как правило, используется для экспериментов и работы процесса.
- `-beta`: бета-версия, которая обычно содержит полный набор функций для следующего запланированного выпуска, но может иметь известные ошибки;
- `-rc`: версия-кандидат, которая обычно может служить итоговой (стабильной), если не будут выявлены серьезные ошибки.

> [!Note]
> Поддерживает NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), поддерживающей предварительного выпуска чисел с помощью точечной нотации, как в *1.0.1-build.23*. В версиях NuGet, предшествующих 4.3.0, точечная нотация не поддерживается. Можно использовать в форме, как *1.0.1-build23*.

При разрешении ссылки на пакет, а также несколько версий пакета отличаются только суффикс, NuGet сначала выбирает версии без суффикса, а затем применяется приоритет к предварительным версиям в обратном алфавитном порядке. Например следующие версии будет выбрана в точной последовательности:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Семантического управления версиями 2.0.0

С помощью NuGet 4.3.0+ и версии 15,3 + 2017 г. Visual Studio, поддерживает NuGet [семантического управления версиями 2.0.0](http://semver.org/spec/v2.0.0.html).

Некоторые семантику SemVer v2.0.0 не поддерживаются в старых клиентах. NuGet считает, что версия пакета для конкретного v2.0.0 SemVer при выполнении любого из следующих инструкций:

- Метка предварительного выпуска разделенный точками, например, *1.0.0-alpha.1*
- Версия имеет сборки метаданных, например, *1.0.0+githash*

Nuget.org пакета определяется как пакет v2.0.0 SemVer при выполнении любого из следующих инструкций:

- Версия пакета собственные — совместимые v2.0.0 SemVer, но не SemVer версии 1.0.0 соответствующим, как указано выше.
- Любой диапазон версий пакета зависимостей имеет версию минимальное или максимальное значение, соответствующие v2.0.0 SemVer, но не SemVer версии 1.0.0 соответствующим, описанный выше; например *[1.0.0-alpha.1,)*.

При отправке пакета конкретного v2.0.0 SemVer в nuget.org пакет является невидимым для старых клиентов и доступны только к следующим клиентам NuGet:

- NuGet 4.3.0+
- Visual Studio 2017 г. версия 15,3 +
- Visual Studio 2015 с [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (2.0.0+ .NET SDK)

Сторонние клиенты:

- Страхование JetBrains
- Paket версии 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Диапазон версий и подстановочные знаки

Применительно к зависимости пакетов NuGet поддерживает нотации интервал для указания диапазонов версий, следующим образом:

| Notation | Примененное правило | Описание: |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Минимальная версия включительно |
| (1.0,) | x > 1.0 | Минимальная версия монопольного |
| [1.0] | x == 1.0 | Точного сопоставления версии |
| (,1.0] | x ≤ 1.0 | Максимальная версия включительно |
| (,1.0) | x < 1.0 | Максимальная версия монопольного |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Точный диапазон включительно |
| (1.0,2.0) | 1.0 < x < 2.0 | Точное монопольного диапазона |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Смешанный включительно минимальное и эксклюзивных Максимальная версия |
| (1.0)    | недействительные | недействительные |

При использовании формата PackageReference NuGet также поддерживает использование нотацию подстановочных знаков, \*основной, незначительное, исправление и частей предварительной версии суффикс числа. Подстановочные знаки не поддерживаются с `packages.config` формат.

> [!Note]
> Предварительные версии, не включаются при разрешении диапазон версий. Предварительные версии *,* включены при использовании подстановочного знака (\*). Диапазон версий *[1.0,2.0]*, например, не включает бета-версии 2.0, но в нотацию подстановочных знаков _2.0-*_ does. В разделе [выдачи 912](https://github.com/NuGet/Home/issues/912) Дополнительные сведения о предварительной версии подстановочные знаки.

### <a name="examples"></a>Примеры

Всегда указывайте версию или диапазон версий для зависимости пакетов в файлах проектов `packages.config` файлы, и `.nuspec` файлов. Без версии или диапазон версий, NuGet 2.8.x и более ранних версий выбирает последнюю версию пакета доступны при разрешении зависимостей, тогда как NuGet 3.x и более поздней версии выбирает самую раннюю версию пакета. Указание версии и версии, что диапазон позволяет избежать этой неопределенности.

#### <a name="references-in-project-files-packagereference"></a>Ссылки в файлы проекта (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Ссылки в `packages.config`:**

В `packages.config`, каждая зависимость отмечены точного `version` атрибут, который используется при восстановлении пакетов. `allowedVersions` Атрибут используется только во время операций обновления для ограничения версии, к которым могут быть обновлены пакета.

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**Ссылки в `.nuspec` файлов**

`version` Атрибута в `<dependency>` элемент описывает диапазон версий, допустимые для зависимости.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>Номера нормализованную версию

> [!Note]
> Это критическое изменение NuGet 3.4 и более поздних версий.

После получения пакетов из репозитория во время установки, переустановки или восстановления, NuGet 3.4 + обрабатывает номера версий следующим образом:

- Начальные нули удаляются из номеров версий:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Ноль в четвертой части номера версии будет пропущен.

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Эта нормализация не влияет на номера версий в пакеты отдельно. он действует как NuGet соответствует только версии при разрешении зависимостей.

Тем не менее репозитории NuGet пакет должен обрабатывать эти значения в так же, как NuGet во избежание дублирования версии пакета. Таким образом, содержащий версию репозиторий *1.0* пакета не также размещают версии *1.0.0* как отдельное пакет.
