---
title: Заметки о выпуске NuGet 5,1 RTM
description: Заметки о выпуске NuGet 5,1, включая новые функции, исправления ошибок и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: d6f6bffc6b5fda9ee1b9d9830f6d7d3c0f5be654
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780140"
---
# <a name="nuget-51-release-notes"></a>Заметки о выпуске NuGet 5,1

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio| Доступно в пакетах SDK для .NET|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core 

<sup>2</sup> Доступно в качестве необязательной установки с помощью Visual Studio 2019 с рабочей нагрузкой .NET Core

## <a name="summary-whats-new-in-51"></a>Сводка: новые возможности в 5,1

* Поддержка пропуска отправки пакета, если он уже существует, чтобы обеспечить лучшую интеграцию с рабочими процессами CI/CD. [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Теперь Visual Studio предоставляет удобную ссылку на страницу коллекции nuget.org пакета — [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Поддержка новых ресурсов .NET Core 3,0, таких как [Целевые пакеты](https://github.com/dotnet/cli/issues/10006) и [пакеты среды выполнения](https://github.com/dotnet/cli/issues/10007)
  * Поддержка пакета NuGet и восстановления для Фрамеворкреференцес для включения целевых объектов и ссылок на пакеты среды выполнения — [#7342](https://github.com/NuGet/Home/issues/7342)
  * Поддержка сценария пакета "только для загрузки" с Паккажедовнлоад- [#7339](https://github.com/NuGet/Home/issues/7339)
  * Исключите среду выполнения и целевые пакеты из результатов поиска & восстановить граф с помощью PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Ошибки**

* Подключаемые модули: сведения об исключении теряются во время создания подключаемого модуля — [#8057](https://github.com/NuGet/Home/issues/8057)

* Диапазон PackageReference с исключающей нижней границей не работает, если нижняя граница существует в одном из источников. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Улучшение сообщения Испаккаблефалсиррор — [#8021](https://github.com/NuGet/Home/issues/8021)

* Пакеты заблокировать файл — повторно создать файл блокировки при изменении графа проекта — [#8019](https://github.com/NuGet/Home/issues/8019)

* Прожектсистем ошибка: пакеты NuGet, получив автоматическое удаление — [#8017](https://github.com/NuGet/Home/issues/8017)

* Добавьте целевой объект для возврата Фрамеворкреференце, аналогичного Коллектпаккажедовнлоадс и Коллектпаккажереференцес- [#8005](https://github.com/NuGet/Home/issues/8005)

* Кэш HTTP: ресурс Репоситориресаурцес не кэшируется с помощью версии [#7997](https://github.com/NuGet/Home/issues/7997)

* Ведение журнала: исключение стеки вызовов не сообщается с подробным уровнем детализации — [#7955](https://github.com/NuGet/Home/issues/7955)

* Изменение всех URL-адресов документов NuGet для использования HTTPS — [#7950](https://github.com/NuGet/Home/issues/7950)

* Улучшение предупреждающего сообщения NU3024 — [#7933](https://github.com/NuGet/Home/issues/7933)

* блокировка файла не обновляется, когда packagereference удалена — [#7930](https://github.com/NuGet/Home/issues/7930)

* Улучшение обработки вариантов ошибок при проверке элемента licenseurl и License в nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)

* Пользовательский интерфейс PM. Щелкните правой кнопкой мыши заголовок вкладки и выберите пункт "открыть расположение файла", что приведет к ошибке- [#7913](https://github.com/NuGet/Home/issues/7913)

* Подключаемые модули: заносить в журнал, когда завершается процесс подключаемого модуля — [#7907](https://github.com/NuGet/Home/issues/7907)

* Подключаемые модули: высокая частота конфликтов при ведении журнала значений даты и времени — [#7899](https://github.com/NuGet/Home/issues/7899)

* Сбой manifest. ReadFrom в любой nuspec с Лиценсикспрессион- [#7894](https://github.com/NuGet/Home/issues/7894)

* Ресторелоккедмоде: непредвиденный NU1004, когда ProjectReference ссылается на проект с настраиваемым AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889)

* Более эффективное сообщение об ошибке при сбое запуска подключаемого модуля с исключением [#7857](https://github.com/NuGet/Home/issues/7857)

* При выполнении восстановления NoOp Избегайте использования * .dgspec.jsпри записи в каталоге obj — [#7854](https://github.com/NuGet/Home/issues/7854)

* Женератепаспроперти = true: не удается создать свойство при несоответствии регистра — [#7843](https://github.com/NuGet/Home/issues/7843)

* Параметры: недопустимый символ в исходном пути пакета может привести к сбою в VS- [#7820](https://github.com/NuGet/Home/issues/7820)

* Если файл блокировки удален, инструкция RESTORE не создает файл блокировки на NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)

* URL-адрес лицензии и лицензия приводит к ошибке чтения с помощью метаданных [#7547](https://github.com/NuGet/Home/issues/7547)

* Необработанные исключения в V2FeedParser — [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe возвращает нулевой код выхода для недопустимых аргументов — [#7178](https://github.com/NuGet/Home/issues/7178)

* Ошибки обновления и документация по предупреждениям, отражающие сценарии, связанные с подписыванием. [#6498](https://github.com/NuGet/Home/issues/6498)

* Для упрощения перемещения проектов в файле ресурсов следует использовать относительные пути [#4582](https://github.com/NuGet/Home/issues/4582)

**Запросы на изменение структуры**

* Подключаемые модули: Включение ведения журнала диагностики — [#7859](https://github.com/NuGet/Home/issues/7859)

* Создайте карту Tizen 6 на NetStandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[Список всех проблем, исправленных в этом выпуске — 5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
