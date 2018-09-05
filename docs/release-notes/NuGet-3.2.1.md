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
# <a name="nuget-321-release-notes"></a><span data-ttu-id="21b17-103">Заметки о выпуске NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="21b17-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="21b17-104">[Заметки о выпуске NuGet 3.2](../release-notes/nuget-3.2.md) | [заметки о выпуске NuGet 3.3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="21b17-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="21b17-105">NuGet 3.2.1 для командной строки, была выпущена 12 октября 2015 г. с небольшим количеством оптимизаций и исправлений для версии 3.2 и доступен из [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="21b17-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="21b17-106">Усовершенствования</span><span class="sxs-lookup"><span data-stu-id="21b17-106">Improvements</span></span>

* <span data-ttu-id="21b17-107">NuGet теперь использует файл конфигурации с исходного регистр `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="21b17-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="21b17-108">Это важно, с учетом регистра в операционных системах [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="21b17-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="21b17-109">Восстановление NuGet теперь будет игнорировать проекты dnx (`*.xproj`), которые должны быть обработаны с `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="21b17-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="21b17-110">Оптимизировать использование сети при работе с `index.json` и данные регистрации пакета [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="21b17-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="21b17-111">Улучшенные ресурсов загрузки обработки более устойчивыми службами v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="21b17-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="21b17-112">Исправления</span><span class="sxs-lookup"><span data-stu-id="21b17-112">Fixes</span></span>

* <span data-ttu-id="21b17-113">Обновления NuGet правильно обновляет `.csproj` / `.vcxproj` ссылки [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="21b17-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="21b17-114">Теперь препятствуя созданию при SpecialFolders.UserProfile не удалось найти папку локального .nuget [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="21b17-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="21b17-115">Улучшенную обработку пакетов в локальном кэше, повреждены во время загрузки [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="21b17-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="21b17-116">Полный список проблемы для расширения командной строки и Visual Studio можно найти в NuGet GitHub [3.2.1 вехи](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="21b17-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="21b17-117">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="21b17-117">Known Issues</span></span>

<span data-ttu-id="21b17-118">Мы продолжаем для отслеживания проблем в нашем списке проблемы GitHub, который можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="21b17-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>