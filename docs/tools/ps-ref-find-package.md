---
title: Справочник по PowerShell NuGet Find-Package
description: Ссылка для команды PowerShell Find-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842526"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (консоль диспетчера пакетов в Visual Studio)

*3.0 и более поздних версиях; в этом разделе описываются команды в [консоль диспетчера пакетов](package-manager-console.md) в Visual Studio в Windows. Общая команда PowerShell Find-Package, см. в разделе [Справочник по PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Получает набор удаленные пакеты с указанным Идентификатором или ключевые слова из источника пакета.

## <a name="syntax"></a>Синтаксис

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Идентификатор &lt;ключевые слова&gt; | (Обязательно) Ключевые слова для поиска источника пакета. С помощью - ExactMatch возвращать только те пакеты, в которых идентификатор пакета соответствует ключевые слова. Если ключевые слова не заданы, `Find-Package` возвращает список пакетов 20 наиболее популярных загрузок или номер, указанных по — сначала. Обратите внимание, что - идентификатор не является обязательным и холостой. |
| Source | Путь к URL-адрес или папке источника пакета для поиска. Пути к локальной папке может быть абсолютным или относительным для текущей папки. Если этот параметр опущен, `Find-Package` выполняет поиск в текущем выбранном источнике пакета. |
| AllVersions | Отображает все доступные версии каждого пакета, а не только последнюю версию. |
| Первая | Количество возвращаемых пакетов из начала списка. значение по умолчанию — 20. |
| Skip | Пропускает первый &lt;int&gt; пакеты из отображаемого списка.  |
| IncludePrerelease | Включает в себя предварительные выпуски пакетов в результатах. |
| ExactMatch | Указанный для использования &lt;ключевые слова&gt; как идентификатор пакета, с учетом регистра. |
| StartWith | Возвращает пакеты, пакета, идентификатор начинается с &lt;ключевые слова&gt;. |

Ни один из этих параметров принимает входные данные или подстановочный знак символов конвейера.

## <a name="common-parameters"></a>Общие параметры

`Find-Package` поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при возникновении ошибки, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction и WarningVariable.

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
