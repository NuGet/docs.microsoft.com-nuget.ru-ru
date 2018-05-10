---
title: Создание пакетов NuGet для Xamarin (iOS, Android и Windows) с помощью Visual Studio 2015
description: Комплексное пошаговое руководство по созданию пакетов NuGet для Xamarin, использующих собственные API в iOS, Android и Windows.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: 1189151b04da6dc4c7b680f759b6a8ca7c5bd85f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a>Создание пакетов для Xamarin с помощью Visual Studio 2015

Пакет Xamarin содержит код, использующий собственные API в iOS, Android и Windows в зависимости от операционной системы во время выполнения. Хотя это несложно сделать, предпочтительнее позволить разработчикам использовать пакет из библиотек .NET Standard или PCL через общую контактную зону API.

В этом пошаговом руководстве с помощью Visual Studio 2015 вы создадите кроссплатформенный пакет NuGet, который можно использовать в проектах для мобильных устройств в Windows, iOS и Android.

1. [Необходимые компоненты](#prerequisites)
1. [Создание структуры проекта и кода абстракции](#create-the-project-structure-and-abstraction-code)
1. [Написание кода для конкретных платформ](#write-your-platform-specific-code)
1. [Создание и изменение файла NUSPEC](#create-and-update-the-nuspec-file)
1. [Упаковка компонента](#package-the-component)
1. [Связанные статьи](#related-topics)

## <a name="prerequisites"></a>Предварительные требования

1. Visual Studio 2015 с универсальной платформой Windows (UWP) и Xamarin. Установите бесплатный выпуск Community с сайта [visualstudio.com](https://www.visualstudio.com/). Вы также можете использовать выпуски Professional и Enterprise. Чтобы включить средства UWP и Xamarin, выберите "Выборочная установка" и задайте соответствующие параметры.
1. Интерфейс командной строки NuGet. Скачайте последнюю версию nuget.exe на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор. Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.

> [!Note]
> nuget.exe является программой интерфейса командной строки, а не установщиком, поэтому сохраните скачиваемый из браузера файл, но не запускайте его.

## <a name="create-the-project-structure-and-abstraction-code"></a>Создание структуры проекта и кода абстракции

1. Скачайте и запустите [расширение шаблонов подключаемого модуля для Xamarin](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) для Visual Studio. Эти шаблоны упрощают создание структуры проекта для этого пошагового руководства.
1. В Visual Studio выберите **Файл > Создать > Проект**, выполните поиск `Plugin`, выберите шаблон **Plugin for Xamarin** (Подключаемый модуль для Xamarin), измените имя на LoggingLibrary и нажмите кнопку "ОК".

    ![Новый проект пустого приложения (переносимое Xamarin.Forms) в Visual Studio](media/CrossPlatform-NewProject.png)

Полученное решение содержит два проекта PCL, а также различные проекты для конкретных платформ:

- PCL с именем `Plugin.LoggingLibrary.Abstractions (Portable)` определяет общий интерфейс (контактную зону API) компонента, в данном случае — интерфейс `ILoggingLibrary`, содержащийся в файле ILoggingLibrary.cs. Именно здесь вы можете определить интерфейс для библиотеки.
- Другой PCL `Plugin.LoggingLibrary (Portable)` содержит код в CrossLoggingLibrary.cs, который будет искать реализацию абстрактного интерфейса во время выполнения для конкретной платформы. В общем случае изменять этот файл не требуется.
- Каждый из проектов для конкретных платформ, таких как `Plugin.LoggingLibrary.Android`, содержит собственную реализацию интерфейса в его соответствующем файле LoggingLibraryImplementation.cs. Именно здесь вы можете создать код библиотеки.

По умолчанию файл ILoggingLibrary.cs проекта Abstractions содержит определение интерфейса, но не методы. В рамках этого пошагового руководства добавьте метод `Log` следующим образом:

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a>Написание кода для конкретных платформ

Чтобы реализовать интерфейс `ILoggingLibrary` и его методы для конкретной платформы, сделайте следующее:

1. Откройте файл `LoggingLibraryImplementation.cs` для проекта каждой платформы и добавьте необходимый код. Например (при использовании проекта `Plugin.LoggingLibrary.Android`):

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. Повторите эту реализацию в проектах для каждой платформы, которую требуется поддерживать.
1. Щелкните правой кнопкой мыши проект iOS, выберите пункт **Свойства**, откройте вкладку **Сборка** и удалите "\iPhone" из параметров **Выходной путь** и **Файл XML-документации**. Это необходимо лишь для более удобного выполнения последующих действий в данном пошаговом руководстве. Когда все будет готово, сохраните файл.
1. Щелкните правой кнопкой мыши решение, выберите **Диспетчер конфигураций...** и установите флажки **Сборка** для PCL и каждой поддерживаемой платформы.
1. Щелкните правой кнопкой мыши решение и выберите **Собрать решение**, чтобы проверить свою работу и создать артефакты, которые вы затем упакуете. Если возникают ошибки об отсутствующих ссылках, щелкните решение правой кнопкой мыши, выберите **Восстановить пакеты NuGet**, чтобы установить зависимости, и повторите сборку.

> [!Note]
> Чтобы выполнить сборку для iOS, необходим сетевой Mac, подключенный к Visual Studio, как описано в разделе [Введение в Xamarin.iOS для Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Если у вас нет доступного Mac, очистите проект iOS в диспетчере конфигураций (шаг 3 выше).

## <a name="create-and-update-the-nuspec-file"></a>Создание и изменение файла NUSPEC

1. Откройте командную строку, перейдите в папку `LoggingLibrary`, находящуюся на один уровень ниже места расположения файла `.sln`, и выполните команду NuGet `spec`, чтобы создать первичный файл `Package.nuspec`:

    ```cli
    nuget spec
    ```

1. Переименуйте этот файл на `LoggingLibrary.nuspec` и откройте его в редакторе.
1. Измените содержимое файла так, как показано ниже, заменив YOUR_NAME на соответствующее значение. Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Кроме того, обратите внимание на то, что необходимо изменить теги author и description, иначе на этапе упаковки произойдет ошибка.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> Вы можете добавить для версии пакета суффикс `-alpha`, `-beta` или `-rc`, чтобы пометить пакет как предварительную версию. Дополнительные сведения о предварительных версиях см. в разделе [Предварительные версии](../create-packages/prerelease-packages.md).

### <a name="add-reference-assemblies"></a>Добавление базовых сборок

Чтобы включить базовые сборки для конкретной платформы, добавьте следующий код в элемент `<files>` файла `LoggingLibrary.nuspec` соответствующим образом для поддерживаемых платформ:

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> Чтобы сократить имена файлов DLL и XML, щелкните правой кнопкой мыши любой заданный проект, откройте вкладку **Библиотека** и измените имена сборок.

### <a name="add-dependencies"></a>Добавление зависимостей

При наличии конкретных зависимостей для собственных реализаций укажите их с помощью элемента `<dependencies>` с элементами `<group>`, например:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

Например, следующий код задает iTextSharp в качестве зависимости для целевого объекта UAP:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Итоговый файл NUSPEC

Итоговый файл `.nuspec` должен выглядеть следующим образом (YOUR_NAME, и в этом случае необходимо заменить на соответствующее значение):

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a>Упаковка компонента

Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду `pack`:

```cli
nuget pack LoggingLibrary.nuspec
```

Будет создан файл `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, отобразится следующее содержимое:

![Пакет LoggingLibrary в обозревателе пакетов NuGet](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> Файл `.nupkg` — это просто ZIP-файл с другим расширением. Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.

Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>См. также

- [Справочник по файлу NUSPEC](../reference/nuspec.md)
- [Пакеты символов](../create-packages/symbol-packages.md)
- [Управление версиями пакета](../reference/package-versioning.md)
- [Поддержка нескольких версий платформы .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Включение в пакет свойств и целевых объектов MSBuild](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Создание локализованных пакетов](../create-packages/creating-localized-packages.md)