---
title: "Установка клиентских средств NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Рекомендации по установке клиентских средств, интерфейса командной строки (CLI) dotnet и nuget, а также диспетчера пакетов для Visual Studio."
keywords: "интерфейс командной строки dotnet.exe, клиентские средства NuGet, диспетчер пакетов NuGet, консоль диспетчера пакетов NuGet, NuGet для Visual Studio, бета-канал NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 462557e939e769f26fe05d6f9e2994eaf43c6e11
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/08/2018
---
# <a name="installing-nuget-client-tools"></a>Установка клиентских средств NuGet

> **Хотите установить пакет? Ознакомьтесь со [способами установки пакетов NuGet](consume-packages/ways-to-install-a-package.md).**

Для работы с NuGet в качестве потребителя или создателя пакета можно использовать [средства кроссплатформенного интерфейса командной строки (CLI)](#cli-tools) и [функции NuGet в Visual Studio](#visual-studio). В этой статье кратко описываются возможности различных средств, их установка и приведена сравнительная таблица [доступности функций](#feature-availability).

| Средство&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Описание: | Скачать&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Входит в состав пакета SDK для .NET Core и обеспечивает основные функции NuGet на всех платформах. | [Пакет SDK для .NET Core](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Обеспечивает все функциональные возможности NuGet в Windows и большинство функций, выполняемых в рамках проекта [Mono](http://www.mono-project.com/docs/getting-started/install/) на Mac и Linux. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Предоставляет возможности NuGet через пользовательский интерфейс и консоль диспетчера пакетов. Прилагается к рабочим нагрузкам, связанным с .NET. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

[MSBuild CLI](reference/msbuild-targets.md) также предоставляет возможности восстановления и создания пакетов, которые применяются на серверах сборки. MSBuild не является универсальным средством для работы с NuGet.

## <a name="cli-tools"></a>Средства CLI

Два средства CLI для NuGet — `dotnet.exe` и `nuget.exe`. См. сравнительную таблицу [доступности функций](#feature-availability).

### <a name="dotnetexe-cli"></a>Интерфейс командной строки dotnet.exe

Интерфейс командной строки .NET Core 2.0, `dotnet.exe`, работает на всех платформах (Windows, Mac и Linux) и предоставляет такие возможности NuGet, как установка, восстановление и публикация пакетов. dotnet обеспечивает прямую интеграцию с файлами проекта .NET Core (например, `.csproj`), что полезно в большинстве сценариев. `dotnet` также создается непосредственно для каждой платформы и не требует установки Mono.

Установка:

- на компьютерах разработчиков установите [пакет SDK для .NET Core](https://aka.ms/dotnetcoregs);
- для серверов сборки следуйте инструкциям в статье [Использование пакета SDK и средств .NET Core при непрерывной интеграции (CI)](/dotnet/core/tools/using-ci-with-cli).

Дополнительные сведения см. в разделе [Команды CLI](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x)

### <a name="nugetexe-cli"></a>Интерфейс командной строки nuget.exe

Интерфейс командной строки NuGet, `nuget.exe`, — это программа командной строки для Windows, которая предоставляет все возможности NuGet. С некоторыми ограничениями ее также можно запустить на Mac OSX и Linux с помощью Mono. В отличие от `dotnet`, CLI `nuget.exe` не влияет на файлы проекта.

Установка:

[!INCLUDE[install-cli](includes/install-cli.md)]

> [!Tip]
> Вы можете обновить существующий nuget.exe до последней версии с помощью команды `nuget update -self`.

> [!Note]
> Последняя рекомендуемая версия интерфейса командной строки NuGet всегда доступна по адресу `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Для обеспечения совместимости со старыми системами непрерывной интеграции сейчас можно скачать средство CLI 2.8.6 по URL-адресу `https://nuget.org/nuget.exe`. [Этот адрес больше не поддерживается](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- В Visual Studio Code: для получения возможностей NuGet можно использовать расширения marketplace или средства CLI `dotnet.exe` или `nuget.exe`.
- В Visual Studio для Mac: некоторые возможности NuGet встроены напрямую. Пошаговое руководство см. в разделе [Включение пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough). Для других возможностей используются средства CLI `dotnet.exe` или `nuget.exe`.

- В Visual Studio для Windows: **диспетчер пакетов NuGet** включен в выпуски Visual Studio 2012 и более поздние версии. Диспетчер пакетов предоставляет [пользовательский интерфейс](tools/package-manager-ui.md) и [консоль](tools/package-manager-console.md), через которые можно выполнять большинство операций NuGet.
  - Установщик Visual Studio 2017 содержит диспетчер пакетов NuGet с любой рабочей нагрузкой, использующей .NET. Чтобы проверить, установлен ли диспетчер пакетов, или установить его отдельно, запустите установщик Visual Studio 2017 и установите флажок **Отдельные компоненты > Средства для работы с кодом > Диспетчер пакетов NuGet**.
  - Пользовательский интерфейс и консоль диспетчера пакетов уникальны в Visual Studio для Windows. В настоящее время они недоступны в Visual Studio для Mac.
  - В Visual Studio нет CLI `nuget.exe` по умолчанию. Его нужно установить отдельно, как описано выше.
  - Команды консоли диспетчера пакетов работают только в Visual Studio для Windows, но не в других средах PowerShell.
  - Для Visual Studio 2010 и более ранних версий установите расширение "Диспетчер пакетов NuGet для Visual Studio".
  - Расширения NuGet для Visual Studio 2013 и 2015 можно скачать по адресу [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
  - Если вы хотите заранее оценить предстоящие возможности NuGet, установите предварительную версию [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), которая работает параллельно со стабильными выпусками Visual Studio. Чтобы сообщить о проблемах или обменяться идеями о предварительных версиях, откройте обращение в [репозитории NuGet GitHub](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Доступность функций

| Функция | CLI dotnet | CLI nuget (Windows) | CLI nuget (Mono) | Visual Studio (Windows) | Visual Studio для Mac |
| --- | --- | --- | --- | --- | --- |
| Поиск пакетов |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Установка или удаление пакетов | &#10004;(1) | &#10004;(2) | &#10004; | &#10004; | &#10004; |
| Обновление пакетов | &#10004; | &#10004; | | &#10004; | &#10004; |
| Восстановление пакетов | &#10004; | &#10004; | &#10004;(3) | &#10004; | &#10004; |
| Управление веб-каналами пакета (источниками) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Управление пакетами в веб-канале | &#10004;(1) | &#10004; | &#10004; | | |
| Установка ключей API для веб-каналов | | &#10004; | &#10004; | | |
| Создание пакетов (4) | &#10004; | &#10004; | &#10004;(5) | &#10004; | |
| Публикация пакетов | &#10004;(1) | &#10004; | &#10004; | &#10004; |  |
| Репликация пакетов |  | &#10004; | &#10004; | | |
| Управление кэшем NuGet | &#10004; | &#10004; | &#10004; | | |
| Управление конфигурацией NuGet | | &#10004; | &#10004; | | |

(1) Только пакеты на сайте nuget.org.

(2) Не влияет на файлы проекта. Используйте `dotnet.exe`.

(3) Работает только с файлом `packages.config`, а не с файлами решения (`.sln`).

(4) Различные дополнительные возможности пакетов доступны через CLI только в том случае, если они не представлены в средствах пользовательского интерфейса Visual Studio.

(5) Работает с файлами `.nuspec`, но не с файлами проекта.

### <a name="related-topics"></a>См. также

- [Команды dotnet](tools/dotnet-commands.md)
- [Справочник по интерфейсу командной строки NuGet](tools/nuget-exe-cli-reference.md)
- [Справочник по пользовательскому интерфейсу диспетчера пакетов](tools/package-manager-ui.md)
- [Справочник по консоли диспетчера пакетов](tools/package-manager-console.md)
- [Справочник по PowerShell для консоли диспетчера пакетов](tools/powershell-reference.md)
- [Создание пакета](create-packages/creating-a-package.md)
- [Публикация пакета](create-packages/publish-a-package.md)

Разработчики, работающие в Windows, также могут рассмотреть [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), автономное средство с открытым исходным кодом, позволяющее визуально изучать, создавать и изменять пакеты NuGet. Это очень удобно, например, для внесения экспериментальных изменений в структуру пакета без необходимости его перестроения.
