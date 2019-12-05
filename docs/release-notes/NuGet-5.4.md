---
title: Заметки о выпуске NuGet 5,4
description: Заметки о выпуске NuGet 5,4, включая новые функции, исправления ошибок и DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 69f78ba5483fcc92887624584663e8c496cfc497
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2019
ms.locfileid: "74828396"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="3534f-103">Заметки о выпуске NuGet 5,4</span><span class="sxs-lookup"><span data-stu-id="3534f-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="3534f-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="3534f-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="3534f-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="3534f-105">NuGet version</span></span> | <span data-ttu-id="3534f-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3534f-106">Available in Visual Studio version</span></span>| <span data-ttu-id="3534f-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="3534f-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="3534f-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="3534f-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="3534f-109">Visual Studio 2019 версии 16,4</span><span class="sxs-lookup"><span data-stu-id="3534f-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="3534f-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="3534f-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="3534f-111"><sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core</span><span class="sxs-lookup"><span data-stu-id="3534f-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="3534f-112">Сводка: новые возможности в 5,4</span><span class="sxs-lookup"><span data-stu-id="3534f-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="3534f-113">Более быстрое время загрузки решения — накладные расходы на выполнение кода NuGet во время первой загрузки решения были сокращены с помощью частичного генератора NGen для сокращения затрат на JIT- [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="3534f-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="3534f-114">Новая вспомогательная функция — для получения списка идентификаторов пакетов и версий следует получить вероятные пакеты верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="3534f-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="3534f-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="3534f-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3534f-116">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="3534f-116">Issues fixed in this release</span></span>

<span data-ttu-id="3534f-117">**Ошибки**</span><span class="sxs-lookup"><span data-stu-id="3534f-117">**Bugs**</span></span>

* <span data-ttu-id="3534f-118">Подключаемый модуль: неправильное время ведения журнала в Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="3534f-118">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="3534f-119">Удаление подключаемого модуля иногда может вызвать и завершить всю операцию.</span><span class="sxs-lookup"><span data-stu-id="3534f-119">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="3534f-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="3534f-120"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="3534f-121">Больше не отображать дубликаты версий в списке разрешенных и заблокированных версий в ПМУИ- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="3534f-121">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="3534f-122">Файл блокировки создан неправильно. Упорядочивание платформы не должно влиять на восстановление с помощью локкедмоде- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="3534f-122">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="3534f-123">Сбой проверки Локкфиле для проектов с набором <RuntimeIdentifiers> в пакете SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="3534f-123">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="3534f-124">Теперь при проверке подписи будут правильно отклоняться подписи с метками времени, которые имеют 2 значения в одном OID- [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="3534f-124">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="3534f-125">Обновление списка лицензий — [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="3534f-125">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="3534f-126">**DCR**</span><span class="sxs-lookup"><span data-stu-id="3534f-126">**DCRs**</span></span>

* <span data-ttu-id="3534f-127">Адаптация файлов диагностики в Ифидбаккдиагностикфилепровидер — [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="3534f-127">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="3534f-128">**[Список всех проблем, исправленных в этом выпуске — 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="3534f-128">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
