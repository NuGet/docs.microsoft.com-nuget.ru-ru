---
title: Ресурс каталога, API NuGet v3
description: Каталог — это индекс всех пакетов, созданных и удаленных в nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6c04453fec9beb7b0998953384ec60694e1213c1
ms.sourcegitcommit: af059dc776cfdcbad20baab2919b5d6dc1e9022d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/09/2021
ms.locfileid: "99990139"
---
# <a name="catalog"></a>Каталог

**Каталог** — это ресурс, в котором записываются все операции пакета в источнике пакета, такие как создание и удаление. Ресурс каталога имеет `Catalog` тип в [индексе службы](service-index.md). Этот ресурс можно использовать для [запроса всех опубликованных пакетов](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Так как каталог не используется официальным клиентом NuGet, не все источники пакетов реализуют каталог.

> [!Note]
> В настоящее время каталог nuget.org недоступен в Китае. Дополнительные сведения см. в разделе [NuGet/нужетгаллери # 4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Управление версиями

Используется следующее `@type` значение:

Значение @type   | Примечания
------------- | -----
Catalog/3.0.0 | Первоначальный выпуск

## <a name="base-url"></a>Базовый URL-адрес

URL-адрес точки входа для следующих API-интерфейсов — это значение `@id` свойства, связанного с вышеупомянутыми `@type` значениями ресурсов. В этом разделе используется URL-адрес заполнителя `{@id}` .

## <a name="http-methods"></a>Методы HTTP

Все URL-адреса, найденные в ресурсе каталога, поддерживают только методы HTTP `GET` и `HEAD` .

## <a name="catalog-index"></a>Индекс каталога

Индекс каталога — это документ в хорошо известном расположении со списком элементов каталога, упорядоченным в хронологическом порядке. Это точка входа ресурса каталога.

Индекс состоит из страниц каталога. Каждая страница каталога содержит элементы каталога. Каждый элемент каталога представляет событие, касающееся одного пакета в момент времени. Элемент каталога может представлять пакет, который был создан, удален из списка, повторно добавлен в него из источника пакета. При обработке элементов каталога в хронологическом порядке Клиент может создать актуальное представление каждого пакета, существующего в источнике пакета v3.

Вкратце, большие двоичные объекты каталога имеют следующую иерархическую структуру:

- **Index**: точка входа для каталога.
- **Страница**: группирование элементов каталога.
- **Лист**: документ, представляющий элемент каталога, который является моментальным снимком состояния одного пакета.

Каждый объект каталога имеет свойство, которое называется `commitTimeStamp` представлением, когда элемент был добавлен в каталог. Элементы каталога добавляются на страницу каталога пакетами, называемыми фиксациями. Все элементы каталога в одной фиксации имеют одинаковую отметку времени фиксации ( `commitTimeStamp` ) и идентификатор фиксации ( `commitId` ). Элементы каталога, размещенные в той же фиксации, представляют события, которые произошли около того же момента времени в источнике пакета. В рамках фиксации каталога нет упорядочения.

Поскольку ИДЕНТИФИКАТОРы и версии каждого пакета уникальны, в фиксации никогда не будет более одного элемента каталога. Это гарантирует, что элементы каталога для одного пакета всегда могут быть однозначно упорядочены по отношению к метке времени фиксации.

В каталоге не может быть больше одной фиксации `commitTimeStamp` . Иными словами, объект `commitId` является избыточным с помощью `commitTimeStamp` .

В отличие от [ресурса метаданных пакета](registration-base-url-resource.md), который индексируется по идентификатору пакета, каталог индексируется (и поддается запросу) только по времени.

Элементы каталога всегда добавляются в каталог в монотонно возрастающем хронологическом порядке. Это означает, что если фиксация каталога добавляется во время X, то фиксация каталога никогда не будет добавляться со временем, меньшим или равным X.

Следующий запрос извлекает индекс каталога.

```
GET {@id}
```

Индекс каталога — это документ JSON, содержащий объект со следующими свойствами:

Имя            | Тип             | Обязательно | Примечания
--------------- | ---------------- | -------- | -----
коммитид        | строка           | да      | Уникальный идентификатор, связанный с последней фиксацией
коммиттиместамп | строка           | да      | Метка времени последней фиксации
count           | целочисленный          | да      | Число страниц в индексе
items           | массив объектов | да      | Массив объектов, каждый объект, представляющий страницу

Каждый элемент `items` массива является объектом с минимальными сведениями о каждой странице. Эти объекты страницы не содержат конечных объектов каталога (элементов). Порядок элементов в этом массиве не определен. Страницы могут быть упорядочены по клиенту в памяти с помощью их `commitTimeStamp` Свойства.

По мере добавления новых страниц значение `count` будет увеличено, а в массиве отобразятся новые объекты `items` .

Когда элементы добавляются в каталог, индекс изменится и увеличится `commitId` `commitTimeStamp` . Эти два свойства, по сути, представляют собой сводку по всем страницам `commitId` и `commitTimeStamp` значениям в `items` массиве.

### <a name="catalog-page-object-in-the-index"></a>Объект страницы каталога в индексе

Объекты страницы каталога, найденные в свойстве индекса каталога, `items` имеют следующие свойства.

Имя            | Тип    | Обязательно | Примечания
--------------- | ------- | -------- | -----
@id             | строка  | да      | Страница "URL-адрес для выборки каталога"
коммитид        | строка  | да      | Уникальный идентификатор, связанный с последней фиксацией на этой странице
коммиттиместамп | строка  | да      | Метка времени последней фиксации на этой странице
count           | целочисленный | да      | Число элементов на странице каталога

В отличие от [ресурса метаданных пакета](registration-base-url-resource.md) , который в некоторых случаях покидает индекс, листья каталога никогда не встроены в индекс и всегда должны быть получены с помощью `@id` URL-адреса страницы.

### <a name="sample-request"></a>Пример запроса

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>Пример ответа

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Страница каталога

Страница каталога представляет собой коллекцию элементов каталога. Это документ, полученный с использованием одного из `@id` значений, найденных в индексе каталога. URL-адрес страницы каталога не предназначен для прогнозирования и должен обнаруживаться только по индексу каталога.

Новые элементы каталога добавляются на страницу в индексе каталога только с наибольшей отметкой времени фиксации или с новой страницей. После добавления страницы с более высокой отметкой времени фиксации в каталог старые страницы никогда не добавляются и не изменяются.

Документ страницы каталога является объектом JSON со следующими свойствами:

Имя            | Тип             | Обязательно | Примечания
--------------- | ---------------- | -------- | -----
коммитид        | строка           | да      | Уникальный идентификатор, связанный с последней фиксацией на этой странице
коммиттиместамп | строка           | да      | Метка времени последней фиксации на этой странице
count           | целочисленный          | да      | Число элементов на странице
items           | массив объектов | да      | Элементы каталога на этой странице
родитель          | строка           | да      | URL-адрес индекса каталога

Каждый элемент `items` массива является объектом с минимальными сведениями об элементе каталога. Эти объекты элементов не содержат все данные элемента каталога. Порядок элементов в `items` массиве страницы не определен. Элементы могут упорядочиваться по клиенту в памяти с помощью их `commitTimeStamp` Свойства.

Количество элементов каталога на странице определяется реализацией сервера. Для nuget.org существует не более 550 элементов на каждой странице, хотя фактическое число для некоторых страниц может быть меньше, в зависимости от размера следующего пакета фиксации на момент времени.

По мере добавления новых элементов в `count` массив появятся новые объекты элементов каталога `items` .

По мере добавления элементов на страницу `commitId` изменения и `commitTimeStamp` увеличиваются. Эти два свойства, по сути, представляют собой сводку по всем `commitId` `commitTimeStamp` значениям и в `items` массиве.

### <a name="catalog-item-object-in-a-page"></a>Объект элемента каталога на странице

Объекты элементов каталога, найденные в свойстве страницы каталога, `items` имеют следующие свойства.

Имя            | Тип    | Обязательно | Примечания
--------------- | ------- | -------- | -----
@id             | строка  | да      | URL-адрес для выборки элемента каталога
@type           | строка  | да      | Тип элемента каталога
коммитид        | строка  | да      | Идентификатор фиксации, связанный с этим элементом каталога
коммиттиместамп | строка  | да      | Метка времени фиксации этого элемента каталога
NuGet: ИД        | строка  | да      | Идентификатор пакета, с которым связан этот конечный объект
NuGet: версия   | строка  | да      | Версия пакета, с которой связан этот конечный объект

`@type`Значением будет одно из следующих двух значений:

1. `nuget:PackageDetails`— соответствует `PackageDetails` типу в конечном документе каталога.
1. `nuget:PackageDelete`— соответствует `PackageDelete` типу в конечном документе каталога.

Дополнительные сведения о том, что означает каждый тип, см. в разделе [соответствующий тип элементов](#item-types) ниже.

### <a name="sample-request"></a>Пример запроса

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>Пример ответа

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Конечный каталог

Конечный объект каталога содержит метаданные об определенном ИДЕНТИФИКАТОРе и версии пакета в определенный момент времени. Это документ, полученный с использованием `@id` значения, найденного на странице каталога. URL-адрес конечного каталога не предназначен для прогнозирования и должен быть обнаружен с использованием только страницы каталога.

Конечный документ каталога — это объект JSON со следующими свойствами:

Имя                    | Тип                       | Обязательно | Примечания
----------------------- | -------------------------- | -------- | -----
@type                   | строка или массив строк | да      | Типы элемента каталога
Каталог: Коммитид        | строка                     | да      | Идентификатор фиксации, связанный с этим элементом каталога
Каталог: Коммиттиместамп | строка                     | да      | Метка времени фиксации этого элемента каталога
идентификатор                      | строка                     | да      | Идентификатор пакета для элемента каталога
published               | строка                     | да      | Дата публикации элемента каталога пакетов
version                 | строка                     | да      | Версия пакета для элемента каталога

### <a name="item-types"></a>Типы элементов

`@type`Свойство является строкой или массивом строк. Для удобства, если `@type` значение является строкой, оно должно рассматриваться как любой массив размера один. Не все возможные значения для `@type` задокументированы. Однако каждый элемент каталога имеет только одно из двух следующих значений строкового типа:

1. `PackageDetails`— представляет моментальный снимок метаданных пакета.
1. `PackageDelete`— представляет пакет, который был удален

### <a name="package-details-catalog-items"></a>Элементы каталога сведений о пакете

Элементы каталога с типом `PackageDetails` содержат моментальный снимок метаданных пакета для определенного пакета (сочетание идентификатора и версии). Элемент каталога сведений о пакете создается, когда в источнике пакета встречается один из следующих сценариев.

1. Пакет **отправлен**.
1. Пакет указан в **списке**.
1. Пакет не входит в **список**.
1. Пакет **переполняется**.

Перекомпоновка пакетов — это административный жест, который по сути создает фиктивную принудительную отправку существующего пакета без изменений самого пакета. В nuget.org используется перекомпоновка после исправления ошибки в одном из фоновых заданий, использующих каталог.

Клиенты, использующие элементы каталога, не должны пытаться определить, какой из этих сценариев создал элемент каталога. Вместо этого клиент должен просто обновить любое сохраненное представление или индекс с метаданными, содержащимися в элементе каталога. Более того, повторяющиеся или избыточные элементы каталога должны обрабатываться надлежащим образом (идемпотентно).

Элементы каталога сведений о пакете имеют следующие свойства в дополнение к тем, которые [включены во все листья каталога](#catalog-leaf).

Имя                    | Тип                       | Обязательно | Примечания
----------------------- | -------------------------- | -------- | -----
authors                 | строка                     | нет       |
created                 | строка                     | нет       | Метка времени, когда пакет был создан впервые. Резервное свойство: `published` .
депенденциграупс        | массив объектов           | нет       | Зависимости пакета, сгруппированные по целевой платформе ([тот же формат, что и ресурс метаданных пакета](registration-base-url-resource.md#package-dependency-group));
Deprecation             | object                     | нет       | Прекращение использования, связанное с пакетом ([тот же формат, что и ресурс метаданных пакета](registration-base-url-resource.md#package-deprecation)).
description             | строка                     | нет       |
iconUrl                 | строка                     | нет       |
испререлеасе            | Логическое                    | нет       | Является ли версия пакета предварительной. Может быть обнаружено из `version` .
Язык                | строка                     | нет       |
licenseUrl              | строка                     | нет       |
перечисленные                  | Логическое                    | нет       | Указывает, указан ли пакет
minClientVersion        | строка                     | нет       |
паккажехаш             | строка                     | да      | Хэш пакета, кодировка с использованием [стандартного базового 64](https://tools.ietf.org/html/rfc4648#section-4)
паккажехашалгорисм    | строка                     | да      |
паккажесизе             | целочисленный                    | да      | Размер пакета. nupkg в байтах
packageTypes            | массив объектов           | нет       | Типы пакетов, заданные автором.
projectUrl              | строка                     | нет       |
releaseNotes            | строка                     | нет       |
рекуирелиценсеагримент | Логическое                    | нет       | Предположить, `false` Если исключен
Итоги                 | строка                     | нет       |
tags                    | Массив строк           | нет       |
title                   | строка                     | нет       |
вербатимверсион         | строка                     | нет       | Строка версии, которая изначально была найдена в. nuspec
уязвимости         | массив объектов           | нет       | Уязвимости пакета

Свойство package `version` представляет собой строку полной версии после нормализации. Это означает, что здесь можно добавить данные о сборке SemVer 2.0.0.

`created`Отметка времени — это момент, когда пакет был впервые получен с помощью источника пакета, что обычно представляет собой короткий промежуток времени перед меткой времени фиксации элемента каталога.

`packageHashAlgorithm`— Это строка, определяемая реализацией сервера, представляющей алгоритм хэширования, используемый для создания `packageHash` . nuget.org всегда использует `packageHashAlgorithm` значение `SHA512` .

`packageTypes`Свойство будет представлено только в том случае, если тип пакета был указан автором. Если он существует, всегда будет иметь хотя бы одну запись (1). Каждый элемент `packageTypes` массива является объектом JSON со следующими свойствами:

Имя      | Тип    | Обязательно | Примечания
--------- | ------- | -------- | -----
name      | строка  | да      | Имя типа пакета.
version    | строка  | нет       | Версия типа пакета. Отображается только в том случае, если автор явно указал версию в nuspec.

Отметка времени `published` — это время последнего перечисления пакета.

> [!Note]
> В nuget.org `published` значение устанавливается равным году 1900, когда пакет удаляется из списка.

#### <a name="vulnerabilities"></a>Уязвимости

Массив объектов `vulnerability`. Каждая уязвимость имеет следующие свойства.

Имя         | Тип   | Обязательно | Примечания
------------ | ------ | -------- | -----
адвисорюрл  | строка | да      | Расположение рекомендаций по безопасности для пакета
severity     | строка | да      | Серьезность рекомендаций: "0" = низкая, "1" = умеренный, "2" = высокий, "3" = критический

Если `severity` свойство содержит значения, отличные от перечисленных здесь, серьезность рекомендаций будет считаться низкой.

#### <a name="sample-request"></a>Пример запроса

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>Пример ответа

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Удаление элементов каталога из пакета

Элементы каталога с типом `PackageDelete` содержат минимальный набор данных, указывающий на клиентов каталога, что пакет был удален из источника пакета и больше недоступен для каких-либо операций с пакетами (например, Restore).

> [!NOTE]
> Пакет может быть удален и позже повторно опубликован с использованием того же идентификатора и версии пакета. В nuget.org это очень редкий случай, поскольку он нарушает официальное допущение клиента о том, что идентификатор пакета и версия предполагают наличие определенного содержимого пакета. Дополнительные сведения об удалении пакетов в nuget.org см. в [нашей политике](../nuget-org/policies/deleting-packages.md).

Элементы каталога удаления пакета не имеют дополнительных свойств, кроме тех, которые [включены во все листья каталога](#catalog-leaf).

`version`Свойство — это исходная строка версии, найденная в пакете. nuspec.

`published`Свойство — это время удаления пакета, которое обычно представляет собой короткое время перед меткой времени фиксации элемента каталога.

#### <a name="sample-request"></a>Пример запроса

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>Пример ответа

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Курсор

### <a name="overview"></a>Обзор

В этом разделе описывается концепция клиента, которая, хотя и не обязательно задается протоколом, должна быть частью любой практичной реализации клиента каталога.

Так как каталог является структурой данных только для добавления, индексированной по времени, клиент должен локально сохранить **курсор** , что представляет момент времени, в течение которого клиент обрабатывал элементы каталога. Обратите внимание, что это значение курсора никогда не должно создаваться с помощью часов компьютера клиента. Вместо этого значение должно быть получено из значения объекта каталога `commitTimestamp` .

Каждый раз, когда клиент хочет обработать новые события в источнике пакета, ему нужно только запросить каталог для всех элементов каталога с меткой времени фиксации, превышающим сохраненный курсор. После успешной обработки клиентом всех новых элементов каталога записывается последняя метка времени фиксации элементов каталога, только что обрабатывалась как новое значение курсора.

Используя этот подход, клиент может не пропустить все события пакета, произошедшие в источнике пакета.
Кроме того, клиенту никогда не придется повторно обрабатывать старые события до записанной метки времени фиксации курсора.

Эта мощная концепция курсоров используется для многих фоновых заданий nuget.org и используется для обновления самого интерфейса API V3. 

### <a name="initial-value"></a>Начальное значение

Когда клиент каталога запускается первый раз (и, следовательно, не имеет значения курсора), он должен использовать значение курсора по умолчанию. NET `System.DateTimeOffset.MinValue` или some, аналогичное понятие минимальной представим метки времени.

### <a name="iterating-over-catalog-items"></a>Перебор элементов каталога

Чтобы запросить следующий набор элементов каталога для обработки, клиент должен выполнить следующие действия:

1. Получение значения записанного курсора из локального хранилища.
1. Скачайте и десериализует индекс каталога.
1. Найти все страницы каталога с меткой времени фиксации *выше* курсора.
1. Объявите пустой список элементов каталога для обработки.
1. Для каждой страницы каталога, сопоставленной на шаге 3:
   1. Скачайте и десериализует страницу каталога.
   1. Найти все элементы каталога с меткой времени фиксации *выше* курсора.
   1. Добавьте все совпадающие элементы каталога в список, объявленный на шаге 4.
1. Сортировка списка элементов каталога по метке времени фиксации.
1. Обрабатывать каждый элемент каталога последовательно:
   1. Скачайте и десериализует элемент каталога.
   1. Соответствующим образом отреагировать на тип элемента каталога.
   1. Обработка документа элемента каталога с учетом особенностей клиента.
1. Запишите метку времени фиксации последнего элемента каталога в качестве нового значения курсора.

С помощью этого базового алгоритма реализация клиента может создать полное представление всех пакетов, доступных в источнике пакета. Клиенту необходимо периодически выполнять этот алгоритм, чтобы всегда знать о последних изменениях в источнике пакета.

> [!Note]
> Это алгоритм, который nuget.org использует для сохранения [метаданных пакета](registration-base-url-resource.md), [содержимого пакета](package-base-address-resource.md), [поиска](search-query-service-resource.md) и [автозаполнения](search-autocomplete-service-resource.md) ресурсов.

### <a name="dependent-cursors"></a>Зависимые курсоры

Предположим, что существует два клиента каталога, которые имеют определенную зависимость, где выходные данные одного клиента зависят от выходных данных другого клиента. 

#### <a name="example"></a>Пример

Например, в nuget.org только что опубликованный пакет не должен отображаться в ресурсе поиска, прежде чем появится в ресурсе метаданных пакета. Это связано с тем, что операция восстановления, выполняемая официальным клиентом NuGet, использует ресурс метаданных пакета. Если клиент обнаруживает пакет с помощью службы поиска, он должен иметь возможность успешно восстановить этот пакет с помощью ресурса метаданных пакета. Иными словами, ресурс поиска зависит от ресурса метаданных пакета. Каждый ресурс имеет фоновое задание клиента каталога, которое обновляет этот ресурс. Каждый клиент имеет собственный курсор.

Так как оба ресурса создаются из каталога, курсор клиента каталога, который обновляет ресурс поиска, *не должен находиться за* курсором клиента каталога метаданных пакета.

#### <a name="algorithm"></a>Алгоритм

Чтобы реализовать это ограничение, просто измените алгоритм выше, чтобы он был следующим:

1. Получение значения записанного курсора из локального хранилища.
1. Скачайте и десериализует индекс каталога.
1. Найти все страницы каталога с меткой времени фиксации *больше, чем* курсор, **меньше или равен курсору зависимости.**
1. Объявите пустой список элементов каталога для обработки.
1. Для каждой страницы каталога, сопоставленной на шаге 3:
   1. Скачайте и десериализует страницу каталога.
   1. Найти все элементы каталога с меткой времени фиксации *больше, чем* курсор, **меньше или равен курсору зависимости.**
   1. Добавьте все совпадающие элементы каталога в список, объявленный на шаге 4.
1. Сортировка списка элементов каталога по метке времени фиксации.
1. Обрабатывать каждый элемент каталога последовательно:
   1. Скачайте и десериализует элемент каталога.
   1. Соответствующим образом отреагировать на тип элемента каталога.
   1. Обработка документа элемента каталога с учетом особенностей клиента.
1. Запишите метку времени фиксации последнего элемента каталога в качестве нового значения курсора.

С помощью этого модифицированного алгоритма можно создать систему клиентов зависимого каталога, создавая свои собственные индексы, артефакты и т. д.
