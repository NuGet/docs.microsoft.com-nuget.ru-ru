---
title: "Заметки о выпуске NuGet 2.2 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 25389d8c-e7db-4920-ab5e-cff20cebee7e
description: "Заметки о выпуске для NuGet 2.2, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.2 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1f6080e01777431c4dfb2278db167bd3bc9a67ea
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-22-release-notes"></a>Заметки о выпуске версии 2.2 NuGet

[Заметки о выпуске NuGet 2.1](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 заметки о выпуске](../release-notes/nuget-2.2.1.md)

12 декабря 2012 года была выпущена NuGet 2.2.

## <a name="visual-studio-quick-launch"></a>Быстрый запуск Visual Studio
Одна из новых функций, добавленные в Visual Studio 2012 была [диалогового окна быстрого запуска](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2.2 расширяет это диалоговое окно, что позволяет инициализировать диалоговое окно диспетчера пакета с условиями поиска, введенных на панели быстрого запуска. Например введите «jquery» на панели быстрого запуска теперь содержит параметр в результатах поиска соответствия «jquery» пакеты NuGet.

![NuGet в Visual Studio быстрого запуска](./media/quick-launch.png)

При выборе этого параметра приведет к запуску результатов поиска диспетчера пакета Стандартная NuGet для термина «jquery».

![Диалоговое окно диспетчера пакетов NuGet предварительно заполненных](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Укажите всю папку для пакета содержимого
NuGet 2.2 теперь можно указать всю папку, в `<file>` элемент `.nuspec` файла следует включить все содержимое этой папки. Например следующие приведет все скрипты в папке скриптов пакет добавляется в папку contents\scripts при установке пакета в проект.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Обновить 24/6/16: пустые папки в папку «content» учитываются при установке пакета.**

## <a name="known-issues"></a>Известные проблемы

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>При использовании консоли диспетчера пакетов для проектов F # сбой установки пакета
При попытке установить пакет NuGet в проекте F #, используя консоль диспетчера пакетов, выдается исключение InvalidOperationException. Мы активно работаем команде F #, чтобы устранить проблему, но в то же время достаточно установить пакеты NuGet в проектов F # с помощью диалогового окна диспетчера пакетов NuGet, а не консоли. [Дополнительные сведения можно найти на сайте CodePlex](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Исправления ошибок
NuGet 2.2 содержит много исправлений ошибок. Полный список рабочих элементов исправления в NuGet 2.2, представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
