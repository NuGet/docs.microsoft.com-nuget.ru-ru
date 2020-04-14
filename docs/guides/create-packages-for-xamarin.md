---
title: Создание пакетов NuGet для Xamarin (iOS, Android и Windows) с помощью Visual Studio 2017 или 2019
description: Комплексное пошаговое руководство по созданию пакетов NuGet для Xamarin, использующих собственные API в iOS, Android и Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230906"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>Создание пакетов для Xamarin с помощью Visual Studio 2017 или 2019

Пакет Xamarin содержит код, использующий собственные API в iOS, Android и Windows в зависимости от операционной системы во время выполнения. Хотя это несложно сделать, предпочтительнее позволить разработчикам использовать пакет из библиотек .NET Standard или PCL через общую контактную зону API.

В этом пошаговом руководстве с помощью Visual Studio 2017 или 2019 вы создадите кроссплатформенный пакет NuGet, который можно использовать в проектах для мобильных устройств в Windows, iOS и Android.

1. [Предварительные требования](#prerequisites)
1. [Создание структуры проекта и кода абстракции](#create-the-project-structure-and-abstraction-code)
1. [Написание кода для конкретных платформ](#write-your-platform-specific-code)
1. [Создание и изменение файла NUSPEC](#create-and-update-the-nuspec-file)
1. [Упаковка компонента](#package-the-component)
1. [Связанные статьи](#related-topics)

## <a name="prerequisites"></a>предварительные требования

1. Visual Studio 2017 или 2019 с универсальной платформой Windows (UWP) и Xamarin. Установите бесплатный выпуск Community с сайта [visualstudio.com](https://www.visualstudio.com/). Вы также можете использовать выпуски Professional и Enterprise. Чтобы включить средства UWP и Xamarin, выберите "Выборочная установка" и задайте соответствующие параметры.
1. Интерфейс командной строки NuGet. Скачайте последнюю версию nuget.exe на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор. Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.

> [!Note]
> nuget.exe является программой интерфейса командной строки, а не установщиком, поэтому сохраните скачиваемый из браузера файл, но не запускайте его.

## <a name="create-the-project-structure-and-abstraction-code"></a>Создание структуры проекта и кода абстракции

1. Скачайте и запустите [расширение шаблонов кроссплатформенного подключаемого модуля .NET Standard](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) для Visual Studio. Эти шаблоны упрощают создание структуры проекта для этого пошагового руководства.
1. В Visual Studio 2017 выберите **Файл > Создать > Проект**, выполните поиск по запросу `Plugin`, выберите шаблон **Cross-Platform .NET Standard Library Plugin** (Подключаемый модуль для кроссплатформенной библиотеки .NET Standard), измените имя на LoggingLibrary и нажмите кнопку OK.

    ![Новый проект пустого приложения (переносимое Xamarin.Forms) в Visual Studio 2017](media/CrossPlatform-NewProject.png)

    В Visual Studio 2019 выберите **Файл > Создать > Проект**, выполните поиск по запросу `Plugin`, выберите шаблон **Cross-Platform .NET Standard Library Plugin** (Подключаемый модуль для кроссплатформенной библиотеки .NET Standard) и нажмите кнопку "Далее".

    ![Новый проект пустого приложения (переносимое Xamarin.Forms) в Visual Studio 2019](media/CrossPlatform-NewProject19-Part1.png)

    Измените имя на LoggingLibrary и щелкните "Создать".

    ![Новая конфигурация пустого приложения (переносимое Xamarin.Forms) в Visual Studio 2019](media/CrossPlatform-NewProject19-Part2.png)

Полученное решение содержит два общих проекта, а также различные проекты для конкретных платформ:

- Проект `ILoggingLibrary`, который содержится в файле `ILoggingLibrary.shared.cs`, определяет общий интерфейс (контактную зону API) компонента. Именно здесь вы можете определить интерфейс для библиотеки.
- Другой общий проект содержит код в `CrossLoggingLibrary.shared.cs`, который будет определять реализацию абстрактного интерфейса во время выполнения для конкретной платформы. В общем случае изменять этот файл не требуется.
- Каждый из проектов для конкретных платформ, таких как `LoggingLibrary.android.cs`, содержит собственную реализацию интерфейса в его соответствующих файлах `LoggingLibraryImplementation.cs` (VS 2017) или `LoggingLibrary.<PLATFORM>.cs` (VS 2019). Именно здесь вы можете создать код библиотеки.

По умолчанию файл ILoggingLibrary.shared.cs проекта `ILoggingLibrary` содержит определение интерфейса, но не методы. В рамках этого пошагового руководства добавьте метод `Log` следующим образом:

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
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

1. Откройте файл `LoggingLibraryImplementation.cs` (VS 2017) или `LoggingLibrary.<PLATFORM>.cs` (VS 2019) для проекта каждой платформы и добавьте необходимый код. Например (при использовании проекта платформы `Android`):

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

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
1. Щелкните правой кнопкой мыши решение и выберите **Собрать решение**, чтобы проверить свою работу и создать артефакты, которые вы затем упакуете. Если возникают ошибки об отсутствующих ссылках, щелкните решение правой кнопкой мыши, выберите **Восстановить пакеты NuGet**, чтобы установить зависимости, и повторите сборку.

> [!Note]
> Если вы используете Visual Studio 2019, перед тем как выбрать параметр **Восстановить пакеты NuGet** и попытаться выполнить перестроение, необходимо изменить версию `MSBuild.Sdk.Extras` на `2.0.54` в `LoggingLibrary.csproj`. Доступ к этому файлу можно получить только щелкнув правой кнопкой мыши проект (под решением) и выбрав `Unload Project`, после чего нужно щелкнуть правой кнопкой мыши выгруженный проект и выбрать `Edit LoggingLibrary.csproj`.

> [!Note]
> Чтобы выполнить сборку для iOS, необходим сетевой Mac, подключенный к Visual Studio, как описано в разделе [Введение в Xamarin.iOS для Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Если у вас нет доступного Mac, очистите проект iOS в диспетчере конфигураций (шаг 3 выше).

## <a name="create-and-update-the-nuspec-file"></a>Создание и изменение файла NUSPEC

1. Откройте командную строку, перейдите в папку `LoggingLibrary`, находящуюся на один уровень ниже места расположения файла `.sln`, и выполните команду NuGet `spec`, чтобы создать первичный файл `Package.nuspec`:

    ```cli
    nuget spec
    ```

1. Переименуйте этот файл на `LoggingLibrary.nuspec` и откройте его в редакторе.
1. Измените содержимое файла так, как показано ниже, заменив YOUR_NAME на соответствующее значение. Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Кроме того, обратите внимание на то, что необходимо изменить теги author и description, иначе на этапе упаковки произойдет ошибка.

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
        <copyright>Copyright 2018</copyright>
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
    <copyright>Copyright 2018</copyright>
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

Это действие создаст файл `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, отобразится следующее содержимое:

![Пакет LoggingLibrary в обозревателе пакетов NuGet](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> Файл `.nupkg` — это просто ZIP-файл с другим расширением. Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.

Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Связанные разделы

- [Справочник по файлу NUSPEC](../reference/nuspec.md)
- [Пакеты символов](../create-packages/symbol-packages.md)
- [Управление версиями пакета](../concepts/package-versioning.md)
- [Поддержка нескольких версий платформы .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Включение в пакет свойств и целей MSBuild](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Создание локализованных пакетов](../create-packages/creating-localized-packages.md)
