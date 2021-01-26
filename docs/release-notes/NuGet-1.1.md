---
title: Заметки о выпуске NuGet 1,0 и 1,1
description: Заметки о выпуске NuGet 1,1, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdd4bad54b08d956dbfdaf54220971492fd3ab02
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777207"
---
# <a name="nuget-10-and-11-release-notes"></a>Заметки о выпуске NuGet 1,0 и 1,1

[Заметки о выпуске NuGet 1,2](../release-notes/nuget-1.2.md)

Версия NuGet 1,0 была выпущена 13 января 2011 г.  Версия NuGet 1,1 была выпущена 12 февраля 2011 г.

## <a name="overview"></a>Обзор

Этот документ содержит заметки о выпуске для различных выпусков NuGet 1,0, сгруппированных в соответствии с основной предварительной версией.

NuGet включает следующие компоненты:

* *NuGet. Tools. VSIX* *, который состоит из:
  * Диалоговое окно **добавления пакета библиотеки** * в Visual Studio, используемое для просмотра и установки пакетов.
  * **Консоль диспетчера пакетов** * консоль на основе PowerShell в Visual Studio.
* Средство *командной строки NuGet* *, используемое для создания пакетов (и, наконец, публикации).

Для расширения "инструменты NuGet" Visual Studio (*NuGet. Tools. VSIX*) требуется:

* Visual Studio 2010 или Visual Web Developer 2010 Express.

Программа командной строки NuGet требует:

* Платформа .NET Framework версии 4

## <a name="installation"></a>Установка

Чтобы использовать этот [последний выпуск](http://nuget.codeplex.com/releases/view/52018), выполните следующие действия.

* Сначала удалите старую сборку. Для этого необходимо запустить VS от имени администратора.
* Удалите все существующие веб-каналы.
* Добавьте новый веб-канал, указывающий на <https://go.microsoft.com/fwlink/?LinkId=206669> .

## <a name="nuget-11"></a>NuGet 1.1

Список проблем, исправленных в этом выпуске, [можно найти здесь](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0) .

## <a name="nuget-10-rtm"></a>NuGet 1,0 RTM

Одна из проблем была исправлена для RTM с версии-КАНДИДАТа.

* [Проблема 474: удаление пакетов затрагивает все проекты в решении](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Версия-кандидат

Ниже приведены изменения, внесенные в этот выпуск-кандидат с момента выпуска CTP-версии 2. Чтобы просмотреть полный список ошибок, посетите средство записи проблем.

* [Обновление пакета из консоли не обновляет зависимости.](http://nuget.codeplex.com/workitem/443)
* [Добавление пакета — не ссылка на пакет (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Обновление пакета оставляет неработающие ссылки](http://nuget.codeplex.com/workitem/440)
* [В диалоговом окне не удается выполнить обновления Get-Package или при выборе в консоли статистического источника "все"](http://nuget.codeplex.com/workitem/439)
* [Получение ошибок проверки пакета](http://nuget.codeplex.com/workitem/426)
* [Предупреждать пользователей, если пакет не может быть установлен из диалогового окна "Добавление пакета"](http://nuget.codeplex.com/workitem/425)
* [При обновлении большого количества пакетов возникает исключение Get-Package-Updates](http://nuget.codeplex.com/workitem/424)
* [Улучшение обработки ошибок при неправильном создании файлов nuspec](http://nuget.codeplex.com/workitem/423)
* [Пакет NuGet игнорирует указанные файлы](http://nuget.codeplex.com/workitem/422)
* [Удаление источника второго и последнего пакетов, а затем нажатие кнопки "Переместить вниз"](http://nuget.codeplex.com/workitem/418)
* [Удалить ссылку на сборку во время установки пакетов](http://nuget.codeplex.com/workitem/413)
* [Исключение InvalidOperationException при открытии диалогового окна параметров](http://nuget.codeplex.com/workitem/411)
* [Ключ доступа для источника пакета в консоли диспетчера пакетов не работает](http://nuget.codeplex.com/workitem/410)
* [Ключи доступа диалогового окна параметров NuGet VS позволяют сосредоточиться на неверных полях](http://nuget.codeplex.com/workitem/409)
* [КОД пакета IntelliSense не должен запрашивать слишком много элементов](http://nuget.codeplex.com/workitem/404)
* [Сбой добавления пакета в проект с символом точки в имени проекта](http://nuget.codeplex.com/workitem/403)
* [Проблемы с указанными файлами в nuspec](http://nuget.codeplex.com/workitem/400)
* [Правильный официальный веб-канал должен быть зарегистрирован при использовании более новой сборки](http://nuget.codeplex.com/workitem/399)
* [Теги должны использовать пробелы вместо #](http://nuget.codeplex.com/workitem/397)
* [В Ипаккажеметадата отсутствуют некоторые полезные сведения](http://nuget.codeplex.com/workitem/388)
* [Добавить ссылку "сообщить о нарушении" в диалоговое окно](http://nuget.codeplex.com/workitem/386)
* [Использование App_Data для распаковки разрывов пакетов в Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Реализация тегов](http://nuget.codeplex.com/workitem/376)
* [Паккажебуилдер допускает создание пустого пакета без зависимостей](http://nuget.codeplex.com/workitem/373)
* [Добавление поля "владельцы" для пакета](http://nuget.codeplex.com/workitem/365)
* [Обновите манифест VSIX, чтобы он указывал диспетчер пакетов NuGet, а не средства VSIX.](http://nuget.codeplex.com/workitem/364)
* [Команда Get-Package вызывает ошибку при выборе всех источников](http://nuget.codeplex.com/workitem/359)
* [Разрешить упорядочивание источников пакетов в диалоговом окне "Параметры"](http://nuget.codeplex.com/workitem/356)
* [Обновление-пакет не удаляет старую версию](http://nuget.codeplex.com/workitem/352)
* [Реализация спецификации диапазона версий для зависимостей](http://nuget.codeplex.com/workitem/347)
* [Visual Studio аварийно завершает работу при нажатии кнопки "добавить новый пакет"](http://nuget.codeplex.com/workitem/346)
* [Отображение загрузок и оценок в диалоговом окне "Добавление пакета"](http://nuget.codeplex.com/workitem/345)
* [Изменение между источниками пакетов в диалоговом окне не приводит к обновлению активного источника](http://nuget.codeplex.com/workitem/344)
* [Удалить привязку клавиш для окна консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/339)
* [Install-Package не распознан как имя командлета...](http://nuget.codeplex.com/workitem/338)
* [Установка пакета из локального канала не удается разрешить зависимости от обычных каналов](http://nuget.codeplex.com/workitem/332)
* [РемоведепенденЦиес должны пропускать зависимости, которые еще используются](http://nuget.codeplex.com/workitem/331)
* [При отмене навигации по страницам пользователь не может перейти на другую страницу при возврате исходного запроса страницы](http://nuget.codeplex.com/workitem/325)
* [Изучите производительность Нупакк. Server для обслуживания каналов с большим количеством пакетов.](http://nuget.codeplex.com/workitem/324)
* [Второй раз при фильтрации пакета используется источник пакета «New», а не ранее выбранный источник.](http://nuget.codeplex.com/workitem/321)
* [При выборе вкладки "в сети" в диалоговом окне следует выбрать источник пакетов по умолчанию.](http://nuget.codeplex.com/workitem/320)
* [List-Package должен показывать установленные пакеты по умолчанию](http://nuget.codeplex.com/workitem/309)
* [Ссылка на сборку Хинтпасс](http://nuget.codeplex.com/workitem/294)
* [Исключение при открытии консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/268)
* [Консоль IntelliSense загружает весь веб-канал](http://nuget.codeplex.com/workitem/259)
* [Источник пакета по умолчанию должен быть переименован в "Active"](http://nuget.codeplex.com/workitem/258)
* [Пользовательский интерфейс источников пакетов: нажмите кнопку "ОК", чтобы добавить новый источник, если поля имени и источника не являются пустыми](http://nuget.codeplex.com/workitem/257)
* [При большом количестве установленных пакетов диалоговое окно становится очень медленным](http://nuget.codeplex.com/workitem/243)
* [Поддержка переадресации привязок для сборок со строгими именами](http://nuget.codeplex.com/workitem/238)
* [Добавить ссылку на пакет... Пользовательский интерфейс для включения раскрывающегося списка для источника пакета](http://nuget.codeplex.com/workitem/226)
* [Нупакк должен поддерживать преобразование конфигурации независимо от имени файла конфигурации](http://nuget.codeplex.com/workitem/224)
* [Позволяет переопределить BasePath в NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Резервное поведение источника пакета](http://nuget.codeplex.com/workitem/204)
* [Сбой на графическом интерфейсе](http://nuget.codeplex.com/workitem/201)
* [Добавление параметров сортировки в диалоговое окно добавления пакета](http://nuget.codeplex.com/workitem/179)
* [сочетание клавиш для очистки консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/174)
* [Поверконсоле приводит к сбою консоли Нупакк](http://nuget.codeplex.com/workitem/166)
* [Диалоговое окно "консоль и Добавление пакета" должно устанавливать агент пользователя в запросах](http://nuget.codeplex.com/workitem/141)
* [Задайте номер версии VSIX и NuPack.exe в сборке.](http://nuget.codeplex.com/workitem/134)
* [Скрыть общие параметры PowerShell от-?](http://nuget.codeplex.com/workitem/118)
* [Справка по дополнительным сведениям для команд консоли](http://nuget.codeplex.com/workitem/110)
* [Диалоговое окно добавления пакета должно позволять выбрать текущий источник пакета](http://nuget.codeplex.com/workitem/88)
* [Перемещение классов Нупакк. Core в разные пространства имен](http://nuget.codeplex.com/workitem/50)
* [Добавление справки в командлеты](http://nuget.codeplex.com/workitem/23)
* [Проверка хэша из веб-канала после скачивания пакета](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

Ниже приведены наиболее существенные изменения, внесенные в CTP-версию 2.

* Переключение канала пакета из ATOM в конечную точку службы OData. при обновлении до версии CTP2 пакета NuGet обязательно добавьте следующий URL-адрес в качестве источника пакетов: `https://feed.nuget.org/ctp2/odata/v1/` .
* Переименована команда Add-Package в *Install-Package*.
* Обновлен `.nuspec` Формат. `.nuspec`Теперь формат содержит поле *иконурл* для задания значка размером 32x32 PNG, который будет отображаться в диалоговом окне Добавление пакета. Поэтому не забудьте установить это значение для различения пакета. Этот `.nuspec` формат также содержит новое поле *прожектурл* , которое можно использовать для указания на веб-страницу, в которой содержатся дополнительные сведения о пакете.

Эта сборка не будет работать со старыми `.nupkg` файлами. Если вы получаете исключения со ссылкой NULL, вы используете старый `.nupkg` файл, и вам нужно перестроить его с помощью обновленного [средства командной строки NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Ниже приведен список компонентов и ошибок, исправленных для NuGet CTP 2 (не включающих ошибки для незначительных очисток кода и т. д.).

* [Ошибка при распаковке сборок пакета при указании TargetFramework для сборки.](http://nuget.codeplex.com/workitem/10)
* [Сделать окно консоли Нупакк более обнаруживаемым](http://nuget.codeplex.com/workitem/14)
* [ILMerge выпуск nupack.exe](http://nuget.codeplex.com/workitem/19)
* [Улучшенная обработка ошибок и исключений](http://nuget.codeplex.com/workitem/24)
* [[Нупакк. Core]: PackageManager должен корректно обработать ошибки, связанные с веб-каналом](http://nuget.codeplex.com/workitem/28)
* [Нужен новый значок для консоли](http://nuget.codeplex.com/workitem/29)
* [Локализация строк в диалоговом окне](http://nuget.codeplex.com/workitem/38)
* [Кэш Нупакк скачанных файлов. нупакк в памяти](http://nuget.codeplex.com/workitem/40)
* [Консоль Нупакк: изменение ярлыка по умолчанию для отображения консоли](http://nuget.codeplex.com/workitem/48)
* [Прожектсистем должен поддерживать значения по умолчанию для общих свойств](http://nuget.codeplex.com/workitem/49)
* [Запуск nupack.exe в папке с одним файлом nuspec должен использовать этот nuspec](http://nuget.codeplex.com/workitem/52)
* [Меню "проект" отображается даже в том случае, если проект или решение не загружены](http://nuget.codeplex.com/workitem/54)
* [Сбой Build. cmd на чистом клоне базы кода](http://nuget.codeplex.com/workitem/56)
* [Доступные обновления](http://nuget.codeplex.com/workitem/57)
* [Диалоговое окно. при добавлении пакета с помощью диалогового окна удаляется запрос в консоли.](http://nuget.codeplex.com/workitem/73)
* [Добавление пакета путем нажатия кнопки "установить" часто является очень высокой скоростью, без визуальной обратной связи](http://nuget.codeplex.com/workitem/80)
* [Невозможно обнаружить, какие из установленных пакетов имеют обновления.](http://nuget.codeplex.com/workitem/82)
* [Невозможно обновить установленный пакет в диалоговом окне.](http://nuget.codeplex.com/workitem/83)
* [Невозможно удалить установленный пакет в диалоговом окне](http://nuget.codeplex.com/workitem/84)
* [&ldquo;&hellip; &rdquo; В контекстном меню установленных ссылок появится ссылка Добавить пакет.](http://nuget.codeplex.com/workitem/85)
* [После обновления пакета из консоли отображается как старая версия, так и новая версия как установленная.](http://nuget.codeplex.com/workitem/86)
* [Действие в консоли при использовании диалогового окна исчезает после использования](http://nuget.codeplex.com/workitem/87)
* [Очистка синтаксического анализа командной строки в nupack.exe](http://nuget.codeplex.com/workitem/89)
* [Добавление понятного имени в источники пакетов](http://nuget.codeplex.com/workitem/98)
* [Обновление. nuspec для поддержки, включая значки пакетов](http://nuget.codeplex.com/workitem/103)
* [Пользовательский интерфейс веб-канала не допускает копирование URL](http://nuget.codeplex.com/workitem/105)
* [Улучшенная обработка ошибок при удалении пакетов.](http://nuget.codeplex.com/workitem/107)
* [Ввод в окне консоли зависит от фокуса курсора](http://nuget.codeplex.com/workitem/112)
* [Сообщения об ошибках выглядят как ужасные](http://nuget.codeplex.com/workitem/116)
* [Неправильное производительность Remove-Package пакета, который не установлен.](http://nuget.codeplex.com/workitem/117)
* [Удаление пакета завершается ошибкой, если нет источников пакетов](http://nuget.codeplex.com/workitem/119)
* [Remove-Package завершается сбоем, если источник пакета недоступен](http://nuget.codeplex.com/workitem/120)
* [Добавьте заголовок в метаданные пакета и веб-канал.](http://nuget.codeplex.com/workitem/125)
* [Добавьте параметр-Source обратно в Add-Package.](http://nuget.codeplex.com/workitem/127)
* [List-Package должен иметь параметр-source](http://nuget.codeplex.com/workitem/128)
* [Обновление Нупакк. Server, чтобы требовать от агента пользователя Нупакк загрузить пакет](http://nuget.codeplex.com/workitem/142)
* [В диалоговом окне принятия условий лицензии должны быть перечислены лицензии для всех зависимостей, требующих принятия.](http://nuget.codeplex.com/workitem/145)
* [Регистрировать ошибку при порождении пакета в веб-канале](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe не должен разрешать пустой &lt; &gt; элемент licenseurl](http://nuget.codeplex.com/workitem/152)
* [Переименование List-Package в Get-Package, Add-Package в Install-Package и Remove-Package для удаления пакета](http://nuget.codeplex.com/workitem/155)
* [Использование пункта меню "добавить ссылку на пакет" из навигатора по решению аварийно завершает работу Visual Studio](http://nuget.codeplex.com/workitem/158)
* [В метке "доступные источники пакетов" отсутствует двоеточие](http://nuget.codeplex.com/workitem/160)
* [Сделать. nuspec XML-элемента с учетом регистра всегда в стиле прописных букв](http://nuget.codeplex.com/workitem/161)
* [Манифест VSIX Нупакк должен включить бит "admin"](http://nuget.codeplex.com/workitem/162)
* [При запуске List-Package без каналов выдается ошибка ref null.](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: укажите конечный путь](http://nuget.codeplex.com/workitem/171)
* [Ошибки PowerShell при открытии консоли Управление пакетами в WinXP](http://nuget.codeplex.com/workitem/175)
* [VS Crashs при попытке загрузить список пакетов](http://nuget.codeplex.com/workitem/176)
* [разрешить мета-пакеты (нет файлов, только зависимости)](http://nuget.codeplex.com/workitem/180)
* [Преобразование скрипта PowerShell в модуль PowerShell 2,0](http://nuget.codeplex.com/workitem/181)
* [Пасресолвер должен удалить часть пути, предшествующую символу-шаблону, если указан целевой объект](http://nuget.codeplex.com/workitem/183)
* [Не содержит зависимостей](http://nuget.codeplex.com/workitem/186)
* [Ошибка при установке ELMAH](http://nuget.codeplex.com/workitem/192)
* [Преобразования конфигурации неправильно работают с &lt; configSections&gt;](http://nuget.codeplex.com/workitem/194)
* [Не удается получить переменную "$global:p Рожекткаче", так как она не была задана](http://nuget.codeplex.com/workitem/203)
* [Добавление задачи MSBuild для создания пакетов Нупакк](http://nuget.codeplex.com/workitem/205)
* [List-Package требуется поддержка поиска и фильтрации](http://nuget.codeplex.com/workitem/206)
* [Всегда отображать ссылку на лицензию, если автор пакета предоставляет URL-адрес лицензии](http://nuget.codeplex.com/workitem/208)
* [Случайное исключение "доступ запрещен" с помощью Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Сбой модульных тестов: Инвалидпаккажеисексклудедфромфидитемс &amp; креатингфидконвертспаккажестоатоментриес](http://nuget.codeplex.com/workitem/214)
* [Разрешить использовать резервный набор файлов и список по умолчанию, если не удается найти версию указанной Framework](http://nuget.codeplex.com/workitem/223)
* [Добавить ссылку на пакет... Пользовательский интерфейс не может удалить пакет](http://nuget.codeplex.com/workitem/225)
* [Добавить ссылку на пакет crashs Studio при выгрузке одного или нескольких проектов](http://nuget.codeplex.com/workitem/228)
* [Преобразование конфигурации не работает в web.debug.config файле](http://nuget.codeplex.com/workitem/229)
* [init.ps1 не срабатывает для пользовательского пакета](http://nuget.codeplex.com/workitem/237)
* [При добавлении путей к фидлист кнопке по умолчанию присваивается значение ОК, поэтому при нажатии клавиши ввод автоматически закрывается](http://nuget.codeplex.com/workitem/240)
* [Попытка удалить зависимость будет завершаться сбоем VS при попытке 2 раз в строке](http://nuget.codeplex.com/workitem/241)
* [Отображение URL-адреса проекта в диалоговом окне добавления пакета](http://nuget.codeplex.com/workitem/253)
* [Диалоговое окно Add-Package по умолчанию для установленных пакетов](http://nuget.codeplex.com/workitem/254)
* [Изменить элемент меню диалогового окна "добавить пакет".](http://nuget.codeplex.com/workitem/261)
* [Переименование пространств имен и сборок](http://nuget.codeplex.com/workitem/274)
* [Переименование проекта Нупакк в NuGet](http://nuget.codeplex.com/workitem/282)
* [Добавьте следующий текст в список зависимостей.](http://nuget.codeplex.com/workitem/288)
* [Изменение текста для принятия условий лицензии в диалоговом окне принятия условий лицензии](http://nuget.codeplex.com/workitem/291)
* [Измените текст в диалоговом окне принятия условий лицензии над списком пакетов.](http://nuget.codeplex.com/workitem/292)
* [OData не работает с URL-адресом fwlink](http://nuget.codeplex.com/workitem/304)
* [Пользовательский интерфейс диспетчера пакетов: чрезмерно агрессивное кэширование количества пакетов, используемого для разбиения на страницы](http://nuget.codeplex.com/workitem/317)
* [Нупакк/NuGet- &gt; ошибка консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/335)
* [Диалоговое окно "Добавление пакета" показывает принятие условий лицензии для уже установленного пакета](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Ниже приведен список компонентов и ошибок, исправленных для NuGet CTP 1.

* [Расширение пакета должно быть переименовано в. нупакк](http://nuget.codeplex.com/workitem/1)
* [Переместить файл пакета в папку](http://nuget.codeplex.com/workitem/2)
* [Слияние установки &amp; Add PS Commands](http://nuget.codeplex.com/workitem/3)
* [Создание псевдонимов для командлетов Verb-Noun](http://nuget.codeplex.com/workitem/4)
* [Нупакк переключается при переключении решения в VS](http://nuget.codeplex.com/workitem/6)
* [По умолчанию следует скрыть папку решения "Packages"](http://nuget.codeplex.com/workitem/11)
* [Добавлена поддержка замены токенов в элементах содержимого.](http://nuget.codeplex.com/workitem/12)
* [Нупакк. UI должен использовать API PackageSource](http://nuget.codeplex.com/workitem/26)
* [[Нупакк. Core]: PackageManager помечает пакеты как установленные перед их установкой](http://nuget.codeplex.com/workitem/27)
* [При удалении проекта по умолчанию из решения по умолчанию будет отображаться удаленный проект](http://nuget.codeplex.com/workitem/30)
* [Новый пакет завершается с ошибкой "не удается добавить часть для указанного URI, так как он уже находится в пакете".](http://nuget.codeplex.com/workitem/32)
* [Удаление строк "Нупакк" из графического пользовательского интерфейса Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Добавление заголовка Apache в файл COPYRIGHT.txt](http://nuget.codeplex.com/workitem/36)
* [Команда удаления Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Диспетчер пакетов непригоден для использования при загрузке профиля вызывает исключение](http://nuget.codeplex.com/workitem/39)
* [init.ps1, install.ps1 и uninstall.ps1 должны получить дополнительное состояние](http://nuget.codeplex.com/workitem/41)
* [Объединение пакетов консоли и графического пользовательского интерфейса в один пакет](http://nuget.codeplex.com/workitem/42)
* [Логика преобразования XML не работает, если применяется к XML, который не находится в корне](http://nuget.codeplex.com/workitem/43)
* [Диалоговое окно "Управление параметрами источников пакетов" не обновляет консоль Нупакк](http://nuget.codeplex.com/workitem/44)
* [Пользовательский интерфейс консоли Нупакк: переименование "веб-канала пакета" в "источник пакета"](http://nuget.codeplex.com/workitem/45)
* [Параметры консоли Нупакк: переименование "пользовательского интерфейса репозитория" для согласования с консолью Нупакк](http://nuget.codeplex.com/workitem/46)
* [Сбой добавления пакета для веб-сайта, открытого из IIS или URL-адреса](http://nuget.codeplex.com/workitem/53)
* [Источник диспетчера пакетов не работает с FwLink](http://nuget.codeplex.com/workitem/55)
* [Задание источника пакетов по умолчанию](http://nuget.codeplex.com/workitem/59)
* [При добавлении источников пакетов в параметре, если указан только один источник, предположим, что это значение по умолчанию.](http://nuget.codeplex.com/workitem/60)
* [В пользовательском интерфейсе диалогового окна отображаются фиктивные «последние» пакеты](http://nuget.codeplex.com/workitem/62)
* [Параметры: нажатие кнопки Отмена не отменяет изменения](http://nuget.codeplex.com/workitem/63)
* [При поиске диалогового окна "Добавление ссылки на пакет" не учитывается регистр](http://nuget.codeplex.com/workitem/65)
* [Исправление метаданных компании в файлах AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Номер версии для VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: using-? Отображает справку дважды](http://nuget.codeplex.com/workitem/72)
* [Выполнение пакетов установки и удаления для пакетов уровня проекта](http://nuget.codeplex.com/workitem/74)
* [Серверу не удалось создать веб-канал, когда один нупакк не прошел проверку](http://nuget.codeplex.com/workitem/90)
* [Необходимо заменить значки Нупакк](http://nuget.codeplex.com/workitem/94)
* [Прокси-сервер NTLM HTTP не проходит проверку подлинности в веб-канале пакета.](http://nuget.codeplex.com/workitem/96)
* [Диалоговое окно не всегда запускается в центре окна VS](http://nuget.codeplex.com/workitem/100)
* [Многие поля в сведениях о пакетах не заполняются в диалоговом окне](http://nuget.codeplex.com/workitem/102)
* [В пользовательском интерфейсе диалогового окна не отображаются имена авторов](http://nuget.codeplex.com/workitem/108)
* [Почему-Version для Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Удаление вкладки "последние" в пользовательском интерфейсе диалогового окна](http://nuget.codeplex.com/workitem/115)
* [VS Crash, если щелкнуть папку решения правой кнопкой мыши после открытия пользовательского интерфейса диалогового окна по крайней мере одного.](http://nuget.codeplex.com/workitem/126)
* [Измените параметр-local List-Package на-installed.](http://nuget.codeplex.com/workitem/129)
* [Переименование packages.xml в NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Консоль принудительно устанавливает курсор на конец строки](http://nuget.codeplex.com/workitem/135)
* [Функция Remove-Package IntelliSense не работает](http://nuget.codeplex.com/workitem/136)
* [Добавление флага RequireLicenseAcceptance в nuspec и веб-канал](http://nuget.codeplex.com/workitem/137)
* [Добавление LicenseUrl в формат nuspec и веб-канал пакета](http://nuget.codeplex.com/workitem/138)
* [Щелкните установить для пакета, для которого требуется принятие согласия, чтобы отобразить диалоговое окно принятия.](http://nuget.codeplex.com/workitem/139)
* [Добавление текста заявления об отказе в диалоговое окно добавления пакета](http://nuget.codeplex.com/workitem/140)
* [Добавить заявление об отказе при первом запуске консоли пакета](http://nuget.codeplex.com/workitem/143)
* [Отображать заявление об отказе после установки пакета в консоли](http://nuget.codeplex.com/workitem/144)
* [Переименуйте расширение. нупакк на. nupkg](http://nuget.codeplex.com/workitem/146)