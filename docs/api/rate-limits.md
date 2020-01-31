---
title: Пределы скорости, API NuGet
description: Интерфейсы API NuGet применяют ограничения скорости для предотвращения нарушения.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813199"
---
# <a name="rate-limits"></a>Ограничения скорости

API NuGet.org обеспечивает ограничение скорости для предотвращения нарушения. Запросы, превышающие предел скорости, возвращают следующую ошибку: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Помимо регулирования запросов с использованием пределов скорости, некоторые API также применяют квоту. Запросы, превышающие квоту, возвращают следующую ошибку:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

В следующих таблицах перечислены ограничения скорости для API NuGet.org.

## <a name="package-search"></a>Поиск пакета

> [!Note]
> Мы рекомендуем использовать API-интерфейсы для [поиска версии 3](search-query-service-resource.md) NuGet. org, так как в настоящее время это не слишком мало частоты. Для API-интерфейсов поиска v1 и v2 применяются следующие ограничения.

| API | Тип ограничения | Значение ограничения | API UseCase |
|:---|:---|:---|:---|
**Получить** `/api/v1/Packages` | IP | 1000/мин | Запрос метаданных пакета NuGet через v1 `Packages` коллекция OData |
**Получить** `/api/v1/Search()` | IP | 3000/мин | Поиск пакетов NuGet с помощью конечной точки поиска v1 | 
**Получить** `/api/v2/Packages` | IP | 20000/мин | Запрос метаданных пакета NuGet через v2 `Packages` коллекция OData | 
**Получить** `/api/v2/Packages/$count` | IP | 100/мин | Запрос числа пакетов NuGet через v2 `Packages` коллекция OData | 

## <a name="package-push-and-unlist"></a>Отправка и вывод пакетов

| API | Тип ограничения | Значение ограничения | API UseCase | 
|:---|:---|:---|:--- |
**Разместить** `/api/v2/package` | Ключ API | 350 в час | Отправка нового пакета NuGet с помощью конечной точки push-уведомлений версии 2 
**Удалить** `/api/v2/package/{id}/{version}` | Ключ API | 250 в час | Отменяет список пакетов NuGet (версии) с помощью конечной точки версии 2 
