---
title: "Создание пакетов символов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4667a70d-5a17-4f1e-b2f2-b8d0c6af3882
description: "В этой статье описывается создание пакетов NuGet, которые содержат только символы, для поддержки отладки других пакетов NuGet в Visual Studio."
keywords: "пакеты символов NuGet, отладка пакета NuGet, поддержка отладки NuGet, символы пакета, соглашения о пакетах символов"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1a29fe6e9a3dec6847dbed07761e28fb8eb9b19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="creating-symbol-packages"></a>Создание пакетов символов

Помимо построения пакетов для веб-сайта nuget.org или других источников, NuGet также поддерживает создание связанных пакетов символов и их публикацию в [репозитории SymbolSource](http://www.symbolsource.org/Public).

Потребители пакетов могут добавить `http://srv.symbolsource.org/pdb/Public` в соответствующие источники символов в Visual Studio, что позволяет осуществлять пошаговую отладку кода пакета в отладчике Visual Studio. Дополнительные сведения об этом процессе см. в разделе [Указание файлов символов (.pdb) и файлов с исходным кодом в отладчике Visual Studio](https://docs.microsoft.com/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).


## <a name="creating-a-symbol-package"></a>Создание пакета символов

При создании пакета символов руководствуйтесь следующими соглашениями:

- Присвойте имя основному пакету (с кодом) `{identifier}.nupkg` и включите в него все файлы, за исключением файлов `.pdb`.
- Присвойте имя пакету символов `{identifier}.symbols.nupkg` и включите в него DLL-файл сборки, файлы `.pdb`, XMLDOC-файлы и файлы с исходным кодом (см. далее).

Можно создать оба пакета с использованием параметра `-Symbols` на основе файла `.nuspec` или файла проекта:

```
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Обратите внимание, что команда `pack` требует наличия Mono 4.4.2 в Mac OS X и не работает в системах Linux. На компьютерах Mac также необходимо преобразовать пути в формате Windows, указанные в файле `.nuspec`, в формат Unix.

## <a name="symbol-package-structure"></a>Структура пакета символов

Пакет символов, так же как и пакет библиотек, может предназначаться для нескольких целевых платформ, поэтому структура папки `lib` должна в точности совпадать с основным пакетом и включать файлы `.pdb` наряду с DLL.

Например, пакет символов для платформы .NET 4.0 и Silverlight 4 должен иметь следующую структуру:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Файлы исходного кода размещаются в отдельной папке `src`, которая должна соответствовать относительной структуре репозитория исходного кода. Это связано с тем, что PDB-файлы содержат абсолютные пути к файлам исходного кода, используемым для компиляции соответствующей библиотеки DLL, и должны быть доступны в процессе публикации. Базовый путь (общий префикс пути) может быть опущен. Например, рассмотрим библиотеку, построенную на основе следующих файлов:

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

Помимо папки `lib`, пакет символов должен содержать следующую структуру:

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a>Ссылки на файлы в nuspec

Пакет символов может быть построен в соответствии с соглашениями на основе структуры папок, как описывается в предыдущем разделе, а также путем указания его содержимого в разделе `files` манифеста. Например, чтобы построить показанный в предыдущем разделе пакет, используйте следующий файл `.nuspec`:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Публикация пакета символов

> [!Important]
> Для принудительной отправки пакетов на веб-сайт nuget.org необходимо использовать [nuget.exe версии 4.1.0 или более поздней](https://www.nuget.org/downloads), где реализуются требуемые [протоколы NuGet](../api/nuget-protocols.md).

1. Для удобства сначала следует сохранить ключ API с помощью NuGet (см. раздел [Публикация пакета](../create-packages/publish-a-package.md)), который будет применяться и к nuget.org, и к symbolsource.org, поскольку веб-сайт symbolsource.org будет проверять информацию о том, что вы являетесь владельцем пакета, на веб-сайте nuget.org.

    ```
    nuget SetApiKey Your-API-Key
    ```

1. После публикации основного пакета на веб-сайте nuget.org выполните принудительную отправку пакета символов, как показано ниже. При этом в качестве назначения будет автоматически использоваться веб-сайт symbolsource.org, поскольку в имени файла указано `.symbols`:

    ```
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> При работе с nuget.exe версии 4.5.0 или более поздней пакеты символов не передаются автоматически на веб-сайт symbolsource.org. В таком случае принудительную отправку пакетов символов необходимо осуществлять отдельно, как описывается на следующем шаге.

1. Чтобы выполнить публикацию в другом репозитории символов или принудительную отправку пакета символов, не соответствующего соглашениям об именовании, следует использовать параметр `-Source`:

    ```
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. Также можно выполнить принудительную отправку одновременно основного пакета и пакета символов в оба репозитория, используя следующую команду:

    ```
    nuget push MyPackage.nupkg
    ```

В этом случае NuGet опубликует файл `MyPackage.symbols.nupkg` (если он есть) на веб-сайте https://nuget.smbsrc.net/ (URL-адрес принудительной отправки для веб-сайта symbolsource.org) после публикации основного пакета на веб-сайте nuget.org.

## <a name="see-also"></a>См. также

 - <a href="https://www.symbolsource.org/Public/Wiki/Using" target="_blank">Использование веб-сайта SymbolSource</a> (symbolsource.org)
