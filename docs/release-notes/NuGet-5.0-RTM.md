---
title: Заметки о выпуске NuGet 5,0 RTM
description: Заметки о выпуске NuGet 5,0, включая известные проблемы, исправления ошибок, новые функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 637db1ae128ce020c33e54e56148c848a5f905a5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776228"
---
# <a name="nuget-50-release-notes"></a>Заметки о выпуске NuGet 5,0

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio| Доступно в пакетах SDK для .NET|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core 

<sup>2</sup> Доступно в качестве необязательной установки с помощью Visual Studio 2019 с рабочей нагрузкой .NET Core

## <a name="summary-whats-new-in-50"></a>Сводка: новые возможности в 5,0

* Поддержка восстановления [отфильтрованных решений](/visualstudio/ide/filtered-solutions?view=vs-2019) в Visual Studio 2019 — [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` папка позволяет пакетам транзитно публиковать целевые объекты и свойства в ведущем проекте — [#6091](https://github.com/NuGet/Home/issues/6091)
* Улучшенная поддержка сценариев PackageReference в интерфейсах API IVs NuGet — [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` является устаревшим — [#7928](https://github.com/NuGet/Home/issues/7928)
* Подключаемый модуль поставщика учетных данных поколения 1 был заменен [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) и скоро станет устаревшим — [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Ошибки**

* При выполнении восстановления NoOp Избегайте использования * .dgspec.jsпри записи в каталоге obj — [#7854](https://github.com/NuGet/Home/issues/7854)

* Разрешения для файлов, созданных в ~/.нужет, слишком открыты [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` не работает с источниками, для которых требуется проверка подлинности [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet. VisualStudio. Ивспаккажеинсталлер — вызов в проекте без ссылок на пакеты всегда использует packages.config, даже если значение по умолчанию — PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: сбой повторной установки Update-Package ("не удается найти пакет") в списке пакетов. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Добавьте уведомление третьих сторон в наш репозиторий и VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet. VisualStudio. Ивспаккажеинсталлер. Инсталлпаккаже должен установить последнюю версию, если не задана версия [#7493](https://github.com/NuGet/Home/issues/7493)

* --Интерактивная поддержка для команды DotNet NuGet Push- [#7519](https://github.com/NuGet/Home/issues/7519)

* При восстановлении с файлом блокировки предупреждение NU1603 не должно быть создано. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet не должен печатать путь проекта во время восстановления с минимальным протоколированием [#7647](https://github.com/NuGet/Home/issues/7647)

* --Интерактивная поддержка для команды DotNet Remove Package- [#7727](https://github.com/NuGet/Home/issues/7727)

* Добавление обратной передачи NuGet. Packaging. Core с TypeForwardedTo attr- [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache требуется более короткий путь, чтобы правильно работать [#7770](https://github.com/NuGet/Home/issues/7770)

* Предпочитать путь для обнаружения MSBuild, если пользователь не запросил конкретную версию MSBuild- [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` следует перечислить правильные версии MSBuild — [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet. targets (498, 5): ошибка: не удалось найти часть пути "/ТМП/нужетскратч-on Mono- [#7793](https://github.com/NuGet/Home/issues/7793)

* При восстановлении необязательно перечисление содержимого всех версий пакетов, на которые имеются ссылки, в кэше компьютера — [#7639](https://github.com/NuGet/Home/issues/7639)

* Автоматическое обнаружение MSBuild всегда выбирает 16,0 после установки VS 2019 Preview — [#7621](https://github.com/NuGet/Home/issues/7621)

* пакет DotNet List в решении выводит дублирующиеся записи для платформы [#7607](https://github.com/NuGet/Home/issues/7607)

* Исключение "пустое имя пути незаконно" при вызове Ивспаккажеинсталлер. Инсталлпаккаже для старых проектов и папки пакетов не существует. - [#5936](https://github.com/NuGet/Home/issues/5936)

* MSBuild/t: восстановление с минимальным уровнем детализации должно быть более минимальным [#4695](https://github.com/NuGet/Home/issues/4695)

* Пользовательский интерфейс NuGet в VS "область элементов" имеет нечитаемые вкладки из-за проблем с цветом. [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet. Core & NuGet. Clients License.txt уточнение [#7629](https://github.com/NuGet/Home/issues/7629)

* Инструкция RESTORE не обязательно перечисляет глобальный каталог пакетов при попытке определить тип [#7596](https://github.com/NuGet/Home/issues/7596)

* Ошибки при применении блокировки файлов должны отображаться в список ошибок окне [#7429](https://github.com/NuGet/Home/issues/7429)

* Устранение NuGet.Configпроблем фигурации — [#7326](https://github.com/NuGet/Home/issues/7326)

* Адаптация к MSBuild обновление расположения установки — [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet. Build. Tasks. Pack должен быть зависимостью разработки — [#7249](https://github.com/NuGet/Home/issues/7249)

* Добавить точку расширения пакета для включения отладочных символов — [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` должен сохранять диапазон версий зависимостей в созданном nupkg (даже если используется плавающая версия) — [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore`сбой в источнике, прошедшем проверку подлинности, когда у конфигурации уровня пользователя также есть [#7209](https://github.com/NuGet/Home/issues/7209) источника

* Пакет не должен ограничивать набор Буилдактионс для файлов содержимого — [#7155](https://github.com/NuGet/Home/issues/7155)

* При использовании ProjectReference, который требует, чтобы Ассеттаржетфаллбакк был выполнен, должен предупредить. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Взаимоблокировка из-за проблем с потоками при вызове CPS (Коммонпрожектсистем) — [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` не использует учетные данные из глобальной конфигурации для источника, указанного в файле Local config- [#6935](https://github.com/NuGet/Home/issues/6935)

* Проблемы с потоками при вызове MEF по асинхронным путям кода — [#6771](https://github.com/NuGet/Home/issues/6771)

* Подписывание: ошибка, обнаруженная дважды и без стека вызовов — [#6455](https://github.com/NuGet/Home/issues/6455)

* При установке подписанного пакета с ненадежным сертификатом подписи отображается ошибка — [#6318](https://github.com/NuGet/Home/issues/6318)

* Неправильное восстановление NuGet Нупс, когда 2 проекта совместно используют каталог obj- [#6114](https://github.com/NuGet/Home/issues/6114)

* Не удается использовать PAT с `dotnet restore` пакетами из веб-канала с проверкой подлинности в Linux. [#5651](https://github.com/NuGet/Home/issues/5651)

* Сбой dotnet restore из-за отключенного веб-канала на уровне компьютера — [#5410](https://github.com/NuGet/Home/issues/5410)

**Запросы на изменение структуры**

* Предупреждение о следующем удалении "пакета DotNet project.json"- [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Добавление предупреждения об устаревании для подключаемого модуля учетных данных Gen1. [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Подписывание: включено репозиторий, чтобы требовать проверку клиента каждого пакета в качестве подписывания репозитория с помощью Репоситорисигнатурес/5.0.0 Resource- [#7759](https://github.com/NuGet/Home/issues/7759)

* ограничение числа запросов HTTP на источник с помощью NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet должен ориентироваться на Net472 (чтобы упростить очистку сборки VSIX 16,0). [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: команда Remove Опенпаккажепаже- [#7384](https://github.com/NuGet/Home/issues/7384)

* Преобразование NetCoreApp 3,0 в NetStandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)

* Добавление поддержки netstandard 2.0 в пакеты NuGet. * — [#6516](https://github.com/NuGet/Home/issues/6516)

* Разрешить авторам пакетов определять транзитивное поведение ресурсов сборки — [#6091](https://github.com/NuGet/Home/issues/6091)

* Поддержка функции фильтра решений VS 2019. Также поддерживает проект, не являющийся решением, или выгруженные проекты. Необходимо восстановить полное решение (с помощью CLI или VS), [#5820](https://github.com/NuGet/Home/issues/5820)

* Сборки NuGet 5,0, для которых требуется 4.7.2 .NET (через TFM Change) — [#7510](https://github.com/NuGet/Home/issues/7510)

* Нужетлиценседата из NuGet. Packaging должен быть общедоступным типом. Обновление метаданных лицензий, принимаемых из спдкс. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Удаление устаревших API параметров — [#7294](https://github.com/NuGet/Home/issues/7294)

* Обход времени ожидания восстановления в системах с 1 процессором [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet предпочитает проверку подлинности NTLM, даже если в NuGet.config добавить параметр конфигурации для фильтрации типов проверки подлинности для учетных данных [#5286](https://github.com/NuGet/Home/issues/5286)

* Включение Ембединтероптипес для PackageReference (функция сопоставления Packages.Config) — [#2365](https://github.com/NuGet/Home/issues/2365)

**[Список всех проблем, исправленных в этом выпуске — 5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Сводка. новые возможности в 5.0.2

* Безопасность (при запуске с помощью dotnet.exe или mono.exe) — папка obj должна быть создана с правильными разрешениями [#7908](https://github.com/NuGet/Home/issues/7908)

* Сбой восстановления nuget.exe в Mono/MacOS с настраиваемыми nuget.config и `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Известные проблемы

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Проблема
При использовании dotnet.exe 2.x для восстановления проекта с несколькими целевыми объектами (netcoreapp 1.x и netcoreapp 2.x) резервная папка обрабатывается как веб-канал файла. Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.<br>
#### <a name="workaround"></a>Обходной путь
Отключите использование резервной папки, задав для параметра значение `RestoreAdditionalProjectSources` Nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Используйте это с осторожностью, так как пакеты, которые будут восстановлены из резервной папки, теперь будут скачаны из NuGet.org.