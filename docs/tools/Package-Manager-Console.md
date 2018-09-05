---
title: Руководство по консоли диспетчера пакетов NuGet
description: Инструкции по использованию консоли диспетчера пакетов NuGet в Visual Studio для работы с пакетами.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 88979c67ea7f073f2ea5a02c445186642f77f210
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546882"
---
# <a name="package-manager-console"></a>Консоль диспетчера пакетов

Консоль диспетчера пакетов NuGet встроены в Visual Studio в Windows 2012 и более поздних версий. (Это не входит в состав Visual Studio для Mac или Visual Studio Code.)

Консоль позволяет использовать [команд NuGet PowerShell](../tools/powershell-reference.md) для поиска, установка, удаление и обновление пакетов NuGet. С помощью консоли необходим в случаях, когда пользовательский Интерфейс диспетчера пакетов, не позволяют выполнить операцию. Чтобы использовать `nuget.exe` команды в консоли, см. в разделе [с помощью интерфейса командной строки nuget.exe в консоли](#using-the-nugetexe-cli-in-the-console).

Например поиск и установка пакета выполняется с помощью трех простых действий:

1. Откройте проект или решение в Visual Studio и откройте консоль, используя **Сервис > Диспетчер пакетов NuGet > консоль диспетчера пакетов** команды.

1. Найти пакет, который вы хотите установить. Если вы уже знаете это, перейдите к шагу 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Выполните команды установки:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Все операции, которые доступны в консоли может также выполняться с помощью [интерфейса командной строки NuGet](../tools/nuget-exe-cli-reference.md). Тем не менее консольные команды работают в контексте Visual Studio и сохраненные решения или проекта и часто выполнять больше, чем их эквивалентные команды интерфейса командной строки. Например установка пакета через консоль добавляет ссылку в проект не поддерживает команду CLI. По этой причине разработчики, работы в Visual Studio, обычно предпочитают использовать консоль для интерфейса командной строки.

> [!Tip]
> Многие операции консоли зависит от наличия открыт в Visual Studio с использованием известных пути решения. Если у вас есть несохраненное решение или решение отсутствует, может появится сообщение об ошибке, «решение не открывается или не сохраняется. Убедитесь, что у вас есть решение открытым и сохраняется.» Это означает, что консоль не может определить папку решения. Сохранение несохраненное решение, или создать и сохранить решение, если у вас его открыть, следует исправить эту ошибку.

## <a name="opening-the-console-and-console-controls"></a>Открытие консоли и консоли управления

1. Откройте консоль в Visual Studio с помощью **Сервис > Диспетчер пакетов NuGet > консоль диспетчера пакетов** команды. Консоль — это окно Visual Studio, в котором могут быть упорядочены и расположение, своему усмотрению (см. в разделе [Настройка макетов окон в Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. По умолчанию команды консоли работают от источника пакета и проекта задаваемое в элементе управления в верхней части окна:

    ![Элементы управления консоли диспетчера пакетов для источника пакета и проекта](media/PackageManagerConsoleControls1.png)

1. При выборе другой пакет источника или проекта меняется эти значения по умолчанию для последующих команд. Чтобы переопределен с помощью этих параметров, не изменяя значения по умолчанию, большинство команд поддерживают `-Source` и `-ProjectName` параметры.

1. Чтобы управлять источники пакетов, щелкните значок шестеренки. Это ярлык для **Сервис > Параметры > Диспетчер пакетов NuGet > источники пакетов** диалоговое окно, как описано в разделе [пользовательский Интерфейс диспетчера пакетов](package-manager-ui.md#package-sources) страницы. Кроме того элемент управления справа от Выбор проекта очищает содержимое консоли:

    ![Параметры консоли диспетчера пакетов и очистить элементы управления](media/PackageManagerConsoleControls2.png)

1. Самую верхнюю кнопку прерывает долго выполняющуюся команду. Например, на котором работают `Get-Package -ListAvailable -PageSize 500` перечислены первые 500 пакетов на источник по умолчанию (например, nuget.org), которая может занять несколько минут.

    ![Остановка управления консоли диспетчера пакетов](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Установка пакета

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

См. в разделе [Install-Package](../tools/ps-ref-install-package.md).

Установка пакета в консоли выполняет те же действия, как описано в разделе [что происходит при установке пакета](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), со следующими дополнениями:

- В консоли отображаются применимых условиях лицензии в своем окне неявные соглашения. Если вы не согласны с условиями, следует удалить пакет немедленно.
- Также добавляется к файлу проекта ссылку на пакет и отображается в **обозревателе решений** под **ссылки** узла, необходимо сохранить проект, чтобы увидеть изменения в файл проекта напрямую.

## <a name="uninstalling-a-package"></a>Удаление пакета

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

См. в разделе [Uninstall-Package](../tools/ps-ref-uninstall-package.md). Используйте [Get-Package](../tools/ps-ref-get-package.md) чтобы видеть все пакеты, установленные в проекте по умолчанию, если вам нужно найти идентификатор.

Удаление пакета выполняет следующие действия:

- Удаляет ссылки на пакет из проекта (и любого привычного формата управления он используется). Ссылки, больше не отображаются в **обозревателе решений**. (Может потребоваться перестроить проект, чтобы просмотреть его удалить **Bin** папки.)
- Отменяет все изменения, внесенные в `app.config` или `web.config` во время установки пакета.
- Удаляет ранее установленные зависимостей, если нет оставшиеся пакеты используют эти зависимости.

## <a name="updating-a-package"></a>Обновление пакета

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

См. в разделе [Get-Package](../tools/ps-ref-get-package.md) и [Update-Package](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>Поиск пакета

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

См. в разделе [Find-Package](../tools/ps-ref-find-package.md). В Visual Studio 2013 и более ранних версий, используйте [Get-Package](../tools/ps-ref-get-package.md) вместо этого.

## <a name="availability-of-the-console"></a>Доступность консоли

В Visual Studio 2017 NuGet и диспетчер пакетов NuGet автоматически устанавливаются при выборе любого. Рабочим нагрузкам, связанным с NET; Можно также установить его по отдельности, установив **отдельные компоненты > средства кода > Диспетчер пакетов NuGet** флажок в установщике Visual Studio 2017.

Кроме того, если вы пропустили диспетчер пакетов NuGet в Visual Studio 2015 и более ранних версий, проверьте **Сервис > расширения и обновления...**  и выполните поиск расширение диспетчера пакетов NuGet. Если вы не удается использовать установщик расширений в Visual Studio, можно загрузить модуль непосредственно из [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

Консоль диспетчера пакетов недоступен в настоящее время с помощью Visual Studio для Mac. Эквивалентные команды, тем не менее, доступны через [интерфейса командной строки NuGet](nuget-exe-CLI-reference.md). Visual Studio для Mac имеют пользовательский Интерфейс для управления пакетами NuGet. См. в разделе [Включение пакета NuGet в проекте](/visualstudio/mac/nuget-walkthrough).

Консоль диспетчера пакетов не входит в состав Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Расширение консоли диспетчера пакетов

Некоторые пакеты устанавливают новые команды для консоли. Например `MvcScaffolding` создает команд, таких как `Scaffold` показано ниже, служащего для контроллеров и представлений ASP.NET MVC:

![Установка и использование MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Настройка профиля NuGet PowerShell

Профиль PowerShell позволяет сделать доступными часто используемые команды при любом использовании PowerShell. NuGet поддерживает NuGet отдельный профиль, как правило, находятся в следующем расположении:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Чтобы найти профиль, введите `$profile` в консоли:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Дополнительные сведения см. в [профили Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Используя интерфейс командной строки nuget.exe в консоли

Чтобы сделать [ `nuget.exe` CLI](nuget-exe-cli-reference.md) доступны в консоли диспетчера пакетов, установите [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) пакета из консоли:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
