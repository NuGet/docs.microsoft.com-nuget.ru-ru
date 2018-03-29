---
title: Заметки о выпуске NuGet 2.5 | Документы Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Заметки о выпуске для NuGet 2.5, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
keywords: NuGet 2.5 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4495e1ea9cc4ec13ef330e56d12de1320cf10b24
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="3381f-104">Заметки о выпуске 2.5 NuGet</span><span class="sxs-lookup"><span data-stu-id="3381f-104">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="3381f-105">[Заметки о выпуске NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [заметки о выпуске NuGet 2.6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="3381f-105">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="3381f-106">NuGet 2.5 была выпущена 25 апреля 2013 г.</span><span class="sxs-lookup"><span data-stu-id="3381f-106">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="3381f-107">Этот выпуск был так велико, мы полагаем, вовсе пропустить версии 2.3 и 2.4!</span><span class="sxs-lookup"><span data-stu-id="3381f-107">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="3381f-108">На сегодняшний день это наибольшее выпуск, для NuGet, как изменилась с через [160 рабочие элементы](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) в выпуске.</span><span class="sxs-lookup"><span data-stu-id="3381f-108">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="3381f-109">Благодарности</span><span class="sxs-lookup"><span data-stu-id="3381f-109">Acknowledgements</span></span>

<span data-ttu-id="3381f-110">Мы бы хотели поблагодарить следующих внешних участников для их значительный вклад в NuGet 2.5 службу:</span><span class="sxs-lookup"><span data-stu-id="3381f-110">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="3381f-111">[Дэниела Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="3381f-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="3381f-112">[#2847](https://nuget.codeplex.com/workitem/2847) -добавить MonoAndroid, MonoTouch и MonoMac в список известных целевых framework идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="3381f-112">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
1. <span data-ttu-id="3381f-113">[Ж. Aragoneses Андреса](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="3381f-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="3381f-114">[#2865](https://nuget.codeplex.com/workitem/2865) -исправьте Правописание `NuGet.targets` для учета регистра ОС</span><span class="sxs-lookup"><span data-stu-id="3381f-114">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
1. <span data-ttu-id="3381f-115">[Дэвид Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="3381f-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="3381f-116">Сделать построения на моно решения.</span><span class="sxs-lookup"><span data-stu-id="3381f-116">Make the solution build on Mono.</span></span>
1. <span data-ttu-id="3381f-117">[Эндрю Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="3381f-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="3381f-118">Устраните сбои на моно модульных тестов.</span><span class="sxs-lookup"><span data-stu-id="3381f-118">Fix unit tests failing on Mono.</span></span>
1. <span data-ttu-id="3381f-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="3381f-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="3381f-120">[#2920](https://nuget.codeplex.com/workitem/2920) -команду nuget.exe пакет не распространяется свойства MSBuild</span><span class="sxs-lookup"><span data-stu-id="3381f-120">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
1. <span data-ttu-id="3381f-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="3381f-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="3381f-122">[#1511](https://nuget.codeplex.com/workitem/1511) — изменить XML код обработки для сохранения форматирования.</span><span class="sxs-lookup"><span data-stu-id="3381f-122">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
1. <span data-ttu-id="3381f-123">[Ральф Адам](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="3381f-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="3381f-124">Добавить распознанные слова в пользовательский словарь, чтобы разрешить build.cmd для успешного выполнения.</span><span class="sxs-lookup"><span data-stu-id="3381f-124">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
1. [<span data-ttu-id="3381f-125">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="3381f-125">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="3381f-126">Исправьте модульные тесты, при работе в локализованных VS.</span><span class="sxs-lookup"><span data-stu-id="3381f-126">Fix unit tests when running in localized VS.</span></span>
1. [<span data-ttu-id="3381f-127">Evans Гарета</span><span class="sxs-lookup"><span data-stu-id="3381f-127">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="3381f-128">Интерфейс, извлеченные из PackageService</span><span class="sxs-lookup"><span data-stu-id="3381f-128">Extracted interface from PackageService</span></span>
1. <span data-ttu-id="3381f-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="3381f-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
    - <span data-ttu-id="3381f-130">[#936](https://nuget.codeplex.com/workitem/936) -обрабатывать зависимости проекта, когда при помощи</span><span class="sxs-lookup"><span data-stu-id="3381f-130">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
1. <span data-ttu-id="3381f-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="3381f-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
    - <span data-ttu-id="3381f-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -поддержки открытым пароля при хранении учетных данных для источника пакета в файлах nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="3381f-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
1. <span data-ttu-id="3381f-133">[Джеймс Мэннинга](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="3381f-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
    - <span data-ttu-id="3381f-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -описание справки исправить Get-Package</span><span class="sxs-lookup"><span data-stu-id="3381f-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="3381f-135">Также Мы ценим следующим специалистам по обнаружению ошибок с помощью NuGet 2.5 бета-версии или версии-Кандидата, были утверждены и исправлена до выпуска окончательной версии:</span><span class="sxs-lookup"><span data-stu-id="3381f-135">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="3381f-136">[Реальное Tony](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="3381f-136">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="3381f-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest разорвано последние версии NuGet 2.4 и 2,5 построений</span><span class="sxs-lookup"><span data-stu-id="3381f-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="3381f-138">Возможности в выпуске</span><span class="sxs-lookup"><span data-stu-id="3381f-138">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="3381f-139">Разрешить пользователям переопределять файлы содержимого, которые уже существуют.</span><span class="sxs-lookup"><span data-stu-id="3381f-139">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="3381f-140">Одной из наиболее часто запрашиваемых функций все время была возможность перезаписывать файлы содержимого, которые уже существуют на диске, включенный в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="3381f-140">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="3381f-141">Начиная с версии NuGet 2.5, определяются эти конфликты и предложит перезаписывать файлы, в то время как ранее эти файлы всегда были пропущены.</span><span class="sxs-lookup"><span data-stu-id="3381f-141">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Перезапись файлов содержимого](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="3381f-143">«nuget.exe обновления» и «Install-Package» теперь имеют новый параметр "-FileConflictAction" некоторых значений по умолчанию для сценариев командной строки.</span><span class="sxs-lookup"><span data-stu-id="3381f-143">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="3381f-144">Задайте действие по умолчанию из пакета уже существует в целевом проекте.</span><span class="sxs-lookup"><span data-stu-id="3381f-144">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="3381f-145">Значение «Перезаписать» всегда перезаписывать файлы.</span><span class="sxs-lookup"><span data-stu-id="3381f-145">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="3381f-146">Задайте значение «Пропустить», чтобы пропустить файлы.</span><span class="sxs-lookup"><span data-stu-id="3381f-146">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="3381f-147">Если не указан, он запрашивает всех конфликтующих файлов.</span><span class="sxs-lookup"><span data-stu-id="3381f-147">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="3381f-148">Автоматический импорт MSBuild целевые объекты и props-файлы</span><span class="sxs-lookup"><span data-stu-id="3381f-148">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="3381f-149">Был создан новый обычную папку верхнего уровня пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="3381f-149">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="3381f-150">Как узел `\lib`, `\content`, и `\tools`, теперь можно включить `\build` папки в пакет.</span><span class="sxs-lookup"><span data-stu-id="3381f-150">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="3381f-151">В этой папке можно разместить два файла с фиксированными именами `{packageid}.targets` или `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="3381f-151">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="3381f-152">Эти два файла может быть либо напрямую в `build` или в отдельных папках так же, как и другие папки.</span><span class="sxs-lookup"><span data-stu-id="3381f-152">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="3381f-153">Правило для выбора папки резервную стратегию наилучшего соответствия платформы имеет точно такое же, как те.</span><span class="sxs-lookup"><span data-stu-id="3381f-153">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="3381f-154">При установке пакета NuGet с файлами \build добавит MSBuild `<Import>` в файле проекта, указывающий на элемент `.targets` и `.props` файлов.</span><span class="sxs-lookup"><span data-stu-id="3381f-154">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="3381f-155">`.props` Файл добавляется в начале, в то время как `.targets` файл будет добавлен в нижней.</span><span class="sxs-lookup"><span data-stu-id="3381f-155">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="3381f-156">Укажите другой ссылок на платформы с помощью `<References/>` элемент</span><span class="sxs-lookup"><span data-stu-id="3381f-156">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="3381f-157">Прежде чем 2.5 в `.nuspec` файла, пользователь может указать только файлы ссылок, нужно добавить для всех framework.</span><span class="sxs-lookup"><span data-stu-id="3381f-157">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="3381f-158">Теперь эта новая функция 2.5 пользователя появляется возможность разрабатывать `<reference/>` элемент для каждого из поддерживаемых платформ, например:</span><span class="sxs-lookup"><span data-stu-id="3381f-158">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="3381f-159">Ниже приведена последовательность действий для как NuGet добавляет ссылки на проекты, на основе `.nuspec` файла:</span><span class="sxs-lookup"><span data-stu-id="3381f-159">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="3381f-160">Найти `lib` папку, которая подходит для целевой версии .NET framework и получение списка сборок из этой папки</span><span class="sxs-lookup"><span data-stu-id="3381f-160">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="3381f-161">Отдельно найти ссылается на группу, которая подходит для целевой версии .NET framework и получение списка сборок из этой группы.</span><span class="sxs-lookup"><span data-stu-id="3381f-161">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="3381f-162">Группы ссылок не указан целевой платформы является группой отката.</span><span class="sxs-lookup"><span data-stu-id="3381f-162">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="3381f-163">Определение пересечения двух списков и использовать его в качестве ссылки для добавления</span><span class="sxs-lookup"><span data-stu-id="3381f-163">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="3381f-164">Эта новая функция позволяет авторам пакетов для использования функции ссылки для использования подмножества сборок в различных платформ, когда иначе потребовалось бы содержат повторяющиеся сборки в несколько `lib` папки.</span><span class="sxs-lookup"><span data-stu-id="3381f-164">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="3381f-165">Примечание: в настоящее время используется пакет nuget.exe для использования этой функции; Обозреватель пакетов NuGet пока не поддерживает его.</span><span class="sxs-lookup"><span data-stu-id="3381f-165">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="3381f-166">Обновить все кнопку, чтобы разрешить обновление всех пакетов за один раз</span><span class="sxs-lookup"><span data-stu-id="3381f-166">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="3381f-167">Многим из вас известно о командлете PowerShell «Обновление» для обновления всех своих пакетов; Теперь имеется простой способ сделать это через пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="3381f-167">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="3381f-168">Чтобы опробовать эту функцию:</span><span class="sxs-lookup"><span data-stu-id="3381f-168">To try this feature out:</span></span>

1. <span data-ttu-id="3381f-169">Создание нового приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="3381f-169">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="3381f-170">Открыть диалоговое окно «Управление пакетами NuGet»</span><span class="sxs-lookup"><span data-stu-id="3381f-170">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="3381f-171">Выберите «Обновления»</span><span class="sxs-lookup"><span data-stu-id="3381f-171">Select 'Updates'</span></span>
1. <span data-ttu-id="3381f-172">Нажмите кнопку "Обновить все"</span><span class="sxs-lookup"><span data-stu-id="3381f-172">Click the 'Update All' button</span></span>

![Кнопка «Обновить все» в диалоговом окне](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="3381f-174">Улучшенные проект ссылку на поддержку nuget.exe пакет</span><span class="sxs-lookup"><span data-stu-id="3381f-174">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="3381f-175">Теперь процессы команду nuget.exe пакетов ссылаться проекты со следующими правилами:</span><span class="sxs-lookup"><span data-stu-id="3381f-175">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="3381f-176">Если указанный проект содержит соответствующий `.nuspec` файла, например, имеется файл с именем `proj1.nuspec` в той же папке, что `proj1.csproj`, затем этот проект добавляется как элемент dependency в пакет, используя идентификатор и версия чтения из `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="3381f-176">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="3381f-177">В противном случае файлы проекта, на который указывает ссылка, объединены в пакет.</span><span class="sxs-lookup"><span data-stu-id="3381f-177">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="3381f-178">Затем проектов ссылается этот проект будет обрабатываться с помощью правила рекурсивно такими же.</span><span class="sxs-lookup"><span data-stu-id="3381f-178">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="3381f-179">Все библиотеки DLL, `.pdb`, и `.exe` добавляются файлы.</span><span class="sxs-lookup"><span data-stu-id="3381f-179">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="3381f-180">Все файлы содержимого добавляются.</span><span class="sxs-lookup"><span data-stu-id="3381f-180">All other content files are added.</span></span>
1. <span data-ttu-id="3381f-181">Все зависимости, объединяются.</span><span class="sxs-lookup"><span data-stu-id="3381f-181">All dependencies are merged.</span></span>

<span data-ttu-id="3381f-182">Это позволяет в связанном проекте следует рассматривать как зависимость, при наличии `.nuspec` файла, в противном случае он становится частью пакета.</span><span class="sxs-lookup"><span data-stu-id="3381f-182">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="3381f-183">Дополнительные сведения о здесь: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="3381f-183">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="3381f-184">Добавление свойства «Минимальная версия NuGet» в пакеты</span><span class="sxs-lookup"><span data-stu-id="3381f-184">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="3381f-185">Новый атрибут метаданных с названием «minClientVersion» теперь можно указать минимальную версию клиента NuGet требуется для использования пакета.</span><span class="sxs-lookup"><span data-stu-id="3381f-185">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="3381f-186">Эта функция позволяет автору пакета, чтобы указать, что пакет будет работать только после определенной версии NuGet.</span><span class="sxs-lookup"><span data-stu-id="3381f-186">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="3381f-187">А новые `.nuspec` функции добавляются после NuGet 2.5, пакеты будут утверждения Минимальная версия NuGet.</span><span class="sxs-lookup"><span data-stu-id="3381f-187">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="3381f-188">Если у пользователя есть NuGet 2.5 установлен и пакета определяется как требующее 2.6, визуальные подсказки присваивается пользователю о том, что пакет не будет иметь возможность установки.</span><span class="sxs-lookup"><span data-stu-id="3381f-188">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="3381f-189">Затем пользователю будет рекомендовано для обновления своих версия NuGet.</span><span class="sxs-lookup"><span data-stu-id="3381f-189">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="3381f-190">Это улучшит на работу существующих начинаются пакеты для установки, но произойдет сбой, указывающий, что версия схемы нераспознанный был определен.</span><span class="sxs-lookup"><span data-stu-id="3381f-190">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="3381f-191">Зависимости излишне больше не обновляются во время установки пакета</span><span class="sxs-lookup"><span data-stu-id="3381f-191">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="3381f-192">Прежде чем NuGet 2.5 при установке пакета, пакет уже установлен в проекте, зависят от зависимость будет обновлено в рамках новой установки, даже если существующая версия зависимости.</span><span class="sxs-lookup"><span data-stu-id="3381f-192">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="3381f-193">Начиная с помощью NuGet 2.5, если уже выполняется версия зависимости, зависимость не обновляется во время установки других пакетов.</span><span class="sxs-lookup"><span data-stu-id="3381f-193">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="3381f-194">**Сценарий:**</span><span class="sxs-lookup"><span data-stu-id="3381f-194">**The scenario:**</span></span>

1. <span data-ttu-id="3381f-195">Исходный репозиторий содержит пакет B версии 1.0.0 и версии 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="3381f-195">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="3381f-196">Он также содержит пакет A имеет зависимость от B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="3381f-196">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="3381f-197">Предполагается, что текущий проект уже содержит пакет B версии 1.0.0 установлен.</span><span class="sxs-lookup"><span data-stu-id="3381f-197">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="3381f-198">Теперь необходимо установить пакет A.</span><span class="sxs-lookup"><span data-stu-id="3381f-198">Now you want to install package A.</span></span>

<span data-ttu-id="3381f-199">**В NuGet версии 2.2 и более ранних версий:**</span><span class="sxs-lookup"><span data-stu-id="3381f-199">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="3381f-200">При установке пакета A, NuGet будет автоматически обновлена B до версии 1.0.2, несмотря на то, что существующие версии 1.0.0 уже удовлетворяющую зависимостей версии, являющийся > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="3381f-200">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="3381f-201">**В NuGet 2.5 и более новых версий:**</span><span class="sxs-lookup"><span data-stu-id="3381f-201">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="3381f-202">NuGet не будет обновляться B, поскольку обнаружит, что существующие версии 1.0.0 удовлетворяющую версию зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3381f-202">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="3381f-203">Дополнительные сведения об этом изменении см. в разделе подробных [рабочий элемент](http://nuget.codeplex.com/workitem/1681) и связанный с ним [поток дискуссии](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="3381f-203">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="3381f-204">NuGet.exe выходные данные HTTP-запросов, если подробный уровень детализации</span><span class="sxs-lookup"><span data-stu-id="3381f-204">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="3381f-205">При устранении неполадок nuget.exe или просто хотите какие запросов HTTP, выполненных во время операций "-детализации подробные" коммутатор теперь выходные данные всех HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="3381f-205">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Выходные данные НТТР из nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="3381f-207">NuGet.exe принудительной теперь поддерживает источники UNC-пути и папок</span><span class="sxs-lookup"><span data-stu-id="3381f-207">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="3381f-208">Перед NuGet 2.5 если предпринята попытка на основе UNC-путь или локальную папку источника пакета для запуска «nuget.exe push» извещающей завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="3381f-208">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="3381f-209">С компонентом недавно добавленных иерархической конфигурации стать часто nuget.exe для ориентируется источник папку в формате UNC или на основе HTTP галереи NuGet.</span><span class="sxs-lookup"><span data-stu-id="3381f-209">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="3381f-210">Начиная с помощью NuGet 2.5, если nuget.exe определяет источник папку в формате UNC, он выполняет копирование файлов в источнике.</span><span class="sxs-lookup"><span data-stu-id="3381f-210">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="3381f-211">Теперь рассмотрим следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3381f-211">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="3381f-212">NuGet.exe поддерживает явно указанные файлы конфигурации</span><span class="sxs-lookup"><span data-stu-id="3381f-212">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="3381f-213">NuGet.exe команды, которые обращаются к конфигурации (все, кроме «спецификация» и «pack») теперь поддерживает новый "-ConfigFile" параметр, благодаря чему файла конфигурации, определенных для использования вместо файла конфигурации по умолчанию в папке % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="3381f-213">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="3381f-214">Пример</span><span class="sxs-lookup"><span data-stu-id="3381f-214">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="3381f-215">Поддержка для собственных проектов</span><span class="sxs-lookup"><span data-stu-id="3381f-215">Support for Native projects</span></span>

<span data-ttu-id="3381f-216">С помощью NuGet 2.5 инструментарий NuGet теперь доступна для собственных проектов в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3381f-216">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="3381f-217">Ожидается, что наиболее простые пакеты будут использовать функцию импорта MSBuild выше, с помощью средства, созданные [CoApp проекта](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="3381f-217">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="3381f-218">Дополнительные сведения см. в статье [сведения об этом средстве](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="3381f-218">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="3381f-219">Имя целевой платформы «native» введено для пакетов, включаемых файлов в \build \content и \tools при установке пакета в проекте.</span><span class="sxs-lookup"><span data-stu-id="3381f-219">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="3381f-220">\`Lib "папка не используется для собственных проектов.</span><span class="sxs-lookup"><span data-stu-id="3381f-220">The \`lib` folder is not used for native projects.</span></span>
