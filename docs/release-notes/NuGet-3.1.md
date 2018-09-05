---
title: Заметки о выпуске 3.1 NuGet
description: Заметки о выпуске для NuGet 3.1, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545351"
---
# <a name="nuget-31-release-notes"></a>Заметки о выпуске 3.1 NuGet

[Заметки о выпуске NuGet 3.0](../release-notes/nuget-3.0.0.md) | [заметки о выпуске NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

NuGet 3.1 была выпущена 27 июля 2015 г. как расширение распространение для пакета SDK универсальной платформы Windows для Visual Studio 2015. Таким образом, чтобы процесс разработки для Windows можно использовать преимущество работы кросс платформенных NuGet, которая была запущена ранее доставлен этот выпуск с пакетом SDK для платформы Windows. Эта версия расширения NuGet доступна только для Visual Studio 2015.

Мы рекомендуем тех разработчиков, имеющих доступ к коллекции Visual Studio с обновлением до последней версии, доступен, как всегда, мы публикуем обновления, исправления ошибок и новые функции.

## <a name="nuget-visual-studio-extension"></a>Расширение NuGet Visual Studio

Проблемы и функции в этом выпуске помечены на сайте GitHub с [вехи «3.1 RTM UWP транзитивное поддержки»](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) в целом, мы закрытых 67 проблем в версии 3.1.

### <a name="new-features"></a>Новые функции

* `project.json` поддерживает использование Windows UWP и ASP.NET 5
* Транзитивное пакета установки

Описания и определения этих функций можно найти в другом месте в документации.

### <a name="deprecated"></a>Устарело

Для Visual Studio 2015 больше не доступны следующие возможности:

* Больше нельзя устанавливать пакеты уровня решения

Следующие функции больше не доступны для Visual Studio 2015 и проекты, использующие `project.json` спецификации

* `install.ps1` и `uninstall.ps1` -эти сценарии будут игнорироваться во время установки пакета, восстановление, обновления и удаления
* Преобразования конфигурации будут пропущены
* Содержимое будут перенесены, но не копируется в проект.
    * Повторно реализовать эту функцию, следите за обсуждениями и выполняться работает команда: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Известные проблемы

Обнаружены несколько известных проблем, присутствующие в этом выпуске.

* Установки 3.1 версии с помощью пакета SDK для Windows 10 будет понизить любая версия расширения NuGet, который ранее был установлен

## <a name="nuget-command-line"></a>Командной строки NuGet

Исполняемый файл командной строки NuGet была обновлена и перемещен в новое расположение распространяемый таким образом, чтобы старые версии nuget.exe по-прежнему будут доступны.  3.1 бета-версии nuget.exe можно загрузить для Windows в: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Новое расположение распространяемый находится на dist.nuget.org хост-компьютере и структуру папок, которая следует за этот шаблон:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Новые функции

* NuGet.exe можно восстановить и установки пакетов в проекты, использующие `project.json` файл.
* NuGet.exe может подключиться к и использовать протокол v3 NuGet на: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Известные проблемы ##

1.    Не удается выполнить пакет с `project.json` файл — [928](https://github.com/NuGet/Home/issues/928)
2.    Не поддерживается в Mono — [1059](https://github.com/NuGet/Home/issues/1059)
3.    Не локализован - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Не имеет подписи, так же, как существующий http://nuget.org/nuget.exe  -  [бинарная](https://github.com/NuGet/Home/issues/1073)
