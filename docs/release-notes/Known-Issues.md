---
title: Известные проблемы
description: Известные проблемы в NuGet, в том числе проблемы с проверкой подлинности, установкой пакетов и средствами.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f170f377a3394694e953a794f2c814388656c21
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822023"
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="c1660-103">Известные проблемы в NuGet</span><span class="sxs-lookup"><span data-stu-id="c1660-103">Known Issues with NuGet</span></span>

<span data-ttu-id="c1660-104">В этом разделе описываются наиболее распространенные известные проблемы в NuGet, о которых сообщается регулярно.</span><span class="sxs-lookup"><span data-stu-id="c1660-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="c1660-105">Если у вас возникают проблемы с установкой NuGet или управлением пакетами, просмотрите этот перечень проблем и способов их решения.</span><span class="sxs-lookup"><span data-stu-id="c1660-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="c1660-106">Начиная с версии NuGet 4.0, сведения об известных проблемах включаются в соответствующие заметки о выпуске.</span><span class="sxs-lookup"><span data-stu-id="c1660-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="c1660-107">Проблемы с проверкой подлинности веб-каналов NuGet в Visual Studio Team Services с версией nuget.exe 3.4.3</span><span class="sxs-lookup"><span data-stu-id="c1660-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="c1660-108">**Проблема:**</span><span class="sxs-lookup"><span data-stu-id="c1660-108">**Problem:**</span></span>

<span data-ttu-id="c1660-109">При использовании следующей команды для сохранения учетных данных личный маркер доступа зашифровывается дважды:</span><span class="sxs-lookup"><span data-stu-id="c1660-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="c1660-110">$PAT = "Личный маркер доступа" $Feed = "URL-адрес" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span><span class="sxs-lookup"><span data-stu-id="c1660-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="c1660-111">**Решение:**</span><span class="sxs-lookup"><span data-stu-id="c1660-111">**Workaround:**</span></span>

<span data-ttu-id="c1660-112">Сохраняйте пароли в виде обычного текста с помощью параметра [-StorePasswordInClearText](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="c1660-112">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="c1660-113">Ошибка при установке пакетов с помощью NuGet версии 3.4 или 3.4.1</span><span class="sxs-lookup"><span data-stu-id="c1660-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="c1660-114">**Проблема:**</span><span class="sxs-lookup"><span data-stu-id="c1660-114">**Problem:**</span></span>

<span data-ttu-id="c1660-115">При использовании надстройки NuGet в NuGet 3.4 и 3.4.1 отсутствуют доступные источники и невозможно добавить новые источники в окне настройки.</span><span class="sxs-lookup"><span data-stu-id="c1660-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="c1660-116">Ниже представлен пример окна.</span><span class="sxs-lookup"><span data-stu-id="c1660-116">The result is similar to the image below:</span></span>

![Окно настройки NuGet без источников](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="c1660-118">Файл `NuGet.Config` в папке `%AppData%\NuGet\` (Windows) или `~/.nuget/` (Mac/Linux) был случайно очищен.</span><span class="sxs-lookup"><span data-stu-id="c1660-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="c1660-119">Чтобы устранить эту проблему, закройте Visual Studio (в Windows, если возможно), удалите файл `NuGet.Config` и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="c1660-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="c1660-120">NuGet создает `NuGet.Config`, и вы можете продолжить работу.</span><span class="sxs-lookup"><span data-stu-id="c1660-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="c1660-121">Ошибка при установке пакетов с помощью NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="c1660-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="c1660-122">**Проблема:**</span><span class="sxs-lookup"><span data-stu-id="c1660-122">**Problem:**</span></span>

<span data-ttu-id="c1660-123">В NuGet 2.7 или более поздней версии при попытке установить пакет, который содержит ссылки на сборки, может появиться сообщение об ошибке **Входная строка имела неверный формат**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c1660-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```

<span data-ttu-id="c1660-124">Причина в том, что библиотека типов для COM-компонента `VSLangProj.dll` не зарегистрирована в системе.</span><span class="sxs-lookup"><span data-stu-id="c1660-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="c1660-125">Это может произойти, например, если у вас одновременно установлены две версии Visual Studio и вы удаляете более раннюю версию.</span><span class="sxs-lookup"><span data-stu-id="c1660-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="c1660-126">Из-за этого регистрация библиотеки COM может быть случайно отменена.</span><span class="sxs-lookup"><span data-stu-id="c1660-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="c1660-127">**Решение:**</span><span class="sxs-lookup"><span data-stu-id="c1660-127">**Solution:**:</span></span>

<span data-ttu-id="c1660-128">Выполните следующую команду из **командной строки с повышенными привилегиями**, чтобы повторно зарегистрировать библиотеку типов для `VSLangProj.dll`:</span><span class="sxs-lookup"><span data-stu-id="c1660-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="c1660-129">Если команда завершается сбоем, проверьте, существует ли файл в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="c1660-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="c1660-130">Дополнительные сведения об этой ошибке см. в описании соответствующего [рабочего элемента](https://nuget.codeplex.com/workitem/3609 "Рабочий элемент 3609").</span><span class="sxs-lookup"><span data-stu-id="c1660-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="c1660-131">Сбой сборки после обновления пакета в Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="c1660-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="c1660-132">Проблема: вы используете Visual Studio 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="c1660-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="c1660-133">При обновлении пакетов NuGet появляется сообщение "Не удалось полностью удалить один или несколько пакетов"</span><span class="sxs-lookup"><span data-stu-id="c1660-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="c1660-134">и запрос на перезапуск Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c1660-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="c1660-135">После перезапуска Visual Studio возникают странные ошибки сборки.</span><span class="sxs-lookup"><span data-stu-id="c1660-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="c1660-136">Причина в том, что некоторые файлы в старых пакетах блокируются фоновым процессом MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c1660-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="c1660-137">Даже после перезапуска Visual Studio фоновый процесс MSBuild по-прежнему использует файлы из старых пакетов, что приводит к сбоям сборки.</span><span class="sxs-lookup"><span data-stu-id="c1660-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="c1660-138">Чтобы устранить эту проблему, установите обновление для Visual Studio 2012, например обновление 2 для Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="c1660-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="c1660-139">Обновление более ранней версии NuGet до последней версии приводит к ошибке проверки подписи</span><span class="sxs-lookup"><span data-stu-id="c1660-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="c1660-140">Если вы используете Visual Studio 2010 с пакетом обновления 1 (SP1), при попытке обновить более раннюю установленную версию NuGet может появиться следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="c1660-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Установщик расширений Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="c1660-142">В журналах можно найти упоминание исключения `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="c1660-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="c1660-143">Чтобы эта ошибка не происходила, можно установить [исправление для Visual Studio 2010 с пакетом обновления 1 (SP1)](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="c1660-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="c1660-144">Кроме того, можно просто удалить диспетчер NuGet (когда среда Visual Studio запущена с правами администратора), а затем установить его снова из коллекции расширений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c1660-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="c1660-145">Дополнительные сведения см. в разделе [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="c1660-145">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="c1660-146">Консоль диспетчера пакетов выдает исключение, если также установлена надстройка Reflector для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c1660-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="c1660-147">При работе с консолью диспетчера пакетов может появиться следующее сообщение об исключении, если установлена надстройка Reflector для Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c1660-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="c1660-148">или</span><span class="sxs-lookup"><span data-stu-id="c1660-148">or</span></span>

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

<span data-ttu-id="c1660-149">Мы обратились к автору этой надстройки с просьбой выработать решение.</span><span class="sxs-lookup"><span data-stu-id="c1660-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="c1660-150">Обновление: мы протестировали последнюю версию надстройки Reflector (6.5) и убедились в том, что она больше не вызывает этого исключения в консоли.</span><span class="sxs-lookup"><span data-stu-id="c1660-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="c1660-151">Сбой при открытии консоли диспетчера пакетов с исключением ObjectSecurity</span><span class="sxs-lookup"><span data-stu-id="c1660-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="c1660-152">При попытке открыть консоль диспетчера пакетов могут возникать следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="c1660-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="c1660-153">В этом случае воспользуйтесь решением, [предложенным в системе StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm).</span><span class="sxs-lookup"><span data-stu-id="c1660-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="c1660-154">Диалоговое окно Add Package Library Reference (Добавление ссылки на библиотеку пакетов) создает исключение, если решение содержит проект InstallShield Limited Edition</span><span class="sxs-lookup"><span data-stu-id="c1660-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="c1660-155">Мы обнаружили, что если решение содержит один или несколько проектов InstallShield Limited Edition, при открытии диалогового окна **Добавление ссылки на библиотеку пакетов** возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="c1660-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="c1660-156">Единственным возможным решением пока является удаление или выгрузка проектов InstallShield.</span><span class="sxs-lookup"><span data-stu-id="c1660-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="c1660-157">Кнопка удаления неактивна,</span><span class="sxs-lookup"><span data-stu-id="c1660-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="c1660-158">так как для установки или удаления NuGet требуются права администратора</span><span class="sxs-lookup"><span data-stu-id="c1660-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="c1660-159">Если вы попытаетесь удалить NuGet через диспетчер расширений Visual Studio, то увидите, что кнопка "Удалить" отключена.</span><span class="sxs-lookup"><span data-stu-id="c1660-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="c1660-160">Для установки и удаления NuGet требуются права администратора.</span><span class="sxs-lookup"><span data-stu-id="c1660-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="c1660-161">Перезапустите Visual Studio с правами администратора, чтобы удалить расширение.</span><span class="sxs-lookup"><span data-stu-id="c1660-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="c1660-162">Для использования NuGet права администратора не требуются.</span><span class="sxs-lookup"><span data-stu-id="c1660-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="c1660-163">При открытии консоли диспетчера пакетов в Windows XP происходит аварийное завершение.</span><span class="sxs-lookup"><span data-stu-id="c1660-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="c1660-164">В чем проблема?</span><span class="sxs-lookup"><span data-stu-id="c1660-164">What's wrong?</span></span>

<span data-ttu-id="c1660-165">Для NuGet требуется среда выполнения PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="c1660-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="c1660-166">В Windows XP она по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="c1660-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="c1660-167">Вы можете скачать среду выполнения PowerShell 2.0 по адресу [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="c1660-167">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="c1660-168">После ее установки перезапустите Visual Studio, и можно будет открыть консоль диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="c1660-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="c1660-169">При выходе из бета-версии Visual Studio 2010 с пакетом обновления 1 (SP1) происходит аварийное завершение, если открыта консоль диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="c1660-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="c1660-170">Если вы установили бета-версию Visual Studio 2010 с пакетом обновления 1 (SP1), то можете заметить, что если оставить консоль диспетчера пакетов открытой и закрыть Visual Studio, произойдет аварийное завершение.</span><span class="sxs-lookup"><span data-stu-id="c1660-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="c1660-171">Это известная проблема в Visual Studio, которая будет исправлена в выпуске RTM пакета обновления 1 (SP1).</span><span class="sxs-lookup"><span data-stu-id="c1660-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="c1660-172">Пока вы можете игнорировать этот сбой или удалить бета-версию пакета обновления 1 (SP1), если это возможно.</span><span class="sxs-lookup"><span data-stu-id="c1660-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="c1660-173">Возникает исключение "Элемент metadata имеет недопустимый дочерний элемент"</span><span class="sxs-lookup"><span data-stu-id="c1660-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="c1660-174">Если вы установили пакеты, сборка которых была выполнена с помощью предварительной версии NuGet, то при использовании версии RTM диспетчера NuGet с этим проектом может появиться следующее сообщение об ошибке: "Элемент metadata в пространстве имен schemas.microsoft.com/packaging/2010/07/nuspec.xsd имеет недопустимый дочерний элемент".</span><span class="sxs-lookup"><span data-stu-id="c1660-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="c1660-175">Необходимо удалить и повторно установить каждый пакет с помощью версии RTM диспетчера NuGet.</span><span class="sxs-lookup"><span data-stu-id="c1660-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="c1660-176">Попытка установки или удаления приводит к ошибке Cannot create a file when that file already exists (Невозможно удалить файл, если этот файл уже существует).</span><span class="sxs-lookup"><span data-stu-id="c1660-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="c1660-177">По какой-то причине расширения Visual Studio могут оказаться в необычном состоянии, если вы удалили расширение VSIX, но некоторые файлы остались.</span><span class="sxs-lookup"><span data-stu-id="c1660-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="c1660-178">Для устранения этой проблемы сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="c1660-178">To work around this issue:</span></span>

1. <span data-ttu-id="c1660-179">Выйти из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c1660-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="c1660-180">Откройте следующую папку (на вашем компьютере она может быть на другом диске):</span><span class="sxs-lookup"><span data-stu-id="c1660-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="c1660-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<версия>\\</span><span class="sxs-lookup"><span data-stu-id="c1660-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="c1660-182">Удалите все файлы с расширением *DELETEME*.</span><span class="sxs-lookup"><span data-stu-id="c1660-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="c1660-183">Откройте Visual Studio еще раз.</span><span class="sxs-lookup"><span data-stu-id="c1660-183">Re-open Visual Studio</span></span>

<span data-ttu-id="c1660-184">После выполнения этих действий вы сможете продолжить работу.</span><span class="sxs-lookup"><span data-stu-id="c1660-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="c1660-185">Иногда компиляция с включенным анализом кода приводит к ошибкам</span><span class="sxs-lookup"><span data-stu-id="c1660-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="c1660-186">Если вы установили FluentNHibernate с консолью диспетчера пакетов и компилируете проект с включенной функцией "Анализ кода", может возникнуть следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="c1660-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="c1660-187">По умолчанию для FluentNHibernate требуется версия NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="c1660-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="c1660-188">Однако по умолчанию NuGet устанавливает в проекте библиотеку NHibernate 3.0.0.4000 и добавляет соответствующую переадресацию привязок, чтобы она работала.</span><span class="sxs-lookup"><span data-stu-id="c1660-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="c1660-189">Если анализ кода отключен, проект будет компилироваться нормально.</span><span class="sxs-lookup"><span data-stu-id="c1660-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="c1660-190">В отличие от компилятора, средство анализа кода не отслеживает переадресацию привязок и поэтому не использует версию 3.0.0.4000 вместо 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="c1660-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="c1660-191">Чтобы решить эту проблему, можно установить версию NHibernate 3.0.0.2001 или настроить средство анализа кода так, чтобы его поведение совпадало с поведением компилятора. Для этого выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="c1660-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="c1660-192">Перейдите в папку *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*.</span><span class="sxs-lookup"><span data-stu-id="c1660-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="c1660-193">Откройте файл FxCopCmd.exe.config и измените значение атрибута `AssemblyReferenceResolveMode` с `StrongName` на `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="c1660-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="c1660-194">Сохраните изменение и выполните сборку проекта повторно.</span><span class="sxs-lookup"><span data-stu-id="c1660-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="c1660-195">Команда Write-Error не работает в скриптах install.ps1, uninstall.ps1 и init.ps1</span><span class="sxs-lookup"><span data-stu-id="c1660-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="c1660-196">Это известная проблема.</span><span class="sxs-lookup"><span data-stu-id="c1660-196">This is a known issue.</span></span> <span data-ttu-id="c1660-197">Вместо вызова команды Write-Error попробуйте вызвать throw.</span><span class="sxs-lookup"><span data-stu-id="c1660-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="c1660-198">Установка NuGet с ограниченными правами доступа в Windows 2003 может привести к аварийному завершению работы Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c1660-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="c1660-199">При попытке установить NuGet с помощью диспетчера расширений Visual Studio, который запущен не от имени администратора, открывается диалоговое окно "Запуск от имени" с установленным по умолчанию флажком "Запустить эту программу с ограниченным доступом".</span><span class="sxs-lookup"><span data-stu-id="c1660-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Параметр ограниченного доступа в диалоговом окне "Запуск от имени"](./media/RunAsRestricted.png)

<span data-ttu-id="c1660-201">Если нажать кнопку "ОК", не снимая этот флажок, произойдет аварийное завершение работы Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c1660-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="c1660-202">Перед установкой NuGet обязательно снимите этот флажок.</span><span class="sxs-lookup"><span data-stu-id="c1660-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="c1660-203">Не удается удалить Средства NuGet для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="c1660-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="c1660-204">Средства Windows Phone не поддерживают диспетчер расширений Visual Studio Extension Manager.</span><span class="sxs-lookup"><span data-stu-id="c1660-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="c1660-205">Чтобы удалить NuGet, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c1660-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="c1660-206">Изменение регистра символов в идентификаторах пакетов NuGet приводит к неполадкам при восстановлении пакетов</span><span class="sxs-lookup"><span data-stu-id="c1660-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="c1660-207">Служба поддержки NuGet может изменить регистр символов в идентификаторах пакетов NuGet, но при восстановлении пакетов это может вызвать сложности у пользователей, в папке *global-packages* которых уже есть пакеты с идентификаторами, имеющими другой регистр символов. Подробное описание можно найти в [этом комментарии на сайте GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932).</span><span class="sxs-lookup"><span data-stu-id="c1660-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="c1660-208">Мы рекомендуем запрашивать смену регистра, только если у вас есть возможность сообщить существующим пользователям пакета о неполадках, которые могут возникнуть при восстановлении пакетов во время сборки.</span><span class="sxs-lookup"><span data-stu-id="c1660-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="c1660-209">Сообщение о проблемах</span><span class="sxs-lookup"><span data-stu-id="c1660-209">Reporting issues</span></span>

<span data-ttu-id="c1660-210">Чтобы сообщить о проблемах с NuGet, посетите [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="c1660-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
