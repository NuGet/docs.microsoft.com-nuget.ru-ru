---
title: Создание пакетов NuGet .NET Standard или .NET Framework с помощью Visual Studio 2015
description: Полное пошаговое руководство по созданию пакетов NuGet для платформы .NET Standard и .NET Framework с помощью NuGet 3.x и Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 1198a781543e581f55740cc0ae5a212d3f8a8b61
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842441"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Создание пакетов .NET Standard или .NET Framework с помощью Visual Studio 2015

**Примечание.** Рекомендуем разрабатывать библиотеки .NET Standard с помощью Visual Studio 2017. Вы можете использовать и Visual Studio 2015, но средства .NET Core доступны только в предварительной пробной версии. Сведения о работе с NuGet 4.x или более поздних версий и Visual Studio 2017 см. в статье [Создание и публикация пакета с помощью Visual Studio (.NET Standard)](../quickstart/create-and-publish-a-package-using-visual-studio.md).

[Библиотека .NET Standard](/dotnet/articles/standard/library) представляет собой формальную спецификацию интерфейсов API .NET, которые должны быть доступны во всех средах выполнения .NET, что позволяет повысить степень унификации экосистемы .NET. Библиотека .NET Standard определяет унифицированный набор API-интерфейсов библиотеки базовых классов (BCL) для реализации всеми платформами .NET независимо от рабочей нагрузки. Это позволяет разработчикам создавать код, который можно использовать во всех средах выполнения .NET, а также позволяет свести к минимуму число директив условной компиляции, предназначенных для конкретных платформ, в общем коде либо полностью исключить их.

В этом руководстве приведены пошаговые инструкции по созданию пакета NuGet для библиотеки .NET Standard 1.4 или .NET Framework 4.6. Библиотека .NET Standard 1.4 работает на платформах .NET Framework 4.6.1, .NET Core, Mono/Xamarin и универсальной платформе Windows 10. Дополнительные сведения см. в разделе [Поддержка реализации .NET](/dotnet/standard/net-standard#net-implementation-support) (документация .NET). При необходимости вы можете выбрать другую версию библиотеки .NET Standard.

## <a name="prerequisites"></a>Предварительные требования

1. Visual Studio 2015 с обновлением 3
1. [Пакет SDK для .NET Core](https://www.microsoft.com/net/download/) (только .NET Standard)
1. Интерфейс командной строки NuGet. Скачайте последнюю версию nuget.exe на странице [nuget.org/downloads](https://nuget.org/downloads), сохранив ее в любом месте на ваш выбор. Затем добавьте это расположение в переменную среды PATH, если это еще не сделано.

    > [!Note]
    > nuget.exe является программой интерфейса командной строки, а не установщиком, поэтому сохраните скачиваемый из браузера файл, но не запускайте его.

## <a name="create-the-class-library-project"></a>Создание проекта для библиотеки классов

1. В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > Windows**, выберите **Библиотека классов (переносимая)** , измените имя на AppLogger и нажмите кнопку **ОК**.

    ![Создание нового проекта для библиотеки классов](media/NetStandard-NewProject.png)

1. В диалоговом окне **Добавление переносимой библиотеки классов** выберите параметры `.NET Framework 4.6` и `ASP.NET Core 1.0`. (Для платформы .NET Framework выберите любой подходящий параметр.)

1. Если библиотека создается для .NET Standard, щелкните правой кнопкой мыши `AppLogger (Portable)` в обозревателе решений, выберите **Свойства**, перейдите на вкладку **Библиотека** и щелкните **Нацелить на стандартную платформу .NET** в разделе **Нацеливание**. Затем появится подтверждение, после чего вы можете выбрать из раскрывающегося списка версию `.NET Standard 1.4` (или любую другую доступную):

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
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Установите конфигурацию "Выпуск", выполните сборку проекта и убедитесь, что файлы DLL и XML создаются в папке `bin\Release`.

## <a name="create-and-update-the-nuspec-file"></a>Создание и изменение файла NUSPEC

1. Откройте командную строку, перейдите в папку, содержащую папку `AppLogger.csproj` (на один уровень ниже места расположения файла `.sln`) и выполните команду NuGet `spec`, чтобы создать первичный файл `AppLogger.nuspec`:

    ```cli
    nuget spec
    ```

1. Откройте файл `AppLogger.nuspec` в редакторе и измените его содержимое так, как показано ниже, заменив YOUR_NAME на соответствующее значение. Значение `<id>` должно быть уникальным в пределах nuget.org (см. соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Кроме того, обратите внимание на то, что необходимо изменить теги author и description, иначе на этапе упаковки произойдет ошибка.

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. Добавьте файл базовой сборки `.nuspec`, а именно DLL-файл библиотеки и XML-файл IntelliSense:

    Для платформы .NET Standard появятся примерно такие записи:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    Для платформы .NET Framework появятся примерно такие записи:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Щелкните решение правой кнопкой мыши и выберите **Построить решение**, чтобы создать все файлы пакета.

### <a name="declaring-dependencies"></a>Объявление зависимостей

Если вы используете зависимости от других пакетов NuGet, перечислите их в элементе `<dependencies>` манифеста с элементами `<group>`. Например, чтобы объявить зависимость от NewtonSoft.Json 8.0.3 или более поздней версии, добавьте следующий код:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Синтаксис атрибута *version* в этом случае указывает, что приемлемыми являются версия 8.0.3 или более поздние. Инструкции по указанию других диапазонов версий см. в разделе [Управление версиями пакета](../reference/package-versioning.md).

### <a name="adding-a-readme"></a>Добавление файла сведений

Создайте файл `readme.txt`, поместите его в корневую папку проекта и задайте ссылку на него в файле `.nuspec`.

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

При установке этого пакета в проекте Visual Studio отображает `readme.txt`. Этот файл не отображается при установке в проектах .NET Core, а также для пакетов, устанавливаемых в качестве зависимости.

## <a name="package-the-component"></a>Упаковка компонента

Когда будет готов файл `.nuspec` со ссылками на все файлы, которые необходимо включить в пакет, можно выполнить команду `pack`:

```cli
nuget pack AppLogger.nuspec
```

Будет создан `AppLogger.YOUR_NAME.1.0.0.nupkg`. Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, отобразится следующее содержимое ( .NET Standard):

![Пакет AppLogger в обозревателе пакетов NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> Файл `.nupkg` — это просто ZIP-файл с другим расширением. Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.

Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../nuget-org/publish-a-package.md).

Обратите внимание, что команда `pack` требует наличия Mono 4.4.2 в Mac OS X и не работает в системах Linux. На компьютерах Mac также необходимо преобразовать пути в формате Windows, указанные в файле `.nuspec`, в формат Unix.

## <a name="related-topics"></a>См. также

- [Справочник по файлу NUSPEC](../reference/nuspec.md)
- [Поддержка нескольких версий платформы .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Включение в пакет свойств и целей MSBuild](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Создание локализованных пакетов](../create-packages/creating-localized-packages.md)
- [Пакеты символов](../create-packages/symbol-packages.md)
- [Управление версиями пакета](../reference/package-versioning.md)
- [Документация по библиотеке .NET Standard](/dotnet/articles/standard/library)
- [Перенос кода в .NET Core из .NET Framework](/dotnet/articles/core/porting/index)
