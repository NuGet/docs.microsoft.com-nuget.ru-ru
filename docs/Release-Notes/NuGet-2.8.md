---
title: "Заметки о выпуске NuGet 2.8 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 77ba98d8-3d66-4126-b2b6-813ddd8ef192
description: "Заметки о выпуске для NuGet 2.8, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.8 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0bb35e9d6ef6f3dde7919cd502b32ba5a550c689
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-28-release-notes"></a>Заметки о выпуске 2,8 NuGet

[Заметки о выпуске NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 заметки о выпуске](../release-notes/nuget-2.8.1.md)

NuGet 2.8 был выпущен 29 января 2014 г.

## <a name="acknowledgements"></a>Благодарности

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) — когда упаковки пакеты, проверка идентификатор зависимостей пакетов.
1. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -удалить суффикс $metadata при persistening учетные данные веб-канала.
1. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - поддержки, указав файл проекта для команды update nuget.exe.
1. [Гонзалес Хуана](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -замены токенов не передан с - IncludeReferencedProjects.
1. [Дэвид Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -Устранение nuget.push генерации OutOfMemoryException при принудительной установке большой пакет.
1. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -исправление неправильный целевой путь, если проект ссылается на другой проект CLI/C++.
1. [Ральф Адам](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -пакетов в качестве зависимости разработки по умолчанию
1. [Дэвид Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -удалить неявные обновления до последней версии исправления
1. [Грегори Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Некоторые ошибки, исправления и улучшения NuGet.Server, команда зеркало nuget.exe и др.
    - Эта работа выполнялась через несколько месяцев с помощью Грегори совместную работу над правой синхронизации для интеграции в основной 2.8.

## <a name="patch-resolution-for-dependencies"></a>Исправление для разрешения для зависимостей

При разрешении зависимостей пакета, NuGet Исторически реализации стратегии выбора самую раннюю версию основной и дополнительный пакет, который удовлетворяет зависимости для пакета. В отличие от основной и вспомогательной версии Однако обновления версия всегда разрешения самую новую версию. Хотя поведение было намерениями, он будет создан отсутствие детерминизм для установки пакетов с зависимостями. Рассмотрим следующий пример.

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

В этом примере, даже если Developer1 Developer2 установки и PackageA@1.0.0, каждый завершена вверх с другой версией PackageB. NuGet 2.8 изменяет это поведение по умолчанию, таким образом, что поведение разрешения зависимостей для обновления версий не согласуется с поведением для основной и дополнительный номер версии. В приведенном выше примере, затем PackageB@1.0.0 будет устанавливаться в результате установки PackageA@1.0.0независимо от того, новая версия исправления.

## <a name="-dependencyversion-switch"></a>-DependencyVersion коммутатор

Хотя изменение NuGet 2.8 _по умолчанию_ поведения при разрешении зависимостей, он также добавляет более точно контролировать процесс разрешения зависимостей через коммутатор - DependencyVersion в консоли диспетчера пакетов. Параметр включает разрешение зависимостей наименьший возможный номер версии (по умолчанию), максимально возможный номер версии, или высоким вспомогательные или версии обновления.  Этот параметр работает только для установки пакета в команду powershell.

![Коммутатор DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Атрибут DependencyVersion

В дополнение к коммутатору - DependencyVersion, рассмотренных в выше NuGet также можно использовать для обеспечения возможности, чтобы задать новый атрибут в файле Nuget.Config определение что такое значение по умолчанию, если не указан параметр - DependencyVersion при вызове пакет установки. Это значение также учитываются в диалоговом окне диспетчера пакетов NuGet для выполнения любых операций пакета установки. Чтобы задать это значение, добавьте атрибут ниже в файл Nuget.Config.

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Просмотр операций NuGet - whatif

Некоторые пакеты NuGet может иметь графами глубокой зависимости, и таким образом, он может быть полезным при установке, удаление или операции сначала узнать, что произойдет. NuGet 2.8 добавляет стандартный коммутатор PowerShell - whatif пакет установки, удаления пакета и пакета обновления команды, чтобы включить визуализация всего закрытия пакетов, к которым применяется команда. Например, на котором работают `install-package Microsoft.AspNet.WebApi -whatif` в пустой веб-узел ASP.NET, приложение возвращает следующее.

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

Довольно часто, чтобы установить предварительную версию пакета, чтобы изучить новые функции, а затем выберите для отката до последней стабильной версии. До NuGet 2.8 это не многоэтапный процесс, при удалении предварительной пакет и его зависимости и затем установить более ранней версии. С помощью NuGet 2.8 тем не менее, пакет обновления будет теперь откат всего пакета закрытия (например дерево зависимостей пакета) к предыдущей версии.

## <a name="development-dependencies"></a>Зависимости разработки

Много различных возможностей могут доставляться в виде пакетов NuGet - включая средств, используемых для оптимизации процесса разработки. Эти компоненты могут быть инструментального при разработке нового пакета, не следует считать опубликованные зависимостей нового пакета, если он является более поздней версии. NuGet 2.8 позволяет пакету для идентификации себя в `.nuspec` файл в качестве элемента developmentDependency. При установке, эти метаданные также будут добавляться в `packages.config` файла проекта, в которую был установлен пакет. Когда, `packages.config` файл позже проанализировать для зависимостей NuGet во время `nuget.exe pack`, исключает эти зависимости пометку разработки зависимости.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Packages.config отдельных файлов для различных платформ

При разработке приложений для нескольких целевых платформ, часто используются файлы другого проекта для каждой из сред соответствующие сборки. Рекомендуется также использовать разные пакеты NuGet в файлы другого проекта как пакеты имеют различные уровни поддержки для разных платформ. NuGet 2.8 обеспечивает улучшенную поддержку для этого сценария, создавая другой `packages.config` файлов для файлов различных проекта под конкретную платформу.

![Несколько файлов package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Переход к локального кэша

Хотя пакеты NuGet обычно используются такие как с помощью удаленного коллекции [галереи NuGet](http://www.nuget.org/) использования сетевого подключения, существует множество сценариев, где клиент не подключен. Без подключения к сети клиент NuGet не удается успешно установить пакеты - даже в том случае, если эти пакеты уже есть на компьютере клиента в локальном кэше NuGet. Консоль диспетчера пакетов NuGet 2.8 добавляет автоматического кэша резервной. Например, при отключении сетевого адаптера и установки jQuery, консоли содержит следующую информацию:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Компонент резервного кэша не требуют аргументов конкретной команды. Кроме того резервный кэша в настоящее время работает только в консоли диспетчера пакетов - поведение не работает в данный момент в диалоговом окне диспетчера пакетов.

## <a name="webmatrix-nuget-client-updates"></a>Обновляет WebMatrix клиента NuGet

Вместе с NuGet 2.8 расширение NuGet для WebMatrix также был изменен для включения многие функциональные возможности, присутствующие в [NuGet 2.5](../release-notes/nuget-2.5.md). Новые возможности относятся, например «Обновить все», «Минимальная версия NuGet» и поддержка перезапись файлов содержимого.

Чтобы обновить расширение диспетчера пакетов NuGet в WebMatrix 3:

1. Откройте WebMatrix 3
1. Щелкните значок «расширения» на ленте
1. Выберите вкладку "обновления"
1. Щелкните, чтобы обновить диспетчер пакетов NuGet для 2.5.0
1. Закройте и перезапустите WebMatrix 3

Это первый выпуск NuGet team расширения диспетчера пакетов NuGet для WebMatrix.  Код недавно отправили корпорацией Майкрософт в проект NuGet открытым исходным кодом. Ранее интеграции NuGet была построена в WebMatrix, и его не удалось обновить аппаратного из WebMatrix.  Теперь у нас есть возможность последующего обновления его вместе с остальной части NuGet клиентских средств.

## <a name="bug-fixes"></a>Исправления ошибок

Одной из основных исправления внесены было улучшение производительности в пакете обновления-переустановить команды.

Помимо этих возможностей и исправления упомянутой выше производительности этот выпуск NuGet также включает много исправлений ошибок. Произошли 181 общее проблемы, описанные в выпуске. Полный список рабочих элементов исправления в NuGet 2.8 представление [NuGet отслеживания проблем в этом выпуске](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
