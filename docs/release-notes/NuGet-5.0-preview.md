---
title: Заметки о выпуске предварительной версии 5.0 NuGet
description: Заметки о выпуске для предварительных версий NuGet 5.0, включая известные проблемы, исправления ошибок, новые функции и запросы на изменение структуры.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: ed3294f88ff99d5e26f630bdbca03aa8446b6e7f
ms.sourcegitcommit: 0cb4c9853cde3647291062eadee2298dd273311e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084940"
---
# <a name="nuget-50-preview-release-notes"></a>Заметки о выпуске NuGet Предварительная версия 5.0

## <a name="summary-whats-new-in-50-preview-2"></a>Сводка: Новые возможности в версии 5.0 предварительной версии 2

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

#### <a name="bugs"></a>Ошибок:

* VS 16.0 в пользовательский Интерфейс NuGet может быть прочитан появляются из-за проблем цвет - [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & разъяснение NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)

* Восстановление без необходимости перечисляет папку глобальных пакетов, пытаясь определить тип - [#7596](https://github.com/NuGet/Home/issues/7596)

* Ошибки из принудительного применения блокировки файла, будет показан в окно списка ошибок - [#7429](https://github.com/NuGet/Home/issues/7429)

* Устранение проблем NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)

* Адаптироваться к MSBuild обновление его в папку установки.  - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack должен быть объект как зависимость разработки - [#7249](https://github.com/NuGet/Home/issues/7249)

* Добавьте пакет точку расширения для включения отладочных символов - [#7234](https://github.com/NuGet/Home/issues/7234)

* DotNet pack должен сохранить диапазон версий зависимости в созданный nupkg. (даже при использовании версии с плавающей запятой) - [#7232](https://github.com/NuGet/Home/issues/7232)

* Команда DotNet restore завершается ошибкой в источнике, прошедшего проверку подлинности, если конфигурации уровня пользователя также имеет источник - [#7209](https://github.com/NuGet/Home/issues/7209)

* Пакет не следует ограничивать набор BuildActions для файлов содержимого - [#7155](https://github.com/NuGet/Home/issues/7155)

* С помощью projectreference, который требует AssetTargetFallback для успешного выполнения, следует предупредить. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Взаимоблокировка из-за проблем многопоточности, при вызове в CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)

* Команда DotNet add, пакет не будет использовать учетные данные из глобального файла конфигурации для источника, указанного в локальном файле конфигурации - [#6935](https://github.com/NuGet/Home/issues/6935)

* Проблемы с MEF, потока вызван для асинхронного путям кода может отсутствовать - [#6771](https://github.com/NuGet/Home/issues/6771)

* Подписи: сообщение об ошибке дважды и без стека вызовов - [#6455](https://github.com/NuGet/Home/issues/6455)

* Установка подписанного пакета с помощью сертификата недоверенном подписи должно отображаться ошибка — [#6318](https://github.com/NuGet/Home/issues/6318)

* Восстановление NuGet неправильно ничего не делают при 2 проекта совместный доступ к каталогу obj - [#6114](https://github.com/NuGet/Home/issues/6114)

* Нельзя использовать личный маркер доступа с dotnet restore на платформе Linux с пакетами из прошедшего проверку подлинности веб-канала - [#5651](https://github.com/NuGet/Home/issues/5651)

* Команда DotNet restore завершается ошибкой из-за расширенных веб-канала - отключено машины [#5410](https://github.com/NuGet/Home/issues/5410)

#### <a name="dcrs"></a>Запросы на изменение структуры

* Сборки NuGet 5.0 требуется .NET Framework 4.7.2 (посредством изменения TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData из NuGet.Packaging должен быть открытым. Обновите метаданные лицензии, полученные из spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Удалить устаревшие параметры API - [#7294](https://github.com/NuGet/Home/issues/7294)

* Обходной путь восстановления тайм-аутов на системах с 1 ЦП — [#6742](https://github.com/NuGet/Home/issues/6742)

* Проверку подлинности NTLM, является предпочтительным NuGet, даже при наличии учетных данных в NuGet.config: Добавление параметра-config для фильтрации типов проверки подлинности учетных данных — [#5286](https://github.com/NuGet/Home/issues/5286)

* Включить EmbedInteropTypes для PackageReference (соответствующие возможности Packages.Config) - [#2365](https://github.com/NuGet/Home/issues/2365)

[Список всех ошибок, исправленных в этом выпуске 5.0.0-preview2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")


## <a name="known-issues"></a>Известные проблемы

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>Выполнение команды dotnet nuget push с параметром --interactive выдает сообщение об ошибке на компьютере Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Проблемы
Аргумент `--interactive` не перенаправляется интерфейсом командной строки dotnet, что приводит к ошибке `error: Missing value for option 'interactive'`.

#### <a name="workaround"></a>Обходной путь
Выполните любую другую команду dotnet с параметром interactive, например `dotnet restore --interactive`, и пройдите проверку подлинности. Результат проверки подлинности затем может быть кэширован поставщиком учетных данных. Затем выполните `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Проблемы
При использовании dotnet.exe 2.x для восстановления проекта с несколькими целевыми объектами (netcoreapp 1.x и netcoreapp 2.x) резервная папка обрабатывается как веб-канал файла. Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.

#### <a name="workaround"></a>Обходной путь
Отключите использование резервной папки, очистив значение для `RestoreAdditionalProjectSources`. `<RestoreAdditionalProjectSources/>` Соблюдайте при этом осторожность, так как это приведет к скачиванию большого количества пакетов с NuGet.org, которые иначе были бы восстановлены из резервной папки.
