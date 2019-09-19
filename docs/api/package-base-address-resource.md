---
title: Содержимое пакета, API NuGet
description: Базовый адрес пакета — это простой интерфейс для выборки самого пакета.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094126"
---
# <a name="package-content"></a>Содержимое пакета

Можно создать URL-адрес для выборки содержимого произвольного пакета (nupkg-файла) с помощью API V3. Ресурс, используемый для выборки содержимого пакета, — `PackageBaseAddress` это ресурс, найденный в [индексе службы](service-index.md). Этот ресурс также включает обнаружение всех версий пакета, перечисленных или отсутствующих в списке.

Этот ресурс обычно называется "базовым адресом пакета" или "плоским контейнером".

## <a name="versioning"></a>Управление версиями

Используется следующее `@type` значение:

Значение@type              | Примечания
------------------------ | -----
Паккажебасеаддресс/3.0.0 | Первоначальный выпуск

## <a name="base-url"></a>Базовый URL-адрес

Базовый URL-адрес для следующих интерфейсов API — это значение `@id` свойства, связанного с вышеупомянутым значением `@type` ресурса. В следующем документе будет использоваться базовый URL-адрес `{@id}` заполнителя.

## <a name="http-methods"></a>Методы HTTP

Все URL-адреса, найденные в ресурсе регистрации `GET` , `HEAD`поддерживают методы HTTP и.

## <a name="enumerate-package-versions"></a>Перечислить версии пакета

Если клиент знает идентификатор пакета и хочет определить, какие версии пакетов доступны в источнике пакета, клиент может создать прогнозируемый URL-адрес для перечисления всех версий пакета. Этот список должен быть списком каталогов для API содержимого пакета, упомянутого ниже.

> [!Note]
> Этот список содержит как перечисленные, так и невключенные версии пакетов.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Параметры запроса

name     | In     | Тип    | Обязательно | Примечания
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | да      | Идентификатор пакета, в нижнем регистре

`LOWER_ID` Значение представляет собой требуемый идентификатор пакета в нижнем регистре, используя правила, реализованные. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Метод NET.

### <a name="response"></a>Отклик

Если источник пакета не имеет версий указанного идентификатора пакета, возвращается код состояния 404.

Если источник пакета имеет одну или несколько версий, возвращается код состояния 200. Текст ответа — это объект JSON со следующим свойством:

name     | Тип             | Обязательно | Примечания
-------- | ---------------- | -------- | -----
версии | Массив строк | да      | Доступные версии

Строки в `versions` массиве — это все строки [нормализованных строк версии NuGet](../concepts/package-versioning.md#normalized-version-numbers)в нижнем регистре. Строки версии не содержат метаданные сборки SemVer 2.0.0.

Цель состоит в том, что строки версии, найденные в этом массиве, можно `LOWER_VERSION` использовать буквально для маркеров, найденных в следующих конечных точках.

### <a name="sample-request"></a>Пример запроса

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Пример ответа

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Скачать содержимое пакета (. nupkg)

Если клиент знает идентификатор и версию пакета и хочет загрузить содержимое пакета, необходимо создать только следующий URL-адрес:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Параметры запроса

name          | In     | Тип   | Обязательно | Примечания
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | да      | Идентификатор пакета, нижний регистр
LOWER_VERSION | URL    | string | да      | Версия пакета, нормализованная и строчная

И, `LOWER_VERSION` и являются строчными, используя правила, реализованные. `LOWER_ID` СЕТЬ[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
метод.

— Это требуемая версия пакета, нормализованная с помощью [правил нормализации](../concepts/package-versioning.md#normalized-version-numbers)версий NuGet. `LOWER_VERSION` Это означает, что в этом случае необходимо исключить метаданные сборки, которые допускаются спецификацией SemVer 2.0.0.

### <a name="response-body"></a>Текст ответа

Если пакет существует в источнике пакета, возвращается код состояния 200. Текст ответа будет самим содержимым пакета.

Если пакет не существует в источнике пакета, возвращается код состояния 404.

### <a name="sample-request"></a>Пример запроса

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Пример ответа

Двоичный поток, который является файлом. nupkg для Newtonsoft. JSON 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Скачать манифест пакета (. nuspec)

Если клиент знает идентификатор и версию пакета и хочет скачать манифест пакета, ему нужно только создать следующий URL-адрес:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Параметры запроса

name          | In     | Тип   | Обязательно | Примечания
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | да      | Идентификатор пакета, нижний регистр
LOWER_VERSION | URL    | string | да      | Версия пакета, нормализованная и строчная

И, `LOWER_VERSION` и являются строчными, используя правила, реализованные. `LOWER_ID` [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Метод NET.

— Это требуемая версия пакета, нормализованная с помощью [правил нормализации](../concepts/package-versioning.md#normalized-version-numbers)версий NuGet. `LOWER_VERSION` Это означает, что в этом случае необходимо исключить метаданные сборки, которые допускаются спецификацией SemVer 2.0.0.

### <a name="response-body"></a>Текст ответа

Если пакет существует в источнике пакета, возвращается код состояния 200. Текст ответа будет манифестом пакета, который является. nuspec, содержащимся в соответствующем nupkg. Nuspec — это XML-документ.

Если пакет не существует в источнике пакета, возвращается код состояния 404.

### <a name="sample-request"></a>Пример запроса

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Пример ответа

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
