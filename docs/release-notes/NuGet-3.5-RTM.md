---
title: Заметки о выпуске версии-кандидата 3.5
description: Заметки о выпуске NuGet 3,5, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776350"
---
# <a name="nuget-35-release-notes"></a>Заметки о выпуске NuGet 3,5

[NuGet 3,5 — заметки о](../release-notes/nuget-3.5-RC.md)  |  ВЫпуске RC [Заметки о выпуске для версии-кандидата NuGet 4,0](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Исправления ошибок

* Пакет не использует MSBuild 14,1 на Mono- [#3550](https://github.com/NuGet/Home/issues/3550)

* На вкладке "обновление" не выбирается последняя доступная версия для обновления вместо выбора текущей установленной версии — [#3498](https://github.com/NuGet/Home/issues/3498)

* Устраните сбой после проверки подлинности закрытого веб-канала MyGet v2 и выбора команды "отобразить дополнительные результаты x" — [#3469](https://github.com/NuGet/Home/issues/3469)

* Сообщения журнала, как кажется, находятся в порядке, соответствующем пользовательскому интерфейсу [#3446](https://github.com/NuGet/Home/issues/3446)

* v 3.4.4. при восстановлении NuGet создается сообщение о том, что формат данного пути не поддерживается — [#3442](https://github.com/NuGet/Home/issues/3442)

* Для NuGet cmdLine 3,6 Beta не учитывается-Prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)

* Неиквмная установка NuGet в больших проектах — [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe обновление — самостоятельное обновление [#3395](https://github.com/NuGet/Home/issues/3395)

* 3,5. Установка и восстановление из общего UNC-ресурса имеет регрессию производительности от 3.4.4 [#3355](https://github.com/NuGet/Home/issues/3355)

* Ошибка при установке MOQ из пользовательского интерфейса управления пакетами для проекта net451 — [#3349](https://github.com/NuGet/Home/issues/3349)

* Вкладка "установить" на уровне решения не отображает версию пакета [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` обновление с установленной вкладки теряет состояние [#3303](https://github.com/NuGet/Home/issues/3303)

* Пакет NuGet On `.csproj` игнорирует пустой элемент Files в `.nuspec` file- [#3257](https://github.com/NuGet/Home/issues/3257)

* Проекты веб-сайтов, размещенные в IIS, не должны вызывать сбой при восстановлении [#3235](https://github.com/NuGet/Home/issues/3235)

* Учетные данные не получены из Nuget.Config при перенаправлении конечных точек v3 в v2- [#3179](https://github.com/NuGet/Home/issues/3179)

* Пакету NuGet не удается разрешить сборку при получении метаданных переносимой сборки — [#3128](https://github.com/NuGet/Home/issues/3128)

* NuGet не удается найти `msbuild.exe` на Mono- [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe Pack не допускает предварительной версии тега, начинающегося с Numbers- [#1743](https://github.com/NuGet/Home/issues/1743)

* Сбой установки пакета NuGet в VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)

* фильтр Алловедверсионс не работает на уровне решения — [#333](https://github.com/NuGet/Home/issues/333)

* Случайное восстановление завершается ошибкой, если уже был добавлен элемент с тем же ключом. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Не удается установить NuGet. Common в `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* При использовании пользовательского интерфейса для поиска источника v2 Финдпаккажесбид вызывается дважды для каждого идентификатора — [#2517](https://github.com/NuGet/Home/issues/2517)

* Пакеты не могут зависеть от проектов — [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe Pack-исключение документировано, но не поддерживается — [#2284](https://github.com/NuGet/Home/issues/2284)

* Проблемы с сообщениями об ошибках при недопустимых разделах "contentFiles" `.nuspec` — [#1686](https://github.com/NuGet/Home/issues/1686)

* Push-уведомления всегда отправляет весь пакет дважды с аутентифицированными источниками пакетов — [#1501](https://github.com/NuGet/Home/issues/1501)

* При вызове nuget.exe обновить *. csproj не было указано никаких сведений, а в проекте нет `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` При восстановлении не выполняется повторная попытка выполнения кодов состояния 5xx из источников v2. [#1217](https://github.com/NuGet/Home/issues/1217)

* Двойная точка в файле src в `.nuspec` не работает — [#2947](https://github.com/NuGet/Home/issues/2947)

* Для восстановления CoreCLR необходимо игнорировать потоки с шифрованием [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe обработки Push 403 — неправильный запрос учетных данных [#2910](https://github.com/NuGet/Home/issues/2910)

* Обновление NuGet с помощью диспетчера пакетов удаляет свойства из `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet. PackageManagement. VisualStudio пытается загрузить "NuGet. TeamFoundationServer14", но имя этой библиотеки DLL изменилось на "NuGet. TeamFoundationServer" — [#2857](https://github.com/NuGet/Home/issues/2857)

* В пользовательском интерфейсе диспетчера пакетов не отображается только что обновленная версия — [#2828](https://github.com/NuGet/Home/issues/2828)

* Update — пакет пытается использовать PackageID, Version вместо Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771)

* Если в проекте не используется NuGet ( `packages.config` или `project.json` ) — [#2766](https://github.com/NuGet/Home/issues/2766)

* Ошибка TFS "[файл] не найдена в рабочей области, или у вас нет разрешения на доступ к нему" во время обновления или удаления, если решение или проект привязаны к системе управления версиями TFS — [#2739](https://github.com/NuGet/Home/issues/2739)

* пакет обновления не получает зависимости для нецелевых пакетов — [#2724](https://github.com/NuGet/Home/issues/2724)

* Невозможно задать уровень детализации журналов для действий пользовательского интерфейса диспетчера пакетов NuGet — [#2705](https://github.com/NuGet/Home/issues/2705)

* Недопустимая конфигурация NuGet — Visual Studio 2015 VSIX (v 3.4.3) — [#2667](https://github.com/NuGet/Home/issues/2667)

* Дефаултпушсаурце в `NuGetDefaults.Config` ( `ProgramData\NuGet` ) не работает — [#2653](https://github.com/NuGet/Home/issues/2653)

* выпуск NuGet 3.4.3 — получение значения не может быть NULL в сборке пакета — [#2648](https://github.com/NuGet/Home/issues/2648)

* RESTORE не использует сохраненные учетные данные из Nuget.Config для веб-каналов VSTS — [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--ConfigFile относится к папке проекта, а не к командлету dir- [#2639](https://github.com/NuGet/Home/issues/2639)

* Избыточное выделение в коде версии компарсион — [#2632](https://github.com/NuGet/Home/issues/2632)

* Несколько экземпляров nuget.exe пытаются установить один и тот же пакет параллельно, вызывает двойную запись [#2628](https://github.com/NuGet/Home/issues/2628)

* Сведения о зависимостях не кэшируются для операций с несколькими проектами. [#2619](https://github.com/NuGet/Home/issues/2619)

* Установите и обновите Скачанные пакеты, не проверяя папку Packages First — [#2618](https://github.com/NuGet/Home/issues/2618)

* Если список источников пакетов пуст, невозможно добавить источник пакетов через пользовательский интерфейс (NuGet 3.4. x) — [#2617](https://github.com/NuGet/Home/issues/2617)

* Ошибка при попытке установить пакет, зависящий от интерфейсов времени разработки, [#2594](https://github.com/NuGet/Home/issues/2594)

* Установка пакета из консоли PackageManager с параметром "ALL" пытается только первый источник — [#2557](https://github.com/NuGet/Home/issues/2557)

* Последняя бета-версия не распаковка Модернхттпклиент- [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 сбой при запуске с помощью самосозданного 3.4.1 NuGet- [#2419](https://github.com/NuGet/Home/issues/2419)

* Команда Update может быть более подробной, если я запросил это так...- [#2418](https://github.com/NuGet/Home/issues/2418)

* Локально построенное расширение VSIX должно иметь те же файлы и библиотеки DLL, что и сборка CI. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Исправление предупреждений о понижении NuGet в сборке — [#2396](https://github.com/NuGet/Home/issues/2396)

* Проверка подлинности источника пакета (3 раза) заблокирована бессрочно [#2362](https://github.com/NuGet/Home/issues/2362)

* Содержимое пакета не восстанавливается надлежащим образом при установке пакета из канала NuGet v 3.3 + с аргументом-with, если пакет содержит `.nupkg` файлы — [#2354](https://github.com/NuGet/Home/issues/2354)

* Установка NuGet со всеми источниками пакетов, но пакет отсутствует в 1 источник, сбой [#2322](https://github.com/NuGet/Home/issues/2322)

* [Перфватсон] Уиделай: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. Всмсбуилднужетпрожектсистем + * lt; &gt; c__DisplayClass_0 + &lt; &lt; AddReference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)

* Установка блокируется, если один источник не проходит авторизацию [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` диапазон версий должен переопределять Инклудереференцедпрожектс Version- [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package "очень медленный" — "попытка собрать сведения о зависимостях" — [#1909](https://github.com/NuGet/Home/issues/1909)

* Пакет NuGet скрытый переход на более раннюю версию при обновлении зависимостей пакетом [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe обновление удаляет строгое имя сборки и частный атрибут. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Относительный путь к файлу для "Дефаултпушсаурце" — [#1746](https://github.com/NuGet/Home/issues/1746)

* Улучшение сообщений об ошибках сопоставителя — [#1373](https://github.com/NuGet/Home/issues/1373)

* Обновление-пакет в v3 завершается сбоем с пакетами, отсутствующими в указанном источнике, [#1013](https://github.com/NuGet/Home/issues/1013)

* Использование относительных путей для источников пакетов является проблемой при использовании [#865](https://github.com/NuGet/Home/issues/865)

* Отсутствует зависимость в NUPKG-файле, созданном из проекта, если косвенная зависимость уже существует с требованием более ранней версии [#759](https://github.com/NuGet/Home/issues/759)

* При удалении проекта закрывается соответствующее окно пользовательского интерфейса, но Переименование проекта не приводит к переименованию окна пользовательского интерфейса. Обратите внимание, что PMC прослушивает события переименования проекта и удаления проекта — [#670](https://github.com/NuGet/Home/issues/670)

* [Веб-Рабочая нагрузка виллов] Создание "зависаний" для Razor V3 WSP- [#3241](https://github.com/NuGet/Home/issues/3241)

* Установка или восстановление определенного пакета завершается сбоем с "пакетом содержит несколько файлов nuspec". - [#3231](https://github.com/NuGet/Home/issues/3231)

* Строчные коды & `packages.config` сценарии — [#3209](https://github.com/NuGet/Home/issues/3209)

* [3,5 — бета-версия] При восстановлении пакета не удается восстановить "устаревшие" пакеты — [#3208](https://github.com/NuGet/Home/issues/3208)

* пакет NuGet принудительно добавляет TT-файлы в папку содержимого независимо от того, что [#3203](https://github.com/NuGet/Home/issues/3203)

* Обновление-пакет для веб-приложения ASP.NET создает предупреждение, связанное с файлом: source- [#3194](https://github.com/NuGet/Home/issues/3194)

* `project.json`Если в JSON-файле нет паккоптионс и владельца, то пакет NuGet Pack CSPROJ (с) завершается сбоем. [#3180](https://github.com/NuGet/Home/issues/3180)

* пакет NuGet для `project.json` игнорирует теги паккоптионс, такие как Summary, authors, Owners и т. д. [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException через NuGet. Packaging. Фисикалпаккажефиле. Вышестояще- [#3160](https://github.com/NuGet/Home/issues/3160)

* Пакет NuGet игнорирует зависимости в выходных данных `.nuspec` для `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Обновление нескольких пакетов с помощью отката оставляет проект в неработающем состоянии — [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles не добавляются для проектов netstandard — [#3118](https://github.com/NuGet/Home/issues/3118)

* Не удалось правильно упаковать библиотеку .NET Standard, [#3108](https://github.com/NuGet/Home/issues/3108)

* Файл-> создание проекта > библиотеки классов (переносимые) в VS2015 и Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* Ошибка nuGet-1.0.0-* не является допустимой строкой версии — [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package не удается отобразить, но Install-Package Works — [#3068](https://github.com/NuGet/Home/issues/3068)

* Ошибка при выполнении установки-пакета jQuery. Validation на dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* пакет NuGet для xproj по умолчанию имеет недопустимый целевой путь — [#3060](https://github.com/NuGet/Home/issues/3060)

* При установке VS 2015 с обновлением 3 на VS, использующем NuGet версии 3.5.0, возникает ошибка. [#3053](https://github.com/NuGet/Home/issues/3053)

* "Заблокировано packages.config" в `project.json` проекте (UWP, a. k. сборка интегрирована) — [#3046](https://github.com/NuGet/Home/issues/3046)

* Обновите интерфейс командной строки DotNet, установленный сценарием сборки, на preview2-003121, который является официальной сборкой preview2. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Пользовательский интерфейс диспетчера пакетов: не отображает новую версию после обновления пакета [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey при удалении Командная строка не считывается и не отправляется в 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Неправильная строка: стабильный выпуск пакета не должен иметь предварительную зависимость. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Кэш Оптимизедзиппаккаже оставляет пустые папки — [#3029](https://github.com/NuGet/Home/issues/3029)

* Создание исключения для получения Нуллреф проекта PCL (net46 и Windows 10). - [#3014](https://github.com/NuGet/Home/issues/3014)

* Обновление NuGet должно предоставлять информативное сообщение, если более поздняя версия ограничена ограничением Алловедверсионс- [#3013](https://github.com/NuGet/Home/issues/3013)

* Проблемы с восстановлением NuGet v3 — [#2891](https://github.com/NuGet/Home/issues/2891)

* Подключаемый модуль учетных данных завершил работу с ошибкой 1/ошибка при скачивании пакета при использовании поставщиков учетных данных с несколькими источниками [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` Восстановление NuGet вызывает повторную компиляцию при отсутствии изменений [#2817](https://github.com/NuGet/Home/issues/2817)

* Пакеты символов не следует использовать при установке или обновлении — [#2807](https://github.com/NuGet/Home/issues/2807)

* VS не поддерживает переменные среды в Репоситорипас (nuget.exe) — [#2763](https://github.com/NuGet/Home/issues/2763)

* Пометка элементов UIElement без метки в пользовательском интерфейсе диспетчера пакетов для специальных возможностей — [#2745](https://github.com/NuGet/Home/issues/2745)

* Переносные платформы с профилем переноса переносов отклоняются. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Диспетчер пакетов NuGet должен очистить, что список параметров в сведениях о пакетах не применяется к `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe принудительная отправка или удаление не использует ключ API — [#2627](https://github.com/NuGet/Home/issues/2627)

* Удалите свойство locked из файла блокировки — [#2379](https://github.com/NuGet/Home/issues/2379)

* Сбой обновления 3.3.0 NuGet с "дополнительным ограничением... определено в packages.config не разрешает эту операцию. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* При установке пакета из локального источника, который не существует, выдается фиктивное сообщение — [#1674](https://github.com/NuGet/Home/issues/1674)

* В фильтре "обновление доступно" отображаются обновления, нарушающие ограничение версии — [#1094](https://github.com/NuGet/Home/issues/1094)

* Не удалось обновить собственные пакеты — [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Компоненты

* Поддержка установки свойства CopyLocal в значение false для ссылок, добавляемых NuGet- [#329](https://github.com/NuGet/Home/issues/329)

* Поддержка nuget.exe для MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)

* Поддержка Pack для.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Отключить действие пользователя при выполнении действий пользователя — [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet должен добавить поддержку для `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Добавлена совместимость платформы в NuGet 2. x (которые уже находятся в 3. x) — [#2720](https://github.com/NuGet/Home/issues/2720)

* Поддержка резервных папок пакетов — [#2899](https://github.com/NuGet/Home/issues/2899)

* Разработайте и реализуйте понятие типа пакета для поддержки пакетов средств — [#2476](https://github.com/NuGet/Home/issues/2476)

* Добавьте API, чтобы получить путь к папке глобальных пакетов — [#2403](https://github.com/NuGet/Home/issues/2403)

* Включение SemVer 2.0.0 в пакетной [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>Запросы на изменение структуры

* nuget.exe параметр времени ожидания push-уведомлений не работает [#2785](https://github.com/NuGet/Home/issues/2785)

* Текст описания пакета должен быть выбираемым [#1769](https://github.com/NuGet/Home/issues/1769)

* Разрешить nuget.exe создавать `.props` и `.targets` файлы для `.nuproj` проектов [#2711](https://github.com/NuGet/Home/issues/2711)

* Добавление API расширяемости для сравнения платформ с помощью Imports- [#2633](https://github.com/NuGet/Home/issues/2633)

* Скрывать параметры зависимости при использовании `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Вывод заголовка nuget.exe версии в подробных выходных данных — [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet должен уведомить пользователей о том, что обновление или установка в PCL TFM на основе библиотеки, может вызвать проблемы. [#3138](https://github.com/NuGet/Home/issues/3138)

* Предупреждать о неправильной установке или обновлении для проекта w/TFM = "DotNet" — [#3137](https://github.com/NuGet/Home/issues/3137)

* Устранение проблем с производительностью с помощью сопоставителя и NuGet для обновления [#3044](https://github.com/NuGet/Home/issues/3044)

* Добавление поддержки netcoreapp11 и netstandard17 — [#2998](https://github.com/NuGet/Home/issues/2998)

* Использование атрибута AssemblyMetadata для `.nuspec` замены токенов — [#2851](https://github.com/NuGet/Home/issues/2851)
