---
title: Поставщики учетных данных NuGet для Visual Studio
description: Поставщики учетных данных NuGet пройти проверку подлинности с веб-каналами путем реализации интерфейса IVsCredentialProvider в расширении Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: abe009fee5863c55a188f4d7c71ed0924dd067ff
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547958"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Проверка подлинности веб-каналов в Visual Studio с помощью поставщиков учетных данных NuGet

Расширение NuGet Visual Studio 3.6 + поддерживает поставщиков учетных данных, которые позволяют NuGet для работы с каналы с проверкой подлинности.
После установки поставщика учетных данных NuGet для Visual Studio, расширение NuGet для Visual Studio автоматически получать и обновлять учетные данные для каналы с проверкой подлинности при необходимости.

Пример реализации можно найти в [пример VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Начиная с 4.8 + NuGet в Visual Studio поддерживает новый кроссплатформенный проверки подлинности подключаемые модули также, но они не рекомендуемый подход для повышения производительности.

> [!Note]
> Поставщики учетных данных NuGet для Visual Studio должен быть установлен как регулярное расширение Visual Studio и потребует [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) или более поздней версии.
>
> Поставщики учетных данных NuGet для Visual Studio работает только в Visual Studio (не в команда dotnet restore или nuget.exe). Поставщики учетных данных с помощью nuget.exe, см. в разделе [поставщиков учетных данных nuget.exe](nuget-exe-Credential-providers.md).
> Учетные данные поставщиков в dotnet и msbuild см. в разделе [NuGet кросс-подключаемые модули платформы](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Доступные поставщики учетных данных NuGet для Visual Studio

Нет поставщика учетных данных, встроенные в расширение Visual Studio NuGet поддерживает Visual Studio Team Services.

Расширение NuGet Visual Studio использует внутренний `VsCredentialProviderImporter` которой также начинает проверку поставщики подключаемый модуль учетных данных. Эти поставщики подключаемый модуль учетных данных должны быть обнаруживаемыми как Экспорт MEF типа `IVsCredentialProvider`.

Поставщики доступных подключаемый модуль учетных данных:

- [Поставщик учетных данных MyGet для Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Создание поставщика учетных данных NuGet для Visual Studio

Расширение NuGet Visual Studio 3.6 + реализует внутренний CredentialService, который используется для получения учетных данных. CredentialService имеет список встроенных и подключаемый модуль учетных данных поставщиков. Каждый поставщик применяется последовательно, пока не полученные учетные данные.

При приобретении учетных данных учетных данных служба попробует поставщиков учетных данных в следующем порядке, остановка, как только полученные учетные данные:

1. Учетные данные будут получены из файлов конфигурации NuGet (с помощью встроенной `SettingsCredentialProvider`).
1. Если источник пакета в Visual Studio Team Services, `VisualStudioAccountProvider` будет использоваться.
1. Все другие подключаемый модуль Visual Studio поставщики учетных данных будет выполнена последовательно.
1. Попробуйте использовать все NuGet кросс-поставщики учетных данных платформы последовательно.
1. Если учетные данные не получены, пользователю предлагается ввести учетные данные, используя диалоговое окно стандартных обычной проверки подлинности.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Реализация IVsCredentialProvider.GetCredentialsAsync

Чтобы создать поставщик удостоверений NuGet для Visual Studio, создать расширение Visual Studio, предоставляющий открытый MEF-Экспорт реализация `IVsCredentialProvider` введите и соответствуют принципам, описанным ниже.

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

Пример реализации можно найти в [пример VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Каждый поставщик учетных данных NuGet для Visual Studio необходимо:

1. Определите, может ли его предоставлять учетные данные для целевого URI перед запуском получение учетных данных. Если поставщик не может предоставить учетные данные для источника, то он должен вернуть `null`.
1. Если поставщик обрабатывать запросы для целевой URI, но не может предоставить учетные данные, должно вызываться исключение.

Необходимо реализовать пользовательский поставщик учетных данных NuGet для Visual Studio `IVsCredentialProvider` интерфейс, доступный в [NuGet.VisualStudio пакета](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Входной параметр |Описание|
| ----------------|-----------|
| URI uri | Uri источника пакета, для которого запрашиваются учетные данные.|
| IWebProxy прокси-сервера | Веб-прокси, который используется для связи в сети. Значение NULL, если проверка подлинности прокси-сервер не настроен. |
| bool isProxyRequest | Значение true, если этот запрос для получения учетных данных проверки подлинности прокси-сервера. Если реализация не является допустимым для получения учетных данных прокси-сервера, должны быть возвращено значение null. |
| bool isRetry | Значение true, если учетные данные ранее запрошенные для данного универсального кода ресурса, но предоставленные учетные данные не разрешает авторизованного доступа. |
| Неинтерактивная bool | Значение true, если поставщик учетных данных необходимо отключить все запросы пользователю и вместо этого используйте значения по умолчанию. |
| CancellationToken cancellationToken | Этот токен отмены должен проверить, чтобы определить, если учетные данные запрашивающего операция была отменена. |

**Возвращаемое значение**: объект учетных данных, реализующий интерфейс [ `System.Net.ICredentials` интерфейс](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
