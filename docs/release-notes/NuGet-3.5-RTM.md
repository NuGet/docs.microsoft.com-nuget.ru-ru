---
title: Заметки о выпуске NuGet 3.5 Beta
description: Заметки о выпуске для NuGet 3.5, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550688"
---
# <a name="nuget-35-release-notes"></a>Заметки о выпуске NuGet 3.5 выпуска

[Заметки о выпуске NuGet 3.5 RC выпуска](../release-notes/nuget-3.5-RC.md) | [заметки о выпуске версии-Кандидата NuGet 4.0](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Исправления ошибок

* Пакет не использует 14,1 MSBuild в mono — [#3550](https://github.com/NuGet/Home/issues/3550)

* Вкладка обновления не выделяет последней доступной версии для обновления. Вместо этого выберите установку текущей версии - [#3498](https://github.com/NuGet/Home/issues/3498)

* После проверки подлинности закрытый версии 2, веб-канал MyGet и нажатия кнопки «Показать x дополнительные результаты», решающее проблему сбоя- [#3469](https://github.com/NuGet/Home/issues/3469)

* Сообщения журнала, по-видимому, являются в обратном порядке для пользовательского интерфейса - [#3446](https://github.com/NuGet/Home/issues/3446)

* V3.4.4 - восстановление Nuget выдает «данный формат пути не поддерживается» - [#3442](https://github.com/NuGet/Home/issues/3442)

* Бета-версия NuGet cmdLine 3.6 не учитывает - Prop конфигурации = выпуска - [#3432](https://github.com/NuGet/Home/issues/3432)

* Установка NuGet IKVM медленно на большого проекта - [#3428](https://github.com/NuGet/Home/issues/3428)

* NuGet.exe - Self отслеживает на самостоятельное обновление - обновление [#3395](https://github.com/NuGet/Home/issues/3395)

* 3,5 установки или восстановления из общей папки в формате UNC имеет производительность регрессии из 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Ошибка при установке Moq из пакета управления пользовательского интерфейса для проекта net451 - [#3349](https://github.com/NuGet/Home/issues/3349)

* Вкладке установки на уровне решения не отображается версия пакета - [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` обновление вкладку "установлено" теряет состояние - [#3303](https://github.com/NuGet/Home/issues/3303)

* Пакет NuGet на `.csproj` игнорирует элемент пустые файлы в `.nuspec` файл — [#3257](https://github.com/NuGet/Home/issues/3257)

* Проекты веб-сайта, размещенного в службах IIS не вызывает сбой - восстановления [#3235](https://github.com/NuGet/Home/issues/3235)

* Учетные данные не получены из Nuget.Config, когда конечная точка v3 перенаправляет до версии 2 - [#3179](https://github.com/NuGet/Home/issues/3179)

* Не удается разрешить сборку при получении метаданных переносимая сборка — пакет NuGet [#3128](https://github.com/NuGet/Home/issues/3128)

* Не удается найти NuGet `msbuild.exe` в Mono — [#3085](https://github.com/NuGet/Home/issues/3085)

* пакет NuGet.exe не допускает тег предварительной версии, который начинается с номера - [#1743](https://github.com/NuGet/Home/issues/1743)

* Установка пакета NuGet завершается сбоем в VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions фильтрации не работы на уровне решения - [#333](https://github.com/NuGet/Home/issues/333)

* Восстановление случайно завершается ошибкой с элемента с тем же ключом уже добавлен. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Не удается установить Nuget.Common в `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* При использовании пользовательского интерфейса для поиска источника V2, FindPackagesById вызывается дважды для каждого идентификатора - [#2517](https://github.com/NuGet/Home/issues/2517)

* Пакеты не может зависеть от проектов — [#2490](https://github.com/NuGet/Home/issues/2490)

* пакет NuGet.exe - Exclude является задокументированы, но не поддерживается - [#2284](https://github.com/NuGet/Home/issues/2284)

* Проблемы с ошибкой сообщения, если раздел «contentFiles» `.nuspec` недопустимый — [#1686](https://github.com/NuGet/Home/issues/1686)

* Push-уведомлений всегда отправляет весь пакет дважды с проверкой подлинности источники пакетов - [#1501](https://github.com/NuGet/Home/issues/1501)

* Сведения не был задан при вызове nuget.exe *.csproj обновления во время выполнения проекта не поддерживает `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` Восстановление не пытается повторно на кодах состояния 5xx из источников V2 - [#1217](https://github.com/NuGet/Home/issues/1217)

* Две точки в файле src в `.nuspec` не работает — [#2947](https://github.com/NuGet/Home/issues/2947)

* CoreCLR восстановления необходимо игнорировать каналов с использованием шифрования - [#2942](https://github.com/NuGet/Home/issues/2942)

* NuGet.exe push 403 обработки - неправильно запроса учетных данных — [#2910](https://github.com/NuGet/Home/issues/2910)

* Обновление диспетчера пакетов для NuGet удаляет свойства из `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* Попробуйте загрузить «NuGet.TeamFoundationServer14», но что имя DLL-Библиотеки изменено на «NuGet.TeamFoundationServer» - NuGet.PackageManagement.VisualStudio [#2857](https://github.com/NuGet/Home/issues/2857)

* Вновь не отображает пользовательский Интерфейс диспетчера пакетов обновленная версия - [#2828](https://github.com/NuGet/Home/issues/2828)

* пакет обновления пытается использовать в качестве ИД пакета версии вместо package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* csproj восстановления NuGet должна ошибка, если проект не использует nuget (`packages.config` или `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* Ошибка TFS «[файл] не удалось найти в рабочей области, или у вас нет разрешения на доступ к нему» во время обновления или удаления, когда решение или проект привязан к системе управления версиями TFS - [#2739](https://github.com/NuGet/Home/issues/2739)

* пакет обновления не получить зависимости для пакетов без целевого - [#2724](https://github.com/NuGet/Home/issues/2724)

* Невозможно задать уровень детализации журналов для действия пользовательского интерфейса диспетчера пакетов Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)

* Недопустимая конфигурация NuGet - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource в `NuGetDefaults.Config` (`ProgramData\NuGet`) не работает — [#2653](https://github.com/NuGet/Home/issues/2653)

* версия NuGet 3.4.3 - получении значения не может быть null при построении пакета - [#2648](https://github.com/NuGet/Home/issues/2648)

* Восстановление не использует сохраненные учетные данные из Nuget.Config для веб-каналов VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--configfile задается относительно dir проекта вместо cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)

* Чрезмерное выделение ресурсов в код версии сравнение - [#2632](https://github.com/NuGet/Home/issues/2632)

* Несколько экземпляров nuget.exe установке же пакета в параллельных приводит к возникновению double запись — [#2628](https://github.com/NuGet/Home/issues/2628)

* Сведения о зависимостях не кэшируется для операции с несколькими проектами — [#2619](https://github.com/NuGet/Home/issues/2619)

* Устанавливать и обновлять пакеты загрузки, не проверяя папке packages - [#2618](https://github.com/NuGet/Home/issues/2618)

* Если список источников пакетов пуста, невозможно добавить источник пакета с помощью пользовательского интерфейса (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Вводящая в заблуждение ошибка при попытке установить пакет, который зависит от времени разработки интерфейсов - [#2594](https://github.com/NuGet/Home/issues/2594)

* Установка пакета из консоли PackageManager с параметром «All» пытается только первый источник - [#2557](https://github.com/NuGet/Home/issues/2557)

* Последнюю бета-версию не распаковке ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* Visual Studio 2015 о сбоях при запуске в автоматически созданном NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Команда обновления может выглядеть более описательны в том случае, если я попросил его быть Итак … - [#2418](https://github.com/NuGet/Home/issues/2418)

* VSIX, созданного локально должны иметь те же библиотеки DLL и файлов, как сборка непрерывной Интеграции. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Устранить предупреждения понижения NuGet в сборке - [#2396](https://github.com/NuGet/Home/issues/2396)

* Не удается выполнить проверку источника пакета (3 раза) блокируется навсегда - [#2362](https://github.com/NuGet/Home/issues/2362)

* Содержимое пакета не восстанавливается правильно при установке пакета из nuget версии 3.3 + веб-канала с аргументом - NoCache Если пакет содержит `.nupkg` файлы — [#2354](https://github.com/NuGet/Home/issues/2354)

* Ошибка установки NuGet в все источники пакетов, но в пакете отсутствуют из источника 1, - [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Установить блоки, если один источник отказывает в авторизации - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` диапазон должен переопределить - IncludeReferencedProjects version — версия [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package очень медленно — «попытка собрать данные о зависимостях» - [#1909](https://github.com/NuGet/Home/issues/1909)

* Вогнутая возврат к предыдущей версии NuGet пакета, когда пакета обновление его зависимостей - [#1903](https://github.com/NuGet/Home/issues/1903)

* NuGet.exe обновления удаляет строгое имя сборки и закрытый атрибут. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Относительный путь к файлу для «DefaultPushSource» - [#1746](https://github.com/NuGet/Home/issues/1746)

* Улучшения сообщений о сбое Сопоставитель - [#1373](https://github.com/NuGet/Home/issues/1373)

* пакет обновления в версии 3 завершается сбоем с пакетами не в указанном источнике - [#1013](https://github.com/NuGet/Home/issues/1013)

* Использование относительных путей для источников пакета трудно используйте параметр - [#865](https://github.com/NuGet/Home/issues/865)

* Отсутствует зависимость в NUPKG-файл, созданный из проекта, если уже существует косвенная зависимость с нижней требование к версии - [#759](https://github.com/NuGet/Home/issues/759)

* Удаление проекта закроется соответствующее окно пользовательского интерфейса, но Переименование проекта не приводит к переименованию окна пользовательского интерфейса. Обратите внимание, что PMC прослушивает переименования проекта и события удаления проекта - [#670](https://github.com/NuGet/Home/issues/670)

* [Рабочая нагрузка Willow] Создание Razor v3 WSP зависает - [#3241](https://github.com/NuGet/Home/issues/3241)

* Установка и восстановление определенного пакета завершается с «Пакет содержит несколько файлов nuspec.» - [#3231](https://github.com/NuGet/Home/issues/3231)

* Нижний регистр идентификаторов & `packages.config` сценариев - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5 beta2] Восстановление пакетов не сможет восстановить пакеты «устаревшего» - [#3208](https://github.com/NuGet/Home/issues/3208)

* пакет NuGet принудительно добавляет tt-файлов в папку content, независимо от того, что - [#3203](https://github.com/NuGet/Home/issues/3203)

* Обновление веб-приложения ASP.NET создает предупреждение, связанные с файлом: источник — [#3194](https://github.com/NuGet/Home/issues/3194)

* csproj пакет NuGet (с `project.json`) вызывает сбой, если нет packOptions и владельца в файле JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* пакет NuGet для `project.json` игнорирует теги packOptions Сводка, авторы, владельцы д - [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException через NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* Пакет NuGet игнорирует зависимости в выходных данных `.nuspec` для `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Обновление нескольких пакетов с откатом оставляет проект в поврежденном состоянии - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles при любом не добавляются для проектов netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Невозможно упаковать библиотеки, предназначенные для .net Standard правильно - [#3108](https://github.com/NuGet/Home/issues/3108)

* Файл "->" новый проект "->" происходит сбой проекта библиотеки классов (переносимая) в Visual Studio 2015 и Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Ошибка NuGet — 1.0.0-* не является допустимой строкой версии - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package не отображается, однако работает Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Ошибка при «Install-Package jquery.validation» в dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* пакет NuGet xproj по умолчанию будет выбран недопустимый целевой путь — [#3060](https://github.com/NuGet/Home/issues/3060)

* При установленной Visual STUDIO 2015 с обновлением 3 на виртуальном СЕРВЕРЕ, используемые NuGet, возникает ошибка версии 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* «Заблокирован, packages.config» `project.json` (UWP, называемые также построения интегрированных) проект - [#3046](https://github.com/NuGet/Home/issues/3046)

* Обновите cli dotnet, устанавливаемая скрипт сборки для имеет предварительную версию 2-003121, — это сборка официальный имеет предварительную версию 2. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Пользовательский Интерфейс диспетчера пакетов: не отображает новой версии после обновления пакета- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey в командной строке удаления не чтения/отправляется в 3.5.0 бета-версии - [#3037](https://github.com/NuGet/Home/issues/3037)

* Неправильная строка: стабильный выпуск пакета не должен зависеть предварительной зависимость. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Кэш OptimizedZipPackage оставляет пустые папки - [#3029](https://github.com/NuGet/Home/issues/3029)

* Создание проекта переносимой библиотеки Классов (net46 и windows 10), get исключение NullRef. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Обновления NuGet должен предоставить информационное сообщение, если более поздней версии ограничивается ограничению allowedVersions — [#3013](https://github.com/NuGet/Home/issues/3013)

* Проблемы восстановления NuGet v3 - [#2891](https://github.com/NuGet/Home/issues/2891)

* Подключаемый модуль учетных данных завершил работу с ошибкой -1 / произошла ошибка при загрузке пакета при использовании поставщиков учетных данных с несколькими источниками - [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` Восстановление NuGet вызвала перекомпиляцию при ничего не изменено - [#2817](https://github.com/NuGet/Home/issues/2817)

* Никогда не следует пакетов символов используется в установке или обновлении - [#2807](https://github.com/NuGet/Home/issues/2807)

* VS не поддерживает переменные среды в repositoryPath (nuget.exe делает) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Метка без метки UIElements в пользовательском Интерфейсе диспетчера пакетов для объекта специальных возможностей - [#2745](https://github.com/NuGet/Home/issues/2745)

* Переносимые платформы с дефисами профили, будут отклонены. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Диспетчер пакетов NuGet должны содержаться этого списка параметры в пакетах, подробно не применяется к `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet.exe Push-уведомлений, удаление не будет использовать ключ API - [#2627](https://github.com/NuGet/Home/issues/2627)

* Удалите заблокированного свойства из файла блокировки - [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0, происходит сбой обновления с помощью "... дополнительное ограничение определенных в packages.config предотвращает эту операцию." - [#1816](https://github.com/NuGet/Home/issues/1816)

* При установке пакета из локального источника, который не существует вызывает исключение поддельное сообщение - [#1674](https://github.com/NuGet/Home/issues/1674)

* «Доступно обновление». отображаются обновления, которые нарушают ограничение по версии - [#1094](https://github.com/NuGet/Home/issues/1094)

* Не удалось обновить собственные пакеты - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Функции

* Поддерживает значение false для параметра CopyLocal для ссылок, добавленные NuGet — [#329](https://github.com/NuGet/Home/issues/329)

* NuGet.exe поддержка MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)

* Пакет поддержки.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Отключение действий пользователя при наличии выполняемой действий пользователя- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet должны обеспечить поддержку для `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Добавление совместимости framework, отсутствующих в NuGet 2.x (который уже 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Поддержка папки резервной пакета - [#2899](https://github.com/NuGet/Home/issues/2899)

* Разрабатывать и реализовывать понятие типа пакета для поддержки пакетов средство — [#2476](https://github.com/NuGet/Home/issues/2476)

* Добавление API для получения пути к папке установки глобальных пакетов - [#2403](https://github.com/NuGet/Home/issues/2403)

* Включить SemVer 2.0.0 в пакет — [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>Запросы на изменение структуры

* NuGet.exe push - параметр времени ожидания не работает — [#2785](https://github.com/NuGet/Home/issues/2785)

* Текст описания пакета будут доступны для выбора - [#1769](https://github.com/NuGet/Home/issues/1769)

* Включить nuget.exe для создания `.props` и `.targets` файлы для `.nuproj` проекты [#2711](https://github.com/NuGet/Home/issues/2711)

* Добавление расширения API для сравнения платформ с imports - [#2633](https://github.com/NuGet/Home/issues/2633)

* Скрыть параметры зависимости при использовании `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Вывод заголовка версии nuget.exe в подробные выходные данные — [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet требуются, чтобы пользователи знали, что обновление или установка в dotnet моникера целевой платформы на основе переносимой библиотеки Классов может привести к ошибкам - [#3138](https://github.com/NuGet/Home/issues/3138)

* Предупреждение bad установку или обновление для проекта с tfm = «dotnet» - [#3137](https://github.com/NuGet/Home/issues/3137)

* Устранение проблем производительности с ReShaper и NuGet для обновления - [#3044](https://github.com/NuGet/Home/issues/3044)

* Добавление поддержки netcoreapp11 и netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Используйте атрибут AssemblyMetadata для `.nuspec` маркер замены - [#2851](https://github.com/NuGet/Home/issues/2851)
