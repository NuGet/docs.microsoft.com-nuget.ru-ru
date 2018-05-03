---
title: Справочник по PowerShell NuGet Find-Package
description: Ссылка для команды Find-Package PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 0faf5c5cf9ae99105e3d76a4f5e37f164c4f4ff3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (консоль диспетчера пакетов в Visual Studio)

*Версия 3.0 +; в этом разделе описываются команды в [консоль диспетчера пакетов NuGet](package-manager-console.md) в Visual Studio в Windows. Общая команда PowerShell Find-Package. в разделе [PowerShell PackageManagement ссылка](/powershell/module/packagemanagement/?view=powershell-6).*

Получает набор удаленных пакетов с указанным Идентификатором или ключевые слова из источника пакета.

## <a name="syntax"></a>Синтаксис

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Идентификатор &lt;ключевые слова&gt; | (Обязательно) Ключевые слова для поиска источника пакета. С помощью - ExactMatch возвращать только те пакеты, ключевые слова совпадает с Идентификатором пакета. Если ключевые слова не заданы, `Find-Package` возвращает список пакетов 20 основных по загрузок или номер заданные - сначала. Обратите внимание, что - идентификатор является необязательным и холостой. |
| Исходный код | Путь URL-адрес или папку источника пакета для поиска. Пути к локальной папке может быть абсолютным или относительным для текущей папки. Если не указано, `Find-Package` выполняет поиск в текущем выбранном источнике пакетов. |
| AllVersions | Отображает все доступные версии каждого пакета, а не только последняя версия. |
| First | Число пакетов, возвращаемых из начала списка; значение по умолчанию — 20. |
| Skip | Пропускает первый &lt;int&gt; пакеты из списка.  |
| IncludePrerelease | Предварительные выпуски пакетов включает в результаты. |
| ExactMatch | Указанный для использования &lt;ключевые слова&gt; как идентификатор пакета с учетом регистра. |
| StartWith | Возвращает пакеты, пакет идентификатор начинается с &lt;ключевые слова&gt;. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Find-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

## <a name="examples"></a>Примеры

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
