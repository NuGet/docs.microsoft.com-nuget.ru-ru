---
title: Отправка и удаление, API NuGet
description: Служба публикации позволяет клиентам публиковать новые пакеты и удалять существующие.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773917"
---
# <a name="push-and-delete"></a>Принудительная отправка и удаление

Можно выполнить принудительную отправку, удаление (или вывод из списка) в зависимости от реализации сервера, а также перечислить пакеты с помощью API NuGet v3. Эти операции основаны на `PackagePublish` ресурсе, найденном в [индексе службы](service-index.md).

## <a name="versioning"></a>Управление версиями

Используется следующее `@type` значение:

Значение @type          | Примечания
-------------------- | -----
Паккажепублиш/2.0.0 | Первоначальный выпуск

## <a name="base-url"></a>Базовый URL-адрес

Базовый URL-адрес для следующих API-интерфейсов — это значение `@id` свойства `PackagePublish/2.0.0` ресурса в [индексе службы](service-index.md)источника пакета. В приведенной ниже документации используется URL-адрес NuGet. org. Рассмотрите в `https://www.nuget.org/api/v2/package` качестве заполнителя для `@id` значения, найденного в индексе службы.

Обратите внимание, что этот URL-адрес указывает на то же расположение, что и конечная точка Push предыдущей версии v2, так как этот протокол совпадает.

## <a name="http-methods"></a>Методы HTTP

В `PUT` `POST` `DELETE` этом ресурсе поддерживаются методы, и HTTP. Сведения о том, какие методы поддерживаются в каждой конечной точке, см. ниже.

## <a name="push-a-package"></a>Отправка пакета

> [!Note]
> nuget.org имеет [Дополнительные требования](NuGet-Protocols.md) для взаимодействия с конечной точкой принудительной отправки.

nuget.org поддерживает принудительную отправку новых пакетов с помощью следующего API. Если пакет с указанным ИДЕНТИФИКАТОРом и версией уже существует, nuget.org отклонит push-уведомление. Другие источники пакетов могут поддерживать замену существующего пакета.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Параметры запроса

Имя           | В     | Тип   | Обязательно | Примечания
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | строка | yes      | Например: `X-NuGet-ApiKey: {USER_API_KEY}`

Ключ API — это непрозрачная строка, полученная пользователем из источника пакета и настроенная в клиенте. Конкретный формат строки не задан, но длина ключа API не должна превышать приемлемый размер для значений заголовка HTTP.

### <a name="request-body"></a>Тело запроса

Текст запроса должен быть в следующем формате:

#### <a name="multipart-form-data"></a>Составные данные форм

Заголовок запроса `Content-Type` — `multipart/form-data` , а первый элемент в тексте запроса — это необработанные байты nupkg. Последующие элементы в составном тексте не учитываются. Имя файла или любые другие заголовки составных элементов игнорируются.

### <a name="response"></a>Ответ

Код состояния | Значение
----------- | -------
201, 202    | Пакет успешно отправлен
400         | Указан недопустимый пакет
409         | Пакет с указанным ИДЕНТИФИКАТОРом и версией уже существует

Серверные реализации зависят от кода состояния успеха, возвращаемого при успешной отправке пакета.

## <a name="delete-a-package"></a>Удаление пакета

nuget.org интерпретирует запрос на удаление пакета как "unlist". Это означает, что пакет по-прежнему доступен для существующих потребителей пакета, но пакет больше не отображается в результатах поиска или в веб-интерфейсе. Дополнительные сведения об этом практическом занятии см. в разделе Политика [удаленных пакетов](../nuget-org/policies/deleting-packages.md) . Другие серверные реализации могут интерпретировать этот сигнал как жесткое удаление, обратимое удаление или удалить из списка. Например, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (Серверная реализация, поддерживающая более старый API версии 2) поддерживает обработку этого запроса в виде несписка или жесткого удаления на основе параметра конфигурации.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Параметры запроса

Имя           | В     | Тип   | Обязательно | Примечания
-------------- | ------ | ------ | -------- | -----
ID             | URL-адрес    | строка | yes      | Идентификатор удаляемого пакета
VERSION        | URL-адрес    | строка | yes      | Версия удаляемого пакета
X-NuGet-ApiKey | Header | строка | yes      | Например: `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Ответ

Код состояния | Значение
----------- | -------
204         | Пакет был удален
404         | Нет пакета с указанным `ID` и не `VERSION` существует

## <a name="relist-a-package"></a>Повторное перечисление пакета

Если пакет не включен в список, можно сделать этот пакет снова видимым в результатах поиска, используя конечную точку "перечисление". Эта конечная точка имеет ту же форму, что и [Конечная точка Delete (удалить из списка)](#delete-a-package) , но использует `POST` метод HTTP вместо `DELETE` метода.

Если пакет уже указан, запрос все равно будет выполнен.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Параметры запроса

Имя           | В     | Тип   | Обязательно | Примечания
-------------- | ------ | ------ | -------- | -----
ID             | URL-адрес    | строка | yes      | Идентификатор пакета для повторного перечисления
VERSION        | URL-адрес    | строка | yes      | Версия пакета для повторного перечисления
X-NuGet-ApiKey | Header | строка | yes      | Например: `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Ответ

Код состояния | Значение
----------- | -------
200         | Пакет теперь указан
404         | Нет пакета с указанным `ID` и не `VERSION` существует
