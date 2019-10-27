---
title: Заметки о выпуске NuGet 5,3
description: Заметки о выпуске NuGet 5,3, включая новые функции, исправления ошибок и DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 994a0da3728e05a09b5537d150f2203477922efc
ms.sourcegitcommit: 904cbee57770af04efcae0b3709301685475bf64
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/26/2019
ms.locfileid: "72962295"
---
# <a name="nuget-53-release-notes"></a>Заметки о выпуске NuGet 5,3

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio| Доступно в пакетах SDK для .NET|
|:---|:---|:---|
| [**5.3.0**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16,3](https://visualstudio.microsoft.com/downloads/) | [3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |
| [**5.3.1**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16.3.6](https://visualstudio.microsoft.com/downloads/) | [Будущая версия: 3.0.101](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core

## <a name="summary-whats-new-in-53"></a>Сводка: новые возможности в 5,3

* [Значок пакета можно встроить в пакет](../reference/msbuild-targets.md#packing-an-icon-image-file), вместо того чтобы использовать внешний URL-адрес. - [#352](https://github.com/NuGet/Home/issues/352)

* Улучшенная безопасность с помощью отслеживания и применения SHA для Packages. config — [#7281](https://github.com/NuGet/Home/issues/7281)

* Включение устаревания устаревших или устаревших пакетов NuGet [#2867](https://github.com/NuGet/Home/issues/2867) | записи [блога](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [документы](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Ошибки**

* Пакеты NuGet, созданные с помощью пакета SDK 3.0.100-preview9, не могут использоваться пользователями пакета SDK 2,2... в зависимости от часового пояса [#8603](https://github.com/NuGet/Home/issues/8603)

* Кавычки "символы в пути приводят к ошибке" недопустимых символов в пути "в `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)

* VS: сборки полностью являются NGen-ED, а не частично NGen-ED- [#8513](https://github.com/NuGet/Home/issues/8513)

* Уменьшение использования памяти (Отмена подписки на события) — [#8471](https://github.com/NuGet/Home/issues/8471)

* Сообщение "Error_UnableToFindProjectInfo" не является правильным грамматически — [#8441](https://github.com/NuGet/Home/issues/8441)

* Улучшения NU1403 — проверка всех пакетов, включение ожидаемых/фактических значений SHA — [#8424](https://github.com/NuGet/Home/issues/8424)

* Множественное перечисление в `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)

* Отмена изменений "Public-> internal" в Плугинпроцесс- [#8390](https://github.com/NuGet/Home/issues/8390)

* Ивспаккажесаурцепровидер.-источники (...) имеют неверно определенное поведение исключений — [#8383](https://github.com/NuGet/Home/issues/8383)

* Снова сделать конструктор Плугинманажер открытым — [#8379](https://github.com/NuGet/Home/issues/8379)

* Метрики для контроля частоты обновления пользовательского интерфейса PM — [#8369](https://github.com/NuGet/Home/issues/8369)

* Уменьшение числа обновлений пользовательского интерфейса при установке с помощью пользовательского интерфейса диспетчера пакетов — [#8358](https://github.com/NuGet/Home/issues/8358)

* Данные телеметрии: значения DateTime используют форматы, зависящие от языка и региональных параметров. [#8351](https://github.com/NuGet/Home/issues/8351)

* Сокращение числа обновлений пользовательского интерфейса на вкладке Обзор в пользовательском интерфейсе диспетчера пакетов #6570 — [#8339](https://github.com/NuGet/Home/issues/8339)

* [Сбой теста] "Не удалось проанализировать файл конфигурации" будет предложено дважды [#8320](https://github.com/NuGet/Home/issues/8320)

* Порождение ошибки NU5037 на странице с хорошим документом, в которой объясняются исправления клиентов (в пакете отсутствует необходимый файл nuspec) — [#8291](https://github.com/NuGet/Home/issues/8291)

* Не удается выполнить восстановление в заблокированном режиме при изменении Рунтимеидентифиер проекта — [#8260](https://github.com/NuGet/Home/issues/8260)

* Сделайте чтение параметров в VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)

* Регрессия в `Nuget sources add` приводит к тому, что символ ":", шестнадцатеричное значение 0x3A, не может включаться в имя "Errors- [#7948](https://github.com/NuGet/Home/issues/7948)

* Поставщики учетных данных подключаемого модуля NuGet — скрытие окна процесса — [#7511](https://github.com/NuGet/Home/issues/7511)

* Принудительное применение Паккажепасресолвер является абсолютным путем [#7349](https://github.com/NuGet/Home/issues/7349)

* Сокращение числа обновлений пользовательского интерфейса на вкладках Установка и обновление пользовательского интерфейса диспетчера пакетов — [#6570](https://github.com/NuGet/Home/issues/6570)

**Запрос на изменение структуры:**

* Обновление платформ Xamarin для соотнесения с NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)

* Включить копирование содержимого окна предварительного просмотра диспетчера пакетов для установки или обновления — [#8324](https://github.com/NuGet/Home/issues/8324)

* Включение восстановления в proj-файлах — [#8212](https://github.com/NuGet/Home/issues/8212)

* Познакомьтесь с `NUGET_NETFX_PLUGIN_PATHS` и `NUGET_NETCORE_PLUGIN_PATHS` для поддержки конфигурации обоих элементов [#8151](https://github.com/NuGet/Home/issues/8151)

* Включение нескольких версий для Паккажедовнлоад с помощью атрибута версии — [#8074](https://github.com/NuGet/Home/issues/8074)

* Добавление параметров-Солутиондиректори и-Паккажедиректори в NuGet. exe Pack — [#7163](https://github.com/NuGet/Home/issues/7163)

**[Список всех проблем, исправленных в этом выпуске — 5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**

## <a name="summary-whats-new-in-531"></a>Сводка. новые возможности в 5.3.1

* Подключаемый модуль: задача отменена — не дотронет отмены, влияющие на создание экземпляра подключаемого модуля — [#8648](https://github.com/NuGet/Home/issues/8648)

* Задача восстановления не может быть безопасно запущена дважды в одном процессе (при использовании поставщиков учетных данных). [#8688](https://github.com/NuGet/Home/issues/8688)
