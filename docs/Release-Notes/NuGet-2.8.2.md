---
title: Заметки о выпуске NuGet 2.8.2
description: Заметки о выпуске для NuGet 2.8.2, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-282-release-notes"></a>Заметки о выпуске NuGet 2.8.2

[Заметки о выпуске NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 заметки о выпуске](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 был выпущен 22 мая 2014 г.  Этот выпуск включены только изменения командной строки nuget.exe, NuGet.Server пакета и других пакетах NuGet.  Выпуск не содержит обновленные расширение Visual Studio или расширения WebMatrix.

## <a name="notable-updates"></a>Важные обновления

В окне командной строки nuget.exe и NuGet.Server пакета (для резидентных каналы NuGet) были наиболее важные обновления.

### <a name="important-nugetexe-bug-fixes"></a>Исправления важных nuget.exe

1. [NuGet.exe принудительной отправки завершается сбоем и отслеживает повторение попытки](https://nuget.codeplex.com/workitem/4000)
1. [NuGet.exe принудительной правильно не отправлять Обычная проверка подлинности учетных данных](https://nuget.codeplex.com/workitem/4109)
1. [NuGet.exe Push не выполните Временное перенаправление](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Исправление ошибки важные NuGet.Server

1. [Неверное значение IsAbsoluteLatestVersion возвращенных NuGet.Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Пакеты обновления

Nuget.exe командной строки и NuGet.Server исправления поставляются как обновления пакета NuGet.  Нет других пакетов с 2.8.2 также.

Ниже приведен перечень обновленные пакеты.

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (пакета, не расширения)

## <a name="all-changes"></a>Все изменения
Возникли проблемы 10, в выпуске. Полный список рабочих элементов исправления в NuGet 2.8.2, представление [NuGet отслеживания проблем в этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
