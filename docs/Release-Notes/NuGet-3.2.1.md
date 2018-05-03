---
title: Заметки о выпуске NuGet 3.2.1
description: Заметки о выпуске для NuGet 3.2.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="bb6da-103">Заметки о выпуске NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="bb6da-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="bb6da-104">[Заметки о выпуске NuGet 3.2](../release-notes/nuget-3.2.md) | [NuGet 3.3 заметки о выпуске](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="bb6da-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="bb6da-105">NuGet 3.2.1 для командной строки был выпущен 12 октября 2015 г. с небольшое количество оптимизаций и исправления для версии 3.2 и доступен из [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="bb6da-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="bb6da-106">Усовершенствования</span><span class="sxs-lookup"><span data-stu-id="bb6da-106">Improvements</span></span>

* <span data-ttu-id="bb6da-107">NuGet теперь использует файл конфигурации с исходного регистр `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="bb6da-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="bb6da-108">Это важно, с учетом регистра в операционных системах [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="bb6da-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="bb6da-109">Восстановление NuGet теперь будет игнорировать проектов dnx (`*.xproj`), которые должны быть обработаны с `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="bb6da-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="bb6da-110">Оптимизации использования сети при работе с `index.json` и данные регистрации пакета [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="bb6da-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="bb6da-111">Улучшенная ресурсов загрузки обработки для повышения надежности со службами v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="bb6da-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="bb6da-112">Исправления</span><span class="sxs-lookup"><span data-stu-id="bb6da-112">Fixes</span></span>

* <span data-ttu-id="bb6da-113">Обновление NuGet правильно обновляет `.csproj` / `.vcxproj` ссылки [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="bb6da-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="bb6da-114">Теперь предотвращая папка локального .nuget при SpecialFolders.UserProfile не удается найти [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="bb6da-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="bb6da-115">Улучшенная обработка в локальном кэше пакетов, которые были повреждены во время загрузки [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="bb6da-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="bb6da-116">Полный список устраненные для расширения командной строки и Visual Studio можно найти в NuGet GitHub [3.2.1 вехи](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="bb6da-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="bb6da-117">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="bb6da-117">Known Issues</span></span>

<span data-ttu-id="bb6da-118">Мы продолжаем отслеживания проблем на наш список проблем GitHub, которую можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="bb6da-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>