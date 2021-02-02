---
title: Справочник по версиям пакета NuGet
description: Точные сведения об указании номеров и диапазонов версий для других пакетов, от которых зависит пакет NuGet, а также об установке зависимостей.
author: JonDouglas
ms.author: jodou
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 5ba7860fae1037c0c0eb4c55d2df12d98b1d77cf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775116"
---
# <a name="package-versioning"></a>Управление версиями пакета

При указании определенного пакета всегда используется его идентификатор и точный номер версии. Например, для [Entity Framework](https://www.nuget.org/packages/EntityFramework/) на сайте nuget.org доступно несколько десятков специальных пакетов, начиная с версии *4.1.10311* и заканчивая версией *6.1.3* (последний стабильный выпуск), а также множество предварительных версий, таких как *6.2.0-beta1*.

При создании пакета вы назначаете определенный номер версии с необязательным текстовым суффиксом предварительной версии. С другой стороны, при использовании пакетов вы можете указать либо точный номер версии, либо диапазон допустимых версий.

В этом разделе.

- [Основные сведения о версиях](#version-basics), включая информацию о суффиксах предварительных версий.
- [Диапазоны версий](#version-ranges)
- [Нормализованные номера версий](#normalized-version-numbers).

## <a name="version-basics"></a>Основные сведения о версиях

Номер определенной версии выглядит следующим образом: *Основной номер.Дополнительный номер.Исправление[-Суффикс]* . Компоненты номера имеют следующие значения:

- *Основной номер*: Критические изменения
- *Дополнительный номер*: новые функции; сохраняется обратная совместимость;
- *Исправление*: исправления ошибок; сохраняется обратная совместимость.
- *-Суффикс* (необязательно): дефис, за которым следует строка, обозначающая предварительную версию (в соответствии с [Семантическим версионированием (или соглашением SemVer 1.0)](https://semver.org/spec/v1.0.0.html)).

**Примеры**

```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> nuget.org отклоняет любую загрузку пакета, в которой отсутствует точный номер версии. Версия должна быть указана в `.nuspec` или файле проекта, с помощью которого был создан пакет.

### <a name="pre-release-versions"></a>Предварительные версии

С технической точки зрения, создатели пакетов могут использовать любую строку в качестве суффикса для обозначения предварительной версии, так как NuGet рассматривает любую такую версию как предварительную версию, не делая других интерпретаций. Это значит, что NuGet отображает полную строку версии в любом пользовательском интерфейсе, предоставляя потребителю возможность по-своему интерпретировать значение суффикса.

Тем не менее, разработчики пакетов обычно следуют общепризнанным соглашениям об именовании:

- `-alpha`. альфа-версия, обычно используемая для текущей работы и экспериментирования;
- `-beta`. бета-версия, которая обычно содержит полный набор функций для следующего запланированного выпуска, но может иметь известные ошибки;
- `-rc`. версия-кандидат, которая обычно может служить итоговой (стабильной), если не будут выявлены серьезные ошибки.

> [!Note]
> NuGet 4.3.0+ поддерживает соглашение [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), которое позволяет использовать номера предварительных версий с точечной нотацией, как в случае с *1.0.1-build.23*. В версиях NuGet, предшествующих 4.3.0, точечная нотация не поддерживается. Вы можете использовать такую форму, как *1.0.1-build23*.

При разрешении ссылок на пакеты и наличии нескольких версий пакета, отличающихся лишь суффиксом, NuGet сначала выбирает версию без суффикса, а затем применяет приоритет к предварительным версиям в обратном алфавитном порядке. Например, приведенные ниже версии будут выбраны в следующем порядке:

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a>Семантическое версионирование 2.0.0

В NuGet 4.3.0+ и Visual Studio 2017 версии 15.3+ NuGet поддерживает систему [Семантическое версионирование 2.0.0](https://semver.org/spec/v2.0.0.html).

Определенная семантика SemVer версии 2.0.0 не поддерживается в более старых клиентах. NuGet определяет версию пакета как соответствующую SemVer версии 2.0.0, если выполнено любое из следующих условий:

- Метка предварительной версии разделена точкой, например *1.0.0-alpha.1*.
- Версия содержит метаданные сборки, например *1.0.0+githash*.

Сайт nuget.org определяет пакет как SemVer версии 2.0.0, если выполнено любое из следующих условий:

- Собственная версия пакета совместима с SemVer версии 2.0.0, но не совместима с SemVer версии 1.0.0, как определено выше.
- Любой из диапазонов версий зависимостей пакета включает минимальную или максимальную версию, совместимую с SemVer версии 2.0.0, но не совместимую с системой SemVer версии 1.0.0, определенной выше, например, *[1.0.0-alpha.1,)* .

Если вы загрузите пакет, соответствующий SemVer версии 2.0.0, на сайт nuget.org, он будет невидим для более старых клиентов и доступен только для приведенных ниже клиентов NuGet:

- NuGet 4.3.0+;
- Visual Studio 2017 версии 15.3+;
- Visual Studio 2015 с [NuGet VSIX версии 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix);
- dotnet
  - dotnetcore.exe (пакета SDK для .NET 2.0.0+).

Сторонние клиенты:

- JetBrains Rider;
- Paket версии 5.0+.

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a>Диапазоны версий

Что касается зависимостей пакетов, NuGet поддерживает использование интервальной нотации для указания диапазонов версий, которые представлены следующим образом:

| Notation | Примененное правило | Описание |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Минимальная версия, включающая |
| (1.0,) | x > 1.0 | Минимальная версия, исключающая |
| [1.0] | x == 1.0 | Точное соответствие версии |
| (,1.0] | x ≤ 1.0 | Максимальная версия, включающая |
| (,1.0) | x < 1.0 | Максимальная версия, исключающая |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Точный диапазон, включающий |
| (1.0,2.0) | 1.0 < x < 2.0 | Точный диапазон, исключающий |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Смешанная включающая минимальная и исключающая максимальная версии |
| (1.0)    | недействительные | недействительные |

При использовании формата PackageReference NuGet также поддерживает применение гибкой нотации \* для основного и дополнительного номеров, а также для исправления и суффикса предварительной версии. В формате `packages.config` гибкие версии не поддерживаются. Если указана гибкая версия, правило предусматривает разрешение к высшей существующей версии, которая соответствует описанию. Примеры гибких версий и разрешений приведены ниже.

> [!Note]
> Диапазоны версий в PackageReference включают предварительные версии. По умолчанию плавающие версии не разрешают предварительные версии, если не указано обратное. Сведения о состоянии запроса соответствующей функции см. [на сайте GitHub](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297) (запрос 6434).

### <a name="examples"></a>Примеры

Всегда указывайте версию или диапазон версий для зависимостей пакетов в файлах проекта (`packages.config` и `.nuspec`). Без версии или диапазона версий NuGet 2.8.x и более ранние версии выбирают последнюю доступную версию пакета при разрешении зависимости, тогда как NuGet 3.x и более поздние версии выбирают самую раннюю версию пакета. Указав версию или диапазон версий, вы сможете избежать этой неопределенности.

#### <a name="references-in-project-files-packagereference"></a>Ссылки в файлах проекта (PackageReference)

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a>Разрешения гибких версий 

| Версия | Версии на сервере | Решение | Причина | Примечания |
|----------|--------------|-------------|-------------|-------------|
| * | 1.1.0 <br> 1.1.1 <br> 1.2.0 <br> 1.3.0-alpha  | 1.2.0 | Последняя стабильная версия. |
| 1.1.* | 1.1.0 <br> 1.1.1 <br> 1.1.2-alpha <br> 1.2.0-alpha | 1.1.1 | Последняя стабильная версия, соответствующая указанному шаблону.|
| * - * | 1.1.0 <br> 1.1.1 <br> 1.1.2-alpha <br> 1.3.0-beta  | 1.3.0-beta | Последняя версия (может быть нестабильной). | Доступно в Visual Studio версии 16.6, NuGet версии 5.6, пакете SDK для .NET Core версии 3.1.300. |
| 1.1.* - * | 1.1.0 <br> 1.1.1 <br> 1.1.2-alpha <br> 1.1.2-beta <br> 1.3.0-beta  | 1.1.2-beta | Последняя версия (может быть нестабильной), соответствующая шаблону. | Доступно в Visual Studio версии 16.6, NuGet версии 5.6, пакете SDK для .NET Core версии 3.1.300. |

**Ссылки в `packages.config`**

В `packages.config` каждая зависимость указана с точным атрибутом `version`, который используется при восстановлении пакетов. Атрибут `allowedVersions` используется только во время выполнения операций обновления, чтобы ограничить версии, до которых может быть обновлен пакет.

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

**Ссылки в файлах `.nuspec`**

Атрибут `version` в элементе `<dependency>` описывает версии диапазона, допустимые для зависимости.

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

## <a name="normalized-version-numbers"></a>Нормализованные номера версий

> [!Note]
> Это критическое изменение для NuGet 3.4 и более поздних версий.

При получении пакетов из репозитория во время выполнения операций установки, переустановки или восстановления NuGet 3.4+ обрабатывает номера версий следующим образом:

- Начальные нули удаляются из номеров версий:

  1.00 обрабатывается как 1.0, 1.01.1 обрабатывается как 1.1.1, а 1.00.0.1 обрабатывается как 1.0.0.1.

- Ноль в четвертой части номера версии будет опущен.

  1.0.0.0 обрабатывается как 1.0.0, а 1.0.01.0 обрабатывается как 1.0.1.

- Удалены метаданные сборки SemVer 2.0.0

  1.0.7+r3456 обрабатывается как 1.0.7.

При возможности операции `pack` и `restore` нормализуют версии. Что касается уже собранных пакетов, эта нормализация не влияет на номера версий в самих пакетах. Она повлияет только на способ сопоставления версий NuGet при разрешении зависимостей.

Однако репозитории пакетов NuGet должны обрабатывать эти значения так же, как NuGet, чтобы предотвратить дублирование версий пакетов. Таким образом, репозиторий, содержащий пакет версии *1.0*, не должен содержать версию *1.0.0* в качестве отдельного пакета.
