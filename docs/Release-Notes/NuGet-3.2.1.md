---
title: "Заметки о выпуске NuGet 3.2.1 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: d27c3bb9-8db1-439a-a134-54e20b7a7766
description: "Заметки о выпуске для NuGet 3.2.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 3.2.1 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2001d9518a34bbd5f2879de6123ec13abf4ae08
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-321-release-notes"></a>Заметки о выпуске NuGet 3.2.1

[Заметки о выпуске NuGet 3.2](../release-notes/nuget-3.2.md) | [NuGet 3.3 заметки о выпуске](../release-notes/nuget-3.3.md)

NuGet 3.2.1 для командной строки был выпущен 12 октября 2015 г. с небольшое количество оптимизаций и исправления для версии 3.2 и доступен из [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Усовершенствования

* NuGet теперь использует файл конфигурации с исходного регистр `NuGet.Config`.  Это важно, с учетом регистра в операционных системах [1427](https://github.com/NuGet/Home/issues/1427)
* Восстановление NuGet теперь будет игнорировать проектов dnx (`*.xproj`), которые должны быть обработаны с `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Оптимизации использования сети при работе с `index.json` и данные регистрации пакета [1426](https://github.com/NuGet/Home/issues/1426)
* Улучшенная ресурсов загрузки обработки для повышения надежности со службами v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Исправления

* Обновление NuGet правильно обновляет `.csproj` / `.vcxproj` ссылки [1483](https://github.com/NuGet/Home/issues/1483)
* Теперь предотвращая папка локального .nuget при SpecialFolders.UserProfile не удается найти [1531](https://github.com/NuGet/Home/issues/1531)
* Улучшенная обработка в локальном кэше пакетов, которые были повреждены во время загрузки [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Полный список устраненные для расширения командной строки и Visual Studio можно найти в NuGet GitHub [3.2.1 вехи](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Известные проблемы

Мы продолжаем отслеживания проблем на наш список проблем GitHub, которую можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)