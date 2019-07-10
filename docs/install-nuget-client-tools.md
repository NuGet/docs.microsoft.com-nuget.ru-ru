---
title: Установка клиентских средств NuGet
description: Рекомендации по установке клиентских средств, интерфейса командной строки (CLI) dotnet и nuget, а также диспетчера пакетов для Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 6e3011493b7b89bc43cd9a267aea7fd32d668cec
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426561"
---
# <a name="install-nuget-client-tools"></a>Установка клиентских средств NuGet

> **Хотите установить пакет? Ознакомьтесь со [способами установки пакетов NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Чтобы работать с NuGet в качестве потребителя или создателя пакета, вы можете использовать средства интерфейса командной строки (CLI) и функции NuGet в Visual Studio. В этой статье кратко описываются возможности различных средств, их установка и приведена сравнительная таблица [доступности функций](#feature-availability). Сведения о начале использования пакетов с помощью NuGet см. в разделах [Установка и использование пакета (.NET CLI)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) и [Установка и использование пакета (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Чтобы приступить к созданию пакетов NuGet, см. разделы [Создание и публикация пакета NET Standard (dotnet CLI)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) и [Создание и публикация пакета NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Средство&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | ОПИСАНИЕ | Скачать&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Средство CLI для библиотек .NET Core и .NET Standard, а также для любых проектов в стиле пакета SDK, нацеленных на .NET Framework (см. раздел [Атрибут SDK](/dotnet/core/tools/csproj#additions)). Входит в состав пакета SDK для .NET Core и обеспечивает основные функции NuGet на всех платформах. | [Пакет SDK для .NET Core](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Средство CLI для библиотек .NET Framework и проектов со стилем, отличным от пакета SDK, нацеленных на библиотеки .NET Standard. Обеспечивает все функциональные возможности NuGet в Windows и большинство функций, выполняемых в рамках проекта Mono на компьютере Mac и Linux. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | В Windows предоставляет возможности NuGet через пользовательский интерфейс и консоль диспетчера пакетов. Прилагается к рабочим нагрузкам, связанным с .NET. На компьютере Mac предоставляет определенные возможности через пользовательский интерфейс. В Visual Studio Code функции NuGet предоставляются через расширения. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[MSBuild CLI](reference/msbuild-targets.md) также предоставляет возможности восстановления и создания пакетов, которые применяются на серверах сборки. MSBuild не является универсальным средством для работы с NuGet.

## <a name="cli-tools"></a>Средства CLI

Два средства CLI для NuGet — `dotnet.exe` и `nuget.exe`. См. сравнительную таблицу [доступности функций](#feature-availability).

* Для нацеливания на .NET Core или .NET Standard используйте CLI для .NET. CLI для .NET является обязательным для проекта с форматом в стиле пакета SDK, использующего [атрибут SDK](/dotnet/core/tools/csproj#additions).
* Для нацеливания на .NET Framework (только проекты со стилем, отличным от пакета SDK) используйте `nuget.exe CLI`. При переносе проекта в `packages.config` используйте CLI dotnet.

### <a name="dotnetexe-cli"></a>Интерфейс командной строки dotnet.exe

Интерфейс командной строки .NET Core 2.0, `dotnet.exe`, работает на всех платформах (Windows, Mac и Linux) и предоставляет такие возможности NuGet, как установка, восстановление и публикация пакетов. `dotnet` обеспечивает прямую интеграцию с файлами проекта .NET Core (например, `.csproj`), что полезно в большинстве сценариев. `dotnet` также создается непосредственно для каждой платформы и не требует установки Mono.

Установка:

- на компьютерах разработчиков установите [пакет SDK для .NET Core](https://aka.ms/dotnetcoregs);
- для серверов сборки следуйте инструкциям в статье [Использование пакета SDK и средств .NET Core при непрерывной интеграции (CI)](/dotnet/core/tools/using-ci-with-cli).

Сведения об использовании основных команд с CLI dotnet см. в статье [Установка и использование пакета с помощью CLI dotnet](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>Интерфейс командной строки nuget.exe

Интерфейс командной строки `nuget.exe` (`nuget.exe`) — это программа командной строки для Windows, которая предоставляет все возможности NuGet. С некоторыми ограничениями ее также можно запустить на Mac OSX и Linux с помощью [Mono](http://www.mono-project.com/docs/getting-started/install/).

Установка:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Вы можете обновить существующий nuget.exe до последней версии с помощью команды `nuget update -self` в Windows.

Сведения об использовании основных команд с CLI `nuget.exe` см. в статье [Установка и использование пакета с помощью CLI nuget.exe](consume-packages/install-use-packages-nuget-cli.md).

> [!Note]
> Последняя рекомендуемая версия интерфейса командной строки NuGet всегда доступна по адресу `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Чтобы обеспечить совместимость со старыми системами непрерывной интеграции, сейчас можно скачать [средство CLI 2.8.6](https://github.com/NuGet/NuGetGallery/issues/5381) по URL-адресу `https://nuget.org/nuget.exe`.

## <a name="visual-studio"></a>Visual Studio

- В Visual Studio Code: для получения возможностей NuGet можно использовать расширения Marketplace либо средства CLI `dotnet.exe` или `nuget.exe`.

- В Visual Studio для Mac: некоторые возможности NuGet встроены напрямую. Пошаговое руководство см. в разделе [Включение пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough). Для других возможностей используются средства CLI `dotnet.exe` или `nuget.exe`.

- В Visual Studio для Windows: **диспетчер пакетов NuGet** включен в Visual Studio 2012 и более поздние версии. Visual Studio предоставляет [пользовательский интерфейс](tools/package-manager-ui.md) и [консоль](tools/package-manager-console.md) диспетчера пакетов, через которые можно выполнять большинство операций NuGet.
  - Начиная с версии Visual Studio 2017, установщик содержит диспетчер пакетов NuGet с любой рабочей нагрузкой, использующей .NET. Чтобы проверить, установлен ли диспетчер пакетов, или установить его отдельно, запустите установщик Visual Studio и установите флажок **Отдельные компоненты > Средства для работы с кодом > Диспетчер пакетов NuGet**.
  - Пользовательский интерфейс и консоль диспетчера пакетов уникальны в Visual Studio для Windows. Сейчас они недоступны в Visual Studio для Mac.
  - Средство CLI является обязательным для поддержки функции NuGet в интегрированной среде разработки. Можно использовать средство CLI `dotnet` или `nuget.exe`. Средство CLI `dotnet` устанавливается вместе с некоторыми рабочими нагрузками Visual Studio, например .NET Core. Средство CLI `nuget.exe` нужно установить отдельно, как описано выше.
  - Команды консоли диспетчера пакетов работают только в Visual Studio для Windows, но не в других средах PowerShell.
  - Для Visual Studio 2010 и более ранних версий установите расширение "Диспетчер пакетов NuGet для Visual Studio".
  - Расширения NuGet для Visual Studio 2013 и 2015 можно скачать по адресу [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
  - Если вы хотите заранее оценить предстоящие возможности NuGet, установите предварительную версию [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), которая работает параллельно со стабильными выпусками Visual Studio. Чтобы сообщить о проблемах или обменяться идеями о предварительных версиях, откройте обращение в [репозитории NuGet GitHub](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Доступность функций

| Функция | CLI dotnet | CLI nuget (Windows) | CLI nuget (Mono) | Visual Studio (Windows) | Visual Studio для Mac |
| --- | --- | --- | --- | --- | --- |
| Поиск пакетов |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Установка или удаление пакетов | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Обновление пакетов | &#10004; | &#10004; | | &#10004; | &#10004; |
| Восстановление пакетов | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Управление веб-каналами пакета (источниками) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Управление пакетами в веб-канале | &#10004; | &#10004; | &#10004; | | |
| Установка ключей API для веб-каналов | | &#10004; | &#10004; | | |
| Создание пакетов (3) | &#10004; | &#10004; | &#10004; (4) | &#10004; | |
| Публикация пакетов | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Репликация пакетов |  | &#10004; | &#10004; | | |
| Управление папками *global-package* и кэша | &#10004; | &#10004; | &#10004; | | |
| Управление конфигурацией NuGet | | &#10004; | &#10004; | | |

(1) Не влияет на файлы проекта. Используйте `dotnet.exe`.

(2) Работает только с файлом `packages.config`, а не с файлами решения (`.sln`).

(3) Различные дополнительные функции пакетов доступны через CLI, только если они не представлены в средствах пользовательского интерфейса Visual Studio.

(4) Работает с файлами `.nuspec`, но не с файлами проекта.

### <a name="related-topics"></a>См. также

- [Установка пакетов и управление ими с использованием Visual Studio](tools/package-manager-ui.md)
- [Установка пакетов и управление ими с использованием PowerShell](tools/package-manager-console.md)
- [Установка пакетов и управление ими с использованием CLI dotnet](consume-packages/install-use-packages-dotnet-cli.md)
- [Установка пакетов и управление ими с использованием CLI nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
- [Справочник по PowerShell для консоли диспетчера пакетов](tools/powershell-reference.md)
- [Создание пакета](create-packages/creating-a-package.md)
- [Публикация пакета](nuget-org/publish-a-package.md)

Разработчики, работающие в Windows, также могут рассмотреть [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), автономное средство с открытым исходным кодом, позволяющее визуально изучать, создавать и изменять пакеты NuGet. Это очень удобно, например, для внесения экспериментальных изменений в структуру пакета без необходимости его перестроения.
