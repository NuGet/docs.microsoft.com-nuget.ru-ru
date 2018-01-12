---
title: "Восстановление пакетов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Описание того, как NuGet восстанавливает пакеты, от которых зависит проект, включая отключение восстановления и ограничения версий."
keywords: "восстановление пакетов NuGet, установка пакетов NuGet, установка пакета, восстановление пакетов, версии зависимостей, отключение автоматического восстановления, ограничение версий пакетов"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a>Восстановление пакетов

Чтобы очистить среду разработки и уменьшить размер репозитория, **функция восстановления пакетов** NuGet устанавливает все указанные в ссылках пакеты перед сборкой проекта. Эта широко применяемая функция гарантирует доступность всех зависимостей в проекте без необходимости сохранения этих пакетов в системе управления исходным кодом (сведения о том, как настроить репозиторий, чтобы исключить двоичные файлы пакетов, см. в разделе [Пакеты и система управления версиями](../consume-packages/packages-and-source-control.md)).

В этом разделе.
- [Краткое руководство по восстановлению пакетов](#quick-guide-to-package-restore)
- [Обзор восстановления пакетов](#package-restore-overview)
- [Включение и отключение восстановления пакетов](#enabling-and-disabling-package-restore)
- [Ограничение версий пакетов при восстановлении](#constraining-package-versions-with-restore)
- [Восстановление из командной строки](#command-line-restore), для всех версий NuGet
- [Автоматическое восстановление в Visual Studio](#automatic-restore-in-visual-studio), для NuGet 2.7 и более поздних версий
- [Встроенное в MSBuild восстановление в Visual Studio](#msbuild-integrated-restore), для NuGet 2.6 и более ранних версий
- [Восстановление пакетов с помощью сборки Team Foundation](#package-restore-with-team-foundation-build)

Поведение при восстановлении зависит от версии. Чтобы узнать используемую версию NuGet, просто запустите `nuget.exe` в командной строке и посмотрите на первую строку выходных данных.

Дополнительные сведения о восстановлении пакетов на серверах сборки см. в разделе [Восстановление пакетов с помощью TFBuild](../consume-packages/team-foundation-build.md).

> [!Note]
> Проекты, настроенные для восстановления пакетов, работают с xbuild в Mono.

## <a name="quick-guide-to-package-restore"></a>Краткое руководство по восстановлению пакетов

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> Если отображается ошибка "Данный проект ссылается на пакеты NuGet, отсутствующие на этом компьютере" или "Необходимо восстановить один или несколько пакетов NuGet, однако это невозможно без вашего согласия", включите автоматическое восстановление, следуя инструкциям в разделе [Включение и отключение восстановления пакетов](#enabling-and-disabling-package-restore).

## <a name="package-restore-overview"></a>Обзор восстановления пакетов

Во-первых, в зависимости от типа проекта и версии NuGet ссылки на пакеты хранятся в одном из указанных ниже форматов управления пакетами. (Обратите внимание, что NuGet 4 и MSBuild 15.1 устанавливаются вместе с Visual Studio 2017.)

| Метод | Версия NuGet | Описание: | 
| --- | --- | --- |
| `packages.config` | 2.x+ | Указывает полный глубокий набор зависимостей. Пакеты, добавляемые в `packages.config`, также должны добавляться в файл проекта, как и целевые объекты и свойства. Это базовый метод для всех версий NuGet, однако он имеет пониженную производительность по сравнению с другими вариантами. (См. раздел [Схема packages.config](../schema/packages-config.md).) | 
| `project.json` | 3.x+ | Используется по умолчанию только с проектами UWP, но проекты можно преобразовать из `packages.config`. `project.json` указывает только высокоуровневые зависимости. Ссылки, целевые объекты и свойства добавляются в проект динамически во время сборки, что обеспечивает более высокую производительность по сравнению с `packages.config`. (См. раздел [Схема project.json](../schema/project-json.md).)|
| PackageReference | 4.x+ | Указывает зависимости прямо в файле проекта в узле `<PackageReference>` вместе с `<Reference>` и `<ProjectReference>`. Работает аналогично `project.json`; см. раздел [Ссылки на пакеты в файлах проекта](../Consume-Packages/Package-References-in-Project-Files.md). |

Во-вторых, запустить восстановление с помощью списка ссылок можно разными способами:

Из командной строки или [консоли диспетчера пакетов](../tools/Package-Manager-Console.md):

| Команда | Применимые сценарии |
| --- | --- | 
| `nuget restore` | Все версии NuGet и все типы ссылок. См. раздел [Восстановление из командной строки](#command-line-restore) ниже. | 
| `dotnet restore` | То же, что и `nuget restore`, для проектов .NET Core. См. раздел [dotnet restore](/dotnet/articles/core/tools/dotnet-restore). |
| `msbuild /t:restore` | Только Nuget 4.x+ и MSBuild 15.1+ со [ссылками на пакеты в файлах проекта](../Consume-Packages/Package-References-in-Project-Files.md). `nuget restore` и `dotnet restore` используют эту команду для подходящих проектов. См. раздел [Объекты pack и restore NuGet в качестве целевых объектов MSBuild — целевой объект restore](../schema/msbuild-targets.md#restore-target).|

В разное время среда Visual Studio также восстанавливает пакеты:

| Тип | Когда происходит восстановление |
| --- | --- |
| Восстановление шаблона | При создании проекта, так как некоторые шаблоны зависят от внешних пакетов. |
| Восстановление сборки | На первом шаге сборки. |
| Восстановление решения | Когда пользователь щелкает правой кнопкой мыши решение и выбирает пункт **Восстановить пакеты NuGet**. |
| Восстановление при изменении проекта | *(Только NuGet 4.x)* Когда используется проект на основе пакета SDK для .NET Core, включая изменение состояния проекта. |

## <a name="enabling-and-disabling-package-restore"></a>Включение и отключение восстановления пакетов

Восстановление пакетов можно включить в меню **Сервис > Параметры > Диспетчер пакетов NuGet** в Visual Studio:

![Управление поведением восстановления пакетов с помощью параметров диспетчера пакетов NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Разрешить NuGet скачивать отсутствующие пакеты**: определяет все формы восстановления пакетов, изменяя `packageRestore/enabled` в файле `%AppData%\NuGet\NuGet.Config`, как показано ниже.

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
    

- **Автоматически проверять отсутствие пакетов при сборке в Visual Studio**: управляет автоматическим восстановлением для NuGet 2.7 и более поздних версий, изменяя `packageRestore/automatic` в файле `%AppData%\NuGet\NuGet.Config`, как показано ниже.
            
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

Справочную информацию см. в разделе [Файл конфигурации NuGet — packageRestore](../Schema/nuget-config-file.md#packagerestore-section).

В некоторых случаях разработчику или организации может потребоваться включить или отключить восстановление пакетов на компьютере по умолчанию для всех пользователей. Это можно сделать, добавив указанные выше параметры в файл глобальной конфигурации NuGet, находящийся в `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. После этого отдельные пользователи могут выборочно включить восстановление на уровне проекта по необходимости. Точные сведения о том, как NuGet устанавливает приоритеты для нескольких файлов конфигурации, см. в разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

## <a name="constraining-package-versions-with-restore"></a>Ограничение версий пакетов при восстановлении

Когда NuGet восстанавливает пакеты любым из методов, он учитывает все ограничения, указанные в `packages.config`, `project.json` или файле проекта:

- `packages.config`: укажите диапазон версий в свойстве `allowedVersion` зависимости. См. раздел [Повторная установка и обновление пакетов](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Пример:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json`: укажите диапазон версий непосредственно с номером версии зависимости. Пример:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- Ссылки на пакеты в файлах проекта: укажите диапазон версий непосредственно с номером версии зависимости. Пример:
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

Во всех случаях используйте нотацию, описанную в статье [Управление версиями пакета](../reference/package-versioning.md).

## <a name="command-line-restore"></a>Восстановление из командной строки

Для NuGet 2.7 и более поздних версий используйте команду [Восстановить](../tools/cli-ref-restore.md), чтобы восстановить все пакеты в решении (использует ли оно `packages.config`, `project.json` или ссылки на пакеты в файлах проекта). Для заданной папки проекта, например `c:\proj\app`, пакеты восстанавливает каждый из следующих вариантов:

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

Для NuGet 4.0+ и MSBuild 15.1+ можно также использовать `MSBuild /t:restore`, как описано в разделе [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../schema/msbuild-targets.md).

## <a name="build-time-restore-in-visual-studio"></a>Восстановление во время сборки в Visual Studio

Visual Studio автоматически восстанавливает отсутствующие пакеты по умолчанию в начале сборки. Это поведение можно изменить, сняв флажок **Сервис > Параметры > Диспетчер пакетов NuGet > Общие > Автоматически проверять отсутствие пакетов при сборке в Visual Studio**.

Когда автоматическое восстановление включено, оно работает следующим образом:

1. В начале сборки Visual Studio предписывает NuGet восстановить пакеты.
1. NuGet рекурсивно ищет все файлы `packages.config` в решении, выполняет поиск `project.json`, а также по файлу проекта.
1. Для каждого из пакетов, указанных в файлах ссылок, NuGet проверяет, существует ли он в решении (в папке `packages`, `project.lock.json` или `project.assets.json` — в зависимости от того, использует ли проект `packages.config`, `project.json` или ссылки на пакеты в файлах проекта).
1. Если пакет не найден, NuGet сначала пытается извлечь его из своего кэша (см. раздел [Управление кэшем NuGet](../consume-packages/managing-the-nuget-cache.md)). Если пакета нет в кэше, NuGet пытается скачать его из включенных источников, как указано в меню **Сервис > Параметры > Диспетчер пакетов NuGet > Источники пакетов**, проверяя их в указанном порядке. В этом случае NuGet не выдает ошибку поиска пакета, пока не проверит все источники, после чего выдает ошибку только для последнего источника в списке. Неявно такая ошибка означает, что пакет отсутствовал и во всех других источниках, хотя отдельные ошибки для них не выдавались.
1. В случае успешного скачивания NuGet кэширует пакет и устанавливает его в решении (опять же в папку `packages`, `project.lock.json` или `project.assets.json`); в противном случае происходит сбой NuGet и сборка завершается с ошибкой.

Во время этого процесса отображается диалоговое окно хода выполнения, где можно отменить восстановление пакетов.

## <a name="package-restore-with-team-foundation-build"></a>Восстановление пакетов с помощью сборки Team Foundation

Восстановление пакетов обычно используется при сборке проектов на серверах сборки, например с помощью Team Foundation Server (TFS) и Visual Studio Team Services (а также других систем сборки, которые здесь не описаны).

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

При создании определения сборки в Team Services просто включите в него задачу "Восстановить пакеты NuGet" до любой задачи сборки. Эта задача по умолчанию входит в несколько шаблонов сборки.

![Задача восстановления пакетов NuGet в определении сборки Visual Studio Team Service](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

В TFS 2013 и более поздних версий пакеты восстанавливаются автоматически по умолчанию во время сборки при условии, что вы используете шаблон командной сборки для Team Foundation Server 2013 или более поздней версии.

Если вы используете предыдущую версию шаблонов сборки (например, в проекте, который был перенесен из более ранних версий TFS), потребуется также выполнить миграцию этих шаблонов сборки в TFS 2013. По существу это означает повторное создание пользовательских частей шаблонов сборки с помощью подходящего шаблона для вашей системы управления исходным кодом (TFVC или Git).

Для более ранней версии TFS можно просто включить шаг сборки, чтобы вызвать [восстановление из командной строки](#command-line-restore), как описано выше.

Дополнительные сведения см. в разделе [Пошаговое руководство по восстановлению пакетов с помощью сборки Team Foundation](../consume-packages/team-foundation-build.md).    
