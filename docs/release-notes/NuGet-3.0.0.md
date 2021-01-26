---
title: Заметки о выпуске NuGet 3,0
description: Заметки о выпуске NuGet 3.0.0, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776557"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="320c9-103">Заметки о выпуске NuGet 3,0</span><span class="sxs-lookup"><span data-stu-id="320c9-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="320c9-104">[Заметки о](../release-notes/nuget-3.0-RC2.md)  |  выпуске NuGet 3,0 RC2 [Заметки о выпуске NuGet 3,1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="320c9-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="320c9-105">Пакет NuGet 3,0 был выпущен 20 июля 2015 в качестве расширения пакета для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="320c9-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="320c9-106">Мы отправили этот выпуск в Visual Studio, чтобы полностью обновленный интерфейс NuGet 3,0 был доступен для новых пользователей Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="320c9-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="320c9-107">Эта версия расширения NuGet доступна только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="320c9-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="320c9-108">Рекомендуется, чтобы разработчики, у которых есть доступ к коллекции Visual Studio, были обновлены до последней доступной версии, так как публикация обновления выполняется вскоре после выпуска Visual Studio 2015, который содержит поддержку для разработки Windows 10.</span><span class="sxs-lookup"><span data-stu-id="320c9-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="320c9-109">В итоге мы закрыли 240 проблемы в выпуске 3,0, и можете ознакомиться с [полным списком проблем на сайте GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="320c9-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="320c9-110">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="320c9-110">Known Issues</span></span>

<span data-ttu-id="320c9-111">В этом выпуске имеется ряд известных проблем, и все эти элементы исправлены в запланированном 3,1 выпуске, чтобы совпадать с выпуском Windows 10 на 29 июля.</span><span class="sxs-lookup"><span data-stu-id="320c9-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="320c9-112">Вы можете обновить расширение Visual Studio из коллекции на эту дату или позже, чтобы устранить эти известные проблемы.</span><span class="sxs-lookup"><span data-stu-id="320c9-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="320c9-113">Не указано преобразование метки "больше не показывать" в окне предварительного просмотра и метки "Authors" в окне описания пакета.</span><span class="sxs-lookup"><span data-stu-id="320c9-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="320c9-114">При работе над проектом с помощью системы управления версиями TFS NuGet не может предоставить пользовательский интерфейс диспетчера пакетов, если файл Nuget.Config помечен как "только для чтения".</span><span class="sxs-lookup"><span data-stu-id="320c9-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="320c9-115">**Обходной путь** Извлеките файл из TFS.</span><span class="sxs-lookup"><span data-stu-id="320c9-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="320c9-116">Текст в желтой строке "перезагрузка" в окне PowerShell NuGet не отображается при использовании темной темы Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="320c9-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="320c9-117">**Обходной путь** Используйте тему "светлое" Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="320c9-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="320c9-118">Сводка по устранению основных проблем</span><span class="sxs-lookup"><span data-stu-id="320c9-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="320c9-119">Частые вызовы сетевых обновлений при обновлении окна диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="320c9-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="320c9-120">Отложенная прокрутка при переходе в режим установленного представления в диспетчере пакетов</span><span class="sxs-lookup"><span data-stu-id="320c9-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="320c9-121">Сетевые вызовы должны выполняться в фоновом потоке.</span><span class="sxs-lookup"><span data-stu-id="320c9-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="320c9-122">Добавлен флажок "не показывать окно предварительного просмотра"</span><span class="sxs-lookup"><span data-stu-id="320c9-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="320c9-123">Добавлено регулирование процессов для сокращения загрузки процессора.</span><span class="sxs-lookup"><span data-stu-id="320c9-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="320c9-124">Улучшенная обработка ссылок на библиотеки переносимых классов</span><span class="sxs-lookup"><span data-stu-id="320c9-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="320c9-125">Служба автозаполнения с учетом регистра</span><span class="sxs-lookup"><span data-stu-id="320c9-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="320c9-126">Обновление для повторного ввода учетных данных базовой проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="320c9-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="320c9-127">Улучшено ведение журналов ошибок.</span><span class="sxs-lookup"><span data-stu-id="320c9-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="320c9-128">Улучшены сообщения об ошибках PowerShell при вызове Update-Package</span><span class="sxs-lookup"><span data-stu-id="320c9-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="320c9-129">Исправлена ссылка "Подробнее о вариантах", чтобы предотвратить сбой в Windows 10</span><span class="sxs-lookup"><span data-stu-id="320c9-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="320c9-130">Запоминать параметр флажка предварительного выпуска</span><span class="sxs-lookup"><span data-stu-id="320c9-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="320c9-131">Повышение производительности сбора путем кэширования результатов по проектам в решении</span><span class="sxs-lookup"><span data-stu-id="320c9-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="320c9-132">Несколько пакетов можно собирать параллельно</span><span class="sxs-lookup"><span data-stu-id="320c9-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="320c9-133">Удалена команда install-Package-Force</span><span class="sxs-lookup"><span data-stu-id="320c9-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="320c9-134">Следите за [нашим блогом](http://blog.nuget.org) , чтобы получить дополнительные сведения и объявления о том, как мы готовы предоставить поддержку для разработки Windows 10.</span><span class="sxs-lookup"><span data-stu-id="320c9-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>