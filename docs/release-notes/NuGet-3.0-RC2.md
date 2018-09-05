---
title: Заметки о выпуске NuGet 3.0 RC2
description: Заметки о выпуске NuGet 3.0 RC2 включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545825"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="7021b-103">Заметки о выпуске NuGet 3.0 RC2</span><span class="sxs-lookup"><span data-stu-id="7021b-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="7021b-104">[Заметки о выпуске версии-Кандидата NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [заметки о выпуске NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="7021b-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="7021b-105">NuGet 3.0 RC2 было выпущено 3 июня 2015 г., промежуточный выпуск доступен из коллекции расширений Visual Studio 2015 и [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="7021b-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="7021b-106">Этот выпуск содержит ряд важных исправлений и улучшений производительности, которые мы полагаем, использовались для того освободить до завершения выпуска Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7021b-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="7021b-107">Эта версия расширения NuGet доступна только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7021b-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="7021b-108">В целом, мы закрытых 158 проблем в этом выпуске, и вы можете просмотреть [полный список проблем на GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="7021b-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="7021b-109">Сводка по устранить основные проблемы</span><span class="sxs-lookup"><span data-stu-id="7021b-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="7021b-110">Обновление сети часто вызывается, когда обновляет окно диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="7021b-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="7021b-111">Отложенной прокрутки, при изменении на установке представление в диспетчере пакетов</span><span class="sxs-lookup"><span data-stu-id="7021b-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="7021b-112">Сетевые вызовы, которые должны выполняться в фоновом потоке</span><span class="sxs-lookup"><span data-stu-id="7021b-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="7021b-113">Добавлен флажок «Больше не показывать окно предварительного просмотра»</span><span class="sxs-lookup"><span data-stu-id="7021b-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="7021b-114">Добавленный процесс, регулирование, чтобы снизить использование процессора</span><span class="sxs-lookup"><span data-stu-id="7021b-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="7021b-115">Улучшенную обработку справочном руководстве библиотеки portable классов</span><span class="sxs-lookup"><span data-stu-id="7021b-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="7021b-116">Автозаполнение служба была с учетом регистра</span><span class="sxs-lookup"><span data-stu-id="7021b-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="7021b-117">Обновления, чтобы повторно ввести учетные данные обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="7021b-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="7021b-118">Улучшено ведение журналов ошибок</span><span class="sxs-lookup"><span data-stu-id="7021b-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="7021b-119">Powershell улучшенные сообщения об ошибках при вызове Update-Package</span><span class="sxs-lookup"><span data-stu-id="7021b-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="7021b-120">Скачайте это [обновления для расширения NuGet](https://nuget.codeplex.com/releases/view/615507) веб-сайте Codeplex и Пожалуйста Обратите внимание на [наш блог](http://blog.nuget.org) дополнительные ход выполнения и объявления для NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="7021b-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>