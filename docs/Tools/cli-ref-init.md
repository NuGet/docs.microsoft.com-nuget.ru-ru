---
title: "Команду NuGet CLI init | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Справочник по команде init nuget.exe"
keywords: "Справочник по init NuGet, команда init"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a>команда init (NuGet CLI)

**Применяется к:** Создание пакета &bullet; **поддерживаемые версии:** 3.3 +

Копирует все пакеты из папки на жестком диске в папку назначения с помощью иерархическом виде, как описано для [добавьте команду](#add) выше. То есть с использованием `init` эквивалентно использованию `add` на каждый пакет в папке.

Как и в `add`, то следует локальную папку или UNC-путь; HTTP пакета репозиториев, таких как nuget.org или закрытый серверы не поддерживаются.

## <a name="usage"></a>Использование

```
nuget init <source> <destination> [options]
```

где `<source>` — папка, содержащая пакеты и `<destination>` — это локальная папка или путь UNC, на который будут скопированы пакеты.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
| ForceEnglishOutput | *(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Expand | Добавляет все файлы в каждом пакете, который добавляется к источнику пакета; то же, что `-Expand` с `add` команды. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*. |

См. также [переменные среды](cli-ref-environment-variables.md)

## <a name="examples"></a>Примеры

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
