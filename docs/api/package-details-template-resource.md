---
title: Шаблон URL-адреса сведения для пакета, NuGet API
description: Сведения о URL-адрес шаблона пакета позволяет клиентам для отображения в их пользовательского интерфейса, веб-ссылки на дополнительные сведения о пакете
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638081"
---
# <a name="package-details-url-template"></a>Шаблона URL-адрес сведений о пакете

Вполне возможно, для клиента, чтобы сформировать URL-адрес, который может использоваться пользователем, чтобы просмотреть дополнительные сведения о пакете веб-обозревателя. Это полезно при источник пакетов для отображения дополнительных сведений о пакете, который может не поместиться в пределах показывает NuGet клиентское приложение.

Ресурс, используемый для сборки этот URL-адрес является `PackageDetailsUriTemplate` найти ресурс в [индекс службы](service-index.md).

## <a name="versioning"></a>Управление версиями

Следующие `@type` значения используются:

Значение@type                      | Примечания
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | Первоначальный выпуск

## <a name="url-template"></a>Шаблон URL-адреса

URL-адрес для следующего API — это значение `@id` свойства, связанные с одной из упомянутых выше ресурсов `@type` значения.

## <a name="http-methods"></a>Методы HTTP

Несмотря на то, что клиент не предназначен для выполнения запросов к URL-адрес пакета сведения от имени пользователя, веб-страницы должен поддерживать `GET` метод, чтобы легко открыть в веб-браузере щелкнули URL-адрес.

## <a name="construct-the-url"></a>Создать URL-адрес

Учитывая известные ИД и версию пакета, реализация клиента можно создать URL-адрес, используемый для доступа к веб-интерфейс. Реализация клиента отображать этот построенный URL-адрес (или активную ссылку) для пользователя, позволяющий открыть веб-браузер на URL-адрес и Дополнительные сведения о пакете. Содержимое странице сведений о пакете определяется в реализации сервера.

URL-адрес должен быть абсолютный URL-адрес и схема (протокол) должна быть HTTPS.

Значение `@id` в службе индекса является URL-адрес строка, содержащая любой из следующих токенов заполнитель:

### <a name="url-placeholders"></a>Местозаполнители URL-адресов

name        | Тип    | Обязательно | Примечания
----------- | ------- | -------- | -----
`{id}`      | string  | Нет       | Идентификатор пакета, чтобы получить подробные сведения о
`{version}` | string  | Нет       | Чтобы получить подробные сведения о версии пакета

Сервер должен принимать `{id}` и `{version}` значения в любом регистре. Кроме того, сервер не должен быть чувствительно к версиях [нормализованное](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers). Другими словами, сервер должен принимать также принимают версии не было нормализовано.

Например шаблон сведения пакета nuget.org выглядит следующим образом:

    https://www.nuget.org/packages/{id}/{version}

Если реализация клиента должен отображать ссылку на сведения о пакете для NuGet.Versioning 4.3.0, он бы привести следующий URL-адрес и предоставляют их пользователю:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0