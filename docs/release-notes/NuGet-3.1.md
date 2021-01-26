---
title: Заметки о выпуске NuGet 3,1
description: Заметки о выпуске NuGet 3,1, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776536"
---
# <a name="nuget-31-release-notes"></a>Заметки о выпуске NuGet 3,1

[Заметки о](../release-notes/nuget-3.0.0.md)  |  выпуске NuGet 3,0 [Заметки о выпуске 3.1.1 NuGet](../release-notes/nuget-3.1.1.md)

Пакет NuGet 3,1 был выпущен 27 июля 2015 в качестве упакованного расширения для пакета SDK универсальная платформа Windows для Visual Studio 2015. Мы доставили этот выпуск с помощью пакета SDK для платформы Windows, чтобы опыт разработки Windows мог воспользоваться преимуществами межплатформенных операций NuGet, которые были ранее запущены. Эта версия расширения NuGet доступна только для Visual Studio 2015.

Рекомендуется, чтобы разработчики, у которых есть доступ к коллекции Visual Studio, могли перейти к последней доступной версии, так как мы всегда публикуем обновления с исправлениями ошибок и новыми функциями.

## <a name="nuget-visual-studio-extension"></a>Расширение NuGet для Visual Studio

Проблемы и функции в этом выпуске помечаются на сайте GitHub на этапе "промежуточная [Поддержка версии UWP в 3,1 RTM"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  . Мы закрыли 67 в выпуске 3,1.

### <a name="new-features"></a>Новые возможности

* `project.json` Поддержка Windows UWP и поддержки ASP.NET 5
* Установка транзитивных пакетов

Описание и определение этих функций можно найти в другой части документации.

### <a name="deprecated"></a>Не рекомендуется

Следующие функции больше не доступны для Visual Studio 2015:

* Пакеты уровня решения больше не могут быть установлены

Следующие функции больше не доступны для Visual Studio 2015 и проектов, использующих `project.json` спецификацию.

* `install.ps1` и `uninstall.ps1` — эти скрипты будут игнорироваться во время установки, восстановления, обновления и удаления пакета
* Преобразования конфигурации будут пропущены
* Содержимое будет перенесено, но не скопировано в проект.
    * Рабочая группа работает над повторной реализацией этой функции, следуйте обсуждению и прогрессу в: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Известные проблемы

В этом выпуске было доставлено несколько известных проблем.

* Установка выпуска 3,1 с пакетом SDK для Windows 10 приведет к понижению версии установленного ранее расширения NuGet.

## <a name="nuget-command-line"></a>Командная строка NuGet

Исполняемый файл командной строки NuGet был обновлен и перемещен в новое распространяемое расположение, чтобы предыдущие версии nuget.exe могли стать доступными.  Бета-версию 3,1 nuget.exe для Windows можно скачать по адресу: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Новое распространяемое расположение находится на узле dist.nuget.org со структурой папок, следующей за этим шаблоном:

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>Новые возможности

* nuget.exe может восстанавливать и устанавливать пакеты в проекты, использующие `project.json` файл.
* nuget.exe можете подключиться к протоколу NuGet v3 и использовать его по адресу: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Известные проблемы ##

1.    Невозможно выполнить пакет для `project.json` файла — [928](https://github.com/NuGet/Home/issues/928)
2.    Не поддерживается на Mono- [1059](https://github.com/NuGet/Home/issues/1059)
3.    Не локализовано — [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)
4.    Не подписан, как и существующий http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
