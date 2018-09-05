---
title: Заметки о выпуске версии 1.3 NuGet
description: Заметки о выпуске для NuGet 1.3, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551355"
---
# <a name="nuget-13-release-notes"></a>Заметки о выпуске версии 1.3 NuGet

[Заметки о выпуске NuGet 1.2](../release-notes/nuget-1.2.md) | [заметки о выпуске NuGet 1.4](../release-notes/nuget-1.4.md)

25 апреля 2011 г. был выпущен NuGet 1.3.

## <a name="new-features"></a>Новые функции

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Упрощенное создание пакета с помощью интеграции сервера символов

Команда NuGet привлечена ребята из [SymbolSource.org](http://www.symbolsource.org/) предложить очень простой способ публикации источников и PDB-файла, а также пакет. Это позволяет клиентам выполнять шаги с заходом источник для пакета в отладчике пакета. Дополнительные сведения см. в статье [Создание и публикация пакета символов](../create-packages/symbol-packages.md) простой способ публикации пакетов NuGet с источниками. Вы также можете посмотреть проведена Демонстрация эту функцию как часть NuGet подробно поговорим в Mix11. Эта функция является полностью показан с отметки времени знак 20-минутное видео.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Команда

Эта команда позволяет легко получить доступ к странице проекта для обновления в консоли диспетчера пакетов. Он также предоставляет параметры, чтобы открыть URL-адрес лицензии и страницы отчета о нарушении для пакета.
Используется следующий синтаксис команды:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru` Параметр используется для возврата значения из указанного URL-адрес.

Примеры

    PM> Open-PackagePage Ninject

Открывает в браузере URL-адрес проекта, указанный в пакете Ninject.

    PM> Open-PackagePage Ninject -License

Открывает в браузере URL-адрес лицензии, указанный в пакете Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Открывает в браузере URL-адрес в текущем источнике пакета, используемый для сообщения о нарушении для указанного пакета.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Назначает URL-адрес лицензии переменной $url, не открывая URL-адрес в браузере.

### <a name="performance-improvements"></a>Улучшения производительности

NuGet 1.3 вызывает массу повышение производительности. NuGet 1.3 позволяет избежать загрузки несколько раз ту же версию пакета, включая кэш локального пользователя. Кэш может быть доступно и очищены с помощью диалогового окна Параметры диспетчера пакетов:

![Диалоговое окно параметров NuGet с параметрами кэша пакета](./media/nuget-options.png)

Другие улучшения производительности включают добавление поддержки HTTP-сжатие и повышение скорости установки пакета в среде Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio и nuget.exe использует тот же список источников пакетов

До 1.3 NuGet список источников пакетов, используемых nuget.exe и NuGet Visual Studio надстройки не были сохранены в одном месте. NuGet 1.3 теперь использует тот же список в обоих местах. Список хранится в `NuGet.Config` и сохраняется в папку AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe не обрабатывает файлы и папки, начинающиеся с "." по умолчанию

Чтобы сделать NuGet работы с системами управления версиями, такие Subversion и Mercurial, nuget.exe игнорирует папки и файлы, которые начинаются с "." символов при создании пакетов. Это может быть переопределено с помощью двух новые флаги:

* __-NoDefaultExcludes__ позволяет переопределить этот параметр и включение всех файлов.
* __-Исключение__ используется для добавления других файлов и папок, чтобы исключить с помощью шаблона. Например, чтобы исключить все файлы с расширением файла '.bak'

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Примечание: шаблон не является рекурсивным по умолчанию._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Поддержка проекты WiX и управлением .NET Micro Framework

Благодаря предложения участников сообщества NuGet включает в себя поддержку для типов проектов WiX, а также .NET Micro Framework.

## <a name="bug-fixes"></a>Исправления ошибок

Полный список исправлений ошибок, просмотр [Issue Tracker NuGet для этого выпуска](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Исправления ошибок, следует отметить

* Пакеты с исходными файлами работать в обоих веб-сайтов и проектов веб-приложений.
Для веб-сайтов, исходные файлы копируются в `App_Code` папки
