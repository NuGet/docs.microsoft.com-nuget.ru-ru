---
title: Преобразование package.config в формат PackageReference
description: Сведения об изменении формата управления проекта с package.config на формат PackageReference, поддерживаемый NuGet 4.0+, VS2017 и .NET Core 2.0.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 6f659af6b09a12be54a5ef843d34f956119b33f4
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520494"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Преобразование packages.config в PackageReference

Visual Studio 2017 версии 15.7 и более поздних поддерживает преобразование формата управления проекта с [packages.config](../reference/packages-config.md) в формат [PackageReference](../consume-packages/Package-References-in-Project-Files.md).

## <a name="benefits-of-using-packagereference"></a>Преимущества использования PackageReference

* **Централизованное управление всеми зависимостями проекта**. Как и в случае со ссылками на проекты и сборки, управление ссылками на пакеты NuGet (с помощью узла `PackageReference`) выполняется непосредственно в файлах проекта, а не в отдельном файле packages.config.
* **Лаконичное представление зависимостей верхнего уровня**. В отличие от packages.config, PackageReference содержит список только тех пакетов NuGet, которые вы непосредственно установили в проекте. В результате пользовательский интерфейс диспетчера пакетов NuGet и файл проекта не загромождены зависимостями нижнего уровня.
* **Повышение производительности**. При использовании PackageReference пакеты хранятся в папке *global-packages* (как описано в статье [Управление папкой установки глобальных пакетов, кэшем и временными папками](../consume-packages/managing-the-global-packages-and-cache-folders.md)), а не в папке `packages` в решении. В результате PackageReference выполняется быстрее и занимает меньше дискового пространства.
* **Точное управление зависимостями и потоком содержимого**. Использование имеющихся функций MSBuild позволяет вам [условно ссылаться на пакет NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) и выбирать ссылки на пакеты для целевой платформы, конфигурации, платформы или других сводок.
* **PackageReference находится в активной разработке**. Дополнительные сведения см. [на сайте GitHub](https://aka.ms/nuget-pr-improvements). Формат packages.config больше не находится в разработке.

### <a name="limitations"></a>Ограничения

* NuGet PackageReference недоступен в Visual Studio 2015 и более ранних версиях. Мигрированные проекты можно открыть только в Visual Studio 2017 и более поздних версиях.
* На данный момент не поддерживается миграция для проектов C++ и ASP.NET.
* Некоторые пакеты могут быть не полностью совместимы с PackageReference. Дополнительные сведения см.в разделе [Проблемы совместимости пакетов](#package-compatibility-issues).

### <a name="known-issues"></a>Известные проблемы

1. Параметр `Migrate packages.config to PackageReference...` недоступен в контекстном меню, которое открывается по щелчку правой кнопкой мыши 

#### <a name="issue"></a>Проблемы 
 
При первом открытии проект NuGet не удается инициализировать до выполнения операции NuGet. В результате параметр миграции не отображается в контекстном меню, которое открывается по щелчку правой кнопкой мыши `packages.config` или `References`. 

#### <a name="workaround"></a>Обходной путь 

Выполните одно из следующих действий NuGet: 
* Откройте пользовательский интерфейс диспетчера пакетов. Для этого щелкните правой кнопкой мыши `References` и выберите `Manage NuGet Packages...`. 
* Откройте консоль диспетчера пакетов. В `Tools > NuGet Package Manager` выберите `Package Manager Console`. 
* Запустите восстановление NuGet. Для этого щелкните правой кнопкой мыши узел решения в обозревателе решений и выберите `Restore NuGet Packages`. 
* Создайте проект, активизирующий восстановление NuGet. 

Теперь параметр миграции должен отобразиться. Обратите внимание, что этот параметр не поддерживается и не будет отображаться для типов проектов ASP.NET и C++. 

## <a name="migration-steps"></a>Этапы миграции

> [!Note]
> Перед началом миграции Visual Studio создает резервную копию проекта, чтобы при необходимости вы могли [выполнить откат к packages.config](#how-to-roll-back-to-packagesconfig).

1. Откройте решение, содержащее проект в формате `packages.config`.

1. В **обозревателе решений** щелкните правой кнопкой мыши узел **ссылок** или файл `packages.config` и выберите **Перенести packages.config в PackageReference...** .

1. Средство миграции выполнит анализ ссылок на пакеты NuGet проекта и попытается разделить их на **зависимости верхнего уровня** (пакеты NuGet, которые вы установили напрямую) и **переходные зависимости** (пакеты, которые были установлены как зависимости пакетов верхнего уровня).

   > [!Note]
   > PackageReference поддерживает восстановление транзитивных пакетов и динамически разрешает зависимости, а это означает, что переходные зависимости не нужно устанавливать явно.

1. (Необязательно.) Вы можете настроить для пакета NuGet, классифицированного как переходная зависимость, обработку в качестве зависимости верхнего уровня, выбрав для пакета параметр **Верхний уровень**. Этот параметр автоматически устанавливается для пакетов, содержащих ресурсы, которые не передаются транзитивно (те, которые находятся в папках `build`, `buildCrossTargeting`, `contentFiles` или `analyzers`) и помечены как зависимость времени разработки (`developmentDependency = "true"`).

1. Просмотрите все [проблемы совместимости пакетов](#package-compatibility-issues).

1. Нажмите кнопку **ОК**, чтобы начать миграцию.

1. По завершении миграции Visual Studio предоставляет отчет, содержащий путь к резервной копии, список установленных пакетов (зависимостей верхнего уровня), список пакетов, отмеченных как переходные зависимости, и список проблем совместимости, обнаруженных в начале миграции. Отчет будет сохранен в папку резервных копий.

1. Убедитесь, что решение выполняет сборку и запуск. Если у вас возникли проблемы, [сообщите о них на сайте GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Выполнение отката к packages.config

1. Закройте перенесенный проект.

1. Скопируйте файл проекта и `packages.config` из резервной копии (обычно `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) в папку проекта. Удалите папку obj (при наличии) в корневой папке проекта.

1. Откройте проект.

1. Откройте консоль диспетчера пакетов с помощью команды меню **Средства > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.

1. В консоли выполните следующую команду:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Создание пакета после миграции

После завершения миграции рекомендуем добавить ссылку на пакет NuGet [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack), а затем с помощью [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) создать пакет. В некоторых случаях вы можете использовать `dotnet.exe pack` вместо `msbuild -t:pack`, однако это не рекомендуется.

## <a name="package-compatibility-issues"></a>Проблемы совместимости пакетов

Некоторые функции, поддерживаемые в package.config, не поддерживаются в PackageReference. Средство миграции анализирует и обнаруживает такие проблемы. Любой пакет с одной или несколькими из описанных ниже проблем может неправильно работать после миграции.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>При установке пакета после миграции сценарии install.ps1 игнорируются

| | |
| --- | --- |
| **Описание** | При использовании PackageReference сценарии PowerShell install.ps1 и uninstall.ps1 не выполняются во время установки или удаления пакета. |
| **Потенциальное влияние** | Пакеты, которые используют эти сценарии для настройки определенных действий в целевом проекте, могут не работать должным образом. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>При установке пакета после миграции ресурсы content недоступны

| | |
| --- | --- |
| **Описание** | PackageReference не поддерживает и игнорирует ресурсы в папке `content` пакета. PackageReference добавляет поддержку для `contentFiles`, обеспечивая лучший уровень транзитивности и общий доступ к содержимому.  |
| **Потенциальное влияние** | Ресурсы, содержащиеся в `content`, не копируются в проект, а код проекта, который зависит от наличия этих ресурсов, требует выполнения рефакторинга.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>При установке пакета после обновления преобразования XDT не применяются

| | |
| --- | --- |
| **Описание** | При установке или удалении пакета PackageReference не поддерживает преобразования XDT и игнорирует файлы `.xdt`.   |
| **Потенциальное влияние** | Преобразования XDT (чаще всего `web.config.install.xdt` и `web.config.uninstall.xdt`) не применяются ни к каким XML-файлам проекта. Это означает, что файл проекта ` web.config` не обновляется при установке или удалении пакета. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>При установке пакета после миграции сборки в корне lib игнорируются

| | |
| --- | --- |
| **Описание** | При использовании PackageReference сборки, находящиеся в корне папки `lib` без определенной подпапки целевой платформы, игнорируются. NuGet ищет подпапку, соответствующую моникеру целевой платформы (TFM) с учетом целевой платформы проекта, и устанавливает необходимые сборки в проект. |
| **Потенциальное влияние** | Пакеты без подпапки, соответствующей моникеру целевой платформы с учетом целевой платформы проекта, после перехода или сбоя установки во время миграции могут работать не так, как ожидалось. |

## <a name="found-an-issue-report-it"></a>Столкнулись с проблемой? Сообщите о ней.

Если у вас возникла проблема с миграцией, [сообщите о ней в репозиторий NuGet на сайте GitHub](https://github.com/NuGet/Home/issues/).