---
title: Создание пакетов NuGet Packages для универсальной платформы Windows
description: Полное пошаговое руководство по созданию пакетов NuGet с помощью компонента среды выполнения Windows для универсальной платформы Windows.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: c5d5bf72b99f6c2fe1b0a708ddb314d5711bc73d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818286"
---
# <a name="create-uwp-packages"></a>Создание пакетов универсальной платформы Windows

[Универсальная платформа Windows (UWP)](https://developer.microsoft.com/windows) предоставляет единую платформу приложений для всех устройств с операционной системой Windows 10. В этой модели приложения UWP могут вызывать как интерфейсы API WinRT, общие для всех устройств, так и интерфейсы API (включая Win32 и .NET), относящиеся только к семейству устройств, на которых работает приложение.

В этом пошаговом руководстве вы создадите пакет NuGet с собственным компонентом UWP (включая элемент управления XAML), который можно использовать как в управляемых, так и в собственных проектах.

## <a name="prerequisites"></a>Предварительные требования

1. Visual Studio 2017 или Visual Studio 2015. Установите бесплатный выпуск Community 2017 с сайта [visualstudio.com](https://www.visualstudio.com/). Вы также можете использовать выпуски Professional и Enterprise.

1. Интерфейс командной строки NuGet. Скачайте последнюю версию `nuget.exe` на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор (скачивается сразу файл `.exe`). Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.

## <a name="create-a-uwp-windows-runtime-component"></a>Создание компонента среды выполнения Windows для UWP

1. В Visual Studio последовательно выберите **Файл > Создать > Проект**, разверните узел **Visual C++ > Windows > Универсальные**, выберите шаблон **Компонент среды выполнения Windows (универсальные приложения для Windows)**, измените имя на ImageEnhancer и нажмите кнопку "ОК". При появлении запроса оставьте значения свойств "Конечная версия" и "Минимальная версия" по умолчанию.

    ![Создание проекта "Компонент среды выполнения Windows" для UWP](media/UWP-NewProject.png)

1. В обозревателе решений щелкните проект правой кнопкой мыши, выберите пункты **Добавить > Новый элемент**, щелкните узел **Visual C++ > XAML**, выберите элемент **Элемент управления-шаблон**, измените имя на AwesomeImageControl.cpp и нажмите кнопку **Добавить**.

    ![Добавление нового элемента управления-шаблона XAML в проект](media/UWP-NewXAMLControl.png)

1. В обозревателе решений щелкните проект правой кнопкой мыши и выберите пункт **Свойства**. На странице "Свойства" разверните узел **Свойства конфигурации > C/C++** и щелкните элемент **Выходные файлы**. В области справа измените значение свойства **Создавать файлы XML-документации** на "Да".

    ![Установка свойства "Создавать файлы XML-документации" в значение "Да"](media/UWP-GenerateXMLDocFiles.png)

1. Теперь щелкните *решение* правой кнопкой мыши, выберите пункт **Пакетная сборка** и в открывшемся диалоговом окне установите три флажка в строках, соответствующих конфигурации отладки, как показано ниже. Благодаря этому при сборке создается полный набор артефактов для каждой из целевых систем, поддерживаемых Windows.

    ![Пакетная сборка](media/UWP-BatchBuild.png)

1. В диалоговом окне "Пакетная сборка" щелкните **Сборка**, чтобы проверить проект и создать выходные файлы, которые потребуются для пакета NuGet.

> [!Note]
> В этом пошаговом руководстве для пакета будут использоваться артефакты отладки. Если пакет не является отладочным, в диалоговом окне "Пакетная сборка" установите вместо этого флажки в строках, соответствующих конфигурации выпуска, и при выполнении последующих действий обращайтесь к полученным папкам выпуска.

## <a name="create-and-update-the-nuspec-file"></a>Создание и изменение файла NUSPEC

Чтобы создать исходный файл `.nuspec`, выполните три указанных ниже действия. В следующих разделах приводятся указания по другим необходимым изменениям.

1. Откройте командную строку и перейдите к папке, содержащей файл `ImageEnhancer.vcxproj` (это вложенная папка в папке с файлом решения).
1. Выполните команду NuGet `spec`, чтобы создать файл `ImageEnhancer.nuspec` (его имя будет соответствовать имени файла `.vcxproj`):

    ```cli
    nuget spec
    ```

1. Откройте файл `ImageEnhancer.nuspec` в редакторе и измените его содержимое так, как показано ниже, заменив YOUR_NAME на соответствующее значение. Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Кроме того, обратите внимание на то, что необходимо изменить теги author и description, иначе на этапе упаковки произойдет ошибка.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Если пакет будет общедоступным, обратите особое внимание на элемент `<tags>`, так как эти теги помогают найти ваш пакет и понять его назначение.

### <a name="adding-windows-metadata-to-the-package"></a>Добавление метаданных Windows в пакет

Компоненту среды выполнения Windows требуются метаданные, которые описывают все его общедоступные типы, что делает возможным использование компонента другими приложениями и библиотеками. Эти метаданные содержатся в файле WINMD, который создается при компиляции проекта и должен быть включен в пакет NuGet. В это же время создается XML-файл с данными IntelliSense, который также необходимо включить в пакет.

Добавьте следующий узел `<files>` в файл `.nuspec`:

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>Добавление содержимого XAML

Чтобы добавить элемент управления XAML вместе с компонентом, необходимо включить XAML-файл с шаблоном по умолчанию для элемента управления (который создается шаблоном проекта). Он также указывается в разделе `<files>`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a>Добавление библиотек, реализованных в машинном коде

В компоненте основная логика типа ImageEnhancer реализована в машинном коде, который содержится в различных сборках `ImageEnhancer.dll`, создаваемых для каждой целевой среды выполнения (ARM, x86 и x64). Чтобы включить их в пакет, добавьте ссылки на них и на связанные с ними PRI-файлы ресурсов в раздел `<files>`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>Добавление файла TARGETS

В проектах C++ и JavaScript, которые могут использовать ваш пакет NuGet, требуется файл TARGETS, в котором определяются необходимые файлы сборок и файлы WINMD. (В C# и Visual Basic это делается автоматически.) Чтобы создать этот файл, скопируйте приведенный ниже текст в файл `ImageEnhancer.targets` и сохраните его в той же папке, что и файл `.nuspec`. _Примечание_. Имя этого файла `.targets` должно совпадать с идентификатором пакета (например, элемент `<Id>` в файле `.nupspec`).

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

Затем добавьте ссылку на файл `ImageEnhancer.targets` в файле `.nuspec`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>Итоговый файл NUSPEC

Итоговый файл `.nuspec` должен выглядеть следующим образом (YOUR_NAME, и в этом случае необходимо заменить на соответствующее значение):

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Упаковка компонента

Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду `pack`:

```cli
nuget pack ImageEnhancer.nuspec
```

Будет создан `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, отобразится следующее содержимое:

![Пакет ImageEnhancer в обозревателе пакетов NuGet](media/UWP-PackageExplorer.png)

> [!Tip]
> Файл `.nupkg` — это просто ZIP-файл с другим расширением. Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.

Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>См. также

- [Справочник по файлу NUSPEC](../reference/nuspec.md)
- [Пакеты символов](../create-packages/symbol-packages.md)
- [Управление версиями пакета](../reference/package-versioning.md)
- [Поддержка нескольких версий платформы .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Включение в пакет свойств и целей MSBuild](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Создание локализованных пакетов](../create-packages/creating-localized-packages.md)
