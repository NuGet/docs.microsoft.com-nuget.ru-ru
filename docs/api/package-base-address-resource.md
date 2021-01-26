---
title: Содержимое пакета, API NuGet
description: Базовый адрес пакета — это простой интерфейс для выборки самого пакета.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773932"
---
# <a name="package-content"></a>Содержимое пакета

Можно создать URL-адрес для выборки содержимого произвольного пакета (nupkg-файла) с помощью API V3. Ресурс, используемый для выборки содержимого пакета, — это `PackageBaseAddress` ресурс, найденный в [индексе службы](service-index.md). Этот ресурс также включает обнаружение всех версий пакета, перечисленных или отсутствующих в списке.

Этот ресурс обычно называется "базовым адресом пакета" или "плоским контейнером".

## <a name="versioning"></a>Управление версиями

Используется следующее `@type` значение:

Значение @type              | Примечания
------------------------ | -----
Паккажебасеаддресс/3.0.0 | Первоначальный выпуск

## <a name="base-url"></a>Базовый URL-адрес

Базовый URL-адрес для следующих интерфейсов API — это значение `@id` свойства, связанного с вышеупомянутым `@type` значением ресурса. В следующем документе будет использоваться базовый URL-адрес заполнителя `{@id}` .

## <a name="http-methods"></a>Методы HTTP

Все URL-адреса, найденные в ресурсе регистрации, поддерживают методы HTTP `GET` и `HEAD` .

## <a name="enumerate-package-versions"></a>Перечислить версии пакета

Если клиент знает идентификатор пакета и хочет определить, какие версии пакетов доступны в источнике пакета, клиент может создать прогнозируемый URL-адрес для перечисления всех версий пакета. Этот список должен быть списком каталогов для API содержимого пакета, упомянутого ниже.

> [!Note]
> Этот список содержит как перечисленные, так и невключенные версии пакетов.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>Параметры запроса

Имя     | В     | Тип    | Обязательно | Примечания
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL-адрес    | строка  | yes      | Идентификатор пакета, в нижнем регистре

`LOWER_ID`Значение представляет собой требуемый идентификатор пакета в нижнем регистре, используя правила, реализованные. Метод NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) .

### <a name="response"></a>Ответ

Если источник пакета не имеет версий указанного идентификатора пакета, возвращается код состояния 404.

Если источник пакета имеет одну или несколько версий, возвращается код состояния 200. Текст ответа — это объект JSON со следующим свойством:

Имя     | Тип             | Обязательно | Примечания
-------- | ---------------- | -------- | -----
versions | Массив строк | yes      | Доступные версии

Строки в `versions` массиве — это все строки [нормализованных строк версии NuGet](../concepts/package-versioning.md#normalized-version-numbers)в нижнем регистре. Строки версии не содержат метаданные сборки SemVer 2.0.0.

Цель состоит в том, что строки версии, найденные в этом массиве, можно использовать буквально для `LOWER_VERSION` маркеров, найденных в следующих конечных точках.

### <a name="sample-request"></a>Пример запроса

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a>Пример ответа

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Скачать содержимое пакета (. nupkg)

Если клиент знает идентификатор и версию пакета и хочет загрузить содержимое пакета, необходимо создать только следующий URL-адрес:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a>Параметры запроса

Имя          | В     | Тип   | Обязательно | Примечания
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL-адрес    | строка | yes      | Идентификатор пакета, нижний регистр
LOWER_VERSION | URL-адрес    | строка | yes      | Версия пакета, нормализованная и строчная

`LOWER_ID`И, и `LOWER_VERSION` являются строчными, используя правила, реализованные. СЕТЬ[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)
метод.

`LOWER_VERSION`— Это требуемая версия пакета, нормализованная с помощью [правил нормализации](../concepts/package-versioning.md#normalized-version-numbers)версий NuGet. Это означает, что в этом случае необходимо исключить метаданные сборки, которые допускаются спецификацией SemVer 2.0.0.

### <a name="response-body"></a>Текст ответа

Если пакет существует в источнике пакета, возвращается код состояния 200. Текст ответа будет самим содержимым пакета.

Если пакет не существует в источнике пакета, возвращается код состояния 404.

### <a name="sample-request"></a>Пример запроса

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a>Пример ответа

Двоичный поток, который является. nupkg для Newtonsoft.Jsв 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Скачать манифест пакета (. nuspec)

Если клиент знает идентификатор и версию пакета и хочет скачать манифест пакета, ему нужно только создать следующий URL-адрес:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a>Параметры запроса

Имя          | В     | Тип   | Обязательно | Примечания
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL-адрес    | строка | yes      | Идентификатор пакета, нижний регистр
LOWER_VERSION | URL-адрес    | строка | yes      | Версия пакета, нормализованная и строчная

`LOWER_ID`И, и `LOWER_VERSION` являются строчными, используя правила, реализованные. Метод NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) .

`LOWER_VERSION`— Это требуемая версия пакета, нормализованная с помощью [правил нормализации](../concepts/package-versioning.md#normalized-version-numbers)версий NuGet. Это означает, что в этом случае необходимо исключить метаданные сборки, которые допускаются спецификацией SemVer 2.0.0.

### <a name="response-body"></a>Текст ответа

Если пакет существует в источнике пакета, возвращается код состояния 200. Текст ответа будет манифестом пакета, который является. nuspec, содержащимся в соответствующем nupkg. Nuspec — это XML-документ.

Если пакет не существует в источнике пакета, возвращается код состояния 404.

### <a name="sample-request"></a>Пример запроса

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a>Пример ответа

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
