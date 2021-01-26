---
title: Пакет SDK для клиента NuGet
description: API развивается и еще не документирован, но примеры доступны в блоге Дейв Гликк.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: e89b50601deb204892536406b4ddabf7005e0642
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776131"
---
# <a name="nuget-client-sdk"></a>Пакет SDK для клиента NuGet

*Пакет SDK клиента NuGet* ссылается на группу пакетов NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) — Используется для взаимодействия с веб-каналами NuGet и на основе файлов.
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) — Используется для взаимодействия с пакетами NuGet. `NuGet.Protocol` зависит от этого пакета

Исходный код для этих пакетов можно найти в репозитории GitHub для [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) .
Исходный код для этих примеров можно найти в проекте [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) на сайте GitHub.

> [!Note]
> Документацию по протоколу сервера NuGet см. в [API сервера NuGet](~/api/overview.md).

## <a name="nugetprotocol"></a>NuGet. Protocol

Установите `NuGet.Protocol` пакет для взаимодействия с веб-каналами пакетов NuGet на основе HTTP и папок.

```ps1
dotnet add package NuGet.Protocol
```

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

### <a name="push-a-package"></a>Отправка пакета

Отправка пакета с помощью [API-интерфейса NuGet v3 Push and Delete](../api/package-publish-resource.md):

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>Удаление пакета

Удаление пакета с помощью [API-интерфейса NuGet v3 Push and Delete](../api/package-publish-resource.md):

> [!Note]
> Серверы NuGet могут интерпретировать запрос на удаление пакета как «жесткое удаление», «обратимое удаление» или «удалить список».
> Например, nuget.org интерпретирует запрос на удаление пакета как "unlist". Дополнительные сведения об этом практическом занятии см. в разделе [Удаление политик пакетов](../nuget-org/policies/deleting-packages.md) .

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>Работа с веб-каналами с проверкой подлинности

Используется [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) для работы с веб-каналами с проверкой подлинности.

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>NuGet. Упаковка

Установите `NuGet.Packaging` пакет для взаимодействия с `.nupkg` файлами и `.nuspec` из потока:

```ps1
dotnet add package NuGet.Packaging
```

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
