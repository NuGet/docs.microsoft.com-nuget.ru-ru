---
title: Содержимое пакета, NuGet API
description: Базовый адрес пакета — это простой интерфейс для получения самого пакета.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426765"
---
# <a name="package-content"></a>Содержимое пакета

Это можно создать URL-адрес для получения содержимого произвольного пакета (nupkg-файл) с помощью V3 API. Ресурс, используемый для извлечения содержимого пакета является `PackageBaseAddress` найти ресурс в [индекс службы](service-index.md). Этот ресурс также позволяет обнаружить все версии пакета, в списке или удалена из списка.

Этот ресурс называется как «пакет базовый адрес» или «неструктурированный контейнер».

## <a name="versioning"></a>Управление версиями

Следующие `@type` используется значение:

Значение@type              | Примечания
------------------------ | -----
PackageBaseAddress/3.0.0 | Первоначальный выпуск

## <a name="base-url"></a>Базовый URL-адрес

Базовый URL-адрес для следующих API-интерфейсов является значением `@id` свойство, связанное с ресурсом, упомянутых выше `@type` значение. В следующем документе заполнитель базовый URL-адрес `{@id}` будет использоваться.

## <a name="http-methods"></a>Методы HTTP

Все URL-адреса, найден в регистрации ресурсов поддерживают методы HTTP `GET` и `HEAD`.

## <a name="enumerate-package-versions"></a>Перечисление версий пакета

Если клиент знает идентификатор пакета и хочет обнаружение также пакеты версии пакета источник имеет доступен, клиент можно создать прогнозируемые URL-адрес для перечисления всех версий пакета. Этот список предназначен быть «список каталогов» для API содержимого пакета, указанный ниже.

> [!Note]
> Этот список содержит обе версии перечисленных и отсутствующие в списке пакетов.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Параметры запроса

name     | Увеличение     | Тип    | Обязательно | Примечания
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL-адрес    | string  | да      | Идентификатор пакета, нижний регистр

`LOWER_ID` Значение является Идентификатором нужного пакета букв с помощью правил, реализованных по. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.

### <a name="response"></a>Ответ

Если источник пакета не установлены версии идентификатор предоставленного пакета, возвращается код состояния 404.

Если источник имеет один или несколько версий, возвращается код состояния 200. Текст ответа представляет собой объект JSON со следующим свойством:

name     | Тип             | Обязательно | Примечания
-------- | ---------------- | -------- | -----
версии | Массив строк | да      | Идентификаторы, доступные пакета

Строки в `versions` массив всех букв, [нормализовать строки версии NuGet](../reference/package-versioning.md#normalized-version-numbers). Строки версии не содержат все метаданные сборки SemVer 2.0.0.

Цель состоит в том, что версии строк, найденных в этот массив может использоваться непосредственно для `LOWER_VERSION` токенов см. в следующих конечных точек.

### <a name="sample-request"></a>Пример запроса

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Пример ответа

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Скачать содержимое пакета (файла nupkg)

Если клиент знает ИД пакета и версии и хочет загрузить содержимое пакета, они достаточно создать следующий URL-адрес:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Параметры запроса

name          | Увеличение     | Тип   | Обязательно | Примечания
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL-адрес    | string | да      | Идентификатор пакета, нижний регистр
LOWER_VERSION | URL-адрес    | string | да      | Версия пакета, нормализованную и букв

Оба `LOWER_ID` и `LOWER_VERSION` являются букв с помощью правил, реализованных по. NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
метод.

`LOWER_VERSION` Нужного пакета версии нормализуется с использованием NuGet версии [правила нормализации](../reference/package-versioning.md#normalized-version-numbers). Это означает, что в этом случае необходимо исключить эти метаданные сборки, для которых разрешено в спецификации SemVer 2.0.0.

### <a name="response-body"></a>Текст ответа

Если пакет существует в источнике пакета, возвращается код состояния 200. Текст ответа будет само содержимое пакета.

Если пакет не существует в источнике пакета, возвращается код состояния 404.

### <a name="sample-request"></a>Пример запроса

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Пример ответа

Двоичный поток, который является файл nupkg для Newtonsoft.Json 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Загрузить манифест пакета (файлу nuspec)

Если клиент знает ИД пакета и версии и хочет загрузить манифест пакета, они достаточно создать следующий URL-адрес:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Параметры запроса

name          | Увеличение     | Тип   | Обязательно | Примечания
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL-адрес    | string | да      | Идентификатор пакета, нижний регистр
LOWER_VERSION | URL-адрес    | string | да      | Версия пакета, нормализованную и букв

Оба `LOWER_ID` и `LOWER_VERSION` являются букв с помощью правил, реализованных по. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) метод.

`LOWER_VERSION` Нужного пакета версии нормализуется с использованием NuGet версии [правила нормализации](../reference/package-versioning.md#normalized-version-numbers). Это означает, что в этом случае необходимо исключить эти метаданные сборки, для которых разрешено в спецификации SemVer 2.0.0.

### <a name="response-body"></a>Текст ответа

Если пакет существует в источнике пакета, возвращается код состояния 200. Текст ответа будет манифест пакета, который является файла nuspec, из соответствующего файла nupkg. Файла nuspec — это документ XML.

Если пакет не существует в источнике пакета, возвращается код состояния 404.

### <a name="sample-request"></a>Пример запроса

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Пример ответа

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
