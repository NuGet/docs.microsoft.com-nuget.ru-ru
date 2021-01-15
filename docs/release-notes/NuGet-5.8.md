---
title: Заметки о выпуске NuGet 5,8
description: Заметки о выпуске NuGet 5,8, включая новые функции, исправления ошибок и DCR.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 7f641c669cdb0cc979d698f6b219cbb4f2692a2e
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235754"
---
# <a name="nuget-58-release-notes"></a>Заметки о выпуске NuGet 5,8

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio | Доступно в пакетах SDK для .NET |
|:---|:---|:---|
| [**5,8**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16.8](https://visualstudio.microsoft.com/downloads/) | [5,0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1</sup> установлен с Visual Studio 2019 с рабочей нагрузкой .NET Core
  
> [!NOTE]
> Для Visual Studio 16,8, MSBuild 16,8 и .NET 5,0 требуется NuGet.exe 5,8 или более поздней версии.


## <a name="summary-whats-new-in-58"></a>Сводка: новые возможности в 5,8
🎉 **это первый выпуск, обеспечивающий полную разработку и восстановление для пакетов NuGet, предназначенных для .net 5,0** 🎉

* Ускорение извлечения nupkg с помощью mmap/CreateFileMapping- [#9807](https://github.com/NuGet/Home/issues/9807)

* Отображение сведений об уязвимости пакета в области сведений пакета пользовательского интерфейса диспетчера пакетов — [#9850](https://github.com/NuGet/Home/issues/9850)

* Проверьте подписанные пакеты NuGet с помощью новой [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) команды [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) поддерживает `--prerelease` возможность добавления последней версии пакета, включая предварительные версии [#4699](https://github.com/NuGet/Home/issues/4699)

* Поиск пакетов в CLI с помощью [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) команды [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) команда поддерживает `--verbosity` параметр- [#9600](https://github.com/NuGet/Home/issues/9600)

* Включение оптимизации быстрого восстановления No-Op для проектов на основе CSPROJ, PackageReference в Visual Studio — [#9565](https://github.com/NuGet/Home/issues/9565)

* Операции пользовательского интерфейса диспетчера пакетов на уровне решения, такие как установки пакетов и обновления, 10 раз быстрее [#6010](https://github.com/NuGet/Home/issues/6010)

* Несколько других улучшений производительности NuGet в Visual Studio — [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**DCR**

* .NET 5,0 TFM: правила приоритета платформы — [#9436](https://github.com/NuGet/Home/issues/9436)

* NuGet не должен вычислять точечную версию платформы при синтаксическом анализе TargetFramework- [#9842](https://github.com/NuGet/Home/issues/9842)

* Используйте TargetFrameworkMoniker & Таржетплатформмоникер, чтобы вывести платформы вместо использования отдельных ТФИ, ТФВ, ТПИ, свойств ТПВ — [#9895](https://github.com/NuGet/Home/issues/9895)

* Обновление `GetReferenceNearestTargetFrameworkTask()` для поддержки целевых платформ с платформами (например, NET 5.0-Windows) — [#9894](https://github.com/NuGet/Home/issues/9894)

* API-интерфейсы Visual Studio для .NET 5,0 — [#9650](https://github.com/NuGet/Home/issues/9650)

* Пользовательский интерфейс диспетчера пакетов: операции консолидации или обновления не должны блокироваться из-за ошибок (понижение уровня пакета и т. д.). [#9224](https://github.com/NuGet/Home/issues/9224)

* Функции NuGet должны быть освещены для проектов, имеющих возможность; "PackageReferences" — [#9957](https://github.com/NuGet/Home/issues/9957)

* Отключение No-Op сообщений о восстановлении в Visual Studio — [#6384](https://github.com/NuGet/Home/issues/6384)

**Появились**

* Конструктор Аутпутвиндовтекствритер не должен вызываться в фоновом потоке — [#9764](https://github.com/NuGet/Home/issues/9764)

* Восстановление подписанных пакетов на процессорах с обратным порядком байтов — [#9547](https://github.com/NuGet/Home/issues/9547)

* Аутпутконсолелогжер не должны вызывать методы привязаны в конструкторах MEF — [#9591](https://github.com/NuGet/Home/issues/9591)

* Ошибка в методе NuGet. CommandLine. Console `PrintJustified()` — [#9737](https://github.com/NuGet/Home/issues/9737)

* Утечка памяти пользовательского интерфейса диспетчера пакетов при сборке мусора метаданных пакета из-за неправильной привязки [#9757](https://github.com/NuGet/Home/issues/9757)

* Завершение В Список ошибок при установке подписанного пакета с форматом packages.config в пользовательском интерфейсе диспетчера пакетов не отображается предупреждение — [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet. CommandLine. XPlat не должен иметь общедоступных API- [#9821](https://github.com/NuGet/Home/issues/9821)

* Уменьшение конфликтов ресурсов при загрузке решения из-за блокировки потока потокового пула с `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* При восстановлении из командной строки с несколькими целевыми проектами NuGet должна считывать связанные сведения о целевой платформе из внутренней сборки — [#9869](https://github.com/NuGet/Home/issues/9869)

* Считывание графа идентификаторов среды выполнения через элемент Таржетфрамеворкинформатион — [#9874](https://github.com/NuGet/Home/issues/9874)

* Статическое восстановление графа не согласуется со свойством Кросстаржетинг в сравнении с Visual Studio и регулярным восстановлением MSBuild- [#9881](https://github.com/NuGet/Home/issues/9881)

* В статическом восстановлении графа с несколькими целевыми проектами NuGet должна считывать связанные сведения о целевой платформе из внутренней сборки. - [#9870](https://github.com/NuGet/Home/issues/9870)

* Разрешить `net5.0-platform` загрузку и восстановление проектов в Visual Studio — [#9863](https://github.com/NuGet/Home/issues/9863)

* Отображение разрешенной версии в пользовательском интерфейсе диспетчера пакетов. [#9826](https://github.com/NuGet/Home/issues/9826)

* Пользовательский интерфейс диспетчера пакетов: обозреватель решений не отображает все зависимости пакетов NuGet — [#9898](https://github.com/NuGet/Home/issues/9898)

* Обновление списка лицензий СПДКС — [#9946](https://github.com/NuGet/Home/issues/9946)

* VS 2019 аварийно завершает работу после открытия окна "Управление пакетами NuGet": значок вызывает необработанное исключение в образе конверсио- [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet. Packaging. Извлечение требует ILMerge исключения Newtonsoft.Js[#9966](https://github.com/NuGet/Home/issues/9966)

* Упаковка с Континуепаккингафтерженератингнуспек = false не должна завершаться ошибкой при отсутствии ошибок — [#9786](https://github.com/NuGet/Home/issues/9786)

* Пользовательский интерфейс диспетчера пакетов: значки не инверсируют цвета правильно [#10017](https://github.com/NuGet/Home/issues/10017)

* Неправильные счетчики проектов для обновлений и No-Op проектов при восстановлении [#10026](https://github.com/NuGet/Home/issues/10026)

* Использование `/p:RestoreUseStaticGraphEvaluation=true` Results в значении не может иметь значение NULL — [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` по ошибке использует псевдоним для проектов библиотеки WPF — [#10020](https://github.com/NuGet/Home/issues/10020)

* Пользовательский интерфейс диспетчера пакетов: NullReferenceException при сбое проверки подписи — [#10042](https://github.com/NuGet/Home/issues/10042)

* Кодеспацес: не используйте `object` тип для значений метаданных проекта — [#10055](https://github.com/NuGet/Home/issues/10055)

* Кодеспацес: сохранение источников пакетов в параметрах инструментов приведет к перезаписи учетных данных [#9711](https://github.com/NuGet/Home/issues/9711)


**[Список всех проблем, исправленных в этом выпуске — 5,8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[Список проблем в этом выпуске — 5,8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>Материалы сообщества

Благодарим всех участников, которые помогли сделать эту версию NuGet более Awesome!

|Куда|Вытягивание|Проблемы|
|----|----|----|
[омажид](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | Опечатка в сообщении об ошибке. "администратора" вместо "Administrator" — [#9662](https://github.com/NuGet/Home/issues/9662)
[одалет](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | Требуется описание пакета NuGet с недопустимыми отчетами AssemblyInformationalVersion "- [#5548](https://github.com/NuGet/Home/issues/5548)
[камперсау](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` не учитывает свойства ветви и фиксации — [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | При щелчке кода ню в Visual Studio список ошибок окно должно переходить в https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[чрисмаддокк](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | Используйте "https://" при добавлении нового источника пакетов с помощью параметров Visual Studio — [#9974](https://github.com/NuGet/Home/issues/9974)
[серзок](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` проблемы с производительностью Mono- [#9989](https://github.com/NuGet/Home/issues/9989)
[сомаслевескуе](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | Добавьте TypeConverter для класса Семантикверсион — [#9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>Сводка. новые возможности в 5.8.1

* packages.config package.lock.jsв использует неправильную целевую платформу в 5,8- [#10257](https://github.com/NuGet/Home/issues/10257)

* 5,8 + 16,8 не может разрешать транзитивные зависимости проектов при смешении PackageReference и packages.config- [#10326](https://github.com/NuGet/Home/issues/10326)

**[Список всех проблем, исправленных в этом выпуске — 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[Список фиксаций в этом выпуске — 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>Добро пожаловать на отзыв

Ваши отзывы очень важны для нас.  Если в этом выпуске возникли какие либо проблемы, ознакомьтесь с нашими [проблемами в GitHub](https://github.com/NuGet/Home/issues) и [сообществом разработчиков Visual Studio](https://developercommunity.visualstudio.com/) за существующими проблемами.  При возникновении новых проблем в NuGet сообщите о [проблемах GitHub](https://github.com/NuGet/Home/issues/new).
Чтобы получить общие сведения о проблемах с NuGet, сообщите нам об этом с помощью параметра [сообщить о проблеме](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) в ИЗБРАННОЙ среде IDE в разделе **Справка > сообщить о проблеме**.
