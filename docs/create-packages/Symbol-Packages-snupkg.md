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
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380422"
---
# <a name="creating-symbol-packages-snupkg"></a>Создание пакетов символов (SNUPKG)

Хороший опыт отладки полагается на наличие отладочных символов, так как они предоставляют важную информацию, такую как связь между скомпилированным и исходным кодом, имена локальных переменных, трассировки стека и многое другое. Пакеты символов (SNUPKG) можно использовать для распространения этих символов и улучшения возможностей отладки пакетов NuGet.

## <a name="prerequisites"></a>предварительные требования

[nuget.exe 4.9.0 или более поздней версии](https://www.nuget.org/downloads) либо [dotnet CLI 2.2.0 или более поздней версии](https://www.microsoft.com/net/download/dotnet-core/2.2), которые реализуют необходимые [протоколы NuGet](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Создание пакета символов

Если вы используете dotnet CLI или MSBuild, необходимо задать свойства `IncludeSymbols` и `SymbolPackageFormat`, чтобы создать SNUPKG-файл в дополнение к NUPKG-файлу.

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

  или диспетчер конфигурации служб

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
- На сервере символов NuGet.org поддерживаются только управляемые [переносимые PDB-файлы](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md).
- Нужно выполнить сборку PDB-файлов и связанных с ними библиотек DLL NUPKG в компиляторе в Visual Studio версии 15.9 или более поздней (см. раздел [Хэш шифрования PDB-файлов](https://github.com/dotnet/roslyn/issues/24429)).

Пакеты символов, опубликованные в NuGet.org, не пройдут проверку, если указанные ограничения не соблюдаются. 

### <a name="symbol-package-validation-and-indexing"></a>Проверка и индексирование пакета символов

Пакеты символов, опубликованные в [NuGet.org](https://www.nuget.org/), проходят несколько проверок, включая проверку на наличие вредоносных программ. Если пакет не проходит проверку, на странице сведений о нем отображается сообщение об ошибке. Кроме того, владельцы пакета получат сообщение электронной почты с инструкциями по устранению выявленных проблем.

После того как пакет символов пройдет все проверки, символы будут проиндексированы серверами символов NuGet.org и доступны для использования.

Проверка и индексирование пакета обычно занимает около 15 минут. Если публикация пакета занимает больше времени, перейдите на веб-сайт [status.nuget.org](https://status.nuget.org/) и убедитесь, что портал NuGet.org работает. Если все системы исправны, но пакет не был опубликован в течение часа, войдите на веб-сайт nuget.org и свяжитесь с нами по ссылке "Связаться со службой поддержки" на странице сведений о пакете.

## <a name="symbol-package-structure"></a>Структура пакета символов

Пакет символов (SNUPKG) имеет следующие характеристики:

1) SNUPKG-файл имеет тот же идентификатор и ту же версию, что и соответствующий пакет NuGet (NUPKG).
2) SNUPKG-файл имеет ту же структуру папок, что и соответствующий NUPKG-файл для всех DLL- и EXE-файлов, но вместо DLL- и EXE-файлов в ту же иерархию папок будут включены соответствующие PDB-файлы. Файлы и папки с расширениями, отличными от PDB, не войдут в пакет SNUPKG.
3) Файл пакета символов NUSPEC имеет тип пакета `SymbolsPackage`:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Если автор решит создать пакеты NUPKG и SNUPKG с помощью пользовательского NUSPEC-файла, пакет SNUPKG должен иметь иерархию папок и файлы, указанные в пункте 2).
5) Следующие поля будут исключены из NUSPEC-файла пакета SNUPKG: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl``` и ```icon```.
6) Не используйте элемент ```<license>```. SNUPKG-файл рассматривается в рамках той же лицензии, что и соответствующий NUPKG-файл.

## <a name="see-also"></a>См. также раздел

Чтобы обеспечить возможность отладки исходного кода сборок .NET, рекомендуется использовать Source Link. Дополнительные сведения см. в [руководстве по Source Link](/dotnet/standard/library-guidance/sourcelink).

Дополнительные сведения о пакетах символов см. в проектной спецификации по [Отладка пакетов NuGet и улучшение символов](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements).
