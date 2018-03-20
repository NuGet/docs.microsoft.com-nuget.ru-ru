---
title: "Восстановление пакетов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Описание того, как NuGet восстанавливает пакеты, от которых зависит проект, включая отключение восстановления и ограничения версий."
keywords: "восстановление пакетов NuGet, установка пакетов NuGet, установка пакета, восстановление пакетов, версии зависимостей, отключение автоматического восстановления, ограничение версий пакетов"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a>Восстановление пакетов

Чтобы очистить среду разработки и уменьшить размер репозитория, **функция восстановления пакетов** NuGet устанавливает все указанные в ссылках пакеты перед сборкой проекта. Эта широко применяемая функция, &mdash;доступная в Visual Studio, .NET Core 2.0+ и xbuild в Mono&mdash;, гарантирует доступность всех зависимостей в проекте без необходимости сохранения этих пакетов в системе управления исходным кодом (сведения о том, как настроить репозиторий, чтобы исключить двоичные файлы пакетов, см. в статье [Пропуск пакетов NuGet в системах управления исходным кодом](../consume-packages/packages-and-source-control.md)). Пакеты можно также восстановить вручную в любое время.

Дополнительные сведения о восстановлении пакетов на серверах сборки см. в разделе [Восстановление пакетов с помощью TFBuild](../consume-packages/team-foundation-build.md).

## <a name="package-restore-overview"></a>Обзор восстановления пакетов

При восстановлении пакетов сначала устанавливаются необходимые прямые зависимости проекта, а затем остальные зависимости этих пакетов во всей схеме зависимостей.

Если пакет не установлен, NuGet сначала попытается извлечь его из [кэша](../consume-packages/managing-the-nuget-cache.md). Если пакета нет в кэше, NuGet пытается скачать (и кэшировать) его из всех включенных источников (см. статью [Настройка поведения NuGet](Configuring-NuGet-Behavior.md)), которые также отображаются в списке **Сервис > Параметры > Диспетчер пакетов NuGet > Источники пакетов** в Visual Studio. NuGet игнорирует порядок источников пакетов, используя пакет из любого источника, первым ответившего на запросы.

> [!Note]
> NuGet не сообщает о сбое восстановления пакета до проверки всех источников. После проверки NuGet сообщает о сбое только для последнего источника в списке. Такая ошибка означает, что пакет отсутствовал и во *всех* других источниках, хотя отдельные ошибки для них не выдавались.

Восстановление пакета инициируется с помощью следующих методов:

- **Интерфейс командной строки dotnet**: выполните команду [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) для восстановления пакетов в файле проекта (дополнительные сведения см. в статье [Ссылки на пакеты (PackageReference) в файлах проектов](../consume-packages/package-references-in-project-files.md)). При использовании .NET Core версии 2.0 и более поздней автоматическое восстановление доступно с помощью команд `dotnet build` и `dotnet run`.

- **Пользовательский интерфейс диспетчера пакетов (Visual Studio в Windows)**: пакеты автоматически восстанавливаются при создании проекта из шаблона и формировании проекта (как описано в разделе [Включение и отключение восстановления пакетов](#enabling-and-disabling-package-restore)). В NuGet 4.0 и более поздних версий также доступно автоматическое восстановление при изменении проекта на основе пакета SDK для .NET Core.

    Чтобы восстановить пакет вручную, щелкните правой кнопкой мыши решение в обозревателе решений и выберите **Восстановить пакеты NuGet**. Если один или несколько отдельных пакетов по-прежнему не установлены надлежащим образом (то есть для них в обозревателе решений отображается значок ошибки), удалите затрагиваемые пакеты с помощью пользовательского интерфейса диспетчера пакетов, после чего повторно установите их. См. раздел [Повторная установка и обновление пакетов](../consume-packages/reinstalling-and-updating-packages.md)

    Если отображается ошибка "Данный проект ссылается на пакеты NuGet, отсутствующие на этом компьютере" или "Необходимо восстановить один или несколько пакетов NuGet, однако это невозможно без вашего согласия", включите автоматическое восстановление, следуя инструкциям в разделе [Включение и отключение восстановления пакетов](#enabling-and-disabling-package-restore).

- **Интерфейс командной строки NuGet**: выполните команду [nuget restore](../tools/cli-ref-restore.md) для восстановления пакетов в файле проекта (дополнительные сведения см. в статье [Ссылки на пакеты (PackageReference) в файлах проектов](../consume-packages/package-references-in-project-files.md)) или файле [packages.config](../reference/packages-config.md). Вы можете также указать файл решения.

- **MSBuild**: выполните команду [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) для восстановления пакетов в файле проекта (дополнительные сведения см. в статье [Ссылки на пакеты (PackageReference) в файлах проектов](../consume-packages/package-references-in-project-files.md)). Доступно только в NuGet версии 4.x и более поздних и MSBuild версии 15.1 и более поздних, включенных в Visual Studio 2017. `nuget restore` и `dotnet restore` используют эту команду для подходящих проектов.

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

В некоторых случаях разработчику или организации может потребоваться включить или отключить восстановление пакетов на компьютере для всех пользователей. Это можно сделать, добавив указанные выше параметры в файл глобальной конфигурации NuGet, находящийся в `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. После этого отдельные пользователи могут выборочно включить восстановление на уровне проекта по необходимости. Точные сведения о том, как NuGet устанавливает приоритеты для нескольких файлов конфигурации, см. в разделе [Порядок применения параметров](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

## <a name="constraining-package-versions-with-restore"></a>Ограничение версий пакетов при восстановлении

При восстановлении пакетов любым из методов NuGet учитывает все ограничения, указанные в `packages.config` или файле проекта:

- `packages.config`: укажите диапазон версий в свойстве `allowedVersion` зависимости. Дополнительные сведения см. в разделе [Ограничение версий для обновления](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Пример:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- PackageReference: укажите диапазон версий непосредственно с номером версии зависимости. Пример:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Во всех случаях используйте нотацию, описанную в статье [Управление версиями пакета](../reference/package-versioning.md).

## <a name="troubleshooting"></a>Устранение неполадок

Дополнительные сведения см. в статье [Устранение ошибок при восстановлении пакетов в Visual Studio](package-restore-troubleshooting.md).