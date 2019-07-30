---
title: Установка пакетов NuGet и управление ими с помощью консоли в Visual Studio
description: Инструкции по использованию консоли диспетчера пакетов NuGet в Visual Studio для работы с пакетами.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 1fb12c6cb9f7702c05990f79a6d43b9dd739e8cc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328071"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Установка пакетов и управление ими с помощью консоли диспетчера пакетов в Visual Studio (PowerShell)

Консоль диспетчера пакетов NuGet позволяет использовать [команды PowerShell NuGet](../reference/powershell-reference.md) для поиска, установки, удаления и обновления пакетов NuGet. Это удобно, когда пользовательский интерфейс диспетчера пакетов не позволяет выполнять операции. См. подробнее об [использовании CLI `nuget.exe` в консоли](#use-the-nugetexe-cli-in-the-console).

Консоль встроена в Visual Studio для Windows. Она не включена в Visual Studio для Mac и Visual Studio Code.

## <a name="find-and-install-a-package"></a>Поиск и установка пакета

Для поиска и установки пакета необходимо выполнить три простых шага:

1. Откройте проект или решение в Visual Studio, а затем откройте консоль, щелкнув **Средства > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.

1. Найдите пакет, который требуется установить. Если вы уже знакомы с этим процессом, перейдите к шагу 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Выполните команду установки:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Все операции, доступные в консоли, также можно выполнить с помощью [CLI NuGet](../reference/nuget-exe-cli-reference.md). Но команды консоли работают в контексте Visual Studio и сохраненного проекта или решения, и область их применения часто шире, чем у их эквивалентов в CLI. Например, при установке пакета с помощью консоли добавляется ссылка на проект, а при использовании команды CLI этого не происходит. По этой причине разработчики, работающие в Visual Studio, обычно предпочитают использовать консоль вместо CLI.

> [!Tip]
> Многие операции консоли зависят от наличия решения, открытого в Visual Studio с использованием известного имени пути. Если у вас нет решения или оно не сохранено, отобразится сообщение об ошибке "Решение не открыто или не сохранено. Убедитесь, что вы открыли и сохранили решение". Это означает, что консоль не может определить папку решения. Эту ошибку можно исправить, сохранив несохраненное решение или создав и сохранив решение, если оно не открыто.

## <a name="opening-the-console-and-console-controls"></a>Открытие консоли и элементов управления консоли

1. Откройте консоль в Visual Studio, щелкнув **Средства > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**. Консоль — это окно Visual Studio, которое может быть упорядочено и размещено по вашему усмотрению (см. руководство по [настройке макетов окон в Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. По умолчанию команды консоли работают с конкретным источником пакета и проектом, как указано в элементе управления в верхней части окна.

    ![Элементы управления консоли диспетчера пакетов для источника пакета и проекта](media/PackageManagerConsoleControls1.png)

1. Выбор другого источника пакета или проекта изменяет эти значения по умолчанию для последующих команд. Чтобы переопределить эти настройки, не меняя значения по умолчанию, большинство команд поддерживают параметры `-Source` и `-ProjectName`.

1. Чтобы управлять источниками пакетов, щелкните значок шестеренки. Это ярлык для диалогового окна **Средства > Параметры > Диспетчер пакетов NuGet > Источники пакетов**, как описано на странице, посвященной [пользовательскому интерфейсу диспетчера пакетов](install-use-packages-visual-studio.md#package-sources). Кроме того, элемент управления справа от средства выбора проектов очищает содержимое консоли.

    ![Параметры консоли диспетчера пакетов и элементы очистки](media/PackageManagerConsoleControls2.png)

1. Крайняя правая кнопка прерывает команду, которая выполняется в течение долгого периода времени. Например, выполнение `Get-Package -ListAvailable -PageSize 500` перечисляет первые 500 пакетов в источнике по умолчанию (например, nuget.org), что может занять несколько минут.

    ![Элемент управления для прерывания выполнения в консоли диспетчера пакетов](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Установка пакета

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

См. подробнее об [Install-Package](../reference/ps-reference/ps-ref-install-package.md).

При установке пакета в консоли выполняются те же действия, которые описаны в руководстве по [установке пакета NuGet](../concepts/package-installation-process.md), со следующими дополнениями:

- Консоль отображает применимые условия лицензии в окне с соответствующим соглашением. Если вы не согласны с условиями, следует сразу же удалить пакет.
- Кроме того, ссылка на пакет добавляется в файл проекта и отображается в **обозревателе решений** в узле **Ссылки**. Сохраните проект, чтобы просмотреть изменения непосредственно в файле проекта.

## <a name="uninstall-a-package"></a>Удаление пакета

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

См. подробнее об [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md). Если необходимо найти идентификатор, чтобы просмотреть все пакеты, установленные в проекте по умолчанию, используйте команду [Get-Package](../reference/ps-reference/ps-ref-get-package.md).

При удалении пакета выполняются следующие действия:

- Удаляются ссылки на пакет из проекта (и любого используемого формата управления). Ссылки больше не отображаются в **обозревателе решений** (возможно, потребуется перестроить проект, чтобы он был удален из папки **Bin**).
- Отменяются все изменения, внесенные в `app.config` или `web.config` при установке пакета.
- Удаляются ранее установленные зависимости, если остальные пакеты не используют эти зависимости.

## <a name="update-a-package"></a>Обновление пакета

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

См. подробнее о [Get-Package](../reference/ps-reference/ps-ref-get-package.md) и [Update-Package](../reference/ps-reference/ps-ref-update-package.md).

## <a name="find-a-package"></a>Поиск пакета

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

См. подробнее о [Find-Package](../reference/ps-reference/ps-ref-find-package.md). В Visual Studio 2013 и более ранних версиях используйте команду [Get-Package](../reference/ps-reference/ps-ref-get-package.md).

## <a name="availability-of-the-console"></a>Доступность консоли

Начиная с Visual Studio 2017, NuGet и диспетчер пакетов NuGet автоматически устанавливаются при выборе рабочей нагрузки, связанной с .NET. Вы также можете установить эти компоненты отдельно, щелкнув **Отдельные компоненты > Средства для работы с кодом > Диспетчер пакетов NuGet** в установщике Visual Studio.

Кроме того, если у вас нет диспетчера пакетов NuGet в Visual Studio 2015 и более ранних версиях, щелкните **Инструменты > Расширения и обновления** и найдите расширение диспетчера пакетов NuGet. Если вы не можете использовать установщик расширений в Visual Studio, скачайте расширение отсюда: [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

Консоль диспетчера пакетов сейчас недоступна в Visual Studio для Mac. Но аналогичные команды доступны через [CLI NuGet](../reference/nuget-exe-CLI-reference.md). В Visual Studio для Mac есть пользовательский интерфейс для управления пакетами NuGet. См. подробнее о [включении пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough).

Консоль диспетчера пакетов не входит в Visual Studio Code.

## <a name="extend-the-package-manager-console"></a>Расширение консоли диспетчера пакетов

Некоторые пакеты устанавливают новые команды для консоли. Например, `MvcScaffolding` создает команды, например команду `Scaffold` (см. ниже), которая, в свою очередь, создает контроллеры и представления ASP.NET MVC.

![Установка и использование MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>Настройка профиля PowerShell NuGet

Профиль PowerShell позволяет сделать часто используемые команды доступными при использовании PowerShell. NuGet поддерживает профиль NuGet, который обычно находится в следующем расположении:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Чтобы найти профиль, в консоли введите `$profile`.

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

См. подробнее о [профилях Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="use-the-nugetexe-cli-in-the-console"></a>Использование CLI nuget.exe в консоли

Чтобы добавить [CLI`nuget.exe`](../reference/nuget-exe-cli-reference.md) в консоль диспетчера пакетов, установите пакет [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) из консоли.

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
