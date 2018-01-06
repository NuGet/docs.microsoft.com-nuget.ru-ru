---
title: "NuGet 1.0 и 1.1 заметки о выпуске | Документы Microsoft"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0e7688f7-09d2-4477-9fdf-0e27f572a4de
description: "Заметки о выпуске для NuGet 1.1, включая известные проблемы, исправленные ошибки, добавленные функции и DCR."
keywords: "NuGet 1.1 заметки о выпуске, исправления, известными проблемами, добавлены функции, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 593848b3e5e063816fbbec8b4d11e6fc789d05cd
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-10-and-11-release-notes"></a>Заметки о выпуске NuGet 1.0 и 1.1

[Заметки о выпуске 1.2 NuGet](../release-notes/nuget-1.2.md)

NuGet 1.0 была выпущена 13 января 2011 г.  12 февраля 2011 г. была выпущена NuGet 1.1.

## <a name="overview"></a>Обзор

Этот документ содержит заметки о выпуске для различных версий, сгруппированные по основных предварительной версии 1.0 NuGet.

NuGet включает следующие компоненты:

* *NuGet.Tools.vsix* * которого состоит из:
  * **Добавить диалоговое окно библиотеки пакета** * диалоговое окно в среде Visual Studio позволяет просматривать и устанавливать пакеты.
  * **Консоль диспетчера пакетов** * консоли в среде Visual Studio, на основе Powershell.
* *Средство командной строки NuGet* * средство используется для создания (и в конечном итоге публикации) пакетов.

Расширение NuGet средств Visual Studio (*NuGet.Tools.vsix*) требуется:

* Visual Studio 2010 или Visual Web Developer 2010 Express.

Средство командной строки NuGet требуются:

* Версия платформы .NET framework 4

## <a name="installation"></a>Установка

Для использования этой [последний выпуск](http://nuget.codeplex.com/releases/view/52018):

* Сначала удалите старые сборки. Необходимо выполнять от имени администратора для этого VS.
* Удалите все существующие веб-каналы, у вас есть.
* Добавить новый канал, указывающий [http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

Список проблем, исправленных в этом выпуске [можно найти здесь](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Одна проблема была устранена для RTM с момента версии-Кандидата.

* [Проблема 474: Удаление пакетов затрагивает всех проектов в решении](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Версия-кандидат

Ниже приведены изменения в этой версии-кандидата, с момента CTP-версии 2. Посетите отслеживания проблем, чтобы просмотреть весь список ошибок.

* [Обновление пакета из консоли не обновляет зависимости.](http://nuget.codeplex.com/workitem/443)
* [Добавление пакета воспринимает bin не пакета ссылки (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Обновление пакета оставляет неработающих ссылок](http://nuget.codeplex.com/workitem/440)
* [Get-Package-обновления, не выполняется в диалоговом окне, или при выборе источника «Все» агрегатов в консоли](http://nuget.codeplex.com/workitem/439)
* [Получение ошибки при проверке пакета](http://nuget.codeplex.com/workitem/426)
* [Предупреждать пользователей, если пакет не может быть установлен из диалогового окна добавления пакета](http://nuget.codeplex.com/workitem/425)
* [Get-Package-обновляет возникает исключение при обновлении большого числа пакетов](http://nuget.codeplex.com/workitem/424)
* [Улучшения обработки ошибок при nuspec-файлы разрабатываются неправильно](http://nuget.codeplex.com/workitem/423)
* [Пакет NuGet игнорирует указанные файлы](http://nuget.codeplex.com/workitem/422)
* [Удаление источнике пакетов в секунду с последним и выбрав команду «Переместить вниз» аварийно завершает работу VS](http://nuget.codeplex.com/workitem/418)
* [Удалить ссылку на сборку во время установки пакетов](http://nuget.codeplex.com/workitem/413)
* [Исключение InvalidOperationException при открытии диалогового окна параметров](http://nuget.codeplex.com/workitem/411)
* [Ключ доступа для источника пакета в консоли диспетчера пакетов не работает](http://nuget.codeplex.com/workitem/410)
* [Ключи доступа диалоговое окно параметров NuGet VS переключать фокус на тех полей](http://nuget.codeplex.com/workitem/409)
* [Intellisense идентификатор пакета не должен запросить слишком много элементов](http://nuget.codeplex.com/workitem/404)
* [Ошибка при добавлении пакета в проект с помощью символа точки в имени проекта](http://nuget.codeplex.com/workitem/403)
* [Проблема с указанных файлов в nuspec](http://nuget.codeplex.com/workitem/400)
* [Должен получить зарегистрирован правильно официальный веб-канала, при использовании новой сборки](http://nuget.codeplex.com/workitem/399)
* [Теги следует использовать пробелы вместо #](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata отсутствуют некоторые полезные сведения](http://nuget.codeplex.com/workitem/388)
* [Добавление отчетов о нарушении ссылки на диалоговое окно](http://nuget.codeplex.com/workitem/386)
* [С помощью App_Data распаковать разрывов пакетов в Visual Studio](http://nuget.codeplex.com/workitem/380)
* [Реализации тегов](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder позволяет пустой пакет должен быть создан без зависимостей](http://nuget.codeplex.com/workitem/373)
* [Добавление поля владельцев для пакета](http://nuget.codeplex.com/workitem/365)
* [Обновить манифест VSIX сказать диспетчера пакетов NuGet, а не средства VSIX](http://nuget.codeplex.com/workitem/364)
* [Команда Get-Package вызывает ошибку при выборе всех источника](http://nuget.codeplex.com/workitem/359)
* [Разрешается источников пакетов в диалоговом окне Параметры](http://nuget.codeplex.com/workitem/356)
* [Пакет обновления не удаляет старую версию](http://nuget.codeplex.com/workitem/352)
* [Реализуйте диапазон версий спецификации для зависимостей](http://nuget.codeplex.com/workitem/347)
* [Visual Studio аварийно завершает работу при нажатии кнопки «Добавить новый пакет»](http://nuget.codeplex.com/workitem/346)
* [Отображение в диалоговом окне Добавить пакет загрузки и оценки](http://nuget.codeplex.com/workitem/345)
* [Смена источников пакетов в диалоговом окне не обновляет активной исходной](http://nuget.codeplex.com/workitem/344)
* [Удаление привязки клавиш для окна консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/339)
* [Пакет установки не распознан как имя командлета...](http://nuget.codeplex.com/workitem/338)
* [Установка пакета из локального веб-канала зависимости на обычных веб-каналов не разрешаются](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies следует пропустить зависимости, которые все еще используются](http://nuget.codeplex.com/workitem/331)
* [Если Отмена навигацию по страницам, а возвращает первоначальный запрос страницы пользователя не удается перейти на другую страницу](http://nuget.codeplex.com/workitem/325)
* [Проверьте производительность NuPack.Server для обслуживания веб-каналы с большим числом пакетов.](http://nuget.codeplex.com/workitem/324)
* [Второй раз, когда я фильтрации для пакета, он использует источник пакета «Новая», вместо ранее выбранного источника.](http://nuget.codeplex.com/workitem/321)
* [Источник пакета по умолчанию должен быть выбран при выборе вкладки «В сети» в диалоговом окне.](http://nuget.codeplex.com/workitem/320)
* [Список пакетов должны показывать установленных пакетов по умолчанию](http://nuget.codeplex.com/workitem/309)
* [HintPaths ссылки на сборки](http://nuget.codeplex.com/workitem/294)
* [Исключение при открытии консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/268)
* [Intellisense консоли загружает весь веб-канал](http://nuget.codeplex.com/workitem/259)
* [Источник пакета «Default» должно быть заменено на «Активно»](http://nuget.codeplex.com/workitem/258)
* [Пакет источники пользовательского интерфейса: нажать кнопку ОК следует добавить новый источник, если имя или исходные поля не являются пустыми](http://nuget.codeplex.com/workitem/257)
* [Диалоговое окно super снижается, если существует большое число установленных пакетов](http://nuget.codeplex.com/workitem/243)
* [Поддержка перенаправления привязки сборки со строгими именами](http://nuget.codeplex.com/workitem/238)
* [Добавьте ссылку на пакет... Пользовательский Интерфейс для включения сброса вниз для источника пакетов](http://nuget.codeplex.com/workitem/226)
* [NuPack должен поддерживать преобразование конфигурации agnostically от имени файла конфигурации](http://nuget.codeplex.com/workitem/224)
* [Позволяет BasePath быть переопределен в NuPack.exe](http://nuget.codeplex.com/workitem/222)
* [Поведение источник пакета](http://nuget.codeplex.com/workitem/204)
* [Аварийно завершить работу в графическом интерфейсе пользователя](http://nuget.codeplex.com/workitem/201)
* [Добавить параметры, чтобы добавить пакет диалоговое окно сортировки](http://nuget.codeplex.com/workitem/179)
* [сочетания клавиш для очистки консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/174)
* [Среде PowerConsole вызывает сбой консоли NuPack](http://nuget.codeplex.com/workitem/166)
* [Консоль и добавить пакет диалоговое окно следует задать агента пользователя в запросах](http://nuget.codeplex.com/workitem/141)
* [Задать номер версии VSIX и NuPack.exe в сборке.](http://nuget.codeplex.com/workitem/134)
* [Скрыть общие параметры PowerShell от-?](http://nuget.codeplex.com/workitem/118)
* [Добавление - подробные справочные сведения о командах консоли](http://nuget.codeplex.com/workitem/110)
* [Добавить что диалоговым пакет должен быть разрешен выбор текущего источника пакетов](http://nuget.codeplex.com/workitem/88)
* [Переместите NuPack.Core классы в разных пространствах имен](http://nuget.codeplex.com/workitem/50)
* [Добавление справки по командлетам](http://nuget.codeplex.com/workitem/23)
* [После загрузки пакета будет проверять хэш из канала](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP-ВЕРСИЯ 2

Ниже приведены наиболее существенные изменения, внесенные в CTP-версии 2.

* Переключения пакета веб-канала из ATOM в конечную точку службы OData: при обновлении до версии CTP2 NuGet, не забудьте добавить следующий URL-адрес в качестве источника пакета: [http://go.microsoft.com/fwlink/?LinkID=204820](http://go.microsoft.com/fwlink/?LinkID=204820).
* Переименовать команду Add-Package для *Install-Package*.
* Обновить `.nuspec` формат. `.nuspec` Формат теперь включает *iconUrl* поле для указания значок png 32 x 32, который будет отображаться в диалоговом окне Добавить пакет. Поэтому следует обязательно задать, чтобы отличить пакета. `.nuspec` Формат также включает новый *projectUrl* поле, которое можно использовать, чтобы она указывала на веб-страницу, в котором содержатся дополнительные сведения о пакете.

Эта сборка не будет работать с старого `.nupkg` файлов. При появлении исключения пустую ссылку, вы используете свой старый `.nupkg` файла и ее необходимо перестроить с обновляемым [средство командной строки NuGet](http://nuget.codeplex.com/releases/52017/download/165468).

Ниже приведен список компонентов и ошибок, которые были исправлены NuGet CTP-версия 2 (нет ошибок для очистки дополнительный код и т. д.).

* [Ошибка распаковки пакета сборок при при указании TargetFramework для сборки.](http://nuget.codeplex.com/workitem/10)
* [Создание окна консоли NuPack более доступными](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe выпуска](http://nuget.codeplex.com/workitem/19)
* [Ошибки и исключения обработки.](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager должен правильно обрабатывать ошибки, связанные с веб-канала](http://nuget.codeplex.com/workitem/28)
* [Требуется новый значок для консоли](http://nuget.codeplex.com/workitem/29)
* [Локализация строк в диалоговом окне](http://nuget.codeplex.com/workitem/38)
* [Кэши NuPack загруженные файлы .nupack в памяти](http://nuget.codeplex.com/workitem/40)
* [Консоль NuPack: Измените сочетание клавиш по умолчанию для отображения консоли](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem должен поддерживать значения по умолчанию для общих свойств](http://nuget.codeplex.com/workitem/49)
* [Запускать nupack.exe в папку с одной nuspec-файла следует использовать, nuspec](http://nuget.codeplex.com/workitem/52)
* [Меню проекта отображается даже при загрузке не проект или решение](http://nuget.codeplex.com/workitem/54)
* [Build.cmd сбой на чистой копией базы кода](http://nuget.codeplex.com/workitem/56)
* [Функция обновления недоступна](http://nuget.codeplex.com/workitem/57)
* [Диалоговое окно: Добавление пакета в диалоговом окне удаляет строки в консоли](http://nuget.codeplex.com/workitem/73)
* [Добавление пакета, нажав кнопку «Установить» часто работает медленно, не визуальную обратную связь](http://nuget.codeplex.com/workitem/80)
* [Нет возможности для обнаружения my установленные пакеты, содержащие обновления.](http://nuget.codeplex.com/workitem/82)
* [Нет возможности для обновления установленного пакета в диалоговом окне.](http://nuget.codeplex.com/workitem/83)
* [Нет возможности для удаления установленного пакета в диалоговом окне](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Добавьте ссылки на пакет&hellip; &rdquo; появляется в контекстном меню установленных ссылок](http://nuget.codeplex.com/workitem/85)
* [После обновления пакета в консоли, он показывает старую версию и новую версию как установленные](http://nuget.codeplex.com/workitem/86)
* [Действия в консоли, когда с помощью диалогового окна исчезает после использования](http://nuget.codeplex.com/workitem/87)
* [Команда очистки синтаксического анализа в nupack.exe](http://nuget.codeplex.com/workitem/89)
* [Добавить понятное имя для источников пакетов](http://nuget.codeplex.com/workitem/98)
* [.Nuspec обновления для поддержки, включая пакет значков](http://nuget.codeplex.com/workitem/103)
* [Потока пользовательского интерфейса не допускает копирование URL-адрес](http://nuget.codeplex.com/workitem/105)
* [Обработку ошибок remove-package.](http://nuget.codeplex.com/workitem/107)
* [Ввод в окне консоли зависит от фокуса курсора](http://nuget.codeplex.com/workitem/112)
* [Найдите плохо, сообщения об ошибках](http://nuget.codeplex.com/workitem/116)
* [Неправильная производительность удаление пакета для пакета, которая не установлена](http://nuget.codeplex.com/workitem/117)
* [Удаление пакета завершается ошибкой, если нет источников пакета](http://nuget.codeplex.com/workitem/119)
* [Удаление пакета завершается ошибкой при недоступности источника пакетов](http://nuget.codeplex.com/workitem/120)
* [Добавление заголовка к метаданным пакета и веб-канала.](http://nuget.codeplex.com/workitem/125)
* [Добавить параметр - источника к Add-Package](http://nuget.codeplex.com/workitem/127)
* [Список пакет должен иметь параметр - источника](http://nuget.codeplex.com/workitem/128)
* [NuPack.Server требовать NuPack пользовательского агента для загрузки пакета обновления](http://nuget.codeplex.com/workitem/142)
* [Диалоговое окно принятия лицензии необходимо перечислить лицензии для всех зависимостей, которые требуют принятия](http://nuget.codeplex.com/workitem/145)
* [Регистрирует ошибку, если пакет вызывает в веб-канала](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe не должен позволять пустой &lt;licenseurl&gt; элемент](http://nuget.codeplex.com/workitem/152)
* [Переименование пакета списка в Get-Package, Add-Package пакет установки и удаления пакета для удаления пакета](http://nuget.codeplex.com/workitem/155)
* [С помощью пункта меню Добавить ссылку на пакет из решения навигатора аварийно завершает работу Visual Studio](http://nuget.codeplex.com/workitem/158)
* [Метка «доступных источниках» отсутствует двоеточие](http://nuget.codeplex.com/workitem/160)
* [Сделать .nuspec xml элемент регистр постоянно camel правильный регистр](http://nuget.codeplex.com/workitem/161)
* [Манифест NuPack VSIX необходимо включить бит «admin»](http://nuget.codeplex.com/workitem/162)
* [При запуске пакета списка с никакие веб-каналы, появляется ошибка null ref](http://nuget.codeplex.com/workitem/164)
* [NuGet.exe: укажите конечный путь](http://nuget.codeplex.com/workitem/171)
* [Открытие консоли управления пакета на WinXP ошибок PowerShell](http://nuget.codeplex.com/workitem/175)
* [VS сбоев при попытке загрузить список пакетов](http://nuget.codeplex.com/workitem/176)
* [Разрешить meta пакетов (нет файлов, только зависимости)](http://nuget.codeplex.com/workitem/180)
* [Преобразование скрипта Powershell в модуль Powershell 2.0](http://nuget.codeplex.com/workitem/181)
* [Если цель указана PathResolver удаляет символы-шаблоны предшествующих часть пути](http://nuget.codeplex.com/workitem/183)
* [Без зависимостей](http://nuget.codeplex.com/workitem/186)
* [Произошла ошибка при установке Elmah](http://nuget.codeplex.com/workitem/192)
* [Настройки преобразований, не работают с &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [Переменная "$глобальное: projectCache" не удается получить, поскольку оно не задано](http://nuget.codeplex.com/workitem/203)
* [Добавить задачу MSBuild для создания пакетов NuPack](http://nuget.codeplex.com/workitem/205)
* [список пакетов должен поддерживать поиск и фильтрация](http://nuget.codeplex.com/workitem/206)
* [Всегда отображать ссылку на лицензии, если у автора пакета предоставляет URL-адрес лицензии](http://nuget.codeplex.com/workitem/208)
* [Иногда исключение «Доступ запрещен» с Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Модульных тестов, завершающихся неудачей: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Разрешить для резервной по умолчанию набор файлов, если не удается найти версию платформы содержится код](http://nuget.codeplex.com/workitem/223)
* [Добавьте ссылку на пакет... Пользовательский Интерфейс не может удалить пакет](http://nuget.codeplex.com/workitem/225)
* [Добавление ссылки на пакет аварийно завершает работу studio, когда один или несколько проект выгружается](http://nuget.codeplex.com/workitem/228)
* [Преобразование конфигурации может не работать в файле web.debug.config](http://nuget.codeplex.com/workitem/229)
* [не удается инициировать на настраиваемый пакет init.ps1](http://nuget.codeplex.com/workitem/237)
* [При добавлении путей feedlist, кнопку по умолчанию имеет значение "ОК", поэтому при нажатии клавиши ENTER автоматически закрывается](http://nuget.codeplex.com/workitem/240)
* [Попытка удалить зависимость, при попытке 2 раза подряд произойдет сбой VS](http://nuget.codeplex.com/workitem/241)
* [Отображение URL-адрес проекта в диалоговом окне Добавление пакета](http://nuget.codeplex.com/workitem/253)
* [По умолчанию в диалоговом окне Add-Package установленные пакеты](http://nuget.codeplex.com/workitem/254)
* [Изменение элемента меню Добавить пакет диалоговое окно.](http://nuget.codeplex.com/workitem/261)
* [Переименование пространств имен и сборок](http://nuget.codeplex.com/workitem/274)
* [Переименование проекта NuPack в NuGet](http://nuget.codeplex.com/workitem/282)
* [Добавьте следующий текст в списке зависимостей.](http://nuget.codeplex.com/workitem/288)
* [Изменения текста принятия лицензии в диалоговое окно принятия лицензии](http://nuget.codeplex.com/workitem/291)
* [Изменить текст в диалоговое окно принятия лицензионного над списком пакетов](http://nuget.codeplex.com/workitem/292)
* [OData поддерживает только URL-адрес fwlink](http://nuget.codeplex.com/workitem/304)
* [Пользовательский Интерфейс диспетчера пакетов: через активное кэширование числа пакетов, используемый для постраничного просмотра](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; ошибка консоли диспетчера пакетов](http://nuget.codeplex.com/workitem/335)
* [Добавление пакета диалоговое окно показывает лицензии приемки для уже установлен упакована](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP-ВЕРСИЯ 1

Ниже приведен список компонентов и ошибок, исправленных в CTP-версия 1 NuGet.

* [Расширение пакета должно быть заменено .nupack](http://nuget.codeplex.com/workitem/1)
* [Переместите файл пакета в папку](http://nuget.codeplex.com/workitem/2)
* [Слияние установки &amp; команды Добавить PS](http://nuget.codeplex.com/workitem/3)
* [Создание псевдонимов для командлетов глагол-существительное](http://nuget.codeplex.com/workitem/4)
* [Возвращает путать NuPack при переключении решений в Visual STUDIO](http://nuget.codeplex.com/workitem/6)
* [Мы должны скрывать папки решения «пакеты» по умолчанию](http://nuget.codeplex.com/workitem/11)
* [Добавьте поддержку для замены токенов в элементы содержимого.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI следует использовать PackageSource API](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager помечает пакеты, которые установлены до начала установки их](http://nuget.codeplex.com/workitem/27)
* [Удаление по умолчанию проект из решения по-прежнему показывает удаленного проекта по умолчанию](http://nuget.codeplex.com/workitem/30)
* [Новый пакет завершает работу с «Не удается добавить часть для указанного URI, поскольку он уже находится в пакете.»](http://nuget.codeplex.com/workitem/32)
* [Удаление строки «NuPack» из графического пользовательского интерфейса Visual Studio](http://nuget.codeplex.com/workitem/35)
* [Добавьте файл Apache заголовок для COPYRIGHT.txt](http://nuget.codeplex.com/workitem/36)
* [Удалить команду Update-PackageSource](http://nuget.codeplex.com/workitem/37)
* [Возникло исключение непригодным для использования при загрузке профиля диспетчера пакетов](http://nuget.codeplex.com/workitem/39)
* [Init.ps1 и install.ps1, uninstall.ps1 должны получать дополнительного состояния](http://nuget.codeplex.com/workitem/41)
* [Объединить в один пакет консоли и пакеты графического пользовательского интерфейса](http://nuget.codeplex.com/workitem/42)
* [Логика преобразования XML не работает, если применяются к XML, которая не находится в корне](http://nuget.codeplex.com/workitem/43)
* [Источники параметров диалоговое окно управления пакетами не обновляя консоль NuPack](http://nuget.codeplex.com/workitem/44)
* [Пользовательский Интерфейс консоли NuPack: Переименование раскрывающегося списка «Пакет веб-канал» для «Источник пакета»](http://nuget.codeplex.com/workitem/45)
* [Параметры консоли NuPack: Переименование «Пользовательского интерфейса репозитория» для соответствия NuPack консоли](http://nuget.codeplex.com/workitem/46)
* [Добавление пакета, не проходящих веб-сайт, который был открыт из IIS или URL-адрес](http://nuget.codeplex.com/workitem/53)
* [Исходный диспетчер пакетов не работает с FwLink](http://nuget.codeplex.com/workitem/55)
* [Задайте источник пакета по умолчанию](http://nuget.codeplex.com/workitem/59)
* [При добавлении источников пакетов в случае, когда задан только один источник, предполагается, что он подразумевается по умолчанию.](http://nuget.codeplex.com/workitem/60)
* [Диалоговое окно пользовательского интерфейса показывает фиктивное пакеты «последние»](http://nuget.codeplex.com/workitem/62)
* [Параметры: Нажмите кнопку "Отмена" отменяет изменения](http://nuget.codeplex.com/workitem/63)
* [Добавить диалоговое окно поиска пакета ссылки должен быть без учета регистра](http://nuget.codeplex.com/workitem/65)
* [Исправьте метаданные компании в файлах AssemblyInfo.cs](http://nuget.codeplex.com/workitem/67)
* [Номер версии для VSIX](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: С помощью-? Вывод справки дважды](http://nuget.codeplex.com/workitem/72)
* [Выполните установку и удаление пакетов для проекта уровня пакетов](http://nuget.codeplex.com/workitem/74)
* [Серверу не удалось создать веб-канала при сбое одного nupack проверки](http://nuget.codeplex.com/workitem/90)
* [Потребность в замене NuPack значки](http://nuget.codeplex.com/workitem/94)
* [Прокси-сервер http NTLM не выполняет проверку подлинности в пакет веб-канала.](http://nuget.codeplex.com/workitem/96)
* [Диалоговое окно всегда не запускается по центру в окне VS](http://nuget.codeplex.com/workitem/100)
* [Многие поля в сведениях пакеты не заполняемых в настоящий момент в диалоговом окне](http://nuget.codeplex.com/workitem/102)
* [Диалоговое окно пользовательского интерфейса не показывает имена авторов](http://nuget.codeplex.com/workitem/108)
* [Почему - версии для удаления пакета](http://nuget.codeplex.com/workitem/113)
* [Удалить вкладку последних диалоговое окно пользовательского интерфейса](http://nuget.codeplex.com/workitem/115)
* [Сбой VS при правом щелкните папку решения после открытия диалогового окна пользовательского интерфейса, по крайней мере один.](http://nuget.codeplex.com/workitem/126)
* [Изменение локального параметра - список пакета - установки](http://nuget.codeplex.com/workitem/129)
* [Переименуйте packages.xml NuPack.config](http://nuget.codeplex.com/workitem/132)
* [Консоль принудительно курсора до конца строки](http://nuget.codeplex.com/workitem/135)
* [Remove-Package intellisense разрывается.](http://nuget.codeplex.com/workitem/136)
* [Добавить флаг RequireLicenseAcceptance .nuspec и веб-канала](http://nuget.codeplex.com/workitem/137)
* [Добавить веб-канал LicenseUrl .nuspec формат и пакета](http://nuget.codeplex.com/workitem/138)
* [Щелкнув установки для пакета, который требует принятия должны показывать диалоговое окно принятия](http://nuget.codeplex.com/workitem/139)
* [Добавьте текст заявления об отказе в диалоговое окно Добавить пакет](http://nuget.codeplex.com/workitem/140)
* [Добавить заявление об отказе при пакета консоль запускается первый раз](http://nuget.codeplex.com/workitem/143)
* [Отображать заявление об отказе после установки пакета в консоли](http://nuget.codeplex.com/workitem/144)
* [Переименуйте расширение .nupack .nupkg](http://nuget.codeplex.com/workitem/146)