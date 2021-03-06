---
title: Заметки о выпуске NuGet 4.9 RTM
description: 'Заметки о выпуске NuGet 4.9: известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.'
author: JonDouglas
ms.author: jodou
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 429218fa4968d572ef187ef1dbfacac8a3bde2b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780154"
---
# <a name="nuget-49-release-notes"></a>Заметки о выпуске NuGet 4.9

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio| Доступно в пакетах SDK для .NET|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 версии 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500, 2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | Н/Д | Н/Д |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 версии 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 версии 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>Сводка: Новые возможности версии 4.9.0

* Подписи. Включение ClientPolicies для настройки требования использовать набор доверенных авторов и репозиториев, перечисленных в NuGet.Config, — [#6961](https://github.com/NuGet/Home/issues/6961), [запись блога](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html).

* Создание файлов с расширением .snupkg для включения символов в пакет и оптимизация отправки для принятия протоколом NuGet файлов .snupkg для сервера символов — [#6878](https://github.com/NuGet/Home/issues/6878), [запись блога](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html).

* Подключаемый модуль учетных данных версии 2 для NuGet — [#6642](https://github.com/NuGet/Home/issues/6642).

* Автономные пакеты NuGet — лицензия — [#4628](https://github.com/NuGet/Home/issues/4628), [объявление](https://github.com/NuGet/Announcements/issues/32).

* Включение согласия для метаданных GeneratePathProperty в PackageReference для создания свойства MSBuild для каждого пакета в каталоге Foo.Bar\1.0\" — [#6949](https://github.com/NuGet/Home/issues/6949).

* Улучшение опыта использования NuGet клиентами — [#7108](https://github.com/NuGet/Home/issues/7108).

* Включение многократного восстановления пакетов с помощью файла блокировки — [#5602](https://github.com/NuGet/Home/issues/5602), [объявление](https://github.com/NuGet/Announcements/issues/28), [запись блога](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

* После предупреждений, преобразованных в ошибки (с помощью WarnAsErrors) и вызываемых PackageExtraction, не должен оставаться извлеченный пакет — [#7445](https://github.com/NuGet/Home/issues/7445).

* Неправильно подписанные пакеты не должны попадать в папку установки глобальных пакетов — [#7423](https://github.com/NuGet/Home/issues/7423).

* Привязка поколения перенаправления не должна пропускать фасадные сборки — [#7393](https://github.com/NuGet/Home/issues/7393).

* VersionRange Equals не сравнивает плавающие диапазоны — [#7324](https://github.com/NuGet/Home/issues/7324).

* Восстановление. Снижение производительности при использовании HTTP-стека .NET Core 2.1 — [#7314](https://github.com/NuGet/Home/issues/7314).

* Обновление пакета не должно изменять PrivateAssets в PackageReference — [#7285](https://github.com/NuGet/Home/issues/7285).

* Подписи. Подписывание не выполняется, если в пакете содержится слишком много записей пакета (> 65 534) — [#7248](https://github.com/NuGet/Home/issues/7248).

* Путь к коду dotnet nuget push должен поддерживать новый поставщик учетных данных — [#7233](https://github.com/NuGet/Home/issues/7233).

* Поддержка выполнения подключаемых модулей с помощью инвариантного языка и региональных параметров (как в Docker) — [#7223](https://github.com/NuGet/Home/issues/7223).

* При добавлении источников NuGet не должны удаляться учетные данные из NuGet.config — [#7200](https://github.com/NuGet/Home/issues/7200).

* Установка devDependency PackageReference по умолчанию должна происходить в excludeassets=compile — [#7084](https://github.com/NuGet/Home/issues/7084).

* Отображение средства переноса для всех проектов и сообщения об ошибке при несовместимости проекта — [#6958](https://github.com/NuGet/Home/issues/6958).

* Dotnet add package должен фиксировать восстановления, выполняемые для файла ресурсов — [#6928](https://github.com/NuGet/Home/issues/6928).

* Подписи. Улучшены сообщения об ошибках, связанные с подписями, — [#6906](https://github.com/NuGet/Home/issues/6906).

* [Сбой теста][zh-TW]. Строка Package Manager Console не локализована в консоли диспетчера пакетов — [#6381](https://github.com/NuGet/Home/issues/6381).

* Сообщение об ошибке Unable to find project information (Не удалось найти сведения о проекте) должно быть более информативным в VS — [#5350](https://github.com/NuGet/Home/issues/5350).

* Неинформативное сообщение об ошибке при неправильном использовании тега версии nuspec пакета NuGet — [#2714](https://github.com/NuGet/Home/issues/2714).

* DCR — подписи. Поддержка протокола NuGet: ресурс RepositorySignatures/4.9.0 — [#7421](https://github.com/NuGet/Home/issues/7421).

* DCR — во время извлечения пакета теперь будет создаваться файл метаданных .nupkg с хэш-кодом содержимого — [#7283](https://github.com/NuGet/Home/issues/7283).

* DCR — пропуск проверки аутентичности кода подключаемых модулей при выполнении в Mono — [#7222](https://github.com/NuGet/Home/issues/7222).

[Список всех проблем, исправленных в выпуске 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Сводка: Новые возможности версии 4.9.1

* Добавлена поддержка чтения записи в файл nuget.config с помощью новой команды trusted-signers — [#7480](https://github.com/NuGet/Home/issues/7480).

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

* Исправлена функция создания ссылок лицензии — [#7515](https://github.com/NuGet/Home/issues/7515).

* Коды ошибок регрессии для проверки подписей — [#7492](https://github.com/NuGet/Home/issues/7492).

* Пакет NuGet.Build.Tasks.Pack не включает сведения о лицензиях — [#7379](https://github.com/NuGet/Home/issues/7379).

[Список всех проблем, исправленных в выпуске 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Сводка: Новые возможности версии 4.9.2

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

* VS/dotnet.exe/nuget.exe/msbuild.exe (восстановление) не использует учетные данные, если имя источника содержит пробел, — [#7517](https://github.com/NuGet/Home/issues/7517).

* Проблемы с доступом к LicenseAcceptanceWindow и LicenseFileWindow — [#7452](https://github.com/NuGet/Home/issues/7452).

* Исправлено FormatException в DateTime.Parse из DateTimeConverter — [#7539](https://github.com/NuGet/Home/issues/7539).

[Список всех проблем, исправленных в выпуске 4.9.2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>Сводка: Новые возможности версии 4.9.3

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>Проблемы с многократным восстановлением пакетов с помощью файла блокировки

* Режим блокировки не работает из-за неправильного вычисления хэша для кэшированных пакетов — [#7682](https://github.com/NuGet/Home/issues/7682)

* Восстановление разрешается для другой версии, отличной от указанной в файле `packages.lock.json` — [#7667](https://github.com/NuGet/Home/issues/7667)

* --locked-mode / RestoreLockedMode вызывает ложные ошибки восстановления при использовании ProjectReferences — [#7646](https://github.com/NuGet/Home/issues/7646)

* Сопоставитель пакетов SDK MSBuild пытается проверить агент работоспособности системы для пакета SDK, который не удалось восстановить с использованием файла packages.lock.json — [#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>Проблемы с блокировкой зависимостей с помощью настраиваемых политик доверия
* Инструмент dotnet.exe не должен проверять доверенную подписывающую сторону, так как подписанные пакеты не поддерживаются — [#7574](https://github.com/NuGet/Home/issues/7574)

* Порядок объектов trustedSigners в файле конфигурации влияет на проверку доверия — [#7572](https://github.com/NuGet/Home/issues/7572)

* Невозможно реализовать ISettings [из-за рефакторинга API-интерфейсов параметров для поддержки функции политики доверия] — [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>Проблемы, связанные с улучшением процесса отладки

* Не удается опубликовать пакет символов для глобального средства .NET Core — [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>Проблемы с автономными пакетами NuGet — лицензия

* Ошибка при создании пакета символов с расширением .snupkg при использовании встроенного файла лицензии — [#7591](https://github.com/NuGet/Home/issues/7591)

[Список всех проблем, исправленных в выпуске 4.9.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a>Сводка: Новые возможности версии 4.9.4

* Исправление безопасности: разрешения на файлы, созданные внутри ~/.nuget, слишком открыты [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)


## <a name="known-issues"></a>Известные проблемы

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a>Выполнение команды dotnet nuget push с параметром --interactive выдает сообщение об ошибке на компьютере Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Проблемы
Аргумент `--interactive` не перенаправляется интерфейсом командной строки dotnet, что приводит к ошибке `error: Missing value for option 'interactive'`.

#### <a name="workaround"></a>Возможное решение
Выполните любую другую команду dotnet с параметром interactive, например `dotnet restore --interactive`, и пройдите проверку подлинности. Результат проверки подлинности затем может быть кэширован поставщиком учетных данных. Затем выполните `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Проблемы
При использовании dotnet.exe 2.x для восстановления проекта с несколькими целевыми объектами (netcoreapp 1.x и netcoreapp 2.x) резервная папка обрабатывается как веб-канал файла. Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.

#### <a name="workaround"></a>Возможное решение
Отключите использование резервной папки, очистив значение для `RestoreAdditionalProjectSources`. `<RestoreAdditionalProjectSources/>` Соблюдайте при этом осторожность, так как это приведет к скачиванию большого количества пакетов с NuGet.org, которые иначе были бы восстановлены из резервной папки.
