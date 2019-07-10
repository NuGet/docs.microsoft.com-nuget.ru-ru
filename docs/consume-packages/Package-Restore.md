---
title: Восстановление пакета NuGet
description: Описание того, как NuGet восстанавливает пакеты, от которых зависит проект, включая отключение восстановления и ограничения версий.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 3b64c035886818496339fe1bdd8f9abce060278a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467794"
---
# <a name="package-restore"></a>Восстановление пакетов

Чтобы очистить среду разработки и уменьшить размер репозитория, **функция восстановления пакетов** NuGet устанавливает все зависимости проекта, указанные в файле проекта или файле `packages.config`. В версиях .NET Core 2.0 и более поздних команды `dotnet build` и `dotnet run` выполняют автоматическое восстановление пакетов. Visual Studio может автоматически восстанавливать пакеты при сборке проекта. Кроме того, вы можете в любой момент самостоятельно восстановить пакеты с помощью Visual Studio, `nuget restore`, `dotnet restore`, а также xbuild в Mono.

Восстановление пакетов гарантирует доступность всех зависимостей проекта без сохранения этих пакетов в системе управления версиями. Дополнительные сведения о настройке исключения двоичных файлов пакетов в репозитории системы управления версиями см. в статье [Пакеты и система управления версиями](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Обзор восстановления пакетов

Функция восстановления пакетов сначала устанавливает необходимые прямые зависимости проекта, а затем остальные зависимости этих пакетов во всей схеме зависимостей.

Если пакет не установлен, NuGet сначала попытается извлечь его из [кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md). Если пакет отсутствует в кэше, NuGet пытается скачать его из всех источников, которые включены в списке в разделе **Средства** > **Параметры** > **Диспетчер пакетов NuGet** > **Источники пакетов** в Visual Studio. Во время восстановления NuGet игнорирует порядок источников пакетов, используя пакет из любого источника, первым ответившего на запросы. Дополнительные сведения о поведении NuGet см. в статье [Распространенные конфигурации NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet не сообщает о сбое восстановления пакета до проверки всех источников. После проверки NuGet сообщает о сбое только для последнего источника в списке. Такая ошибка означает, что пакет отсутствовал и во *всех* других источниках, хотя отдельные ошибки для них не выдавались.

Включить функцию восстановления пакетов можно следующими способами:

- **CLI dotnet**: С помощью команды [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) вы можете восстановить пакеты, включенные в файл проекта с [PackageReference](../consume-packages/package-references-in-project-files.md). При использовании .NET Core версии 2.0 и более поздней автоматическое восстановление доступно с помощью команд `dotnet build` и `dotnet run`.  

- **Диспетчер пакетов**: В Visual Studio в Windows восстановление пакетов осуществляется автоматически при создании проекта на основе шаблона или во время сборки проекта. При этом учитываются значения параметров, представленных в разделе [Включение и отключение восстановления пакетов](#enable-and-disable-package-restore). В NuGet 4.0 и более поздних версий также доступно автоматическое восстановление при изменении проекта на основе пакета SDK для .NET Core.

    Чтобы восстановить пакеты вручную, щелкните правой кнопкой мыши решение в **обозревателе решений** и выберите **Восстановить пакеты NuGet**. Если какие-либо пакеты по-прежнему установлены некорректно, в **обозревателе решений** отображается значок ошибки. Щелкните правой кнопкой мыши и выберите **Управление пакетами NuGet**, после чего удалите и переустановите затронутые пакеты с помощью **диспетчера пакетов**. Дополнительные сведения см. в статье [Переустановка и обновление пакетов](../consume-packages/reinstalling-and-updating-packages.md)

    Если отображается ошибка "Данный проект ссылается на пакеты NuGet, отсутствующие на этом компьютере" или "Необходимо восстановить один или несколько пакетов NuGet, однако это невозможно без вашего согласия", [включите автоматическое восстановление](#enable-and-disable-package-restore). Дополнительные сведения см. в статье [Устранение ошибок при восстановлении пакетов](Package-restore-troubleshooting.md).

- **Интерфейс командной строки nuget.exe**: Выполните команду [nuget restore](../tools/cli-ref-restore.md), которая позволяет восстановить пакеты, указанные в файле проекта или решения, либо в файле `packages.config`. 

- **MSBuild**: С помощью команды [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) вы можете восстановить пакеты, включенные в файл проекта с PackageReference. Эта команда доступна только в NuGet версии 4.x и более поздних и MSBuild версии 15.1 и более поздних, включенных в Visual Studio 2017 и более поздних версий. `nuget restore` и `dotnet restore` используют эту команду для подходящих проектов.

- **Azure Pipelines**: При создании определения сборки в Azure Pipelines включите в него задачу восстановления [NuGet](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) или [.NET Core](/azure/devops/pipelines/tasks/build/dotnet-core#restore-nuget-packages), а затем добавьте задачу сборки. В некоторые шаблоны сборки задача восстановления включена по умолчанию.

- **Azure DevOps Server**: В Azure DevOps Server и TFS 2013 и более поздних версий пакеты восстанавливаются автоматически во время сборки при условии, что вы используете шаблон командной сборки для TFS 2013 или более поздней версии. В более ранних версиях TFS вы можете включить в процесс сборки этап, на котором будет выполняться команда восстановления из командной строки, а также при необходимости перенести шаблон сборки в более позднюю версию. Дополнительные сведения см. в статье [Настройка восстановления пакетов с помощью сборки Team Foundation](../consume-packages/team-foundation-build.md).

## <a name="enable-and-disable-package-restore"></a>Включение и отключение восстановления пакетов

В Visual Studio для управления восстановлением пакетов используются преимущественно параметры в разделе **Средства** > **Параметры** > **Диспетчер пакетов NuGet**:

![Управление восстановлением пакетов с помощью параметров диспетчера пакетов NuGet](media/Restore-01-AutoRestoreOptions.png)

- Параметр **Разрешить NuGet скачивать отсутствующие пакеты** определяет все формы восстановления пакетов посредством изменения параметра `packageRestore/enabled` в [разделе packageRestore](../reference/nuget-config-file.md#packagerestore-section) файла `NuGet.Config` в каталоге `%AppData%\NuGet\` в Windows или `~/.nuget/NuGet/` в Mac/Linux. Этот параметр также обеспечивает работу команды **Восстановить пакеты NuGet** в контекстном меню решения в Visual Studio.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > Параметр `packageRestore/enabled` можно переопределить на глобальном уровне, задав для переменной среды с именем **EnableNuGetPackageRestore** значение True или False перед запуском Visual Studio или началом сборки.

- Параметр **Автоматически проверять отсутствие пакетов при сборке в Visual Studio** управляет автоматическим восстановлением путем изменения параметра `packageRestore/automatic` в [разделе packageRestore](../reference/nuget-config-file.md#packagerestore-section) файла `NuGet.Config`. Когда этот параметр имеет значение True, при запуске сборки из Visual Studio все отсутствующие пакеты восстанавливаются автоматически. Этот параметр не влияет на сборки, выполняемые из командной строки MSBuild.

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

Чтобы включить или отключить восстановление пакетов для всех пользователей на компьютере, разработчик или компания могут добавить параметры конфигурации в глобальный файл `nuget.config`. Глобальный файл `nuget.config` в Windows находится в каталоге `%ProgramData%\NuGet\Config` и иногда может размещаться в конкретной папке Visual Studio `\{IDE}\{Version}\{SKU}\`. В Mac/Linux его следует искать в каталоге `~/.local/share`. После этого отдельные пользователи могут выборочно включить восстановление на уровне проекта по необходимости. Дополнительные сведения о том, как NuGet устанавливает приоритеты для нескольких файлов конфигурации, см. в статье [Распространенные конфигурации NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> При изменении параметров `packageRestore` прямо в `nuget.config` нужно перезапустить Visual Studio, чтобы диалоговое окно **Параметры** отображало текущие значения.

## <a name="constrain-package-versions-with-restore"></a>Ограничение версий пакетов при восстановлении

Когда NuGet восстанавливает пакеты любым из методов, учитываются все ограничения, указанные в `packages.config` или файле проекта:

- В файле `packages.config`, вы можете указать диапазон версий в свойстве `allowedVersion` зависимости. Дополнительные сведения см. в статье [Ограничение версий при обновлении](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Например:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- В файле проекта вы можете указать диапазон для зависимости напрямую, используя PackageReference. Например:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Во всех случаях используйте нотацию, описанную в статье [Управление версиями пакета](../reference/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Принудительное восстановление из источников пакетов

По умолчанию в операциях восстановления NuGet используются пакеты из папки *global-packages* и *http-cache*, как описано в статье [Управление папкой установки глобальных пакетов, кэшем и временными папками](managing-the-global-packages-and-cache-folders.md).

Чтобы папка *global-packages* не использовалась, сделайте следующее:

- Очистите папку с помощью команды `nuget locals global-packages -clear` или `dotnet nuget locals global-packages --clear`.
- Перед операцией восстановления временно измените расположение папки *global-packages* с помощью одного из следующих методов:
  - В качестве значения переменной среды NUGET_PACKAGES задайте другую папку.
  - Создайте файл `NuGet.Config`, который в качестве значения параметра `globalPackagesFolder` (при использовании формата PackageReference) или `repositoryPath` (при использовании `packages.config`) задает другую папку. Дополнительные сведения см. в статье, посвященной [параметрам конфигурации](../reference/nuget-config-file.md#config-section).
  - Только для MSBuild: Укажите другую папку с помощью свойства `RestorePackagesPath`.

Чтобы не использовать кэш с источниками HTTP, выполните одно из следующих действий:

- Используйте параметр `-NoCache` с `nuget restore` или параметр `--no-cache` с `dotnet restore`. Эти параметры не влияют на операции восстановления с помощью диспетчера пакетов или консоли Visual Studio.
- Очистите кэш с помощью команды `nuget locals http-cache -clear` или `dotnet nuget locals http-cache --clear`.
- Временно в качестве значения переменной среды NUGET_HTTP_CACHE_PATH задайте другую папку.

## <a name="troubleshooting"></a>Устранение неполадок

Дополнительные сведения см. в статье [Устранение ошибок при восстановлении пакетов](package-restore-troubleshooting.md).
