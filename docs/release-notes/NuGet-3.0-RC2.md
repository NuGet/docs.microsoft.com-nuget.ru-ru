---
title: Заметки о выпуске версии-кандидата 2 NuGet 3.0
description: Заметки о выпуске NuGet 3.0 RC2 включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eb8b514fa967cc6ef850483b6b2a5df3ab27a550
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819888"
---
# <a name="nuget-30-rc2-release-notes"></a>Заметки о выпуске версии-кандидата 2 NuGet 3.0

[Заметки о выпуске версии-Кандидата NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [заметки о выпуске NuGet 3.0](../release-notes/nuget-3.0.0.md)

Промежуточный выпуск доступен из галереи расширений Visual Studio 2015 NuGet 3.0 RC2 был выпущен 3 июня 2015 г. и [Codeplex](https://nuget.codeplex.com/releases/view/615507). Этот выпуск содержит ряд важных исправлений и повышение производительности, мы полагаем, было необходимо освободить до завершения выпуска Visual Studio 2015. Эта версия расширения NuGet доступна только для Visual Studio 2015.

В итоге мы закрытых 158 проблем в этом выпуске, и можно будет просмотреть [полный список проблем на GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Сводка по верхней устранения проблем

* [Обновления сети часто вызывается, когда обновляет окно диспетчера пакетов](https://github.com/NuGet/Home/issues/515)
* [Отложенная прокрутки установленные изменение на представление в диспетчере пакетов](https://github.com/NuGet/Home/issues/519)
* [Сетевые вызовы должны выполняться в фоновом потоке](https://github.com/NuGet/Home/issues/516)
* [Добавить флажок «Больше не показывать окно предварительного просмотра»](https://github.com/NuGet/Home/issues/566)
* [Добавленный процесс регулирования для уменьшения использования процессора](https://github.com/NuGet/Home/issues/356)
* Улучшенная обработка библиотек классов portable ссылки
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Автозаполнение служба была с учетом регистра](https://github.com/NuGet/Home/issues/198)
* [Обновления, чтобы повторно ввести учетные данные Обычная проверка подлинности](https://github.com/NuGet/Home/issues/456)
* [Улучшенная Ошибка ведения журнала](https://github.com/NuGet/Home/issues/407)
* [Powershell улучшенные сообщения об ошибках при вызове пакета обновления](https://github.com/NuGet/Home/issues/5)

Загрузить это [обновления с расширением NuGet](https://nuget.codeplex.com/releases/view/615507) на сайте Codeplex и проверьте следить за [наш блог](http://blog.nuget.org) дополнительные хода выполнения и объявления для NuGet 3.0!