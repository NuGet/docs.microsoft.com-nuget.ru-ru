---
title: Заметки о выпуске NuGet 1.0 и 1.1
description: Заметки о выпуске для NuGet 1.1, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547025"
---
# <a name="nuget-10-and-11-release-notes"></a>Заметки о выпуске NuGet 1.0 и 1.1

[Заметки о выпуске для NuGet 1.2 выпуска](../release-notes/nuget-1.2.md)

NuGet 1.0 была выпущена 13 января 2011 г.  NuGet 1.1 была выпущена 12 февраля 2011 г.

## <a name="overview"></a>Обзор

Этот документ содержит заметки о выпуске для различных версий NuGet 1.0, сгруппированных в соответствии с основной предварительной версии.

NuGet включает в себя следующие компоненты:

* *NuGet.Tools.vsix* * которого состоит из:
  * **Добавить диалоговое окно библиотеки пакета** * диалоговое окно в Visual Studio, используемый для просмотра и установки пакетов.
  * **Консоль диспетчера пакетов** * консоли в среде Visual Studio на основе Powershell.
* *Средство командной строки NuGet* * средство используется для создания (и последующей публикации) пакеты.

Расширение NuGet средства Visual Studio (*NuGet.Tools.vsix*) требуется:

* Visual Studio 2010 или Visual Web Developer 2010 Express.

Требуется средство командной строки NuGet:

* Версии платформы .NET framework 4

## <a name="installation"></a>Установка

Чтобы использовать это [последний выпуск](http://nuget.codeplex.com/releases/view/52018):

* Сначала удалите старые сборки. Необходимо запустить VS от имени администратора, чтобы сделать это.
* Удалите все существующие веб-каналы, на которые у вас есть.
* Добавить новый канал, который указывает на [ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

Список проблем, исправленных в этом выпуске [можно найти здесь](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Одна проблема была исправлена для RTM-версии, начиная с версии RC.

* [Проблема 474: Удаление пакетов затрагивает все проекты в решении](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Версия-кандидат

Ниже приведены изменения, внесенные в этой версии-кандидате после CTP-версия 2. Посетите отслеживание вопросов, чтобы просмотреть полный список ошибок.

* [Обновление пакета из консоли не обновляет зависимости.](http://nuget.codeplex.com/workitem/443)
* [Добавление пакета воспринимает bin не упаковывает ссылки (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Обновление пакета оставляет неработающих ссылок](http://nuget.codeplex.com/workitem/440)
* [Get-Package-обновлений произошел сбой, в диалоговом окне, или при выборе источником «Все» в консоли](http://nuget.codeplex.com/workitem/439)
* [Получение ошибок проверки пакетов](http://nuget.codeplex.com/workitem/426)
* [Предупреждать пользователей, если пакет не может быть установлен в диалоговом окне Добавление пакета](http://nuget.codeplex.com/workitem/425)
* [Get-Package-обновляет вызывает исключение при обновлении большого числа пакетов](http://nuget.codeplex.com/workitem/424)
* [Улучшения в обработке ошибок при nuspec-файлы разрабатываются неправильно](http://nuget.codeplex.com/workitem/423)
* [Пакет NuGet игнорирует указанные файлы](http://nuget.codeplex.com/workitem/422)
* [Удаление источника второй с конца пакета и выбрав команду «Переместить вниз» происходит сбой VS](http://nuget.codeplex.com/workitem/418)
* [Удалить ссылку на сборку во время установки пакетов](http://nuget.codeplex.com/workitem/413)
* [InvalidOperationException при открытии диалогового окна параметров](http://nuget.codeplex.com/workitem/411)
* [Ключ доступа для источника пакета в консоли диспетчера пакетов не работает](http://nuget.codeplex.com/workitem/410)
* [Ключи доступа диалоговое окно настройки NuGet VS перевести фокус в тех полей](http://nuget.codeplex.com/workitem/409)
* [Intellisense идентификатор пакета не должны запрашивать это слишком много элементов](http://nuget.codeplex.com/workitem/404)
* [Ошибка добавления пакета в проект с помощью символа точки в имени проекта](http://nuget.codeplex.com/workitem/403)
* [Проблема с указанные файлы в nuspec](http://nuget.codeplex.com/workitem/400)
* [Правильный официальный веб-канала должен получить зарегистрирован, при использовании новой сборки](http://nuget.codeplex.com/workitem/399)
* [Теги следует использовать пробелы вместо #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata отсутствуют некоторые полезные сведения](http://nuget.codeplex.com/workitem/388)
* [Добавьте ссылку на отчет о нарушении в диалоговое окно](http://nuget.codeplex.com/workitem/386)
* [С помощью App_Data, чтобы распаковать разрывы пакетов в Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Реализации тегов](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder позволяет пустой пакет без зависимостей, должен быть создан](http://nuget.codeplex.com/workitem/373)
* [Добавление поля владельцев для пакета](http://nuget.codeplex.com/workitem/365)
* [Обновить манифест VSIX сказать, диспетчер пакетов NuGet, а не инструменты VSIX](http://nuget.codeplex.com/workitem/364)
* [Команда Get-Package вызывает ошибку, при выборе всех источника](http://nuget.codeplex.com/workitem/359)
* [Разрешить порядок источников пакетов в диалоговом окне параметров](http://nuget.codeplex.com/workitem/356)
* [Пакет обновления не приводит к удалению более старой версии](http://nuget.codeplex.com/workitem/352)
* [Реализуйте диапазон версий спецификации для зависимостей](http://nuget.codeplex.com/workitem/347)
* [Visual Studio аварийно завершает работу, при нажатии кнопки «Добавить новый пакет»](http://nuget.codeplex.com/workitem/346)
* [Отображать файлы для загрузки и оценки в диалоговое окно добавления пакета](http://nuget.codeplex.com/workitem/345)
* [Смена источники пакетов в диалоговом окне не обновляет активной исходной](http://nuget.codeplex.com/workitem/344)
* [Удаление привязки ключей для окна консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/339)
* [Install-Package не распознан как имя командлета...](http://nuget.codeplex.com/workitem/338)
* [Установка пакета из локального веб-канала зависимости в обычных веб-каналы, не разрешаются](http://nuget.codeplex.com/workitem/332)
* [Пропустить зависимости, которые все еще используют RemoveDependencies](http://nuget.codeplex.com/workitem/331)
* [Если Отмена Навигация по страницам, пользователь не может перемещаться на другую страницу, а возвращает исходный запрос страницы](http://nuget.codeplex.com/workitem/325)
* [Проверьте производительность NuPack.Server для обслуживания веб-каналы с большим количеством пакетов.](http://nuget.codeplex.com/workitem/324)
* [Во второй раз ли фильтр для пакета, он использует источника пакета «Создать», вместо ранее выбранного источника.](http://nuget.codeplex.com/workitem/321)
* [Источник пакета по умолчанию должен быть выбран, при выборе вкладки «В сети» в диалоговом окне.](http://nuget.codeplex.com/workitem/320)
* [Пакета списка должно отображаться установленные пакеты по умолчанию](http://nuget.codeplex.com/workitem/309)
* [HintPaths ссылки сборки](http://nuget.codeplex.com/workitem/294)
* [Исключение при открытии консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/268)
* [Intellisense консоли загружает весь веб-канал](http://nuget.codeplex.com/workitem/259)
* [«Default» источник пакета должен быть переименован на «Активно»](http://nuget.codeplex.com/workitem/258)
* [Пакет источники пользовательского интерфейса: нажмите кнопку ОК следует добавить новый источник, если источник/имени поля пустым](http://nuget.codeplex.com/workitem/257)
* [Диалоговое окно становится она слишком медленная, если велико число установленных пакетов](http://nuget.codeplex.com/workitem/243)
* [Поддержка переадресации привязок для сборок со строгими именами](http://nuget.codeplex.com/workitem/238)
* [Добавление ссылки на пакет... Пользовательский Интерфейс для включения перетаскивания вниз источника пакетов](http://nuget.codeplex.com/workitem/226)
* [NuPack должен поддерживать преобразование конфигурации agnostically имя файла конфигурации](http://nuget.codeplex.com/workitem/224)
* [Позволяет BasePath переопределяемого в NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Поведение источника пакета](http://nuget.codeplex.com/workitem/204)
* [Аварийно завершить работу в графического пользовательского интерфейса](http://nuget.codeplex.com/workitem/201)
* [Добавить параметры, чтобы добавить диалоговое окно пакета сортировки](http://nuget.codeplex.com/workitem/179)
* [сочетание клавиш или клавиша снимите консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/174)
* [PowerConsole приводит к консоли NuPack переход на другой](http://nuget.codeplex.com/workitem/166)
* [Консоль и добавить диалоговое окно пакета следует задать агент пользователя в запросах](http://nuget.codeplex.com/workitem/141)
* [Задать номер версии VSIX и NuPack.exe в сборке.](http://nuget.codeplex.com/workitem/134)
* [Скрыть общие параметры PowerShell от-?](http://nuget.codeplex.com/workitem/118)
* [Добавить — подробные справочные сведения о командах консоли](http://nuget.codeplex.com/workitem/110)
* [Добавить, что диалоговое окно пакета должен быть разрешен выбор текущего источника пакета](http://nuget.codeplex.com/workitem/88)
* [Переместите NuPack.Core классы в разных пространствах имен](http://nuget.codeplex.com/workitem/50)
* [Добавление справки для командлетов](http://nuget.codeplex.com/workitem/23)
* [После загрузки пакета будет проверять хэш из веб-канала](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP-ВЕРСИЯ 2

Ниже приведены наиболее значительные изменения, внесенные в CTP-версия 2.

* Переключения пакета канал ATOM для конечной точки службы OData: при обновлении до версии CTP2 NuGet, не забудьте добавить следующий URL-адрес в качестве источника пакета: `https://feed.nuget.org/ctp2/odata/v1/`.
* Переименовать команду Add-Package, чтобы *Install-Package*.
* Обновить `.nuspec` формат. `.nuspec` Формат теперь включает *iconUrl* поле для указания значок png 32 x 32, которое будет отображаться в диалоговом окне Добавление пакета. Поэтому не забудьте задать, чтобы отличить пакета. `.nuspec` Формат также включает новый *projectUrl* поле, которое можно использовать, чтобы она указывала на веб-страницу, с дополнительными сведениями о пакете.

Эта сборка не будет работать с старый `.nupkg` файлов. При получении исключения пустую ссылку, вы используете старый `.nupkg` файл и ее необходимо перестроить с измененным [средство командной строки NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Ниже приведен список компонентов и ошибок, которые были исправлены для NuGet CTP-версия 2 (не включает сведения об ошибках дополнительный код очистки и т.д.).

* [Ошибка распаковки сборки пакетов при указании TargetFramework для сборки.](http://nuget.codeplex.com/workitem/10)
* [Сделать окно консоли NuPack более доступным для обнаружения](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe выпуска](http://nuget.codeplex.com/workitem/19)
* [Усовершенствованная обработка ошибок и исключений](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager должно корректно обрабатывать ошибки, связанные с веб-канал](http://nuget.codeplex.com/workitem/28)
* [Требуется новый значок для консоли](http://nuget.codeplex.com/workitem/29)
* [Локализация строк в диалоговом окне](http://nuget.codeplex.com/workitem/38)
* [Кэши NuPack загруженные файлы .nupack в памяти](http://nuget.codeplex.com/workitem/40)
* [Консоль NuPack: Измените сочетание клавиш по умолчанию для отображения консоли](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem должен поддерживать значения по умолчанию для общих свойств](http://nuget.codeplex.com/workitem/49)
* [Выполнив только один файл nuspec nupack.exe в папке следует использовать эти метаданные nuspec](http://nuget.codeplex.com/workitem/52)
* [Меню "проект" отображается даже при загрузке нет проект или решение](http://nuget.codeplex.com/workitem/54)
* [Build.cmd завершается сбоем в чистую копию базы кода](http://nuget.codeplex.com/workitem/56)
* [Функция доступных обновлений](http://nuget.codeplex.com/workitem/57)
* [Диалоговое окно: Добавление пакета с помощью диалогового окна удаляет строки в консоли](http://nuget.codeplex.com/workitem/73)
* [Добавление пакета, нажав кнопку «Установить» часто работает медленно, не визуальную обратную связь](http://nuget.codeplex.com/workitem/80)
* [Нет способа для обнаружения каких моей установленные пакеты установлены обновления.](http://nuget.codeplex.com/workitem/82)
* [Нет способа для обновления установленного пакета в диалоговом окне.](http://nuget.codeplex.com/workitem/83)
* [Нет способа для удаления установленного пакета в диалоговом окне](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Добавление ссылки на пакет&hellip; &rdquo; появляется в контекстном меню установленного ссылок](http://nuget.codeplex.com/workitem/85)
* [После обновления пакета из консоли, он показан в старой версии и в новой версии виде установлен](http://nuget.codeplex.com/workitem/86)
* [Действия в консоли, при использовании диалогового окна, исчезает после использования](http://nuget.codeplex.com/workitem/87)
* [Очистка командной строки, синтаксический анализ в nupack.exe](http://nuget.codeplex.com/workitem/89)
* [Добавьте понятное имя для источников пакетов](http://nuget.codeplex.com/workitem/98)
* [Обновить файлу nuspec для поддержки, включая значки пакета](http://nuget.codeplex.com/workitem/103)
* [Пользовательский Интерфейс веб-канала не допускает копирование URL-адрес](http://nuget.codeplex.com/workitem/105)
* [Улучшенную обработку ошибок remove-package.](http://nuget.codeplex.com/workitem/107)
* [Введите в окне консоли зависит от фокус курсора](http://nuget.codeplex.com/workitem/112)
* [Найдите ужасная сообщения об ошибках](http://nuget.codeplex.com/workitem/116)
* [Производительность Remove-пакет для пакета, которая не была установлена неверная](http://nuget.codeplex.com/workitem/117)
* [Удаление пакета завершается ошибкой, если нет источников пакета](http://nuget.codeplex.com/workitem/119)
* [Удаление пакета завершается с ошибкой при недоступности источника пакета](http://nuget.codeplex.com/workitem/120)
* [Добавьте заголовок в метаданные пакета, а также веб-канала.](http://nuget.codeplex.com/workitem/125)
* [Добавить параметр - источник обратно в Add-Package](http://nuget.codeplex.com/workitem/127)
* [Список-пакет должен иметь параметр - источника](http://nuget.codeplex.com/workitem/128)
* [Обновить NuPack.Server требуется NuPack пользователя для загрузки пакета агента](http://nuget.codeplex.com/workitem/142)
* [Диалоговое окно принятия лицензии необходимо перечислить лицензии для всех зависимостей, запрос на принятие условий](http://nuget.codeplex.com/workitem/145)
* [Регистрирует ошибку в том случае, когда создает пакет в веб-канала](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe не должен разрешать пустая &lt;licenseurl&gt; элемент](http://nuget.codeplex.com/workitem/152)
* [Переименование пакета списка в Get-Package, Add-Package Remove-Package и Install-Package Uninstall-Package](http://nuget.codeplex.com/workitem/155)
* [С помощью пункта меню Добавить ссылку на пакет из Навигатор по решению аварийно завершает работу Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Метка «доступных источниках» отсутствует двоеточие](http://nuget.codeplex.com/workitem/160)
* [Сделать файлу nuspec xml элемент регистр согласованно смешанный регистр](http://nuget.codeplex.com/workitem/161)
* [Манифест NuPack VSIX необходимо включить бит «admin»](http://nuget.codeplex.com/workitem/162)
* [При запуске пакета списка с не веб-каналы, возникнет ошибка пустая ссылка на](http://nuget.codeplex.com/workitem/164)
* [NuGet.exe: укажите конечный путь](http://nuget.codeplex.com/workitem/171)
* [Открытие консоли управления пакетами в WinXP ошибок PowerShell](http://nuget.codeplex.com/workitem/175)
* [VS сбоев при попытке загрузить список пакетов](http://nuget.codeplex.com/workitem/176)
* [Разрешает пакетам meta (нет файлов, только зависимости)](http://nuget.codeplex.com/workitem/180)
* [Преобразование скрипта Powershell для модуля Powershell 2.0](http://nuget.codeplex.com/workitem/181)
* [Если целевой объект указан PathResolver удаляет символы-шаблоны выше часть пути](http://nuget.codeplex.com/workitem/183)
* [Без зависимостей](http://nuget.codeplex.com/workitem/186)
* [Произошла ошибка при установке Elmah](http://nuget.codeplex.com/workitem/192)
* [Преобразования конфигурации могут работать некорректно с &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [Переменной "$глобальное: projectCache" невозможно извлечь, поскольку он не задан](http://nuget.codeplex.com/workitem/203)
* [Добавление задачи MSBuild для создания пакетов NuPack](http://nuget.codeplex.com/workitem/205)
* [список пакетов должен поддерживать фильтрации или поиска](http://nuget.codeplex.com/workitem/206)
* [Всегда отображать ссылку на лицензию, если автор пакета предоставляет URL-адрес лицензии](http://nuget.codeplex.com/workitem/208)
* [Редкое исключение «Доступ запрещен», с помощью Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Сбой модульных тестов: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Разрешить откат/по умолчанию набор файлов, если не удается найти версию платформы содержится код](http://nuget.codeplex.com/workitem/223)
* [Добавление ссылки на пакет... Пользовательский Интерфейс не может удалить пакет](http://nuget.codeplex.com/workitem/225)
* [Добавить ссылку на пакет аварийно завершает работу studio, если в одном или нескольких проект выгружается](http://nuget.codeplex.com/workitem/228)
* [Преобразование конфигурации может не работать в файле web.debug.config](http://nuget.codeplex.com/workitem/229)
* [Init.ps1, возникает не возможности пользовательского пакета](http://nuget.codeplex.com/workitem/237)
* [При добавлении путей feedlist, кнопкой по умолчанию задано значение "ОК", поэтому при нажатии клавиши ENTER автоматически закрывается](http://nuget.codeplex.com/workitem/240)
* [Попытаться удалить зависимости произойдет сбой VS при попытке это сделать в два раза подряд](http://nuget.codeplex.com/workitem/241)
* [Отображение URL-адрес проекта в диалоговом окне Add Package](http://nuget.codeplex.com/workitem/253)
* [По умолчанию в диалоговом окне Add-Package установленные пакеты](http://nuget.codeplex.com/workitem/254)
* [Изменение элемента меню Добавить диалоговое окно пакета.](http://nuget.codeplex.com/workitem/261)
* [Переименуйте пространства имен и сборки](http://nuget.codeplex.com/workitem/274)
* [Переименование проекта NuPack в NuGet](http://nuget.codeplex.com/workitem/282)
* [Добавьте следующий текст в списке зависимостей](http://nuget.codeplex.com/workitem/288)
* [Измените текст принятия лицензии в диалоговое окно принятия лицензии](http://nuget.codeplex.com/workitem/291)
* [Измените текст в диалоговое окно принятия лицензионного над списком пакетов](http://nuget.codeplex.com/workitem/292)
* [OData не работает с URL-адрес fwlink](http://nuget.codeplex.com/workitem/304)
* [Пользовательский Интерфейс диспетчера пакетов: через активное кэширование число пакетов, используемый для разбиения на страницы](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet —&gt; ошибка консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/335)
* [Добавьте пакет диалоговое окно показывает лицензии приемки для установки поставляется в виде](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP-ВЕРСИЯ 1

Ниже приведен список компонентов и ошибок, которые были исправлены для NuGet CTP 1.

* [Расширение пакета должно быть заменено .nupack](http://nuget.codeplex.com/workitem/1)
* [Переместите файл пакета в папку](http://nuget.codeplex.com/workitem/2)
* [Слияние установки &amp; команды Добавить PS](http://nuget.codeplex.com/workitem/3)
* [Создание псевдонимов для командлетов глагол-существительное](http://nuget.codeplex.com/workitem/4)
* [Получает путать NuPack при переключении решение в Visual STUDIO](http://nuget.codeplex.com/workitem/6)
* [Скрывать папки решения «пакеты» по умолчанию](http://nuget.codeplex.com/workitem/11)
* [Добавьте поддержку для замены токенов в элементы содержимого.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI должны использовать PackageSource API](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager помечает пакеты, как установить перед их установкой](http://nuget.codeplex.com/workitem/27)
* [Удаление проекта по умолчанию из решения по-прежнему показывает удаленного проекта по умолчанию](http://nuget.codeplex.com/workitem/30)
* [Новый пакет завершается сбоем с «Невозможно добавить часть для заданного URI, поскольку он уже находится в пакете.»](http://nuget.codeplex.com/workitem/32)
* [Удаление строки «NuPack» из графического пользовательского интерфейса Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Добавьте файл Apache заголовка для COPYRIGHT.txt](http://nuget.codeplex.com/workitem/36)
* [Удалить команду Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Невозможно использовать, при загрузке профиля диспетчера пакетов возникло исключение](http://nuget.codeplex.com/workitem/39)
* [Init.ps1, возникает и install.ps1, uninstall.ps1 должны получить дополнительное состояние](http://nuget.codeplex.com/workitem/41)
* [Объединить в один пакет консоли и пакеты графического пользовательского интерфейса](http://nuget.codeplex.com/workitem/42)
* [Логика преобразования XML не работает, если применить к XML, который находится в корне](http://nuget.codeplex.com/workitem/43)
* [Диалоговое окно параметров источников пакета не обновляя NuPack консоль управления](http://nuget.codeplex.com/workitem/44)
* [Пользовательский Интерфейс консоли NuPack: Переименование раскрывающегося списка «Веб-канал пакетов» в «Источник пакета»](http://nuget.codeplex.com/workitem/45)
* [Параметры консоли NuPack: Переименовать «Пользовательского интерфейса репозитория» для согласования с NuPack консоли](http://nuget.codeplex.com/workitem/46)
* [Не удается добавить пакет с веб-сайта, который был открыт из IIS или URL-адрес](http://nuget.codeplex.com/workitem/53)
* [Диспетчер пакетов источника не работает с FwLink](http://nuget.codeplex.com/workitem/55)
* [Задайте источник пакета по умолчанию](http://nuget.codeplex.com/workitem/59)
* [При добавлении источники пакетов в случае, если задан только один источник, предполагается, что он используется по умолчанию.](http://nuget.codeplex.com/workitem/60)
* [Диалоговое окно пользовательского интерфейса показаны поддельных пакетов «последние»](http://nuget.codeplex.com/workitem/62)
* [Параметры: Нажмите кнопку "Отмена" не отменяет изменения](http://nuget.codeplex.com/workitem/63)
* [Добавьте пакет ссылку диалоговое окно поиска должен быть без учета регистра](http://nuget.codeplex.com/workitem/65)
* [Устраните компании метаданных в файле AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Номер версии для VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: С помощью-? Отображает справку в два раза](http://nuget.codeplex.com/workitem/72)
* [Выполнение установки или удаления пакетов для пакетов уровня проекта](http://nuget.codeplex.com/workitem/74)
* [Серверу не удалось создать веб-канала, если один nupack возникает ошибка проверки](http://nuget.codeplex.com/workitem/90)
* [Потребность в замене NuPack значки](http://nuget.codeplex.com/workitem/94)
* [Прокси-сервер http NTLM не выполняет проверку подлинности для веб-канал пакетов.](http://nuget.codeplex.com/workitem/96)
* [Диалоговое окно всегда не запускается по центру в окне VS](http://nuget.codeplex.com/workitem/100)
* [Многие поля подробно пакеты не заполняемых в настоящий момент в диалоговом окне](http://nuget.codeplex.com/workitem/102)
* [Диалоговое окно пользовательского интерфейса не показывает имена авторов](http://nuget.codeplex.com/workitem/108)
* [Почему - версии для Remove-Package](http://nuget.codeplex.com/workitem/113)
* [Удаление последней вкладки диалогового окна пользовательского интерфейса](http://nuget.codeplex.com/workitem/115)
* [Сбой VS при справа щелкните папку решения после открытия диалогового окна пользовательского интерфейса, по крайней мере один.](http://nuget.codeplex.com/workitem/126)
* [Измените параметр - Local пакета списка - установленных](http://nuget.codeplex.com/workitem/129)
* [Переименуйте packages.xml в NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Консоль заставляет курсор в конец строки](http://nuget.codeplex.com/workitem/135)
* [Происходит нарушение работы intellisense Remove-Package](http://nuget.codeplex.com/workitem/136)
* [Добавить флаг RequireLicenseAcceptance к файлу nuspec и веб-канал](http://nuget.codeplex.com/workitem/137)
* [Добавление веб-канала LicenseUrl по файлу nuspec форматированию и созданию пакета](http://nuget.codeplex.com/workitem/138)
* [Щелкнув установки для пакета, который требует принятия должно отображаться диалоговое окно принятия](http://nuget.codeplex.com/workitem/139)
* [Добавить текст заявления об отказе в диалоговом окне Добавить пакет](http://nuget.codeplex.com/workitem/140)
* [Добавить заявление об отказе при пакета консоль запускается первый раз](http://nuget.codeplex.com/workitem/143)
* [Отображать заявление об отказе после установки пакета в консоли](http://nuget.codeplex.com/workitem/144)
* [Переименуйте .nupack расширение файла nupkg](http://nuget.codeplex.com/workitem/146)