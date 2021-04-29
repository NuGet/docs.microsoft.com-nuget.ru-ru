---
title: Использование пакетов из веб-каналов, прошедших проверку подлинности
description: Использование пакетов из веб-каналов, прошедших проверку подлинности, во всех сценариях клиента NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901516"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Использование пакетов из веб-каналов, прошедших проверку подлинности

Кроме [общедоступного веб-канала](https://api.nuget.org/v3/index.json) nuget.org клиенты NuGet могут взаимодействовать с веб-каналами файлов и частными веб-каналами HTTP.


Для проверки подлинности с использованием частных веб-каналов HTTP применяются два подхода:

* Добавление учетных данных в [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)
* Проверка подлинности с использованием одной из многих моделей расширяемости в зависимости от применяемого клиента.

## <a name="nuget-clients-authentication-extensibility"></a>Расширяемость проверки подлинности клиентов NuGet

Для различных клиентов NuGet за проверку подлинности отвечает сам поставщик частных веб-каналов.
Все клиенты NuGet имеют методы расширения для поддержки этой возможности. Это либо расширение Visual Studio, либо подключаемый модуль, которые могут взаимодействовать с NuGet для получения учетных данных.

### <a name="visual-studio"></a>Visual Studio

В Visual Studio NuGet предоставляет интерфейс, который поставщики веб-каналов могут реализовывать и предоставлять своим клиентам. Дополнительные сведения см. в документации по [созданию поставщика учетных данных Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Доступные поставщики учетных данных NuGet для Visual Studio

Существует поставщик учетных данных, встроенный в Visual Studio для поддержки Azure DevOps.


Доступные поставщики учетных данных подключаемых модулей:

* [Поставщик учетных данных MyGet для Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Когда средству `nuget.exe` требуются учетные данные для проверки подлинности в веб-канале, оно ищет их следующим образом:

1. Поиск учетных данных в файлах `NuGet.config`.
1. Использование поставщиков учетных данных подключаемых модулей версии 2.
1. Использование поставщиков учетных данных подключаемых модулей версии 1.
1. Затем NuGet запрашивает у пользователя учетные данные в командной строке.

#### <a name="nugetexe-and-v2-credential-providers"></a>Поставщики учетных данных nuget.exe и версии 2

В версии `4.8` NuGet определяет новый механизм подключаемого модуля проверки подлинности, который далее называется поставщиками учетных данных версии 2.
Сведения об установке и обнаружении этих поставщиков см. в разделе [Кроссплатформенные подключаемые модули NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>Поставщики учетных данных nuget.exe и версии 1

В версии `3.3` NuGet представляет первую версию подключаемых модулей проверки подлинности.
Сведения об установке и обнаружении этих поставщиков см. в разделе [Поставщики учетных данных nuget.exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery).

#### <a name="available-credential-providers-for-nugetexe"></a>Доступные поставщики учетных данных для nuget.exe

* [Поставщики учетных данных версии 2 Azure DevOps](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) или [Поставщик учетных данных Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

В Visual Studio 2017 версии 15.9 и более поздней поставщик учетных данных Azure DevOps входит в состав Visual Studio.
Если `nuget.exe` использует MSBuild из этого конкретного набора инструментов Visual Studio, подключаемый модуль будет обнаружен автоматически.

### <a name="dotnetexe"></a>dotnet.exe

Когда средству `dotnet.exe` требуются учетные данные для проверки подлинности в веб-канале, оно ищет их следующим образом:

1. Поиск учетных данных в файлах `NuGet.config`.
1. Использование поставщиков учетных данных подключаемых модулей версии 2.

По умолчанию `dotnet.exe` не является интерактивным, поэтому может потребоваться передать флаг `--interactive`, чтобы обеспечить блокировку для проверки подлинности.

#### <a name="dotnetexe-and-v2-credential-providers"></a>Поставщики учетных данных dotnet.exe и версии 2

В версии `2.2.100` пакета SDK NuGet определяет механизм подключаемого модуля проверки подлинности, который работает во всех клиентах.
Сведения об установке и обнаружении этих поставщиков см. в разделе [Кроссплатформенные подключаемые модули NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Доступные поставщики учетных данных для dotnet.exe

* [Поставщик учетных данных Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

Когда средству `MSBuild.exe` требуются учетные данные для проверки подлинности в веб-канале, оно ищет их следующим образом:

1. Поиск учетных данных в файлах `NuGet.config`.
1. Использование поставщиков учетных данных подключаемых модулей версии 2.

По умолчанию `MSBuild.exe` не является интерактивным, поэтому может потребоваться задать свойство `/p:NuGetInteractive=true`, чтобы обеспечить блокировку для проверки подлинности.

#### <a name="msbuildexe-and-v2-credential-providers"></a>Поставщики учетных данных MSBuild.exe и версии 2

В Visual Studio 2019 с обновлением 9 NuGet определяет механизм подключаемого модуля проверки подлинности, который работает во всех клиентах.
Сведения об установке и обнаружении этих поставщиков см. в разделе [Кроссплатформенные подключаемые модули NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Доступные поставщики учетных данных для MSBuild.exe

* [Поставщик учетных данных Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

В Visual Studio 2017 с обновлением 9 и более поздней поставщик учетных данных Azure DevOps входит в состав Visual Studio. Дополнительные действия не требуются.
