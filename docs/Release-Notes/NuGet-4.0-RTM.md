---
title: Заметки о выпуске версии-кандидата NuGet 4.0 | Документы Майкрософт
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Заметки о выпуске для NuGet 4.0 RTM, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
keywords: заметки о выпуске NuGet 4.0 RTM, исправления ошибок, известные проблемы, добавленные функции и запросы на изменение структуры
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 75ce757c209afd74f8d4f45d58d4e13a23b3b743
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-40-rtm-release-notes"></a>Заметки о выпуске версии NuGet 4.0 RTM

В состав [Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) входит версия NuGet 4.0, в которую добавлена поддержка платформы .NET Core, а также представлено множество исправлений, направленных на повышение качества и производительности. Кроме того, в этой версии появился ряд усовершенствований, таких как поддержка формата PackageReference, использование команд NuGet в качестве целей MSBuild, восстановление пакетов в фоновом режиме и других.

## <a name="known-issues"></a>Известные проблемы

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>Сбой восстановления NuGet может завершиться ошибкой, если в решении есть несколько проектов, ссылающихся на другой проект

#### <a name="issue"></a>Проблеми

Восстановление NuGet может не работать, если в решении есть проекты, которые ссылаются на один и тот же проект с разным регистром или с другими относительными путями. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>Обходной путь

Исправьте регистр и относительные пути, чтобы они совпадали во всех ссылках на проект.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>При использовании консоли диспетчера пакетов клавиша ВВОД может не работать

#### <a name="issue"></a>Проблеми

Периодически клавиша ВВОД не работает в консоли диспетчера пакетов. В этом случае проверьте ход исправления и укажите дополнительные сведения для воспроизведения ошибки. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Обходной путь

Перезапустите Visual Studio и откройте консоль управления пакетами перед тем, как открыть решение. Кроме того, попробуйте удалить файл `project.lock.json` и выполнить восстановление еще раз.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>При использовании пакета, содержащего сборку с недопустимой подписью, в проектах .NET Core может возникнуть бесконечный цикл восстановления

#### <a name="issue"></a>Проблеми

Иногда при использовании пакета, содержащего сборку с недопустимой подписью, или если для версии пакета задан тикер DateTime, возникает бесконечный цикл автоматического восстановления пакета. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Обходной путь

Сейчас для этой проблемы не существует обходного решения.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Вы не можете просмотреть, добавить или обновить DotNetCLITools с помощью диспетчера пакетов NuGet.

#### <a name="issue"></a>Проблеми

Диспетчер пакетов NuGet не отображается и не позволяет добавить или обновить DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Обходной путь

DotNetCLIToolReferences нужно изменить вручную в файле проекта.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>При установке свойства PackageId для проектов произойдет сбой восстановления NuGet

#### <a name="issue"></a>Проблеми

Для проектов .NET Core восстановление NuGet в Visual Studio не связано со свойством PackageId проектов. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>Обходной путь

Выполните восстановление с использованием командной строки.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>Если в проекте нет папки obj, произойдет сбой восстановления пакета

#### <a name="issue"></a>Проблеми

Visual Studio не удается восстановить PackageReferences, если папка obj удалена. [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>Обходной путь

Создайте папку obj вручную, и восстановление должно заработать.

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>Обновление пакетов вручную с использованием Update-Package в консоли может завершиться ошибкой

#### <a name="issue"></a>Проблеми

Использование Update-Package вручную в консоли работает только один раз для только что преобразованных проектов PackageReferences. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>Обходной путь

Сейчас для этой проблемы не существует обходного решения.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Изменение требуемой версии .NET Framework может привести к частичному отсутствию данных функции IntelliSense

#### <a name="issue"></a>Проблеми

Если изменить требуемую версию .NET Framework в Visual Studio, вы можете получить неполные данные функции IntelliSense. Это происходит, если использовать PackageReferences в качестве формата диспетчера пакетов. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Обходной путь

Выполните восстановление вручную.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>Операция MSBuild /t:restore завершается ошибкой, если проект, предназначенный для .NET 4.6.1, ссылается на другой проект, предназначенный для .NET Standard

#### <a name="issue"></a>Проблеми

Операция MSBuild /t:restore завершается ошибкой, если проект на основе PackageReferenece, предназначенный для .NET 4.6.1, ссылается на другой проект на основе PackageReferenece, предназначенный для .NET Standard.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Обходной путь

Сейчас для этой проблемы не существует обходного решения.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Проблемы, исправленные в рамках NuGet 4.0 RTM

Проблемы, исправленные в NuGet 4.0 RC, описаны в разделе [Заметки о выпуске NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md)

### <a name="features"></a>Функции

- Локализация строк в NuGet.Core.sln — [2041](https://github.com/NuGet/Home/issues/2041)

- Nuget вызывает принудительную загрузку проектов веб-приложений в режиме LSL — [4258](https://github.com/NuGet/Home/issues/4258)

- Поддержка автоматически задаваемых ссылок проектов для блокировки изменений версии в пользовательском интерфейсе для пакетов "sdk installed" — [4044](https://github.com/NuGet/Home/issues/4044)

- Передача правильного значения PackageSpec.Version для любых зависимостей проектов (PackageRef) — [3902](https://github.com/NuGet/Home/issues/3902)

- Поддержка удаления ссылок в `.csproj` из командной строки — [4101](https://github.com/NuGet/Home/issues/4101)

- Поддержка восстановления пакетов PackageReference (обычные и xplat) и загрузки упрощенного решения — [4003](https://github.com/NuGet/Home/issues/4003)

- Поддержка добавления ссылок в `.csproj` из командной строки — [3751](https://github.com/NuGet/Home/issues/3751)

- Поддержка восстановления NuGet для загрузки упрощенного решения для `packages.config` или `project.json` - [3711](https://github.com/NuGet/Home/issues/3711)

- Поддержка contentFiles в создаваемых nuget файлах целевых объектов — [3683](https://github.com/NuGet/Home/issues/3683)

- Установка Mono CI для проверки nuget.exe на Mac с использованием MSBuild — [3646](https://github.com/NuGet/Home/issues/3646)

- Отказ от зависимостей NuGet от v2 NuGet.Core — [3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Ошибки

- Восстановление NuGet в Visual Studio не связано со свойством PackageId проектов — [4586](https://github.com/NuGet/Home/issues/4586)

- Ошибка NuGet ProjectSystemCache при добавлении пакета в пакет vsix — [4545](https://github.com/NuGet/Home/issues/4545)

- Операция упаковки вызывает исключение при использовании IncludeSource в проекте с несколькими моникерами целевой платформы — [4536](https://github.com/NuGet/Home/issues/4536)

- Работа VS 2017 RC3 завершается сбоем при использовании обновления из среды управления пакетами на уровне решения — [4474](https://github.com/NuGet/Home/issues/4474)

- Не удается удалить вновь установленный пакет — [4435](https://github.com/NuGet/Home/issues/4435)

- При переносе в PackageRef наблюдается неожиданное поведение функции восстановления гибридных решений — [4433](https://github.com/NuGet/Home/issues/4433)

- При выполнении построения вскоре после запуска операции NuGet (установка, обновление, восстановление) возможно зависание VS — [4420](https://github.com/NuGet/Home/issues/4420)

- Зависание пользовательского интерфейса — взаимоблокировка при инициализации NuGet.SolutionRestoreManager.RestoreManagerPackage — [4371](https://github.com/NuGet/Home/issues/4371)

- Команда add package должна добавлять версию в качестве атрибута вместо элемента — [4325](https://github.com/NuGet/Home/issues/4325)

- dotnet restore foo.sln — сбой в случаях, когда конфигурации в SLN приводит к дублированию проектов в графе восстановления с разными конфигурациями — [4316](https://github.com/NuGet/Home/issues/4316)

- Пакеты только с содержимым — [3668](https://github.com/NuGet/Home/issues/3668)

- Отказ по умолчанию от параметра селектора формата пакета — [4468](https://github.com/NuGet/Home/issues/4468)

- Производительность: CreateUAP_CSharp_VS.01.1. Время создания проекта Duration_TotalElapsedTime ухудшилось на 3153,570 мс (149,1 %). Базовая версия 26129.02 — [4452](https://github.com/NuGet/Home/issues/4452)

- Производительность: для решения ManagedLangs_CS_DDRIT.0300. Время повторного построения Duration_TotalElapsedTime ухудшилось на 1,5 с. Базовая версия 26105 — [4441](https://github.com/NuGet/Home/issues/4441)

- Сбой заявки в проектах с несколькими моникерами целевой платформы — [4419](https://github.com/NuGet/Home/issues/4419)

- Производительность: WebForms_DDRIT.1200. Время закрытия решения VM_ImagesInMemory_Total_devenv ухудшилось на 3,000 значения счетчика (0,5 %). Базовая версия 26123.04 — [4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback — предупреждения упаковки при нацеливании на netcoreapp1.1 — [4397](https://github.com/NuGet/Home/issues/4397)

- Исключение PathTooLongException при попытке добавить пакет NuGet в пустое веб-приложение ASP.NET Core — [4391](https://github.com/NuGet/Home/issues/4391)

- Упаковка выполняется слишком часто — команда dotnet pack завершается сбоем при наличии циклической зависимости в целевом графе зависимостей, включающем целевую операцию упаковки — [4381](https://github.com/NuGet/Home/issues/4381)

- Упаковка выполняется слишком часто — при создании пакета NuGet не включаются все конфигурации — [4380](https://github.com/NuGet/Home/issues/4380)

- Исключение NullReferenceException при добавлении nuget с packageref в проект C++ — [4378](https://github.com/NuGet/Home/issues/4378)

- Специальные возможности: экранный диктор не воспроизводит название флажка, позволяющего выбрать проекты, в которые требуется установить пакет — [4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 периодически не может подключиться к веб-каналам VSO/VSTS — ошибка VS 365798 — [4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles выводит данные в неверное расположение, если PackagePath задает путь в виде "contentFiles" — [4348](https://github.com/NuGet/Home/issues/4348)

- При упаковке целевого объекта добавляется свойство PackageVersion с VersionSuffix — [4324](https://github.com/NuGet/Home/issues/4324)

- Не удается указать путь к пакету при использовании dotnet pack — [4321](https://github.com/NuGet/Home/issues/4321)

- NuGet выводит серию предупреждений о повторяющихся операциях импорта во время восстановления — [4304](https://github.com/NuGet/Home/issues/4304)

- Диалоговое окно для выбора формата диспетчера пакетов NuGet плохо выглядит при установке темной темы — [4300](https://github.com/NuGet/Home/issues/4300)

- Сбой VS при восстановлении сборки — [4298](https://github.com/NuGet/Home/issues/4298)

- Взаимоблокировка Visual Studio при добавлении моникера целевой платформы в targetframeworks, сохранении и последующем выполнении перестроения. 10 % времени — [4295](https://github.com/NuGet/Home/issues/4295)

- nuget pack не выводит сообщение об успехе в случае успешной упаковки проекта — [4294](https://github.com/NuGet/Home/issues/4294)

- PackTask завершается сбоем из-за того, что не удается найти System.IO.Compression 4.1 — [4290](https://github.com/NuGet/Home/issues/4290)

- Упаковка выполняется слишком часто — PackTask часто завершается сбоем из-за конфликтов при доступе к файлу — [4289](https://github.com/NuGet/Home/issues/4289)

- NuGet открывает окно вывода во время фонового восстановления — [4274](https://github.com/NuGet/Home/issues/4274)

- Исключение ServiceProvider как потенциально опасного шаблона написания кода (может приводить к зависаниям) — [4268](https://github.com/NuGet/Home/issues/4268)

- Производительность или зависание пользовательского интерфейса — повышение производительности считывания DownloadTimeoutStream — [4266](https://github.com/NuGet/Home/issues/4266)

- Взаимоблокировка Visual Studio при попытке закрыть проект до завершения операции восстановления NuGet — [4257](https://github.com/NuGet/Home/issues/4257)

- Проблемы с PackTask и упаковкой — `.nuspec` - [4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Не удается разрешить пакеты nuget для нового проекта (требуется перезапуск Visual Studio) — [4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] Раскрывающийся список "Версия", в котором отображаются доступные версии пакета, плохо синхронизируется с выбранным пакетом nuGet... — [4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client должен использовать CPS JoinableTaskFactory при взаимодействии с CPS для предотвращения взаимоблокировок — [4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 не распаковывает `.targets` из пакета — [4171](https://github.com/NuGet/Home/issues/4171)

- dotnet pack не поддерживает заголовок в `.csproj` - [4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package приводит к появлению диалогового окна ошибки в версии VS2017 RC — [4127](https://github.com/NuGet/Home/issues/4127)

- Не работает обновление пакета для проекта .Net Core, поскольку пользовательский интерфейс не получает обновление CPS из назначения. - [4035](https://github.com/NuGet/Home/issues/4035)

- Предупреждение об улучшении неразрешенных ссылок — [3955](https://github.com/NuGet/Home/issues/3955)

- dotnet pack — ProjectReference теряет сведения о версии — [3953](https://github.com/NuGet/Home/issues/3953)

- Общее ухудшение времени создания и повторного построения проекта приложения для универсальной платформы Windows — [3873](https://github.com/NuGet/Home/issues/3873)

- Сообщение об успешном восстановлении отображается даже при возникновении ошибок в процессе восстановления. - [3799](https://github.com/NuGet/Home/issues/3799)

- Повторная публикация Nuget.CommandLine 3.4.4 на веб-сайте Nuget.org — [2931](https://github.com/NuGet/Home/issues/2931)

- При переносе проекты изменяются с `project.json` на `.csproj` — восстановление завершается сбоем — [4297](https://github.com/NuGet/Home/issues/4297)

- Сбой при восстановлении только что созданного тестового проекта xunit — [4296](https://github.com/NuGet/Home/issues/4296)

- При открытии проектов Core возможно зависание пользовательского интерфейса — [4269](https://github.com/NuGet/Home/issues/4269)

- Исправление файла целевых объектов для задач построения — [4267](https://github.com/NuGet/Home/issues/4267)

- Список ошибок содержит ошибку после построения решения, которое выгружает указанный по ссылке проект — [4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: целевой объект "_GenerateRestoreGraphProjectEntry" не существует в проекте. - [4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: пользовательский интерфейс диспетчера nuget для решения завершает работу со сбоем при выборе всех проектов — [4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath завершается сбоем при наличии конечного знака косой черты — [4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: операция восстановления NuGet выдает несколько предупреждений о ссылке на проект для проекта LinqToTwitter — [4156](https://github.com/NuGet/Home/issues/4156)

- При упаковке из `.csproj` не включается атрибут minClientVersion — [4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll поставляется с отложенной подписью в VS2017 (d15rel 26014.00) — [4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: восстановление завершается сбоем для проекта VS 2015, созданного с помощью CMake 3.7.1 — [4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: ошибки восстановления могут скрывать более полные сообщения об ошибках, которые могут выдаваться при построении — [4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Ошибка при восстановлении пакетов NuGet для проекта веб-сайта: значение не может быть null. - [4092](https://github.com/NuGet/Home/issues/4092)

- Операция переноса вызывает исключение ссылки на объект в NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker — [4067](https://github.com/NuGet/Home/issues/4067)

- Команда dotnet pack должна выполнять упаковку средств с версиями, для которых было выполнено построение пакета — [4063](https://github.com/NuGet/Home/issues/4063)

- Новая операция фонового восстановления записывает в строку состояния значение в миллисекундах, тогда как восстановление занимает секунды — [4036](https://github.com/NuGet/Home/issues/4036)

- Опечатка в сообщении о сбое при разрешении всех ссылок проекта —[4018](https://github.com/NuGet/Home/issues/4018)

- Включение рабочих процессов PCM в сценариях ссылок на пакет —[4016](https://github.com/NuGet/Home/issues/4016)

- Не удается найти установленные пакеты в пользовательском интерфейсе диспетчера пакетов — [4015](https://github.com/NuGet/Home/issues/4015)

- dotnet pack завершается сбоем при пустом PackagePath —[3993](https://github.com/NuGet/Home/issues/3993)

- Задача восстановления завершается сбоем в многопользовательском сценарии — [3897](https://github.com/NuGet/Home/issues/3897)

- Не удается изменить тип содержимого при упаковке с использованием задачи упаковки NuGet — [3895](https://github.com/NuGet/Home/issues/3895)

- Неверная копия по умолчанию ContentFiles для MsBuild /t:pack — [3894](https://github.com/NuGet/Home/issues/3894)

- При восстановлении установки пакета в журналах дублируется сообщение о восстановлении пакетов — [3785](https://github.com/NuGet/Home/issues/3785)

- Снятие защитных функций — восстановление раздела сред выполнения должно применяться только к текущему проекту — [3768](https://github.com/NuGet/Home/issues/3768)

- Задача упаковки помещает файлы содержимого одновременно в "content/" и "contentFiles/" — [3718](https://github.com/NuGet/Home/issues/3718)

- dotnet pack3 выполняет дополнительное разделение тегов — [3701](https://github.com/NuGet/Home/issues/3701)

- dotnet pack: упаковка проектов с использованием ссылок на проекты приводит к дублированию предупреждения об импорте — [3665](https://github.com/NuGet/Home/issues/3665)

- Не всегда отображается журнал восстановления в VS — [3633](https://github.com/NuGet/Home/issues/3633)

- В тексте справки по локальным компонентам nuget по-прежнему упоминается кэш пакетов — [3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 связывает PackageReferences с TargetFrameworks. - [3504](https://github.com/NuGet/Home/issues/3504)

- Nuget выбирает неожиданную версию MSBuild в командной строке разработчика VS "15", предварительная версия 4 — [3408](https://github.com/NuGet/Home/issues/3408)

- Запись файлов целевых объектов или свойств при завершившемся сбоем восстановлении — [3399](https://github.com/NuGet/Home/issues/3399)

- NuGet во время восстановления не учитывает те же оболочки совместимости, что и MSBuild при выполнении в командной строке VS 15 — [3387](https://github.com/NuGet/Home/issues/3387)

- Повторное включение PackFromProjectWithDevelopmentDependencySet для VS15 — [3272](https://github.com/NuGet/Home/issues/3272)

- Проблемы с Blend при работе с NuGet — [4043](https://github.com/NuGet/Home/issues/4043)

- Интеграция версии 4.0.0.2067 в репозитории интерфейса командной строки и SDK для поставки вместе с RC2 — [4029](https://github.com/NuGet/Home/issues/4029)

- VS зависает при создании нового консольного приложения Core, закрытии решения, а также открытии и закрытии решения — [4008](https://github.com/NuGet/Home/issues/4008)

- Зависание при открытии проекта d15prerel.25916.01 — [3982](https://github.com/NuGet/Home/issues/3982)

- Исправление сообщения в справке и документации по dotnet и локальным компонентам nuget.exe — [3919](https://github.com/NuGet/Home/issues/3919)

- Проверка PackTask на наличие проблем, связанных с начальным или конечным пробелом — [3906](https://github.com/NuGet/Home/issues/3906)

- dotnet pack выполняет упаковку из obj, а не из bin — [3880](https://github.com/NuGet/Home/issues/3880)

- dotnet pack всегда присваивает ProjectReference версию 1.0.0 — [3874](https://github.com/NuGet/Home/issues/3874)

- dotnet pack завершается сбоем со ссылками на проект и <TargetFramework> - [3865](https://github.com/NuGet/Home/issues/3865)

- Исключение LockRecursionException в ProjectSystemCache.TryGetProjectNameByShortName — [3861](https://github.com/NuGet/Home/issues/3861)

- Обрезка пробелов из свойств MSBuild — [3819](https://github.com/NuGet/Home/issues/3819)

- Объединение двух событий проекта, возникающих при загрузке проекта — [3759](https://github.com/NuGet/Home/issues/3759)

- Библиотеки P2P в файле `project.assets.json` файл имеют неправильную версию — [3748](https://github.com/NuGet/Home/issues/3748)

- Восстановление завершается сбоем из-за отсутствия ответа веб-канала и недоступности пакета — [3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe может зависнуть при большом объеме выходных данных ошибки MSBuild — [3572](https://github.com/NuGet/Home/issues/3572)

- Задача восстановления при построении для Blend завершается сбоем в первый раз и успешно выполняется во второй (исправлен сценарий для VS) — [2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>Запросы на изменение структуры

- перенос vsix из v2 vsix в v3 vsix — [4196](https://github.com/NuGet/Home/issues/4196)

- NuGet должен предусматривать механизм получения пути к файлу блокировки в MSBuild — [3351](https://github.com/NuGet/Home/issues/3351)

- Добавление ресурсов построения в проверку совместимости моникера целевой платформы и файл ресурсов — [3296](https://github.com/NuGet/Home/issues/3296)

- Определение нового объекта ProjectCapability "Pack" в целевых объектах упаковки для реализации связанных с пакетом возможностей — [4146](https://github.com/NuGet/Home/issues/4146)

- Запуск пакета в качестве целевого объекта после построения с условием на основе свойства MSBuild "GeneratePackageOnBuild" — [4145](https://github.com/NuGet/Home/issues/4145)

- Использование свойства NuGet RestoreProjectStyle для создания отдельных проектов NuGet — [4134](https://github.com/NuGet/Home/issues/4134)

- Адаптивное восстановление для изменений переходных ссылок проекта — [4076](https://github.com/NuGet/Home/issues/4076)

- Добавление свойств NuGet в целевой файл для проектов, не предназначенных для универсальной платформы Windows — [4030](https://github.com/NuGet/Home/issues/4030)

- Поддержка TargetPlatformVersion для универсальной платформы Windows — [3923](https://github.com/NuGet/Home/issues/3923)

- Передача метаданных ссылок проекта в систему проектов NuGet — [3922](https://github.com/NuGet/Home/issues/3922)

- Добавление пользовательского интерфейса для режима упаковки — [3921](https://github.com/NuGet/Home/issues/3921)

- Для прежних версий `.csproj` требуется установка NugetTargetMoniker и RuntimeIdentifiers в proj/targets — [3854](https://github.com/NuGet/Home/issues/3854)

- Установка пакета может перекрываться с автоматическим восстановлением — [3836](https://github.com/NuGet/Home/issues/3836)

- Контекстное меню QueryStatus не появляется в том случае, если не загружен VSPackage — [3835](https://github.com/NuGet/Home/issues/3835)

- Для операций восстановления решения и сборки диалоговое окно по-прежнему отображается — [3789](https://github.com/NuGet/Home/issues/3789)

- Изоляция версии VSSDK при построении решения NuGet.Clients — [3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Ссылки на проблемы GitHub, исправленные в версии RTM
[Список проблем 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[Список проблем 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[Список проблем 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[Список проблем 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[Список проблем 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")
