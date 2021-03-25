---
title: Упаковка элементов управления пользовательским интерфейсом с помощью NuGet
description: Создание пакетов NuGet, которые содержат элементы управления UWP или WPF, включая необходимые метаданные и вспомогательные файлы для конструкторов Visual Studio и Blend.
author: JonDouglas
ms.author: jodou
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 7660203ec44db75b7764767b519c9ff10dd1122e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859087"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Создание элементов управления пользовательским интерфейсом в виде пакетов NuGet

Начиная с версии Visual Studio 2017, вы можете использовать возможности добавления элементов управления UWP и WPF в пакеты NuGet. В руководстве описано, как использовать эти возможности в контексте элементов управления UWP с использованием [примера ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/main/ExtensionSDKasNuGetPackage). Это же применимо к элементам управления WPF, если не указано иное.

## <a name="prerequisites"></a>Предварительные требования

1. Visual Studio 2017
1. Умение [создавать пакеты UWP](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Создание структуры библиотеки

> [!Note]
> Это применимо только к элементам управления UWP.

Настраивая свойство `GenerateLibraryLayout`, вы обеспечите создание результатов сборки проекта в макете, который готов к упаковке без необходимости включать записи отдельных файлов в nuspec.

В окне свойств проекта перейдите на вкладку сборки и установите флажок "Создать структуру библиотеки". Это изменит файл проекта и задаст для флага `GenerateLibraryLayout` значение true для текущее выбранной конфигурации сборки и платформы.

Можно также изменить файл проекта, чтобы добавить `<GenerateLibraryLayout>true</GenerateLibraryLayout>` в первую безусловную группу свойств. Так свойство будет применено независимо от конфигурации сборки и платформы.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Добавление поддержки элементов управления XAML на панели элементов или в области ресурсов

Чтобы элемент управления XAML отображался на панели элементов конструктора XAML в Visual Studio и в области ресурсов Blend, создайте файл `VisualStudioToolsManifest.xml` в корне папки `tools` проекта пакета. Этот файл не требуется, если не нужно, чтобы элемент управления отображался на панели элементов или в области ресурсов.

```
\build
\lib
\tools
    VisualStudioToolsManifest.xml
```

Файл имеет следующую структуру:

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
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
- *vs_category*: метка группы, в которой должен отображаться элемент управления на панели элементов в конструкторе Visual Studio. Элемент `VSCategory` необходим для отображения элемента управления на панели элементов.
*ui_framework*. Имя платформы, например WPF. Обратите внимание, что атрибут `UIFramework` требуется для узлов ToolboxItems в Visual Studio 16.7 Preview 3 и более поздних версиях, чтобы элемент управления отображался в панели элементов.
- *blend_category* — метка группы, в которой должен отображаться элемент управления в области ресурсов конструктора Blend. Элемент `BlendCategory` необходим для отображения элемента управления в области ресурсов.
- *type_full_name_n* — полное имя каждого элемента управления, включая пространство имен, например `ManagedPackage.MyCustomControl`. Обратите внимание на то, что нотация с точкой используется как для управляемых, так и для собственных типов.

Если один пакет содержит несколько сборок элементов управления, можно включить несколько элементов `<File>` в элемент `<FileList>`. Вы также можете добавить несколько узлов `<ToolboxItems>` в один элемент `<File>`, чтобы упорядочить элементы управления по отдельным категориям.

В приведенном ниже примере элемент управления, реализованный в файле `ManagedPackage.winmd`, будет отображаться в Visual Studio и Blend в группе "Managed Package" (Управляемый пакет) и иметь имя MyCustomControl. Все эти имена являются произвольными.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
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

Чтобы на панели элементов или в области ресурсов отображался пользовательский значок, добавьте изображение в свой проект или соответствующий проект `design.dll` с именем Namespace.ControlName.extension и выберите действие сборки "Внедренный ресурс". Также нужно убедиться, что в соответствующем файле `AssemblyInfo.cs` указан атрибут ProvideMetadata — `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`. См. этот [пример](https://github.com/NuGet/Samples/blob/main/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).

Поддерживаемые форматы: `.png`, `.jpg`, `.jpeg`, `.gif` и `.bmp`. Рекомендуемый формат — BMP24 размером 16 на 16 пикселей.

![Пример значка поля инструмента](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

Розовый фон заменяется во время выполнения. Цвет значков меняется при изменении темы Visual Studio и если ожидается этот цвет фона. Дополнительные сведения см. в разделе [Изображения и значки для Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).

В приведенном ниже примере проект содержит файл изображения с именем ManagedPackage.MyCustomControl.png.

![Задание пользовательского значка в проекте](media/UWP-control-custom-icon.png)

> [!Note]
> Для собственных элементов управления значки следует добавлять в качестве ресурсов в проект `design.dll`.

## <a name="support-specific-windows-platform-versions"></a>Поддержка определенных версий платформы Windows

Пакеты UWP имеют свойства TargetPlatformVersion (TPV) и TargetPlatformMinVersion (TPMinV), которые определяют самую позднюю и самую раннюю версии ОС, в которых может быть установлено приложение. Кроме того, свойство TPV определяет версию пакета SDK, на основе которой создается приложение. Учитывайте эти свойства при разработке пакета UWP: использование интерфейсов API, которые выходят за пределы определенных в приложении версий платформы, приведет либо к сбою сборки, либо к ошибке приложения во время выполнения.

Например, предположим, что вы указали в качестве значения свойства TPMinV для пакета элементов управления юбилейное обновление Windows 10 (версия 10.0, сборка 14393), и вам нужно, чтобы пакет использовался проектами UWP, предназначенными только для этой или более поздних версий. Чтобы пакет могли потреблять проекты UWP, необходимо упаковать элементы управления, используя следующие имена папок:

```
\lib\uap10.0.14393\*
\ref\uap10.0.14393\*
```

NuGet автоматически проверит TPMinV для используемого проекта и отменит установку, если версия будет ниже Windows 10 Anniversary Edition (10.0; сборка 14393).

Для WPF вы можете настроить использование пакета элементов управления WPF в проектах, предназначенных для .NET Framework версии 4.6.1 и выше. Для этого вам нужно упаковать элементы управления, используя следующие имена папок:

```
\lib\net461\*
\ref\net461\*
```

## <a name="add-design-time-support"></a>Добавление поддержки на этапе разработки

Чтобы указать, где должны отображаться свойства элемента управления в инспекторе свойств, добавьте пользовательские графические элементы и другие элементы, а затем поместите файл `design.dll` в папку `lib\uap10.0.14393\Design` для соответствующей целевой платформы. Кроме того, чтобы работала команда **[Изменить шаблон > Изменить копию](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**, нужно включить файл `Generic.xaml` и все объединяемые словари ресурсов в папку `<your_assembly_name>\Themes` (опять с использованием фактического имени сборки). (Этот файл не влияет на поведение элемента управления во время выполнения.) В результате структура папок будет выглядеть следующим образом.

```
\lib
  \uap10.0.14393
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

Пример, в котором можно настроить использование пакета средств управления WPF в проектах, предназначенных для .NET Framework версии 4.6.1 и выше:

```
\lib
  \net461
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

> [!Note]
> По умолчанию свойства элемента управления отображаются в инспекторе свойств в категории "Прочее".

## <a name="use-strings-and-resources"></a>Использование строк и ресурсов

В пакет можно внедрить строковые ресурсы (`.resw`), которые могут использоваться элементом управления или проектом UWP. Выберите для свойства **Действие сборки** файла `.resw` значение **PRIResource**.

Пример можно найти в файле [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/main/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) в образце пакета ExtensionSDKasNuGetPackage.

> [!Note]
> Это применимо только к элементам управления UWP.

## <a name="see-also"></a>См. также

- [Создание пакетов универсальной платформы Windows](create-uwp-packages.md)
- [Образец ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/main/ExtensionSDKasNuGetPackage)