---
title: Пакет SDK клиента NuGet
description: API развивается и еще не документирован, но примеры доступны в блоге Дейв Гликк.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231244"
---
# <a name="nuget-client-sdk"></a>Пакет SDK клиента NuGet

*Пакет SDK клиента NuGet* ссылается на группу пакетов NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — используется для взаимодействия с веб-каналами NuGet и файлов на основе HTTP
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — используется для взаимодействия с пакетами NuGet. `NuGet.Protocol` зависит от этого пакета

Исходный код для этих пакетов можно найти в репозитории GitHub для [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) .

> [!Note]
> Документацию по протоколу сервера NuGet см. в [API сервера NuGet](~/api/overview.md).

## <a name="getting-started"></a>Начало работы

### <a name="install-the-package"></a>Установка пакета

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>Примеры

Эти примеры можно найти в проекте [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) на сайте GitHub.

### <a name="list-package-versions"></a>Список версий пакета

Найдите все версии Newtonsoft. JSON с помощью [API содержимого пакета NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Скачать пакет

Скачайте Newtonsoft. JSON v 12.0.1 с помощью [API содержимого пакета NuGet v3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Получение метаданных пакета

Получите метаданные для пакета "Newtonsoft. JSON" с помощью [API метаданных пакета NuGet v3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Поиск пакетов

Поиск пакетов "JSON" с помощью [API поиска NuGet v3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

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
