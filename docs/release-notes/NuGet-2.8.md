---
title: Заметки о выпуске NuGet 2.8 выпуска
description: Заметки о выпуске для NuGet 2.8, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547463"
---
# <a name="nuget-28-release-notes"></a>Заметки о выпуске NuGet 2.8 выпуска

[Заметки о выпуске NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [заметки о выпуске NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2.8 был выпущен 29 января 2014 г.

## <a name="acknowledgements"></a>Благодарности

1. [Притчарда Llewellyn](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) — когда упаковку в пакеты, проверка идентификатор зависимостей пакетов.
2. [Маартен Баллиау](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -удалить суффикс $metadata, при persistening учетные данные веб-канала.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - поддержки, указав файл проекта для команды nuget.exe обновления.
4. [Хуан Гонзалес](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -замена маркеров не пройдена с - IncludeReferencedProjects.
5. [Дэвид Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -исправить nuget.push генерации OutOfMemoryException при отправке большого пакета.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -исправление неправильный целевой путь, если проект ссылается на другой проект интерфейса командной строки/C++.
7. [Ральф ADAM](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -разрешает пакетам, которые должны быть установлены в зависимости разработки по умолчанию
8. [Дэвид Фаулер](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -удалить неявные обновления до последней версии исправления
9. [Грегори Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Устранено несколько ошибок и усовершенствования для NuGet.Server, команда nuget.exe зеркало и другие.
    - Эта работа выполнялась в течение нескольких месяцев с помощью Грегори совместную работу над правой синхронизации для интеграции в главную ветвь для 2.8.

## <a name="patch-resolution-for-dependencies"></a>Разрешение patch для зависимостей

При разрешении зависимостей пакета, NuGet Исторически реализовала стратегии выбора самую раннюю версию основной и дополнительный пакет, который удовлетворяет зависимостям для пакета. В отличие от основной и вспомогательной версии Однако версия исправления всегда разрешения до последней версии. На то, что поведение было намерениями, он создан отсутствия детерминизм для установки пакетов с зависимостями. Рассмотрим следующий пример.

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

В этом примере, даже если Developer1 Developer2 установки и PackageA@1.0.0, чтобы каждый завершена, вверх с другой версией PackageB. NuGet 2.8 изменяет это поведение по умолчанию, таким образом, режима разрешения зависимостей для версий исправлений согласуется с поведением для основного и дополнительного номеров версий. В приведенном выше примере, затем PackageB@1.0.0 устанавливается после установки PackageA@1.0.0, независимо от нового номера исправления.

## <a name="-dependencyversion-switch"></a>-DependencyVersion коммутатор

Хотя изменяет NuGet 2.8 _по умолчанию_ поведение для разрешения зависимостей, он также добавляет более точно контролировать процесс разрешения зависимостей с помощью параметра - DependencyVersion в консоли диспетчера пакетов. Параметр включает разрешение зависимостей для возможных самую раннюю версию (поведение по умолчанию), максимально возможный номер версии, или наивысший minor или версию исправления.  Этот параметр работает только для install-package в команду powershell.

![DependencyVersion коммутатора](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Атрибут DependencyVersion

Помимо параметра - DependencyVersion, рассмотренных в выше, NuGet также разрешил для возможности, чтобы задать новый атрибут в файле Nuget.Config определение что такое значение по умолчанию, если не указан параметр - DependencyVersion при вызове install-package. Это значение будет соблюдаться также в диалоговом окне диспетчера пакетов NuGet для всех операций установки пакета. Чтобы задать это значение, добавьте атрибут ниже в файл Nuget.Config.

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Просмотр операций NuGet с помощью - whatif

Некоторые пакеты NuGet могут иметь графами глубокой зависимости, и таким образом, он может пригодиться во время установки, удалить или обновить операцию, чтобы сначала посмотреть, что произойдет. NuGet 2.8 добавляет стандартный коммутатор - whatif PowerShell install-package, удалите пакет и команды update-package, чтобы включить визуализации всей замыкание пакетов, к которым применяется команда. Например, на котором работают `install-package Microsoft.AspNet.WebApi -whatif` в пустой веб-узел ASP.NET приложения, получится примерно следующее.

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a>Возврат к предыдущей версии пакета

Нередко установить предварительную версию пакета, чтобы изучить новые функции, а затем решить выполнить откат до последней стабильной версии. До NuGet 2.8 это было многоэтапный процесс, при удалении предварительной пакет и его зависимости, и последующая установка более ранней версии. С помощью NuGet 2.8 тем не менее, пакет обновления теперь откатит замыкание весь пакет (например дерево зависимостей пакета) к предыдущей версии.

## <a name="development-dependencies"></a>Зависимости разработки

Множество различных возможностей могут доставляться в виде пакетов NuGet - в том числе средства, которые используются для оптимизации процесса разработки. Эти компоненты, хотя они могут быть очень важна при разработке нового пакета, не должен считаться зависимость нового пакета при его позже публикации. NuGet 2.8 пакет можно идентифицировать себя в `.nuspec` файл в качестве developmentDependency. При установке, эти метаданные также будут добавляться в `packages.config` файл проекта, в которую был установлен пакет. Когда, `packages.config` файл позже проанализировать зависимости NuGet во время `nuget.exe pack`, оно не будет содержать эти зависимости, которые помечены как зависимости разработки.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Файлы отдельных packages.config для различных платформ

При разработке приложений для нескольких целевых платформ, это часто используются для каждой из сред сборки в соответствующих файлах разных проектов. Также часто бывает для получения различных пакетов NuGet в разных файлах проекта, так как пакеты имеют различные уровни поддержки для различных платформ. NuGet 2.8 обеспечивает улучшенную поддержку для этого сценария, создавая другой `packages.config` файлов для файлов разных проекта под конкретную платформу.

![Несколько файлов package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Переход к локального кэша

Хотя пакеты NuGet обычно используются такие как из удаленной коллекции [коллекции NuGet](http://www.nuget.org/) использования сетевого подключения, существует множество сценариев, где клиент не подключен. Без подключения к сети клиент NuGet не удалось успешно установить пакеты - даже в том случае, если эти пакеты уже были на клиентском компьютере в локальном кэше NuGet. NuGet 2.8 добавляет автоматического Резервный кэш консоли диспетчера пакетов. Например, при отключении сетевого адаптера и установка jQuery, консоли содержит следующую информацию:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Функции резервного кэша не требуют аргументов определенную команду. Кроме того резервный кэш в настоящее время работает только в консоли диспетчера пакетов - поведение не работает в данный момент в диалоговом окне диспетчера пакетов.

## <a name="webmatrix-nuget-client-updates"></a>Обновляет клиент NuGet WebMatrix

Вместе с NuGet 2.8 расширения NuGet для WebMatrix также обновляется, чтобы добавить многие из основных возможностей, обеспечиваемых [NuGet 2.5](../release-notes/nuget-2.5.md). Новые возможности включают те, такие как «Обновить все», «Минимальная версия NuGet» и позволяя для перезаписи содержимого файлов.

Чтобы обновить расширение диспетчера пакетов NuGet в WebMatrix 3:

1. Откройте WebMatrix 3
1. Щелкните значок расширения на ленте
1. Выберите вкладку "обновления"
1. Щелкните, чтобы обновить диспетчер пакетов NuGet для 2.5.0
1. Закройте и перезапустите WebMatrix 3

Это первый выпуск команда NuGet расширения диспетчера пакетов NuGet для WebMatrix.  Код был недавно добавленные корпорацией Майкрософт в проект NuGet открытым исходным кодом. Ранее интеграцию с NuGet была встроена в WebMatrix, и его не удалось обновить аппаратного из WebMatrix.  Теперь у нас есть возможность последующего обновления его вместе с остальной части клиентских средств NuGet.

## <a name="bug-fixes"></a>Исправления ошибок

Одним из основных ошибок исправления, внесенные было улучшение производительности в пакете обновления-переустановить команды.

Помимо этих возможностей и исправления производительности, упомянутых выше этот выпуск NuGet также включает много исправлений ошибок. Возникали 181 общее проблемы, описанной в выпуске. Полный список рабочих элементов исправленные в NuGet 2.8 обратитесь представление [Issue Tracker NuGet для этого выпуска](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
