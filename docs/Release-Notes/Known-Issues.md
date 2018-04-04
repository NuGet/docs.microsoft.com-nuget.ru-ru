---
title: Известные проблемы NuGet | Документы Майкрософт
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Известные проблемы в NuGet, в том числе проблемы с проверкой подлинности, установкой пакетов и средствами.
keywords: известные проблемы NuGet, проблемы в NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: c36da5dc73dddbd540a36d171583cbf542e0678f
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="known-issues-with-nuget"></a>Известные проблемы в NuGet

В этом разделе описываются наиболее распространенные известные проблемы в NuGet, о которых сообщается регулярно. Если у вас возникают проблемы с установкой NuGet или управлением пакетами, просмотрите этот перечень проблем и способов их решения.

> [!Note]
> Начиная с версии NuGet 4.0, сведения об известных проблемах включаются в соответствующие заметки о выпуске.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Проблемы с проверкой подлинности веб-каналов NuGet в Visual Studio Team Services с версией nuget.exe 3.4.3

**Проблема:**

При использовании следующей команды для сохранения учетных данных личный маркер доступа зашифровывается дважды:

$PAT = "Личный маркер доступа" $Feed = "URL-адрес" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT

**Решение:**

Сохраняйте пароли в виде обычного текста с помощью параметра [-StorePasswordInClearText](../tools/cli-ref-sources.md).

## <a name="error-installing-packages-with-nuget-34-341"></a>Ошибка при установке пакетов с помощью NuGet версии 3.4 или 3.4.1

**Проблема:**

При использовании надстройки NuGet в NuGet 3.4 и 3.4.1 отсутствуют доступные источники и невозможно добавить новые источники в окне настройки. Ниже представлен пример окна.

![Окно настройки NuGet без источников](./media/knownIssue-34-NoSources.PNG)

Файл `NuGet.Config` в папке `%AppData%\NuGet\` (Windows) или `~/.nuget/` (Mac/Linux) был случайно очищен. Чтобы устранить эту проблему, закройте Visual Studio (в Windows, если возможно), удалите файл `NuGet.Config` и повторите попытку. NuGet создает `NuGet.Config`, и вы можете продолжить работу.

## <a name="error-installing-packages-with-nuget-27"></a>Ошибка при установке пакетов с помощью NuGet 2.7

**Проблема:**

В NuGet 2.7 или более поздней версии при попытке установить пакет, который содержит ссылки на сборки, может появиться сообщение об ошибке **Входная строка имела неверный формат**, как показано ниже.

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

Причина в том, что библиотека типов для COM-компонента `VSLangProj.dll` не зарегистрирована в системе. Это может произойти, например, если у вас одновременно установлены две версии Visual Studio и вы удаляете более раннюю версию. Из-за этого регистрация библиотеки COM может быть случайно отменена.

**Решение:**

Выполните следующую команду из **командной строки с повышенными привилегиями**, чтобы повторно зарегистрировать библиотеку типов для `VSLangProj.dll`:

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Если команда завершается сбоем, проверьте, существует ли файл в этом расположении.

Дополнительные сведения об этой ошибке см. в описании соответствующего [рабочего элемента](https://nuget.codeplex.com/workitem/3609 "Рабочий элемент 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Сбой сборки после обновления пакета в Visual Studio 2012

Проблема: вы используете Visual Studio 2012 RTM. При обновлении пакетов NuGet появляется сообщение "Не удалось полностью удалить один или несколько пакетов" и запрос на перезапуск Visual Studio. После перезапуска Visual Studio возникают странные ошибки сборки.

Причина в том, что некоторые файлы в старых пакетах блокируются фоновым процессом MSBuild. Даже после перезапуска Visual Studio фоновый процесс MSBuild по-прежнему использует файлы из старых пакетов, что приводит к сбоям сборки.

Чтобы устранить эту проблему, установите обновление для Visual Studio 2012, например обновление 2 для Visual Studio 2012.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Обновление более ранней версии NuGet до последней версии приводит к ошибке проверки подписи

Если вы используете Visual Studio 2010 с пакетом обновления 1 (SP1), при попытке обновить более раннюю установленную версию NuGet может появиться следующее сообщение об ошибке:

![Установщик расширений Visual Studio](./media/Visual-Studio-Extension-Installer.png)

В журналах можно найти упоминание исключения `SignatureMismatchException`.

Чтобы эта ошибка не происходила, можно установить [исправление для Visual Studio 2010 с пакетом обновления 1 (SP1)](http://bit.ly/vsixcertfix).
Кроме того, можно просто удалить диспетчер NuGet (когда среда Visual Studio запущена с правами администратора), а затем установить его снова из коллекции расширений Visual Studio.  Дополнительные сведения см. в разделе [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Консоль диспетчера пакетов выдает исключение, если также установлена надстройка Reflector для Visual Studio

При работе с консолью диспетчера пакетов может появиться следующее сообщение об исключении, если установлена надстройка Reflector для Visual Studio:

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

или

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

Мы обратились к автору этой надстройки с просьбой выработать решение.

<p class="info">Обновление: мы протестировали последнюю версию надстройки Reflector (6.5) и убедились в том, что она больше не вызывает этого исключения в консоли.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Сбой при открытии консоли диспетчера пакетов с исключением ObjectSecurity

При попытке открыть консоль диспетчера пакетов могут возникать следующие ошибки:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

В этом случае воспользуйтесь решением, [предложенным в системе StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm).

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Диалоговое окно Add Package Library Reference (Добавление ссылки на библиотеку пакетов) создает исключение, если решение содержит проект InstallShield Limited Edition

Мы обнаружили, что если решение содержит один или несколько проектов InstallShield Limited Edition, при открытии диалогового окна **Добавление ссылки на библиотеку пакетов** возникает исключение. Единственным возможным решением пока является удаление или выгрузка проектов InstallShield.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Кнопка удаления неактивна, так как для установки или удаления NuGet требуются права администратора

Если вы попытаетесь удалить NuGet через диспетчер расширений Visual Studio, то увидите, что кнопка "Удалить" отключена. Для установки и удаления NuGet требуются права администратора. Перезапустите Visual Studio с правами администратора, чтобы удалить расширение. Для использования NuGet права администратора не требуются.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>При открытии консоли диспетчера пакетов в Windows XP происходит аварийное завершение. В чем проблема?

Для NuGet требуется среда выполнения PowerShell 2.0. В Windows XP она по умолчанию отсутствует. Вы можете скачать среду выполнения PowerShell 2.0 по адресу [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929). После ее установки перезапустите Visual Studio, и можно будет открыть консоль диспетчера пакетов.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>При выходе из бета-версии Visual Studio 2010 с пакетом обновления 1 (SP1) происходит аварийное завершение, если открыта консоль диспетчера пакетов.

Если вы установили бета-версию Visual Studio 2010 с пакетом обновления 1 (SP1), то можете заметить, что если оставить консоль диспетчера пакетов открытой и закрыть Visual Studio, произойдет аварийное завершение. Это известная проблема в Visual Studio, которая будет исправлена в выпуске RTM пакета обновления 1 (SP1). Пока вы можете игнорировать этот сбой или удалить бета-версию пакета обновления 1 (SP1), если это возможно.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Возникает исключение "Элемент metadata имеет недопустимый дочерний элемент"

Если вы установили пакеты, сборка которых была выполнена с помощью предварительной версии NuGet, то при использовании версии RTM диспетчера NuGet с этим проектом может появиться следующее сообщение об ошибке: "Элемент metadata в пространстве имен schemas.microsoft.com/packaging/2010/07/nuspec.xsd имеет недопустимый дочерний элемент". Необходимо удалить и повторно установить каждый пакет с помощью версии RTM диспетчера NuGet.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Попытка установки или удаления приводит к ошибке Cannot create a file when that file already exists (Невозможно удалить файл, если этот файл уже существует).

По какой-то причине расширения Visual Studio могут оказаться в необычном состоянии, если вы удалили расширение VSIX, но некоторые файлы остались. Для устранения этой проблемы сделайте следующее.

1. Выйти из Visual Studio
1. Откройте следующую папку (на вашем компьютере она может быть на другом диске):

    C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<версия>\

1. Удалите все файлы с расширением *DELETEME*.
1. Откройте Visual Studio еще раз.

После выполнения этих действий вы сможете продолжить работу.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>Иногда компиляция с включенным анализом кода приводит к ошибкам

Если вы установили FluentNHibernate с консолью диспетчера пакетов и компилируете проект с включенной функцией "Анализ кода", может возникнуть следующая ошибка:

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

По умолчанию для FluentNHibernate требуется версия NHibernate 3.0.0.2001. Однако по умолчанию NuGet устанавливает в проекте библиотеку NHibernate 3.0.0.4000 и добавляет соответствующую переадресацию привязок, чтобы она работала. Если анализ кода отключен, проект будет компилироваться нормально. В отличие от компилятора, средство анализа кода не отслеживает переадресацию привязок и поэтому не использует версию 3.0.0.4000 вместо 3.0.0.2001. Чтобы решить эту проблему, можно установить версию NHibernate 3.0.0.2001 или настроить средство анализа кода так, чтобы его поведение совпадало с поведением компилятора. Для этого выполните указанные ниже действия.

1. Перейдите в папку *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*.
1. Откройте файл FxCopCmd.exe.config и измените значение атрибута `AssemblyReferenceResolveMode` с `StrongName` на `StrongNameIgnoringVersion`.
1. Сохраните изменение и выполните сборку проекта повторно.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Команда Write-Error не работает в скриптах install.ps1, uninstall.ps1 и init.ps1

Это известная проблема. Вместо вызова команды Write-Error попробуйте вызвать throw.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Установка NuGet с ограниченными правами доступа в Windows 2003 может привести к аварийному завершению работы Visual Studio

При попытке установить NuGet с помощью диспетчера расширений Visual Studio, который запущен не от имени администратора, открывается диалоговое окно "Запуск от имени" с установленным по умолчанию флажком "Запустить эту программу с ограниченным доступом".

![Параметр ограниченного доступа в диалоговом окне "Запуск от имени"](./media/RunAsRestricted.png)

Если нажать кнопку "ОК", не снимая этот флажок, произойдет аварийное завершение работы Visual Studio. Перед установкой NuGet обязательно снимите этот флажок.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Не удается удалить Средства NuGet для Windows Phone

Средства Windows Phone не поддерживают диспетчер расширений Visual Studio Extension Manager. Чтобы удалить NuGet, выполните следующую команду.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Изменение регистра символов в идентификаторах пакетов NuGet приводит к неполадкам при восстановлении пакетов

Служба поддержки NuGet может изменить регистр символов в идентификаторах пакетов NuGet, но при восстановлении пакетов это может вызвать сложности у пользователей, в папке *global-packages* которых уже есть пакеты с идентификаторами, имеющими другой регистр символов. Подробное описание можно найти в [этом комментарии на сайте GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932). Мы рекомендуем запрашивать смену регистра, только если у вас есть возможность сообщить существующим пользователям пакета о неполадках, которые могут возникнуть при восстановлении пакетов во время сборки.

## <a name="reporting-issues"></a>Сообщение о проблемах

Чтобы сообщить о проблемах с NuGet, посетите [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).
