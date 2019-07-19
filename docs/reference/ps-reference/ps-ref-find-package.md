---
title: Справочник по PowerShell для поиска NuGet
description: Справочник по командам PowerShell Find-Package в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327391"
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
| Ключевые &lt;слова ID&gt; | Необходимости Ключевые слова, используемые при поиске в источнике пакета. Используйте параметр-ExactMatch, чтобы получить только те пакеты, идентификатор пакета которых соответствует ключевым словам. Если ключевые слова не заданы `Find-Package` , возвращает список 20 основных пакетов по скачиваниям или число, указанное в параметре-first. Обратите внимание, что-ID является необязательным и не-Op. |
| Source | URL-адрес или путь к папке для источника пакета для поиска. Пути к локальным папкам могут быть абсолютными или относительно текущей папки. Если этот параметр опущен `Find-Package` , поиск выполняется в текущем выбранном источнике пакета. |
| AllVersions | Отображает все доступные версии каждого пакета, а не только последнюю версию. |
| Первая | Число пакетов, возвращаемых с начала списка; значение по умолчанию — 20. |
| Skip | Опускает первые &lt;целочисленные&gt; пакеты из отображаемого списка.  |
| инклудепререлеасе | Включает в результаты предварительные пакеты. |
| ExactMatch | Задается &lt;для&gt; использования ключевых слов в качестве идентификатора пакета с учетом регистра. |
| стартвис | Возвращает пакеты, идентификатор пакета которых начинается &lt;с&gt;ключевых слов. |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Find-Package`поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

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
