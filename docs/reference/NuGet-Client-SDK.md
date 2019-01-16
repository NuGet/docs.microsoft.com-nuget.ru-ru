---
title: Пакет SDK для клиента NuGet
description: API-Интерфейс является развивающейся и еще не рассматриваются, но примеры доступны в блоге Дэйв Глику.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 97ed3ec7d41d2847c0521af69373a1871eb585dd
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324686"
---
# <a name="nuget-client-sdk"></a>Пакет SDK для клиента NuGet

> [!Note]
> Не следует путать с [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)

*Пакет SDK для клиента NuGet* относится к группе библиотек .NET вокруг [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), и [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol). Эти пакеты замените раннюю [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) библиотеки.

Мы работаем над наличие стабильной контактную зону, который мы скоро документировать.

## <a name="source-code"></a>Исходный код

Исходный код публикуется на сайте GitHub в проекте [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Документацией

Примеры и документация для некоторые API-Интерфейсы можно найти в следующей серии публикаций в блоге, Дэйв Глику, опубликованные 2016:

- [Изучение библиотек NuGet v3, часть 1: Введение и основные понятия](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Изучение библиотек NuGet v3, часть 2: Поиск пакетов](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Изучение библиотек NuGet v3, часть 3: Установка пакетов](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Эти сообщения в блогах были написаны вскоре после **3.4.3** версию NuGet, выпущенные пакеты SDK для клиента.
> Более новые версии пакетов могут быть несовместимы с информацией в записях блога.

Мартин Björkström сделали исполнению блога к серии публикаций в блоге Дэйв Глику, где он представляет другой подход по использованию клиентский пакет SDK NuGet для установки пакетов NuGet:

- [Возвращаясь к библиотек NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
