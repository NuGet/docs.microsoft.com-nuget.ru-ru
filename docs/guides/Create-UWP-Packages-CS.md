---
title: Создание пакетов NuGet для универсальной платформы Windows (C#)
description: Полное пошаговое руководство по созданию пакетов NuGet с помощью компонента среды выполнения Windows для универсальной платформы Windows C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 22df2cd6dc374ba265c79a019747191e797b774c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774280"
---
# <a name="create-uwp-packages-c"></a>Создание пакетов универсальной платформы Windows (C#)

[Универсальная платформа Windows (UWP)](/windows/uwp) предоставляет единую платформу приложений для всех устройств с операционной системой Windows 10. В этой модели приложения UWP могут вызывать как интерфейсы API WinRT, общие для всех устройств, так и интерфейсы API (включая Win32 и .NET), относящиеся только к семейству устройств, на которых работает приложение.

В этом пошаговом руководстве вы создадите пакет NuGet с компонентом UWP на C# (включая элемент управления XAML), который можно использовать как в управляемых, так и в собственных проектах.

## <a name="prerequisites"></a>предварительные требования

1. Visual Studio 2019. Установите бесплатный выпуск Community 2019 с сайта [visualstudio.com](https://www.visualstudio.com/). Вы также можете использовать выпуски Professional и Enterprise.

1. Интерфейс командной строки NuGet. Скачайте последнюю версию `nuget.exe` на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор (скачивается сразу файл `.exe`). Затем добавьте это расположение в переменную среды PATH, если это еще не сделано. [Дополнительные сведения](../reference/nuget-exe-cli-reference.md#windows).

## <a name="create-a-uwp-windows-runtime-component"></a>Создание компонента среды выполнения Windows для UWP

1. В Visual Studio последовательно выберите **Файл > Создать > Проект**, выполните поиск "uwp c#", выберите шаблон **Компонент среды выполнения Windows (универсальные приложения для Windows)** , нажмите кнопку "Далее", измените имя на ImageEnhancer и нажмите кнопку "Создать". При появлении запроса оставьте значения свойств "Конечная версия" и "Минимальная версия" по умолчанию.

    ![Создание проекта "Компонент среды выполнения Windows" для UWP](media/UWP-NewProject-CS.png)

1. В обозревателе решений щелкните проект правой кнопкой мыши, выберите пункты **Добавить > Новый элемент**, выберите элемент **Элемент управления-шаблон**, измените имя на AwesomeImageControl.cs и нажмите кнопку **Добавить**:

    ![Добавление нового элемента управления-шаблона XAML в проект](media/UWP-NewXAMLControl-CS.png)

1. В обозревателе решений щелкните проект правой кнопкой мыши и выберите пункт **Свойства**. На странице "Свойства" выберите вкладку **Сборка** и включите **файл документации XML**:

    ![Установка свойства "Создавать файлы XML-документации" в значение "Да"](media/UWP-GenerateXMLDocFiles-CS.png)

1. Теперь щелкните *решение* правой кнопкой мыши, выберите пункт **Пакетная сборка** и в открывшемся диалоговом окне установите пять флажков сборки в диалоговом окне, как показано ниже. Благодаря этому при сборке создается полный набор артефактов для каждой из целевых систем, поддерживаемых Windows.

    ![Пакетная сборка](media/UWP-BatchBuild-CS.png)

1. В диалоговом окне "Пакетная сборка" щелкните **Сборка**, чтобы проверить проект и создать выходные файлы, которые потребуются для пакета NuGet.

> [!Note]
> В этом пошаговом руководстве для пакета будут использоваться артефакты отладки. Если пакет не является отладочным, в диалоговом окне "Пакетная сборка" установите вместо этого флажки в строках, соответствующих конфигурации выпуска, и при выполнении последующих действий обращайтесь к полученным папкам выпуска.

## <a name="create-and-update-the-nuspec-file"></a>Создание и изменение файла NUSPEC

Чтобы создать исходный файл `.nuspec`, выполните три указанных ниже действия. В следующих разделах приводятся указания по другим необходимым изменениям.

1. Откройте командную строку и перейдите к папке, содержащей файл `ImageEnhancer.csproj` (это вложенная папка в папке с файлом решения).
1. Выполните команду [`NuGet spec`](../reference/cli-reference/cli-ref-spec.md), чтобы создать файл `ImageEnhancer.nuspec` (его имя будет соответствовать имени файла `.csroj`):

    ```cli
    nuget spec
    ```

1. Откройте файл `ImageEnhancer.nuspec` в редакторе и измените его содержимое так, как показано ниже, заменив YOUR_NAME на соответствующее значение. Не оставляйте никаких значений $propertyName$. Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Кроме того, обратите внимание на то, что необходимо изменить теги author и description, иначе на этапе упаковки произойдет ошибка.

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
        <copyright>Copyright 2020</copyright>
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
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
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

В компоненте основная логика типа ImageEnhancer реализована в машинном коде, который содержится в различных сборках `ImageEnhancer.winmd`, создаваемых для каждой целевой среды выполнения (ARM, ARM64, x86 и x64). Чтобы включить их в пакет, добавьте ссылки на них и на связанные с ними PRI-файлы ресурсов в раздел `<files>`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Упаковка компонента

Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду [`nuget pack`](../reference/cli-reference/cli-ref-pack.md):

```cli
nuget pack ImageEnhancer.nuspec
```

Будет создан `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, отобразится следующее содержимое:

![Пакет ImageEnhancer в обозревателе пакетов NuGet](media/UWP-PackageExplorer.png)

> [!Tip]
> Файл `.nupkg` — это просто ZIP-файл с другим расширением. Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.

Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Связанные разделы

- [Справочник по файлу NUSPEC](../reference/nuspec.md)
- [Пакеты символов](../create-packages/symbol-packages-snupkg.md)
- [Управление версиями пакета](../concepts/package-versioning.md)
- [Поддержка нескольких версий платформы .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Включение в пакет свойств и целей MSBuild](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Создание локализованных пакетов](../create-packages/creating-localized-packages.md)