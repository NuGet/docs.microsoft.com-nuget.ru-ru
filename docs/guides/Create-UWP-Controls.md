---
title: "Упаковка элементов управления универсальной платформы Windows с помощью NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/14/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Описывается, как создавать пакеты NuGet, содержащие элементы управления универсальной платформы Windows, включая необходимые метаданные и вспомогательные файлы для конструкторов Visual Studio и Blend."
keywords: "элементы управления UWP NuGet, конструктор XAML в Visual Studio, конструктор Blend, пользовательские элементы управления"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1af5118eb71836d8b8bcfa8ff713d9fef3c86374
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>Создание элементов управления универсальной платформы Windows в виде пакетов NuGet

В Visual Studio 2017 вы можете использовать возможности добавления элементов управления универсальной платформы Windows (UWP) в пакеты NuGet. В данном руководстве рассматривается использование этих возможностей на примере [образца пакета ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). 

## <a name="prerequisites"></a>Предварительные требования

1. Visual Studio 2017
1. Умение [создавать пакеты UWP](create-uwp-packages.md)

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Добавление поддержки элементов управления XAML на панели элементов или в области ресурсов

Чтобы элемент управления XAML отображался на панели элементов конструктора XAML в Visual Studio и в области ресурсов Blend, создайте файл `VisualStudioToolsManifest.xml` в корне папки `tools` проекта пакета. Этот файл не требуется, если не нужно, чтобы элемент управления отображался на панели элементов или в области ресурсов.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

Файл имеет следующую структуру:

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

Здесь:

- *your_package_file* — имя файла элемента управления, например `ManagedPackage.winmd` (ManagedPackage — это произвольное имя, которое взято для примера и не имеет особого значения).
- *vs_category* — метка группы, в которой должен отображаться элемент управления на панели элементов в конструкторе Visual Studio. Элемент `VSCategory` необходим для отображения элемента управления на панели элементов.
- *blend_category* — метка группы, в которой должен отображаться элемент управления в области ресурсов конструктора Blend. Элемент `BlendCategory` необходим для отображения элемента управления в области ресурсов.
- *type_full_name_n* — полное имя каждого элемента управления, включая пространство имен, например `ManagedPackage.MyCustomControl`. Обратите внимание на то, что нотация с точкой используется как для управляемых, так и для собственных типов.

Если один пакет содержит несколько сборок элементов управления, можно включить несколько элементов `<File>` в элемент `<FileList>`. Вы также можете добавить несколько узлов `<ToolboxItems>` в один элемент `<File>`, чтобы упорядочить элементы управления по отдельным категориям.

В приведенном ниже примере элемент управления, реализованный в файле `ManagedPackage.winmd`, будет отображаться в Visual Studio и Blend в группе "Managed Package" (Управляемый пакет) и иметь имя MyCustomControl. Все эти имена являются произвольными.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Пример элемента управления в Visual Studio](media/UWP-control-vs-toolbox.png)

![Пример элемента управления в Blend](media/UWP-control-blend-assets.png)

> [!Note]
> Каждый элемент, который должен отображаться на панели элементов или в области ресурсов, необходимо указывать явным образом. При этом следует использовать формат `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Добавление пользовательских значков для элементов управления

Чтобы на панели элементов или в области ресурсов отображался пользовательский значок, добавьте изображение в свой проект или соответствующий проект `design.dll` с именем Namespace.ControlName.extension и выберите действие сборки "Внедренный ресурс". Поддерживаемые форматы: `.png`, `.jpg`, `.jpeg`, `.gif` и `.bmp`. Рекомендуемый размер изображения — 64 на 64 пикселя.

В приведенном ниже примере проект содержит файл изображения с именем ManagedPackage.MyCustomControl.png.

![Задание пользовательского значка в проекте](media/UWP-control-custom-icon.png)

> [!Note]
> Для собственных элементов управления значки следует добавлять в качестве ресурсов в проект `design.dll`.

## <a name="support-specific-windows-platform-versions"></a>Поддержка определенных версий платформы Windows

Пакеты UWP имеют свойства TargetPlatformVersion (TPV) и TargetPlatformMinVersion (TPMinV), которые определяют самую позднюю и самую раннюю версии ОС, в которых может быть установлено приложение. Кроме того, свойство TPV определяет версию пакета SDK, на основе которой создается приложение. Учитывайте эти свойства при разработке пакета UWP: использование интерфейсов API, которые выходят за пределы определенных в приложении версий платформы, приведет либо к сбою сборки, либо к ошибке приложения во время выполнения.

Например, предположим, что вы указали в качестве значения свойства TPMinV для пакета элементов управления юбилейное обновление Windows 10 (версия 10.0, сборка 14393), и вам необходимо сделать так, чтобы пакет использовался проектами UWP, предназначенными только для этой или более поздних версий. Чтобы пакет могли потреблять проекты UWP, необходимо упаковать элементы управления, используя следующие имена папок:

    \lib\uap10.0\*
    \ref\uap10.0\*

Для проведения проверки TPMinV создайте [файл целей MSBuild](/visualstudio/msbuild/msbuild-targets) и включите его в пакет в папке `build\uap10.0" folder as `<имя_вашей_сборки>.targets`, replacing `<имя_вашей_сборки> на имя собственной сборки.

Вот пример того, как должен выглядеть файл целей:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>Добавление поддержки на этапе разработки

Чтобы указать, где должны отображаться свойства элемента управления в инспекторе свойств, добавьте пользовательские графические элементы и другие элементы, а затем поместите файл `design.dll` в папку `lib\uap10.0\Design` для соответствующей целевой платформы. Кроме того, чтобы работала команда **[Изменить шаблон > Изменить копию](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**, нужно включить файл `Generic.xaml` и все объединяемые словари ресурсов в папку `<your_assembly_name>\Themes` (опять с использованием фактического имени сборки). (Этот файл не влияет на поведение элемента управления во время выполнения.) В результате структура папок будет выглядеть следующим образом.

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> По умолчанию свойства элемента управления отображаются в инспекторе свойств в категории "Прочее".

## <a name="use-strings-and-resources"></a>Использование строк и ресурсов

В пакет можно внедрить строковые ресурсы (`.resw`), которые могут использоваться элементом управления или проектом UWP. Выберите для свойства **Действие сборки** файла `.resw` значение **PRIResource**.

Пример можно найти в файле [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) в образце пакета ExtensionSDKasNuGetPackage.

## <a name="package-content-such-as-images"></a>Упаковка содержимого, такого как изображения

Чтобы упаковать содержимое, например изображения, которое может использоваться элементом управления или проектом UWP, поместите эти файлы в папку `lib\uap10.0`.

Вы также можете создать [файл целей MSBuild](/visualstudio/msbuild/msbuild-targets), чтобы ресурс копировался в выходную папку проекта.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>См. также

- [Создание пакетов универсальной платформы Windows](create-uwp-packages.md)
- [Образец ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
