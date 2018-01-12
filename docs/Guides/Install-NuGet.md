---
title: "Установка клиентских средств NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Рекомендации по установке клиентских средств, интерфейса командной строки (CLI) и диспетчера пакетов для Visual Studio."
keywords: "интерфейс командной строки nuget.exe, клиентские средства NuGet, диспетчер пакетов NuGet, консоль диспетчера пакетов NuGet, NuGet для Visual Studio, бета-канал NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2f67c298d269149bba9f36ad9e026d5443c39b6a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="7a777-104">Установка клиентских средств NuGet</span><span class="sxs-lookup"><span data-stu-id="7a777-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="7a777-105">**Хотите установить пакет? См. раздел [Краткое руководство. Использование пакета](../Quickstart/Use-a-Package.md).**</span><span class="sxs-lookup"><span data-stu-id="7a777-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="7a777-106">Существует два основных средства для создания, публикации и использования пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="7a777-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="7a777-107">[**NuGet CLI**](#nuget-cli) — это программа командной строки для Windows, которая предоставляет все возможности NuGet. Ее также можно запустить на Mac OSX и Linux с помощью Mono либо интерфейса командной строки .NET Core (`dotnet`).</span><span class="sxs-lookup"><span data-stu-id="7a777-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="7a777-108">[**Диспетчер пакетов NuGet в Visual Studio**](#nuget-package-manager-in-visual-studio) (только Windows) — это средство с графическим интерфейсом для управления пакетами. Оно включает в себя консоль PowerShell, позволяющую использовать некоторые команды NuGet прямо в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a777-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="7a777-109">Пользовательский интерфейс и консоль диспетчера пакетов входят в состав Visual Studio 2012 и более поздних версий (в Windows), а для более ранних версий их можно установить вручную.</span><span class="sxs-lookup"><span data-stu-id="7a777-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="7a777-110">В Visual Studio для Mac функции NuGet встроены напрямую.</span><span class="sxs-lookup"><span data-stu-id="7a777-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="7a777-111">Пошаговое руководство см. в разделе [Включение пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="7a777-111">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="7a777-112">Сейчас Visual Studio Code не имеет встроенной поддержки NuGet.</span><span class="sxs-lookup"><span data-stu-id="7a777-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="7a777-113">Используйте NuGet CLI или [dotnet CLI](../Tools/dotnet-Commands.md).</span><span class="sxs-lookup"><span data-stu-id="7a777-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="7a777-114">Как NuGet CLI, так и диспетчер пакетов поддерживают следующие операции:</span><span class="sxs-lookup"><span data-stu-id="7a777-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="7a777-115">Поиск пакетов</span><span class="sxs-lookup"><span data-stu-id="7a777-115">Search packages</span></span>
- <span data-ttu-id="7a777-116">Установка пакетов</span><span class="sxs-lookup"><span data-stu-id="7a777-116">Install packages</span></span>
- <span data-ttu-id="7a777-117">Обновление пакетов</span><span class="sxs-lookup"><span data-stu-id="7a777-117">Update packages</span></span>
- <span data-ttu-id="7a777-118">Удаление пакетов</span><span class="sxs-lookup"><span data-stu-id="7a777-118">Uninstall packages</span></span>
- <span data-ttu-id="7a777-119">Восстановление пакетов (только в пользовательском интерфейсе диспетчера пакетов)</span><span class="sxs-lookup"><span data-stu-id="7a777-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="7a777-120">Управление источниками NuGet</span><span class="sxs-lookup"><span data-stu-id="7a777-120">Manage NuGet sources</span></span>

<span data-ttu-id="7a777-121">Следующие возможности поддерживаются только в NuGet CLI:</span><span class="sxs-lookup"><span data-stu-id="7a777-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="7a777-122">Управление пакетами (nuget.org или закрытый веб-канал)</span><span class="sxs-lookup"><span data-stu-id="7a777-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="7a777-123">Создание пакетов</span><span class="sxs-lookup"><span data-stu-id="7a777-123">Create packages</span></span> 
- <span data-ttu-id="7a777-124">Публикация пакетов</span><span class="sxs-lookup"><span data-stu-id="7a777-124">Publish packages</span></span>
- <span data-ttu-id="7a777-125">Управление Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="7a777-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="7a777-126">Управление кэшем NuGet</span><span class="sxs-lookup"><span data-stu-id="7a777-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="7a777-127">Репликация пакета</span><span class="sxs-lookup"><span data-stu-id="7a777-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="7a777-128">Другим хорошим средством является автономный [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) с открытым исходным кодом, позволяющий визуально изучать, создавать и изменять пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="7a777-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="7a777-129">Это очень удобно, например, для внесения экспериментальных изменений в структуру пакета без необходимости его перестроения.</span><span class="sxs-lookup"><span data-stu-id="7a777-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="7a777-130">Кроссплатформенная цепочка инструментов [.NET Core CLI](/dotnet/articles/core/tools/index#installation), используемая для разработки приложений .NET Core, поддерживает несколько команд NuGet, таких как delete, locals, push, pack и restore.</span><span class="sxs-lookup"><span data-stu-id="7a777-130">The cross-platform [.NET Core CLI](/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="7a777-131">NuGet CLI</span><span class="sxs-lookup"><span data-stu-id="7a777-131">NuGet CLI</span></span>

<span data-ttu-id="7a777-132">Интерфейс командной строки NuGet предоставляет доступ ко всем возможностям NuGet и может выполняться в Windows, Mac OSX и Linux, как описано в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="7a777-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="7a777-133">Windows</span><span class="sxs-lookup"><span data-stu-id="7a777-133">Windows</span></span>

<span data-ttu-id="7a777-134">**Прямое скачивание:**</span><span class="sxs-lookup"><span data-stu-id="7a777-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="7a777-135">С помощью NuGet 1.4+ вы можете использовать `nuget update -self` для обновления существующего nuget.exe до последней версии.</span><span class="sxs-lookup"><span data-stu-id="7a777-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="7a777-136">**Другие методы:**</span><span class="sxs-lookup"><span data-stu-id="7a777-136">**Other methods:**</span></span>

- <span data-ttu-id="7a777-137">**Chocolatey**: установите пакет Chocolatey [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) с помощью клиента [Chocolatey](http://chocolatey.org).</span><span class="sxs-lookup"><span data-stu-id="7a777-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="7a777-138">**Visual Studio**: установите пакет [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) из консоли диспетчера пакетов в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a777-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="7a777-139">**Для пользователей NuGet 2.x**: в связи с критическими изменениями в NuGet 3.2 [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) указывает на последний стабильный выпуск NuGet 2.x во избежание потенциальных неполадок в системах непрерывной интеграции.</span><span class="sxs-lookup"><span data-stu-id="7a777-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="7a777-140">Mac OSX и Linux</span><span class="sxs-lookup"><span data-stu-id="7a777-140">Mac OSX and Linux</span></span>

<span data-ttu-id="7a777-141">В Mac OSX и Linux запустить NuGet CLI можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="7a777-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="7a777-142">Установите [пакет SDK для .NET Core](https://www.microsoft.com/net/download/core), содержащий основные возможности NuGet.</span><span class="sxs-lookup"><span data-stu-id="7a777-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="7a777-143">Файлы для скачивания также указаны на странице [github.com/dotnet/cli](https://github.com/dotnet/cli).</span><span class="sxs-lookup"><span data-stu-id="7a777-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="7a777-144">Если вам нужны более развернутые возможности, используйте описанный ниже второй вариант использования `nuget.exe` с помощью Mono.</span><span class="sxs-lookup"><span data-stu-id="7a777-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="7a777-145">Установите [Mono](http://www.mono-project.com/docs/getting-started/install/), а затем используйте исполняемый файл командной строки `nuget.exe` для Windows (версии 3.2 и более поздней) из [nuget.org/downloads](https://nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="7a777-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="7a777-146">На запуск NuGet в Mono накладываются следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="7a777-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="7a777-147">Команды, работоспособность которых проверяется:</span><span class="sxs-lookup"><span data-stu-id="7a777-147">Commands tested to work:</span></span>
        - <span data-ttu-id="7a777-148">config</span><span class="sxs-lookup"><span data-stu-id="7a777-148">config</span></span>
        - <span data-ttu-id="7a777-149">удалить</span><span class="sxs-lookup"><span data-stu-id="7a777-149">delete</span></span>
        - <span data-ttu-id="7a777-150">help</span><span class="sxs-lookup"><span data-stu-id="7a777-150">help</span></span>
        - <span data-ttu-id="7a777-151">install</span><span class="sxs-lookup"><span data-stu-id="7a777-151">install</span></span>
        - <span data-ttu-id="7a777-152">списка</span><span class="sxs-lookup"><span data-stu-id="7a777-152">list</span></span>
        - <span data-ttu-id="7a777-153">push</span><span class="sxs-lookup"><span data-stu-id="7a777-153">push</span></span>
        - <span data-ttu-id="7a777-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="7a777-154">setApiKey</span></span>
        - <span data-ttu-id="7a777-155">sources</span><span class="sxs-lookup"><span data-stu-id="7a777-155">sources</span></span>
        - <span data-ttu-id="7a777-156">spec</span><span class="sxs-lookup"><span data-stu-id="7a777-156">spec</span></span>

    - <span data-ttu-id="7a777-157">Частично работающие команды:</span><span class="sxs-lookup"><span data-stu-id="7a777-157">Partially-working commands:</span></span>
        - <span data-ttu-id="7a777-158">pack: работает с файлами `.nuspec`, но не с файлами проекта.</span><span class="sxs-lookup"><span data-stu-id="7a777-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="7a777-159">restore: работает с файлами `packages.config` и `project.json`, но не с файлами решения (`.sln`).</span><span class="sxs-lookup"><span data-stu-id="7a777-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="7a777-160">Неработающие команды:</span><span class="sxs-lookup"><span data-stu-id="7a777-160">Commands that do not work:</span></span>
        - <span data-ttu-id="7a777-161">обновить</span><span class="sxs-lookup"><span data-stu-id="7a777-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="7a777-162">См. также</span><span class="sxs-lookup"><span data-stu-id="7a777-162">Related topics</span></span>

- [<span data-ttu-id="7a777-163">Справочник по интерфейсу командной строки NuGet</span><span class="sxs-lookup"><span data-stu-id="7a777-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="7a777-164">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="7a777-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="7a777-165">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="7a777-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="7a777-166">Диспетчер пакетов NuGet в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a777-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="7a777-167">Диспетчер пакетов NuGet включен во все выпуски Visual Studio 2012 и более поздней версии для Windows.</span><span class="sxs-lookup"><span data-stu-id="7a777-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="7a777-168">Он содержит пользовательский интерфейс диспетчера пакетов ([ссылка](../tools/package-manager-ui.md)) и консоль диспетчера пакетов, через которую осуществляется доступ к средствам, входящим в состав определенных пакетов ([ссылка](../tools/package-manager-console.md)).</span><span class="sxs-lookup"><span data-stu-id="7a777-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="7a777-169">Установщик Visual Studio 2017 содержит диспетчер пакетов NuGet с любой рабочей нагрузкой, использующей .NET.</span><span class="sxs-lookup"><span data-stu-id="7a777-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="7a777-170">Чтобы проверить, установлен ли диспетчер пакетов, или установить его отдельно, запустите установщик Visual Studio 2017 и установите флажок **Отдельные компоненты > Средства для работы с кодом > Диспетчер пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7a777-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="7a777-171">Консоли требуется [PowerShell 2.0](http://support.microsoft.com/kb/968929), который уже установлен в Windows 7 или более поздней версии и Windows Server 2008 R2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7a777-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="7a777-172">Команды консоли диспетчера пакетов работают только в Visual Studio для Windows.</span><span class="sxs-lookup"><span data-stu-id="7a777-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="7a777-173">За пределами этой среды, включая Visual Studio для Mac и Visual Studio Code, используйте NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="7a777-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="7a777-174">Установка диспетчера пакетов для Visual Studio 2010 и более ранних версий</span><span class="sxs-lookup"><span data-stu-id="7a777-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="7a777-175">*Эти действия не требуются для Visual Studio 2012 и более поздних версий, которые уже содержат диспетчер пакетов.*</span><span class="sxs-lookup"><span data-stu-id="7a777-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="7a777-176">В Visual Studio 2010 и более ранних версий выберите **Сервис > Расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="7a777-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="7a777-177">Перейдите к полю **В сети**, выполните поиск фразы "диспетчер пакетов NuGet для Visual Studio" и нажмите кнопку **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="7a777-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="7a777-178">В диалоговом окне установщика нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="7a777-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="7a777-179">После завершения установки перезапустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a777-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="7a777-180">Если вам не удается воспользоваться диалоговым окном **Расширения и обновления** в Visual Studio (например, его блокирует прокси-сервер), вы можете скачать расширения для Visual Studio 2013 и 2015 по адресу [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="7a777-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="7a777-181">Обновление диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="7a777-181">Updating the Package Manager</span></span>

<span data-ttu-id="7a777-182">Для Visual Studio 2015 с обновлением 2 и более поздних версий диспетчер пакетов автоматически обновляется до последнего стабильного выпуска.</span><span class="sxs-lookup"><span data-stu-id="7a777-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="7a777-183">Для Visual Studio 2015 с обновлением 1 и более ранних версий выберите **Сервис > Расширения и обновления** и откройте вкладку **Обновления**, чтобы узнать, доступна ли новая версия диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="7a777-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="7a777-184">Предварительные версии NuGet</span><span class="sxs-lookup"><span data-stu-id="7a777-184">NuGet previews</span></span>

<span data-ttu-id="7a777-185">Если вы хотите заранее оценить предстоящие возможности NuGet, установите предварительную версию [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), которая работает параллельно со стабильными выпусками Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a777-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="7a777-186">Обратите внимание, что предыдущий бета-канал NuGet (`https://dotnet.myget.org/F/nuget-beta/vsix/`) для Visual Studio 2015 больше не используется.</span><span class="sxs-lookup"><span data-stu-id="7a777-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="7a777-187">Чтобы сообщить о проблемах с любым из выпусков NuGet или обменяться идеями, откройте вопрос в [репозитории NuGet GitHub](https://github.com/Nuget/Home).</span><span class="sxs-lookup"><span data-stu-id="7a777-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="7a777-188">См. также</span><span class="sxs-lookup"><span data-stu-id="7a777-188">Related topics</span></span>

- [<span data-ttu-id="7a777-189">Справочник по пользовательскому интерфейсу диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="7a777-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="7a777-190">Справочник по консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="7a777-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="7a777-191">Справочник по PowerShell для консоли диспетчера пакетов</span><span class="sxs-lookup"><span data-stu-id="7a777-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)