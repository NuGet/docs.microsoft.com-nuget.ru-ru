---
title: Заметки о выпуске 2.7 NuGet
description: Заметки о выпуске для NuGet 2.7, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b7cea360764e1b069afacabadd9b94d87e21ecc
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-27-release-notes"></a>Заметки о выпуске 2.7 NuGet

[NuGet 2.6.1 заметки о выпуске WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 заметки о выпуске](../release-notes/nuget-2.7.1.md)

Дата выпуска NuGet 2.7 22 августа 2013 г.

## <a name="acknowledgements"></a>Благодарности

Мы бы хотели поблагодарить следующих внешних участников для их значительный вклад в NuGet 2.7:

1. [Майк рот](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Отображение URL-адрес лицензии, если список пакетов и детализации подробно описан.
2. [Ральф Адам](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -добавить атрибут элемента developmentDependency `packages.config` и использовать их в пакет для включения пакета среды выполнения
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Избегайте повторяющийся ключ свойства в команде пакет nuget.exe.
4. [Phegan Бен](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -увеличить размер кэша на компьютере до 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -диалоговое окно устранить NuGet отображение обновлений на вкладке "Ошибка"
    - Исправление Project.TargetFramework может иметь значение null в РуководительПроекта
    - [#3248](http://nuget.codeplex.com/workitem/3248) -на несуществующий packageId не удастся исправить SharedPackageRepository FindPackage/FindPackagesById
6. [Кевин Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -включить поддержку Nomad проекта
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -код Сбой команды push исправление с выхода 0, если файл не существует.
8. [Veselý Мартин](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -исправление ошибок с помощью команды Добавить BindingRedirect, когда проект ссылается на проект базы данных.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -исправление ошибки из nuget.pack неправильного подстановочный знак в атрибуте «исключить».
10. [Джастин Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -исправление ошибок `NuGet.targets` не передает $(Platform) nuget.exe при восстановлении пакетов.
11. [Брайан Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -исправление ошибки в команду nuget.exe пакета, которая позволит добавлять файлы с одинаковыми именами, но в разных регистрах, вызывает исключение «Уже существует элемент».
12. [Дэниела Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -добавить версию свойство NetPortableProfile классу.
13. [Дэвид Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -исправлена ошибка NullReferenceException, если requireApiKey = true, но заголовок X-NUGET-APIKEY не существуют
14. [Майкл Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -файл исправления NuGet.Build целевых объектов, чтобы он правильно работает с MonoDevelop
15. [Кришнамурти Pranav](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Повысить производительность команды восстановления, увеличение параллелизма

## <a name="notable-features-in-the-release"></a>Возможности в выпуске

### <a name="package-restore-by-default-with-implicit-consent"></a>Восстановление пакета по умолчанию (с согласия)

Представляет новый подход к восстановлении пакета NuGet 2.7 и решены основных препятствие: пакет восстановления согласия теперь по умолчанию установлен! Сочетание нового подхода и явного согласия значительно упростит сценарии восстановления пакета.

#### <a name="implicit-consent"></a>Явного согласия пользователя.

С помощью NuGet версии 2.0, 2.1, 2.2, 2.5 и 2.6 пользователям необходимо явно разрешить NuGet скачивать отсутствующие пакеты во время построения. Если это согласие не было явным образом предоставлено, а затем сможет до пользователю предоставлено согласие построение решения, которые включены восстановления пакета.

Начиная с NuGet 2.7, согласия восстановления пакета включено по умолчанию, позволяет пользователям явно *отказаться от участия* пакет восстановления, при необходимости, используя флажок в параметрах NuGet в Visual Studio. Это изменение для явного согласия влияет NuGet в следующих средах:

* Предварительная версия Visual Studio 2013
* Visual Studio 2012
* Visual Studio 2010
* Программы командной строки NuGet.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Восстановление автоматического пакета в Visual Studio

Начиная с NuGet 2.7 NuGet автоматически загрузит отсутствующие пакеты при сборке в Visual Studio, даже если восстановление пакета не было явно включено для решения. Это автоматическое восстановление пакетов происходит в Visual Studio, при построении проекта или решения, но до вызова MSBuild. Это дает ряд существенных преимуществ:

1. Больше не требуется использовать жестов «Включите восстановление пакетов NuGet» для решения
1. Проекты не требуется вносить изменения и NuGet не внести изменения в проект, чтобы убедиться, что включена восстановления пакета
1. Будут восстановлены все пакеты NuGet, включая те, которые включены импорты MSBuild для props или целевых файлов, *перед* вызывается MSBuild, обеспечивая их props цели правильно распознаются во время сборки

Только, чтобы использовать автоматическое восстановление пакетов в Visual Studio, необходимо выполнить одно (действие в):

1. Не устанавливайте флажок вашей `packages` папки

Существует несколько способов для пропуска вашей `packages` папку из системы управления версиями. Дополнительные сведения см. в разделе [пакетов и системы управления версиями](../consume-packages/packages-and-source-control.md) раздела.

Пока все пользователи являются неявно согласие автоматическое восстановление пакетов согласие, можно просто исключать параметрах диспетчера пакетов в Visual Studio.

![Параметры диспетчера пакетов](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Восстановление упрощенный пакета из командной строки

NuGet 2.7 появилась новая функция для nuget.exe: `nuget.exe restore`

Эта новая команда Restore позволяет легко восстановить все пакеты для решения с помощью одной команды, принимая решения файл или папку в качестве аргумента. Кроме того этот аргумент выводится, если в текущей папке присутствует только одно решение. Это означает, что все следующие работать на папку, содержащую одиночного файла решения (MySolution.sln):

1. восстановления NuGet.exe MySolution.sln
1. Восстановление NuGet.exe.
1. восстановления NuGet.exe

Команда восстановления откройте файл решения и найдите все проекты в решении. После этого он нашел `packages.config` файлы для всех проектов и восстановления, найти все пакеты. Он также восстанавливает решения на уровне пакетов, обнаруженных в `.nuget\packages.config` файла. Дополнительные сведения о новой команды восстановления можно найти в [Справочник по командной строке](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Новый рабочий процесс восстановления пакета

Мы рады об этих изменениях, чтобы восстановить пакет, как она порождает новый рабочий процесс. Если требуется исключить из системы управления версиями пакетов просто не будет зафиксирован `packages` папки. Пользователи Visual Studio, откройте и постройте решение увидите пакеты автоматически восстановится. Построение из командной строки, достаточно вызвать `nuget.exe restore` перед вызовом `msbuild`. Больше не нужно не забывайте использовать жест «Включите восстановление пакетов NuGet» для решения, и мы больше не нужно изменять проекты для изменения сборки. И это также обеспечивает значительно улучшенное взаимодействие с пользователем для пакеты, содержащие импортируемые элементы MSBuild, особенно для импортов, добавляемые с помощью NuGet последние функции для [автоматического импорта props или целевых файлов](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) из папки \build.

Помимо работу, которую мы сделали сами мы работаем с некоторых важных партнеров для завершения этого нового подхода. Мы конкретных временных шкалах для любой из них еще нет, но каждого участника как сообщаем, как мы о нового подхода.

* Team Foundation Service — они работают для интеграции вызов `nuget.exe restore` в группу по умолчанию создания сценариев.
* Windows Azure веб-сайтов — они работают позволяет принудительные проекта в Azure и имеют `nuget.exe restore` вызывается перед построением веб-сайте.
* TeamCity - они обновляют их установщик NuGet подключаемого модуля для TeamCity 8.x
* AppHarbor — они работают позволяет принудительно отправлять репозиторию AppHarbor и иметь `nuget.exe restore` вызывается до построения решения.

С каждым из участников выше приложение может использовать собственную копию nuget.exe и не потребовалось бы выполнить nuget.exe в решении.

#### <a name="known-issues"></a>Известные проблемы

Были известны две проблемы восстановления nuget.exe с первоначального выпуска 2.7, но они были устранены на 9/6/2013 с обновлением [NuGet.CommandLine пакета](http://www.nuget.org/packages/NuGet.CommandLine/).  Это обновление также можно найти в [страницы загрузки NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) на сайте CodePlex.  Под управлением `nuget.exe update -self` будут обновлены до последней версии.

Фиксированного были:

1. [Новый пакет восстановления не работает в моно при использовании SLN-файла](https://nuget.codeplex.com/workitem/3596)
1. [Новый пакет восстановления не работает с проектами Wix](https://nuget.codeplex.com/workitem/3598)

Имеется также с известными проблемами новый рабочий процесс восстановления пакета при котором [автоматическое восстановление пакетов не работает для проектов в папке решения](https://nuget.codeplex.com/workitem/3625). Эта проблема была исправлена в NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Изменение целевой платформы проекта и обновление сборки ошибок и предупреждений

Сколько раз после целевой платформы или обновления проекта, можно найти, некоторые пакеты NuGet не работает должным образом. К сожалению нет никаких признаков данного объекта и выполняется без указания о том, как ее устранить. С помощью NuGet 2.7 воспользуемся некоторые события Visual Studio с ними, когда были перенаправлены или обновить свой проект в влияет установленные пакеты NuGet.

Если обнаруживается, что все пакеты были затронуты целевой платформы или обновления, мы будет приводить к ошибкам построения немедленно сообщить. Кроме ошибки немедленно сборки, мы также сохранить `requireReinstallation="true"` флаг в вашей `packages.config` файл для всех пакетов, которые были зависит от целевой платформы и каждое последующее сборки в Visual Studio будет создавать предупреждения при построении для этих пакетов.

Несмотря на то, что NuGet не может предпринимать автоматические действия для переустановки затронутые пакеты, мы надеемся, что это указание и предупреждение поможет справки выясняется, при необходимости переустановите пакетов. Мы работаем над [пакета документации руководства по процессам для переустановки](../consume-packages/reinstalling-and-updating-packages.md) , эти сообщения об ошибках указывают на необходимость.

### <a name="nuget-configuration-defaults"></a>По умолчанию конфигурация NuGet

Многие компании используют NuGet внутренне, но у было сложно, направляя их разработчикам использовать внутренний пакета, а не nuget.org. NuGet 2.7 вводит значения конфигурации по умолчанию функция, позволяющая компьютера по умолчанию указывать для:

1. Включенных источников пакетов
1. Источники пакетов, зарегистрированных, но отключена
1. Источник по умолчанию для принудительной nuget.exe

Каждый из них теперь можно настроить в файле, расположенном в `%ProgramData%\NuGet\NuGetDefaults.Config`. Если этот файл конфигурации указывает источников пакетов, то источник пакета по умолчанию nuget.org не будет зарегистрирована автоматически и для них в `NuGetDefaults.Config` вместо этого будет зарегистрирована.

Не обязательно, чтобы использовать эту функцию, ожидается, что компании для развертывания `NuGetDefaults.Config` файлов с помощью групповой политики.

*Обратите внимание, что источник пакета, удаляемый из параметров разработчика NuGet никогда не вызывает эту функцию. Это значит, если разработчик уже использован NuGet и поэтому имеет источник пакета nuget.org зарегистрирован, он не будет удален после создания `NuGetDefaults.Config` файла.*

В разделе [по умолчанию используется конфигурация NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) Дополнительные сведения об этой функции.

### <a name="renaming-the-default-package-source"></a>Переименование источник пакета по умолчанию

NuGet всегда зарегистрировал источник пакета по умолчанию называется «Источник официального пакета NuGet», указывающий на nuget.org. Это имя было verbose и она также не указывать куда он фактически указывает. Для решения этих двух проблем переименовали этот источник пакета, чтобы просто «nuget.org» в пользовательском Интерфейсе. URL-адрес источника пакета также было изменено для включения «www». c префиксом "group.". После использования NuGet 2.7, вашей существующей «источник официального пакета NuGet» автоматически обновится до «nuget.org», как его имя и «<https://www.nuget.org/api/v2/>» как его URL-адрес.

### <a name="performance-improvements"></a>Улучшения производительности

Мы внесли некоторые улучшения производительности в 2.7, которое создаст меньше памяти, меньше использования диска и быстрее установки пакета. Мы также внесли оптимизированное запросов на основе OData веб-каналы, чтобы сократить количество общую полезных данных.

### <a name="new-extensibility-apis"></a>Новые API-интерфейсы расширяемости

Мы добавили некоторые новые интерфейсы API для наших служб расширяемости для заполнения пропуска отсутствующие функциональные возможности в предыдущих выпусках.

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>Зависимости только для разработки

Эта функция была, представленные [Ральф Адам](https://twitter.com/adamralph) и позволяет авторам пакетов для объявления зависимости, которые использовались только на этапе разработки, времени и не требуют зависимости пакетов. Добавив `developmentDependency="true"` атрибут пакета в `packages.config`, `nuget.exe pack` больше не будет включать этот пакет в качестве зависимости.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Прекращена поддержка Visual Studio 2010 Express для Windows Phone

Новая модель восстановления пакета в 2.7 реализуется новый пакет VSPackage, отличается от основного NuGet VSPackage. Из-за технической проблемы, этого нового пакета VSPackage не правильно работал в *Visual Studio 2010 Express для Windows Phone* SKU, так как мы использовать тот же базовый код совместно с другими поддерживается SKU Visual Studio. Таким образом, начиная с NuGet 2.7, мы пропускают поддержка *Visual Studio 2010 Express для Windows Phone* из опубликованного расширения. Поддержка *Visual Studio 2010 Express для Web* по-прежнему имеется в расширении первичного публикуются в коллекции расширений Visual Studio.

Так как мы не уверены, как многие разработчики по-прежнему используют NuGet в этой версии и выпуска Visual Studio, мы публикации отдельное расширение Visual Studio специально для тех пользователей и его публикации на сайте CodePlex (а не в коллекции расширений Visual Studio) . Мы не планируем сохранить этот модуль, но если это влияет на работу дайте нам знать, создайте проблемы на сайте CodePlex.

Загрузить диспетчер пакетов NuGet (для Visual Studio 2010 Express для Windows Phone), можно [загружает 2.7 NuGet](https://nuget.codeplex.com/releases/view/107605) страницы.

### <a name="bug-fixes"></a>Исправления ошибок

Помимо этих функций этого выпуска NuGet также включает много исправлений ошибок. Произошли 97 общее проблемы, описанные в выпуске. Полный список рабочих элементов исправления в NuGet 2.7 представление [NuGet отслеживания проблем в этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
