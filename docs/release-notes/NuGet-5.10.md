---
title: Заметки о выпуске NuGet 5,10
description: Заметки о выпуске NuGet 5,10, включая новые функции, исправления ошибок и DCR.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356503"
---
# <a name="nuget-510-release-notes"></a>Заметки о выпуске NuGet 5,10

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio | Доступно в пакетах SDK для .NET |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16,10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> установлен с Visual Studio 2019 с рабочей нагрузкой .NET Core
  
> [!NOTE]
> Для Visual Studio 16,10, MSBuild 16,10 и .NET 5.0.300 + требуется NuGet.exe 5,10 или более поздней версии.

## <a name="summary-whats-new-in-510"></a>Сводка: новые возможности в 5,10

* Подписывание: реализуйте команду DotNet Trusted-Signs- [#8053](https://github.com/NuGet/Home/issues/8053)

* Сделать проверку по умолчанию отключенной в Linux, но включена по умолчанию в Windows — [#10713](https://github.com/NuGet/Home/issues/10713)

* Добавление переменной ENV для проверки подписи пакета в .NET 5 + Linux/MAC- [#10742](https://github.com/NuGet/Home/issues/10742)

* Улучшение установки новой производительности пакета для крупных решений — [#10166](https://github.com/NuGet/Home/issues/10166)

* Добавьте тип проекта `nfproj` в список суппортедпрожектекстенсионс для интерфейса командной строки NuGet. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

* Подавлять <requireLicenseAcceptance> элемент при упаковке проекта [#5133](https://github.com/NuGet/Home/issues/5133)

* [КПВМ] предупреждение о предварительной версии должно отображаться в DotNet CLI- [#10226](https://github.com/NuGet/Home/issues/10226)

* Обновите маркеры цвета фона и переднего плана ПМУИ на Коммондокументколорс- [#10608](https://github.com/NuGet/Home/issues/10608)

* [Ошибка Bash] Ошибка "операция отменена пользователем" отображается в список ошибокном окне при быстром переключении между вкладками в пользовательском интерфейсе PM: [#10671](https://github.com/NuGet/Home/issues/10671)

* Пользовательский интерфейс PM: улучшение производительности установки пакетов на уровне решения — [#10210](https://github.com/NuGet/Home/issues/10210)

* Замена службы Жетсервицеасинк везде в NuGet. Clients — [#3784](https://github.com/NuGet/Home/issues/3784)

* NuGet.exe проблемы с производительностью пакета с `..` относительным путем [#5016](https://github.com/NuGet/Home/issues/5016)

* Производительность пакета NuGet снижается с увеличением уровней в исходных путях — [#5706](https://github.com/NuGet/Home/issues/5706)

* NuGet не выдает ошибку при упаковке nuspec с повторяющимися файлами. - [#6941](https://github.com/NuGet/Home/issues/6941)

* Пакет NuGet "указанное значение DateTimeOffset не может быть преобразовано в метку времени ZIP-файла" — [#7001](https://github.com/NuGet/Home/issues/7001)

* Метки времени файла упакованного пакета сдвигаются по часовому поясу — [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 должен содержать более практичные сведения — [#7696](https://github.com/NuGet/Home/issues/7696)

* [Ошибка Bash] [Сбой теста] Пустой или неправильно сформированный файл блокировки не должен обновляться при запуске "dotnet restore--use-Lock-File--заблокированный режим"- [#8640](https://github.com/NuGet/Home/issues/8640)

* Нужетверсионранже позволяет логически синтаксически неправильные диапазоны для анализа. [#9145](https://github.com/NuGet/Home/issues/9145)

* В пользовательском интерфейсе PM не удается отобразить различимый цвет фона между выбранными и источниками пакетов с наведением. [#9538](https://github.com/NuGet/Home/issues/9538)

* Флажок выбора проектов для установки не читается средством чтения с экрана — [#9578](https://github.com/NuGet/Home/issues/9578)

* Список версий панели сведений выбор по умолчанию должен быть установлен или Латестстабле на вкладках "установленные" и "обновления"- [#9887](https://github.com/NuGet/Home/issues/9887)

* Удаление учетной записи обхода для некоторых пакетов SDK для .NET 5 таржетплатформмоникер ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)

* Проверка NuGet в DotNet слишком тихий [#10316](https://github.com/NuGet/Home/issues/10316)

* Версионранже не удается проанализировать диапазоны из одной цифры — [#10342](https://github.com/NuGet/Home/issues/10342)

* Диспетчер решений VS создает исключение null для во время отладки — [#10352](https://github.com/NuGet/Home/issues/10352)

* Перемещение сообщений об исключениях интерфейса командной строки в строковые файлы ресурсов — [#10392](https://github.com/NuGet/Home/issues/10392)

* Удаление неработающего кода (Табитембуттонаутоматионпир) — [#10435](https://github.com/NuGet/Home/issues/10435)

* Контекстное меню обновления должно перейти к первому выбранному элементу — [#10498](https://github.com/NuGet/Home/issues/10498)

* Сведения о ПМУИе решения перекрываются горизонтальной чертой [#10533](https://github.com/NuGet/Home/issues/10533)

* Подписывание: сведения о первичной подписи не отображаются, когда истек срок действия сертификата и отметка времени без доверия — [#10535](https://github.com/NuGet/Home/issues/10535)

* Отсутствие включенных источников предотвращает отображение пользовательского интерфейса PM [#10541](https://github.com/NuGet/Home/issues/10541)

* Метаданные пакета (сведения, нерекомендуемый) иногда не извлекаются из nuget.org в Кодеспацес- [#10549](https://github.com/NuGet/Home/issues/10549)

* Инициализация ПМУИ завершается с исключением во время сеанса отладки — [#10559](https://github.com/NuGet/Home/issues/10559)

* Восстановление NuGet приводит к сбою проверки целостности пакета в системе с обратным порядком байтов — [#10567](https://github.com/NuGet/Home/issues/10567)

* Вместо Паккагинжексцептион- [#10595](https://github.com/NuGet/Home/issues/10595) создается исключение

* КПВМ — проблемы параллелизма в алгоритме прохода графа — [#10598](https://github.com/NuGet/Home/issues/10598)

* Добавление телеметрии версии для PowerShell для PMC — [#10609](https://github.com/NuGet/Home/issues/10609)

* Повышение производительности Нужетверсион сортировки — [#10611](https://github.com/NuGet/Home/issues/10611)

* В добавлении доверенных подписывающих аргументов есть непоследовательные аргументы — [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v 16.9.0: переключение вкладок в диспетчере пакетов NuGet с "Updates" на "installed" не приводит к обновлению кадра. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Удалите "v" из номера версии в ПМУИ- [#10677](https://github.com/NuGet/Home/issues/10677)

* Инужетпрожектсервице. Жетинсталледпаккажесасинк вызывает исключение перед получением системы проекта CPS предварительного утверждения- [#10681](https://github.com/NuGet/Home/issues/10681)

* Встроенные значки вызывают отказ в доступе из источника "Microsoft Visual Studio автономные пакеты" на вкладке "Обзор" — [#10687](https://github.com/NuGet/Home/issues/10687)

* Инужетпрожектсервице. Жетинсталледпаккажесасинк вызывает исключение, если Мсбуилдпрожектекстенсионспас не задано — [#10739](https://github.com/NuGet/Home/issues/10739)

* "команда DotNet NuGet Remove Source nuget.org" не работает при первом [#10745](https://github.com/NuGet/Home/issues/10745)

* NuGet блокирует поток ThreadPool в асинхронном методе, делая синхронный вызов потока пользовательского интерфейса [#10775](https://github.com/NuGet/Home/issues/10775)

* Сервис — параметры > — строка диспетчера пакетов NuGet > усечена — [#10779](https://github.com/NuGet/Home/issues/10779)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` является неиспользуемым кодом и повредит производительность — [#10790](https://github.com/NuGet/Home/issues/10790)

* Использование внедренного значка в пакетах SDK для NuGet — [#10795](https://github.com/NuGet/Home/issues/10795)

* Обновление списка лицензий СПДКС — [#10806](https://github.com/NuGet/Home/issues/10806)

**[Список всех проблем, исправленных в этом выпуске — 5,10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Список фиксаций в этом выпуске — 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Материалы сообщества

Благодарим всех участников, которые помогли сделать эту версию NuGet более Awesome!

|Куда|Вытягивание|Проблемы|
|----|----|----|
[-Луи-z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | Версионранже не удается проанализировать диапазоны из одной цифры — [#10342](https://github.com/NuGet/Home/issues/10342)
[омажид](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet. build.sh клиента работает [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet. build.sh клиента работает [#10139](https://github.com/NuGet/Home/issues/10139)
[блаккгад](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Производительность пакета NuGet снижается с увеличением уровней в исходных путях — [#5706](https://github.com/NuGet/Home/issues/5706)
[блаккгад](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe проблем с производительностью пакета... относительный путь — [#5016](https://github.com/NuGet/Home/issues/5016)
[Марцин — кристианк](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | КПВМ — проблемы параллелизма в алгоритме прохода графа — [#10598](https://github.com/NuGet/Home/issues/10598)
[жосесимоес](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Добавьте тип проекта нфпрож в список Суппортедпрожектекстенсионс для интерфейса командной строки NuGet. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Добро пожаловать на отзыв

Ваши отзывы очень важны для нас.  Если в этом выпуске возникли какие либо проблемы, ознакомьтесь с нашими [проблемами в GitHub](https://github.com/NuGet/Home/issues) и [сообществом разработчиков Visual Studio](https://developercommunity.visualstudio.com/) за существующими проблемами.  При возникновении новых проблем в NuGet сообщите о [проблемах GitHub](https://github.com/NuGet/Home/issues/new).
Чтобы получить общие сведения о проблемах с NuGet, сообщите нам об этом с помощью параметра [сообщить о проблеме](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) в ИЗБРАННОЙ среде IDE в разделе **Справка > сообщить о проблеме**.
