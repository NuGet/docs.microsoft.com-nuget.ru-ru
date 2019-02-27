---
title: Ссылка на пакет NuGet версии
description: Точные сведения об указании номеров версий и диапазонов для других пакетов, от которых зависит пакет NuGet, и способ установки зависимостей.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6407cd2ea5e5e7a9c9e2be679764a8a0d5dd9260
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852472"
---
# <a name="package-versioning"></a>Управление версиями пакета

Конкретный пакет всегда называются с помощью его идентификатора пакета и точный номер версии. Например [Entity Framework](https://www.nuget.org/packages/EntityFramework/) на сайте nuget.org имеет несколько десятков конкретных доступных пакетов, начиная с версии *4.1.10311* до версии *6.1.3* (последняя стабильная версия выпуск) и широкий набор предварительных версий, например *6.2.0-beta1*.

При создании пакета, можно назначить определенный номер версии с суффиксом дополнительный текст для предварительного выпуска. При использовании пакетов, с другой стороны, можно указать точный номер версии или диапазон допустимых версий.

В этом разделе.

- [Основные сведения о версии](#version-basics) включая суффиксы предварительной версии.
- [Диапазон версий и подстановочные знаки](#version-ranges-and-wildcards)
- [Номера нормализованную версию](#normalized-version-numbers)

## <a name="version-basics"></a>Основные сведения о версии

Определенный номер версии указывается в формате *основной_номер.дополнительный_номер.исправление [-суффикс]*, где компоненты имеют следующий смысл:

- *Основные*: Критические изменения
- *Дополнительный номер*: новые функции; сохраняется обратная совместимость;
- *Исправление*: исправления ошибок; сохраняется обратная совместимость.
- *-Суффикс* (необязательно): дефиса и строки в предварительной версии, обозначающая (ниже [семантического управления версиями или SemVer 1.0 соглашение](http://semver.org/spec/v1.0.0.html)).

**Примеры:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> NuGet.org отклоняет любые отправить пакет, который не имеет точный номер версии. Должна быть указана версия в `.nuspec` или файл проекта, используемый для создания пакета.

### <a name="pre-release-versions"></a>Предварительные версии

Говоря техническим языком, создатели пакета можно использовать любую строку как суффикс для обозначения предварительной версии, поскольку NuGet считает любой такой версии предварительной версии и делает без других интерпретации. Т. е участвует полной версии строки в любой пользовательский Интерфейс отображает NuGet, оставив Любая обработка значение суффикса объекту-получателю.

С другой стороны, разработчики пакетов соблюдаться общепринятых соглашений об именовании:

- `-alpha`: Альфа-версии, обычно используемых для ветви стадии и экспериментов.
- `-beta`: бета-версия, которая обычно содержит полный набор функций для следующего запланированного выпуска, но может иметь известные ошибки;
- `-rc`: версия-кандидат, которая обычно может служить итоговой (стабильной), если не будут выявлены серьезные ошибки.

> [!Note]
> NuGet 4.3.0+ поддерживает [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), который поддерживает номера предварительных с точечной нотацией, как показано на *1.0.1-build.23*. В версиях NuGet, предшествующих 4.3.0, точечная нотация не поддерживается. Можно использовать формат наподобие *1.0.1-build23*.

При разрешении ссылок на пакеты, а также несколько версий пакета отличаются только суффиксами, NuGet сначала выбирает версии без суффикса, а затем применяется приоритет к предварительным версиям в обратном алфавитном порядке. Например следующие версии будет выбрана в точной последовательности:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Семантического Версионирования 2.0.0

NuGet 4.3.0+ и Visual Studio 2017 версии 15.3 и более поздних, NuGet поддерживает [семантического Версионирования 2.0.0](http://semver.org/spec/v2.0.0.html).

Определенные семантики версии SemVer 2.0.0 не поддерживаются в старых клиентов. NuGet считает, что версия пакета, чтобы быть определенной v2.0.0 SemVer, если выполняется любое из следующих инструкций:

- Метка предварительной версии разделенные точками, например, *1.0.0-alpha.1*
- Версия имеет метаданных для построения, например, *1.0.0+githash*

Для nuget.org пакета определяется как пакет SemVer версии 2.0.0, если выполняется любое из следующих инструкций:

- Собственные версия пакета является совместимым v2.0.0 SemVer, но не о версиях SemVer 1.0.0 соответствует требованиям, как указано выше.
- Какой-либо из диапазонов версий пакета зависимостей имеет минимальную или максимальную версию, которая является совместимым v2.0.0 SemVer, но не о версиях SemVer 1.0.0 соответствует требованиям, определенным выше; например *[1.0.0-alpha.1,)*.

Если вы отправляете SemVer версии 2.0.0 пакет на сайте nuget.org, пакет невидимым для старых клиентов и доступны только следующих клиентов NuGet:

- NuGet 4.3.0+
- Visual Studio 2017 версии 15.3 и более поздних
- Visual Studio 2015 с [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (2.0.0+ пакета SDK для .NET)

Сторонние клиенты:

- JetBrains Rider
- Paket 5.0 и более поздних версиях

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Диапазон версий и подстановочные знаки

Применительно к зависимости пакетов NuGet поддерживает, используя интервал для указания диапазонов версий, выполняется следующим образом:

| Notation | Примененное правило | Описание: |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Минимальная версия, включительно |
| (1.0,) | x > 1.0 | Минимальная версия, эксклюзивные |
| [1.0] | x == 1.0 | Точное соответствие версии |
| (,1.0] | x ≤ 1.0 | Максимальная версия включительно |
| (,1.0) | x < 1.0 | Максимальная версия монопольного |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Точный диапазон, включительно |
| (1.0,2.0) | 1.0 < x < 2.0 | Точное монопольного диапазона |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Смешанный включительно минимальное и исключающие Максимальная версия |
| (1.0)    | недействительные | недействительные |

При использовании формата PackageReference, NuGet также поддерживает использование в нотацию подстановочных знаков \*, для основной, версии, исправления и суффикс предварительной версии части числа. Подстановочные знаки не поддерживаются с `packages.config` формат.

> [!Note]
> Предварительные версии не включаются при разрешении диапазон версий. Предварительные версии *являются* включены при использовании подстановочного знака (\*). Диапазон версий *[1.0,2.0]*, например, не поддерживает бета-версии 2.0, но в нотацию подстановочных знаков _2.0-*_ does. См. в разделе [выдавать 912](https://github.com/NuGet/Home/issues/912) Дополнительные сведения о подстановочных знаках предварительной версии.

### <a name="examples"></a>Примеры

Всегда указывайте версию или диапазон версий для зависимости пакетов в файлах проекта, `packages.config` файлы, и `.nuspec` файлы. Без версию или диапазон версий, NuGet 2.8.x и ранее выбирает последнюю версию пакета, доступные при разрешении зависимостей, тогда как NuGet 3.x и более поздней версии выбирает самую раннюю версию пакета. Указание версии или версии, что диапазон позволяет избежать этой неопределенностью.

#### <a name="references-in-project-files-packagereference"></a>Ссылки в файлах проекта (PackageReference)

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

В `packages.config`, каждая зависимость отмечены точного `version` атрибут, используемый при восстановлении пакетов. `allowedVersions` Атрибут используется только во время операций обновления для ограничения версий, к которым могут быть обновлены пакета.

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

`version` Атрибут в `<dependency>` элемент описывает диапазон версий, которые являются допустимыми для зависимости.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

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

После получения пакетов из репозитория во время установки, переустановки или восстановления NuGet 3.4 и более поздних обрабатывает номера версий следующим образом:

- Начальные нули удаляются из номера версий:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Ноль в четвертой части номера версии будет пропущено

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Эта нормализация не влияет на номера версий в пакетах отдельно. он затрагивает только, как NuGet соответствует версии при разрешении зависимостей.

Тем не менее репозиториями пакетов NuGet должен обрабатывать эти значения в так же, как NuGet во избежание дублирования версии пакета. Таким образом репозиторий, который содержит версию *1.0* пакета не должно также включать версии *1.0.0* как пакет и отличается.
