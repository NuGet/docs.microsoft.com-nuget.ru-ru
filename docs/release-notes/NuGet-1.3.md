---
title: Заметки о выпуске NuGet 1,3
description: Заметки о выпуске NuGet 1,3, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825259"
---
# <a name="nuget-13-release-notes"></a>Заметки о выпуске NuGet 1,3

[Заметки о выпуске nuget 1,2](../release-notes/nuget-1.2.md) | [заметок о выпуске NuGet 1,4](../release-notes/nuget-1.4.md)

Версия NuGet 1,3 была выпущена 25 апреля 2011.

## <a name="new-features"></a>Новые функции

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Упрощенное создание пакетов с помощью интеграции с сервером символов

Группа NuGet, которая взаимодействует с сотрудниками в [SymbolSource.org](http://www.symbolsource.org/) , предлагает простой способ публикации источников и PDB вместе с пакетом. Это позволяет пользователям пакета выполнять шаг с заходом в исходный код для пакета в отладчике. Дополнительные сведения см. в статье [Создание и Публикация пакета символов](../create-packages/symbol-packages.md) с помощью простого способа публикации пакетов NuGet с источниками. Вы также можете просмотреть динамическую демонстрацию этой функции в составе NuGet, подробно обсудим по адресу Mix11. Эта функция полностью демонстрируется, начиная с 20-минутной метки видео.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Command

Эта команда позволяет легко перейти на страницу проекта пакета из консоли диспетчера пакетов. Он также предоставляет параметры для открытия URL-адреса лицензии и страницы «сообщение о нарушении» для пакета.
Синтаксис команды:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

Параметр `-PassThru` используется для получения значения указанного URL-адреса.

Примеры:

    PM> Open-PackagePage Ninject

Открывает браузер по URL-адресу проекта, указанному в пакете Нинжект.

    PM> Open-PackagePage Ninject -License

Открывает браузер с URL-адресом лицензии, указанным в пакете Нинжект.

    PM> Open-PackagePage Ninject -ReportAbuse

Открывает браузер по URL-адресу в текущем источнике пакета, который используется для сообщения о нарушении для указанного пакета.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Присваивает переменной URL-адрес лицензии $url, не открывая URL-адрес в браузере.

### <a name="performance-improvements"></a>Повышение производительности

NuGet 1,3 вносит значительные улучшения в производительность. NuGet 1,3 не позволяет загружать одну и ту же версию пакета несколько раз, включая локальный кэш для каждого пользователя. Доступ к кэшу можно получить и очистить с помощью диалогового окна "Параметры диспетчера пакетов":

![Диалоговое окно параметров NuGet с параметрами кэша пакетов](./media/nuget-options.png)

К другим улучшениям производительности относятся добавление поддержки сжатия HTTP и повышение скорости установки пакета в Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>В Visual Studio и NuGet. exe используется тот же список источников пакетов.

До NuGet 1,3 список источников пакетов, используемых NuGet. exe и надстройкой NuGet для Visual Studio, не хранился в одном месте. NuGet 1,3 теперь использует один и тот же список в обоих местах. Список хранится в `NuGet.Config` и хранится в папке AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet. exe игнорирует файлы и папки, которые начинаются с "." по умолчанию

Чтобы NuGet хорошо работала с системами управления версиями, такими как Subversion и Mercurial, NuGet. exe игнорирует папки и файлы, которые начинаются с символа "." при создании пакетов. Это можно переопределить с помощью двух новых флагов:

* __-Нодефаултексклудес__ используется для переопределения этого параметра и включения всех файлов.
* __-Exclude__ используется для добавления других файлов или папок, исключаемых с помощью шаблона. Например, чтобы исключить все файлы с расширением BAK

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Примечание. по умолчанию шаблон не является рекурсивным._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Поддержка проектов WiX и .NET Micro Framework

Благодаря вкладам сообщества NuGet обеспечивает поддержку типов проектов WiX, а также .NET Micro Framework.

## <a name="bug-fixes"></a>Исправления ошибок

Полный список исправлений ошибок см. в [этой версии средства регистрации проблем NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Исправлены ошибки, которые следует отметить

* Пакеты с исходными файлами работают как на веб-сайтах, так и в проектах веб-приложений.
Исходные файлы для веб-сайтов копируются в папку `App_Code`
