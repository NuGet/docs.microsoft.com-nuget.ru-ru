---
title: Заметки о выпуске NuGet 3,0
description: Заметки о выпуске NuGet 3.0.0, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776557"
---
# <a name="nuget-30-release-notes"></a>Заметки о выпуске NuGet 3,0

[Заметки о](../release-notes/nuget-3.0-RC2.md)  |  выпуске NuGet 3,0 RC2 [Заметки о выпуске NuGet 3,1](../release-notes/nuget-3.1.md)

Пакет NuGet 3,0 был выпущен 20 июля 2015 в качестве расширения пакета для Visual Studio 2015. Мы отправили этот выпуск в Visual Studio, чтобы полностью обновленный интерфейс NuGet 3,0 был доступен для новых пользователей Visual Studio. Эта версия расширения NuGet доступна только для Visual Studio 2015.

Рекомендуется, чтобы разработчики, у которых есть доступ к коллекции Visual Studio, были обновлены до последней доступной версии, так как публикация обновления выполняется вскоре после выпуска Visual Studio 2015, который содержит поддержку для разработки Windows 10.

В итоге мы закрыли 240 проблемы в выпуске 3,0, и можете ознакомиться с [полным списком проблем на сайте GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Известные проблемы

В этом выпуске имеется ряд известных проблем, и все эти элементы исправлены в запланированном 3,1 выпуске, чтобы совпадать с выпуском Windows 10 на 29 июля.  Вы можете обновить расширение Visual Studio из коллекции на эту дату или позже, чтобы устранить эти известные проблемы.

*  Не указано преобразование метки "больше не показывать" в окне предварительного просмотра и метки "Authors" в окне описания пакета.
*  При работе над проектом с помощью системы управления версиями TFS NuGet не может предоставить пользовательский интерфейс диспетчера пакетов, если файл Nuget.Config помечен как "только для чтения".
   * **Обходной путь** Извлеките файл из TFS.
*  Текст в желтой строке "перезагрузка" в окне PowerShell NuGet не отображается при использовании темной темы Visual Studio.
   * **Обходной путь** Используйте тему "светлое" Visual Studio.


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
* [Исправлена ссылка "Подробнее о вариантах", чтобы предотвратить сбой в Windows 10](https://github.com/NuGet/Home/issues/822)
* [Запоминать параметр флажка предварительного выпуска](https://github.com/NuGet/Home/issues/732)
* [Повышение производительности сбора путем кэширования результатов по проектам в решении](https://github.com/NuGet/Home/issues/721)
* [Несколько пакетов можно собирать параллельно](https://github.com/NuGet/Home/issues/713)
* [Удалена команда install-Package-Force](https://github.com/NuGet/Home/issues/697)

Следите за [нашим блогом](http://blog.nuget.org) , чтобы получить дополнительные сведения и объявления о том, как мы готовы предоставить поддержку для разработки Windows 10.