---
title: Заметки о выпуске NuGet 3.0 RC2
description: Заметки о выпуске NuGet 3.0 RC2 включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545825"
---
# <a name="nuget-30-rc2-release-notes"></a>Заметки о выпуске NuGet 3.0 RC2

[Заметки о выпуске версии-Кандидата NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [заметки о выпуске NuGet 3.0](../release-notes/nuget-3.0.0.md)

NuGet 3.0 RC2 было выпущено 3 июня 2015 г., промежуточный выпуск доступен из коллекции расширений Visual Studio 2015 и [Codeplex](https://nuget.codeplex.com/releases/view/615507). Этот выпуск содержит ряд важных исправлений и улучшений производительности, которые мы полагаем, использовались для того освободить до завершения выпуска Visual Studio 2015. Эта версия расширения NuGet доступна только для Visual Studio 2015.

В целом, мы закрытых 158 проблем в этом выпуске, и вы можете просмотреть [полный список проблем на GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Сводка по устранить основные проблемы

* [Обновление сети часто вызывается, когда обновляет окно диспетчера пакетов](https://github.com/NuGet/Home/issues/515)
* [Отложенной прокрутки, при изменении на установке представление в диспетчере пакетов](https://github.com/NuGet/Home/issues/519)
* [Сетевые вызовы, которые должны выполняться в фоновом потоке](https://github.com/NuGet/Home/issues/516)
* [Добавлен флажок «Больше не показывать окно предварительного просмотра»](https://github.com/NuGet/Home/issues/566)
* [Добавленный процесс, регулирование, чтобы снизить использование процессора](https://github.com/NuGet/Home/issues/356)
* Улучшенную обработку справочном руководстве библиотеки portable классов
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Автозаполнение служба была с учетом регистра](https://github.com/NuGet/Home/issues/198)
* [Обновления, чтобы повторно ввести учетные данные обычной проверки подлинности](https://github.com/NuGet/Home/issues/456)
* [Улучшено ведение журналов ошибок](https://github.com/NuGet/Home/issues/407)
* [Powershell улучшенные сообщения об ошибках при вызове Update-Package](https://github.com/NuGet/Home/issues/5)

Скачайте это [обновления для расширения NuGet](https://nuget.codeplex.com/releases/view/615507) веб-сайте Codeplex и Пожалуйста Обратите внимание на [наш блог](http://blog.nuget.org) дополнительные ход выполнения и объявления для NuGet 3.0!