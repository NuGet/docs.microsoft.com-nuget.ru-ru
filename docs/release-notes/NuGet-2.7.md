---
title: Заметки о выпуске для NuGet 2.7 выпуска
description: Заметки о выпуске для NuGet 2.7, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550969"
---
# <a name="nuget-27-release-notes"></a>Заметки о выпуске для NuGet 2.7 выпуска

[NuGet 2.6.1 для WebMatrix заметки](../release-notes/nuget-2.6.1-for-webmatrix.md) | [заметки о выпуске NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

NuGet 2.7 было выпущено 22 августа 2013 г.

## <a name="acknowledgements"></a>Благодарности

Мы бы хотели поблагодарить следующих внешних участников для их вклад в NuGet 2.7:

1. [Майк рот](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Показать URL-адрес лицензии, если список пакетов и уровень детализации подробно описан.
2. [Ральф ADAM](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -добавить атрибут developmentDependency в `packages.config` и использовать его в пакет команд для включения только пакеты среды выполнения
3. [Рафаэль Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Избегайте повторяющийся ключ свойства в команде пакет nuget.exe.
4. [Бен Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -увеличение размера кэша машины до размера 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -диалоговое окно устранения NuGet, отображение обновлений на вкладке "Ошибка"
    - Исправление Project.TargetFramework может иметь значение null, если в РуководительПроекта
    - [#3248](http://nuget.codeplex.com/workitem/3248) -на несуществующие packageId не удастся устранить SharedPackageRepository FindPackage/FindPackagesById
6. [Кевин Бойл](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -включить поддержку Nomad проекта
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -исправление ошибки команды Push-уведомлений с выхода код 0, если файл не существует.
8. [Мартин Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -исправить ошибку с помощью команды Add-BindingRedirect, если проект ссылается на проект базы данных.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -исправить ошибку из nuget.pack неправильно синтаксический анализ шаблона в атрибуте «исключить».
10. [Джастин Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -исправить ошибку `NuGet.targets` не передает $(Platform) nuget.exe при восстановлении пакетов.
11. [Брайан Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -исправить ошибку в команде пакет nuget.exe, что позволит добавлять файлы с тем же именем, но в разных регистрах, в результате чего исключение «Элемент уже существует».
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -свойство Version, добавьте к классу NetPortableProfile.
13. [Дэвид Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -исправлена ошибка NullReferenceException, если requireApiKey = true, но заголовок X-NUGET-APIKEY отсутствует
14. [Майкл Фриис](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -файл исправления NuGet.Build целевых объектов таким образом, чтобы оно правильно работает на MonoDevelop
15. [Получения Кришнамурти](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Повысить производительность команды Restore, увеличив параллелизации

## <a name="notable-features-in-the-release"></a>Важные возможности в выпуске

### <a name="package-restore-by-default-with-implicit-consent"></a>Восстановление пакетов по умолчанию (с согласия)

Представляет новый подход к восстановление пакета NuGet 2.7 и решены основных полноценной: согласия пакет восстановления теперь включен по умолчанию! Сочетание новый подход и явного согласия значительно упростит сценарии восстановления пакета.

#### <a name="implicit-consent"></a>Согласия

В версиях NuGet, 2.0, 2.1, 2.2, 2.5 и 2.6 пользователям необходимо явным образом разрешить NuGet скачивать отсутствующие пакеты во время построения. Если это согласие не было явным образом предоставлено, то решения, которые включены восстановление пакетов не сможет строятся, пока ему предоставлены разрешения.

Начиная с NuGet 2.7, согласия восстановления пакета включено по умолчанию дает возможность пользователям явно *отказаться* восстановления пакетов, при необходимости, с помощью флажка в параметрах NuGet в Visual Studio. Это изменение для явного согласия затрагивает NuGet в следующих средах:

* Предварительная версия Visual Studio 2013
* Visual Studio 2012
* Visual Studio 2010
* Программа командной строки NuGet.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Автоматическое восстановление пакетов в Visual Studio

Начиная с NuGet 2.7, NuGet автоматически загрузит отсутствующие пакеты во время сборки в Visual Studio, даже если восстановление пакетов не были явно включены для решения. Это автоматическое восстановление пакетов производится в Visual Studio, при сборке проекта или решения, но перед вызовом MSBuild. Это обеспечивает несколько значительные преимущества:

1. Больше не нужно использовать жест «Включить восстановление пакета NuGet» в решении
1. Проекты не нужно изменить, и NuGet не будет вносить изменения в проект, чтобы убедиться, что включается восстановление пакетов
1. Восстанавливаются все пакеты NuGet, включая те, которые включены импорты MSBuild для файлов, свойства и целевые объекты, *перед* MSBuild вызывается, обеспечивая эти свойства и целевые объекты правильного распознавания во время сборки

Только, чтобы использовать автоматическое восстановление пакетов в Visual Studio, необходимо выполнить одно (действие в):

1. Не устанавливайте флажок вашей `packages` папки

Существует несколько способов для пропуска вашей `packages` папку из системы управления версиями. Дополнительные сведения см. в разделе [пакеты и система управления версиями](../consume-packages/packages-and-source-control.md) раздела.

Хотя все пользователи являются неявно согласие согласия, автоматическое восстановление пакетов, можно легко отказаться через параметры диспетчера пакетов в Visual Studio.

![Параметры диспетчера пакетов](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Восстановление упрощенного пакета из командной строки

NuGet 2.7 появилась новая функция для nuget.exe: `nuget.exe restore`

Эта новая команда Restore позволяет легко восстановить все пакеты для решения с помощью одной команды, принимая решения файла или папки в качестве аргумента. Кроме того этот аргумент предусмотрено, при наличии только одного решения в текущей папке. Это означает, что все следующие работать из папки, содержащей файл единое решение (MySolution.sln):

1. Восстановление NuGet.exe MySolution.sln
1. Восстановление NuGet.exe.
1. Восстановление NuGet.exe

Команда восстановления откройте файл решения и найти все проекты в решении. После этого будут найдены `packages.config` файлы для всех проектов и восстановления, найти все пакеты. Он также восстанавливает пакеты уровня решения в `.nuget\packages.config` файл. Дополнительные сведения о новой команды восстановления можно найти в [справочнике по командной строке](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Новый рабочий процесс восстановления пакета

Мы рады об этих изменениях, чтобы восстановить пакет, так как он вводит новый рабочий процесс. Если вы хотите пропустить пакеты из системы управления версиями просто не будет зафиксирован `packages` папки. Пользователи Visual Studio, откройте и постройте решение увидите пакеты, восстановленные автоматически. Для построения из командной строки, просто вызвать `nuget.exe restore` перед вызовом `msbuild`. Вам больше не нужно не забывайте использовать жест «Включить восстановление пакета NuGet» на своем решении, и мы больше не нужно изменять проекты для изменения сборки. И это также дает возможность значительно улучшенную для пакетов, содержащих импорты MSBuild, особенно для импортов, добавленные с помощью NuGet из новых функций для [автоматического импорта свойства и целевые объекты файлы](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) из папки \build.

Помимо работы, мы сделали сами мы также работаем с некоторыми важные захотелось этого нового подхода. У нас конкретные временные шкалы для любой из них еще нет, но каждый партнер — это как интересно, как мы о новый подход.

* Team Foundation Service — они работаем над интеграцией вызов `nuget.exe restore` в значение по умолчанию построения.
* Windows Azure Web Sites - они работают над можно отправить проект в Azure и иметь `nuget.exe restore` вызывается перед построением веб-сайт.
* TeamCity — они обновляют их установщика NuGet подключаемый модуль для TeamCity 8.x
* AppHarbor — они работают над позволяют отправьте репозиторий в AppHarbor и иметь `nuget.exe restore` вызывается перед построения решения.

С каждым из участников выше они будут использовать свою собственную копию nuget.exe и не потребовалось бы для выполнения nuget.exe в решении.

#### <a name="known-issues"></a>Известные проблемы

За два известных проблем с nuget.exe restore с первоначального выпуска 2.7, но они были устранены на 9/6/2013 с обновлением [NuGet.CommandLine пакета](http://www.nuget.org/packages/NuGet.CommandLine/).  Это обновление также доступно на [страницу скачивания NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) на сайте CodePlex.  Под управлением `nuget.exe update -self` будет обновляться до последней версии.

Фиксированного были:

1. [При использовании файла SLN новый восстановление пакетов не работает на Mono](https://nuget.codeplex.com/workitem/3596)
1. [Новый восстановление пакетов не работает с проектами Wix](https://nuget.codeplex.com/workitem/3598)

Имеется известная проблема, новый рабочий процесс восстановления пакета при котором [автоматическое восстановление пакетов не работает для проектов в папке решения](https://nuget.codeplex.com/workitem/3625). Эта проблема была исправлена в NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Изменение целевой платформы проекта и обновление сборки ошибок и предупреждений

Много раз после перенацеливании или обновлении проекта, обнаружится, что некоторые пакеты NuGet не работает должным образом. К сожалению нет никаких признаков того, это и есть нет рекомендаций о том, как для решения этой проблемы. С помощью NuGet 2.7 теперь мы используем некоторые события Visual Studio с, когда перенацелен или обновлен проект способом, который влияет на установленные пакеты NuGet.

Если будет обнаружено, что все пакеты были затронуты при перенацеливании или обновления, мы будет приводить к ошибкам сборки, немедленно сообщить вам о. В дополнение к ошибки интерпретации сборки, мы будем продолжать `requireReinstallation="true"` флаг в вашей `packages.config` файл все пакеты, которые были зависит от целевой платформы и каждое последующее сборке в Visual Studio вызывает предупреждения сборки для этих пакетов.

Несмотря на то, что NuGet не может предпринимать автоматические действия для переустановки затрагиваемые пакеты, мы надеемся, что это значение, указывающее, и предупреждение поможет справки вы обнаруживаете, если вам нужно переустановить пакеты. Мы также работаем над [пакетов переустановка документацией](../consume-packages/reinstalling-and-updating-packages.md) , эти сообщения об ошибках указывают на необходимость.

### <a name="nuget-configuration-defaults"></a>По умолчанию конфигурация NuGet

Многие компании при использовании NuGet внутренне, но было сложно руководство для разработчиков, их для использования источников внутренних пакетов вместо nuget.org. NuGet 2.7 представлена функция настройки по умолчанию, которая позволяет компьютера значения по умолчанию для:

1. Источники пакетов включена
1. Зарегистрировано, но Отключенные источники пакетов
1. Источник по умолчанию nuget.exe Push-уведомлений

Каждый из них теперь можно настроить в файл, расположенный в `%ProgramData%\NuGet\NuGetDefaults.Config`. Если этот файл конфигурации задает источники пакетов, а затем автоматически, не будет зарегистрирован источник пакетов nuget.org по умолчанию и для них в `NuGetDefaults.Config` вместо этого будет зарегистрировано.

Хотя не требуется, чтобы использовать эту функцию, мы ожидаем, что организациям развертывать `NuGetDefaults.Config` файлов с помощью групповой политики.

*Обратите внимание, что эта функция никогда не вызовет источника пакета, удаляемый из параметров NuGet разработчика. Это означает, если разработчик уже использовал NuGet и поэтому имеет источник пакетов nuget.org зарегистрировано, он не будет использован после создания `NuGetDefaults.Config` файла.*

См. в разделе [по умолчанию используется конфигурация NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) Дополнительные сведения об этой функции.

### <a name="renaming-the-default-package-source"></a>Переименование источника пакетов по умолчанию

NuGet всегда зарегистрирован источник пакета по умолчанию называется «Источник официального пакета NuGet», указывающий на сайте nuget.org. Это имя было verbose и она также не указывать куда он фактически указывает. Для решения этих двух проблем, мы переименовали этого источника пакетов просто «NuGet.org» в пользовательском Интерфейсе. URL-адрес источника пакета также был изменен для включения «www.» c префиксом "group.". После использования NuGet 2.7, ваши существующие «источник официального пакета NuGet» автоматически обновляется «NuGet.org», как его имя и "<https://www.nuget.org/api/v2/>" как его URL-адрес.

### <a name="performance-improvements"></a>Улучшения производительности

Мы внесли некоторые улучшения производительности в 2.7, которое создаст меньше памяти, меньше использования диска и Ускоренная установка пакета. Мы также внесли более интеллектуальные запросы на основе OData веб-каналы, чтобы сократить общее полезных данных.

### <a name="new-extensibility-apis"></a>Новые интерфейсы API расширяемости

Мы добавили некоторые новые интерфейсы API для наших служб расширяемости для восполнения отсутствует функциональных возможностей в предыдущих выпусках.

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

Эта функция была порожденного [Ральф Adam](https://twitter.com/adamralph) и позволяет создателям пакетов объявление зависимостей, которые использовались только на этапе разработки, времени и не требуют зависимости пакетов. Добавив `developmentDependency="true"` атрибут в пакет в `packages.config`, `nuget.exe pack` больше не будет включать этот пакет как зависимость.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Удалена поддержка для Visual Studio 2010 Express для Windows Phone

Новая модель восстановления пакета в 2.7 реализуется нового пакета VSPackage, который отличается от основного NuGet VSPackage. Из-за технической проблемы, этого нового пакета VSPackage не правильно работал в *Visual Studio 2010 Express для Windows Phone* номер SKU, что мы организуем той же базе кода с другими поддерживается SKU Visual Studio. Таким образом, начиная с NuGet 2.7, мы пропускают поддержка *Visual Studio 2010 Express для Windows Phone* из опубликованных расширений. Поддержка *Visual Studio 2010 Express для Web* по-прежнему включается в основной добавочный номер, опубликованные в коллекции расширений Visual Studio.

Так как мы не уверены, как многие разработчики по-прежнему используете NuGet в этой версии или выпуска Visual Studio, мы публикации использовать отдельное расширение Visual Studio специально для тех пользователей и его публикации на CodePlex (а не коллекция расширений Visual Studio) . Мы не планируем сохранить этот модуль, но если это влияет на работу свяжитесь с нами можно на сайте CodePlex.

Чтобы скачать диспетчер пакетов NuGet (для Visual Studio 2010 Express для Windows Phone), посетите [для скачивания NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) страницы.

### <a name="bug-fixes"></a>Исправления ошибок

Помимо этих функций в этот выпуск NuGet также включает много исправлений ошибок. Возникали 97 общее проблемы, описанной в выпуске. Полный список рабочих элементов исправленные в NuGet 2.7. представление [Issue Tracker NuGet для этого выпуска](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
