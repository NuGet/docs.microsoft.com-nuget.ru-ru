---
title: "Заметки о выпуске NuGet 3.1 | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Заметки о выпуске для NuGet 3.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 3.1 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a7aa43b8701b3bbef8f6ebce9a5d636ee1bc6abe
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-31-release-notes"></a>Заметки о выпуске 3.1 NuGet

[Заметки о выпуске NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 заметки о выпуске](../release-notes/nuget-3.1.1.md)

NuGet 3.1 был выпущен 27 июля 2015 г. как расширение распространение для универсальных Windows Platform SDK для Visual Studio 2015. Мы доставлено этой версии с Windows Platform SDK, чтобы процесс разработки Windows может использовать преимущества работы кросс платформенных NuGet, которая ранее была запущена. Эта версия расширения NuGet доступна только для Visual Studio 2015.

Мы рекомендуем разработчиков, которые имеют доступ к коллекции Visual Studio обновление до последней версии, которая доступна, как мы всегда выполняется публикация обновлений с помощью исправления и новые функции.

## <a name="nuget-visual-studio-extension"></a>Расширение NuGet Visual Studio

Проблемы и функций в этом выпуске помечены в GitHub с [вехи «3.1 RTM UWP транзитивное поддержки»](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) всего, мы закрытых 67 проблем в версии 3.1.

### <a name="new-features"></a>Новые функции

* `project.json`Поддержка для поддержки Windows UWP и ASP.NET 5
* Транзитивное пакета установки

Описание и определение этих возможностей можно найти в другом месте в документации.

### <a name="deprecated"></a>Рекомендуется использовать

Для Visual Studio 2015 больше недоступны следующие функции:

* Больше нельзя устанавливать пакеты уровня решения

Следующие функции недоступны для Visual Studio 2015 и проектов, использующих `project.json` спецификации

* `install.ps1`и `uninstall.ps1` -эти сценарии будут пропущены во время установки пакета, восстановление, обновление и удаление
* Конфигурация преобразования будет игнорироваться.
* Содержимое будет выполнена, но не копируется в проект.
    * Повторно реализовать эту функцию, обсуждения и инструкциями хода выполнения, в которой работает команда: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Известные проблемы

Обнаружены несколько известных проблем, присутствующие в этом выпуске.

* 3.1 выпуска с помощью пакета SDK Windows 10 будет произведено изменение настроек любой версии расширение NuGet, который был ранее установлен

## <a name="nuget-command-line"></a>NuGet командной строки

Исполняемый файл командной строки NuGet была обновлена и перемещен в новое расположение распространяемый, что исторические версии nuget.exe продолжения должны быть доступны.  Вы можете скачать 3.1 бета-версии nuget.exe для Windows, посетите: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Новое расположение распространяемый находится на узле dist.nuget.org со структурой папок, соответствует этому шаблону.

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Новые функции

* можно восстановить и установить пакеты в проекты, использующие NuGet.exe `project.json` файл.
* можно подключиться и использовать протокол v3 NuGet на NuGet.exe: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Известные проблемы ##

1.    Не удается выполнить пакет с `project.json` файл - [928](https://github.com/NuGet/Home/issues/928)
2.    Не поддерживается в моно - [1059](https://github.com/NuGet/Home/issues/1059)
3.    Не локализован - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Не имеет подписи, так же, как существующие http://nuget.org/nuget.exe - [бинарная](https://github.com/NuGet/Home/issues/1073)
