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
# <a name="nuget-321-release-notes"></a><span data-ttu-id="9e985-103">Заметки о выпуске NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="9e985-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="9e985-104">[Заметки о](../release-notes/nuget-3.2.md)  |  выпуске NuGet 3,2 [Заметки о выпуске NuGet 3,3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="9e985-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="9e985-105">NuGet 3.2.1 для командной строки была выпущена 12 октября 2015 с несколькими оптимизациями и исправлениями для выпуска 3,2 и доступен в [dist.NuGet.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="9e985-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="9e985-106">Улучшения</span><span class="sxs-lookup"><span data-stu-id="9e985-106">Improvements</span></span>

* <span data-ttu-id="9e985-107">NuGet теперь использует файл конфигурации с исходным регистром `NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="9e985-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="9e985-108">Это важно в операционных системах с учетом регистра [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="9e985-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="9e985-109">Теперь при восстановлении NuGet будут игнорироваться DNX проекты ( `*.xproj` ), которые должны обрабатываться с `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="9e985-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="9e985-110">Оптимизированная загрузка сети при работе с `index.json` данными регистрации пакета [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="9e985-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="9e985-111">Улучшенная обработка загрузки ресурсов в целях повышения надежности служб версии 2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="9e985-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="9e985-112">Исправления</span><span class="sxs-lookup"><span data-stu-id="9e985-112">Fixes</span></span>

* <span data-ttu-id="9e985-113">Правильное обновление NuGet `.csproj` / `.vcxproj` ссылается на [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="9e985-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="9e985-114">Теперь предотвращается создание локальной папки NuGet, если не удается найти СпеЦиалфолдерс. UserProfile [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="9e985-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="9e985-115">Улучшена обработка пакетов в локальном кэше, которые повреждены во время загрузки [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="9e985-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="9e985-116">Полный список проблем, устраняемых с помощью командной строки и расширения Visual Studio, можно найти в этой [вехе](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) .</span><span class="sxs-lookup"><span data-stu-id="9e985-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="9e985-117">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="9e985-117">Known Issues</span></span>

<span data-ttu-id="9e985-118">Мы продолжаем отслеживанием проблем в нашем списке проблем GitHub, который можно найти по адресу: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="9e985-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>