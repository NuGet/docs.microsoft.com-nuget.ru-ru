---
title: Заметки о выпуске NuGet 3.4.3
description: Заметки о выпуске для NuGet 3.4.3, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820330"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="ccb3f-103">Заметки о выпуске NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="ccb3f-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="ccb3f-104">[Заметки о выпуске NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 заметки о выпуске](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="ccb3f-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="ccb3f-105">NuGet 3.4.3 был выпущен 22 апреля 2016 г. Чтобы решить некоторые проблемы, которые были определены в 3,4 и последующих выпусках.</span><span class="sxs-lookup"><span data-stu-id="ccb3f-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="ccb3f-106">Можно загрузить VSIX и nuget.exe [здесь](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="ccb3f-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="ccb3f-107">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="ccb3f-107">Updates and Improvements</span></span>

* <span data-ttu-id="ccb3f-108">Повышенная надежность Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ccb3f-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="ccb3f-109">Мы исправили некоторые проблемы в NuGet, причиной сбоев в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ccb3f-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="ccb3f-110">Исправления</span><span class="sxs-lookup"><span data-stu-id="ccb3f-110">Fixes</span></span>

* <span data-ttu-id="ccb3f-111">Исправлены некоторые проблемы авторизации с частной nuget защищенные паролем веб-каналов.</span><span class="sxs-lookup"><span data-stu-id="ccb3f-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="ccb3f-112">Устранена проблема вокруг не удается восстановить PCL элемента из `project.json` в указанный средах выполнения.</span><span class="sxs-lookup"><span data-stu-id="ccb3f-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="ccb3f-113">Некоторые клиенты были запущены в временные сбои при установке пакетов.</span><span class="sxs-lookup"><span data-stu-id="ccb3f-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="ccb3f-114">Теперь эта проблема была исправлена в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="ccb3f-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="ccb3f-115">Устранена проблема, вызвавшая восстановления сбоев в C + +/ CLI проекты с `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ccb3f-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="ccb3f-116">Некоторые пакеты (например ModernHttpClient) где не распаковал правильно при использовании nuget в моно.</span><span class="sxs-lookup"><span data-stu-id="ccb3f-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="ccb3f-117">Теперь эта проблема была исправлена в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="ccb3f-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="ccb3f-118">Полный список исправлений и улучшений данного выпуска, см. список проблем [здесь](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="ccb3f-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>