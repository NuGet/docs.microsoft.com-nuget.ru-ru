---
title: Ограничения, NuGet API скорости
description: API-интерфейсы NuGet будет обязательные ограничения скорости, чтобы избежать злонамеренного использования.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548681"
---
# <a name="rate-limits"></a>Ограничения скорости

NuGet.org API применяет ограничение скорости, чтобы избежать злонамеренного использования. Запросы, которые превышают ограничение частоты возвращает следующую ошибку: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

В дополнение к регулирование с помощью ограничений скорости запросов некоторые API-интерфейсы также обеспечивают квоты. Запросы, которые превышают квоту возвращает следующую ошибку:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

В следующих таблицах перечислены ограничения скорости для NuGet.org API.

## <a name="package-search"></a>Поиск пакетов

> [!Note]
> Мы рекомендуем использовать для NuGet.org [API-интерфейсы V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) для поиска, который обладает низкой производительностью и каких-либо ограничения в настоящее время. Для версий 1 и 2 поиска API-интерфейсы, followins ограничения относятся:


| API | Тип ограничения | Предельное значение | API usecase |
|:---|:---|:---|:---|
**ПОЛУЧИТЬ** `/api/v1/Packages` | IP | 1000 / мин | Запросить метаданные пакета NuGet с помощью v1 OData `Packages` коллекции |
**ПОЛУЧИТЬ** `/api/v1/Search()` | IP | 3000 / мин | Поиск пакетов NuGet через конечную точку версии 1 поиска | 
**ПОЛУЧИТЬ** `/api/v2/Packages` | IP | 20000 / мин | Запросить метаданные пакета NuGet с помощью v2 OData `Packages` коллекции | 
**ПОЛУЧИТЬ** `/api/v2/Packages/$count` | IP | 100 / мин | Запрос количества пакетов NuGet с помощью v2 OData `Packages` коллекции | 

## <a name="package-push-and-unlist"></a>Пакет Push-уведомлений и удалить из списка

| API | Тип ограничения | Предельное значение | API usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Ключ API | 250 / час | Отправьте новый пакет NuGet (версии) с помощью конечной точки версии 2 Push-уведомлений 
**УДАЛЕНИЕ** `/api/v2/package/{id}/{version}` | Ключ API | 250 / час | Удалить из списка пакет NuGet (версии) с помощью конечной точки версии 2 
