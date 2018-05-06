---
title: Пределы NuGet API скорости
description: API-интерфейсы NuGet будет обязательные пределы скорости для предотвращения нарушений.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: e236d685a700d0f47480336cece8edfd44c28863
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
---
# <a name="rate-limits"></a>Ограничения скорости

NuGet.org API применяет ограничение скорости для предотвращения нарушений. Запросы, превышающие ограничение частоты возвращает следующую ошибку: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

В следующих таблицах перечислены ограничения скорости для NuGet.org API.

## <a name="package-search"></a>Поиск пакетов

> [!Note]
> Мы рекомендуем использовать NuGet.org [API-интерфейсы V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) для поиска, которые обращаются и не имеющие ограничить в настоящее время. Для V1 и V2 поиск интерфейсов API, followins ограничения относятся:


| API | Ограничение типа | Предельное значение | API usecase |
|:---|:---|:---|:---|
**ПОЛУЧИТЬ** `/api/v1/Packages` | IP | 1000 / мин | Запросить метаданные пакета NuGet через v1 OData `Packages` коллекции |
**ПОЛУЧИТЬ** `/api/v1/Search()` | IP | 3000 / мин | Поиск пакетов NuGet через конечную точку поиска v1 | 
**ПОЛУЧИТЬ** `/api/v2/Packages` | IP | 20000 / мин | Запросить метаданные пакета NuGet через v2 OData `Packages` коллекции | 
**ПОЛУЧИТЬ** `/api/v2/Packages/$count` | IP | 100 / мин | Запросить число пакета NuGet через v2 OData `Packages` коллекции | 

## <a name="package-push-and-unlist"></a>Пакет Push и исключить

| API | Ограничение типа | Предельное значение | API usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Ключ API | 100 / мин | Отправьте новый пакет NuGet (версия) через конечную точку принудительной v2 
**УДАЛИТЬ** `/api/v2/package/{id}/{version}` | Ключ API | 100 / мин | Исключить пакет NuGet (версия) через конечную точку v2 
