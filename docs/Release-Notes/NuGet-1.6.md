---
title: "Заметки о выпуске NuGet 1.6 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 1.6, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 1.6 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 114b03cede24dee520ace1d8aa920a648ad16af1
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
 # <a name="nuget-16-release-notes"></a>Заметки о выпуске 1,6 NuGet

[Заметки о выпуске NuGet 1.5](../release-notes/nuget-1.5.md) | [NuGet 1.7 заметки о выпуске](../release-notes/nuget-1.7.md)

13 декабря 2011 года была выпущена NuGet 1.6.

## <a name="known-installation-issue"></a>Известные проблемы
Если вы используете VS 2010 с пакетом обновления 1, вы можете столкнуться ошибка установки при попытке обновить NuGet, если у вас установлена более ранняя версия.

Достаточно просто удалить NuGet, а затем установить его из библиотеки расширения VS.  Дополнительные сведения см. на странице по адресу [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Примечание: Если Visual Studio не позволяют удалить расширение (кнопка удаления отключена), скорее всего, необходимо перезапустить Visual Studio, используя «Запуск от имени администратора».

## <a name="features"></a>Функции

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Поддержка семантического управления версиями и предварительные версии пакетов
NuGet 1.6 появилась поддержка семантического управления версиями (SemVer). Дополнительные сведения об использовании SemVer чтения [управление версиями документации](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>С помощью NuGet без проверки в пакетах (восстановление пакета)
NuGet 1.6 теперь полностью поддерживает для рабочего процесса, в какие NuGet пакеты не добавляются в систему управления версиями, но вместо этого будут восстановлены во время построения, если отсутствует. Дополнительные сведения см. в статье [с помощью NuGet без фиксации пакетов в систему управления версиями](../consume-packages/packages-and-source-control.md) раздела.

### <a name="item-templates-that-install-nuget-packages"></a>Шаблоны элементов, установить пакеты NuGet
Основываясь на работает для поддержки предварительно установленного пакета NuGet для шаблонов проектов Visual Studio, NuGet 1.6 также добавляет поддержку для шаблонов элементов Visual Studio. Шаблоны элементов могут иметь связанные пакеты NuGet, которые устанавливаются при вызове шаблона.

Дополнительные сведения о способах изменения шаблона проекта или элемента для установки пакетов NuGet читать [пакетов в Visual Studio шаблоны](../visual-studio-extensibility/visual-studio-templates.md) раздела.

### <a name="support-for-disabling-package-sources"></a>Поддержка отключения источники пакетов
При настройке нескольких источников пакета NuGet будет выглядеть в каждом из них для пакетов во время установки пакета и его зависимости. Источник пакета, не работает для какой-либо причине может значительно замедлить NuGet.

До NuGet 1.6 источника пакета можно удалить, но вам придется запоминать подробности при необходимости добавьте его обратно в.

NuGet 1.6 позволяет источнику пакета, чтобы отключить его, но сохранить его вокруг сняв флажок.

![Отключение пакета](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Исправления ошибок
NuGet 1.6 было всего 106 рабочие элементы фиксированной. 95 те из них были классифицируются как ошибки и 10 из них были функции.

Полный список рабочих элементов исправления в NuGet версии 1.6, представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
