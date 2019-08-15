---
title: Ссылка на версию пакета NuGet
description: Точные сведения об указании номеров версий и диапазонов для других пакетов, от которых зависит пакет NuGet, и о том, как устанавливаются зависимости.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019996"
---
# <a name="package-versioning"></a>Управление версиями пакета

Конкретный пакет всегда называется идентификатором пакета и точным номером версии. Например, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) в NuGet.org содержит несколько десятков отдельных пакетов, от версии *4.1.10311* до версии *6.1.3* (последний стабильный выпуск) и различных предварительных версий, таких как *6.2.0-Beta1.* .

При создании пакета вы назначаете определенный номер версии с помощью необязательного текстового суффикса предварительной версии. При использовании пакетов, с другой стороны, можно указать либо точный номер версии, либо диапазон допустимых версий.

В этом разделе.

- [Основы версии](#version-basics) , включая суффиксы предварительной версии.
- [Диапазоны версий и подстановочные знаки](#version-ranges-and-wildcards)
- [Нормализованные номера версий](#normalized-version-numbers)

## <a name="version-basics"></a>Основные сведения о версии

Конкретный номер версии указан в формате *основной. дополнительный. patch [-суффикс]* , где компоненты имеют следующие значения:

- *Основной*: Критические изменения
- *Дополнительный номер*: новые функции; сохраняется обратная совместимость;
- *Исправление*: исправления ошибок; сохраняется обратная совместимость.
- *-Суффикс* (необязательно): дефис, за которым следует строка, обозначающая предварительную версию (следуя [правилам семантического управления версиями или SemVer 1,0](http://semver.org/spec/v1.0.0.html)).

**Примеров**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org отклоняет передачу пакетов, в которой отсутствует точный номер версии. Версия должна быть указана в `.nuspec` файле проекта или, который используется для создания пакета.

### <a name="pre-release-versions"></a>Предварительные версии

Технически говоря, создатели пакетов могут использовать любую строку в качестве суффикса, чтобы обозначить предварительную версию, так как NuGet рассматривает любую такую версию как предварительную и не делает других интерпретаций. Это значит, что NuGet отображает полную строку версии в любом используемом пользовательском интерфейсе, в результате чего любая интерпретация значения суффикса для потребителя.

С другой стороны, разработчики пакетов обычно следуют признанным соглашениям об именовании:

- `-alpha`: Альфа-выпуск, обычно используемый для выполнения и экспериментирования.
- `-beta`: бета-версия, которая обычно содержит полный набор функций для следующего запланированного выпуска, но может иметь известные ошибки;
- `-rc`: версия-кандидат, которая обычно может служить итоговой (стабильной), если не будут выявлены серьезные ошибки.

> [!Note]
> NuGet 4.3.0 + поддерживает [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), который поддерживает номера предварительных версий с точечной нотацией, как в *1.0.1-Build. 23*. В версиях NuGet, предшествующих 4.3.0, точечная нотация не поддерживается. Можно использовать форму, например *1.0.1-build23*.

При разрешении ссылок на пакеты и нескольких версий пакетов по суффиксу NuGet выбирает версию без суффикса, а затем применяет приоритет к предварительным версиям в обратный алфавитный порядок. Например, следующие версии будут выбраны в указанном порядке:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>2\.0.0 семантического управления версиями

С помощью NuGet 4.3.0 + и Visual Studio 2017 версии 15.3 + NuGet поддерживает [семантическую версию 2.0.0](http://semver.org/spec/v2.0.0.html).

Определенная семантика SemVer v 2.0.0 не поддерживается в старых клиентах. NuGet считает версию пакета SemVer v 2.0.0 конкретной, если выполняется одно из следующих условий:

- Метка предварительного выпуска отделяется точкой с запятой, например *1.0.0-Alpha. 1*
- Версия содержит метаданные сборки, например *1.0.0 + гисаш*

Для nuget.org пакет определяется как пакет SemVer v, если выполняется одно из следующих условий.

- Собственная версия пакета — SemVer v 2.0.0 соответствует требованиям, но не совместим с SemVer v 1.0.0, как определено выше.
- Любой из диапазонов версий зависимостей пакета имеет минимальную или максимальную версию, совместимую с SemVer v 2.0.0, но не совместимую с SemVer v 1.0.0, определенную выше. Например, *[1.0.0-Alpha. 1,)* .

При передаче пакета SemVer v 2.0.0 в nuget.org пакет невидим для старых клиентов и доступен только следующим клиентам NuGet:

- NuGet 4.3.0 +
- Visual Studio 2017 версии 15.3 +
- Visual Studio 2015 с [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - Команда dotnetcore. exe (пакет SDK для .NET 2.0.0 +)

Сторонние клиенты:

- JetBrains Rider
- Пакет версии 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Диапазоны версий и подстановочные знаки

При ссылке на зависимости пакетов NuGet поддерживает использование нотации интервала для указания диапазонов версий, как описано ниже.

| Notation | Примененное правило | Описание |
|----------|--------------|-------------|
| 1.0 | x ≥ 1,0 | Минимальная версия, включительно |
| (1.0,) | x > 1,0 | Минимальная версия, монопольная |
| [1.0] | x = = 1,0 | Точное соответствие версии |
| (,1.0] | x ≤ 1,0 | Максимальная версия, включительно |
| (,1.0) | x < 1,0 | Максимальная версия, монопольная |
| [1.0,2.0] | 1,0 ≤ x ≤ 2,0 | Точный диапазон, включительно |
| (1.0,2.0) | 1,0 < x < 2,0 | Точный диапазон, исключающий |
| [1.0,2.0) | 1,0 ≤ x < 2,0 | Смешанная включающая минимальная и эксклюзивная Максимальная версия |
| (1.0)    | недействительные | недействительные |

При использовании формата PackageReference NuGet также поддерживает использование нотации \*с подстановочными знаками, для основных, дополнительных, исправлений и предварительных версий суффиксов номера. Подстановочные знаки не поддерживаются `packages.config` в формате.

> [!Note]
> Диапазоны версий в PackageReference включают предварительные версии. В режиме с плавающей версией не разрешаются предварительные версии, кроме случая, когда они участвуют в. Сведения о состоянии соответствующего запроса функции см. в описании [проблемы 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Примеры

Всегда указывайте версию или диапазон версий для зависимостей пакетов в файлах проекта, `packages.config` файлах и `.nuspec` файлах. Без версии или диапазона версий, NuGet 2.8. x и более ранних версий выбирает последнюю доступную версию пакета при разрешении зависимости, тогда как NuGet 3. x и более поздних версий выбирает наименьшую версию пакета. Указание версии или диапазона версий позволяет избежать этой неопределенности.

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

В `packages.config`каждой зависимости указывается точный `version` атрибут, используемый при восстановлении пакетов. `allowedVersions` Атрибут используется только во время операций обновления, чтобы ограничить версии, в которые может быть обновлен пакет.

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

**Ссылки в `.nuspec` файлах**

`version` Атрибут`<dependency>` в элементе описывает версии диапазона, допустимые для зависимости.

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
> Это критическое изменение для NuGet 3,4 и более поздних версий.

При получении пакетов из репозитория во время операций установки, переустановки или восстановления NuGet 3.4 + обрабатывает номера версий следующим образом:

- Начальные нули удаляются из номеров версий:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Ноль в четвертой части номера версии будет опущен.

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`и `restore` операции нормализации версий везде, где это возможно. Для уже собранных пакетов эта нормализация не влияет на номера версий в самих пакетах. Он влияет только на то, как NuGet соответствует версиям при разрешении зависимостей.

Однако репозитории пакетов NuGet должны интерпретировать эти значения так же, как NuGet, чтобы предотвратить дублирование версий пакета. Таким образом, репозиторий, содержащий пакет версии *1,0* , не должен размещать версию *1.0.0* как отдельный и другой пакет.
