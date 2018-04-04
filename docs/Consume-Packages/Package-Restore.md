---
title: Восстановление пакетов NuGet | Документы Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Описание того, как NuGet восстанавливает пакеты, от которых зависит проект, включая отключение восстановления и ограничения версий.
keywords: восстановление пакетов NuGet, установка пакетов NuGet, установка пакета, восстановление пакетов, версии зависимостей, отключение автоматического восстановления, ограничение версий пакетов
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: d5c9c9f571ea25f8877f78c3fba114562d31fcd8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="package-restore"></a>Восстановление пакетов

Чтобы очистить среду разработки и уменьшить размер репозитория, **функция восстановления пакетов** NuGet устанавливает все зависимости проекта, указанные в файле проекта или файле `packages.config`. Visual Studio может автоматически восстановить пакеты при построении проекта. Это можно сделать также с помощью команд `dotnet build` и `dotnet run` (.NET Core 2.0 и более поздних версий). Кроме того, пакеты можно восстановить в любое время с помощью Visual Studio, `nuget restore`, `dotnet restore` и xbuild в Mono.

Восстановление пакетов гарантирует доступность всех зависимостей проекта без сохранения этих пакетов в системе управления версиями. Дополнительные сведения о настройке исключения двоичных файлов пакетов в репозитории см. в статье [Пропуск пакетов NuGet в системах управления исходным кодом](../consume-packages/packages-and-source-control.md).

## <a name="package-restore-overview"></a>Обзор восстановления пакетов

При восстановлении пакетов сначала устанавливаются необходимые прямые зависимости проекта, а затем остальные зависимости этих пакетов во всей схеме зависимостей.

Если пакет не установлен, NuGet сначала попытается извлечь его из [кэша](../consume-packages/managing-the-global-packages-and-cache-folders.md). Если пакета нет в кэше, NuGet пытается скачать его из всех включенных источников (см. статью [Настройка поведения NuGet](Configuring-NuGet-Behavior.md)), которые также отображаются в списке **Сервис > Параметры > Диспетчер пакетов NuGet > Источники пакетов** в Visual Studio. Во время восстановления NuGet игнорирует порядок источников пакетов, используя пакет из любого источника, первым ответившего на запросы.

> [!Note]
> NuGet не сообщает о сбое восстановления пакета до проверки всех источников. После проверки NuGet сообщает о сбое только для последнего источника в списке. Такая ошибка означает, что пакет отсутствовал и во *всех* других источниках, хотя отдельные ошибки для них не выдавались.

Восстановление пакета инициируется с помощью следующих методов:

- **Интерфейс командной строки dotnet**: выполните команду [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) для восстановления пакетов в файле проекта (дополнительные сведения см. в статье [Ссылки на пакеты (PackageReference) в файлах проектов](../consume-packages/package-references-in-project-files.md)). При использовании .NET Core версии 2.0 и более поздней автоматическое восстановление доступно с помощью команд `dotnet build` и `dotnet run`.

- **Пользовательский интерфейс диспетчера пакетов (Visual Studio в Windows)**: пакеты автоматически восстанавливаются при создании проекта из шаблона и формировании проекта (как описано в разделе [Включение и отключение восстановления пакетов](#enabling-and-disabling-package-restore)). В NuGet 4.0 и более поздних версий также доступно автоматическое восстановление при изменении проекта на основе пакета SDK для .NET Core.

    Чтобы восстановить пакет вручную, щелкните правой кнопкой мыши решение в обозревателе решений и выберите **Восстановить пакеты NuGet**. Если один или несколько отдельных пакетов по-прежнему не установлены надлежащим образом (то есть для них в обозревателе решений отображается значок ошибки), удалите затрагиваемые пакеты с помощью пользовательского интерфейса диспетчера пакетов, после чего повторно установите их. См. раздел [Повторная установка и обновление пакетов](../consume-packages/reinstalling-and-updating-packages.md)

    Если отображается ошибка "Данный проект ссылается на пакеты NuGet, отсутствующие на этом компьютере" или "Необходимо восстановить один или несколько пакетов NuGet, однако это невозможно без вашего согласия", включите автоматическое восстановление, следуя инструкциям в разделе [Включение и отключение восстановления пакетов](#enabling-and-disabling-package-restore). Дополнительные сведения см. в статье [Устранение ошибок при восстановлении пакетов](Package-restore-troubleshooting.md).

- **NuGet CLI.** Выполните команду [nuget restore](../tools/cli-ref-restore.md), которая позволяет восстановить пакеты, указанные в файле проекта или файле `packages.config`. Вы можете также указать файл решения.

- **MSBuild.** Выполните команду [msbuild /t:restore](../reference/msbuild-targets.md#restore-target), которая позволяет восстановить пакеты в файле проекта (только формат PackageReference). Доступно только в NuGet версии 4.x и более поздних и MSBuild версии 15.1 и более поздних, включенных в Visual Studio 2017. `nuget restore` и `dotnet restore` используют эту команду для подходящих проектов.

- **Visual Studio Team Services**: при создании определения сборки в Team Services включите в него задачу [восстановления NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) или [.NET Core](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages), а затем добавьте задачу сборки. Эта задача по умолчанию входит в несколько шаблонов сборки.

- **Team Foundation Server**: в TFS 2013 и более поздних версий пакеты восстанавливаются автоматически во время сборки при условии, что вы используете шаблон командной сборки для TFS 2013 или более поздней версии. Для более ранней версии TFS можно просто включить шаг сборки, чтобы вызвать один из параметров восстановления из командной строки, как описано выше. При необходимости можно перенести шаблон сборки в TFS 2013. Дополнительные сведения см. в статье [Настройка восстановления пакетов с помощью сборки Team Foundation](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Включение и отключение восстановления пакетов

Восстановление пакетов можно включить в меню **Сервис > Параметры > Диспетчер пакетов NuGet** в Visual Studio:

![Управление поведением восстановления пакетов с помощью параметров диспетчера пакетов NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Разрешить NuGet скачивать отсутствующие пакеты**: определяет все формы восстановления пакетов, изменяя `packageRestore/enabled` в файле `NuGet.Config`, как показано ниже (`%AppData%\NuGet\NuGet.Config` в Windows, `~/.nuget/NuGet/NuGet.Config` в Mac/Linux). В Visual Studio этот параметр обеспечивает работу команды **Восстановить пакеты NuGet** в контекстном меню решения.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  Параметр `packageRestore/enabled` можно переопределить на глобальном уровне, задав для переменной среды с именем **EnableNuGetPackageRestore** значение TRUE или FALSE перед запуском Visual Studio или началом сборки.

- **Автоматически проверять отсутствие пакетов при сборке в Visual Studio**: управляет автоматическим восстановлением, изменяя параметр `packageRestore/automatic` в файле `NuGet.Config`, как показано ниже (`%AppData%\NuGet\NuGet.Config` в Windows, `~/.nuget/NuGet/NuGet.Config` в Mac/Linux). Когда этот параметр задан, при запуске сборки из Visual Studio все отсутствующие пакеты восстанавливаются автоматически. Этот параметр не затрагивает сборки, запускаемые из командной строки с помощью MSBuild.

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

Справочную информацию см. в разделе [Файл конфигурации NuGet — packageRestore](../reference/nuget-config-file.md#packagerestore-section).

В некоторых случаях разработчику или организации может потребоваться включить или отключить восстановление пакетов на компьютере для всех пользователей. Это можно сделать, добавив указанные выше параметры в файл глобальной конфигурации NuGet, находящийся в папке `%ProgramData%\NuGet\Config` (папка `\{IDE}\{Version}\{SKU}\` для Visual Studio в ОС Windows) или `~/.local/share` (Mac или Linux). После этого отдельные пользователи могут выборочно включить восстановление на уровне проекта по необходимости. Точные сведения о том, как NuGet устанавливает приоритеты для нескольких файлов конфигурации, см. в разделе [Порядок применения параметров](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> При изменении параметров `packageRestore` прямо в `nuget.config` нужно перезапустить Visual Studio, чтобы диалоговое окно параметров отображало текущие значения.

## <a name="constraining-package-versions-with-restore"></a>Ограничение версий пакетов при восстановлении

При восстановлении пакетов любым из методов NuGet учитывает все ограничения, указанные в `packages.config` или файле проекта:

- `packages.config`: укажите диапазон версий в свойстве `allowedVersion` зависимости. Дополнительные сведения см. в разделе [Ограничение версий для обновления](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Пример:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Файл проекта (PackageReference): укажите диапазон версий непосредственно с номером версии зависимости. Пример:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Во всех случаях используйте нотацию, описанную в статье [Управление версиями пакета](../reference/package-versioning.md).

## <a name="forcing-restore-from-package-sources"></a>Принудительное восстановление из источников пакетов

По умолчанию в операциях восстановления NuGet используются пакеты из папки *global-packages* и *http-cache*, как описано в статье [Управление папкой установки глобальных пакетов, кэшем и временными папками](managing-the-global-packages-and-cache-folders.md).

Чтобы папка *global-packages* не использовалась, сделайте следующее:

- Очистите папку с помощью команды `nuget locals global-packages -clear` или `dotnet nuget locals global-packages --clear`.
- Перед операцией восстановления временно измените расположение папки *global-packages* с помощью одного из следующих методов:
  - В качестве значения переменной среды NUGET_PACKAGES задайте другую папку.
  - Создайте файл `NuGet.Config`, который в качестве значения параметра `globalPackagesFolder` (при использовании формата PackageReference) или `repositoryPath` (при использовании `packages.config`) задает другую папку (см. раздел о [параметрах конфигурации](../reference/nuget-config-file.md#config-section)).
  - Только MSBuild. Укажите другую папку с помощью свойства `RestorePackagesPath`.

Чтобы не использовать кэш с источниками HTTP, выполните одно из следующих действий:

- Используйте параметр `-NoCache` с `nuget restore` или параметр `--no-cache` с `dotnet restore`. Эти параметры не влияют на операции восстановления с помощью пользовательского интерфейса диспетчера пакетов или консоли Visual Studio.
- Очистите кэш с помощью команды `nuget locals http-cache -clear` или `dotnet nuget locals http-cache --clear`.
- Временно в качестве значения переменной среды NUGET_HTTP_CACHE_PATH задайте другую папку.

## <a name="troubleshooting"></a>Устранение неполадок

Дополнительные сведения см. в статье [Устранение ошибок при восстановлении пакетов в Visual Studio](package-restore-troubleshooting.md).