---
title: "Создание пакетов NuGet для платформы .NET Standard 2.0 с помощью Visual Studio 2017 | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "Полное пошаговое руководство по созданию пакетов NuGet для платформы .NET Standard 2.0 с использованием NuGet 4.x и Visual Studio 2017."
keywords: "создание пакета, пакеты .NET Standard, .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>Создание пакетов .NET Standard 2.0 с помощью Visual Studio 2017

*Применяется к NuGet 4.x+ и MSBuild 15.3 + в соответствии с обновлением 3 для Visual Studio 2017. Для более ранних версий Visual Studio 2017 эти инструкции можно применить к .NET Standard версий с 1.4 до 1.6, изменив свойство \<TargetFramework\>. Сведения о работе с NuGet 3.x+ см. в разделе [Создание пакетов для платформы .NET Standard с помощью Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

[Библиотека .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library) представляет собой формальную спецификацию интерфейсов API .NET, которые должны быть доступны во всех средах выполнения .NET, что позволяет повысить степень унификации экосистемы .NET. Библиотека .NET Standard определяет унифицированный набор API-интерфейсов библиотеки базовых классов (BCL) для реализации всеми платформами .NET независимо от рабочей нагрузки. Таким образом, разработчики могут создавать переносимые библиотеки классов, которые могут использоваться во всех средах выполнения .NET, что позволяет свести к минимуму число директив условной компиляции, предназначенных для конкретных платформ, в общем коде либо полностью исключить их.

В этом руководстве приведены пошаговые инструкции по созданию пакета NuGet для библиотеки .NET Standard 2.0 с использованием обновления 3 для Visual Studio 2017 и NuGet 4.0.

1. [Предварительные требования](#pre-requisites)
1. [Создание проекта для библиотеки классов](#create-the-netstandard-class-library-project)
1. [Изменение метаданных в CSPROJ-файле](#edit-metadata-in-the-csproj-file)
1. [Упаковка компонента](#package-the-component)
1. [Связанные статьи](#related-topics)

## <a name="pre-requisites"></a>Предварительные требования

Для прохождения этого руководства требуется обновление 3 для Visual Studio 2017 с рабочей нагрузкой **Кроссплатформенная разработка .NET Core**. Вы можете установить бесплатный выпуск Community с сайта [visualstudio.com](https://www.visualstudio.com/) либо использовать выпуск Professional или Enterprise.

Нужная рабочая нагрузка выглядит в Visual Studio Installer следующим образом:

![Рабочая нагрузка "Кроссплатформенная разработка .NET Core" в Visual Studio Installer](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>Создание проекта библиотеки классов .NET Standard

1. В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > .NET Standard**, выберите **Библиотека классов (.NET Standard)**, измените имя на "AppLogger" и нажмите кнопку "ОК".

    ![Создание нового проекта для библиотеки классов](media/NuGet4-02-NewProject.png)

1. Измените конфигурацию сборки на **Выпуск**.
1. Щелкните правой кнопкой мыши проект `AppLogger` в обозревателе решений и выберите пункт **Свойства**, откройте вкладку **Сборка**, установите флажок **Файл XML-документации** и задайте в качестве имени файла только `AppLogger.xml`. Сохраните проект.

1. Добавьте код в компонент, например, следующий (который лишь выводит сообщения на консоль):

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

1. Выполните сборку проекта с использованием конфигурации выпуска и убедитесь, что файлы DLL и XML создаются в папке `bin\Release\netstandard2.0`.

## <a name="edit-metadata-in-the-csproj-file"></a>Изменение метаданных в CSPROJ-файле

Для проектов NuGet 4.0 и .NET Core метаданные пакета содержатся непосредственно в файле `.csproj`, а не во внешних файлах, таких как `.nuspec`. Полное описание этих метаданных приведено в разделе [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../schema/msbuild-targets.md#pack-target).

1. Щелкните правой кнопкой мыши проект в обозревателе решений, выберите пункт **Изменить AppLogger.csproj** и измените первую группу свойств, чтобы включить сведения о пакете, например следующего вида:

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. Сохраните проект, щелкните решение правой кнопкой мыши и выберите пункт **Собрать решение**, чтобы снова создать все файлы пакета, на этот раз с правильными метаданными.


## <a name="package-the-component"></a>Упаковка компонента

NuGet 4.0 поддерживает целевой объект pack с помощью MSBuild версии 15.1+ (включая MSBuild 15.3, входящий в состав обновления 3 для Visual Studio 2017), если проект содержит необходимые метаданные пакета, добавленные в предыдущем разделе. Чтобы вызывать MSBuild таким образом, просто укажите целевой объект pack в командной строке в той же папке, где находится файл `.csproj`:

    msbuild /t:pack /p:Configuration=Release

Сведения о дополнительных возможностях использования `msbuild /t:pack`, таких как включение файлов содержимого, символов и исходного кода, см. в разделе [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../schema/msbuild-targets.md#pack-target).

В любом случае приведенная выше команда создает `AppLogger.YOUR_NAME.1.0.0.nupkg` в папке `bin\Release` по умолчанию при сборе этой конфигурации. Если опустить параметр `/p`, конфигурацией по умолчанию будет `Debug`. 

Если открыть файл в таком средстве, как [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), и развернуть все узлы, вы увидите следующее содержимое:

![Пакет AppLogger в обозревателе пакетов NuGet](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> Файл `.nupkg` — это просто ZIP-файл с другим расширением. Поэтому чтобы просмотреть содержимое пакета, можно просто изменить расширение `.nupkg` на `.zip`, но не забудьте восстановить расширение перед отправкой пакета на сайт nuget.org.

Чтобы предоставить доступ к пакету другим разработчикам, следуйте инструкциям в разделе [Публикация пакета](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>См. также

- Раздел [Ссылки на пакеты в файлах проекта](../consume-packages/package-references-in-project-files.md) подробно рассказывает, как описать пакет непосредственно в файле проекта.
- Раздел [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../schema/msbuild-targets.md) описывает все возможности использования `msbuild /t:pack` для создания пакета.
- [Документация по библиотеке .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library)
- [Перенос кода в .NET Core из .NET Framework](https://docs.microsoft.com/dotnet/articles/core/porting/index)
