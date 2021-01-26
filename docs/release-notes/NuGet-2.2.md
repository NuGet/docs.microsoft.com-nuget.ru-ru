---
title: Заметки о выпуске NuGet 2,2
description: Заметки о выпуске NuGet 2,2, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780437"
---
# <a name="nuget-22-release-notes"></a>Заметки о выпуске NuGet 2,2

[Заметки о](../release-notes/nuget-2.1.md)  |  выпуске NuGet 2,1 [Заметки о выпуске NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

Версия NuGet 2,2 была выпущена 12 декабря 2012 г.

## <a name="visual-studio-quick-launch"></a>Быстрый запуск Visual Studio
Одной из новых функций, добавленных в Visual Studio 2012, было [диалоговое окно быстрого запуска](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2,2 расширяет это диалоговое окно, позволяя ему инициализировать диалоговое окно диспетчера пакетов с помощью условий поиска, вводимых в области Быстрый запуск. Например, если ввести "jQuery" в быстрый запуск, в результатах поиска можно искать пакеты NuGet, соответствующие "jQuery".

![Быстрый запуск NuGet в Visual Studio](./media/quick-launch.png)

При выборе этого параметра будет запущен стандартный интерфейс поиска диспетчера пакетов NuGet для термина jQuery.

![Диалоговое окно диспетчера пакетов NuGet предварительно заполнено](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Указать всю папку для содержимого пакета
NuGet 2,2 теперь позволяет указать всю папку в `<file>` элементе `.nuspec` файла, чтобы включить все содержимое этой папки. Например, следующий сценарий приведет к добавлению всех скриптов в папке Scripts пакета в папку контентс\скриптс при установке пакета в проект.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Обновление 6/24/16: при установке пакета пустые папки в папке "содержимое" игнорируются.**

## <a name="known-issues"></a>Известные проблемы

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Сбой установки пакета для проектов F # при использовании консоли диспетчера пакетов
При попытке установить пакет NuGet в проект F # с помощью консоли диспетчера пакетов создается исключение InvalidOperationException. Мы активно работаем с командой F # для устранения проблемы, но в то же время обходной путь заключается в установке пакетов NuGet в проекты F # с помощью диалогового окна диспетчера пакетов NuGet, а не консоли. [Дополнительные сведения можно найти на сайте CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Исправления ошибок
NuGet 2,2 включает множество исправлений ошибок. Полный список рабочих элементов, исправленных в NuGet 2,2, см. в [этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
