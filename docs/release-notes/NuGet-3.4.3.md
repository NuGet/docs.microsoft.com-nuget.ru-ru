---
title: Заметки о выпуске NuGet 3.4.3
description: Заметки о выпуске для NuGet 3.4.3, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549169"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="fa566-103">Заметки о выпуске NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="fa566-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="fa566-104">[Заметки о выпуске NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [заметки о выпуске NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="fa566-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="fa566-105">NuGet 3.4.3 был выпущен 22 апреля 2016 г. решить некоторые проблемы, которые были определены в версии 3.4 и последующих выпусках.</span><span class="sxs-lookup"><span data-stu-id="fa566-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="fa566-106">Можно загрузить VSIX и nuget.exe [здесь](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="fa566-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="fa566-107">Обновления и улучшения</span><span class="sxs-lookup"><span data-stu-id="fa566-107">Updates and Improvements</span></span>

* <span data-ttu-id="fa566-108">Повышенная надежность Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa566-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="fa566-109">Мы исправили некоторые проблемы в NuGet, причиной сбоев в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa566-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="fa566-110">Исправления</span><span class="sxs-lookup"><span data-stu-id="fa566-110">Fixes</span></span>

* <span data-ttu-id="fa566-111">Исправлены некоторые проблемы авторизации с помощью частного nuget защищен паролем, веб-каналы.</span><span class="sxs-lookup"><span data-stu-id="fa566-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="fa566-112">Исправлена проблема вокруг не сможет восстановить переносимой библиотеки Классов от `project.json` с указан средами выполнения.</span><span class="sxs-lookup"><span data-stu-id="fa566-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="fa566-113">Некоторые клиенты были запущены в временные сбои при установке пакетов.</span><span class="sxs-lookup"><span data-stu-id="fa566-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="fa566-114">Теперь эта проблема была исправлена в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="fa566-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="fa566-115">Исправлена проблема, которая вызвала ошибки восстановления в C + +/ CLI проектов с помощью `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fa566-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="fa566-116">Некоторые пакеты (например ModernHttpClient) где не распакован правильно при использовании nuget в mono.</span><span class="sxs-lookup"><span data-stu-id="fa566-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="fa566-117">Теперь эта проблема была исправлена в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="fa566-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="fa566-118">Полный список исправлений и усовершенствований этого выпуска, ознакомьтесь со списком проблем [здесь](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="fa566-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>