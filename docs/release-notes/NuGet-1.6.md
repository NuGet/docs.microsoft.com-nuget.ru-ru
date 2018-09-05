---
title: Заметки о выпуске 1,6 NuGet
description: Заметки о выпуске для NuGet 1.6, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549016"
---
 # <a name="nuget-16-release-notes"></a>Заметки о выпуске 1,6 NuGet

[Заметки о выпуске NuGet 1.5](../release-notes/nuget-1.5.md) | [заметки о выпуске NuGet 1.7](../release-notes/nuget-1.7.md)

NuGet 1.6 было выпущено 13 декабря 2011 г.

## <a name="known-installation-issue"></a>Известные проблемы
Если вы используете VS 2010 SP1, вы можете столкнуться ошибка установки при попытке обновить NuGet, если у вас установлена более ранняя версия.

Обойти это просто удалить диспетчер NuGet, а затем установить его из коллекции расширений VS.  Дополнительные сведения см. в разделе [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Примечание: Если Visual Studio не позволяют удалить расширение (кнопка "Удалить" отключена), скорее всего, потребуется перезапустить Visual Studio, используя «Запуск от имени администратора».

## <a name="features"></a>Функции

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Поддержка семантического управления версиями и предварительные версии пакетов
NuGet 1.6 введена поддержка семантическое Версионирование (SemVer). Дополнительные сведения об использовании SemVer см [управление версиями документации](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>С помощью NuGet без проверки в пакетах (восстановление пакетов)
NuGet 1.6 теперь имеет превосходную поддержку рабочего процесса, в какие NuGet не добавляются в систему управления версиями пакетов, но вместо этого будут восстановлены во время сборки, если отсутствует. Дополнительные сведения см. в статье [с помощью NuGet без фиксации пакетов в системе управления версиями](../consume-packages/packages-and-source-control.md) раздела.

### <a name="item-templates-that-install-nuget-packages"></a>Шаблоны элементов, установка пакетов NuGet
Основываясь на работает для поддержки предварительно установленного пакета NuGet в шаблоны проектов Visual Studio, NuGet 1.6 также добавлена поддержка шаблонов элементов Visual Studio. Шаблоны элементов могут иметь связанные пакеты NuGet, установленные при вызове шаблона в.

Дополнительные сведения о том, как изменять шаблоны проектов и элементов для установки пакетов NuGet см [пакеты в шаблонах Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) раздела.

### <a name="support-for-disabling-package-sources"></a>Поддержка отключения источников пакетов
После настройки нескольких источников пакетов NuGet будет выглядеть в каждом из них для пакетов во время установки пакета и его зависимости. Источник пакета, который не работает, для какой-либо причине может значительно замедлить NuGet.

До NuGet 1.6 можно удалить источника пакета, но необходимо помнить, что сведения, если требуется добавить его обратно в.

NuGet 1.6 позволяет, сняв флажок источника пакета, чтобы отключить его, но держите его.

![Отключение пакета](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Исправления ошибок
NuGet 1.6 было всего 106 рабочие элементы фиксированной. 95 из них были классифицированы как ошибки и 10 из них были функции.

Полный список рабочих элементов исправленные в NuGet 1.6, пожалуйста представление [Issue Tracker NuGet для этого выпуска](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
