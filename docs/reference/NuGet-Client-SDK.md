---
title: Пакет SDK клиента NuGet
description: API развивается и еще не документирован, но примеры доступны в блоге Дейв Гликк.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924605"
---
# <a name="nuget-client-sdk"></a>Пакет SDK клиента NuGet

*Клиентский пакет SDK для NuGet* ссылается на группу пакетов NuGet, которые находятся в центре по отношению к [NuGet. Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet. Packaging](https://www.nuget.org/packages/NuGet.Packaging)и [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol). Эти пакеты заменяют предыдущую библиотеку [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) .

> [!Note]
>  Документацию по протоколу сервера NuGet см. в [API сервера NuGet](~/api/overview.md).

## <a name="source-code"></a>Исходный код

Исходный код публикуется на сайте GitHub в проекте [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Документация по сторонним производителям

Примеры и документацию для некоторых API-интерфейсов можно найти в следующем ряде блогов: Дейв Гликк, Опубликовано 2016.

- [Изучение библиотек NuGet версии 3, часть 1. Введение и основные понятия](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Изучение библиотек NuGet версии 3. часть 2. Поиск пакетов](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Изучение библиотек NuGet v3, часть 3. Установка пакетов](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Эти записи блога были написаны вскоре после выпуска **3.4.3** версии пакетов SDK клиента NuGet.
> Более новые версии пакетов могут быть несовместимы с данными в записях блога.

"Мартен Бжöркстрöм" выполнил следующую запись блога в серии блогов Дейв Гликк, где он вводит другой подход к использованию пакета SDK клиента NuGet для установки пакетов NuGet:

- [Повторное посещение библиотек NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
