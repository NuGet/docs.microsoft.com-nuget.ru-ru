---
title: "Устранение неполадок с восстановлением пакетов NuGet в Visual Studio | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Описание распространенных ошибок восстановления NuGet в Visual Studio и способов их устранения."
keywords: "восстановление пакетов NuGet, восстановление пакетов, устранение неполадок, устранение ошибок"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="29149-104">Устранение ошибок при восстановлении пакетов</span><span class="sxs-lookup"><span data-stu-id="29149-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="29149-105">Эта статья посвящена распространенным ошибкам, возникающим при восстановлении пакетов, и мерам по их устранению.</span><span class="sxs-lookup"><span data-stu-id="29149-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="29149-106">Дополнительные сведения о восстановлении пакетов см. в разделе [Восстановление пакета](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="29149-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="29149-107">Если приведенные здесь инструкции не работают, [сообщите о проблеме на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли тщательнее изучить ваш случай.</span><span class="sxs-lookup"><span data-stu-id="29149-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="29149-108">Не используйте элемент управления "Была ли эта страница полезной?",</span><span class="sxs-lookup"><span data-stu-id="29149-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="29149-109">который может отображаться на этой странице, так как это не позволяет нам связаться с вами для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="29149-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="29149-110">Быстрое решение для пользователей Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29149-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="29149-111">Если вы используете Visual Studio, сначала включите восстановление пакета, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="29149-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="29149-112">В противном случае перейдите к приведенным далее разделам.</span><span class="sxs-lookup"><span data-stu-id="29149-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="29149-113">Выберите команду **Сервис > Диспетчер пакетов NuGet > Параметры диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="29149-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="29149-114">Задайте оба параметра в разделе **Восстановление пакета**.</span><span class="sxs-lookup"><span data-stu-id="29149-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="29149-115">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="29149-115">Select **OK**.</span></span>
1. <span data-ttu-id="29149-116">Повторите сборку проекта.</span><span class="sxs-lookup"><span data-stu-id="29149-116">Build your project again.</span></span>

![Включите восстановление пакетов NuGet в меню "Сервис", "Параметры".](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="29149-118">Эти параметры также можно изменить в файле `NuGet.config`; см раздел о [согласии](#consent).</span><span class="sxs-lookup"><span data-stu-id="29149-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="29149-119">Данный проект ссылается на пакеты NuGet, отсутствующие на этом компьютере</span><span class="sxs-lookup"><span data-stu-id="29149-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="29149-120">Полное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="29149-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="29149-121">Эта ошибка возникает при попытке выполнить сборку проекта, содержащего ссылки на один пакет NuGet ли несколько, которые сейчас не кэшированы в проекте.</span><span class="sxs-lookup"><span data-stu-id="29149-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently cached in the project.</span></span> <span data-ttu-id="29149-122">(Пакеты кэшируются в папке `packages` в корне решения, если проект использует `packages.config`, или в файле `obj/project.assets.json`, если проект использует формат PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="29149-122">(Packages are cached in a `packages` folder at the solution root if the project uses `packages.config`, or in the `obj/project.assets.json` file if the project uses the PackageReference format.)</span></span>

<span data-ttu-id="29149-123">Обычно такая ситуация возникает при получении исходного кода проекта из системы управления версиями или другого скачанного файла.</span><span class="sxs-lookup"><span data-stu-id="29149-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="29149-124">Пакеты обычно исключаются из системы управления версиями или скачиваемых файлов, так как их можно восстановить из веб-каналов пакета, например nuget.org (см. раздел [Пакеты и система управления версиями](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="29149-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="29149-125">Их включение приведет к раздуванию репозитория или созданию слишком больших ZIP-файлов.</span><span class="sxs-lookup"><span data-stu-id="29149-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="29149-126">Для восстановления пакетов используйте один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="29149-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="29149-127">В Visual Studio включите восстановление пакетов, выбрав команду **Сервис > Диспетчер пакетов NuGet > Параметры диспетчера пакета**, задав оба параметра в разделе **Восстановление пакета** и нажав кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="29149-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="29149-128">Выполните сборку решения еще раз.</span><span class="sxs-lookup"><span data-stu-id="29149-128">Then build the solution again.</span></span>
- <span data-ttu-id="29149-129">Для проектов .NET Core запустите `dotnet restore` или `dotnet build` (при этом восстановление запускается автоматически).</span><span class="sxs-lookup"><span data-stu-id="29149-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="29149-130">В командной строке запустите `nuget restore` (за исключением проектов, созданных с помощью `dotnet`, для них используйте `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="29149-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="29149-131">В командной строке с проектами, использующими формат PackageReference, запустите `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="29149-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="29149-132">После успешного восстановления вы должны увидеть либо папку `packages` (при использовании `packages.config`), либо файл `obj/project.assets.json` (при использовании PackageReference).</span><span class="sxs-lookup"><span data-stu-id="29149-132">After a successful restore, you should see either a `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference).</span></span> <span data-ttu-id="29149-133">Теперь сборка проекта должна пройти без ошибок.</span><span class="sxs-lookup"><span data-stu-id="29149-133">The project should now build successfully.</span></span> <span data-ttu-id="29149-134">В противном случае [сообщите о проблеме на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли связаться с вами.</span><span class="sxs-lookup"><span data-stu-id="29149-134">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="29149-135">Файл ресурсов project.assets.json не найден</span><span class="sxs-lookup"><span data-stu-id="29149-135">Assets file project.assets.json not found</span></span>

<span data-ttu-id="29149-136">Полное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="29149-136">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="29149-137">Эта ошибка возникает по тем же причинам, которые описаны в [предыдущем разделе](#missing), и устраняется теми же способами.</span><span class="sxs-lookup"><span data-stu-id="29149-137">This error occurs for the same reasons as explained in the [previous section](#missing), and has the same remedies.</span></span> <span data-ttu-id="29149-138">Например, если запустить `msbuild` для проекта .NET Core, который не был получен из системы управления версиями, пакеты не восстанавливаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="29149-138">For example, running `msbuild` on a .NET Core project that's been obtained from source control won't automatically restore packages.</span></span> <span data-ttu-id="29149-139">В этом случае запустите `msbuild /t:restore` и затем `msbuild` или используйте `dotnet build` (при этом пакеты восстанавливаются автоматически).</span><span class="sxs-lookup"><span data-stu-id="29149-139">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="29149-140">Необходимо восстановить один пакет NuGet или несколько, но это не удалось выполнить, так как не было получено согласие</span><span class="sxs-lookup"><span data-stu-id="29149-140">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="29149-141">Полное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="29149-141">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="29149-142">Эта ошибка означает, что восстановление пакета отключено в конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="29149-142">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="29149-143">Вы можете изменить подходящие параметры в Visual Studio, как описано выше в разделе [Быстрое решение для пользователей Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="29149-143">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="29149-144">Можно также изменить эти параметры напрямую в соответствующем файле `nuget.config` (обычно это `%AppData%\NuGet\NuGet.Config` в Windows и `~/.nuget/NuGet/NuGet.Config` в Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="29149-144">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="29149-145">Убедитесь, что для ключей `enabled` и `automatic` в разделе `packageRestore` задано значение True.</span><span class="sxs-lookup"><span data-stu-id="29149-145">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="29149-146">Обратите внимание, что при изменении параметров `packageRestore` прямо в `nuget.config` нужно перезапустить Visual Studio, чтобы диалоговое окно параметров отображало текущие значения.</span><span class="sxs-lookup"><span data-stu-id="29149-146">Note that if you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="29149-147">Другие потенциальные условия</span><span class="sxs-lookup"><span data-stu-id="29149-147">Other potential conditions</span></span>

- <span data-ttu-id="29149-148">Могут возникнуть ошибки сборки, связанные с отсутствием файлов и указывающие, что для их скачивания следует использовать NuGet restore.</span><span class="sxs-lookup"><span data-stu-id="29149-148">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="29149-149">Но при выполнении команды restore может появиться сообщение "Все пакеты уже установлены, и элементы для восстановления отсутствуют".</span><span class="sxs-lookup"><span data-stu-id="29149-149">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="29149-150">В этом случае удалите папку `packages` (при использовании `packages.config`) или файл `obj/project.assets.json` (при использовании PackageReference) и запустите restore еще раз.</span><span class="sxs-lookup"><span data-stu-id="29149-150">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span>

- <span data-ttu-id="29149-151">При получении проекта из системы управления версиями папки вашего проекта могут быть сделаны доступными только для чтения.</span><span class="sxs-lookup"><span data-stu-id="29149-151">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="29149-152">Измените разрешения для папок и попробуйте восстановить пакеты еще раз.</span><span class="sxs-lookup"><span data-stu-id="29149-152">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="29149-153">Возможно, вы используете старую версию NuGet.</span><span class="sxs-lookup"><span data-stu-id="29149-153">You may be using an old version of NuGet.</span></span> <span data-ttu-id="29149-154">Ознакомьтесь с последними рекомендуемыми версиями на странице [nuget.org/downloads](https://www.nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="29149-154">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="29149-155">Для Visual Studio 2015 рекомендуется версия 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="29149-155">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="29149-156">При возникновении других проблем [сообщите о них на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли получить у вас дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="29149-156">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>