---
title: Заметки о выпуске NuGet версии 3.0
description: Заметки о выпуске для NuGet 3.0.0, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551867"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="87d21-103">Заметки о выпуске NuGet версии 3.0</span><span class="sxs-lookup"><span data-stu-id="87d21-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="87d21-104">[Заметки о выпуске NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [заметки о выпуске NuGet 3.1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="87d21-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="87d21-105">NuGet 3.0 был выпущен 20 июля 2015 г. как расширение пакета в Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="87d21-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="87d21-106">Мы реализовали для доставки этого выпуска с помощью Visual Studio, чтобы полный обновленный интерфейс NuGet 3.0 будут доступны для новых пользователей Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87d21-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="87d21-107">Эта версия расширения NuGet доступна только для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="87d21-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="87d21-108">Мы рекомендуем тех разработчиков, имеющих доступ к коллекции Visual Studio с обновлением до последней версии, доступен, как мы публикуем обновления вскоре после выпуска Visual Studio 2015, который включает в себя поддержку разработки для Windows 10.</span><span class="sxs-lookup"><span data-stu-id="87d21-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="87d21-109">В целом, мы закрытых 240 проблем в версии 3.0, и вы можете просмотреть [полный список проблем на GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="87d21-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="87d21-110">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="87d21-110">Known Issues</span></span>

<span data-ttu-id="87d21-111">Несколько известных проблем, присутствующие в этом выпуске, и все эти элементы являются исправлено в наших запланированных 3.1 совпал с выпуском Windows 10, 29 июля.</span><span class="sxs-lookup"><span data-stu-id="87d21-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="87d21-112">Вы сможете обновить расширение Visual Studio из коллекции не ранее этой даты устранения этих известных проблем.</span><span class="sxs-lookup"><span data-stu-id="87d21-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="87d21-113">Перевод не предоставляется для метки «Больше не показывать это снова» в окне предварительного просмотра и метка «Авторы» в окне Описание пакета.</span><span class="sxs-lookup"><span data-stu-id="87d21-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="87d21-114">Когда вы работаете над проектом с помощью TFS система управления версиями, NuGet не может представить диспетчер пакетов пользовательский интерфейс, если файл Nuget.Config помечен как доступный только для чтения.</span><span class="sxs-lookup"><span data-stu-id="87d21-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="87d21-115">**Инструкции по решению** извлечь файл из Team Foundation Server.</span><span class="sxs-lookup"><span data-stu-id="87d21-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="87d21-116">При использовании Visual Studio "темной" теме текст желтым «перезапуск рама» в окне NuGet Powershell не отображается.</span><span class="sxs-lookup"><span data-stu-id="87d21-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="87d21-117">**Инструкции по решению** использовать Visual Studio "светлой" теме.</span><span class="sxs-lookup"><span data-stu-id="87d21-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="87d21-118">Сводка по устранить основные проблемы</span><span class="sxs-lookup"><span data-stu-id="87d21-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="87d21-119">Обновление сети часто вызывается, когда обновляет окно диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="87d21-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="87d21-120">Отложенной прокрутки, при изменении на установке представление в диспетчере пакетов</span><span class="sxs-lookup"><span data-stu-id="87d21-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="87d21-121">Сетевые вызовы, которые должны выполняться в фоновом потоке</span><span class="sxs-lookup"><span data-stu-id="87d21-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="87d21-122">Добавлен флажок «Больше не показывать окно предварительного просмотра»</span><span class="sxs-lookup"><span data-stu-id="87d21-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="87d21-123">Добавленный процесс, регулирование, чтобы снизить использование процессора</span><span class="sxs-lookup"><span data-stu-id="87d21-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="87d21-124">Улучшенную обработку справочном руководстве библиотеки portable классов</span><span class="sxs-lookup"><span data-stu-id="87d21-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="87d21-125">Автозаполнение служба была с учетом регистра</span><span class="sxs-lookup"><span data-stu-id="87d21-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="87d21-126">Обновления, чтобы повторно ввести учетные данные обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="87d21-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="87d21-127">Улучшено ведение журналов ошибок</span><span class="sxs-lookup"><span data-stu-id="87d21-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="87d21-128">Powershell улучшенные сообщения об ошибках при вызове Update-Package</span><span class="sxs-lookup"><span data-stu-id="87d21-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="87d21-129">Исправлена ссылка «Дополнительные сведения о параметрах» во избежание аварийно завершается на Windows 10</span><span class="sxs-lookup"><span data-stu-id="87d21-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="87d21-130">Помните, параметр флажок предварительной версии</span><span class="sxs-lookup"><span data-stu-id="87d21-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="87d21-131">Улучшенная сбора сведений о производительности путем кэширования результатов по проектам в решении</span><span class="sxs-lookup"><span data-stu-id="87d21-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="87d21-132">Несколько пакетов могут собираться в параллельном режиме</span><span class="sxs-lookup"><span data-stu-id="87d21-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="87d21-133">Удалены install-package-принудительно команда</span><span class="sxs-lookup"><span data-stu-id="87d21-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="87d21-134">Пожалуйста, обратите внимание на [наш блог](http://blog.nuget.org) дополнительные ход выполнения и объявления поскольку мы получаем вы готовы предоставлять поддержку разработки для Windows 10.</span><span class="sxs-lookup"><span data-stu-id="87d21-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>