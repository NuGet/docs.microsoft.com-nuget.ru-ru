---
title: Заметки о выпуске 3.4.4 NuGet
description: Заметки о выпуске NuGet 3.4.4, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780232"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="f6601-103">Заметки о выпуске 3.4.4 NuGet</span><span class="sxs-lookup"><span data-stu-id="f6601-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="f6601-104">[Заметки о](../release-notes/nuget-3.4.3.md)  |  выпуске 3.4.3 NuGet [NuGet 3,5 — заметки о выпуске бета-версии](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="f6601-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="f6601-105">Основное внимание в этом выпуске было улучшение качества 3.4.3 версии nuget.exe с помощью нескольких исправлений для расширения Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6601-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="f6601-106">Вы можете скачать VSIX и nuget.exe [здесь](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="f6601-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="f6601-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="f6601-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="f6601-108">Полный журнал изменений</span><span class="sxs-lookup"><span data-stu-id="f6601-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="f6601-109">Список проблем</span><span class="sxs-lookup"><span data-stu-id="f6601-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="f6601-110">Изменения</span><span class="sxs-lookup"><span data-stu-id="f6601-110">Changes</span></span>

- <span data-ttu-id="f6601-111">Улучшения в пакетах: улучшения упаковки символов, упаковка с `project.json` и более [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="f6601-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="f6601-112">Отображать исключение при сбое поиска проектов в команде Update [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="f6601-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="f6601-113">Считывание типа пакета из входных данных `.nuspec` и `project.json` при упаковке [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="f6601-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="f6601-114">Сделайте NuGet. Shared не проектом.</span><span class="sxs-lookup"><span data-stu-id="f6601-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="f6601-115">\#602</span><span class="sxs-lookup"><span data-stu-id="f6601-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="f6601-116">Использовать время ожидания отправки для HTTP-ответа [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="f6601-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="f6601-117">Файлы пакета со временем не будут использоваться в будущем [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="f6601-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="f6601-118">Обновление `NuGet.Core.dll` версии до 2.12.0 для исправления ошибки XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="f6601-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="f6601-119">Поддержка./нужет.коммандлине.ксплат-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="f6601-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="f6601-120">Отображать ошибку при восстановлении без `project.json` или `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="f6601-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="f6601-121">Исправление версий зависимостей, если требуемые версии отличаются [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="f6601-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>