---
title: "Заметки о выпуске NuGet 2.0 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 51c7e94f-0084-4c62-bfba-7dfd81675361
description: "Заметки о выпуске для NuGet 2.0, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 2.0 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 41eed1a7c6ad91d63813fb74986aa498765f3dea
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-20-release-notes"></a>Заметки о версии 2.0 NuGet

[Заметки о выпуске NuGet 1.8](../release-notes/nuget-1.8.md) | [заметки о выпуске NuGet 2.1](../release-notes/nuget-2.1.md)

NuGet 2.0 была выпущена 19 июня 2012 г.

## <a name="known-installation-issue"></a>Известные проблемы
Если вы используете VS 2010 с пакетом обновления 1, вы можете столкнуться ошибка установки при попытке обновить NuGet, если у вас установлена более ранняя версия.

Достаточно просто удалить NuGet, а затем установить его из библиотеки расширения VS.  В разделе [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) Дополнительные сведения или [перейдите непосредственно на исправление VS](http://bit.ly/vsixcertfix).

Примечание: Если Visual Studio не позволяют удалить расширение (кнопка удаления отключена), скорее всего, необходимо перезапустить Visual Studio, используя «Запуск от имени администратора».

## <a name="package-restore-consent-is-now-active"></a>Сейчас активен согласия восстановления пакета

Как описано в этом [разместить на согласия восстановления пакета](http://blog.nuget.org/20120518/package-restore-and-consent.html), теперь требуют NuGet 2.0 согласия присваивается включить восстановление пакета, чтобы подключиться к Интернету и загрузки пакетов. Убедитесь, что вы предоставили согласие через диалоговое окно конфигурации диспетчера пакет или переменной среды EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Группы зависимостей путем целевые платформы

Начиная с версии 2.0, пакет может отличаться в зависимости на основе профиле .NET framework целевого проекта. Это достигается с помощью обновленной `.nuspec` схемы. `<dependencies>` Элемент теперь может содержать набор `<group>` элементов. Каждая группа содержит ноль или более `<dependency>` элементы и `targetFramework` атрибута. Все зависимости внутри группы устанавливаются вместе, если требуемая версия .NET framework совместима с профиль целевой платформы проекта. Пример:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

Обратите внимание, что группа может содержать **нуля** зависимости. В приведенном выше примере Если пакет не установлен в проекте, ориентированном на Silverlight 3.0 или более поздней версии, зависимости не будут устанавливаться. Если пакет установлен в проекте, ориентированном на .NET 4.0 или более поздней версии, двумя зависимостями, jQuery и WebActivator, будет установлен.  Если пакет установлен в проекте, ориентированном на ранней версией этих платформ 2 или любой другой платформе, будут устанавливаться RouteMagic 1.1.0. Нет без наследования между группами. Если целевая платформа проекта соответствует `targetFramework` будет установлен атрибут группы, а только зависимости в пределах этой группы.

Пакет можно задать зависимости пакета в двух форматах: старый формат списка `<dependency>` элементов или групп. Если `<group>` используется формат, пакет не установлен в версиях NuGet до версии 2.0.

Обратите внимание, что нельзя совместно использовать два формата. Например, следующий фрагмент кода является **недопустимый** и будут отклонены NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Группирование содержимого файлов и сценариев PowerShell, требуемая версия .NET framework

Помимо ссылки на сборки файлы содержимого и сценариев PowerShell можно также группировать по требуемой версии .NET framework. Найти структуру папок в `lib` папку для указания целевой платформы теперь можно применять таким же образом, чтобы `content` и `tools` папки. Пример:

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**Примечание**: поскольку `init.ps1` выполняется на уровне решения и является не зависят от любого отдельного проекта, он должен быть помещен непосредственно под `tools` папки. Если поместить в папку отдельной платформы, он будет игнорироваться.

Кроме того, новая функция в NuGet 2.0 — возможность, папки платформы *пустой*, в этом случае NuGet будет не добавлять ссылки на сборки, файлы содержимого или запускать скрипты PowerShell для версии конкретной платформы. В примере выше папки `content\net40` пуст.

## <a name="improved-tab-completion-performance"></a>Улучшенная вкладку завершения производительности
Функция завершения tab в консоли диспетчера пакетов NuGet теперь значительно повысить производительность. Будет гораздо меньше задержка между временем нажатии клавиши tab, пока не появится раскрывающийся список предложений.

## <a name="bug-fixes"></a>Исправления ошибок
NuGet 2.0 включает множество исправлений ошибок с акцентом на пакет восстановления согласия и производительности.
Полный список рабочих элементов исправления в NuGet 2.0 представление [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).