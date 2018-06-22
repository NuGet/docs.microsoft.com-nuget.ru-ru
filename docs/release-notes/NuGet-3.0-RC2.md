---
title: Заметки о выпуске версии-кандидата 2 NuGet 3.0
description: Заметки о выпуске NuGet 3.0 RC2 включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eb8b514fa967cc6ef850483b6b2a5df3ab27a550
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819888"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="83440-103">Заметки о выпуске версии-кандидата 2 NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="83440-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="83440-104">[Заметки о выпуске версии-Кандидата NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [заметки о выпуске NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="83440-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="83440-105">Промежуточный выпуск доступен из галереи расширений Visual Studio 2015 NuGet 3.0 RC2 был выпущен 3 июня 2015 г. и [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="83440-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="83440-106">Этот выпуск содержит ряд важных исправлений и повышение производительности, мы полагаем, было необходимо освободить до завершения выпуска Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="83440-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="83440-107">Эта версия расширения NuGet доступна только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="83440-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="83440-108">В итоге мы закрытых 158 проблем в этом выпуске, и можно будет просмотреть [полный список проблем на GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="83440-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="83440-109">Сводка по верхней устранения проблем</span><span class="sxs-lookup"><span data-stu-id="83440-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="83440-110">Обновления сети часто вызывается, когда обновляет окно диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="83440-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="83440-111">Отложенная прокрутки установленные изменение на представление в диспетчере пакетов</span><span class="sxs-lookup"><span data-stu-id="83440-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="83440-112">Сетевые вызовы должны выполняться в фоновом потоке</span><span class="sxs-lookup"><span data-stu-id="83440-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="83440-113">Добавить флажок «Больше не показывать окно предварительного просмотра»</span><span class="sxs-lookup"><span data-stu-id="83440-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="83440-114">Добавленный процесс регулирования для уменьшения использования процессора</span><span class="sxs-lookup"><span data-stu-id="83440-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="83440-115">Улучшенная обработка библиотек классов portable ссылки</span><span class="sxs-lookup"><span data-stu-id="83440-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="83440-116">Автозаполнение служба была с учетом регистра</span><span class="sxs-lookup"><span data-stu-id="83440-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="83440-117">Обновления, чтобы повторно ввести учетные данные Обычная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="83440-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="83440-118">Улучшенная Ошибка ведения журнала</span><span class="sxs-lookup"><span data-stu-id="83440-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="83440-119">Powershell улучшенные сообщения об ошибках при вызове пакета обновления</span><span class="sxs-lookup"><span data-stu-id="83440-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="83440-120">Загрузить это [обновления с расширением NuGet](https://nuget.codeplex.com/releases/view/615507) на сайте Codeplex и проверьте следить за [наш блог](http://blog.nuget.org) дополнительные хода выполнения и объявления для NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="83440-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>