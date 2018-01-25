---
title: "Заметки о выпуске версии-кандидата 2 NuGet 3.0 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске NuGet 3.0 RC2 включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 3.0 RC2 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67299408170ae3c3676c2866bec2945b41ad4184
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="d2c4d-104">Заметки о выпуске версии-кандидата 2 NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="d2c4d-104">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="d2c4d-105">[Заметки о выпуске версии-Кандидата NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [заметки о выпуске NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="d2c4d-105">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="d2c4d-106">Промежуточный выпуск доступен из галереи расширений Visual Studio 2015 NuGet 3.0 RC2 был выпущен 3 июня 2015 г. и [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="d2c4d-106">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="d2c4d-107">Этот выпуск содержит ряд важных исправлений и повышение производительности, мы полагаем, было необходимо освободить до завершения выпуска Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-107">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="d2c4d-108">Эта версия расширения NuGet доступна только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d2c4d-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="d2c4d-109">В итоге мы закрытых 158 проблем в этом выпуске, и можно будет просмотреть [полный список проблем на GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="d2c4d-109">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="d2c4d-110">Сводка по верхней устранения проблем</span><span class="sxs-lookup"><span data-stu-id="d2c4d-110">Summary of top issues resolved</span></span>

* [<span data-ttu-id="d2c4d-111">Обновления сети часто вызывается, когда обновляет окно диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="d2c4d-111">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="d2c4d-112">Отложенная прокрутки установленные изменение на представление в диспетчере пакетов</span><span class="sxs-lookup"><span data-stu-id="d2c4d-112">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="d2c4d-113">Сетевые вызовы должны выполняться в фоновом потоке</span><span class="sxs-lookup"><span data-stu-id="d2c4d-113">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="d2c4d-114">Добавить флажок «Больше не показывать окно предварительного просмотра»</span><span class="sxs-lookup"><span data-stu-id="d2c4d-114">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="d2c4d-115">Добавленный процесс регулирования для уменьшения использования процессора</span><span class="sxs-lookup"><span data-stu-id="d2c4d-115">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="d2c4d-116">Улучшенная обработка библиотек классов portable ссылки</span><span class="sxs-lookup"><span data-stu-id="d2c4d-116">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="d2c4d-117">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="d2c4d-117">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="d2c4d-118">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="d2c4d-118">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="d2c4d-119">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="d2c4d-119">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="d2c4d-120">Автозаполнение служба была с учетом регистра</span><span class="sxs-lookup"><span data-stu-id="d2c4d-120">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="d2c4d-121">Обновления, чтобы повторно ввести учетные данные Обычная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="d2c4d-121">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="d2c4d-122">Улучшенная Ошибка ведения журнала</span><span class="sxs-lookup"><span data-stu-id="d2c4d-122">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="d2c4d-123">Powershell улучшенные сообщения об ошибках при вызове пакета обновления</span><span class="sxs-lookup"><span data-stu-id="d2c4d-123">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="d2c4d-124">Загрузить это [обновления с расширением NuGet](https://nuget.codeplex.com/releases/view/615507) на сайте Codeplex и проверьте следить за [наш блог](http://blog.nuget.org) дополнительные хода выполнения и объявления для NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="d2c4d-124">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>