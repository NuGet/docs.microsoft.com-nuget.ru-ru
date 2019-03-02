---
title: Заметки о выпуске предварительной версии 5.0 NuGet
description: Заметки о выпуске для предварительных версий NuGet 5.0, включая известные проблемы, исправления ошибок, новые функции и запросы на изменение структуры.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 4b05dcb9a2960c1e3231e81d4b4c122d3a518753
ms.sourcegitcommit: 571644118e3c5a2fd818891d305b4b8de8ef21de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2019
ms.locfileid: "57225892"
---
# <a name="nuget-50-preview-release-notes"></a>Заметки о выпуске NuGet Предварительная версия 5.0

## <a name="nuget-50-preview-releases"></a>NuGet 5.0 предварительных выпусков

* 27 февраля 2019 г. - [NuGet 5.0 Preview 4](#whats-new-in-nuget-50-preview-4)
* 13 февраля 2019 г. - [NuGet 5.0 Preview 3](#whats-new-in-nuget-50-preview-3)
* 23 января 2019 г. - [NuGet 5.0 предварительной версии 2](#whats-new-in-nuget-50-preview-2)

## <a name="whats-new-in-nuget-50-preview-4"></a>Новые возможности в предварительной версии NuGet 5.0 4

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Ошибки**

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

**Запросы на изменение структуры**

* Максимальное число запросов http на каждый источник через NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet должны быть нацелены на Net472 (для очистки 16.0 сборку VSIX) — [#7143](https://github.com/NuGet/Home/issues/7143)

* В КОНСОЛИ ДИСПЕТЧЕРА ПАКЕТОВ: Удалить команду OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)

* Создание NetCoreApp 3.0 сопоставляются NetStandard 2.1 — [#7762](https://github.com/NuGet/Home/issues/7762)

* Добавление поддержки netstandard2.0 к пакетам NuGet.* - [#6516](https://github.com/NuGet/Home/issues/6516)


## <a name="whats-new-in-nuget-50-preview-3"></a>Новые возможности в предварительной версии NuGet 5.0 3

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске 

**Ошибки**

* nuget.exe /? должно отобразиться правильное msbuild версии — [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): ошибка: Не удалось найти часть пути "/ tmp/NuGetScratch - в mono — [#7793](https://github.com/NuGet/Home/issues/7793)

* Восстановление без необходимости выполняет перечисление содержимого всех версий пакета, на которые имеются ссылки в кэше машины - [#7639](https://github.com/NuGet/Home/issues/7639)

* Автоматическое обнаружение MSBuild всегда выбирает 16.0 после установки VS 2019 предварительной версии — [#7621](https://github.com/NuGet/Home/issues/7621)

* DotNet пакета списка над решением, выводит повторяющиеся записи для framework — [#7607](https://github.com/NuGet/Home/issues/7607)

* Исключение «пустой путь не является допустимым» при вызывающий IVsPackageInstaller.InstallPackage прежние проектов и пакетов папка не существует. - [#5936](https://github.com/NuGet/Home/issues/5936)

* минимальной детализации MSBuild/t: RESTORE должно быть более минимальным - [#4695](https://github.com/NuGet/Home/issues/4695)

**Запросы на изменение структуры**

* Авторы пакета для определения поведения транзитивное активы сборки - [#6091](https://github.com/NuGet/Home/issues/6091)

* Включить восстановление в Visual STUDIO завершится успешно, если проект не является частью решения или не загружен, но ранее был восстановлен - [#5820](https://github.com/NuGet/Home/issues/5820)


## <a name="whats-new-in-nuget-50-preview-2"></a>Новые возможности в предварительной версии NuGet 5.0 2

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Ошибки**

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

**Запросы на изменение структуры**

* Сборки NuGet 5.0 требуется .NET Framework 4.7.2 (посредством изменения TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData из NuGet.Packaging должен быть открытым. Обновите метаданные лицензии, полученные из spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Удалить устаревшие параметры API - [#7294](https://github.com/NuGet/Home/issues/7294)

* Обходной путь восстановления тайм-аутов на системах с 1 ЦП — [#6742](https://github.com/NuGet/Home/issues/6742)

* Проверку подлинности NTLM, является предпочтительным NuGet, даже при наличии учетных данных в NuGet.config: Добавление параметра-config для фильтрации типов проверки подлинности учетных данных — [#5286](https://github.com/NuGet/Home/issues/5286)

* Включить EmbedInteropTypes для PackageReference (соответствующие возможности Packages.Config) - [#2365](https://github.com/NuGet/Home/issues/2365)

[Список всех ошибок, исправленных в этом выпуске 5.0.0-preview2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>Известные проблемы

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи. - [#7414](https://github.com/NuGet/Home/issues/7414)
**Проблема** при использовании dotnet.exe 2.x для восстановления этой netcoreapp нескольких целевых объектов проекта 1.x и netcoreapp 2.x, папке резервной обрабатывается как файл веб-канала. Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.
**Инструкции по решению** отключить использование резервной папки, задав `RestoreAdditionalProjectSources` значение nothing. `<RestoreAdditionalProjectSources/>` Соблюдайте при этом осторожность, так как это приведет к скачиванию большого количества пакетов с NuGet.org, которые иначе были бы восстановлены из резервной папки.
