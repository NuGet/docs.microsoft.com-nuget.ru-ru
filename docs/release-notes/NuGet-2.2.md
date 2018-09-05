---
title: Заметки о выпуске версии 2.2 NuGet
description: Заметки о выпуске для NuGet 2.2, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545996"
---
# <a name="nuget-22-release-notes"></a>Заметки о выпуске версии 2.2 NuGet

[Заметки о выпуске NuGet 2.1](../release-notes/nuget-2.1.md) | [заметки о выпуске NuGet 2.2.1](../release-notes/nuget-2.2.1.md)

NuGet 2.2 была выпущена 12 декабря 2012 г.

## <a name="visual-studio-quick-launch"></a>Быстрый запуск Visual Studio
Одна из новых функций, добавленных в Visual Studio 2012 был [диалоговое окно быстрого запуска](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2.2 расширяет это диалоговое окно, что позволяет инициализировать диалоговое окно диспетчера пакета с условиями поиска, введенные в панели быстрого запуска. Например введя «jquery» на панели быстрого запуска теперь включает в себя параметр в результатах поиска пакетов NuGet по запросу «jquery».

![NuGet в Visual Studio быстрого запуска](./media/quick-launch.png)

При выборе этого параметра приведет к запуску стандартный NuGet пакета диспетчера реализации возможностей поиска для термина «jquery».

![Диалоговое окно диспетчера пакетов NuGet, предварительно заполненный](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Укажите всю папку для пакета содержимого
NuGet 2.2 теперь можно указать всю папку в `<file>` элемент `.nuspec` файл, чтобы включить все содержимое этой папки. Например ниже приведет все скрипты в папке scripts пакета для добавления к папке contents\scripts при установке пакета в проект.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Обновление 6/24/16: пустые папки в папке «content» учитываются при установке пакета.**

## <a name="known-issues"></a>Известные проблемы

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Установка пакета завершается сбоем для проектов F #, при использовании консоли диспетчера пакетов
При попытке установить пакет NuGet в проекте F # с помощью консоли диспетчера пакетов, генерируется исключение InvalidOperationException. Мы активно работаем с группой разработки F # для решения проблемы, но в то же время обходным путем является установка пакетов NuGet в проектах F # с помощью диалогового окна диспетчера пакетов NuGet, а не консоль. [Дополнительные сведения можно найти на сайте CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Исправления ошибок
NuGet 2.2 включает множество исправлений ошибок. Полный список рабочих элементов исправленные в NuGet 2.2, пожалуйста представление [Issue Tracker NuGet для этого выпуска](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
