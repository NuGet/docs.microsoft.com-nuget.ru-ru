---
title: Заметки о выпуске версии-Кандидата NuGet 3.2
description: Заметки о выпуске для RC NuGet 3.2, включая известные проблемы, исправленные ошибки, добавленные функции и DCR.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0310bac6fdb3ef92176f9224ace1620a230664af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-32-rc-release-notes"></a>Заметки о выпуске версии-Кандидата NuGet 3.2

[Заметки о выпуске NuGet 3.1.1](../release-notes/nuget-3.1.1.md) | [NuGet 3.2 заметки о выпуске](../release-notes/nuget-3.2.md)

Выпущено NuGet 3.2 версии-кандидата 2 сентября 2015 г. как коллекция усовершенствований и исправлений для 3.1.1 выпуска.  Кроме того это первый выпуски, сначала опубликованные на новое хранилище dist.nuget.org.

## <a name="new-features"></a>Новые функции

* Проекты, которые находятся в той же папке, теперь могут иметь разные `project.json` файлы в этой папке, относящиеся к каждому проекту.  Для каждого проекта имя `project.json` файл `{ProjectName}.project.json` и NuGet правильно будет ссылаться и использовать содержимое для каждого проекта, соответствующим образом.  Это поддерживает новую функцию [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` Теперь поддерживает параметр globalPackagesFolder, как относительный путь — [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Обновления командной строки

Это первая версия nuget.exe клиента, который поддерживает серверы NuGet v3 и восстановление пакетов для проектов управляемого с `project.json` файла.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>Обнаружены несколько прошедших проверку подлинности веб-канала проблемы, которые были в этом выпуске для улучшения взаимодействия с клиентом.

* Установить / восстановления взаимодействий подавать только учетные данные для начального запроса, прошедшего проверку подлинности веб-канала - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Команда Push не разрешить учетные данные из конфигурации - [1248](https://github.com/NuGet/Home/issues/1248)
* Заголовки и агент пользователя теперь отправленные в репозитории NuGet, чтобы помочь при отслеживании статистики - [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Мы внесли ряд улучшений, чтобы лучше обрабатывать сбои в сети при попытке удаленного репозитория NuGet:

* Улучшенные сообщения об ошибках, если не удается подключиться к удаленной веб-каналы - [1238](https://github.com/NuGet/Home/issues/1238)
* Исправлено команды restore NuGet правильно возвращать 1, если ошибка возникает - [1186](https://github.com/NuGet/Home/issues/1186)
* Теперь Повтор сетевые подключения каждые 200 мс, не более 5 попыток в случае ошибки HTTP 5xx - [1120](https://github.com/NuGet/Home/issues/1120)
* Улучшенную обработку ответов сервера перенаправления при выполнении команды push - [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` Теперь поддерживает URL-адрес или репозитория имя из Nuget.Config в качестве аргумента - [1046](https://github.com/NuGet/Home/issues/1046)
* Отсутствующие пакеты, которые не были найдены в репозитории, во время восстановления теперь помечаются как ошибки вместо предупреждения [1038](https://github.com/NuGet/Home/issues/1038)
* Исправлена обработка multipartwebrequest \r\n для Unix/Linux сценариев - [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Существует ряд исправлений к проблемам различные команды.

* Команда Push больше не делает GET перед PUT в источнике пакета - [1237](https://github.com/NuGet/Home/issues/1237)
* Команда list больше не повторяется номера версий - [1185](https://github.com/NuGet/Home/issues/1185)
* Пакет с аргументом - сборки теперь правильно поддерживает C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Исправленные проблемы, попытка упаковать проекта F #, созданного с помощью Visual Studio 2015 — [1048](https://github.com/NuGet/Home/issues/1048)
* Если пакеты уже существует - восстановить сейчас нет ops [1040](https://github.com/NuGet/Home/issues/1040)
* Улучшенная ошибки сообщения, когда `packages.config` файл имеет неправильный формат - [1034](https://github.com/NuGet/Home/issues/1034)
* Исправлено команды restore с `-SolutionDirectory` коммутатора для работы с относительными путями - [992](https://github.com/NuGet/Home/issues/992)
* Улучшенная команда обновлено для поддержки обновления решения - [924](https://github.com/NuGet/Home/issues/924)

Полный список проблем, в этом выпуске можно найти в NuGet GitHub [командной строки вехи](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Обновление расширений Visual Studio

### <a name="new-features-in-visual-studio"></a>Новые возможности в Visual Studio

* Был добавлен новый пункт контекстного меню в обозревателе решений в узле решений и позволяющая пакетов для восстановления без построения решения ([1274](https://github.com/NuGet/Home/issues/1274)).

![Новый «Восстановить пакеты» пункт контекстного меню](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Обновления и исправления в Visual Studio

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Исправления для прошедших проверку подлинности веб-каналы были свертки и описываются в расширении, а также.  Параметры проверки подлинности также были модернизированы в расширении:

* Правильно обработке NuGet v3 прошедшие проверку подлинности веб-каналы правильно, а не v2 проверки подлинности веб-каналы - [1216](https://github.com/NuGet/Home/issues/1216)
* Исправленный запрашивает учетные данные проверки подлинности в проектах с помощью `project.json` и обмена данными с веб-каналы v2 - [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>Сетевое подключение затрагиваются пользовательский интерфейс в Visual Studio, и мы исправили с следующие исправления:

* Улучшенное обслуживание локального кэша версии пакетов - [тезисы:](https://github.com/NuGet/Home/issues/1096)
* Изменить поведение сбоя при подключении к версии 3, веб-канал больше не попытка считать канал v2 - [1253](https://github.com/NuGet/Home/issues/1253)
* Теперь позволяют установить сбои при установке пакета с несколькими источниками пакета - [1183](https://github.com/NuGet/Home/issues/1183)

Мы улучшенную обработку взаимодействий с операции построения:

* Теперь продолжением для построения проектов, если восстановление пакетов для отдельного проекта завершается ошибкой - [1169](https://github.com/NuGet/Home/issues/1169)
* Установка пакета в проект, который зависит другим проектом в решении вызывает повторное построение решения - [981](https://github.com/NuGet/Home/issues/981)
* Исправлено устанавливает при неудачном выполнении пакета, чтобы правильно откат изменений в проект - [1265](https://github.com/NuGet/Home/issues/1265)
* Исправлено непреднамеренного удаления `developmentDependency` атрибут пакета в `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Вызовы `install.ps1` теперь имеют собственное `$package.AssemblyReferences` объекта, переданного - [1245](https://github.com/NuGet/Home/issues/1245)
* Больше не препятствует удаляет пакетов в проектах UWP, когда проект находится в неисправном состоянии - [1128](https://github.com/NuGet/Home/issues/1128)
* Решения, содержащие сочетание `packages.config` и `project.json` проекты теперь правильно построены без необходимости второй операции - сборки [1122](https://github.com/NuGet/Home/issues/1122)
* Правильно найти файлы app.config, если они связаны или находится в другой папке - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* Проекты UWP, теперь можно установить, отсутствующие в списке пакетов - [1109](https://github.com/NuGet/Home/issues/1109)
* Восстановление пакета теперь разрешено пока решение не находится в сохраненном состоянии - [1081](https://github.com/NuGet/Home/issues/1081)


Обработка обновлений, чтобы исправить файлы конфигурации:

* Удаление целевой файл больше не доставлено из пакета на последующих сборках `project.json` управляемый проект - [1288](https://github.com/NuGet/Home/issues/1288)
* Больше не изменение Nuget.Config файлов во время построения решения ASP.NET 5 - [1201](https://github.com/NuGet/Home/issues/1201)
* Изменение больше не допускается ограничение версий, во время обновления пакета - [1130](https://github.com/NuGet/Home/issues/1130)
* Блокировка файлов теперь остаются заблокированными во время сборки - [1127](https://github.com/NuGet/Home/issues/1127)
* Изменение `packages.config` и не переписывая его во время обновления - [585](https://github.com/NuGet/Home/issues/585)


Улучшение взаимодействия с системой управления версиями TFS:

* Больше не произошел сбой установки для пакетов, которые привязаны к TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* Исправленный NuGet пользовательский интерфейс для интеграции TFS 2013 — Разрешить [1071](https://github.com/NuGet/Home/issues/1071)
* Исправлены ссылки на пакеты восстановлена правильно происходят из папки пакетов - [1004](https://github.com/NuGet/Home/issues/1004)

Наконец мы также улучшены следующие элементы:

* Уменьшить уровень детализации сообщений журнала для `project.json` управляемых проектов - [1163](https://github.com/NuGet/Home/issues/1163)
* Теперь правильно отображение установленная версия пакета в пользовательском интерфейсе - [1061](https://github.com/NuGet/Home/issues/1061)


Полный список устраненные для расширения Visual Studio можно найти в NuGet GitHub [3,2 вехи](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Известные проблемы

Мы продолжаем отслеживания проблем на наш список проблем GitHub, которую можно найти в: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)