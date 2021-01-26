---
title: Заметки о выпуске NuGet 3.2.1
description: Заметки о выпуске NuGet 3.2.1, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776515"
---
# <a name="nuget-321-release-notes"></a>Заметки о выпуске NuGet 3.2.1

[Заметки о](../release-notes/nuget-3.2.md)  |  выпуске NuGet 3,2 [Заметки о выпуске NuGet 3,3](../release-notes/nuget-3.3.md)

NuGet 3.2.1 для командной строки была выпущена 12 октября 2015 с несколькими оптимизациями и исправлениями для выпуска 3,2 и доступен в [dist.NuGet.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Улучшения

* NuGet теперь использует файл конфигурации с исходным регистром `NuGet.Config` .  Это важно в операционных системах с учетом регистра [1427](https://github.com/NuGet/Home/issues/1427)
* Теперь при восстановлении NuGet будут игнорироваться DNX проекты ( `*.xproj` ), которые должны обрабатываться с `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Оптимизированная загрузка сети при работе с `index.json` данными регистрации пакета [1426](https://github.com/NuGet/Home/issues/1426)
* Улучшенная обработка загрузки ресурсов в целях повышения надежности служб версии 2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Исправления

* Правильное обновление NuGet `.csproj` / `.vcxproj` ссылается на [1483](https://github.com/NuGet/Home/issues/1483)
* Теперь предотвращается создание локальной папки NuGet, если не удается найти СпеЦиалфолдерс. UserProfile [1531](https://github.com/NuGet/Home/issues/1531)
* Улучшена обработка пакетов в локальном кэше, которые повреждены во время загрузки [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Полный список проблем, устраняемых с помощью командной строки и расширения Visual Studio, можно найти в этой [вехе](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) .

## <a name="known-issues"></a>Известные проблемы

Мы продолжаем отслеживанием проблем в нашем списке проблем GitHub, который можно найти по адресу: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)