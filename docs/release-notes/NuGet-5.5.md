---
title: Заметки о выпуске NuGet 5,5
description: Заметки о выпуске NuGet 5,5, включая новые функции, исправления ошибок и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780104"
---
# <a name="nuget-55-release-notes"></a>Заметки о выпуске NuGet 5,5

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio| Доступно в пакетах SDK для .NET|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019, версия 16.5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core

## <a name="summary-whats-new-in-55"></a>Сводка: новые возможности в 5,5

* Улучшена поддержка специальных возможностей и средств чтения с экрана для пользовательского интерфейса диспетчера пакетов NuGet в Visual Studio
    * Проблемы специальных возможностей в средствах чтения с экрана, отсутствует Алттекст и доступное имя для установленного текстового поля и т. д., [#9059](https://github.com/NuGet/Home/issues/9059)
    * Проблемы специальных возможностей в интерфейсе чтения с экрана в списке пакетов — [#9077](https://github.com/NuGet/Home/issues/9077)
    * Проблемы специальных возможностей в средствах чтения с экрана, связанные с вкладками "Обзор", "установить", "Обновить" — [#9078](https://github.com/NuGet/Home/issues/9078)
    * Программа "Экранный диктор" не объявляет "пустое", "нет ДепенденЦиес", "нужет. org", метку ссылки MIT [#9157](https://github.com/NuGet/Home/issues/9157)

* Поддержка автономных значков отображая в пользовательском интерфейсе диспетчера пакетов Visual Studio для пакетов, размещенных в локальных веб-каналах. [#8189](https://github.com/NuGet/Home/issues/8189)

* Значительно улучшена производительность восстановления без операций с использованием `RestoreUseStaticGraphEvaluation` , что ускоряет вычисление за счет вызова интерфейсов API статических графов MSBuild — [8791](https://github.com/NuGet/Home/issues/8791)

* Повышение надежности dotnet.exe с помощью подключаемых модулей межплатформенной проверки подлинности
    * Сбой dotnet restore с Таскканцеледексцептион- [#7842](https://github.com/NuGet/Home/issues/7842)
    * Подключаемый модуль: "задача отменена" — проблема с проверкой подлинности ADO по этой причине. - [#8528](https://github.com/NuGet/Home/issues/8528)

* Добавление `dotnet nuget <add|remove|update|disable|enable|list> source` команды [#4126](https://github.com/NuGet/Home/issues/4126)

* Поддержка для `--skip-duplicate`  использования команды DotNet NuGet Push- [#8778](https://github.com/NuGet/Home/issues/8778)

* Поддержка `packages.config` с помощью MSBuild/Restore- [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Ошибки**

* Переработайте Self-Updater с помощью API V3 — [#4197](https://github.com/NuGet/Home/issues/4197)

* Неправильная версия зависимости пакета, если для версии зависимости пакета задано значение "*" — [#6697](https://github.com/NuGet/Home/issues/6697)

* Сообщение об ошибке Еррорунсафепаккажеентри не указывает на источник проблемы — [#7505](https://github.com/NuGet/Home/issues/7505)

* Файл блокировки не учитывается в сценариях "*" — [#8073](https://github.com/NuGet/Home/issues/8073)

* NuGet.exe не разрешается в последнюю версию пакета при использовании * в PackageReference (восстановление MSBuild/DotNet/VS) — [#8432](https://github.com/NuGet/Home/issues/8432)

* пакет списка DotNet с несколькими нацеливанием на проект WPF — [#8463](https://github.com/NuGet/Home/issues/8463)

* Улучшение Конкурренциутилитиес (сокращение загрузки ЦП) — [#8653](https://github.com/NuGet/Home/issues/8653)

* Спецификация разгрузки для выгруженных сценариев проекта не должна быть создана в предварительном восстановлении — [#8793](https://github.com/NuGet/Home/issues/8793)

* Пакеты NuGet Visual Studio (RestoreManagerPackage) должны быть автоматической загрузкой событий сборки решения — [#8796](https://github.com/NuGet/Home/issues/8796)

* Блокировка в процессе инициализации VSSettings- [#8842](https://github.com/NuGet/Home/issues/8842)

* Панель элементов VisualStudio не заполняется из пакета NuGet, если проект помещен в папку решения — [#8868](https://github.com/NuGet/Home/issues/8868)

* VS: бессрочный сбой восстановления решения из-за состояния гонки — [#8881](https://github.com/NuGet/Home/issues/8881)

* Константа "Загрузка.." на вкладке "установленные" и "Поиск <term>.. "на вкладке" обновления "— [#8890](https://github.com/NuGet/Home/issues/8890)

* Отсутствие внедренных значков в пользовательском интерфейсе VS PM после истечения срока действия кэша — [#9069](https://github.com/NuGet/Home/issues/9069)

* Запуск пользовательского интерфейса Фиреандфоржет PM — [#9112](https://github.com/NuGet/Home/issues/9112)

* Восстановление: недопустимая реализация Инклудиксклудефилес. Equals (...) — [#9167](https://github.com/NuGet/Home/issues/9167)

* RESTORE: Паккажеспек. Clone () создает неравенство клона- [#9211](https://github.com/NuGet/Home/issues/9211)

* Отображается список ошибок, хотя флажок "всегда показывать список ошибок, если сборка завершается с ошибками" не установлен — [#8190](https://github.com/NuGet/Home/issues/8190)

* Статическое восстановление графа не должно передавать пустое SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061)

* Восстановление: время, вычисленное для каждого проекта 4 раз, [#9042](https://github.com/NuGet/Home/issues/9042)

* RESTORE: Депенденциграфспек. Load (...) не требует JObject- [#9040](https://github.com/NuGet/Home/issues/9040)

* Восстановление: большие строки, созданные в куче больших объектов (LOH) — [#9031](https://github.com/NuGet/Home/issues/9031)

* Пользовательские nuget.exe на более поздние версии Mono могут быть нарушены из-за сопоставителя пакета SDK для MSBuild — [8848](https://github.com/NuGet/Home/issues/8848)

* Восстановление завершается сбоем, если nuget.dgspec.js"используется другим процессом"- [8692](https://github.com/NuGet/Home/issues/8692)

**Запросы на изменение структуры**

* Логика в _GetRestoreProjectStyle должна быть в задаче [#8804](https://github.com/NuGet/Home/issues/8804)

* По умолчанию на вкладке "установленные" добавьте сведения об устаревании, [#8541](https://github.com/NuGet/Home/issues/8541)

**[Список всех проблем, исправленных в этом выпуске — 5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
