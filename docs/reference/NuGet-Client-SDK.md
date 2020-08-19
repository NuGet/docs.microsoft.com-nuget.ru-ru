---
title: Пакет SDK для клиента NuGet
description: API развивается и еще не документирован, но примеры доступны в блоге Дейв Гликк.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622932"
---
# <a name="nuget-client-sdk"></a>Пакет SDK для клиента NuGet

*Пакет SDK клиента NuGet* ссылается на группу пакетов NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — Используется для взаимодействия с веб-каналами NuGet и на основе файлов.
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — Используется для взаимодействия с пакетами NuGet. `NuGet.Protocol` зависит от этого пакета

Исходный код для этих пакетов можно найти в репозитории GitHub для [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) .

> [!Note]
> Документацию по протоколу сервера NuGet см. в [API сервера NuGet](~/api/overview.md).

## <a name="getting-started"></a>Начало работы

### <a name="install-the-packages"></a>Установка пакетов

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a>Примеры

Эти примеры можно найти в проекте [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) на сайте GitHub.

### <a name="list-package-versions"></a>Список версий пакета

Найдите все версии Newtonsoft.Jsс помощью [API содержимого пакета NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Скачать пакет

Скачайте Newtonsoft.Jsна v 12.0.1 с помощью [API содержимого пакета NuGet v3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Получение метаданных пакета

Получите метаданные для пакета "Newtonsoft.Jsдля" с помощью [API метаданных пакета NuGet v3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Поиск пакетов

Поиск пакетов "JSON" с помощью [API поиска NuGet v3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a>Создание пакета

Создание пакета, Установка метаданных и Добавление зависимостей с помощью [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

> [!IMPORTANT]
> Настоятельно рекомендуется создавать пакеты NuGet с помощью официального инструментария NuGet, а **не** использовать этот низкоуровневый API. Существует множество характеристик, важных для правильно сформированного пакета, и последняя версия инструментов помогает реализовать эти рекомендации.
> 
> Дополнительные сведения о создании пакетов NuGet см. в обзоре [рабочего процесса создания пакета](../create-packages/overview-and-workflow.md) и документации по официальному набору средств для работы с пакетами (например, [с помощью DotNet CLI](../create-packages/creating-a-package-dotnet-cli.md)).

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Чтение пакета

Чтение пакета из файлового потока с помощью [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>Документация по сторонним производителям

Примеры и документацию для некоторых API-интерфейсов можно найти в следующем ряде блогов: Дейв Гликк, Опубликовано 2016.

- [Изучение библиотек NuGet версии 3, часть 1. Введение и основные понятия](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Изучение библиотек NuGet версии 3. часть 2. Поиск пакетов](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Изучение библиотек NuGet v3, часть 3. Установка пакетов](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Эти записи блога были написаны вскоре после выпуска **3.4.3** версии пакетов SDK клиента NuGet.
> Более новые версии пакетов могут быть несовместимы с данными в записях блога.

Бжöркстрöм в блоге Дейв Гликк, где появился другой подход к использованию пакета SDK клиента NuGet для установки пакетов NuGet:

- [Повторное посещение библиотек NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
