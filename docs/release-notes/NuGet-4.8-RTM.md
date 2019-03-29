---
title: Заметки о выпуске NuGet 4.8 RTM
description: Заметки о выпуске NuGet 4.8.1, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: f85042b8fe1511934d6a3ac7de34da92c575f6e0
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432530"
---
# <a name="nuget-48-release-notes"></a>Заметки о выпуске NuGet 4.8

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает функции NuGet 4.8 RTM.


Также доступны версии этого компонента для командной строки:
* NuGet.exe 4.8 — [nuget.org/downloads](https://nuget.org/downloads);
* DotNet.exe — [пакет SDK 2.1.400 для .NET Core](https://www.microsoft.com/net/download/visual-studio-sdks).


## <a name="summary-whats-new-in-480"></a>Сводка: Новые возможности версии 4.8.0
* NuGet.exe теперь поддерживает длинные имена файлов в Windows 10 — [#6937](https://github.com/NuGet/Home/issues/6937)
* Подключаемые модули аутентификации теперь работают на платформах MsBuild, DotNet.exe, NuGet.exe и Visual Studio, в том числе на нескольких сразу. Подключаемые модули аутентификации первого поколения не поддерживались в MsBuild и DotNet.exe. Примечание. Предварительные версии сборок Visual Studio 2017 15.9 уже содержат подключаемый модуль аутентификации VSTS. [#6486](https://github.com/NuGet/Home/issues/6486)
* Сопоставитель пакетов SDK для MsBuild теперь компилируется вместе с NuGet и устанавливается через средства NuGet для Visual Studio. Это позволяет избежать рассинхронизации версий. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference теперь поддерживает метаданные DevelopmentDependency — [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>Сводка: Новые возможности версии 4.8.2

* Исправление безопасности: разрешения на файлы, созданные внутри ~/.nuget, слишком открыты [#7673](https://github.com/NuGet/Home/issues/7673)[CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="known-issues"></a>Известные проблемы
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>Установка подписанных пакетов на компьютере непрерывной интеграции или в автономной среде занимает больше времени, чем обычно

#### <a name="issue"></a>Проблемы
Если для компьютера ограничен доступ к Интернету (например, в сценарии компьютера сборки для CI/CD), установка и восстановление подписанного пакета NuGet вызывает предупреждение ([NU3028](https://docs.microsoft.com/en-us/nuget/reference/errors-and-warnings/nu3028)), так как серверы отзыва недоступны. Подобный результат является ожидаемым. Но в некоторых случаях это может привести к непреднамеренным последствиям, например к непривычной длительности процессов установки и восстановления пакета.

#### <a name="workaround"></a>Обходной путь
Обновитесь до версий Visual Studio 15.8.4 и NuGet.exe 4.8.1, в которых мы добавили переменную среды для переключения режима проверки отзыва.
Если для переменной среды `NUGET_CERT_REVOCATION_MODE` установлено значение `offline`, NuGet будет проверять состояние отзыва для сертификата только по кэшированному списку отзыва сертификатов, без попыток связаться с серверами отзыва. Если установлен режим проверки отзыва `offline`, вместо предупреждения формируется информационное сообщение.

> [!Warning]
> Мы рекомендуем не использовать автономный режим проверки отзыва в обычных условиях. В этом режиме NuGet пропускает проверку отзыва сертификатов через Интернет, а используемый кэшированный список отзыва сертификатов может оказаться устаревшим. В таком случае он продолжит устанавливать пакеты, у которых уже отозван сертификат для подписи, и для которых обычная проверка отзыва приведет к блокированию установки.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>Параметр `Migrate packages.config to PackageReference...` недоступен в контекстном меню, которое открывается по щелчку правой кнопкой мыши

#### <a name="issue"></a>Проблемы

При первом открытии проект NuGet не удается инициализировать до выполнения операции NuGet. В результате параметр миграции не отображается в контекстном меню, которое открывается по щелчку правой кнопкой мыши `packages.config` или `References`.

#### <a name="workaround"></a>Обходной путь

Выполните одно из следующих действий NuGet:
* Откройте пользовательский интерфейс диспетчера пакетов. Для этого щелкните правой кнопкой мыши `References` и выберите `Manage NuGet Packages...`.
* Откройте консоль диспетчера пакетов. В `Tools > NuGet Package Manager` выберите `Package Manager Console`.
* Запустите восстановление NuGet. Для этого щелкните правой кнопкой мыши узел решения в обозревателе решений и выберите `Restore NuGet Packages`.
* Создайте проект, активизирующий восстановление NuGet.

Теперь параметр миграции должен отобразиться. Обратите внимание, что этот параметр не поддерживается и не будет отображаться для типов проектов ASP.NET и C++.
Примечание. Эта проблема исправлена в VS 2017 15.9 предварительной версии 3

## <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

### <a name="bugs"></a>Ошибки
#### <a name="signing"></a>Добавление подписи
* Подписи. Установка подписанного пакета в автономной среде исправлена в версии 4.8.1 — [#7008](https://github.com/NuGet/Home/issues/7008)
* Подписывание. Неверная проверка URL-адресов — [#7174](https://github.com/NuGet/Home/issues/7174)
* Подписывание. Проверка целостности пакета в RepositorySignatureVerifier, если к пакету добавлена вторая подпись репозитория — [#6926](https://github.com/NuGet/Home/issues/6926)
* Ошибка "Проверка целостности пакета не пройдена." должна содержать в тексте сообщения (и коде ошибки) идентификатор пакета — [#6944](https://github.com/NuGet/Home/issues/6944)
* Проверка подписанного пакета в репозитории позволяет использовать пакеты, подписанные разными сертификатами — [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet — подписывание — не допускается URL-адрес отметки времени https:// ? - [#6871](https://github.com/NuGet/Home/issues/6871)
* Устранение NullRef в сценарии упаковки NuSpec, улучшение некоторых параметров — [#6866](https://github.com/NuGet/Home/issues/6866)
* При обновлении сведений о подписавшем возникает ошибка недопустимой памяти, когда добавляется метка времени для второй подписи — [#6840](https://github.com/NuGet/Home/issues/6840)
* Подписывание. Удаление исключений CTL — [#6794](https://github.com/NuGet/Home/issues/6794)
* Подписывание. ContentUrl должен быть ТОЛЬКО HTTPS — [#6777](https://github.com/NuGet/Home/issues/6777)
* Подписи.  SignedPackageVerifierSettings.VSClientDefaultPolicy не применяется — [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Упаковка
* Восстановление и сборка не должны быть обязательными при использовании dotnet.exe для упаковки nuspec — [#6866](https://github.com/NuGet/Home/issues/6866)
* Разрешение использовать пустые маркеры замены в NuspecProperties — [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask создает исключение NullReferenceException, если указать NuspecProperties — [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Специальные возможности
* [Специальные возможности] В пользовательском интерфейсе диспетчера пакетов строка предварительного выпуска под кнопкой пакета закрыта описанием пакета — [#4504](https://github.com/NuGet/Home/issues/4504)
* [Специальные возможности] В пользовательском интерфейсе диспетчера пакетов раскрывающийся список источников и кнопка "Параметры" усекаются, если выбран вариант "Автономные пакеты Microsoft Visual Studio" — [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Консоль управления PowerShell (PMC)
* `Update-Package` игнорирует диапазон версий PackageReference — [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall` — проблема во всем решении — [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` переустанавливает все пакеты, а не только указанный пакет — [#737](https://github.com/NuGet/Home/issues/737)
* Из консоли диспетчера пакетов можно обновиться до пакета NuGet, не включенного в список — [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Прочее
* Исправление `NuGet update self`, где для NuGet.Commandline nupkg не должно быть указано значение semver2.0 — [#7116](https://github.com/NuGet/Home/issues/7116)
* Улучшение взаимодействия с ошибками при установке NU1107 — [#7107](https://github.com/NuGet/Home/issues/7107)
* Неверная сериализация GetAuthenticationCredentialRequest — [#6983](https://github.com/NuGet/Home/issues/6983)
* Ошибка при загрузке NuGet Visual Studio AsyncPackage при инициализации вне потока пользовательского интерфейса — [#6976](https://github.com/NuGet/Home/issues/6976)
* При восстановлении возвращается вводящая в заблуждение ошибка о том, что требуется project.json — [#6959](https://github.com/NuGet/Home/issues/6959)
* Пользовательский интерфейс диспетчера пакетов. В режиме предварительного просмотра изменений кнопка "ОК" недоступна с клавиатуры автоматически — [#6893](https://github.com/NuGet/Home/issues/6893)
* RestoreSources игнорируются для проекта со ссылками p2p — [#6776](https://github.com/NuGet/Home/issues/6776)
* Создание проекта модульного теста с помощью шаблона .NET Framework приводит к открытию старой модели проекта с файлом packages.config — [#6736](https://github.com/NuGet/Home/issues/6736)
* Разрешение переопределять зависимости пакета ссылками в проекте —[#6536](https://github.com/NuGet/Home/issues/6536)
* Предоставление NoDefaultExcludes в задаче MSBuild — [#6450](https://github.com/NuGet/Home/issues/6450)
* Сообщение о состоянии "Очистить все кэши NuGet" может скрываться при изменении размера окна — [#5938](https://github.com/NuGet/Home/issues/5938)


[Список всех ошибок, исправленных в этом выпуске](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
