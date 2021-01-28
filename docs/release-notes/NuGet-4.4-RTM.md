---
title: Заметки о выпуске версии NuGet 4.4 RTM
description: Заметки о выпуске для NuGet 4.3 RTM, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 970a920a401b8a74c04d84cbad9933c54e3cd19e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776284"
---
# <a name="nuget-44-release-notes"></a>Заметки о выпуске NuGet 4.4

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает в себя NuGet 4.4 RTM.

## <a name="summary-whats-new-in-440"></a>Сводка: Новые возможности версии 4.4.0

## <a name="summary-whats-new-in-442"></a>Сводка: Новые возможности версии 4.4.2

* Исправление безопасности: разрешения на файлы, созданные внутри ~/.nuget, слишком открыты [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-443"></a>Сводка: Новые возможности версии 4.4.3

* Исправление безопасности: файлы внутри NUPKG могут иметь относительный путь выше каталога NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Известные проблемы

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Проблемы с .NET Standard 2.0, связанные с .NET Framework и NuGet 

Платформа .NET Standard и ее инструментарий были разработаны таким образом, чтобы проекты, предназначенные для .NET Framework 4.6.1, могли использовать пакеты NuGet и проекты, предназначенные для .NET Standard 2.0 или более ранних версий. [В этом документе](https://github.com/dotnet/standard/issues/481) кратко описаны проблемы, связанные с таким сценарием, план их решения, а также обходные пути, которые можно применить в текущем состоянии.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>При использовании консоли диспетчера пакетов клавиша ВВОД может не работать

#### <a name="issue"></a>Проблемы

Периодически клавиша ВВОД не работает в консоли диспетчера пакетов. В этом случае проверьте ход исправления и укажите дополнительные сведения для воспроизведения ошибки. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Возможное решение

Перезапустите Visual Studio и откройте консоль управления пакетами перед тем, как открыть решение. Кроме того, попробуйте удалить файл `project.lock.json` и выполнить восстановление еще раз.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Вы не можете просмотреть, добавить или обновить DotNetCLITools с помощью диспетчера пакетов NuGet.

#### <a name="issue"></a>Проблемы

Диспетчер пакетов NuGet не отображается и не позволяет добавить или обновить DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Возможное решение

DotNetCLIToolReferences нужно изменить вручную в файле проекта.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Изменение требуемой версии .NET Framework может привести к частичному отсутствию данных функции IntelliSense

#### <a name="issue"></a>Проблемы

Если изменить требуемую версию .NET Framework в Visual Studio, вы можете получить неполные данные функции IntelliSense. Это происходит, если использовать PackageReferences в качестве формата диспетчера пакетов. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Возможное решение

Выполните восстановление вручную.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Пакет в проекте .NET Core, который содержит сборку с недопустимой подписью, может инициировать бесконечный цикл восстановления.

#### <a name="issue"></a>Проблемы

Иногда при использовании пакета, содержащего сборку с недопустимой подписью, или при использовании пакета, версия которого задается с помощью параметра DateTime, возникает бесконечный цикл автоматического восстановления пакета (dotnet/project-system#1457).

#### <a name="workaround"></a>Возможное решение

Сейчас для этой проблемы не существует обходного решения.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Проблемы, исправленные в рамках NuGet 4.4 RTM

Проблемы, исправленные в NuGet 4.3 RTM, описаны в разделе [Заметки о выпуске NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md)

### <a name="features"></a>Функции

- Поддержка упрощенной загрузки решения в сценариях PMC и пользовательского интерфейса PM NuGet — [#5180](https://github.com/NuGet/Home/issues/5180)

- Целевой объект pack MSBuild должен иметь общедоступный обработчик для запуска целевых объектов пользователя перед собой — [#5143](https://github.com/NuGet/Home/issues/5143)

- Функция: добавление параметра dependencyVersion в установку NuGet — [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.TODO.0 должен соответствовать .NET Standard 2.0 для NuGet — [#5684](https://github.com/NuGet/Home/issues/5684)

- Поддержка SKU Visual Studio Build Tools с помощью msbuild /t:restore — [#5562](https://github.com/NuGet/Home/issues/5562)

- Во время восстановления выдается ошибка, если поддержка .NET 4.6.1 для .NET Standard 2.0 требуется, но не установлена — [#5325](https://github.com/NuGet/Home/issues/5325)

- Клиентский пользовательский интерфейс для резервирования префикса идентификатора пакета — [#5572](https://github.com/NuGet/Home/issues/5572)

- Предоставление локализованных компонентов NuGet для поддержки локализации dotnet.exe — [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Ошибки

- Разный регистр в путях проекта может привести к потере PackageReferences во время восстановления — [#5855](https://github.com/NuGet/Home/issues/5855)

- Перемещение кодов ошибок с номерами предупреждений в диапазон ошибок — [#5824](https://github.com/NuGet/Home/issues/5824)

- Вводящая в заблуждение ошибка, когда неизвестно, совместима ли версия .NET Standard с целевой платформой — [#5818](https://github.com/NuGet/Home/issues/5818)

- Файлы теста с вносящими путаницу лицензиями — [#5776](https://github.com/NuGet/Home/issues/5776)

- Отсутствующие заголовки лицензии в шаблонах тестов EndToEnd — [#5774](https://github.com/NuGet/Home/issues/5774)

- Операция восстановления packages.config показывает ошибки как NU1000 — [#5743](https://github.com/NuGet/Home/issues/5743)

- Команда nuget.exe install должна иметь DisableParallelProcessing в Mono — [#5741](https://github.com/NuGet/Home/issues/5741)

- Команда nuget.exe install отключает кэширование неправильно — [#5737](https://github.com/NuGet/Home/issues/5737)

- VS: если запустить команду восстановления для packages.config при отключенном восстановлении, отображается неправильное сообщение — [#5718](https://github.com/NuGet/Home/issues/5718)

- VS: если запустить команду восстановления при отключенном восстановлении, отображается вносящее путаницу сообщение — [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask завершается со сбоем при отсутствии метаданных версии — [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet
  - Команда dotnetcore add package может очистить пустые строки из файла CSPROJ — [#5697](https://github.com/NuGet/Home/issues/5697)

- Исходные имена параметров учетных данных в NuGet.Config чувствительны к регистру — [#5695](https://github.com/NuGet/Home/issues/5695)

- Включение GeneratePackageOnBuild привело к удалению всего моего журнала пакетов — [#5676](https://github.com/NuGet/Home/issues/5676)

- Команда restore не восстанавливает пакеты mono.cecil и semver, но все остальные пакеты восстанавливаются. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Ошибки и предупреждения — ошибка при недоступном источнике.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] Текст о состоянии установки NuGet выглядит неправильно при темной теме. - [#5642](https://github.com/NuGet/Home/issues/5642)

- При обновлении пакетов на уровне решения создаются действия обновления/установки для всех проектов — [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet
  - Команда dotnetcore pack работает по-разному в зависимости от того, используется ли TargetFramework или TargetFrameworks — [#5281](https://github.com/NuGet/Home/issues/5281)

- Включенные библиотеки DLL в папке Tools вызывают предупреждения — [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel использует слишком много памяти для операций со строками — [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux возвращает значение true для OSX — [#4648](https://github.com/NuGet/Home/issues/4648)

- Команда "dotnet pack" помещает NUSPEC-файл в obj вместо obj\Debug — [#4644](https://github.com/NuGet/Home/issues/4644)

- Крайне медленное обновление пакетов в NuGet — [#4534](https://github.com/NuGet/Home/issues/4534)

- CPS не синхронизируется с операцией восстановления для больших решений, где не включено упрощенное восстановление решения (LSL) — [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 — пакет NuGet с указанной версией игнорирует метаданные (3.5.0-rtm-1938) — [#3643](https://github.com/NuGet/Home/issues/3643)

- Команда "install package" с номером версии и флагом ExcludeVersion в NuGet.exe (3+) не обновляет пакет до более новой версии — [#2405](https://github.com/NuGet/Home/issues/2405)

- Операция восстановления Project.json должна выдавать предупреждение, когда пакеты верхнего уровня нарушают ограничения — [#2358](https://github.com/NuGet/Home/issues/2358)

- Параметр -ConfigFile не задает пользовательскую конфигурацию в команде install — [#1646](https://github.com/NuGet/Home/issues/1646)

- Команда nuget.exe install не учитывает параметр "-DisableParallelProcessing" — [#1556](https://github.com/NuGet/Home/issues/1556)

- Отключенные источники продолжают использоваться DotNet.exe или msbuild.exe — [#5704](https://github.com/NuGet/Home/issues/5704)

- Исправьте зависания в сценарии LSL — [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>Запросы на изменение структуры

- Поддержка TargetFramework для nuget.exe install — [#5736](https://github.com/NuGet/Home/issues/5736)

- Добавление других строк UserAgent для задачи msbuild (netcore или классический msbuild) — [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName должен быть виртуальным — [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] Вводящее в заблуждение сообщение при добавлении пакета NuGet — [#5641](https://github.com/NuGet/Home/issues/5641)

- [Предупреждения и ошибки] NoWarn не переходит транзитивно по одноранговым ссылкам — [#5501](https://github.com/NuGet/Home/issues/5501)

- Загрузка упрощенного решения: общее ядро для пользовательского интерфейса PM, PMC и IV — [#5057](https://github.com/NuGet/Home/issues/5057)

- Загрузка упрощенного решения: поддержка — PMC — [#5053](https://github.com/NuGet/Home/issues/5053)

- Добавление поддержки для предварительного восстановления целевого объекта MSBuild, который активирует Visual Studio — [#4781](https://github.com/NuGet/Home/issues/4781)

- Добавление общедоступного целевого объекта в NuGet.targets, на который можно сослаться с помощью BeforeTargets — [#4634](https://github.com/NuGet/Home/issues/4634)

- Целевому объекту pack не удается правильно создать contentFiles с действиями сборки — [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do блокирует потоки пула потоков — [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Документация для флагов DependencyVersion и Framework команды Install — [#5858](https://github.com/NuGet/Home/issues/5858)

- Обновление документации по предупреждениям и ошибкам NuGet — [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Ссылки на проблемы GitHub, исправленные в версии 4.4 RTM

[Список проблем 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Список проблем 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Список проблем 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
