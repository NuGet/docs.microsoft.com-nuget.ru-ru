---
title: "Создание пакетов NuGet для платформы .NET Standard с помощью Visual Studio 2015 | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "Полное пошаговое руководство по созданию пакетов NuGet для платформы .NET Standard с использованием NuGet 3.x и Visual Studio 2015."
keywords: "создание пакета, пакеты .NET Standard, таблица сопоставления .NET Standard"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a912c27e1873d60426f2147995f69e2dcc433ca9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Создание пакетов .NET Standard с помощью Visual Studio 2015

*Применяется к NuGet 3.x. Сведения о работе с NuGet 4.x и более поздних версий см. в разделе [Создание пакетов для платформы .NET Standard с помощью Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md).*

[Библиотека .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library) представляет собой формальную спецификацию интерфейсов API .NET, которые должны быть доступны во всех средах выполнения .NET, что позволяет повысить степень унификации экосистемы .NET. Библиотека .NET Standard определяет унифицированный набор API-интерфейсов библиотеки базовых классов (BCL) для реализации всеми платформами .NET независимо от рабочей нагрузки. Таким образом, разработчики могут создавать переносимые библиотеки классов, которые могут использоваться во всех средах выполнения .NET, что позволяет свести к минимуму число директив условной компиляции, предназначенных для конкретных платформ, в общем коде либо полностью исключить их.

В этом руководстве приводятся пошаговые инструкции по созданию пакета nuget для библиотеки .NET Standard 1.4. Этот пакет будет работать на платформах .NET Framework 4.6.1, .NET Core, Mono/Xamarin и универсальной платформе Windows 10. Дополнительные сведения см. в разделе [Таблица сопоставления .NET Standard](#net-standard-mapping-table) далее в этой статье.

1. [Предварительные требования](#pre-requisites)
1. [Создание проекта для библиотеки классов](#create-the-class-library-project)
1. [Создание и изменение файла NUSPEC](#create-and-update-the-nuspec-file)
1. [Упаковка компонента](#package-the-component)
1. [Дополнительные параметры](#additional-options)
1. [Таблица сопоставления .NET Standard](#net-standard-mapping-table)
1. [Связанные статьи](#related-topics)


## <a name="pre-requisites"></a>Предварительные требования

1. Visual Studio 2015. Установите бесплатный выпуск Community с сайта [visualstudio.com](https://www.visualstudio.com/). Вы также можете использовать выпуски Professional и Enterprise.
1. .NET Core. Установите .NET Core вместе с шаблонами и другими средствами для Visual Studio 2015 с веб-страницы [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).
1. Интерфейс командной строки NuGet. Скачайте последнюю версию nuget.exe на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор. Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.

> [!Note]
> nuget.exe является программой интерфейса командной строки, а не установщиком, поэтому сохраните скачиваемый из браузера файл, но не запускайте его.



## <a name="create-the-class-library-project"></a>Создание проекта для библиотеки классов

1. В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > Windows**, выберите **Библиотека классов (переносимая)**, измените имя на "AppLogger" и нажмите кнопку "ОК".

    ![Создание нового проекта для библиотеки классов](media/NetStandard-NewProject.png)

1. В диалоговом окне **Добавление переносимой библиотеки классов** выберите параметры `.NET Framework 4.6` и `ASP.NET Core 1.0`.
1. Щелкните правой кнопкой мыши `AppLogger (Portable)` в обозревателе решений, выберите **Свойства**, перейдите на вкладку **Библиотека** и щелкните **Нацелить на стандартную платформу .NET** в разделе **Нацеливание**. Появится запрос на подтверждение, после которого вы можете выбрать `.NET Standard 1.4` в раскрывающемся списке:

    ![Настройка нацеливания на платформу .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Перейдите на вкладку **Построение**, в разделе **Конфигурация** выберите `Release`, после чего установите флажок **XML-файл документации**.
1. Добавьте собственный код для компонента, например:

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. Выполните построение проекта с использованием конфигурации выпуска и убедитесь, что файлы DLL и XML создаются в папке bin\Release.

## <a name="create-and-update-the-nuspec-file"></a>Создание и изменение файла NUSPEC

1. Откройте командную строку, перейдите в папку, содержащую папку `AppLogg.csproj` (на один уровень ниже места расположения файла `.sln`) и выполните команду NuGet `spec`, чтобы создать первичный файл `AppLogger.nuspec`:

```
nuget spec
```

1. Откройте файл `AppLogger.nuspec` в редакторе и измените его содержимое так, как показано ниже, заменив YOUR_NAME на соответствующее значение. Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Кроме того, обратите внимание на то, что необходимо изменить теги authors и description, иначе на этапе упаковки произойдет ошибка.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. Добавьте файл базовой сборки `.nuspec`, а именно DLL-файл библиотеки и XML-файл IntelliSense:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. Щелкните решение правой кнопкой мыши и выберите **Построить решение**, чтобы создать все файлы пакета.


## <a name="package-the-component"></a>Упаковка компонента

Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду `pack`:

```
nuget pack AppLogger.nuspec
```

Будет создан файл `AppLogger.YOUR_NAME.1.0.0.nupkg`. Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, вы увидите следующее содержимое:

![Пакет AppLogger в обозревателе пакетов NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> Файл `.nupkg` — это просто ZIP-файл с другим расширением. Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.

Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../create-packages/publish-a-package.md).

Обратите внимание, что команда `pack` требует наличия Mono 4.4.2 в Mac OS X и не работает в системах Linux. На компьютерах Mac также необходимо преобразовать пути в формате Windows, указанные в файле `.nuspec`, в формат Unix.

## <a name="additional-options"></a>Дополнительные параметры

В следующих разделах описываются дополнительные возможности, доступные при создании пакета NuGet:

- [Объявление зависимостей](#declaring-dependencies)
- [Поддержка нескольких целевых платформ](#supporting-multiple-target-frameworks)
- [Добавление целевых объектов и свойств MSBuild](#adding-targets-and-props-for-msbuild)
- [Создание локализованных пакетов](#creating-localized-packages)
- [Добавление файла сведений](#adding-a-readme)

### <a name="declaring-dependencies"></a>Объявление зависимостей

Если вы используете зависимости от других пакетов NuGet, их следует перечислить в элементе `<dependencies>` с элементами `<group>`. Например, чтобы объявить зависимость от NewtonSoft.Json 8.0.3 или более поздней версии, добавьте следующий код:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Синтаксис атрибута *version* в этом случае указывает, что приемлемыми являются версия 8.0.3 или более поздние. Инструкции по указанию других диапазонов версий см. в разделе [Управление версиями пакета](../reference/package-versioning.md).

### <a name="supporting-multiple-target-frameworks"></a>Поддержка нескольких целевых платформ

Предположим, вам необходимо использовать преимущество API платформы .NET Framework 4.6.2, которое недоступно на платформе .NET Standard 1.4. Для этого сначала необходимо обеспечить компиляцию библиотеки для .NET 4.6.2 с использованием условной компиляции или общих проектов. (В Visual Studio вы можете создать проект NetCore, добавить нужную платформу в раздел управления несколькими платформами, после чего выполнить построение.) Затем следует создать пакет, используя простую методику с применением рабочего каталога на основе соглашения, как показано ниже:

1. В корневой папке проекта, содержащей файл `.nuspec`, создайте папку с именем `lib`.
1. В папке `lib` создайте папку для каждой платформы, поддержку которой требуется реализовать:

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. В файл `.nuspec` добавьте узел `files` под узлом `package` и задайте ссылки на файлы в папке `lib`, используя подстановочные знаки. **Примечание**. В методике с применением рабочего каталога на основе соглашения не поддерживаются замены маркеров, поэтому необходимо заменить их литеральными значениями:

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Создайте пакет снова, используя `nuget pack AppLogger.spec`.

Дополнительные сведения об использовании этого метода см. в разделе [Поддержка нескольких версий платформы .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)

### <a name="adding-targets-and-props-for-msbuild"></a>Добавление целевых объектов и свойств MSBuild

В некоторых случаях в проекты, использующие пакет, необходимо добавить пользовательские целевые объекты сборки или свойства, например, если во время сборки должно запускаться пользовательское средство или процесс. Это можно сделать, добавив файлы в папку `\build`, как описывается ниже. Когда диспетчер NuGet устанавливает пакет с файлами \build, он добавляет в файл проекта элемент MSBuild, указывающий на файлы с расширениями .targets и .props.

> [!Note]
> При использовании `project.json` целевые платформы не добавляются в проект, а предоставляются через файл `project.lock.json`.


1. В папке проекта, содержащей файл `.nuspec`, создайте папку с именем `build`.
1. В папке `build` создайте папки для каждой поддерживаемой платформы и поместите в них файлы `.targets` и `.props`:

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. В файл `.nuspec` добавьте узел `files` под узлом `package` и задайте ссылки на файлы в папке `build`, используя подстановочные знаки.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. Создайте пакет снова, используя `nuget pack AppLogger.nuspec`.

Дополнительные сведения см. в разделе [Включение в пакет свойств и целей MSBuild](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).


### <a name="creating-localized-packages"></a>Создание локализованных пакетов

Для создания локализованных версий библиотеки можно создать отдельные пакеты для каждого языкового стандарта или включить локализованные сборки ресурсов в один пакет. Далее показана реализация второго подхода для немецкого и итальянского языков:

1. В папке каждой целевой платформы в папке `lib` создайте папки для каждого поддерживаемого языка (кроме английского). В эти папки можно поместить сборки ресурсов и локализованные XML-файлы IntelliSense. Пример:

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. В файл `.nuspec` добавьте ссылки на эти файлы в узел `<files>`:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Создайте пакет снова, используя `nuget pack AppLogger.nuspec`.


### <a name="adding-a-readme"></a>Добавление файла сведений

Если включить файл `readme.txt` в корень пакета, Visual Studio будет отображать его при непосредственной установке пакета.

> [!Note]
> Файлы сведений не отображаются для пакетов, которые устанавливаются в качестве зависимостей, или для проектов .NET Core.


Чтобы сделать это, создайте файл `readme.txt`, поместите его в корневую папку проекта и задайте ссылку на него в файле `.nuspec`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a>Таблица сопоставления .NET Standard

|Имя платформы |Alias|
|--------------|-----|
|.NET Standard | netstandard| 1,0| 1.1| 1.2| 1.3| 1.4| 1.5| 1.6|
|.NET Core | netcoreapp| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| 1,0|
|.NET Framework| net| 4.5| 4.5.1| 4.6| 4.6.1| 4.6.2| 4.6.3|
|Платформы Mono и Xamarin| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;|
|Универсальная платформа Windows | uap| &#x2192;| &#x2192;| &#x2192;| &#x2192;|10.0|
|Windows| win| &#x2192;| 8.0| 8.1|
|Windows Phone| wpa| &#x2192;| &#x2192;|8.1|
|Windows Phone Silverlight| wp| 8.0|



## <a name="related-topics"></a>См. также

- [Справочник по файлу NUSPEC](../schema/nuspec.md)
- [Пакеты символов](../create-packages/symbol-packages.md)
- [Управление версиями пакета](../reference/package-versioning.md)
- [Поддержка нескольких версий платформы .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Включение в пакет свойств и целей MSBuild](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Создание локализованных пакетов](../create-packages/creating-localized-packages.md)
- [Документация по библиотеке .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library)
- [Перенос кода в .NET Core из .NET Framework](https://docs.microsoft.com/dotnet/articles/core/porting/index)
