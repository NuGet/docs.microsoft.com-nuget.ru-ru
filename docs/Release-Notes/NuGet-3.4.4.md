---
title: "Заметки о выпуске NuGet 3.4.4 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6f0aa9bb-75e5-429d-9954-3cb41a909c14
description: "Заметки о выпуске для NuGet 3.4.4, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 3.4.4 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 51ddb918d2269990588e9cba4d15ffeb878de5f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="a1701-104">Заметки о выпуске NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="a1701-104">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="a1701-105">[Заметки о выпуске NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [заметки о выпуске 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="a1701-105">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="a1701-106">Основная цель данного выпуска — это улучшение с качеством 3.4.3 версии nuget.exe несколько исправлений в расширение Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a1701-106">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="a1701-107">Можно загрузить VSIX и nuget.exe [здесь](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="a1701-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="a1701-108">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="a1701-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="a1701-109">Полный журнал изменений</span><span class="sxs-lookup"><span data-stu-id="a1701-109">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="a1701-110">Список проблем</span><span class="sxs-lookup"><span data-stu-id="a1701-110">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="a1701-111">Изменения</span><span class="sxs-lookup"><span data-stu-id="a1701-111">Changes</span></span>

- <span data-ttu-id="a1701-112">Улучшения в пакет усовершенствования упаковкой символов, упаковки с `project.json` и дополнительные [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="a1701-112">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="a1701-113">Отображение исключений при сбое, поиск проектов в команде обновления [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="a1701-113">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="a1701-114">Чтение входных данных типа пакета `.nuspec` и `project.json` при упаковки [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="a1701-114">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="a1701-115">Сделайте NuGet.Shared не отдельного проекта.</span><span class="sxs-lookup"><span data-stu-id="a1701-115">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="a1701-116">\#602</span><span class="sxs-lookup"><span data-stu-id="a1701-116">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="a1701-117">Использование времени ожидания принудительной как время ожидания ответа HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="a1701-117">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="a1701-118">Файлы пакета со временем в будущем не будет их использовать времени [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="a1701-118">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="a1701-119">Обновление `NuGet.Core.dll` версии 2.12.0 устранению XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="a1701-119">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="a1701-120">Поддерживает./NuGet.CommandLine.XPlat - v \<детализации\> \<режим\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="a1701-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="a1701-121">Ошибка отображения при восстановлении без `project.json` или `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="a1701-121">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="a1701-122">Исправления версии зависимостей, когда требуемые версии отличаются [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="a1701-122">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>