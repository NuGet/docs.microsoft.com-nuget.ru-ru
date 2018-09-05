---
title: Заметки о выпуске NuGet 2.8.2
description: Заметки о выпуске для NuGet 2.8.2, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551152"
---
# <a name="nuget-282-release-notes"></a>Заметки о выпуске NuGet 2.8.2

[Заметки о выпуске NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [заметки о выпуске NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 было выпущено 22 мая 2014 г.  Этот выпуск включены только изменения командной строки nuget.exe, пакета NuGet.Server и других пакетах NuGet.  Выпуск не включала обновленные расширение Visual Studio или WebMatrix.

## <a name="notable-updates"></a>Важные обновления

Наиболее важные обновления были в командной строки nuget.exe и пакета NuGet.Server (для резидентных веб-каналов NuGet).

### <a name="important-nugetexe-bug-fixes"></a>Nuget.exe важные исправления ошибок

1. [NuGet.exe Push-уведомлений, завершается ошибкой и отслеживает повторная попытка](https://nuget.codeplex.com/workitem/4000)
1. [NuGet.exe Push-уведомлений не отправляет учетные данные обычной проверки подлинности правильно](https://nuget.codeplex.com/workitem/4109)
1. [NuGet.exe Push-уведомлений не следуйте Временное перенаправление](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Исправление ошибки важные NuGet.Server

1. [Неверное значение IsAbsoluteLatestVersion, возвращенный NuGet.Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Пакеты обновлены

Командной строки nuget.exe и NuGet.Server исправления поставляются как обновлений пакета NuGet.  Произошли другие пакеты, обновляется также 2.8.2.

Ниже приведен список обновленных пакетов:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (пакета, не расширения)

## <a name="all-changes"></a>Все изменения
Возникли 10 ошибок, устраненных в выпуске. Полный список рабочих элементов исправленные в NuGet 2.8.2, пожалуйста представление [Issue Tracker NuGet для этого выпуска](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
