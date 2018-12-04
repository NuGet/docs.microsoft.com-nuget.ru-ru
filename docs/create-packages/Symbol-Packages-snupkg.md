---
title: Публикация пакетов символов NuGet с помощью нового формата, SNUPKG| Документация Майкрософт
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
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
ms.openlocfilehash: 48ca4b62e722988b3dfe69306565d7f159805962
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453459"
---
# <a name="creating-symbol-packages-snupkg"></a>Создание пакетов символов (SNUPKG)

## <a name="prerequisites"></a>Предварительные требования

[nuget.exe 4.9.0 или более поздней версии](https://www.nuget.org/downloads) либо [dotnet.exe 2.2.0 или более поздней версии](https://www.microsoft.com/net/download/dotnet-core/2.2), которые реализуют необходимые [протоколы NuGet](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Создание пакета символов

Пакет символов SNUPKG можно создать из NUSPEC- или CSPROJ-файла. Поддерживаются NuGet.exe и dotnet.exe. Если для команды пакета nuget.exe используются параметры ```-Symbols -SymbolPackageFormat snupkg```, в дополнение к NUPKG-файлу будет создан SNUPKG-файл.

Примеры команд для создания SNUPKG-файлов
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild -t:pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
```

`.snupkgs` не создаются по умолчанию. В случае использования nuget.exe необходимо передать свойство `SymbolPackageFormat` вместе с `-Symbols`, в случае использования dotnet.exe — `--include-symbols`, а в случае использования msbuild — `-p:IncludeSymbols`.

Свойство SymbolPackageFormat может иметь одно из двух значений: `symbols.nupkg` (по умолчанию) или `snupkg`. Если значение SymbolPackageFormat не указано, по умолчанию будет использоваться `symbols.nupkg` и будет создан устаревший пакет символов.

> [!Note]
> Устаревший формат `.symbols.nupkg` все еще поддерживается, но только в целях совместимости (см. раздел [Устаревшие пакеты символов](Symbol-Packages.md)). Сервер символов NuGet.org принимает только новый формат пакетов символов: `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Публикация пакета символов

1. Для удобства сначала сохраните ключ API с NuGet (см. раздел [Публикация пакета](../create-packages/publish-a-package.md)).

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

## <a name="nugetorg-symbol-server"></a>Сервер символов NuGet.org

NuGet.org поддерживает собственный репозиторий сервера символов и принимает только новый формат пакетов символов: `.snupkg`. Потребители пакетов могут добавить `https://symbols.nuget.org/download/symbols` в соответствующие источники символов в Visual Studio с помощью символов, опубликованных на сервер символов nuget.org, что позволяет осуществлять пошаговую отладку кода пакета в отладчике Visual Studio. Дополнительные сведения об этом процессе см. в разделе [Указание файлов символов (.pdb) и файлов с исходным кодом в отладчике Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017).

### <a name="nugetorg-symbol-package-constraints"></a>Ограничения пакета символов Nuget.org

Пакеты символов, поддерживаемые в nuget.org, имеют следующие ограничения.

- В пакет символов можно добавлять только следующие расширения файлов. ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- Сейчас на сервере символов NuGet поддерживаются только управляемые [переносимые PDB-файлы](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md).
- Нужно выполнить сборку PDB-файлов и связанных библиотек DLL NUPKG в компиляторе в Visual Studio версии 15.9 или выше (см. раздел [Хэш шифрования PDB-файлов](https://github.com/dotnet/roslyn/issues/24429)).

Если в SNUPKG-файл включены любые другие типы файлов, произойдет сбой публикации в nuget.org.

### <a name="symbol-package-validation-and-indexing"></a>Проверка и индексирование пакета символов

Пакеты символов, опубликованные в [NuGet.org](https://www.nuget.org/), проходят несколько проверок, например, проверку на вирусы.

После прохождения пакетом всех проверок может пройти некоторое время, прежде чем символы будут проиндексированы и станут доступны для использования на серверах символов NuGet.org. Если пакет не проходит проверку, на странице сведений о пакете NUPKG отображается соответствующее уведомление об ошибке и вы также получите сообщение электронной почты с уведомлением.

Проверка и индексирование пакета обычно занимает около 15 минут. Если публикация пакета занимает больше времени, перейдите на веб-сайт [status.nuget.org](https://status.nuget.org/) и убедитесь, что портал nuget.org работает. Если все системы исправны, но пакет не был опубликован в течение часа, войдите на веб-сайт nuget.org и свяжитесь с нами по ссылке "Связаться со службой поддержки" на странице сведений о пакете.

## <a name="symbol-package-structure"></a>Структура пакета символов

NUPKG-файл не будет отличаться от текущего, а SNUPKG-файл будет обладать следующими характеристиками.

1) SNUPKG-файл будет иметь тот же идентификатор и ту же версию, что и соответствующий NUPKG-файл.
2) SNUPKG-файл будет иметь ту же структуру папок, что и NUPKG-файл, для всех DLL- и EXE-файлов за следующим исключением. Вместо DLL- и EXE-файлов в ту же иерархию папок будут включены соответствующие PDB-файлы. Файлы и папки с расширениями, отличными от PDB, не войдут в пакет SNUPKG.
3) NUSPEC-файл в SNUPKG также укажет новый тип PackageType, как показано ниже. Тип PackageType должен быть единственным указанным. 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) Если автор решит создать пакеты NUPKG и SNUPKG с помощью пользовательского NUSPEC-файла, пакет SNUPKG должен иметь иерархию папок и файлы, указанные в пункте 2).
5) Поля ```authors``` и ```owners``` будут исключены из NUSPEC-файла пакета SNUPKG.

## <a name="see-also"></a>См. также

[Отладка пакетов NuGet и улучшения символов](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
