---
title: Заметки о выпуске версии NuGet 4.6 RTM
description: Заметки о выпуске для NuGet 4.6.0, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: 3c71d05144aa2b92b916d4ebf319c5a4e321581f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549848"
---
# <a name="nuget-46-rtm-release-notes"></a>Заметки о выпуске версии NuGet 4.6 RTM

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает в себя [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Сводка. Новые возможности этого выпуска

* Добавлена поддержка для [подписывания пакетов](../create-packages/sign-a-package.md).
* Теперь Visual Studio 2017 и nuget.exe проверяют целостность пакетов перед установкой, восстанавливая пакеты для [подписанных пакетов](../reference/signed-packages-reference.md).
* Улучшена производительность последовательных восстановлений.

## <a name="known-issues"></a>Известные проблемы

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Проблемы с .NET Standard 2.0, связанные с .NET Framework и NuGet 

Платформа .NET Standard и ее инструментарий были разработаны таким образом, чтобы проекты, предназначенные для .NET Framework 4.6.1, могли использовать пакеты NuGet и проекты, предназначенные для .NET Standard 2.0 или более ранних версий. [В этом документе](https://github.com/dotnet/standard/issues/481) кратко описаны проблемы, связанные с таким сценарием, план их решения, а также обходные пути, которые можно применить в текущем состоянии.

## <a name="top-issues-fixed-in-this-release"></a>Основные ошибки, исправленные в этом выпуске

**Исправления производительности**

* Файлы ресурсов не записываются при отсутствии изменений — [№ 6491](https://github.com/NuGet/Home/issues/6491)
* Восстановление приводит к лишним оценкам MSBuild, когда TFM дочерних проектов не совпадают с TFM родительского проекта — [№ 6311](https://github.com/NuGet/Home/issues/6311)
* Улучшена производительности восстановления NoOp за счет оптимизации характеристик для создания графа зависимостей — [№ 6252](https://github.com/NuGet/Home/issues/6252)

**Ошибки**

* Отправка в локальную папку оставляет NUPKG заблокированным — [№ 6325](https://github.com/NuGet/Home/issues/6325)
* Реализация подключаемого модуля NuGet: несколько проблем — [№ 6149](https://github.com/NuGet/Home/issues/6149)
* UIHang — удаление вызова службы запросов из инициализации MEF в VSSolutionManager — [№ 6110](https://github.com/NuGet/Home/issues/6110)
* Исключение отчетов об ошибках для отмененной задачи скачивания пакета — [№ 6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe заменяет "+" на "%2B" в имени сборки — [№ 5956](https://github.com/NuGet/Home/issues/5956)
* Сочетание клавиш FN+F1 не открывает подходящую страницу справки для консоли и пользовательского интерфейса диспетчера пакетов — [№ 5912](https://github.com/NuGet/Home/issues/5912)
* При определенных условиях VS NuGet записывает абсолютные пути в файлы проекта — [№ 5888](https://github.com/NuGet/Home/issues/5888)
* Исправление регрессии 4.3 — заполнители $product$ и $AssemblyGuid$ не заменяются в файле содержимого при преобразовании — [№ 5880](https://github.com/NuGet/Home/issues/5880)
* Команда dotnet restore с несколькими источниками завершается сбоем — [№ 5817](https://github.com/NuGet/Home/issues/5817)
* Пакет должен повторно оценить версии проекта, чтобы разрешить управление версиями Git — [№ 4790](https://github.com/NuGet/Home/issues/4790)
* Исправление трудных для понимания ошибок при установке несовместимого пакета — [№ 4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard нужен параметр, чтобы установить пакеты как PackageReferences — [№ 4549](https://github.com/NuGet/Home/issues/4549)
* Предоставленные пакетом файлы свойств не учитываются при запуске MSBuild.exe извне Командной строки разработчика — [№ 4530](https://github.com/NuGet/Home/issues/4530)
* Исправление некорректного сообщения об ошибке при ссылке на неприменимую к проекту библиотеку .NET Standard — [№ 4423](https://github.com/NuGet/Home/issues/4423)
* Команда dotnet add package завершается со сбоем для пакета, ориентированного на переносимый профиль, а сведения об этом отсутствуют — [№ 4349](https://github.com/NuGet/Home/issues/4349)
* Отсутствует суффикс версии dotnet pack в ProjectReference — [№ 4337](https://github.com/NuGet/Home/issues/4337)
* Ошибки сборки и аварийное завершение VS пи использовании шаблона .NET Core — [№ 3973](https://github.com/NuGet/Home/issues/3973)
* Не удается загрузить индекс службы для исходного HTTPS:* — [№ 3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe list -allversions не работает — [№ 3441](https://github.com/NuGet/Home/issues/3441)
* Вводящее в заблуждение сообщение об ошибке разрешения зависимости — [№ 2984](https://github.com/NuGet/Home/issues/2984)
* Команда nuget.exe restore не создает файлы PROPS и TARGETS для MSBUILDPROJ (регрессия в обновлении версии 3.3.0–3.4.4) — [№ 2921](https://github.com/NuGet/Home/issues/2921)
* Задержка в пользовательском интерфейсе при обновлении пакета NuGet при открытом файле XAML — [№ 2878](https://github.com/NuGet/Home/issues/2878)
* Проект веб-сайта из IIS завершается сбоем с недопустимыми символами в пути — [№ 2798](https://github.com/NuGet/Home/issues/2798)
* Команда Nuget add приводит к зависанию CentOS — [№ 2708](https://github.com/NuGet/Home/issues/2708)
* Восстановление с использованием packagesavemode -nupkg завершается сбоем для json.net — [№ 2706](https://github.com/NuGet/Home/issues/2706)
* Фильтр диспетчера пакетов недоступен в окне выходных данных Visual Studio для команды restore — [№ 2704](https://github.com/NuGet/Home/issues/2704)

[Список всех ошибок, исправленных в этом выпуске](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
