---
title: Заметки о выпуске версии-кандидата NuGet 4.0
description: Заметки о выпуске для версии-кандидата NuGet 4.0, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496640"
---
# <a name="nuget-40-rc-release-notes"></a>Заметки о выпуске версии-кандидата NuGet 4.0

[Заметки о выпуске версии-кандидата 3.5](../release-notes/nuget-3.5-RTM.md)

В [версии-кандидате NuGet 4.0 для Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) реализована поддержка сценариев использования .NET Core, учтены основные пожелания клиентов и улучшена производительность в различных ситуациях. В этой версии появился ряд усовершенствований, таких как поддержка формата PackageReference, использование команд NuGet в качестве целей MSBuild, восстановление пакетов в фоновом режиме и других.

## <a name="bug-fixes"></a>Исправления ошибок

- Изменение поведения команды `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)

- Сбой команды nuget.exe restore на компьютерах только со средой Visual Studio 15 — [#3834](https://github.com/NuGet/Home/issues/3834)

- При выборе команды "Файл" > "Новый проект" > ".NET Core" должна блокироваться сборка во время восстановления — [#3780](https://github.com/NuGet/Home/issues/3780)

- Невозможно восстановить веб-приложение ASP.NET Core, перенесенное из Visual Studio 2015 в Visual Studio 15. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Сбой теста] Пакет jQuery Validation невозможно удалить с помощью пользовательского интерфейса диспетчера пакетов — [#3755](https://github.com/NuGet/Home/issues/3755)

- При установке пакета в проекте универсальной платформы Windows на основе файла `project.json` родительские проекты также должны восстанавливаться — [#3731](https://github.com/NuGet/Home/issues/3731)

- Уровень детализации при записи источников пакетов в журнал для целей NuGet следует изменить с обычного на высокий — [#3719](https://github.com/NuGet/Home/issues/3719)

- dotnet
  - Команда dotnetcore pack3 должна включать документацию XML по умолчанию — [#3698](https://github.com/NuGet/Home/issues/3698)

- Операция пакетного обновления из пользовательского интерфейса завершается сбоем, если источник без пакета является первым в списке и выбран параметр "Весь источник" — [#3696](https://github.com/NuGet/Home/issues/3696)

- Команда nuget pack включает не все файлы — [#3678](https://github.com/NuGet/Home/issues/3678)

- Проблема нехватки памяти — [#3661](https://github.com/NuGet/Home/issues/3661)

- В разделе ProjectFileDependencyGroups файла ресурсов следует использовать имена библиотек для проектов — [#3611](https://github.com/NuGet/Home/issues/3611)

- Команда dotnet restore и рекурсивные каталоги — [#3517](https://github.com/NuGet/Home/issues/3517)

- Сбои Restore3 записываются в журнал как предупреждения, а не как ошибки — [#3503](https://github.com/NuGet/Home/issues/3503)

- Ошибка Team Foundation Server: "Не удалось найти элемент [файл] в рабочей области или у вас нет разрешения на доступ к нему" — [#2805](https://github.com/NuGet/Home/issues/2805)

- Если ввести "nuget <packagename>" в поле быстрого поиска Visual Studio, префикс "nuget " сохраняется — [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException. Нераспознанный корневой элемент в части "Core Properties". Строка 2, позиция 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- Сборка файлов `.nuspec` с экранированными символами &lt; или &gt; в текстовых полях больше не выполняется — [#2651](https://github.com/NuGet/Home/issues/2651)

- При выполнении команды nuget.exe delete не запрашиваются учетные данные (используется неинтерактивный режим) — [#2626](https://github.com/NuGet/Home/issues/2626)

- При выполнении команды nuget.exe delete выводится предупреждение о ключе API для локальных источников, хотя это не имеет смысла — [#2625](https://github.com/NuGet/Home/issues/2625)

- Требуются более понятные сведения об ошибке при установке пакета EF с параметром -pre — [#2566](https://github.com/NuGet/Home/issues/2566)

- После изменения выбранных решений в диспетчере пакетов произошло аварийное завершение работы Visual Studio — [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - Команда dotnetcore restore выполняет поиск идентификаторов с учетом регистра в локальных репозиториях в формате плоского списка при использовании гибких версий — [#2516](https://github.com/NuGet/Home/issues/2516)

- Команда nuget.exe delete неправильно работает для веб-канала версии 2 — [#2509](https://github.com/NuGet/Home/issues/2509)

- Требуется более понятное сообщение об ошибке истечения срока действия для команды nuget.exe push — [#2503](https://github.com/NuGet/Home/issues/2503)

- Восстановление средства завершается сбоем при отсутствии надлежащих операторов импорта без вывода сообщений об ошибках. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet запрашивает учетные данные при наличии закрытого веб-канала, даже если установка производится с сайта nuget.org — [#2346](https://github.com/NuGet/Home/issues/2346)

- Пакет ApplicationInsights 2.0 имеется в списке, но пока не существует — [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay в ветви предварительной версии 5 среды Visual Studio 15 — [#3500](https://github.com/NuGet/Home/issues/3500)

- Первое событие OnBuild отсутствует при восстановлении во время сборки для проекта универсальной платформы Windows — [#3489](https://github.com/NuGet/Home/issues/3489)

- Нарушение работы PowerShell5 при установке EntityFramework. - [#3312](https://github.com/NuGet/Home/issues/3312)

- Необходимо добавить источник при подробном ведении журнала (рекомендуется для версии 3.5) — [#3294](https://github.com/NuGet/Home/issues/3294)

- Параметр NoCache не учитывается в версии клиента NuGet 3.4 и более поздних — [#3074](https://github.com/NuGet/Home/issues/3074)

- Если в Visual Studio не удается загрузить поставщик учетных данных, не следует прерывать работу NuGet — [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Компоненты

- Настройка непрерывной интеграции для выполнения на 86-разрядных компьютерах — [#3868](https://github.com/NuGet/Home/issues/3868)

- Автоматическое восстановление, 3 из 3: пользовательский интерфейс без блокировки — [#3658](https://github.com/NuGet/Home/issues/3658)

- Автоматическое восстановление, 2 из 3: восстановление в фоновом режиме при назначении — [#3657](https://github.com/NuGet/Home/issues/3657)

- Восстановление ссылок проекта в соответствии с поведением сборки (рекурсивная обработка) — [#3615](https://github.com/NuGet/Home/issues/3615)

- Поддержка DPL в Visual Studio 15 — minbar — [#3614](https://github.com/NuGet/Home/issues/3614)

- Перенос файла параметров в папку Program Files — [#3613](https://github.com/NuGet/Home/issues/3613)

- Создаваемым свойствам и целям восстановления требуется поддержка кроссплатформенного нацеливания — [#3496](https://github.com/NuGet/Home/issues/3496)

- Поддержка восстановления NuGet для PackageTargetFallback (прежнее название — Imports) — [#3494](https://github.com/NuGet/Home/issues/3494)

- Реализация ToolsRef — [#3472](https://github.com/NuGet/Home/issues/3472)

- Restore3 для RID — [#3465](https://github.com/NuGet/Home/issues/3465)

- Поддержка добавления, удаления и обновления ссылок на пакеты в пользовательском интерфейсе NuGet — [#3457](https://github.com/NuGet/Home/issues/3457)

- Автоматическое восстановление, 1 из 3: реализация API номинации путем кэширования сведений о восстановлении проектов — [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] Задача и цели восстановления NuGet — [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] Обеспечение восстановления на уровне решения в MSBuild — [#2993](https://github.com/NuGet/Home/issues/2993)

- Поддержка общедоступной расширяемости для поставщика учетных данных в Visual Studio — [#2909](https://github.com/NuGet/Home/issues/2909)

- Рекурсивное восстановление NuGet — [#2533](https://github.com/NuGet/Home/issues/2533)

- Невозможно загрузить Microsoft.TeamFoundation.Client в dev15; необходимо обновить Microsoft.TeamFoundation.Client до версии 15.0 для предварительной версии Visual Studio 15 — [#2392](https://github.com/NuGet/Home/issues/2392)

- Невозможно установить пакет C++ в проекте универсальной платформы Windows на C++ в предварительной версии Visual Studio 15 — [#2369](https://github.com/NuGet/Home/issues/2369)

- Формат Nupkg должен поддерживать папку \buildCrossTargeting\ и импортировать `.targets` / `.props` при кроссплатформенном нацеливании MSBuild. - [#3499](https://github.com/NuGet/Home/issues/3499)

- Структура ToolsReference — [#3462](https://github.com/NuGet/Home/issues/3462)

- Исправлен пользовательский интерфейс NuGet для поддержки восстановления со ссылками PackageReference в `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)

- Добавлена кнопка очистки кэша в параметры диспетчера пакетов Visual Studio — [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>Запросы на изменение структуры

- Восстановление решения должно блокироваться во время автоматического восстановления. - [#3797](https://github.com/NuGet/Home/issues/3797)

- Установка NetCore из пользовательского интерфейса диспетчера пакетов NuGet производится для каждого моникера целевой платформы, а не только для тех, которые поддерживаются пакетом — [#3721](https://github.com/NuGet/Home/issues/3721)

- Интерфейс API назначения на восстановление должен также поддерживать DotNetCliToolsReferences. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Расширение VSIX для Visual Studio 15 помечено как systemcomponent — [#3700](https://github.com/NuGet/Home/issues/3700)

- Переход от ссылок на MS.VS.Services.Client к ссылкам на MS.VS.Services.Client.Interactive — [#3670](https://github.com/NuGet/Home/issues/3670)

- Свойство $(RestoreLegacyPackagesDirectory) должно учитываться командой восстановления на уровне проекта — [#3618](https://github.com/NuGet/Home/issues/3618)

- При восстановлении в проекте с одним значением TargetFramework не должны применяться условия к свойствам — [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet
  - Команда dotnetcore restore3 foo.csproj должна учитывать зависимости projectref и восстанавливать их так же, как при сборке. - [#3577](https://github.com/NuGet/Home/issues/3577)

- Зависимости "type": "platform" представлены как "type":"package" в файле блокировки — [#2695](https://github.com/NuGet/Home/issues/2695)

- В режиме подробного вывода nuget.exe должен отображаться URL-адрес скачивания — [#2629](https://github.com/NuGet/Home/issues/2629)

- Перенос NuGet xplat в Microsoft.NetCore.App и netcoreapp1.0 — [#2483](https://github.com/NuGet/Home/issues/2483)

- Принудительная отправка — при отправке из командной строки должна быть возможность переопределить сервер символов — [#2348](https://github.com/NuGet/Home/issues/2348)

- Объединение кода для определения пути к папке глобальных пакетов — [#2296](https://github.com/NuGet/Home/issues/2296)

- suppressParent необходимо заменить на лучшее имя — [#2196](https://github.com/NuGet/Home/issues/2196)

- Определение имени зависимости `project.json`, которое следует использовать для проектов MSBuild — [#1914](https://github.com/NuGet/Home/issues/1914)

- Добавление поддержки SemVer 2.0.0 в NuGet.Core — [#3383](https://github.com/NuGet/Home/issues/3383)

- Доступность файлов NUPKG транзитивной зависимости с `.targets` в MSBuild — [#3342](https://github.com/NuGet/Home/issues/3342)

- Операция восстановления NuGet из командной строки выполняется значительно медленнее, чем в Visual Studio — [#3330](https://github.com/NuGet/Home/issues/3330)

- Отключение учета регистра при сравнении идентификаторов и версий пакетов — [#2522](https://github.com/NuGet/Home/issues/2522)

- Параметр NoCache не работает при восстановлении или установке на основе `packages.config` (GlobalPackagesFolder) — [#1406](https://github.com/NuGet/Home/issues/1406)

- Ресурсам FindPackageByIdResource требуется контекст кэша по умолчанию и средство ведения журнала — [#1357](https://github.com/NuGet/Home/issues/1357)
