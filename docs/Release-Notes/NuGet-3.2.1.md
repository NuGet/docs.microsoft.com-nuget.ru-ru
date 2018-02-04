---
title: "Заметки о выпуске NuGet 3.2.1 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 3.2.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 3.2.1 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c9c2457c33eb3630f632c98bf0cf96703c3a548
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="8f484-104">Заметки о выпуске NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="8f484-104">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="8f484-105">[Заметки о выпуске NuGet 3.2](../release-notes/nuget-3.2.md) | [NuGet 3.3 заметки о выпуске](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="8f484-105">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="8f484-106">NuGet 3.2.1 для командной строки был выпущен 12 октября 2015 г. с небольшое количество оптимизаций и исправления для версии 3.2 и доступен из [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="8f484-106">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="8f484-107">Усовершенствования</span><span class="sxs-lookup"><span data-stu-id="8f484-107">Improvements</span></span>

* <span data-ttu-id="8f484-108">NuGet теперь использует файл конфигурации с исходного регистр `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="8f484-108">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="8f484-109">Это важно, с учетом регистра в операционных системах [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="8f484-109">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="8f484-110">Восстановление NuGet теперь будет игнорировать проектов dnx (`*.xproj`), которые должны быть обработаны с `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="8f484-110">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="8f484-111">Оптимизации использования сети при работе с `index.json` и данные регистрации пакета [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="8f484-111">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="8f484-112">Улучшенная ресурсов загрузки обработки для повышения надежности со службами v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="8f484-112">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="8f484-113">Исправления</span><span class="sxs-lookup"><span data-stu-id="8f484-113">Fixes</span></span>

* <span data-ttu-id="8f484-114">Обновление NuGet правильно обновляет `.csproj` / `.vcxproj` ссылки [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="8f484-114">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="8f484-115">Теперь предотвращая папка локального .nuget при SpecialFolders.UserProfile не удается найти [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="8f484-115">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="8f484-116">Улучшенная обработка в локальном кэше пакетов, которые были повреждены во время загрузки [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="8f484-116">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="8f484-117">Полный список устраненные для расширения командной строки и Visual Studio можно найти в NuGet GitHub [3.2.1 вехи](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="8f484-117">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="8f484-118">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="8f484-118">Known Issues</span></span>

<span data-ttu-id="8f484-119">Мы продолжаем отслеживания проблем на наш список проблем GitHub, которую можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="8f484-119">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>