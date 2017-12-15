---
title: "Автозаполнение, NuGet API | Документы Microsoft"
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
ms.assetid: ead5cf7a-e51e-4cbb-8798-58226f4c853f
description: "Автозаполнение службы поиска поддерживает интерактивный обнаружения пакета идентификаторы и версии."
keywords: "API автозаполнения NuGet, идентификатор пакета NuGet поиска, идентификатор пакета подстроки"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 313ceb630947b46c34b98e14044ecf121b725087
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="autocomplete"></a>Автозавершение

Существует возможность создания пакета идентификатор и версия Автозаполнение опыт работы с V3 API. Ресурс, используемый для автозаполнения запросов является `SearchAutocompleteService` найти ресурс в [служба индекс](service-index.md).

## <a name="versioning"></a>Управление версиями

Следующие `@type` используются значения:

Значение @type                          | Примечания
------------------------------------ | -----
SearchAutocompleteService            | Первоначальный выпуск
SearchAutocompleteService/3.0.0-beta | Псевдоним`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Псевдоним`SearchAutocompleteService`

## <a name="base-url"></a>Базовый URL-адрес

Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойства, связанные с одной из упомянутых выше ресурсов `@type` значения. В следующем документе заполнитель базовый URL-адрес `{@id}` будет использоваться.

## <a name="http-methods"></a>Методы HTTP

Все URL-адреса, найден в поддержку ресурсов регистрации методов HTTP `GET` и `HEAD`.

## <a name="search-for-package-ids"></a>Выполните поиск пакета идентификаторы

Первый автозаполнения API поддерживает поиск строки идентификатор пакета. Это очень полезно, если вы хотите предоставляют функцию typeahead пакета в пользовательском интерфейсе интегрирован с источника пакета NuGet.

Пакет, содержащий только версии, отсутствующие в списке не будет отображаться в результатах.

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>Параметры запроса

Имя        | Увеличение     | Тип    | Обязательно | Примечания
----------- | ------ | ------- | -------- | -----
q           | URL-адрес    | string  | Нет       | Строка для сравнения с идентификаторами пакетов
skip        | URL-адрес    | целочисленный | Нет       | Количество пропускаемых для разбиения на страницы результатов
Take        | URL-адрес    | целочисленный | Нет       | Число результатов, возвращаемых для разбиения на страницы
Предварительный выпуск  | URL-адрес    | boolean | Нет       | `true`или `false` определения, следует ли включать [пакеты предварительного выпуска](../create-packages/prerelease-packages.md)
semVerLevel | URL-адрес    | string  | Нет       | Строка версии 1.0.0 SemVer 

Запрос автозаполнения `q` анализируется таким способом, который определен с помощью реализации сервера. NuGet.org поддерживает выполнение запросов для префикса маркеров идентификатор пакета, которые — это идентификатор, созданный spliting исходный счет camel регистр и символы.

`skip` Параметра по умолчанию равно 0.

`take` Параметра должно быть целое число больше нуля. Реализация сервера может наложить максимальное значение.

Если `prerelease` не указан, исключаются пакеты предварительного выпуска.

`semVerLevel` Параметра запроса используется для согласиться на [SemVer 2.0.0 пакетов](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Если этот параметр запроса не исключается, будут возвращены только идентификаторы пакета с SemVer 1.0.0 совместимые версии (с [стандартные управление версиями NuGet](../reference/package-versioning.md) предупреждения, такие как строки версии 4 частей целое число).
Если `semVerLevel=2.0.0` указан, будут возвращены SemVer 1.0.0 и совместимые пакеты SemVer 2.0.0. В разделе [SemVer 2.0.0 поддержка nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) для получения дополнительной информации.

### <a name="response"></a>Ответ

Ответ представляет документ JSON, содержащий до `take` результаты автозаполнения.

Корневой объект JSON имеет следующие свойства:

Имя      | Тип             | Обязательно | Примечания
--------- | ---------------- | -------- | -----
totalHits | целочисленный          | да      | Общее количество совпадений, без учета `skip` и`take`
Данные      | Массив строк | да      | Запрос соответствует ИД пакета

### <a name="sample-request"></a>Пример запроса

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a>Пример ответа

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Перечисление версий пакета

После обнаружения идентификатор пакета с помощью предыдущего API клиента можно использовать автозаполнение API для перечисления версии пакета для идентификатора указанного пакета.

Версия пакета, отсутствующие в списке не будет отображаться в результатах.

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>Параметры запроса

Имя        | Увеличение     | Тип    | Обязательно | Примечания
----------- | ------ | ------- | -------- | -----
id          | URL-адрес    | string  | да      | Идентификатор пакета для версии для выборки
Предварительный выпуск  | URL-адрес    | boolean | Нет       | `true`или `false` определения, следует ли включать [пакеты предварительного выпуска](../create-packages/prerelease-packages.md)
semVerLevel | URL-адрес    | string  | Нет       | Строка версии SemVer 2.0.0 

Если `prerelease` не указан, исключаются пакеты предварительного выпуска.

`semVerLevel` Параметра запроса используется для согласиться на пакеты SemVer 2.0.0. Если этот параметр запроса не исключается, будут возвращены только версии SemVer 1.0.0. Если `semVerLevel=2.0.0` указан, будут возвращены SemVer 1.0.0 и версии SemVer 2.0.0. В разделе [SemVer 2.0.0 поддержка nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) для получения дополнительной информации.

### <a name="response"></a>Ответ

Ответ — документ JSON, содержащий все версии пакета идентификатор предоставленного пакета, фильтрация на основе параметров данного запроса.

Корневой объект JSON имеет следующее свойство:

Имя      | Тип             | Обязательно | Примечания
--------- | ---------------- | -------- | -----
Данные      | Массив строк | да      | Запрос на соответствует версии пакета

Версии пакетов в `data` массив может содержать метаданные сборки SemVer 2.0.0 (например `1.0.0+metadata`) Если `semVerLevel=2.0.0` был представлен в строке запроса.

### <a name="sample-request"></a>Пример запроса

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a>Пример ответа

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
