---
title: Заметки о выпуске NuGet 3.4.4
description: Заметки о выпуске для NuGet 3.4.4, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547477"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="0cd76-103">Заметки о выпуске NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="0cd76-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="0cd76-104">[Заметки о выпуске NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [заметки о выпуске бета-версии 3.5 NuGet](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="0cd76-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="0cd76-105">Основная цель этой версии — это улучшение с качеством 3.4.3 версию nuget.exe с несколько исправлений в расширение Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0cd76-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="0cd76-106">Можно загрузить VSIX и nuget.exe [здесь](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="0cd76-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="0cd76-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="0cd76-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="0cd76-108">Полный журнал изменений</span><span class="sxs-lookup"><span data-stu-id="0cd76-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="0cd76-109">Список проблем</span><span class="sxs-lookup"><span data-stu-id="0cd76-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="0cd76-110">Изменения</span><span class="sxs-lookup"><span data-stu-id="0cd76-110">Changes</span></span>

- <span data-ttu-id="0cd76-111">Улучшения в пакете: Усовершенствования упаковка символов, упаковки с `project.json` и дополнительные [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="0cd76-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="0cd76-112">Отображение исключений при сбое, поиск проектов в команде обновления [\#605](https://github.com/NuGet/NuGet.Client/pull/605)</span><span class="sxs-lookup"><span data-stu-id="0cd76-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="0cd76-113">Чтение входных данных в тип пакета `.nuspec` и `project.json` при упаковке [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="0cd76-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="0cd76-114">Сделайте NuGet.Shared не отдельного проекта.</span><span class="sxs-lookup"><span data-stu-id="0cd76-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="0cd76-115">\#602</span><span class="sxs-lookup"><span data-stu-id="0cd76-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="0cd76-116">Используйте время ожидания Push-уведомлений как время ожидания ответа HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="0cd76-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="0cd76-117">Файлы пакета с будущих периодов не будет использовать для них времени [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="0cd76-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="0cd76-118">Обновление `NuGet.Core.dll` версии 2.12.0, чтобы устранить проблему XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="0cd76-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="0cd76-119">Поддерживает./NuGet.CommandLine.XPlat - v \<детализации\> \<режим\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="0cd76-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="0cd76-120">Ошибка отображения при восстановлении без `project.json` или `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="0cd76-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="0cd76-121">Исправление версии зависимостей, если необходимые версии отличаются [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="0cd76-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>