---
title: "Руководство по консоли диспетчера пакетов NuGet | Документы Microsoft"
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
description: "Инструкции по использованию консоли диспетчера пакетов NuGet в Visual Studio для работы с пакетами."
keywords: "Консоль диспетчера пакетов NuGet, powershell NuGet, управлять пакетами NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d9df514c6f92a3ea0841503d86c44271e70f95f2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="package-manager-console"></a>Консоль диспетчера пакетов

Консоль диспетчера пакетов NuGet встроены в Visual Studio в Windows 2012 и более поздних версий. (Это не входят в состав Visual Studio для Mac или кода Visual Studio.)

Консоль дает возможность использовать [команд NuGet PowerShell](../tools/powershell-reference.md) для поиска, установки, удаления и обновить пакеты NuGet. С помощью консоли требуется в случаях, где пользовательский Интерфейс диспетчера пакетов не обеспечивает способ выполнения операции.

Например поиск и установка пакета выполняется с 3 простых шага:

1. Откройте проект или решение в Visual Studio, чтобы открыть консоль, используя **Сервис > Диспетчер пакетов NuGet > консоль диспетчера пакетов** команды.

1. Найти пакет, который вы хотите установить. Если вы уже знаете это, перейдите к шагу 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Выполните команду установки:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

Содержание раздела

- [Открытие консоли](#opening-the-console-and-console-controls)
- [Установка пакета](#installing-a-package)
- [Удаление пакета](#uninstalling-a-package)
- [Поиск пакета](#finding-a-package)
- [Обновление пакета](#updating-a-package)
- [Доступность консоли](#availability-of-the-console)
- [Расширение консоли диспетчера пакетов](#extending-the-package-manager-console)
- [Настройка профиля NuGet PowerShell](#setting-up-a-nuget-powershell-profile)

> [!Important]
> Все операции, которые доступны в консоли можно также с [NuGet CLI](../tools/nuget-exe-cli-reference.md). Однако команды консоли работать в контексте Visual Studio и сохраненное решение или проект и часто выполнять больше, чем их эквивалентные команды CLI. Например установка пакета через консоль добавляет ссылку на проект, тогда как команду CLI не делает. По этой причине разработчики, работающие в Visual Studio обычно используется консоль, чтобы CLI.

> [!Tip]
> Многие операции в консоли зависит от наличия решение открывается в Visual Studio с именем известному пути. Если у вас есть несохраненное решение или ни одно решение, можно увидеть ошибку, «решение не открыто или не сохранено. Убедитесь, что вы уже открыли и сохранили решение.» Это означает, что консоль невозможно определить папку решения. Сохранение несохраненное решение, или создание и сохранение решения в том случае, если у вас нет открыт, необходимо исправить ошибку.

## <a name="opening-the-console-and-console-controls"></a>Открытие консоли и консоли управления

1. Откройте консоль в Visual Studio с помощью **Сервис > Диспетчер пакетов NuGet > консоль диспетчера пакетов** команды. Консоль — это окно Visual Studio, в котором упорядочены и располагается, однако вам нравится (см. [Настройка макетов окон в Visual Studio](https://docs.microsoft.com/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. По умолчанию команды консоли работают от исходного пакета и проекта как набор в элементе управления в верхней части окна:

    ![Консоль диспетчера пакетов управления для источника пакета и проекта](media/PackageManagerConsoleControls1.png)

1. При выборе источника другой пакет или проект изменения этих значений по умолчанию для последующих команд. Переопределен эти параметры, не меняя значений по умолчанию, большинство команд поддержки `-Source` и `-ProjectName` параметры.

1. Чтобы управлять источников пакетов, щелкните значок шестеренки. Ярлык для **Сервис > Параметры > Диспетчер пакетов NuGet > источники пакетов** диалоговое окно «», как описано в статье [пользовательского интерфейса диспетчера пакетов](Package-Manager-UI.md#package-sources) страницы. Кроме того элемент управления справа от проекта селектор очищает содержимое консоли:

    ![Параметры консоли диспетчера пакетов и очистить элементы управления](media/PackageManagerConsoleControls2.png)

1. Самую верхнюю кнопку прерывает долго выполняющуюся команду. Например, на котором работают `Get-Package -ListAvailable -PageSize 500` перечисляет первые 500 пакетов на источник по умолчанию (например nuget.org), которая может занять несколько минут.

    ![Остановка управления консоли диспетчера пакетов](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Установка пакета

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

В разделе [Install-Package](../tools/ps-ref-install-package.md).

Установка пакета выполняет следующие действия:

- Отображает применимые условия лицензионных соглашений в окне консоли с неявные соглашения. Если вы не согласны с условиями, следует удалить пакет немедленно.
- Добавляет ссылку на проект в любой формат ссылки уже используется. В обозревателе решений и в нем применяется ссылка впоследствии отображаются ссылки. Обратите внимание, что с PackageReference, необходимо сохранить проект, чтобы увидеть изменения в файл проекта напрямую.
- Кэширует пакета:
    - PackageReference: пакет кэшируется в `%USERPROFILE%\.nuget\packages` и блокировки файлов, т. е. `project.assets.json` обновляется.
    - `packages.config`: создает `packages` перейдите в папку корень решения и копирует файлы пакетов в подпапку внутри него. `package.config` Обновить файл.
- Обновления `app.config` и/или `web.config` Если пакет использует [источника и конфигурации файла преобразования](../create-packages/source-and-config-file-transformations.md).
- Устанавливает все зависимости, если он уже имеется в проекте. Это обновление версий пакета в процессе, как описано в [разрешении зависимостей](../consume-packages/dependency-resolution.md).
- Отображает файл readme пакета, если он доступен в окне Visual Studio.

> [!Tip]
> Одно из главных преимуществ установки пакетов с `Install-Package` является команды в консоли, добавляет ссылку на проект, как если бы вы использовали пользовательский Интерфейс диспетчера пакетов. Напротив `nuget install` команду CLI загружает пакет и автоматически не добавляются ссылки.

## <a name="uninstalling-a-package"></a>Удаление пакета

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

В разделе [Uninstall-Package](../tools/ps-ref-uninstall-package.md). Используйте [Get-Package](../tools/ps-ref-get-package.md) чтобы видеть все пакеты, установленные в проекте по умолчанию, если требуется найти идентификатор.

При удалении пакет выполняет следующие действия:

- Удаляет ссылки на пакет из проекта (и используется формат ссылки на любые). Ссылки больше не отображаются в обозревателе решений. (Может потребоваться перестроить проект, чтобы увидеть его удалить **Bin** папки.)
- Отменяет все изменения, внесенные в `app.config` или `web.config` во время установки пакета.
- Удаляет ранее установленные зависимости, если нет оставшиеся пакеты используют эти зависимости.

> [!Tip]
> Как `Install-Package`, `Uninstall-Package` команда имеет преимущество управление ссылками в проекте, в отличие от `nuget uninstall` команду CLI.

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

В разделе [Get-Package](../tools/ps-ref-get-package.md) и [пакета обновления](../tools/ps-ref-update-package.md)

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

В разделе [Find-Package](../tools/ps-ref-find-package.md). В Visual Studio 2013 и более ранних версий, используйте [Get-Package](../tools/ps-ref-get-package.md) вместо него.

## <a name="availability-of-the-console"></a>Доступность консоли

В Visual Studio 2017 г NuGet и диспетчер пакетов NuGet устанавливаются автоматически при выборе любого. Рабочие нагрузки, связанные с NET; Можно также установить его по отдельности, проверив **отдельные компоненты > средства кода > Диспетчер пакетов NuGet** в установщике Visual Studio 2017 г.

Кроме того, если диспетчер пакетов NuGet в Visual Studio 2015 и более ранних версий, что отсутствует, проверьте **Сервис > расширения и обновления...**  и выполните поиск расширение диспетчера пакетов NuGet. Если вы не удается использовать установщик расширения в Visual Studio, можно загрузить модуль непосредственно из [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

Консоль диспетчера пакетов недоступна в настоящее время Visual Studio для Mac. Эквивалентные команды, однако доступны через [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio для Mac имеет пользовательский Интерфейс для управления пакетами NuGet. В разделе [пакет NuGet, включая в проекте](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).

Консоль диспетчера пакетов не включено с кодом Visual Studio.

## <a name="extending-the-package-manager-console"></a>Расширение консоли диспетчера пакетов

Некоторые пакеты установки новых команд консоли. Например `MvcScaffolding` создает команды `Scaffold` показано ниже, который приводит к возникновению ошибки ASP.NET MVC контроллеры и представления:

![Установка и использование MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Настройка профиля PowerShell NuGet

Профиль PowerShell позволяет сделать доступными часто используемые команды при любом использовании PowerShell. NuGet поддерживает NuGet отдельный профиль, обычно находятся в следующем расположении:

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Чтобы найти профиль, введите `$profile` в консоли:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Дополнительные сведения см. в [профили Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).
