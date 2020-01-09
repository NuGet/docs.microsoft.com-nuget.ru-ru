---
title: Заметки о выпуске NuGet 1,6
description: Заметки о выпуске NuGet 1,6, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384141"
---
 # <a name="nuget-16-release-notes"></a>Заметки о выпуске NuGet 1,6

[Заметки о выпуске nuget 1,5](../release-notes/nuget-1.5.md) | [заметок о выпуске NuGet 1,7](../release-notes/nuget-1.7.md)

Версия NuGet 1,6 была выпущена 13 декабря 2011 г.

## <a name="known-installation-issue"></a>Известная ошибка установки
Если вы используете VS 2010 с пакетом обновления 1 (SP1), при попытке обновить NuGet, если установлена более старая версия, может возникнуть ошибка установки.

Чтобы решить эту проблему, просто удалите NuGet, а затем установите его из коллекции расширений VS.  Дополнительные сведения см. в разделе <https://support.microsoft.com/kb/2581019>.

Примечание. Если Visual Studio не позволит удалить расширение (кнопка удаления отключена), скорее всего, потребуется перезапустить Visual Studio с помощью команды "Запуск от имени администратора".

## <a name="features"></a>Функции

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Поддержка семантического управления версиями и предварительных пакетов
В NuGet 1,6 введена поддержка семантического управления версиями (SemVer). Дополнительные сведения об использовании SemVer см. в [документации по системе управления версиями](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Использование NuGet без возврата пакетов (восстановление пакета)
NuGet 1,6 теперь обладает первой поддержкой класса для рабочего процесса, в котором пакеты NuGet не добавляются в систему управления версиями, а восстанавливаются во время сборки, если они отсутствуют. Дополнительные сведения см. в разделе [Использование NuGet без фиксации пакетов в системе управления версиями](../consume-packages/packages-and-source-control.md) .

### <a name="item-templates-that-install-nuget-packages"></a>Шаблоны элементов, устанавливающие пакеты NuGet
При построении на работе для поддержки предварительно установленного пакета NuGet в шаблонах проектов Visual Studio NuGet 1,6 также добавляет поддержку шаблонов элементов Visual Studio. Шаблоны элементов могут иметь связанные пакеты NuGet, которые устанавливаются при вызове шаблона.

Дополнительные сведения о том, как изменить шаблон проекта или элемента для установки пакетов NuGet, см. в разделе [пакеты в Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) .

### <a name="support-for-disabling-package-sources"></a>Поддержка отключения источников пакетов
Если настроено несколько источников пакетов, NuGet будет просматривать каждый из них для пакетов во время установки пакета и его зависимостей. Источник пакета, который не работает по какой-либо причине, может значительно замедлить работу NuGet.

До NuGet 1,6 можно было удалить источник пакета, но затем необходимо запомнить сведения о том, когда нужно добавить его обратно.

NuGet 1,6 позволяет отменить проверку источника пакета, чтобы отключить его, но не учитывать его.

![Отключение пакета](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Исправления ошибок
В NuGet 1,6 было исправлено всего 106 рабочих элементов. 95 из них были классифицированы как ошибки и 10 из них.

Полный список рабочих элементов, исправленных в NuGet 1,6, см. в [этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
