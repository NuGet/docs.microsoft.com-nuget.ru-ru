---
title: Устранение неполадок с восстановлением пакетов NuGet в Visual Studio
description: Описание распространенных ошибок восстановления NuGet в Visual Studio и способов их устранения.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860624"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="fa14f-103">Устранение ошибок при восстановлении пакетов</span><span class="sxs-lookup"><span data-stu-id="fa14f-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="fa14f-104">Эта статья посвящена распространенным ошибкам, возникающим при восстановлении пакетов, и мерам по их устранению.</span><span class="sxs-lookup"><span data-stu-id="fa14f-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="fa14f-105">Функция восстановления пакетов пытается установить все зависимости пакетов в правильном состоянии с учетом ссылок на пакет в файле проекта ( *.csproj*) или файле *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="fa14f-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="fa14f-106">(В Visual Studio ссылки отображаются в обозревателе решений в узле **Зависимости \ NuGet** или **Ссылки**.) См. о [восстановлении пакетов](../consume-packages/package-restore.md#restore-packages).</span><span class="sxs-lookup"><span data-stu-id="fa14f-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="fa14f-107">Если пакет ссылается на файл проекта( *.csproj*) или если файл *packages.config* неправильный (не соответствует требуемому состоянию после восстановления пакета), необходимо установить или обновить пакеты. Не используйте вместо этого функцию восстановления пакетов.</span><span class="sxs-lookup"><span data-stu-id="fa14f-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="fa14f-108">Если приведенные здесь инструкции не работают, [сообщите о проблеме на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли тщательнее изучить ваш случай.</span><span class="sxs-lookup"><span data-stu-id="fa14f-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="fa14f-109">Не используйте элемент управления "Была ли эта страница полезной?",</span><span class="sxs-lookup"><span data-stu-id="fa14f-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="fa14f-110">который может отображаться на этой странице, так как это не позволяет нам связаться с вами для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="fa14f-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="fa14f-111">Быстрое решение для пользователей Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fa14f-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="fa14f-112">Если вы используете Visual Studio, сначала включите восстановление пакета, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="fa14f-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="fa14f-113">В противном случае перейдите к приведенным далее разделам.</span><span class="sxs-lookup"><span data-stu-id="fa14f-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="fa14f-114">Выберите команду **Сервис > Диспетчер пакетов NuGet > Параметры диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="fa14f-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="fa14f-115">Задайте оба параметра в разделе **Восстановление пакета**.</span><span class="sxs-lookup"><span data-stu-id="fa14f-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="fa14f-116">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fa14f-116">Select **OK**.</span></span>
1. <span data-ttu-id="fa14f-117">Повторите сборку проекта.</span><span class="sxs-lookup"><span data-stu-id="fa14f-117">Build your project again.</span></span>

![Включите восстановление пакетов NuGet в меню "Сервис", "Параметры".](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="fa14f-119">Эти параметры также можно изменить в файле `NuGet.config`; см раздел о [согласии](#consent).</span><span class="sxs-lookup"><span data-stu-id="fa14f-119">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="fa14f-120">Для достаточно ранних проектов, использующих встроенную в MSBuild функцию восстановление пакетов, возможно, потребуется [перейти](package-restore.md#migrate-to-automatic-package-restore-visual-studio) на автоматическое восстановление пакетов.</span><span class="sxs-lookup"><span data-stu-id="fa14f-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="fa14f-121">Данный проект ссылается на пакеты NuGet, отсутствующие на этом компьютере</span><span class="sxs-lookup"><span data-stu-id="fa14f-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="fa14f-122">Полное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="fa14f-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="fa14f-123">Эта ошибка возникает при попытке выполнить сборку проекта, содержащего ссылки на один или несколько пакетов NuGet, которые сейчас не установлены на компьютере или в проекте.</span><span class="sxs-lookup"><span data-stu-id="fa14f-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="fa14f-124">Если используется формат управления [PackageReference](package-references-in-project-files.md), эта ошибка означает, что пакет не установлен в папке *global-packages*, как описано в руководстве по [управлению папкой кэша и глобальных пакетов](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fa14f-124">When using the [PackageReference](package-references-in-project-files.md) management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="fa14f-125">Если используется файл [packages.config](../reference/packages-config.md) эта ошибка означает, что пакет не установлен в папке`packages` в корне решения.</span><span class="sxs-lookup"><span data-stu-id="fa14f-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="fa14f-126">Обычно такая ситуация возникает при получении исходного кода проекта из системы управления версиями или другого скачанного файла.</span><span class="sxs-lookup"><span data-stu-id="fa14f-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="fa14f-127">Пакеты обычно исключаются из системы управления версиями или скачиваемых файлов, так как их можно восстановить из веб-каналов пакета, например nuget.org (см. раздел [Пакеты и система управления версиями](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="fa14f-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="fa14f-128">Их включение приведет к раздуванию репозитория или созданию слишком больших ZIP-файлов.</span><span class="sxs-lookup"><span data-stu-id="fa14f-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="fa14f-129">Эта ошибка также может возникнуть, если файл проекта содержит абсолютные пути для расположений пакетов и вы перемещаете этот проект.</span><span class="sxs-lookup"><span data-stu-id="fa14f-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="fa14f-130">Для восстановления пакетов используйте один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="fa14f-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="fa14f-131">После перемещения файла проекта отредактируйте его напрямую, чтобы обновить ссылки на пакеты.</span><span class="sxs-lookup"><span data-stu-id="fa14f-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="fa14f-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([автоматическое восстановление](package-restore.md#restore-packages-automatically-using-visual-studio) или [восстановление вручную](package-restore.md#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="fa14f-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="fa14f-133">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="fa14f-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="fa14f-134">Интерфейс командной строки nuget.exe</span><span class="sxs-lookup"><span data-stu-id="fa14f-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="fa14f-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="fa14f-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="fa14f-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="fa14f-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="fa14f-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="fa14f-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="fa14f-138">После восстановления пакет должен присутствовать в папке *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="fa14f-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="fa14f-139">В проектах, использующих формат PackageReference, в процессе восстановления повторно создается файл `obj/project.assets.json`, а в проектах, использующих файл `packages.config`, пакет должен появиться в папке `packages`.</span><span class="sxs-lookup"><span data-stu-id="fa14f-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="fa14f-140">Теперь сборка проекта должна пройти без ошибок.</span><span class="sxs-lookup"><span data-stu-id="fa14f-140">The project should now build successfully.</span></span> <span data-ttu-id="fa14f-141">В противном случае [сообщите о проблеме на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли связаться с вами.</span><span class="sxs-lookup"><span data-stu-id="fa14f-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="fa14f-142">Файл ресурсов project.assets.json не найден</span><span class="sxs-lookup"><span data-stu-id="fa14f-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="fa14f-143">Полное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="fa14f-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="fa14f-144">Если используется формат управления PackageReference, который проверяет, установлены ли на компьютере все необходимые пакеты, в файле `project.assets.json` определена схема зависимостей проекта.</span><span class="sxs-lookup"><span data-stu-id="fa14f-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="fa14f-145">Этот файл создается динамически во время восстановления пакета. Поэтому он обычно не добавляется в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="fa14f-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="fa14f-146">В результате эта ошибка возникает при попытке выполнить сборку проекта с помощью такого средства, как `msbuild`, которое не восстанавливает пакеты автоматически.</span><span class="sxs-lookup"><span data-stu-id="fa14f-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="fa14f-147">В этом случае запустите `msbuild -t:restore` и затем `msbuild` или используйте `dotnet build` (при этом пакеты восстанавливаются автоматически).</span><span class="sxs-lookup"><span data-stu-id="fa14f-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="fa14f-148">Кроме того, вы можете использовать любой из методов восстановления пакетов, описанных в [предыдущем разделе](#missing).</span><span class="sxs-lookup"><span data-stu-id="fa14f-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="fa14f-149">Необходимо восстановить один пакет NuGet или несколько, но это не удалось выполнить, так как не было получено согласие</span><span class="sxs-lookup"><span data-stu-id="fa14f-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="fa14f-150">Полное сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="fa14f-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="fa14f-151">Эта ошибка означает, что восстановление пакета отключено в конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa14f-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="fa14f-152">Вы можете изменить подходящие параметры в Visual Studio, как описано выше в разделе [Быстрое решение для пользователей Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="fa14f-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="fa14f-153">Можно также изменить эти параметры напрямую в соответствующем файле `nuget.config` (обычно это `%AppData%\NuGet\NuGet.Config` в Windows и `~/.nuget/NuGet/NuGet.Config` в Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="fa14f-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="fa14f-154">Убедитесь, что для ключей `enabled` и `automatic` в разделе `packageRestore` задано значение True.</span><span class="sxs-lookup"><span data-stu-id="fa14f-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="fa14f-155">При изменении параметров `packageRestore` прямо в `nuget.config` нужно перезапустить Visual Studio, чтобы диалоговое окно параметров отображало текущие значения.</span><span class="sxs-lookup"><span data-stu-id="fa14f-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="fa14f-156">Другие потенциальные условия</span><span class="sxs-lookup"><span data-stu-id="fa14f-156">Other potential conditions</span></span>

- <span data-ttu-id="fa14f-157">Могут возникнуть ошибки сборки, связанные с отсутствием файлов и указывающие, что для их скачивания следует использовать NuGet restore.</span><span class="sxs-lookup"><span data-stu-id="fa14f-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="fa14f-158">Но при выполнении команды restore может появиться сообщение "Все пакеты уже установлены, и элементы для восстановления отсутствуют".</span><span class="sxs-lookup"><span data-stu-id="fa14f-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="fa14f-159">В этом случае удалите папку `packages` (при использовании `packages.config`) или файл `obj/project.assets.json` (при использовании PackageReference) и запустите restore еще раз.</span><span class="sxs-lookup"><span data-stu-id="fa14f-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="fa14f-160">Если это не помогло решить проблему, очистите папку *global-packages* и кэш, выполнив в окне командной строки команду `nuget locals all -clear` или `dotnet locals all --clear`. Дополнительные сведения см. в статье [Управление папкой установки глобальных пакетов, кэшем и временными папками](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fa14f-160">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="fa14f-161">При получении проекта из системы управления версиями папки вашего проекта могут быть сделаны доступными только для чтения.</span><span class="sxs-lookup"><span data-stu-id="fa14f-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="fa14f-162">Измените разрешения для папок и попробуйте восстановить пакеты еще раз.</span><span class="sxs-lookup"><span data-stu-id="fa14f-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="fa14f-163">Возможно, вы используете старую версию NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa14f-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="fa14f-164">Ознакомьтесь с последними рекомендуемыми версиями на странице [nuget.org/downloads](https://www.nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="fa14f-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="fa14f-165">Для Visual Studio 2015 рекомендуется версия 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="fa14f-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="fa14f-166">При возникновении других проблем [сообщите о них на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли получить у вас дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="fa14f-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
