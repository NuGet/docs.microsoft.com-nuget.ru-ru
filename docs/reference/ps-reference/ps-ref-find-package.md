---
title: Справочник по Find-Package PowerShell для NuGet
description: Справочник по Find-Package команде PowerShell в консоли диспетчера пакетов NuGet в Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 83d0d62bbda07d07ea1e3b58e531447e2001b680
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777507"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (консоль диспетчера пакетов в Visual Studio)

*Версия 3.0 +; в этом разделе описывается команда в [консоли диспетчера пакетов](../../consume-packages/install-use-packages-powershell.md) в Visual Studio в Windows. Общие команды PowerShell Find-Package см. в [справочнике по PackageManagement для PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*

Возвращает набор удаленных пакетов с указанным ИДЕНТИФИКАТОРом или ключевыми словами из источника пакета.

## <a name="syntax"></a>Синтаксис

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| &lt;Ключевые слова ID&gt; | Необходимости Ключевые слова, используемые при поиске в источнике пакета. Используйте параметр-ExactMatch, чтобы получить только те пакеты, идентификатор пакета которых соответствует ключевым словам. Если ключевые слова не заданы, `Find-Package` возвращает список 20 основных пакетов по скачиваниям или число, указанное в параметре-first. Обратите внимание, что-ID является необязательным и не-Op. |
| Источник | URL-адрес или путь к папке для источника пакета для поиска. Пути к локальным папкам могут быть абсолютными или относительно текущей папки. Если этот параметр опущен, `Find-Package` Поиск выполняется в текущем выбранном источнике пакета. |
| AllVersions | Отображает все доступные версии каждого пакета, а не только последнюю версию. |
| First | Число пакетов, возвращаемых с начала списка; значение по умолчанию — 20. |
| Пропустить | Опускает первые &lt; целочисленные &gt; пакеты из отображаемого списка.  |
| инклудепререлеасе | Включает в результаты предварительные пакеты. |
| ExactMatch | Задается для использования &lt; ключевых слов в &gt; качестве идентификатора пакета с учетом регистра. |
| StartWith | Возвращает пакеты, идентификатор пакета которых начинается с &lt; ключевых слов &gt; . |

Ни один из этих параметров не принимает входные данные конвейера или подстановочные знаки.

## <a name="common-parameters"></a>Общие параметры

`Find-Package` поддерживает следующие [Общие параметры PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Отладка, действие при ошибке, ErrorVariable, буфер, переменная, PipelineVariable, Verbose, WarningAction и WarningVariable.

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