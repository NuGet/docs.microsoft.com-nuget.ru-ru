---
title: "Заметки о выпуске NuGet 3.4.3 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 3.4.3, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 3.4.3 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="65851-104">Заметки о выпуске NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="65851-104">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="65851-105">[Заметки о выпуске NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 заметки о выпуске](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="65851-105">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="65851-106">NuGet 3.4.3 был выпущен 22 апреля 2016 г. Чтобы решить некоторые проблемы, которые были определены в 3,4 и последующих выпусках.</span><span class="sxs-lookup"><span data-stu-id="65851-106">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="65851-107">Можно загрузить VSIX и nuget.exe [здесь](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="65851-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="65851-108">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="65851-108">Updates and Improvements</span></span>

* <span data-ttu-id="65851-109">Повышенная надежность Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65851-109">Improved Visual Studio reliability.</span></span> <span data-ttu-id="65851-110">Мы исправили некоторые проблемы в NuGet, причиной сбоев в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65851-110">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="65851-111">Исправления</span><span class="sxs-lookup"><span data-stu-id="65851-111">Fixes</span></span>

* <span data-ttu-id="65851-112">Исправлены некоторые проблемы авторизации с частной nuget защищенные паролем веб-каналов.</span><span class="sxs-lookup"><span data-stu-id="65851-112">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="65851-113">Устранена проблема вокруг не удается восстановить PCL элемента из `project.json` в указанный средах выполнения.</span><span class="sxs-lookup"><span data-stu-id="65851-113">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="65851-114">Некоторые клиенты были запущены в временные сбои при установке пакетов.</span><span class="sxs-lookup"><span data-stu-id="65851-114">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="65851-115">Теперь эта проблема была исправлена в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="65851-115">This has now been fixed in this release.</span></span>
* <span data-ttu-id="65851-116">Устранена проблема, вызвавшая восстановления сбоев в C + +/ CLI проекты с `project.json`.</span><span class="sxs-lookup"><span data-stu-id="65851-116">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="65851-117">Некоторые пакеты (например ModernHttpClient) где не распаковал правильно при использовании nuget в моно.</span><span class="sxs-lookup"><span data-stu-id="65851-117">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="65851-118">Теперь эта проблема была исправлена в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="65851-118">This has now been fixed in this release.</span></span>

<span data-ttu-id="65851-119">Полный список исправлений и улучшений данного выпуска, см. список проблем [здесь](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="65851-119">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>