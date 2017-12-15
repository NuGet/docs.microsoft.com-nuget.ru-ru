---
title: "Заметки о выпуске NuGet 3.0 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 8ad13a67-9348-4f04-8f8b-b8f4a0b2c6df
description: "Заметки о выпуске для NuGet 3.0.0, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 3.0.0 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 95c4bf92f5eeb676fa6bcc3b7bcbf191efa9cb9e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-release-notes"></a>Заметки о выпуске 3.0 NuGet

[Заметки о выпуске версии-кандидата 2 NuGet 3.0](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 заметки о выпуске](../release-notes/nuget-3.1.md)

NuGet 3.0 как расширение пакета Visual Studio 2015 был выпущен 20 июля 2015 г. Мы помещено доставки этой версии с Visual Studio, чтобы процесс завершения обновленные NuGet 3.0 будет доступен для новых пользователей Visual Studio. Эта версия расширения NuGet доступна только для Visual Studio 2015.

Мы рекомендуем разработчиков, которые имеют доступ к коллекции Visual Studio обновление до последней версии, которая доступна, как мы публикуем обновления вскоре после выпуска Visual Studio 2015, который включает в себя поддержку для разработки приложений Windows 10.

В итоге мы закрытых 240 проблем в версии 3.0, и можно будет просмотреть [полный список проблем на GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Известные проблемы

Несколько известных проблем, присутствующие в этом выпуске, и все эти элементы являются исправлено в нашем запланированных 3.1 совпадают с выпуска Windows 10 29 июля.  Можно обновить расширение Visual Studio из коллекции в течение или после этой даты, чтобы устранить эти проблемы.

*  Перевод для метки «Больше не показывать» в окне предварительного просмотра и метка «Авторы» в окне описания пакета не поддерживается.
*  Если при работе над проектом с помощью TFS система управления версиями, NuGet нельзя представить диспетчер пакетов пользовательский интерфейс при Nuget.Config файл помечен как доступный только для чтения.
   * **Инструкции по решению** извлечь файл из Team Foundation Server.
*  Текст в желтый «перезапуск панель» в окне NuGet Powershell не отображается при использовании темной темами Visual Studio.
   * **Инструкции по решению** использование светлого оформления Visual Studio.


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
* [Исправлена ссылку «Дополнительные сведения о параметрах», чтобы предотвратить сбой в Windows 10](https://github.com/NuGet/Home/issues/822)
* [Следует помнить флажок предварительного выпуска параметр](https://github.com/NuGet/Home/issues/732)
* [Улучшенная сбора производительности путем кэширования результатов между проектами в решении](https://github.com/NuGet/Home/issues/721)
* [Параллельно можно собрать несколько пакетов](https://github.com/NuGet/Home/issues/713)
* [Удалить пакет установки-force команды](https://github.com/NuGet/Home/issues/697)

Пожалуйста, обратите внимание на [наш блог](http://blog.nuget.org) дополнительные хода выполнения и объявления как мы получаем готовы к предоставлению поддержка разработки Windows 10.