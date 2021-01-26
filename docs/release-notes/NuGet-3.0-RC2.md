---
title: Заметки о выпуске NuGet 3,0 RC2
description: Заметки о выпуске NuGet 3,0 RC2, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780283"
---
# <a name="nuget-30-rc2-release-notes"></a>Заметки о выпуске NuGet 3,0 RC2

[Заметки о](../release-notes/nuget-3.0-RC.md)  |  выпуске для версии-кандидата NuGet 3,0 [Заметки о выпуске NuGet 3,0](../release-notes/nuget-3.0.0.md)

Версия NuGet 3,0 RC2 была выпущена 3 июня 2015 в качестве промежуточного выпуска из коллекции расширений Visual Studio 2015 и [CodePlex](https://nuget.codeplex.com/releases/view/615507). В этом выпуске имеется ряд важных исправлений ошибок и улучшений производительности, которые были важны для выпуска до завершения выпуска Visual Studio 2015. Эта версия расширения NuGet доступна только для Visual Studio 2015.

В итоге мы закрыли 158 проблемы в этом выпуске, и вы можете просмотреть [полный список проблем на сайте GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Сводка по устранению основных проблем

* [Частые вызовы сетевых обновлений при обновлении окна диспетчера пакетов](https://github.com/NuGet/Home/issues/515)
* [Отложенная прокрутка при переходе в режим установленного представления в диспетчере пакетов](https://github.com/NuGet/Home/issues/519)
* [Сетевые вызовы должны выполняться в фоновом потоке.](https://github.com/NuGet/Home/issues/516)
* [Добавлен флажок "не показывать окно предварительного просмотра"](https://github.com/NuGet/Home/issues/566)
* [Добавлено регулирование процессов для сокращения загрузки процессора.](https://github.com/NuGet/Home/issues/356)
* Улучшенная обработка ссылок на библиотеки переносимых классов
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Служба автозаполнения с учетом регистра](https://github.com/NuGet/Home/issues/198)
* [Обновление для повторного ввода учетных данных базовой проверки подлинности](https://github.com/NuGet/Home/issues/456)
* [Улучшено ведение журналов ошибок.](https://github.com/NuGet/Home/issues/407)
* [Улучшены сообщения об ошибках PowerShell при вызове Update-Package](https://github.com/NuGet/Home/issues/5)

Скачайте это [Обновление для расширения NuGet](https://nuget.codeplex.com/releases/view/615507) из CodePlex и следите за [нашим блогом](http://blog.nuget.org) , чтобы получить дополнительные сведения о ходе и объявлениях для NuGet 3,0!