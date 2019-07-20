---
title: Справочник по целевым платформам для NuGet
description: Ссылки на целевую платформу NuGet позволяют определить и изолировать зависимые от платформы компоненты пакета.
author: karann-msft
ms.author: karann
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: ea9f699b202d7f32648f0ccfeac3ceb1ca325b7e
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342445"
---
# <a name="target-frameworks"></a>Требуемые версии .NET Framework

NuGet использует ссылки на целевую платформу в различных местах, чтобы точно определить и изолировать зависимые от платформы компоненты пакета:

- [файл проекта](../create-packages/multiple-target-frameworks-project-file.md): Для проектов в стиле SDK в *CSPROJ* содержатся ссылки на целевую платформу.
- [манифест. nuspec](../reference/nuspec.md): Пакет может указывать отдельные пакеты для включения в проект в зависимости от целевой платформы проекта.
- [имя папки nupkg](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): Папки в `lib` папке пакета могут называться в соответствии с целевой платформой, каждая из которых содержит библиотеки DLL и другое содержимое, соответствующее этой платформе.
- [Packages. config](../reference/packages-config.md): `targetframework` Атрибут зависимости указывает вариант пакета для установки.

> [!Note]
> Исходный код клиента NuGet, который рассчитывает приведенные ниже таблицы, располагается в следующих местах:
> - Поддерживаемые имена платформ: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Приоритет и сопоставление платформы: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Поддерживаемые платформы

Платформа обычно указывается коротким моникером целевой платформы (TFM). В .NET Standard это также обобщенно *TxM* , чтобы разрешить единую ссылку на несколько платформ.

Клиенты NuGet поддерживают платформы, представленные в следующей таблице. Эквивалентные обозначения отображаются в квадратных скобках []. Обратите внимание, что некоторые средства, например `dotnet`, могут использовать в некоторых файлах варианты канонических моникеров целевой платформы (TFM). Например, `dotnet pack` использует `.NETCoreApp2.0` в файле `.nuspec` вместо `netcoreapp2.0`. Различные клиентские средства NuGet обрабатывают эти варианты различным образом, однако при непосредственном редактировании файлов всегда следует использовать канонические моникеры целевой платформы (TFM).

| name | Сокращение | TFM/TxM |
| ------------- | ------------ | --------- |
|.NET Framework | net | net11 |
| | | net20 |
| | | net35 |
| | | net40 |
| | | net403 |
| | | net45 |
| | | net451 |
| | | net452 |
| | | net46 |
| | | net461 |
| | | net462 |
| | | net47 |
| | | net471 |
| | | net472 |
| | | net48 |
|Microsoft Store (Магазин Windows) | netcore | netcore [netcore45] |
| | | netcore45 [win, win8] |
| | | netcore451 [win81] |
| | | netcore50 |
|.NET MicroFramework | netmf | netmf |
|Windows | win | win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (не поддерживается платформой Windows 10) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Универсальная платформа Windows | uap | uap [uap10.0] |
| | | uap10.0 |
| | | UAP 10.0. xxxxx (где 10.0. XXXXX — это минимальная версия приложения, используемая для использования в качестве целевой платформы) |
.NET Standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
Приложение .NET Core | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
| | | netcoreapp2.1 |
| | | netcoreapp2.2 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Устаревшие платформы

Следующие среды являются устаревшими. Пакеты, предназначенные для этих платформ, следует перевести на предлагаемые для замены.

| Устаревшая платформа | Замена
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | win |

## <a name="precedence"></a>Приоритет

Некоторые платформы являются родственными и совместимыми друг с другом, хотя и не полностью идентичными:

| Платформа | Можно использовать |
| -- | --- |
| Универсальная платформа Windows (uap) | win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | winrt |
| | |

## <a name="net-standard"></a>NET Standard

[.NET Standard](/dotnet/standard/net-standard) упрощает ссылки между двоично-совместимыми платформами, позволяя одной целевой платформе ссылаться на сочетание других. (Общие сведения см. в [учебнике по .NET для начинающих](/dotnet/articles/standard/index).)

[Средство получения ближайшей платформы из набора средств NuGet](https://aka.ms/s2m3th) имитирует логику NuGet, которая используется для выбора конкретной платформы из нескольких доступных в пакете вариантов в зависимости от платформы проекта.

В NuGet 3.3 и более ранних версий следует использовать последовательность моникеров `dotnet`. В версии 3.4 и более поздних должен использоваться синтаксис моникеров `netstandard`.

## <a name="portable-class-libraries"></a>Переносимые библиотеки классов

> [!Warning]
> **Использовать переносимые библиотеки классов не рекомендуется**. Несмотря на то, что переносимые библиотеки классов поддерживаются, вместо них авторам следует реализовать поддержку netstandard. Платформа .NET Standard является развитием PCL и представляет двоичную переносимость на разных платформах с помощью одного специального имени, которое не привязано к статической библиотеке, такой как переносимые моникеры *+ b + c* .

Чтобы определить целевую платформу, которая ссылается на несколько дочерних целевых платформ, используйте ключевое слово `portable` в качестве префикса для списка платформ, на которые указывают ссылки. Не следует искусственно включать дополнительные платформы, для которых не выполняется компиляция, поскольку это может привести к возникновению непредвиденных побочных эффектов.

Дополнительные платформы, определяемые третьими лицами, обеспечивают совместимость с другими средами, которые доступны таким образом. Кроме того, существуют сокращенные номера профиля, которые можно использовать для ссылки на такие сочетания связанных платформ, вида `Profile#`. Тем не менее применять такой подход также не рекомендуется, поскольку это снижает удобочитаемость папок и файлов `.nuspec`.

| № профиля | Инфраструктуры | Полное имя | .NET Standard |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

Кроме того, пакеты NuGet для Xamarin могут использовать дополнительные платформы, определенные для Xamarin. См. раздел [Создание пакетов NuGet для Xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| name | Описание | .NET Standard |
| --- | --- | ---
| monoandroid | Поддержка Mono для ОС Android | netstandard1.4 |
| monotouch | Поддержка Mono для iOS | netstandard1.4 |
| monomac | Поддержка Mono для OSX | netstandard1.4 |
| xamarinios | Поддержка Xamarin для iOS | netstandard1.4 |
| xamarinmac | Поддержка Xamarin для Mac | netstandard1.4 |
| xamarinpsthree | Поддержка Xamarin для Playstation 3 | netstandard1.4 |
| xamarinpsfour | Поддержка Xamarin для Playstation 4 | netstandard1.4 |
| xamarinpsvita | Поддержка Xamarin для PS Vita | netstandard1.4 |
| xamarinwatchos | Xamarin для Watch OS | netstandard1.4 |
| xamarintvos | Xamarin для TV OS | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin для XBox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin для XBox One | netstandard1.4 |

> [!Note]
> Стивен Клири (Stephen Cleary) создал средство, которое выводит список поддерживаемых переносимых библиотек классов, который можно найти в его статье [Профили платформы в .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
