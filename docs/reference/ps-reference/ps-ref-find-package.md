---
title: Справочник по PowerShell для поиска NuGet
description: Справочник по командам PowerShell Find-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384637"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (консоль диспетчера пакетов в Visual Studio)

*Версия 3.0 +; в этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Сведения об универсальной команде PowerShell Find-package см. в справочнике по модульу [PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Возвращает набор удаленных пакетов с указанным ИДЕНТИФИКАТОРом или ключевыми словами из источника пакета.

## <a name="syntax"></a>Синтаксис

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| &lt;ключевые слова ID&gt; | Необходимости Ключевые слова, используемые при поиске в источнике пакета. Используйте параметр-ExactMatch, чтобы получить только те пакеты, идентификатор пакета которых соответствует ключевым словам. Если ключевые слова не заданы, `Find-Package` возвращает список первых 20 пакетов по скачиваниям или число, указанное в параметре-first. Обратите внимание, что-ID является необязательным и не-Op. |
| Source | URL-адрес или путь к папке для источника пакета для поиска. Пути к локальным папкам могут быть абсолютными или относительно текущей папки. Если этот параметр опущен, `Find-Package` выполняет поиск выбранного в данный момент источника пакета. |
| AllVersions | Отображает все доступные версии каждого пакета, а не только последнюю версию. |
| First | Число пакетов, возвращаемых с начала списка; значение по умолчанию — 20. |
| Skip | Опускает первые &lt;int&gt; пакеты из отображаемого списка.  |
| инклудепререлеасе | Включает в результаты предварительные пакеты. |
| ExactMatch | Задается для использования ключевых слов &lt;&gt; как идентификатор пакета с учетом регистра. |
| StartWith | Возвращает пакеты, идентификатор пакета которых начинается с &lt;ключевых слов&gt;. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Find-Package` поддерживает следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

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
