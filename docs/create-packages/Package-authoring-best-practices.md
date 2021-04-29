---
title: Рекомендации по созданию пакетов
description: Общее рекомендации по созданию высококачественных пакетов NuGet.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 358e574339688514448b684aadc6911f9d83611f
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901451"
---
# <a name="package-authoring-best-practices"></a>Рекомендации по созданию пакетов

Это руководство содержит упрощенный справочник по созданию и публикации высококачественных пакетов для авторов пакетов NuGet. Основное внимание уделяется рекомендациям по работе с пакетами, связанными с метаданными и упаковкой. Более подробные рекомендации по созданию высококачественных библиотек см. в [руководстве по использованию библиотеки .NET с открытым кодом](/dotnet/standard/library-guidance/).

## <a name="types-of-recommendations"></a>Типы рекомендаций

В каждой статье приводится список рекомендаций таких типов: **Do**, **Consider**, **Avoid** и **Do not**. Тип рекомендации указывает на то, насколько строго следует ее придерживаться.

Рекомендациям **Do** нужно следовать практически всегда. Пример:

✔️ СЛЕДУЕТ включить краткое описание пакета, которое описывает его содержимое.

Рекомендациям типа **РЕКОМЕНДУЕТСЯ** обычно также нужно следовать, но могут быть и исключения:

✔ РЕКОМЕНДУЕТСЯ выбрать имя пакета NuGet с префиксом, который соответствует [критериям](../nuget-org/id-prefix-reservation.md) для резервирования префикса NuGet.

Рекомендации **Avoid** обычно относятся к нежелательным действиям, но иногда их можно нарушать.

❌ НЕЖЕЛАТЕЛЬНО использовать ссылки на пакеты NuGet, требующие указания точной версии.

Рекомендации **Do not** указывают на то, чего практически никогда не следует делать.

❌ НЕ СЛЕДУЕТ использовать свойство метаданных `LicenseUrl`.

## <a name="create-a-nuget-package"></a>Создание пакета NuGet

Последний рекомендуемый способ создания пакета NuGet — на основе [проекта в стиле пакета SDK](../resources/check-project-format.md). Свойства проекта в стиле пакета SDK, включая [целевую платформу](/dotnet/standard/frameworks) и [метаданные пакета](#package-metadata) определяются в [файле проекта](/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).

Создайте пакет из проекта в стиле пакета SDK, определив необходимые свойства и упаковку в [Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli) или [dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

✔️ СЛЕДУЕТ создать проект в стиле пакета SDK и создать (упаковать) пакет с помощью Visual Studio или dotnet CLI.

Более подробные инструкции по созданию пакетов, включая необходимые клиентские средства, примеры файлов проекта и команды, см. в статье [Создание пакета NuGet с помощью dotnet CLI](./creating-a-package-dotnet-cli.md).

Чтобы решить, на какие платформы .NET ориентироваться, ознакомьтесь с нашим [последним руководством по кросс-платформенной поддержке](/dotnet/standard/library-guidance/cross-platform-targeting).

## <a name="package-metadata"></a>Метаданные пакета

Метаданные — это базовый компонент любого пакета NuGet. Качество ваших метаданных может значительно повлиять на возможность обнаружения, удобство использования и надежность пакета.

В Visual Studio для указания метаданных пакета выберите Project > [имя проекта] Properties > Package. (Проект > Свойства [имя проекта] > Пакет).

Элементы метаданных пакета также могут быть [указаны непосредственно в файле проекта](./creating-a-package-msbuild.md#set-properties).

Ниже приведено сопоставление таблиц и описание доступных элементов метаданных пакета.

| Имя свойства Visual Studio                       | [Имя файла проекта или свойства MSBuild](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                            | [Имя свойства nuspec](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema)     | Описание                                                                                                           |
|-----------------------------------------------    |-----------------------------------------------------------------------------------------------------------------------------------------  |---------------------------------------------------------------------------------------------------    |-------------------------------------------------------------------------------------------------------------------    |
| [`Package id`](#package-id)                       | [`PackageId`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                             | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                          | Имя или идентификатор пакета.                                                                                       |
| [`Package version`](#package-version)             | [`PackageVersion`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                    | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                                | Версия пакета NuGet.                                                                                                |
| [`Authors`](#authors)                             | [`Authors`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                                   | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                                | Разделенный запятыми список авторов пакетов, часто с указанием имен отдельных пользователей или названия организации.           |
| [`Description`](#description)                     | [`Description`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                           | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                        | Описание пакета.                                                                                         |
| [`Copyright`](#copyright)                         | [`Copyright`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                             | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                            | Сведения об авторских правах для пакета.                                                                                    |
| [`Licensing - Expression`](#licensing)            | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)   | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)              | Выражение лицензии SPDX.                                                                                           |
| [`Licensing - File`](#licensing)                  | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)         | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                    | Путь к пользовательскому файлу лицензии.                                                                                        |
| [`Project URL`](#project-url)                     | `PackageProjectUrl`                                                                                                                       | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                          | URL-адрес домашней страницы проекта.                                                                                       |
| [`Icon File`](#icon)                              | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                    | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                      | Путь к файлу изображения значка пакета.                                                                                  |
| [`Repository URL`](#repository-type-and-url)      | [`RepositoryUrl`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                     | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)                      | URL-адрес репозитория, из которого был создан пакет.                                                               |
| [`Repository type`](#repository-type-and-url)     | [`RespositoryType`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                   | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)                     | Тип репозитория, на который указывает URL-адрес репозитория (например, git).                                                    |
| [`Tags`](#tags)                                   | [`PackageTags`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                                           | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                      | Разделенный пробелами список тегов и ключевых слов для описания пакета. Теги используются при поиске пакетов.     |
| [`Release notes`](#release-notes)                 | [`PackageReleaseNotes`](https://docs.microsoft.com/nuget/reference/msbuild-targets#pack-target)                                           | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                      | Разделенный пробелами список тегов и ключевых слов для описания пакета.                                                     |
### <a name="package-id"></a>Идентификатор пакета

При публикации совершенно нового пакета:

✔️ СЛЕДУЕТ выбрать уникальный идентификатор пакета, который отличается от идентификаторов существующих пакетов на сайте NuGet.org.
> Вы можете проверить, является ли идентификатор пакета уникальным, выполнив поиск идентификатора на сайте NuGet.org или проверив, существует ли следующая ссылка: https://www.nuget.org/packages/<package name\>.

✔ РЕКОМЕНДУЕТСЯ выбрать имя пакета NuGet с префиксом, который соответствует [критериям резервирования префикса](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) NuGet.
> Когда вы зарезервируете идентификатор префикса для пакета, отобразится галочка, указывающая на успешную проверку: ![изображение](media/Verified-check-mark.png)
> 
> Чтобы узнать больше, ознакомьтесь с [документацией по резервированию префикса идентификатора пакета](../nuget-org/id-prefix-reservation.md).

### <a name="package-version"></a>Версия пакета

✔ СЛЕДУЕТ использовать [SemVer](https://semver.org/) для управления версиями пакета NuGet.
> По сути это означает, что используется следующий формат: основная_версия.дополнительная_версия.исправление[-предварительный_выпуск].

✔️ СЛЕДУЕТ опубликовать пакет в виде пакета [предварительного выпуска](./prerelease-packages.md), если он не является стабильным или является предварительной версией.

Дополнительные рекомендации см. в [руководстве по управлению версиями библиотеки .NET](/dotnet/standard/library-guidance/versioning).

### <a name="authors"></a>Авторы

✔️ СЛЕДУЕТ использовать поле Author (Автор) для указания своего имени или названия организации.
> Например, если имя пользователя NuGet.org — m.ivanova и вы используете "Marina Ivanova" в этом поле, пользователям будет легче распознать автора. Если имя пользователя NuGet.org для организации — ContosoToolkit, название "Contoso Corporation" так же будет более узнаваемым и внушающим доверие.
### <a name="description"></a>Описание

✔️ СЛЕДУЕТ включить краткое описание пакета (до 4000 символов).
> Описание пакета — это один из наиболее значимых блоков информации при поиске NuGet. Обычно это первое, на что обращают внимание пользователи при определении того, подходит ли им такой пакет.

### <a name="copyright"></a>Copyright

✔️ РЕКОМЕНДУЕТСЯ защитить авторское право, указав "Copyright (c) <имя/компания\> <год\>".
>Уведомление об авторских правах означает, что вашу работу нельзя копировать без разрешения. Включение уведомления об авторских правах в пакет — это простая операция, которая не влечет никаких последствий.

Пример. Copyright (c) Contoso 2020

### <a name="licensing"></a>Лицензирование

✔️ СЛЕДУЕТ [включить выражение лицензии или файл лицензии в пакет](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> Проект без лицензии по умолчанию предусматривает [монопольное авторское право](https://choosealicense.com/no-permission/). Это означает, что вы не предоставили кому-либо разрешения на использование вашего проекта.

❌ НЕ СЛЕДУЕТ использовать устаревшее свойство метаданных `LicenseUrl`.
> Так вы создадите юридически неоднозначную ситуацию, ведь изменения лицензии в URL-адресе приведут к изменению отображаемой лицензии для предыдущих версий пакета.

#### <a name="if-your-package-is-open-source"></a>Если пакет имеет [открытый код](https://opensource.org/osd)

✔️ СЛЕДУЕТ [выбрать лицензию с открытым кодом](https://choosealicense.com/), чтобы сделать пакет открытым.
> *"Лицензии с открытым исходным кодом — это лицензии, которые соответствуют определению открытого исходного кода. По сути, они позволяют свободно использовать, изменять и распространять программное обеспечение".* — Open Source Initiative. Дополнительные сведения о программном обеспечении с открытым кодом и Open Source Initiative см. здесь: https://opensource.org/.

✔️ РЕКОМЕНДУЕТСЯ [включить выражение лицензии в пакет](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> Выражения лицензий являются наиболее понятными. Они информируют пользователей о том, могут ли они использовать ваш пакет или изменилась ли лицензия. 
> [!Note]
> NuGet.org принимает только лицензионные выражения для лицензий, утвержденных Open Source Initiative или Free Software Foundation.

#### <a name="if-your-package-is-not-open-source"></a>Если пакет не включает открытый код

✔️ СЛЕДУЕТ [добавить файл лицензии в пакет](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> В пакет можно включить любой файл лицензии (в формате TXT или MD), в том числе нестандартные лицензии. 

### <a name="project-url"></a>URL проекта

✔️ РЕКОМЕНДУЕТСЯ включить ссылку на связанный проект, репозиторий или веб-сайт компании.
> Сайт проекта должен предоставлять всю информацию о пакете. Обычно именно там пользователи будут искать документацию.

### <a name="icon"></a>Значок

✔️ РЕКОМЕНДУЕТСЯ [использовать значок для пакета](../reference/msbuild-targets.md#packing-an-icon-image-file), чтобы его можно было визуально отличить. Даже такое относительно небольшое улучшение положительно влияет на оценку пакета.
> Значки могут быть разными для отдельных пакетов, а также использовать фирменную символику.

✔️ СЛЕДУЕТ использовать изображение размером 128×128 пикселей с прозрачным фоном (в формате PNG), чтобы обеспечить оптимальное отображение.
> NuGet автоматически масштабирует изображение для клиента, в котором он отображается.

❌ НЕ СЛЕДУЕТ использовать устаревшее свойство метаданных `IconUrl`.

### <a name="repository-type-and-url"></a>Тип репозитория и URL-адрес

✔ РЕКОМЕНДУЕТСЯ настроить [Source Link](/dotnet/standard/library-guidance/sourcelink), чтобы автоматически добавить метаданные системы управления версиями в пакет NuGet и упростить отладку библиотеки.
> Source Link автоматически добавляет `Repository URL` и `Repository Type` в метаданные пакета. При этом также добавляется конкретная фиксация, связанная с версией пакета.

### <a name="tags"></a>Теги

✔️ СЛЕДУЕТ включить несколько тегов с ключевыми терминами, описывающими ваш пакет, чтобы улучшить обнаружение.
> Теги обрабатываются алгоритмом поиска NuGet.org и особенно полезны при наличии терминов, которые не включены в идентификатор пакета, но являются релевантными.

Например, при публикации пакета для записи строк в консоль можно включить следующее: "ведение журнала, журнал, консоль, строка, выходные данные".

### <a name="release-notes"></a>Заметки о выпуске

✔️ РЕКОМЕНДУЕТСЯ включать заметки о выпуске в каждое обновление с описанием внесенных изменений.
> Хотя для заметок о выпуске не требуется специальный формат, рекомендуется включить сведения о следующем:
>
> 1. Критические изменения
> 2. новые функции;
> 3. Исправления ошибок
> 
> Если вы уже отслеживаете заметки о выпуске или журнал изменений в репозитории, можно также включить ссылку на соответствующий файл.

## <a name="related-topics"></a>Связанные разделы

- [Создание и публикация пакета (dotnet CLI)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Создание и публикация пакета (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli)
