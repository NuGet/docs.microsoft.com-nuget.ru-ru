---
title: Заметки о выпуске 2.5 NuGet
description: Заметки о выпуске для NuGet 2.5, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550487"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="57010-103">Заметки о выпуске 2.5 NuGet</span><span class="sxs-lookup"><span data-stu-id="57010-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="57010-104">[Заметки о выпуске NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [заметки о выпуске NuGet 2.6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="57010-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="57010-105">25 апреля 2013 г. был выпущен NuGet 2.5.</span><span class="sxs-lookup"><span data-stu-id="57010-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="57010-106">Этот выпуск был такой большой размер, мы полагаем, необходимость пропустить версии 2.3 и 2.4!</span><span class="sxs-lookup"><span data-stu-id="57010-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="57010-107">На сегодняшний день это самый крупный выпуск, мы открыли для NuGet, через [160 рабочие элементы](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) в выпуске.</span><span class="sxs-lookup"><span data-stu-id="57010-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="57010-108">Благодарности</span><span class="sxs-lookup"><span data-stu-id="57010-108">Acknowledgements</span></span>

<span data-ttu-id="57010-109">Мы бы хотели поблагодарить следующих внешних участников для их вклад в NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="57010-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="57010-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="57010-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="57010-111">[#2847](https://nuget.codeplex.com/workitem/2847) -добавить MonoAndroid MonoTouch и MonoMac в список известных целевых идентификаторов платформы.</span><span class="sxs-lookup"><span data-stu-id="57010-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="57010-112">[Ж. Aragoneses Андрес](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="57010-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="57010-113">[#2865](https://nuget.codeplex.com/workitem/2865) -исправьте Правописание `NuGet.targets` для операционной системы с учетом регистра</span><span class="sxs-lookup"><span data-stu-id="57010-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="57010-114">[Дэвид Фаулер](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="57010-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="57010-115">Сделайте построения в Mono решения.</span><span class="sxs-lookup"><span data-stu-id="57010-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="57010-116">[Эндрю Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="57010-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="57010-117">Исправьте модульных тестов, сбой в Mono.</span><span class="sxs-lookup"><span data-stu-id="57010-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="57010-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="57010-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="57010-119">[#2920](https://nuget.codeplex.com/workitem/2920) -команда nuget.exe pack не передает свойства в MSBuild</span><span class="sxs-lookup"><span data-stu-id="57010-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="57010-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="57010-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="57010-121">[#1511](https://nuget.codeplex.com/workitem/1511) — изменить XML код обработки для сохранения форматирования.</span><span class="sxs-lookup"><span data-stu-id="57010-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="57010-122">[Ральф ADAM](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="57010-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="57010-123">Добавить пользовательский словарь, чтобы разрешить build.cmd для успешного выполнения распознанных слов.</span><span class="sxs-lookup"><span data-stu-id="57010-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="57010-124">Бруно Roggeri</span><span class="sxs-lookup"><span data-stu-id="57010-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="57010-125">Исправьте модульные тесты, при работе в локализованных VS.</span><span class="sxs-lookup"><span data-stu-id="57010-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="57010-126">Гарет Эванс</span><span class="sxs-lookup"><span data-stu-id="57010-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="57010-127">Интерфейс, извлеченные из PackageService</span><span class="sxs-lookup"><span data-stu-id="57010-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="57010-128">[Максим Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="57010-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="57010-129">[#936](https://nuget.codeplex.com/workitem/936) -обработка зависимостей проекта, при упаковке</span><span class="sxs-lookup"><span data-stu-id="57010-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="57010-130">[Ксавье Декостера](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="57010-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="57010-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -поддержка Очистить текст пароля при хранении учетных данных для источника пакета в файлах nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="57010-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="57010-132">[Джеймса Мэннинга](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="57010-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="57010-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -описание help Get-Package, исправить</span><span class="sxs-lookup"><span data-stu-id="57010-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="57010-134">Мы также рады будем услышать следующим по обнаружению ошибок с помощью NuGet 2.5 бета-версии или версии-Кандидата, были утверждены и исправлены в окончательном выпуске:</span><span class="sxs-lookup"><span data-stu-id="57010-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="57010-135">[Тони стены](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="57010-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="57010-136">[#3200](https://nuget.codeplex.com/workitem/3200) — MSTest, с возможностью разрыва с последней NuGet 2.4 и 2.5 сборки</span><span class="sxs-lookup"><span data-stu-id="57010-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="57010-137">Важные возможности в выпуске</span><span class="sxs-lookup"><span data-stu-id="57010-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="57010-138">Разрешить пользователям переопределять файлы содержимого, которые уже существуют</span><span class="sxs-lookup"><span data-stu-id="57010-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="57010-139">Одной из наиболее востребованных функций от общего времени была возможность перезаписывать файлы содержимого, которые уже существуют на диске, включенная в пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="57010-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="57010-140">Начиная с NuGet 2.5, определяются эти конфликты и будет предложено перезаписать файлы, тогда как ранее эти файлы всегда были пропущены.</span><span class="sxs-lookup"><span data-stu-id="57010-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Перезаписать файлы содержимого](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="57010-142">«nuget.exe обновления» и «Install-Package» теперь имеют новый параметр "-FileConflictAction" задать некоторые по умолчанию для сценариев командной строки.</span><span class="sxs-lookup"><span data-stu-id="57010-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="57010-143">Задайте действие по умолчанию, когда файл из пакета уже существует в целевом проекте.</span><span class="sxs-lookup"><span data-stu-id="57010-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="57010-144">Значение «Перезаписать», чтобы всегда перезаписывать файлы.</span><span class="sxs-lookup"><span data-stu-id="57010-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="57010-145">Значение «Пропустить», чтобы пропустить файлы.</span><span class="sxs-lookup"><span data-stu-id="57010-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="57010-146">Если не указан, он предложит ввести каждый конфликтующий файл.</span><span class="sxs-lookup"><span data-stu-id="57010-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="57010-147">Автоматический импорт файлов целевых объектов и свойств MSBuild</span><span class="sxs-lookup"><span data-stu-id="57010-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="57010-148">Был создан новый обычную папку верхнего уровня пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="57010-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="57010-149">Как узел `\lib`, `\content`, и `\tools`, вы теперь можете включать `\build` папку в пакет.</span><span class="sxs-lookup"><span data-stu-id="57010-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="57010-150">В этой папке можно поместить два файла с фиксированными именами `{packageid}.targets` или `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="57010-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="57010-151">Эти два файла может быть либо непосредственно в разделе `build` или в папках зависящие от платформы, как другие папки.</span><span class="sxs-lookup"><span data-stu-id="57010-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="57010-152">Правило для выбора папки стратегия наилучшего соответствия framework именно то, как в их.</span><span class="sxs-lookup"><span data-stu-id="57010-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="57010-153">Когда NuGet устанавливает пакет с файлами \build, он добавит MSBuild `<Import>` в файле проекта, указывающий на элемент `.targets` и `.props` файлы.</span><span class="sxs-lookup"><span data-stu-id="57010-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="57010-154">`.props` Файл добавляется в верхней, тогда как `.targets` файл добавляется в нижнюю.</span><span class="sxs-lookup"><span data-stu-id="57010-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="57010-155">Укажите различные ссылки на платформу с помощью `<References/>` элемент</span><span class="sxs-lookup"><span data-stu-id="57010-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="57010-156">Прежде чем 2.5 в `.nuspec` файл, пользователь может указать только файлы ссылок, которую нужно добавить для всех framework.</span><span class="sxs-lookup"><span data-stu-id="57010-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="57010-157">Теперь эта новая функция в версии 2.5, можно создать пользователя `<reference/>` элемент для каждой поддерживаемой платформы, например:</span><span class="sxs-lookup"><span data-stu-id="57010-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="57010-158">Ниже приведена последовательность действий для как NuGet добавляет ссылки на проекты на основе `.nuspec` файла:</span><span class="sxs-lookup"><span data-stu-id="57010-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="57010-159">Найти `lib` папку, которая подходит для целевой платформы и получить список сборок, из этой папки</span><span class="sxs-lookup"><span data-stu-id="57010-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="57010-160">Отдельно найти ссылки на группы, соответствующий требуемой версии .NET framework и получить список сборок, из этой группы.</span><span class="sxs-lookup"><span data-stu-id="57010-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="57010-161">Группа ссылок без целевой платформы, указанной является группой резервный.</span><span class="sxs-lookup"><span data-stu-id="57010-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="57010-162">Определение пересечения двух списков и использовать его в качестве ссылки для добавления</span><span class="sxs-lookup"><span data-stu-id="57010-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="57010-163">Эта новая функция позволяет авторам пакетов для использования ссылки для применения подмножеств сборок для различных платформ, когда в противном случае потребуется для выполнения повторяющихся сборок в нескольких `lib` папки.</span><span class="sxs-lookup"><span data-stu-id="57010-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="57010-164">Примечание: необходимо сейчас использовать пакет nuget.exe для использования этой функции; Обозреватель пакетов NuGet пока не поддерживает его.</span><span class="sxs-lookup"><span data-stu-id="57010-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="57010-165">Кнопка «Обновить все», чтобы разрешить обновление всех пакетов за один раз</span><span class="sxs-lookup"><span data-stu-id="57010-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="57010-166">Многие из вас знают о командлете PowerShell «Update-Package» обновить все пакеты; Теперь есть простой способ сделать это через пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="57010-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="57010-167">Чтобы опробовать эту функцию:</span><span class="sxs-lookup"><span data-stu-id="57010-167">To try this feature out:</span></span>

1. <span data-ttu-id="57010-168">Создайте новое приложение ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="57010-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="57010-169">Открыть диалоговое окно «Управление пакетами NuGet»</span><span class="sxs-lookup"><span data-stu-id="57010-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="57010-170">Выберите «Обновления»</span><span class="sxs-lookup"><span data-stu-id="57010-170">Select 'Updates'</span></span>
1. <span data-ttu-id="57010-171">Нажмите кнопку "Обновить все"</span><span class="sxs-lookup"><span data-stu-id="57010-171">Click the 'Update All' button</span></span>

![Кнопка «Обновить все» в диалоговом окне](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="57010-173">Поддержка ссылок на улучшенные проекта для nuget.exe пакета</span><span class="sxs-lookup"><span data-stu-id="57010-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="57010-174">Теперь процессов команды пакет nuget.exe ссылки на проекты со следующими правилами:</span><span class="sxs-lookup"><span data-stu-id="57010-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="57010-175">Если у упоминаемого проекта есть соответствующий `.nuspec` файл, например — в файл с именем `proj1.nuspec` в той же папке, что `proj1.csproj`, то этот проект добавляется как зависимость для пакета, используя идентификатор и версия чтение из `.nuspec` файла.</span><span class="sxs-lookup"><span data-stu-id="57010-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="57010-176">В противном случае файлы проекта, на который указывает ссылка, объединяются в пакет.</span><span class="sxs-lookup"><span data-stu-id="57010-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="57010-177">Затем проектов ссылается этот проект будет обрабатываться с помощью правил привычными рекурсивно.</span><span class="sxs-lookup"><span data-stu-id="57010-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="57010-178">Все библиотеки DLL, `.pdb`, и `.exe` будут добавлены файлы.</span><span class="sxs-lookup"><span data-stu-id="57010-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="57010-179">Все файлы содержимого добавляются.</span><span class="sxs-lookup"><span data-stu-id="57010-179">All other content files are added.</span></span>
1. <span data-ttu-id="57010-180">Объединяются все зависимости.</span><span class="sxs-lookup"><span data-stu-id="57010-180">All dependencies are merged.</span></span>

<span data-ttu-id="57010-181">Таким образом, на которую указывает ссылка проекта следует рассматривать как зависимость, если имеется `.nuspec` файл, в противном случае он становится частью пакета.</span><span class="sxs-lookup"><span data-stu-id="57010-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="57010-182">Подробные сведения приведены здесь: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="57010-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="57010-183">Добавить свойство «Минимальная версия NuGet» в пакеты</span><span class="sxs-lookup"><span data-stu-id="57010-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="57010-184">Новый атрибут метаданных с именем «minClientVersion» теперь можно указать минимальную версию клиента NuGet, необходимые для использования пакета.</span><span class="sxs-lookup"><span data-stu-id="57010-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="57010-185">Эта функция позволяет автору пакета для указания, что пакет будет работать только после определенной версии NuGet.</span><span class="sxs-lookup"><span data-stu-id="57010-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="57010-186">А новые `.nuspec` функции добавляются после NuGet 2.5, пакеты будут иметь возможность утверждения под управлением версии NuGet.</span><span class="sxs-lookup"><span data-stu-id="57010-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="57010-187">Если у пользователя установлена NuGet 2.5, пакета определяется как требование 2.6 визуальные подсказки будет назначено пользователю, указывающий, что пакет не будет иметь возможность установки.</span><span class="sxs-lookup"><span data-stu-id="57010-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="57010-188">Затем пользователю будет рекомендовано для обновления своей версии NuGet.</span><span class="sxs-lookup"><span data-stu-id="57010-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="57010-189">Это улучшит по существующему процессу, где пакеты приступить к установке, но затем произойдет сбой, указывающий, что обнаружена версия схемы не распознана.</span><span class="sxs-lookup"><span data-stu-id="57010-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="57010-190">Зависимости излишне больше не обновляются во время установки пакета</span><span class="sxs-lookup"><span data-stu-id="57010-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="57010-191">Перед NuGet 2.5 при установке пакета, зависит от пакета, уже установленного в проекте, зависимость будет обновлено как часть новой установкой, даже если существующая версия соответствует зависимости.</span><span class="sxs-lookup"><span data-stu-id="57010-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="57010-192">Начиная с NuGet 2.5, если версия зависимости уже удовлетворена, зависимость не обновляется при установке других пакетов.</span><span class="sxs-lookup"><span data-stu-id="57010-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="57010-193">**Сценарий:**</span><span class="sxs-lookup"><span data-stu-id="57010-193">**The scenario:**</span></span>

1. <span data-ttu-id="57010-194">Исходный репозиторий содержит пакет B версии 1.0.0 и 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="57010-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="57010-195">Он также содержит пакета A, который имеет зависимость от B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="57010-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="57010-196">Предположим, что текущий проект уже содержит пакет B версии 1.0.0 установлен.</span><span class="sxs-lookup"><span data-stu-id="57010-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="57010-197">Теперь вы хотите установить пакет A.</span><span class="sxs-lookup"><span data-stu-id="57010-197">Now you want to install package A.</span></span>

<span data-ttu-id="57010-198">**В NuGet версии 2.2 и более ранних версий:**</span><span class="sxs-lookup"><span data-stu-id="57010-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="57010-199">При установке пакета A, NuGet будет автоматически обновлен B 1.0.2, несмотря на то, что существующая версия 1.0.0 уже удовлетворяет ограничение версии зависимостей, который является > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="57010-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="57010-200">**В NuGet 2.5 и более поздних версий:**</span><span class="sxs-lookup"><span data-stu-id="57010-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="57010-201">NuGet не будет обновляться B, так как он обнаруживает, что существующая версия 1.0.0 удовлетворяет ограничению по версии зависимости.</span><span class="sxs-lookup"><span data-stu-id="57010-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="57010-202">Дополнительные сведения об этом изменении см. подробные [рабочий элемент](http://nuget.codeplex.com/workitem/1681) а также связанные [обсуждений](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="57010-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="57010-203">NuGet.exe выводит HTTP-запросов с подробным уровнем детализации</span><span class="sxs-lookup"><span data-stu-id="57010-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="57010-204">Если вы устраняете nuget.exe, или просто интересно, какие HTTP-запросы выполняются во время операций, "-уровень детализации подробные" коммутатор теперь выходные данные всех HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="57010-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Выходные данные HTTP nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="57010-206">NuGet.exe push теперь поддерживает источники UNC и папки</span><span class="sxs-lookup"><span data-stu-id="57010-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="57010-207">Прежде чем NuGet 2.5 Если была предпринята попытка запуска «nuget.exe push» к источнику пакета, на основе UNC-путь или локальную папку, отправка завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="57010-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="57010-208">С помощью функции недавно добавленных иерархической конфигурации его стали распространенными для nuget.exe для нужно выбрать источник папку в формате UNC или коллекции NuGet на основе HTTP.</span><span class="sxs-lookup"><span data-stu-id="57010-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="57010-209">Начиная с NuGet 2.5, если nuget.exe обнаружит источник папку в формате UNC, он выполняет копирование файлов в источник.</span><span class="sxs-lookup"><span data-stu-id="57010-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="57010-210">Теперь рассмотрим следующую команду:</span><span class="sxs-lookup"><span data-stu-id="57010-210">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="57010-211">NuGet.exe поддерживает явно указанные файлы конфигурации</span><span class="sxs-lookup"><span data-stu-id="57010-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="57010-212">команды NuGet.exe, которые обращаются к конфигурации (все, кроме «спецификации» и «pack») теперь поддерживает новый "-ConfigFile" параметр, который заставляет файла конфигурации, определенной для использования вместо файла конфигурации по умолчанию в папке % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="57010-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="57010-213">Пример</span><span class="sxs-lookup"><span data-stu-id="57010-213">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="57010-214">Поддержка проектов в машинном коде</span><span class="sxs-lookup"><span data-stu-id="57010-214">Support for Native projects</span></span>

<span data-ttu-id="57010-215">В NuGet 2.5 инструменты NuGet теперь доступна для собственных проектов в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="57010-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="57010-216">Ожидается, что наиболее собственные пакеты будут использовать функцию импорты MSBuild выше, с помощью средства, созданные [CoApp проекта](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="57010-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="57010-217">Дополнительные сведения в статье [сведения об этом средстве](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="57010-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="57010-218">Имя целевой платформы из «native» введено для пакетов включить файлы в \build, \content и \tools, когда пакет устанавливается в собственный проект.</span><span class="sxs-lookup"><span data-stu-id="57010-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="57010-219">\`Lib "папка не используется для собственных проектов.</span><span class="sxs-lookup"><span data-stu-id="57010-219">The \`lib` folder is not used for native projects.</span></span>
