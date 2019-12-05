---
title: Публикация пакетов символов NuGet с помощью нового формата, SNUPKG| Документация Майкрософт
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Создание пакетов символов NuGet (SNUPKG).
keywords: пакеты символов NuGet, отладка пакета NuGet, поддержка отладки NuGet, символы пакета, соглашения о пакетах символов
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 8528261f90e75e2dfac8cb746b396d227c3741f4
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825180"
---
# <a name="creating-symbol-packages-snupkg"></a>Создание пакетов символов (SNUPKG)

Пакеты символов позволяют улучшить интерфейс отладки пакетов NuGet.

## <a name="prerequisites"></a>Предварительные требования

[nuget.exe 4.9.0 или более поздней версии](https://www.nuget.org/downloads) либо [dotnet.exe 2.2.0 или более поздней версии](https://www.microsoft.com/net/download/dotnet-core/2.2), которые реализуют необходимые [протоколы NuGet](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Создание пакета символов

Если вы используете dotnet.exe или MSBuild, необходимо задать свойства `IncludeSymbols` и `SymbolPackageFormat`, чтобы создать SNUPKG-файл в дополнение к NUPKG-файлу.

* Как вариант, добавьте следующие свойства в CSPROJ-файл.

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* Вы также можете указать эти свойства в командной строке.

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  or

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Если вы используете NuGet.exe, вы можете с помощью следующих команд создать SNUPKG-файл в дополнение к NUPKG-файлу:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Свойство [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) может иметь одно из двух значений: `symbols.nupkg` (по умолчанию) или `snupkg`. Если значение этого свойства не указано, будет создан устаревший пакет символов.

> [!Note]
> Устаревший формат `.symbols.nupkg` все еще поддерживается, но только в целях совместимости (см. раздел [Устаревшие пакеты символов](Symbol-Packages.md)). Сервер символов NuGet.org принимает только новый формат пакетов символов: `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Публикация пакета символов

1. Для удобства сначала сохраните ключ API с NuGet (см. раздел [Публикация пакета](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. После публикации основного пакета в nuget.org передайте пакет символов следующим образом.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Также можно выполнить принудительную отправку одновременно основного пакета и пакета символов, используя указанную ниже команду. Оба файла (.nupkg и .snupkg) должны находиться в текущей папке.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet опубликует оба пакета на сайте nuget.org. Пакет `MyPackage.nupkg` будет опубликован первым, а `MyPackage.snupkg` — вторым.

> [!Note]
> Если пакет символов не опубликован, убедитесь, что вы настроили источник NuGet.org в виде `https://api.nuget.org/v3/index.json`. Публикация пакетов символов поддерживается только в [API NuGet версии 3](../api/overview.md#versioning).

## <a name="nugetorg-symbol-server"></a>Сервер символов NuGet.org

NuGet.org поддерживает собственный репозиторий сервера символов и принимает только новый формат пакетов символов: `.snupkg`. Потребители пакетов могут добавить `https://symbols.nuget.org/download/symbols` в соответствующие источники символов в Visual Studio с помощью символов, опубликованных на сервер символов nuget.org, что позволяет осуществлять пошаговую отладку кода пакета в отладчике Visual Studio. Дополнительные сведения об этом процессе см. в разделе [Указание файлов символов (.pdb) и файлов с исходным кодом в отладчике Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).

### <a name="nugetorg-symbol-package-constraints"></a>Ограничения пакета символов NuGet.org

NuGet.org налагает на пакеты символов следующие ограничения:

- В пакетах символов допускаются только следующие расширения файлов: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`
- На сервере символов NuGet.org поддерживаются только управляемые [переносимые PDB-файлы](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md).
- Нужно выполнить сборку PDB-файлов и связанных с ними библиотек DLL NUPKG в компиляторе в Visual Studio версии 15.9 или более поздней (см. раздел [Хэш шифрования PDB-файлов](https://github.com/dotnet/roslyn/issues/24429)).

Пакеты символов, опубликованные в NuGet.org, не пройдут проверку, если указанные ограничения не соблюдаются. 

### <a name="symbol-package-validation-and-indexing"></a>Проверка и индексирование пакета символов

Пакеты символов, опубликованные в [NuGet.org](https://www.nuget.org/), проходят несколько проверок, включая проверку на наличие вредоносных программ. Если пакет не проходит проверку, на странице сведений о нем отображается сообщение об ошибке. Кроме того, владельцы пакета получат сообщение электронной почты с инструкциями по устранению выявленных проблем.

После того как пакет символов пройдет все проверки, символы будут проиндексированы серверами символов NuGet.org. После индексирования символ будет доступен для использования на серверах символов NuGet.org.

Проверка и индексирование пакета обычно занимает около 15 минут. Если публикация пакета занимает больше времени, перейдите на веб-сайт [status.nuget.org](https://status.nuget.org/) и убедитесь, что портал NuGet.org работает. Если все системы исправны, но пакет не был опубликован в течение часа, войдите на веб-сайт nuget.org и свяжитесь с нами по ссылке "Связаться со службой поддержки" на странице сведений о пакете.

## <a name="symbol-package-structure"></a>Структура пакета символов

NUPKG-файл не будет отличаться от текущего, а SNUPKG-файл будет обладать следующими характеристиками.

1) SNUPKG-файл будет иметь тот же идентификатор и ту же версию, что и соответствующий NUPKG-файл.
2) SNUPKG-файл будет иметь ту же структуру папок, что и NUPKG-файл, для всех DLL- и EXE-файлов за следующим исключением. Вместо DLL- и EXE-файлов в ту же иерархию папок будут включены соответствующие PDB-файлы. Файлы и папки с расширениями, отличными от PDB, не войдут в пакет SNUPKG.
3) NUSPEC-файл в SNUPKG также укажет новый тип PackageType, как показано ниже. Тип PackageType должен быть единственным указанным.

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Если автор решит создать пакеты NUPKG и SNUPKG с помощью пользовательского NUSPEC-файла, пакет SNUPKG должен иметь иерархию папок и файлы, указанные в пункте 2).
5) Поля ```authors``` и ```owners``` будут исключены из NUSPEC-файла пакета SNUPKG.
6) Не используйте элемент ```<license>```. SNUPKG-файл рассматривается в рамках той же лицензии, что и соответствующий NUPKG-файл.

## <a name="see-also"></a>См. также

Чтобы обеспечить возможность отладки исходного кода сборок .NET, рекомендуется использовать Source Link. Дополнительные сведения см. в [руководстве по Source Link](/dotnet/standard/library-guidance/sourcelink).

Дополнительные сведения о пакетах символов см. в проектной спецификации по [Отладка пакетов NuGet и улучшение символов](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements).
