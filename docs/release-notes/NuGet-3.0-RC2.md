---
title: Заметки о выпуске NuGet 3,0 RC2
description: Заметки о выпуске NuGet 3,0 RC2, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780283"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="97b5d-103">Заметки о выпуске NuGet 3,0 RC2</span><span class="sxs-lookup"><span data-stu-id="97b5d-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="97b5d-104">[Заметки о](../release-notes/nuget-3.0-RC.md)  |  выпуске для версии-кандидата NuGet 3,0 [Заметки о выпуске NuGet 3,0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="97b5d-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="97b5d-105">Версия NuGet 3,0 RC2 была выпущена 3 июня 2015 в качестве промежуточного выпуска из коллекции расширений Visual Studio 2015 и [CodePlex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="97b5d-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="97b5d-106">В этом выпуске имеется ряд важных исправлений ошибок и улучшений производительности, которые были важны для выпуска до завершения выпуска Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="97b5d-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="97b5d-107">Эта версия расширения NuGet доступна только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="97b5d-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="97b5d-108">В итоге мы закрыли 158 проблемы в этом выпуске, и вы можете просмотреть [полный список проблем на сайте GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="97b5d-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="97b5d-109">Сводка по устранению основных проблем</span><span class="sxs-lookup"><span data-stu-id="97b5d-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="97b5d-110">Частые вызовы сетевых обновлений при обновлении окна диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="97b5d-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="97b5d-111">Отложенная прокрутка при переходе в режим установленного представления в диспетчере пакетов</span><span class="sxs-lookup"><span data-stu-id="97b5d-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="97b5d-112">Сетевые вызовы должны выполняться в фоновом потоке.</span><span class="sxs-lookup"><span data-stu-id="97b5d-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="97b5d-113">Добавлен флажок "не показывать окно предварительного просмотра"</span><span class="sxs-lookup"><span data-stu-id="97b5d-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="97b5d-114">Добавлено регулирование процессов для сокращения загрузки процессора.</span><span class="sxs-lookup"><span data-stu-id="97b5d-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="97b5d-115">Улучшенная обработка ссылок на библиотеки переносимых классов</span><span class="sxs-lookup"><span data-stu-id="97b5d-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="97b5d-116">Служба автозаполнения с учетом регистра</span><span class="sxs-lookup"><span data-stu-id="97b5d-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="97b5d-117">Обновление для повторного ввода учетных данных базовой проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="97b5d-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="97b5d-118">Улучшено ведение журналов ошибок.</span><span class="sxs-lookup"><span data-stu-id="97b5d-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="97b5d-119">Улучшены сообщения об ошибках PowerShell при вызове Update-Package</span><span class="sxs-lookup"><span data-stu-id="97b5d-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="97b5d-120">Скачайте это [Обновление для расширения NuGet](https://nuget.codeplex.com/releases/view/615507) из CodePlex и следите за [нашим блогом](http://blog.nuget.org) , чтобы получить дополнительные сведения о ходе и объявлениях для NuGet 3,0!</span><span class="sxs-lookup"><span data-stu-id="97b5d-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>