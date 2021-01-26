---
title: Заметки о выпуске 2.8.2 NuGet
description: Заметки о выпуске NuGet 2.8.2, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780367"
---
# <a name="nuget-282-release-notes"></a>Заметки о выпуске 2.8.2 NuGet

[Заметки о](../release-notes/nuget-2.8.1.md)  |  выпуске 2.8.1 NuGet [Заметки о выпуске 2.8.3 NuGet](../release-notes/nuget-2.8.3.md)

2.8.2 NuGet выпущен 22 мая, 2014.  Этот выпуск включал только изменения в командной строке nuget.exe, пакете NuGet. Server и других пакетах NuGet.  Выпуск не включал в себя обновленное расширение Visual Studio или расширение WebMatrix.

## <a name="notable-updates"></a>Важные обновления

Наиболее важные обновления находились в командной строке nuget.exe и пакете NuGet. Server (для самостоятельно размещенных веб-каналов NuGet).

### <a name="important-nugetexe-bug-fixes"></a>Важные исправления ошибок nuget.exe

1. [ Сбой принудительной отправкиnuget.exe и повторная попытка](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe принудительная отправка неправильно отправляет учетные данные обычной проверки подлинности](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe push-уведомления не подчиняются временному перенаправлению](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Важное исправление ошибки NuGet. Server

1. [Неверное значение Исабсолутелатестверсион, возвращенное NuGet. Server](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Пакеты обновлены

Исправления командной строки nuget.exe и NuGet. Server поставляются как обновления пакетов NuGet.  Существуют и другие пакеты, обновленные с помощью 2.8.2.

Ниже приведен список обновленных пакетов.

1. [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet. Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (пакет, а не расширение)

## <a name="all-changes"></a>Все изменения
В выпуске было решено 10 проблем. Полный список рабочих элементов, исправленных в NuGet 2.8.2, см. в [этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
