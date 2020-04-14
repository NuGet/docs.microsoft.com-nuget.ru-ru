---
title: Создание пакетов символов прежних версий (.symbols.nupkg)
description: В этой статье описывается создание пакетов NuGet, которые содержат только символы, для поддержки отладки других пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476273"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Создание пакетов символов прежних версий (.symbols.nupkg)

> [!Important]
> Новый рекомендуемый формат для пакетов символов — .snupkg. См. раздел [Создание пакетов символов (.snupkg)](Symbol-Packages-snupkg.md). </br>
> Формат .symbols.nupkg все еще поддерживается, но только в целях совместимости.

Наряду с возможностью создания пакетов для веб-сайта nuget.org или других источников NuGet также позволяет создавать связанные пакеты символов, которые можно опубликовать на серверах символов. Пакеты символов прежних версий в формате .symbols.nupkg можно отправить в репозиторий SymbolSource.

Потребители пакетов могут добавить `https://nuget.smbsrc.net` в соответствующие источники символов в Visual Studio, что позволяет осуществлять пошаговую отладку кода пакета в отладчике Visual Studio. Дополнительные сведения об этом процессе см. в разделе [Указание файлов символов (.pdb) и файлов с исходным кодом в отладчике Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).

## <a name="creating-a-legacy-symbol-package"></a>Создание пакета символов прежних версий

При создании пакета символов прежних версий руководствуйтесь следующими соглашениями:

- Присвойте имя основному пакету (с кодом) `{identifier}.nupkg` и включите в него все файлы, за исключением файлов `.pdb`.
- Присвойте пакету имя `{identifier}.symbols.nupkg` и включите в него DLL-файл сборки, файлы `.pdb`, XMLDOC-файлы и файлы с исходным кодом (см. далее).

Можно создать оба пакета с использованием параметра `-Symbols` на основе файла `.nuspec` или файла проекта:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Обратите внимание, что команда `pack` требует наличия Mono 4.4.2 в Mac OS X и не работает в системах Linux. На компьютерах Mac также необходимо преобразовать пути в формате Windows, указанные в файле `.nuspec`, в формат Unix.

## <a name="legacy-symbol-package-structure"></a>Структура пакета символов прежних версий

Как и пакет библиотек, пакет символов прежних версий может предназначаться для нескольких целевых платформ, поэтому структура папки `lib` должна точно соответствовать основному пакету и включать файлы `.pdb` вместе с DLL.

Например, пакет символов устаревших версий для .NET 4.0 и Silverlight 4 должен иметь следующую структуру:

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

Кроме папки `lib`, пакет символов прежних версий должен содержать следующую структуру:

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

Пакет символов прежних версий можно создать в соответствии с соглашениями на основе структуры папок, как описывается в предыдущем разделе, а также путем указания его содержимого в разделе `files` манифеста. Например, чтобы построить показанный в предыдущем разделе пакет, используйте следующий файл `.nuspec`:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>Публикация пакета символов прежних версий

> [!Important]
> Для принудительной отправки пакетов на веб-сайт nuget.org необходимо использовать [nuget.exe версии 4.9.1 или более поздней](https://www.nuget.org/downloads), где реализуются требуемые [протоколы NuGet](../api/nuget-protocols.md).

1. Для удобства сначала следует сохранить ключ API с помощью NuGet (см. раздел [Публикация пакета](../nuget-org/publish-a-package.md)), который будет применяться и к nuget.org, и к symbolsource.org, поскольку веб-сайт symbolsource.org будет проверять информацию о том, что вы являетесь владельцем пакета, на веб-сайте nuget.org.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. После публикации основного пакета на веб-сайте nuget.org выполните принудительную отправку пакета символов прежних версий, как показано ниже. При этом в качестве назначения будет автоматически использоваться веб-сайт symbolsource.org, так как в имени файла указано `.symbols`:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Чтобы выполнить публикацию в другом репозитории символов или принудительную отправку пакета символов прежних версий, не соответствующего соглашениям об именовании, следует использовать параметр `-Source`:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Также можно выполнить принудительную отправку одновременно основного пакета и пакета символов в оба репозитория, используя следующую команду:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > При работе с nuget.exe версии 4.5.0 или более поздней пакеты символов не передаются автоматически на веб-сайт symbolsource.org. В таком случае принудительную отправку пакетов символов необходимо осуществлять отдельно, как было описано ранее.
   
В этом случае NuGet опубликует файл `MyPackage.symbols.nupkg` (если он есть) на веб-сайте https://nuget.smbsrc.net/ (URL-адрес принудительной отправки для веб-сайта symbolsource.org) после публикации основного пакета на веб-сайте nuget.org.

## <a name="see-also"></a>См. также

* [Создание пакетов символов (.snupkg)](Symbol-Packages-snupkg.md) — новый рекомендуемый формат для пакетов символов
* [Сведения о переходе на новый модуль SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
