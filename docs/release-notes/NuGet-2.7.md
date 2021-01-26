---
title: Заметки о выпуске NuGet 2,7
description: Заметки о выпуске NuGet 2,7, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 70600e3c563e357663b4a2f24139d2fc25f75fdf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780400"
---
# <a name="nuget-27-release-notes"></a>Заметки о выпуске NuGet 2,7

[Заметки о](../release-notes/nuget-2.6.1-for-webmatrix.md)  |  выпуске NuGet 2.6.1 для WebMatrix [Заметки о выпуске 2.7.1 NuGet](../release-notes/nuget-2.7.1.md)

Версия NuGet 2,7 была выпущена 22 августа 2013.

## <a name="acknowledgements"></a>Благодарности

Мы хотели бы поблагодарить следующих внешних участников для значительного вклада в NuGet 2,7:

1. [Майк Roth)](http://www.codeplex.com/site/users/view/mxrss) ( [@mxrss](https://twitter.com/mxrss) )
    - Отображать URL-адрес лицензии при перечислении пакетов и подробностей.
2. [Адам Ральф](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#1956](http://nuget.codeplex.com/workitem/1956) добавить атрибут developmentDependency в `packages.config` и использовать его в команде Pack для включения только пакетов среды выполнения
3. [Рафаэль Николетти](http://www.codeplex.com/site/users/view/tkrafael) ( [@tkrafael](https://twitter.com/tkrafael) )
    - Избегайте дублирования ключей свойств в команде nuget.exe Pack.
4. [Бен Феган](http://www.codeplex.com/site/users/view/benphegan) ( [@BenPhegan](https://twitter.com/benphegan) )
    - [#2610](http://nuget.codeplex.com/workitem/2610) увеличить размер кэша компьютера до 200.
5. [Слава треногин](http://www.codeplex.com/site/users/view/derigel) ( [@derigel](https://twitter.com/derigel) )
    - [#3217](http://nuget.codeplex.com/workitem/3217) — исправить диалоговое окно NuGet, в котором отображаются обновления на неправильной вкладке
    - Исправление Project. TargetFramework может иметь значение NULL в Прожектманажер
    - [#3248](http://nuget.codeplex.com/workitem/3248) -Fix шаредпаккажерепоситори Финдпаккаже/финдпаккажесбид не будет работать на несуществующем packageId
6. [Кевин Бойле](http://www.codeplex.com/site/users/view/KevinBoyleRG) ( [@kevfromireland](https://twitter.com/kevfromireland) )
    - [#3234](http://nuget.codeplex.com/workitem/3234) — включить поддержку для проекта Номад
7. [Корин блаикие](http://www.codeplex.com/site/users/view/corinblaikie) ( [@corinblaikie](https://twitter.com/corinblaikie) )
    - [#3252](http://nuget.codeplex.com/workitem/3252) -Fix Push команда завершается с кодом завершения 0, если файл не существует.
8. [Мартен Веселý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) — исправьте ошибку с помощью команды Add-BindingRedirect, когда проект ссылается на проект базы данных.
9. [Мирослав бажтос](http://www.codeplex.com/site/users/view/miroslavbajtos) ( [@bajtos](https://twitter.com/bajtos) )
    - [#2891](http://nuget.codeplex.com/workitem/2891) — исправление ошибки в атрибуте Exclude в неправильном шаблоне синтаксического анализа NuGet. Pack.
10. [Джастин Уважаемый](http://www.codeplex.com/site/users/view/zippy1981) ( [@zippy1981](https://twitter.com/zippy1981) )
     - [#3307](http://nuget.codeplex.com/workitem/3307) — исправление ошибки `NuGet.targets` не передает $ (Platform) в nuget.exe при восстановлении пакетов.
11. [Брайан ФедериЦи](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) исправить ошибку в команде nuget.exe пакета, которая позволяла добавлять файлы с тем же именем, но с разным регистром, в конечном итоге вызывая исключение "элемент уже существует".
12. [Даниэль каззулино](http://www.codeplex.com/site/users/view/dcazzulino) ( [@kzu](https://twitter.com/kzu) )
     - [#2990](http://nuget.codeplex.com/workitem/2990) — добавить свойство Version в класс нетпортаблепрофиле.
13. [Дэвид Симнер](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) — исправьте ошибку NullReferenceException, если рекуиреапикэй = true, но заголовок X-NUGET-APIKEY отсутствует
14. [Майкл Фриис](https://www.codeplex.com/site/users/view/friism) ( [@friism](https://twitter.com/friism) )
     - [#3278](https://nuget.codeplex.com/workitem/3278) — исправляет файл целевых объектов NuGet. Build в, чтобы он правильно работал в MonoDevelop
15. [Получения кришнамурси](https://www.codeplex.com/site/users/view/pranavkm) ( [@pranav_km](https://twitter.com/pranav_km) )
     - Повышение производительности команды восстановления путем увеличения параллелизма

## <a name="notable-features-in-the-release"></a>Важные функции в выпуске

### <a name="package-restore-by-default-with-implicit-consent"></a>Восстановление пакетов по умолчанию (с неявным согласием)

В NuGet 2,7 появился новый подход к восстановлению пакетов, а также основные препятствия: согласие на восстановление пакетов теперь включено по умолчанию! Сочетание нового подхода и неявного согласия значительно упрощает сценарии восстановления пакетов.

#### <a name="implicit-consent"></a>Неявное согласие

С помощью NuGet версий 2,0, 2,1, 2,2, 2,5 и 2,6 пользователям необходимо явно разрешить NuGet скачивать недостающие пакеты во время сборки. Если это согласие не было явно указано, то решения, для которых было включено восстановление пакетов, не смогут выполнить сборку, пока пользователь не предоставил согласие.

Начиная с NuGet 2,7, согласие на восстановление пакетов включено по умолчанию, в то же время предоставляя пользователям возможность явно *отказаться* от восстановления пакета при необходимости, используя флажок в параметрах NuGet в Visual Studio. Это изменение для неявного согласия затрагивает NuGet в следующих средах:

* Предварительная версия Visual Studio 2013
* Visual Studio 2012
* Visual Studio 2010
* Служебная программа nuget.exe Command-Line

#### <a name="automatic-package-restore-in-visual-studio"></a>Автоматическое восстановление пакетов в Visual Studio

Начиная с NuGet 2,7, NuGet автоматически скачивает недостающие пакеты во время сборки в Visual Studio, даже если для решения не было явно включено восстановление пакетов. Автоматическое восстановление пакетов происходит в Visual Studio при построении проекта или решения, но до вызова MSBuild. Это дает несколько существенных преимуществ.

1. Для решения не нужно использовать жест "включить восстановление пакетов NuGet".
1. Проекты не нужно изменять, и NuGet не вносит изменения в проект, чтобы обеспечить включение восстановления пакетов.
1. Все пакеты NuGet, включая те, которые включали в себя операции импорта MSBuild для файлов PROPS/targets, будут восстановлены *перед* вызовом MSBuild, гарантируя, что эти свойства и целевые объекты должным образом распознаются во время сборки.

Чтобы использовать автоматическое восстановление пакетов в Visual Studio, необходимо выполнить только одно действие (в):

1. Не возвращать `packages` папку

Существует несколько способов опустить `packages` папку в системе управления версиями. Дополнительные сведения см. в разделе [пакеты и система управления версиями](../consume-packages/packages-and-source-control.md) .

Хотя все пользователи неявно согласие на автоматическое восстановление пакетов, вы можете легко отказаться от параметров диспетчера пакетов в Visual Studio.

![Параметры диспетчера пакетов](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Упрощенное восстановление пакетов из Command-Line

NuGet 2,7 вводит новую функцию для nuget.exe: `nuget.exe restore`

Эта новая команда Restore позволяет легко восстановить все пакеты решения с помощью одной команды, принимая файл решения или папку в качестве аргумента. Кроме того, этот аргумент подразумевается, если в текущей папке имеется только одно решение. Это означает, что следующая вся работа из папки, содержащей один файл решения (MySolution. sln):

1. nuget.exe восстановить MySolution. sln
1. nuget.exe восстановить.
1. Восстановление nuget.exe

Команда Restore открывает файл решения и находит все проекты в решении. После этого будут найдены `packages.config` файлы для каждого проекта и восстановлены все найденные пакеты. Он также восстанавливает пакеты уровня решения, найденные в `.nuget\packages.config` файле. Дополнительные сведения о новой команде RESTORE можно найти в [справочнике по командной строке](../reference/cli-reference/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Рабочий процесс восстановления нового пакета

Мы рады, что эти изменения были внесены в восстановление пакета, так как в нем появился новый рабочий процесс. Если вы хотите исключить пакеты из системы управления версиями, просто не зафиксируйте `packages` папку. Пользователи Visual Studio, которые открывают и производили сборку решения, увидят, что пакеты будут автоматически восстановлены. Для сборок из командной строки просто вызывается `nuget.exe restore` перед вызовом `msbuild` . Больше не нужно забывать использовать в решении жест "включить восстановление пакетов NuGet", и больше не нужно изменять проекты для изменения сборки. Кроме того, это обеспечивает значительно улучшенный интерфейс для пакетов, включающих импорты MSBuild, особенно для импорта, добавленных с помощью функции "Недавние" в NuGet, для [автоматического импорта файлов PROPS/targets](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) из папки \буилд.

В дополнение к выполненной работе мы также работаем с некоторыми важными партнерами для округления этого нового подхода. У нас пока нет конкретных временных шкал, но каждый из них очень напоминает новый подход.

* Team Foundation Service — они работают для интеграции вызова в `nuget.exe restore` сценарии сборки по умолчанию.
* Веб-сайты Windows Azure. они работают, чтобы вы могли отправить проект в Azure и вызвать его `nuget.exe restore` до создания веб-сайта.
* TeamCity — они обновляют подключаемый модуль установщика NuGet для TeamCity 8. x
* Апфарбор — они работают, чтобы вы могли передать свой репозиторий в Апфарбор и `nuget.exe restore` вызывали его до сборки решения.

Для каждого из упомянутых выше партнеров они будут использовать собственную копию nuget.exe и вам не нужно будет nuget.exe в решении.

#### <a name="known-issues"></a>Известные проблемы

Существует две известные проблемы с nuget.exeным восстановлением с первоначальным выпуском 2,7, но они были исправлены на 9/6/2013 с обновлением [пакета NuGet. commandline](http://www.nuget.org/packages/NuGet.CommandLine/).  Это обновление также доступно на [странице загрузки NuGet 2,7](https://nuget.codeplex.com/releases/view/107605) на сайте CodePlex.  Выполнение `nuget.exe update -self` обновится до последнего выпуска.

Исправлено:

1. [Восстановление нового пакета не работает на Mono при использовании файла SLN](https://nuget.codeplex.com/workitem/3596)
1. [Восстановление нового пакета не работает с проектами WiX](https://nuget.codeplex.com/workitem/3598)

Существует также известная ошибка в новом рабочем процессе восстановления пакета, в ходе которой [Автоматическое восстановление пакетов не работает для проектов в папке решения](https://nuget.codeplex.com/workitem/3625). Эта проблема была исправлена в NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Изменение целевой платформы проекта и обновление ошибок и предупреждений сборки

Несколько раз после перенацеленности или обновления проекта вы обнаружите, что некоторые пакеты NuGet работают неправильно. К сожалению, это не означает, что нет рекомендаций по ее устранению. С помощью NuGet 2,7 мы теперь можем использовать некоторые события Visual Studio, чтобы распознать, когда вы перенацелены на проект или обновили его в то же время, что влияет на установленные пакеты NuGet.

Если мы обнаружите, что какие бы то ни было пакеты были затронуты изменением целевой платформы или обновлением, мы выберем немедленные ошибки сборки, чтобы вы могли знать. В дополнение к немедленной ошибке сборки мы также сохраняем `requireReinstallation="true"` флаг в `packages.config` файле для всех пакетов, которые затронули изменение целевой платформы, и каждая последующая сборка в Visual Studio будет вызывать предупреждения сборки для этих пакетов.

Несмотря на то, что NuGet не может выполнить автоматическое действие для переустановки затронутых пакетов, мы надеемся, что эта индикация и предупреждение помогут вам обнаружить необходимость переустановки пакетов. Мы также работаем над [руководством по переустановке пакетов](../consume-packages/reinstalling-and-updating-packages.md) , на которое направляются эти сообщения об ошибках.

### <a name="nuget-configuration-defaults"></a>Параметры конфигурации NuGet по умолчанию

Многие компании используют NuGet на внутреннем уровне, но имели жесткое время, чтобы разработчики использовали внутренние источники пакетов, а не nuget.org. NuGet 2,7 вводит функцию конфигурации по умолчанию, которая позволяет указать значения по умолчанию для всей машины для:

1. Включенные источники пакетов
1. Зарегистрированные, но отключенные источники пакетов
1. Источник nuget.exe push-уведомлений по умолчанию

Теперь каждый из них можно настроить в файле, расположенном в папке `%ProgramData%\NuGet\NuGetDefaults.Config` . Если в этом файле конфигурации указаны источники пакетов, то источник пакетов nuget.org по умолчанию не будет автоматически зарегистрирован, а `NuGetDefaults.Config` вместо этого будут зарегистрированы.

Хотя для использования этой функции не требуется, компании должны развертывать `NuGetDefaults.Config` файлы с помощью групповая политика.

*Обратите внимание, что эта функция никогда не приведет к удалению источника пакета из параметров NuGet разработчика. Это означает, что если разработчик уже использовал NuGet и, следовательно, зарегистрирован источник пакета nuget.org, он не будет удален после создания `NuGetDefaults.Config` файла.*

Дополнительные сведения об этой функции см. в разделе [Параметры конфигурации NuGet по умолчанию](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) .

### <a name="renaming-the-default-package-source"></a>Переименование источника пакета по умолчанию

NuGet всегда зарегистрировал источник пакета по умолчанию с именем "официальный источник пакета NuGet", указывающий на nuget.org. Это имя было подробным, а также не указал там, где он был на самом деле указывал. Чтобы устранить эти две проблемы, мы переименовали этот источник пакета, просто "nuget.org" в пользовательском интерфейсе. URL-адрес источника пакета был также изменен для включения www. . После использования NuGet 2,7 существующий "официальный источник пакета NuGet" будет автоматически обновлен до "nuget.org" в качестве своего имени и " <https://www.nuget.org/api/v2/> " в качестве URL-адреса.

### <a name="performance-improvements"></a>Повышение производительности

Мы внесли некоторое повышение производительности в 2,7, что приведет к уменьшению объема памяти, уменьшению использования диска и ускоренной установке пакета. Мы также сделали более интеллектуальные запросы к каналам на основе OData, которые будут снижать общую полезную нагрузку.

### <a name="new-extensibility-apis"></a>Новые API расширяемости

Мы добавили новые интерфейсы API в наши службы расширения для заполнения зазора недостающих функций в предыдущих выпусках.

#### <a name="ivspackageinstallerservices"></a>ивспаккажеинсталлерсервицес

```cs
// Checks if a NuGet package with the specified Id and version is installed in the specified project.
bool IsPackageInstalledEx(Project project, string id, string versionString);

// Get the list of NuGet packages installed in the specified project.
IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
```

#### <a name="ivspackageinstaller"></a>ивспаккажеинсталлер

```cs
// Installs one or more packages that exist on disk in a folder defined in the registry.
void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

// Installs one or more packages that are embedded in a Visual Studio Extension Package.
void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
```

### <a name="development-only-dependencies"></a>Зависимости Development-Only

Эта функция была создана [ADAM Ральф](https://twitter.com/adamralph) и позволяет авторам пакетов объявлять зависимости, которые использовались только во время разработки и не нуждаются в зависимостях пакетов. Если добавить `developmentDependency="true"` атрибут в пакет в `packages.config` , `nuget.exe pack` он больше не будет включать этот пакет в качестве зависимости.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Удалена поддержка Visual Studio 2010 Express для Windows Phone

Новая модель восстановления пакетов в 2,7 реализуется новым пакетом VSPackage, который отличается от основного пакета пакетов NuGet. Из-за технической проблемы этот новый пакет VSPackage не работает правильно в *Visual studio 2010 Express для Windows Phone* SKU, так как мы совместно используем ту же базу кода с другими поддерживаемыми номерами SKU Visual Studio. Поэтому начиная с NuGet 2,7 мы отменяем поддержку *Visual Studio 2010 Express для Windows Phone* из опубликованного расширения. Поддержка *Visual studio 2010 Express для Web* по-прежнему включена в основное расширение, опубликованное в галерее расширений Visual Studio.

Поскольку мы не уверены, сколько разработчиков все еще используют NuGet в этой версии или выпуске Visual Studio, мы публикуем отдельное расширение Visual Studio специально для этих пользователей и публикуем их на CodePlex (а не в галерее расширений Visual Studio). Мы не планируем продолжать поддерживать это расширение, но если это повлияет на вас, сообщите нам о наличии проблемы на сайте CodePlex.

Чтобы скачать диспетчер пакетов NuGet (для Visual Studio 2010 Express для Windows Phone), посетите страницу [загрузки NuGet 2,7](https://nuget.codeplex.com/releases/view/107605) .

### <a name="bug-fixes"></a>Исправления ошибок

Помимо этих функций, в этом выпуске NuGet также содержится множество исправлений ошибок. В выпуске было 97о общих проблем. Полный список рабочих элементов, исправленных в NuGet 2,7, см. в [этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
