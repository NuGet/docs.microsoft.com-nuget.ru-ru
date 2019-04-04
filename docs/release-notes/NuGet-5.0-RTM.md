---
title: Заметки о выпуске NuGet 5.0 RTM
description: Заметки о выпуске для NuGet 5.0, включая известные проблемы, исправления ошибок, новые функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921589"
---
# <a name="nuget-50-release-notes"></a>Заметки о выпуске 5.0 NuGet

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio| Доступно в пакетах SDK для .NET|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Версия 16.0 2019 г. Visual Studio](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core 

<sup>2</sup>доступно в виде необязательно установку с помощью Visual Studio 2019 с рабочей нагрузкой .NET Core

## <a name="summary-whats-new-in-50"></a>Сводка: Новые возможности в версии 5.0

* Поддержка восстановления [отфильтрованные решения](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) в Visual Studio 2019 г. - [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` Папка включает пакеты транзитивно участвовать целевых объектов и свойств, проект ведущего приложения — [#6091](https://github.com/NuGet/Home/issues/6091)
* Улучшенная поддержка сценариев PackageReference в NuGet IV API - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` является устаревшим - [#7928](https://github.com/NuGet/Home/issues/7928)
* Подключаемый модуль поставщика учетных данных Gen 1 был замещен стандартом [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) и вскоре будет объявлен устаревшим - [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Ошибки**

* При выполнении восстановления NoOp, избегайте использования *. dgspec.json записи в каталоге obj - [#7854](https://github.com/NuGet/Home/issues/7854)

* Разрешения на файлы, созданные внутри ~/.nuget слишком открыты - [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` не работает с источниками, которым требуется проверка подлинности - [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller - вызов метода для проекта без пакета ссылается на всегда использует packages.config, даже если значение по умолчанию имеет значение PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)

* В КОНСОЛИ ДИСПЕТЧЕРА ПАКЕТОВ: Update-Package переустановите завершается сбоем («не удалось найти пакет») на delisted пакетов. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Добавить уведомление третьих лиц в репозиторий, а также VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage следует установить последнюю версию, если версия, не учитывая - [#7493](https://github.com/NuGet/Home/issues/7493)

* --интерактивной поддержки dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)

* При восстановлении с помощью блокировки файла, не должны вызываться NU1603 предупреждение. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet не следует печатать путь проекта во время восстановления при минимальном ведении журнала - [#7647](https://github.com/NuGet/Home/issues/7647)

* --пакет удаляется интерактивной поддержки для команды dotnet - [#7727](https://github.com/NuGet/Home/issues/7727)

* Добавьте обратно NuGet.Packaging.Core с TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache требуется более короткий путь к работают хорошо - [#7770](https://github.com/NuGet/Home/issues/7770)

* Предпочитать путь для обнаружения msbuild, если пользователь не запросить определенные msbuild версии - [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` должно отобразиться правильное msbuild версии — [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): ошибка: Не удалось найти часть пути "/ tmp/NuGetScratch - в mono — [#7793](https://github.com/NuGet/Home/issues/7793)

* Восстановление без необходимости выполняет перечисление содержимого всех версий пакета, на которые имеются ссылки в кэше машины - [#7639](https://github.com/NuGet/Home/issues/7639)

* Автоматическое обнаружение MSBuild всегда выбирает 16.0 после установки VS 2019 предварительной версии — [#7621](https://github.com/NuGet/Home/issues/7621)

* DotNet пакета списка над решением, выводит повторяющиеся записи для framework — [#7607](https://github.com/NuGet/Home/issues/7607)

* Исключение «пустой путь не является допустимым» при вызывающий IVsPackageInstaller.InstallPackage прежние проектов и пакетов папка не существует. - [#5936](https://github.com/NuGet/Home/issues/5936)

* минимальной детализации MSBuild/t: RESTORE должно быть более минимальным - [#4695](https://github.com/NuGet/Home/issues/4695)

* VS 16.0 в пользовательский Интерфейс NuGet может быть прочитан появляются из-за проблем цвет - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & разъяснение NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)

* Восстановление без необходимости перечисляет папку глобальных пакетов, пытаясь определить тип - [#7596](https://github.com/NuGet/Home/issues/7596)

* Ошибки из принудительного применения блокировки файла, будет показан в окно списка ошибок - [#7429](https://github.com/NuGet/Home/issues/7429)

* Устранение проблем NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)

* Адаптироваться к MSBuild, обновление его установки расположение - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack должен быть объект как зависимость разработки - [#7249](https://github.com/NuGet/Home/issues/7249)

* Добавьте пакет точку расширения для включения отладочных символов - [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` необходимо сохранять диапазон версий зависимости в созданный nupkg (даже при использовании версии с плавающей запятой) - [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` происходит сбой на прошедшего проверку подлинности источника при конфигурации уровня пользователя также имеет источник - [#7209](https://github.com/NuGet/Home/issues/7209)

* Пакет не следует ограничивать набор BuildActions для файлов содержимого - [#7155](https://github.com/NuGet/Home/issues/7155)

* С помощью ProjectReference, который требует AssetTargetFallback для успешного выполнения, следует предупредить. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Взаимоблокировка из-за проблем многопоточности, при вызове в CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` не использует учетные данные из глобального файла конфигурации для источника, указанного в локальном файле конфигурации - [#6935](https://github.com/NuGet/Home/issues/6935)

* Потоков проблемы с MEF, вызываемого на async кодовых пути - [#6771](https://github.com/NuGet/Home/issues/6771)

* Подписи: сообщение об ошибке дважды и без стека вызовов - [#6455](https://github.com/NuGet/Home/issues/6455)

* Установка подписанного пакета с помощью сертификата недоверенном подписи должно отображаться ошибка — [#6318](https://github.com/NuGet/Home/issues/6318)

* Восстановление NuGet неправильно ничего не делают при 2 проекта совместный доступ к каталогу obj - [#6114](https://github.com/NuGet/Home/issues/6114)

* Нельзя использовать личный маркер доступа с `dotnet restore` на платформе Linux с помощью пакетов из прошедшего проверку подлинности веб-канала - [#5651](https://github.com/NuGet/Home/issues/5651)

* Команда DotNet restore завершается ошибкой из-за расширенных веб-канала - отключено машины [#5410](https://github.com/NuGet/Home/issues/5410)

**Запросы на изменение структуры**

* Предупреждать о будущих удаления «dotnet pack project.json —» [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Добавить предупреждение об устаревании для подключаемый модуль учетных данных Gen1 - [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Подписи. Автоматический включен репозиторий, чтобы требовать проверку клиента каждый пакет как репозиторий — с помощью ресурса RepositorySignatures/5.0.0 - [#7759](https://github.com/NuGet/Home/issues/7759)

* Максимальное число запросов http на каждый источник через NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet должны быть нацелены на Net472 (для очистки 16.0 сборку VSIX) — [#7143](https://github.com/NuGet/Home/issues/7143)

* В КОНСОЛИ ДИСПЕТЧЕРА ПАКЕТОВ: Удалить команду OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)

* Создание NetCoreApp 3.0 сопоставляются NetStandard 2.1 — [#7762](https://github.com/NuGet/Home/issues/7762)

* Добавление поддержки netstandard2.0 к пакетам NuGet.* - [#6516](https://github.com/NuGet/Home/issues/6516)

* Авторы пакета для определения поведения транзитивное активы сборки - [#6091](https://github.com/NuGet/Home/issues/6091)

* Поддерживает функцию фильтра решения VS 2019 г. Также поддерживает проект не в решении или выгруженные проекты. Сначала потребуется восстановление полного решения (с помощью интерфейса командной строки или Visual STUDIO) - [#5820](https://github.com/NuGet/Home/issues/5820)

* Сборки NuGet 5.0 требуется .NET Framework 4.7.2 (посредством изменения TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData из NuGet.Packaging должен быть открытым. Обновите метаданные лицензии, полученные из spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Удалить устаревшие параметры API - [#7294](https://github.com/NuGet/Home/issues/7294)

* Обходной путь восстановления тайм-аутов на системах с 1 ЦП — [#6742](https://github.com/NuGet/Home/issues/6742)

* Проверку подлинности NTLM, является предпочтительным NuGet, даже при наличии учетных данных в NuGet.config: Добавление параметра-config для фильтрации типов проверки подлинности учетных данных — [#5286](https://github.com/NuGet/Home/issues/5286)

* Включить EmbedInteropTypes для PackageReference (соответствующие возможности Packages.Config) - [#2365](https://github.com/NuGet/Home/issues/2365)

**[Список всех проблем, исправленных в этом выпуске - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="known-issues"></a>Известные проблемы

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Проблемы
При использовании dotnet.exe 2.x для восстановления проекта с несколькими целевыми объектами (netcoreapp 1.x и netcoreapp 2.x) резервная папка обрабатывается как веб-канал файла. Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.<br>
#### <a name="workaround"></a>Обходной путь
Отключить использование резервной папки, задав `RestoreAdditionalProjectSources` значение nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Используйте это с осторожностью, поскольку теперь пакеты, которые будет восстановлен из резервной папки будут загружены с сайта NuGet.org.
