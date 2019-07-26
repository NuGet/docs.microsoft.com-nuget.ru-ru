---
title: Заметки о выпуске NuGet 5,2 RTM
description: Заметки о выпуске NuGet 5,2, включая новые функции, исправления ошибок и DCR.
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471187"
---
# <a name="nuget-52-release-notes"></a>Заметки о выпуске NuGet 5,2

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio| Доступно в пакетах SDK для .NET|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16,2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1) <sup>1</sup>, [2.2.40 X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core 

<sup>2</sup> Доступно в качестве необязательной установки с помощью Visual Studio 2019 с рабочей нагрузкой .NET Core

## <a name="summary-whats-new-in-52"></a>Сводка: Новые возможности в 5,2

* Исправлена критическая ошибка, которая привела к случайным сбоям операций NuGet из-за проблем с путями в Linux & Mac- [#7341](https://github.com/NuGet/Home/issues/7341)

* Улучшена скорость реагирования пользовательского интерфейса при просмотре пакетов с помощью пользовательского интерфейса диспетчера пакетов NuGet в Visual Studio, особенно заметных для снижения производительности источников. [#8039](https://github.com/NuGet/Home/issues/8039)

* Многочисленные исправления надежности для файла блокировки ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) и подключаемого модуля проверки подлинности ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Ошибки**

* Счетчик Консоль диспетчера пакетов:  Время задержки пользовательского интерфейса при обновлении "проекта по умолчанию" выбрано значение — [#8235](https://github.com/NuGet/Home/issues/8235)

* Счетчик Улучшения производительности в пользовательском интерфейсе PM — [#8039](https://github.com/NuGet/Home/issues/8039)

* Счетчик Задержка пользовательского интерфейса при чтении проекта по умолчанию в PMC- [#6824](https://github.com/NuGet/Home/issues/6824)

* Perf: [vsfeedback] вкладка обновления NuGet зависает для локального источника пакетов — [#6470](https://github.com/NuGet/Home/issues/6470)

* Подключаемые модули  NuGet ожидает время ожидания полного подтверждения, если подключаемому модулю не удается запуститься или прекращается раннее [#8300](https://github.com/NuGet/Home/issues/8300)

* Подключаемые модули. Улучшенная диагностика сбоя при запуске подключаемого модуля — [#8271](https://github.com/NuGet/Home/issues/8271)

* Подключаемые модули Ошибка при обнаружении NuGet. exe встроенных подключаемых модулей — [#8269](https://github.com/NuGet/Home/issues/8269)

* Подключаемые модули: файл кэша никогда не читается — [#8210](https://github.com/NuGet/Home/issues/8210)

* Подключаемые модули  "Задача была отменена". ошибки с подключаемым модулем проверки подлинности во время восстановления [#8198](https://github.com/NuGet/Home/issues/8198)

* Кэш подключаемых модулей не удается обнаружить периодически на платформах Linux — [#7845](https://github.com/NuGet/Home/issues/7845)

* Локкфиле: с ATF имеет значение false NU1004 из-за неправильной проверки на равенство целевой платформы — [#8187](https://github.com/NuGet/Home/issues/8187)

* Локкфиле: флаг восстановления "--заблокирован-Mode" не учитывается, если файл блокировки пуст или имеет неправильный формат [#8160](https://github.com/NuGet/Home/issues/8160)

* Локкфиле: Не делать строчные и пользовательские имена сборок в пакетах заблокировать файл — [#8114](https://github.com/NuGet/Home/issues/8114)

* Локкфиле: Сделать ссылку на проект в нижнем регистре в файле блокировки [#7840](https://github.com/NuGet/Home/issues/7840)

* Восстановление: Установка поддельного подписанного пакета приводит к неудачной попытке установки (с повторяющимися выходными данными). [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: не удается выполнить десериализацию пользовательских параметров решения после обновления NuGet [#8166](https://github.com/NuGet/Home/issues/8166)

* DotNet-List-Package в проекте UnitTest возвращает ошибку — [#8154](https://github.com/NuGet/Home/issues/8154)

* Создание группы пакетов NuGet для установщика VS — устранение некоторых проблем с установкой VSIX — [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild не должен устанавливать параметр "Build". - [#7801](https://github.com/NuGet/Home/issues/7801)

* Новый параметр "-Симболпаккажеформат снупкг" создает ошибку, если файл nuspec содержит явный элемент ссылки на сборку — [#7638](https://github.com/NuGet/Home/issues/7638)

* NuGet. targets (498, 5): ошибка: Не удалось найти часть пути "/ТМП/нужетскратч- [#7341](https://github.com/NuGet/Home/issues/7341)

**Запрос на изменение структуры:**

* Добавьте свойство MSBuild, которое указывает, что Паккажедовнлоад поддерживается — [#8106](https://github.com/NuGet/Home/issues/8106)

* Фрамеворкреференце подавлять поток зависимостей с помощью Фрамеворкреференце. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* Механизм для предоставления Runtime. JSON вне пакета — [#7351](https://github.com/NuGet/Home/issues/7351)

**[Список всех проблем, исправленных в этом выпуске — 5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


