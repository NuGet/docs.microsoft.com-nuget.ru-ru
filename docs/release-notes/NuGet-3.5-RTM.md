---
title: Заметки о выпуске бета-версии 3.5 NuGet
description: Заметки о выпуске для NuGet 3.5, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdb540229cae0e6e952ac2a0c00c8801ccbbb28d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822595"
---
# <a name="nuget-35-release-notes"></a>Заметки о выпуске 3.5 NuGet

[Заметки о выпуске 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md) | [заметки о выпуске версии-Кандидата NuGet 4.0](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Исправления ошибок

* Пакет не использует 14,1 MSBuild на моно - [#3550](https://github.com/NuGet/Home/issues/3550)

* Обновление не установите последнюю версию вместо этого обновите выберите текущую установленную версию - [#3498](https://github.com/NuGet/Home/issues/3498)

* Устраните сбой после проверки подлинности закрытый v2 веб-канал MyGet и нажмите кнопку «Показать x больше результатов»- [#3469](https://github.com/NuGet/Home/issues/3469)

* Сообщения журнала, кажется в обратном порядке для пользовательского интерфейса - [#3446](https://github.com/NuGet/Home/issues/3446)

* вызывает восстановление Nuget v3.4.4 - «данный формат пути не поддерживается» - [#3442](https://github.com/NuGet/Home/issues/3442)

* Бета-версии cmdLine 3.6 NuGet не учитывает - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)

* Установка NuGet IKVM медленно на большого проекта - [#3428](https://github.com/NuGet/Home/issues/3428)

* NuGet.exe - Self сохраняет на самостоятельное обновление - обновление [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 установки или восстановления из общего ресурса UNC имеет производительность регрессии из 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Ошибка при установке заказа из пакета управления пользовательского интерфейса для проекта net451 - [#3349](https://github.com/NuGet/Home/issues/3349)

* Вкладка установки на уровне решений не отображается версия пакета — [#3339](https://github.com/NuGet/Home/issues/3339)

* компилируемых `project.json` "Обновить" на вкладку "установлено" теряет состояние - [#3303](https://github.com/NuGet/Home/issues/3303)

* Пакет NuGet на `.csproj` игнорирует элемент пустые файлы в `.nuspec` файл - [#3257](https://github.com/NuGet/Home/issues/3257)

* Проекты веб-сайтов, размещенных в IIS не должны быть причиной восстановления к сбою - [#3235](https://github.com/NuGet/Home/issues/3235)

* Учетные данные не извлечен из Nuget.Config, когда конечная точка v3 перенаправляет v2 - [#3179](https://github.com/NuGet/Home/issues/3179)

* Не удается разрешить сборку при получении метаданных сборки переносимой - пакет NuGet [#3128](https://github.com/NuGet/Home/issues/3128)

* Не удается найти NuGet `msbuild.exe` на моно - [#3085](https://github.com/NuGet/Home/issues/3085)

* пакет NuGet.exe не разрешается использовать тег предварительного выпуска, который начинается с цифры - [#1743](https://github.com/NuGet/Home/issues/1743)

* Установка пакета NuGet не выполняется на VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* значение allowedVersions фильтрации не работы на уровне решений - [#333](https://github.com/NuGet/Home/issues/333)

* Восстановление случайно завершается ошибкой с элемента с тем же ключом уже был добавлен. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Не удается установить Nuget.Common в `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* При использовании пользовательского интерфейса для поиска источника V2, FindPackagesById вызывается дважды для каждого идентификатора - [#2517](https://github.com/NuGet/Home/issues/2517)

* Пакеты не могут зависеть от проектов - [#2490](https://github.com/NuGet/Home/issues/2490)

* пакет NuGet.exe - задокументированы но не поддерживается Exclude - [#2284](https://github.com/NuGet/Home/issues/2284)

* Сообщения проблемы с ошибкой, если раздел «contentFiles» `.nuspec` недопустимый — [#1686](https://github.com/NuGet/Home/issues/1686)

* Принудительная всегда отправляет весь пакет дважды с проверкой подлинности источники пакетов - [#1501](https://github.com/NuGet/Home/issues/1501)

* Нет данных был задан при вызов nuget.exe *.csproj обновления во время выполнения проекта не поддерживает `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` Восстановление не пытается повторно на коды состояния 5xx из источников V2 - [#1217](https://github.com/NuGet/Home/issues/1217)

* Двумя точками в файл src в `.nuspec` не работает — [#2947](https://github.com/NuGet/Home/issues/2947)

* Восстановление CoreCLR необходимо игнорировать веб-каналы с шифрованием - [#2942](https://github.com/NuGet/Home/issues/2942)

* NuGet.exe push 403 обработки - неправильно запроса учетных данных — [#2910](https://github.com/NuGet/Home/issues/2910)

* Диспетчер пакетов NuGet обновления удаляет свойства из `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* Попробуйте загрузить «NuGet.TeamFoundationServer14», но что имя DLL-файла изменено на «NuGet.TeamFoundationServer» - NuGet.PackageManagement.VisualStudio [#2857](https://github.com/NuGet/Home/issues/2857)

* Диспетчер пакетов пользовательского интерфейса не показывает только что обновленную версию - [#2828](https://github.com/NuGet/Home/issues/2828)

* пакет пытается использовать в качестве ИД пакета обновления версии вместо package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* csproj восстановления NuGet должна ошибки, если в проекте не с помощью nuget (`packages.config` или `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* Ошибка TFS «[файл] быть не найден в рабочей области или у вас разрешения на доступ к нему» во время обновления или удаления, когда решение или проект привязан к системе управления версиями TFS - [#2739](https://github.com/NuGet/Home/issues/2739)

* пакет обновления не получить зависимости для пакетов без целевого - [#2724](https://github.com/NuGet/Home/issues/2724)

* Невозможно задать уровень детализации журналов для действия пользовательского интерфейса диспетчера пакетов Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)

* Недопустимая конфигурация NuGet - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource в `NuGetDefaults.Config` (`ProgramData\NuGet`) не работает — [#2653](https://github.com/NuGet/Home/issues/2653)

* версия NuGet 3.4.3 - получении значения не может быть null при построении пакета - [#2648](https://github.com/NuGet/Home/issues/2648)

* Восстановление не использует сохраненные учетные данные из Nuget.Config для веб-каналов VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet восстановления]--configfile задается относительно dir проекта вместо cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)

* Чрезмерное выделения в код сравнения версии - [#2632](https://github.com/NuGet/Home/issues/2632)

* Несколько экземпляров nuget.exe установке же пакета в параллельных приводит к возникновению двойные запись — [#2628](https://github.com/NuGet/Home/issues/2628)

* Сведения о зависимостях не кэшируется для операций с несколькими проектами - [#2619](https://github.com/NuGet/Home/issues/2619)

* Установка и загрузка пакетов обновления, не проверяя «пакеты» - [#2618](https://github.com/NuGet/Home/issues/2618)

* Если список источников пакетов пуста, невозможно добавить источника пакета при помощи пользовательского интерфейса (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Ввести в заблуждение ошибка при попытке установить пакет, который зависит от роли внешних разработки - [#2594](https://github.com/NuGet/Home/issues/2594)

* Установка пакета в консоли PackageManager с параметр «All» пытается первого источника - [#2557](https://github.com/NuGet/Home/issues/2557)

* Последняя бета-версии не распаковки ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 сбоя при запуске с собственной сборки NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Команда обновления может быть более подробных сведений, если они требуются перезагрузку.. - i [#2418](https://github.com/NuGet/Home/issues/2418)

* VSIX, созданного локально должны иметь те же библиотеки DLL и файлов как сборки CI. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Устранить предупреждения переход к более раннему NuGet в построении - [#2396](https://github.com/NuGet/Home/issues/2396)

* Не пройдет проверку подлинности источника пакета (3 раза) блокируется навсегда - [#2362](https://github.com/NuGet/Home/issues/2362)

* Содержимое пакета не является правильно восстановить при установке пакета из nuget v3.3 + веб-канала с аргументом - NoCache Если пакет содержит `.nupkg` файлы - [#2354](https://github.com/NuGet/Home/issues/2354)

* Ошибка установки NuGet в все источники пакетов, но отсутствующие на 1 источник пакета — [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Установить блоки, если один источник отказывает в авторизации - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` диапазон, должны переопределять версия - IncludeReferencedProjects - версии [#1983](https://github.com/NuGet/Home/issues/1983)

* Пакет обновления super медленно — «попытка собрать информацию о зависимостях» - [#1909](https://github.com/NuGet/Home/issues/1909)

* Вогнутая возврат к предыдущей версии NuGet пакета при пакетное обновление зависимостям - [#1903](https://github.com/NuGet/Home/issues/1903)

* NuGet.exe обновления удаляет строгое имя сборки и атрибут Private. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Относительный путь к файлу для «DefaultPushSource» - [#1746](https://github.com/NuGet/Home/issues/1746)

* Улучшения сообщений о сбое Сопоставитель - [#1373](https://github.com/NuGet/Home/issues/1373)

* пакет обновления в версии 3 завершается пакеты не в указанном источнике - [#1013](https://github.com/NuGet/Home/issues/1013)

* Использование относительных путей для источников пакетов, затруднительно для использования - [#865](https://github.com/NuGet/Home/issues/865)

* Отсутствует зависимость в NUPKG-файла, созданного из проекта, если уже существует косвенная зависимость с нижней требование к версии - [#759](https://github.com/NuGet/Home/issues/759)

* При удалении проекта закрывает соответствующее окно пользовательского интерфейса, но Переименование проекта не приводит к переименованию окно пользовательского интерфейса. Обратите внимание, что PMC прослушивает переименования проекта и удаление событий проекта - [#670](https://github.com/NuGet/Home/issues/670)

* [Willow рабочая нагрузка] Создание Razor v3 WSP зависает - [#3241](https://github.com/NuGet/Home/issues/3241)

* Установки или восстановления определенного пакета завершается с «Пакет содержит несколько nuspec-файлов». - [#3231](https://github.com/NuGet/Home/issues/3231)

* Нижний регистр идентификаторов & `packages.config` сценарии - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5 beta2] Восстановление пакетов не удается восстановить пакеты «устаревшего» - [#3208](https://github.com/NuGet/Home/issues/3208)

* пакет NuGet принудительно добавляет tt-файлы в папку контента, независимо от того, что - [#3203](https://github.com/NuGet/Home/issues/3203)

* Обновление веб-приложения ASP.NET приводит к возникновению предупреждения, относящиеся к файлу: источника — [#3194](https://github.com/NuGet/Home/issues/3194)

* csproj пакет NuGet (с `project.json`) аварийно завершает работу при наличии не packOptions и владельцем в файле JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* пакет NuGet для `project.json` игнорирует теги packOptions Сводка, авторов, владельцев и т. д - [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException через NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* Пакет NuGet не учитывает зависимости в выходных данных `.nuspec` для `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Обновление нескольких пакетов с помощью отката оставляет проект в поврежденном состоянии - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles при выполнении любого не добавляются для проектов моникеров netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Невозможно упаковать библиотеки, предназначенные для .net Standard правильно - [#3108](https://github.com/NuGet/Home/issues/3108)

* Файл -> Новый проект библиотеки классов (переносимая) проекта завершается с ошибкой VS2015 и Dev15 - "->" [#3094](https://github.com/NuGet/Home/issues/3094)

* Ошибка nuGet - 1.0.0-* не является допустимой строкой версии - [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package не отображается, однако works Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Ошибка при «Install-Package jquery.validation» на dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* пакет NuGet компилируемых по умолчанию будет выбран недопустимый целевой путь - [#3060](https://github.com/NuGet/Home/issues/3060)

* При установленной VS 2015 с обновлением 3 на виртуальном СЕРВЕРЕ, используемые NuGet, возникает ошибка версии 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* «Заблокирован packages.config» `project.json` (UWP, называемые также построения интеграции) проект - [#3046](https://github.com/NuGet/Home/issues/3046)

* Обновите cli dotnet установленные скрипт построения для preview2 003121, являющегося официальным preview2 сборки. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Пакет пользовательского интерфейса диспетчера: не отображает новые версии после обновления пакета- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey в командной строке удаления не чтения и отправляется в 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Неправильная строка: стабильный выпуск пакета не должен зависеть предварительной зависимостей. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Кэш OptimizedZipPackage оставляет пустой папки - [#3029](https://github.com/NuGet/Home/issues/3029)

* Создание проекта PCL (net46 и windows 10) get NullRef исключение. - [#3014](https://github.com/NuGet/Home/issues/3014)

* NuGet обновления должен предоставить информационное сообщение, когда более поздняя версия ограничен ограничением значение allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)

* Проблемы восстановления NuGet v3 - [#2891](https://github.com/NuGet/Home/issues/2891)

* Подключаемый модуль учетных данных завершился с ошибкой -1 / Ошибка загрузки пакета при использовании поставщиков учетных данных с несколькими источниками - [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` Восстановление NuGet вызвала перекомпиляцию, если ничего не изменено - [#2817](https://github.com/NuGet/Home/issues/2817)

* Никогда не следует пакеты символы используются для установки или обновления - [#2807](https://github.com/NuGet/Home/issues/2807)

* VS не поддерживает переменные среды в repositoryPath (nuget.exe делает) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Метка неразмеченных UIElements в пользовательском Интерфейсе диспетчера пакетов для специальных возможностей - [#2745](https://github.com/NuGet/Home/issues/2745)

* Переносимый платформы с дефисами профилей, отклоняются. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Диспетчер пакетов NuGet должны содержаться этого списка параметры в пакетах, подробно не применяется к `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet.exe принудительной или удаления не будет использовать ключ API - [#2627](https://github.com/NuGet/Home/issues/2627)

* Удалите свойство заблокированные из файла блокировки - [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 при попытке установить "дополнительное ограничение... определенные в packages.config предотвращает эту операцию." - [#1816](https://github.com/NuGet/Home/issues/1816)

* Установка пакета из локального источника, не существует вызывает поддельное сообщение — [#1674](https://github.com/NuGet/Home/issues/1674)

* «Доступно обновление» отображаются обновления, которые нарушают ограничения версии - [#1094](https://github.com/NuGet/Home/issues/1094)

* Не удается обновить пакетов машинного кода - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Функции

* Поддерживает настройку CopyLocal значение false для ссылок, добавленные NuGet - [#329](https://github.com/NuGet/Home/issues/329)

* NuGet.exe поддержка MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)

* Пакет поддержки.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Отключить действия пользователя при наличии действия пользователя при выполнении- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet необходимо добавить поддержку для `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Добавить framework совместимости отсутствует в NuGet 2.x (который уже 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Поддержка пакета резервной папки - [#2899](https://github.com/NuGet/Home/issues/2899)

* Разрабатывать и реализовывать понятие типа пакета для поддержки пакетов средство - [#2476](https://github.com/NuGet/Home/issues/2476)

* Добавить API для получения пути к папке глобального пакетов - [#2403](https://github.com/NuGet/Home/issues/2403)

* Включить SemVer 2.0.0 в пакете - [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>Запросы на изменение структуры

* Принудительная, NuGet.exe не работает параметр времени ожидания - [#2785](https://github.com/NuGet/Home/issues/2785)

* Текст описания пакета должно быть доступным для выбора - [#1769](https://github.com/NuGet/Home/issues/1769)

* Включить nuget.exe для создания `.props` и `.targets` файлы для `.nuproj` проекты [#2711](https://github.com/NuGet/Home/issues/2711)

* Добавление расширения API для сравнения платформы с imports - [#2633](https://github.com/NuGet/Home/issues/2633)

* Скрыть параметры зависимостей при использовании `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Распечатать заголовок версии nuget.exe в подробные выходные данные - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet необходимо сообщить пользователям, обновление или установка в tfm dotnet, в основе PCL может привести к ошибкам - [#3138](https://github.com/NuGet/Home/issues/3138)

* Предупреждать неправильный установку или обновление для проекта с tfm = «dotnet» - [#3137](https://github.com/NuGet/Home/issues/3137)

* Устранение проблем с производительностью с ReShaper и NuGet для обработки - [#3044](https://github.com/NuGet/Home/issues/3044)

* Добавление поддержки netcoreapp11 и netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Использование атрибута AssemblyMetadata для `.nuspec` токен замены - [#2851](https://github.com/NuGet/Home/issues/2851)
