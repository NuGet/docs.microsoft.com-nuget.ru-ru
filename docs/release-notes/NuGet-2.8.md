---
title: Заметки о выпуске NuGet 2,8
description: Заметки о выпуске NuGet 2,8, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428357"
---
# <a name="nuget-28-release-notes"></a>Заметки о выпуске NuGet 2,8

[Заметки о выпуске NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [заметки о выпуске NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

Версия NuGet 2,8 была выпущена 29 января 2014 г.

## <a name="acknowledgements"></a>Благодарности

1. [Ллевеллин Притчард](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) — при упаковке пакетов проверяет идентификатор пакетов зависимостей.
2. [Мартен-Balliauw)](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) — удалите суффикс $Metadata при учетных данных веб-канала персистенинг.
3. [Филип de вос](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) — поддержка указания файла проекта для команды NuGet. exe Update.
4. [Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - токены замены [#3536](http://nuget.codeplex.com/workitem/3536) не передаются с помощью-инклудереференцедпрожектс.
5. [Дэвид пуле](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -Fix NuGet. push OutOfMemoryException при помещении большого пакета.
6. [Ваутер Аувенс](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) — исправьте неверный целевой путь, если проект ссылаетсяC++ на другой интерфейс командной строки или проект.
7. [Адам Ральф](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) — разрешить установку пакетов в качестве зависимостей разработки по умолчанию
8. [Дэвид Фаулер](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) — удалить неявные обновления до последней версии исправления
9. [Грегори Ванденбраукк](https://www.codeplex.com/site/users/view/vdbg)
    - Некоторые исправления ошибок и улучшения для NuGet. Server, команда NuGet. exe Mirror и другие.
    - Эта работа была выполнена в течение нескольких месяцев, а Грегори работает с нами в соответствии со временем, чтобы интегрироваться в главную базу для 2,8.

## <a name="patch-resolution-for-dependencies"></a>Разрешение исправлений для зависимостей

При разрешении зависимостей пакетов NuGet реализовала стратегию выбора наименьшей основной и дополнительной версии пакета, удовлетворяющей зависимостям пакета. Однако, в отличие от основной и дополнительной версий, версия исправления всегда была решена до самой высокой версии. Хотя поведение было хорошо намерено, было создано отсутствие детерминированности при установке пакетов с зависимостями. Рассмотрим следующий пример:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

В этом примере, несмотря на то, что Developer1 и Developer2 установлен PackageA@1.0.0, каждый из них завершился с другой версией Паккажеб. NuGet 2,8 изменяет это поведение по умолчанию таким образом, что поведение разрешения зависимостей для версий исправлений согласуется с поведением для основных и вспомогательных версий. В приведенном выше примере PackageB@1.0.0 будет установлен в результате установки PackageA@1.0.0, независимо от более новой версии исправления.

## <a name="-dependencyversion-switch"></a>Параметр-Депенденциверсион

Хотя NuGet 2,8 изменяет поведение _по умолчанию_ для разрешения зависимостей, оно также добавляет более точный контроль над процессом разрешения зависимостей с помощью параметра-депенденциверсион в консоли диспетчера пакетов. Параметр позволяет разрешать зависимости от наименьшей возможной версии (поведения по умолчанию), максимально возможной версии или самой высокой версии или исправления.  Этот параметр работает только для Install-Package в команде PowerShell.

![Депенденциверсион, параметр](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Атрибут Депенденциверсион

В дополнение к коммутатору-Депенденциверсион, описанному выше, NuGet также допускал возможность установки нового атрибута в файле NuGet. config, определяющего значение по умолчанию, если параметр-Депенденциверсион не указан при вызове Install-Package. Это значение будет также соблюдаться в диалоговом окне диспетчера пакетов NuGet для всех операций установки пакета. Чтобы задать это значение, добавьте приведенный ниже атрибут в файл NuGet. config:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Предварительный просмотр операций NuGet с помощью-WhatIf

Некоторые пакеты NuGet могут иметь детализированные графы зависимостей, поэтому они могут быть полезны во время операции установки, удаления или обновления, чтобы сначала увидеть, что произойдет. NuGet 2,8 добавляет стандартный параметр PowerShell-WhatIf в команды install-Package, uninstall-package и Update-Package, чтобы обеспечить визуализацию всего замыкания пакетов, к которым будет применена команда. Например, при выполнении `install-package Microsoft.AspNet.WebApi -whatif` в пустом веб-приложении ASP.NET выдается следующее.

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

## <a name="downgrade-package"></a>Переход на более раннюю версию пакета

Установка предварительной версии пакета не является редким вариантом, чтобы исследовать новые возможности, а затем решили выполнить откат до последней стабильной версии. До NuGet 2,8 этот процесс был многошаговым процессом удаления пакета предварительной версии и его зависимостей, а затем установки более ранней версии. Однако в NuGet 2,8 пакет Update-Package теперь будет выполнять откат всего замыкания пакета (например, дерева зависимостей пакета) до предыдущей версии.

## <a name="development-dependencies"></a>Зависимости разработки

В качестве пакетов NuGet могут доставляться различные типы возможностей, включая средства, которые используются для оптимизации процесса разработки. Эти компоненты, хотя они могут быть Instrumental при разработке нового пакета, не должны рассматриваться как зависимость нового пакета при последующей публикации. NuGet 2,8 позволяет пакету идентифицировать себя в файле `.nuspec` как developmentDependency. При установке эти метаданные также будут добавлены в файл `packages.config` проекта, в который был установлен пакет. Когда этот `packages.config`ный файл впоследствии анализируется на зависимости NuGet во время `nuget.exe pack`, он будет исключать эти зависимости, помеченные как зависимости разработки.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Отдельные файлы Packages. config для различных платформ

При разработке приложений для нескольких целевых платформ часто используются разные файлы проекта для каждой из соответствующих сред сборки. Также часто используются разные пакеты NuGet в разных файлах проекта, так как пакеты имеют разные уровни поддержки для разных платформ. NuGet 2,8 обеспечивает улучшенную поддержку этого сценария, создавая различные файлы `packages.config` для различных файлов проекта для конкретной платформы.

![Несколько файлов Package. config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Откат к локальному кэшу

Хотя пакеты NuGet обычно используются из удаленной галереи, такой как [коллекция NuGet](http://www.nuget.org/) , с помощью сетевого подключения, существует множество сценариев, в которых клиент не подключен. Без подключения к сети клиент NuGet не смог успешно установить пакеты, даже если эти пакеты уже были на компьютере клиента в локальном кэше NuGet. NuGet 2,8 добавляет автоматический возврат кэша в консоль диспетчера пакетов. Например, при отключении сетевого адаптера и установке jQuery в консоли отображается следующее:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Функция резервного кэша не требует никаких конкретных аргументов команды. Кроме того, резерв кэша в настоящее время работает только в консоли диспетчера пакетов. в настоящее время поведение не работает в диалоговом окне диспетчера пакетов.

## <a name="webmatrix-nuget-client-updates"></a>Обновления клиента NuGet WebMatrix

Кроме NuGet 2,8, расширение NuGet для WebMatrix также было обновлено для включения многих основных функций, поставляемых с [NuGet 2,5](../release-notes/nuget-2.5.md). К новым возможностям относятся такие возможности, как "обновить все", "минимальная версия NuGet", что позволяет перезаписывать файлы содержимого.

Обновление расширения диспетчера пакетов NuGet в WebMatrix 3:

1. Открыть WebMatrix 3
1. Щелкните значок расширения на ленте.
1. Выберите вкладку обновления.
1. Щелкните, чтобы обновить диспетчер пакетов NuGet до 2.5.0
1. Закрытие и перезапуск WebMatrix 3

Это первый выпуск команды NuGet с расширением диспетчера пакетов NuGet для WebMatrix.  Код недавно был принят корпорацией Майкрософт в проект NuGet с открытым кодом. Ранее интеграция NuGet была встроена в WebMatrix, и ее не удалось обновить с помощью аппаратного контроллера управления WebMatrix.  Теперь у нас есть возможность дальнейшего обновления вместе с остальными клиентскими средствами NuGet.

## <a name="bug-fixes"></a>Исправления ошибок

Одна из основных исправленных ошибок была улучшена в производительности в команде Update-Package-REINSTALL.

В дополнение к этим функциям и упомянутому выше исправлению производительности в этом выпуске NuGet также содержится множество других исправлений ошибок. В выпуске было 181о общих проблем. Полный список рабочих элементов, исправленных в NuGet 2,8, см. в [этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
