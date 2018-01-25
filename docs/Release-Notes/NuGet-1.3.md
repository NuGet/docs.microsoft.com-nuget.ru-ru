---
title: "Заметки о выпуске NuGet 1.3 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 1.3, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 1.3 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-13-release-notes"></a>Заметки о выпуске 1,3 NuGet

[Заметки о выпуске NuGet 1.2](../release-notes/nuget-1.2.md) | [заметки о выпуске NuGet 1.4](../release-notes/nuget-1.4.md)

NuGet 1.3 был выпущен 25 апреля 2011 г.

## <a name="new-features"></a>Новые функции

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Упрощенное создание пакета с помощью интеграции сервера символов

Команды NuGet, сотрудничающих с ребятами [SymbolSource.org](http://www.symbolsource.org/) предоставляет очень простой способ публикации источников и PDB-файла вместе с вашего пакета. Это позволяет клиентам пакета шаг с заходом в исходный для пакета в отладчике. Дополнительные сведения см. в статье [создания и публикации пакета символов](../create-packages/symbol-packages.md) легко публиковать пакеты NuGet с источниками. Также можно просматривать динамическую демонстрацию этой функции как часть NuGet в глубину обращения во Mix11. Эта функция полностью демонстрируется начиная с 20-минутное знаком видео.

### <a name="open-packagepage-command"></a>`Open-PackagePage`Команда

Эта команда позволяет легко перейти на страницу проекта для пакета из консоли диспетчера пакетов. Он также предоставляет параметры, чтобы открыть URL-адрес лицензии и о нарушении страницы отчета для пакета.
Ниже приведен синтаксис для команды.

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru` Параметр используется для возврата значения из указанного URL-адреса.

Примеры

    PM> Open-PackagePage Ninject

Открывает в браузере URL-адрес проекта, указанный в пакете Ninject.

    PM> Open-PackagePage Ninject -License

Открывает в браузере URL-адрес лицензии, указанный в пакете Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Открывает в браузере URL-адрес текущего источника пакетов, используемый для сообщения о нарушении для указанного пакета.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Назначает URL-адрес лицензии переменной $url, не открывая его в браузере.

### <a name="performance-improvements"></a>Улучшения производительности

NuGet 1.3 предоставляет много улучшений производительности. NuGet 1.3 позволяет избежать загрузки несколько раз одну и ту же версию пакета, включая кэш локального пользователя. Кэш может осуществлять доступ к очищен через диалоговое окно параметров диспетчера пакетов:

![Диалоговое окно параметров NuGet с параметрами кэша пакета](./media/nuget-options.png)

Другие усовершенствования производительности включают добавление поддержка сжатия HTTP и повышение скорости установки пакета в среде Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio и nuget.exe использует тот же список источников пакетов

До NuGet 1.3 список источников пакетов, используемых nuget.exe NuGet Visual Studio надстройка и не были сохранены в том же месте. NuGet 1.3 теперь использует тот же список в обоих местах. Список хранится в `NuGet.Config` и помещен в папку AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe не учитывает файлы и папки, которые начинаются с "." по умолчанию

Для упрощения работы с системами управления версиями, таких как Subversion и Mercurial NuGet, nuget.exe не учитывает папки и файлы, которые начинаются с "." символов при создании пакетов. Это может быть переопределено с помощью двух новых флаги:

* __-NoDefaultExcludes__ используется для переопределения этого параметра и включает все файлы.
* __-Исключить__ используется для добавления других файлов и папок для исключения с помощью шаблона. Например, чтобы исключить все файлы с расширением '.bak'

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Примечание: шаблон не является рекурсивным по умолчанию._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Поддержка проектов WiX и Micro .NET Framework

Благодаря материалы сообщества NuGet включает поддержку WiX типы проектов, а также Micro .NET Framework.

## <a name="bug-fixes"></a>Исправления ошибок

Полный список исправлений ошибок, просмотреть [NuGet отслеживания проблем в этом выпуске](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Исправления следует отметить

* Пакеты с исходными файлами работать в двух веб-сайтов и проектов веб-приложений.
Для веб-сайтов, исходные файлы копируются в `App_Code` папки
