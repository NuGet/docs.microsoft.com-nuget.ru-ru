---
title: Заметки о выпуске NuGet 3.2.1
description: Заметки о выпуске для NuGet 3.2.1, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548194"
---
# <a name="nuget-321-release-notes"></a>Заметки о выпуске NuGet 3.2.1

[Заметки о выпуске NuGet 3.2](../release-notes/nuget-3.2.md) | [заметки о выпуске NuGet 3.3](../release-notes/nuget-3.3.md)

NuGet 3.2.1 для командной строки, была выпущена 12 октября 2015 г. с небольшим количеством оптимизаций и исправлений для версии 3.2 и доступен из [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Усовершенствования

* NuGet теперь использует файл конфигурации с исходного регистр `NuGet.Config`.  Это важно, с учетом регистра в операционных системах [1427](https://github.com/NuGet/Home/issues/1427)
* Восстановление NuGet теперь будет игнорировать проекты dnx (`*.xproj`), которые должны быть обработаны с `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Оптимизировать использование сети при работе с `index.json` и данные регистрации пакета [1426](https://github.com/NuGet/Home/issues/1426)
* Улучшенные ресурсов загрузки обработки более устойчивыми службами v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Исправления

* Обновления NuGet правильно обновляет `.csproj` / `.vcxproj` ссылки [1483](https://github.com/NuGet/Home/issues/1483)
* Теперь препятствуя созданию при SpecialFolders.UserProfile не удалось найти папку локального .nuget [1531](https://github.com/NuGet/Home/issues/1531)
* Улучшенную обработку пакетов в локальном кэше, повреждены во время загрузки [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Полный список проблемы для расширения командной строки и Visual Studio можно найти в NuGet GitHub [3.2.1 вехи](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Известные проблемы

Мы продолжаем для отслеживания проблем в нашем списке проблемы GitHub, который можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)