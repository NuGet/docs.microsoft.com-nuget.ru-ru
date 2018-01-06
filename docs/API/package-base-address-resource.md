---
title: "Пакет содержимого NuGet API | Документы Microsoft"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: ec68b5d1-a684-4995-b1a6-6210dbb24875
description: "Базовый адрес пакета — это простой интерфейс для выборки в самом пакете."
keywords: "Контейнер, базовый адрес для пакета NuGet, nupkg NuGet API версии пакета NuGet API, NuGet API с плоскими NuGet не включенных в список пакетов, nuspec загрузки NuGet API"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: a581f9854410bc1a84d65310b38928a1d889ece2
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="package-content"></a>Содержимое пакета

Можно создать URL-адрес для выборки произвольного пакета содержимого (nupkg-файла) с помощью V3 API. Ресурс, используемый для получения содержимого пакета — `PackageBaseAddress` найти ресурс в [служба индекс](service-index.md). Этот ресурс также включает обнаружение всех версий пакета, в списке или не включенных в список.

Этот ресурс называется как либо» пакета базовый адрес» или «неструктурированный контейнер».

## <a name="versioning"></a>Управление версиями

Следующие `@type` используется значение:

Значение @type              | Примечания
------------------------ | -----
PackageBaseAddress/3.0.0 | Первоначальный выпуск

## <a name="base-url"></a>Базовый URL-адрес

Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойства, связанные с ресурсом упомянутой выше `@type` значение. В следующем документе заполнитель базовый URL-адрес `{@id}` будет использоваться.

## <a name="http-methods"></a>Методы HTTP

Все URL-адреса, найден в поддержку ресурсов регистрации методов HTTP `GET` и `HEAD`.

## <a name="enumerate-package-versions"></a>Перечисление версий пакета

Если клиент знает, идентификатор пакета и хочет, чтобы обнаружить, что пакета версии пакета источник был доступен, клиент можно создать прогнозируемые URL-адрес для перечисления всех версий пакета. Этот список предназначена для «список каталогов» для упомянутых ниже API содержимого пакета.

> [!Note]
> Этот список содержит обе версии указанные и неуказанные пакета.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>Параметры запроса

name     | Увеличение     | Тип    | Обязательно | Примечания
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL-адрес    | string  | да      | Идентификатор пакета, нижний регистр

`LOWER_ID` Значение является Идентификатором нужный пакет букв с помощью правил, реализуемый. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.

### <a name="response"></a>Ответ

Если источник пакета не установлены версии предоставленный идентификатор, возвращается код состояния 404.

Если исходный пакет имеет одну или несколько версий, возвращается код состояния 200. Текст ответа — это объект JSON с использованием следующего свойства:

name     | Тип             | Обязательно | Примечания
-------- | ---------------- | -------- | -----
версии | Массив строк | да      | Идентификаторы, доступные пакета

Строки в `versions` массив всех букв, [нормализации строки NuGet версии](../reference/package-versioning.md#normalized-version-numbers). Все метаданные сборки SemVer 2.0.0 не содержат строки версии.

Целью является то, что версии строк, найденных в этом массиве можно использовать без изменений для `LOWER_VERSION` токены, найденные в следующих конечных точек.

### <a name="sample-request"></a>Пример запроса

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a>Пример ответа

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Скачать содержимое пакета (.nupkg)

Если клиент знает ИД пакета и версия и хочет скачать содержимое пакета, достаточно лишь создать следующий URL-адрес:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a>Параметры запроса

name          | Увеличение     | Тип   | Обязательно | Примечания
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL-адрес    | string | да      | Идентификатор пакета, нижний регистр
LOWER_VERSION | URL-адрес    | string | да      | Версия пакета, нормализованную и букв

Оба `LOWER_ID` и `LOWER_VERSION` являются букв с помощью правил, реализуемый. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.

`LOWER_VERSION` Версии пакета на нужное нормализуется с использованием NuGet версии [правила нормализации](../reference/package-versioning.md#normalized-version-numbers). Это означает, что в этом случае необходимо исключить эти метаданные сборки, который разрешен спецификацией SemVer 2.0.0.

### <a name="response-body"></a>Текст ответа

Если пакет существует в источнике пакета, возвращается код состояния 200. Текст ответа будет содержимое пакета.

Если пакет не существует в источнике пакета, возвращается код состояния 404.

### <a name="sample-request"></a>Пример запроса

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a>Пример ответа

Двоичный поток, который является .nupkg для Newtonsoft.Json 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Загрузить манифест пакета (.nuspec)

Если клиент знает ИД пакета и версия и хочет загрузить манифест пакета, достаточно лишь создать следующий URL-адрес:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a>Параметры запроса

name          | Увеличение     | Тип    | Обязательно | Примечания
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL-адрес    | string  | да      | Идентификатор пакета, нижний регистр
LOWER_VERSION | URL-адрес    | целочисленный | да      | Версия пакета, нормализованную и букв

Оба `LOWER_ID` и `LOWER_VERSION` являются букв с помощью правил, реализуемый. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.

`LOWER_VERSION` Версии пакета на нужное нормализуется с использованием NuGet версии [правила нормализации](../reference/package-versioning.md#normalized-version-numbers). Это означает, что в этом случае необходимо исключить эти метаданные сборки, который разрешен спецификацией SemVer 2.0.0.

### <a name="response-body"></a>Текст ответа

Если пакет существует в источнике пакета, возвращается код состояния 200. Текст ответа будет манифест пакета, который является .nuspec, содержащиеся в соответствующей .nupkg. .nuspec — это документ XML.

Если пакет не существует в источнике пакета, возвращается код состояния 404.

### <a name="sample-request"></a>Пример запроса

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a>Пример ответа

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
