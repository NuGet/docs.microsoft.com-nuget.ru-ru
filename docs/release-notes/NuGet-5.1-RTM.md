---
title: Заметки о выпуске NuGet 5.1 RTM
description: Заметки о выпуске для NuGet 5.1, включая новые возможности, исправления ошибок и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842580"
---
# <a name="nuget-51-release-notes"></a>Заметки о выпуске 5.1 NuGet

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio| Доступно в пакетах SDK для .NET|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16.1](https://visualstudio.microsoft.com/downloads/) | [2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core 

<sup>2</sup>доступно в виде необязательно установку с помощью Visual Studio 2019 с рабочей нагрузкой .NET Core

## <a name="summary-whats-new-in-51"></a>Сводка: Новые возможности в версии 5.1

* Поддержка для пропуска отправка пакета, если он уже существует для обеспечения более эффективную интеграцию с Непрерывной интеграции и рабочие процессы — [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio предоставляет удобную ссылку на страницу коллекции nuget.org пакета - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Поддержка новых средств .NET Core 3.0, таких как [целевые пакеты](https://github.com/dotnet/cli/issues/10006) и [пакеты среды выполнения](https://github.com/dotnet/cli/issues/10007)
  * Pack и restore NuGet поддержка FrameworkReferences для включения целевая и среды выполнения ссылки на пакет - [#7342](https://github.com/NuGet/Home/issues/7342)
  * «Скачать только» пакет сценарию поддержки с PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)
  * Среда выполнения Exlcude и целевые пакеты в результатах поиска и восстановления граф с использованием PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Ошибки**

* Подключаемые модули: сведения об исключении потеряны во время создания подключаемого модуля - [#8057](https://github.com/NuGet/Home/issues/8057)

* Диапазон PackageReference с эксклюзивные нижняя граница не работает, если нижняя граница присутствует на один из источников. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Улучшить сообщение IsPackableFalseError - [#8021](https://github.com/NuGet/Home/issues/8021)

* Блокировка файла - файле повторное создание блокировки при изменении схемы проекта — [#8019](https://github.com/NuGet/Home/issues/8019)

* Ошибка ProjectSystem: Удалено пакетов NuGet, получение auto - [#8017](https://github.com/NuGet/Home/issues/8017)

* Добавить целевой объект для возвращения FrameworkReference аналогичную CollectPackageDownloads и CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)

* Кэш HTTP:  RepositoryResources ресурсов не кэшируется с версиями образом - [#7997](https://github.com/NuGet/Home/issues/7997)

* Ведение журнала: исключение стеки вызовов, не передаются с подробным уровнем детализации - [#7955](https://github.com/NuGet/Home/issues/7955)

* Изменить все NuGet документация URL-адреса для использования протокола HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)

* Улучшить NU3024 предупреждающее сообщение - [#7933](https://github.com/NuGet/Home/issues/7933)

* Файл блокировки не обновляется при packagereference removed — [#7930](https://github.com/NuGet/Home/issues/7930)

* Улучшения вариантов обработки ошибок при проверке элемента licenseurl и лицензии в nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)

* Пользовательского интерфейса PM - щелкните правой кнопкой мыши заголовок вкладки и выберите команду «Открыть расположение файла» приведет к ошибке - [#7913](https://github.com/NuGet/Home/issues/7913)

* Подключаемые модули: журнал при завершении работы подключаемого модуля процесса - [#7907](https://github.com/NuGet/Home/issues/7907)

* Подключаемые модули: частота высокой конфликтов в значения даты и времени для ведения журнала - [#7899](https://github.com/NuGet/Home/issues/7899)

* Manifest.ReadFrom завершается сбоем в любой nuspec с LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: Непредвиденная NU1004 при ProjectReference ссылается на проект с помощью пользовательских AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)

* Улучшенное сообщение об ошибке при сбое запуска подключаемого модуля с исключением - [#7857](https://github.com/NuGet/Home/issues/7857)

* При выполнении восстановления NoOp, избегайте использования *. dgspec.json записи в каталоге obj - [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true не удается создать свойство на несоответствие регистра - [#7843](https://github.com/NuGet/Home/issues/7843)

* Параметры: недопустимый символ в исходный путь к пакету могут вызвать сбой VS - [#7820](https://github.com/NuGet/Home/issues/7820)

* Если удаляется файл блокировки, восстановление не создает файл блокировки на NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)

* URL-адрес лицензии и лицензии причины, ошибка с метаданными - чтения [#7547](https://github.com/NuGet/Home/issues/7547)

* Необработанные исключения в V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)

* NuGet.exe возвращает нулевой код выхода для недопустимые аргументы - [#7178](https://github.com/NuGet/Home/issues/7178)

* Обновление ошибки и предупреждение документация, в соответствии с подписи связанные сценарии - [#6498](https://github.com/NuGet/Home/issues/6498)

* Файл ресурсов следует использовать относительные пути для включения более легко - проектами [#4582](https://github.com/NuGet/Home/issues/4582)

**Запросы на изменение структуры**

* Подключаемые модули: включить ведение журнала диагностики - [#7859](https://github.com/NuGet/Home/issues/7859)

* Создание Tizen 6 сопоставляются NetStandard 2.1 — [#7773](https://github.com/NuGet/Home/issues/7773)

**[Список всех проблем, исправленных в этом выпуске — 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
