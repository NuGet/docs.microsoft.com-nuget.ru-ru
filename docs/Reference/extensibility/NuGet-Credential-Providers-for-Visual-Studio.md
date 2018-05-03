---
title: Поставщики учетных данных NuGet для Visual Studio
description: NuGet поставщиков учетных данных проверки подлинности с каналами, реализовав интерфейс IVsCredentialProvider в расширение Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 740df87b0d663aac482d888e916662528ce27030
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Проверка подлинности веб-каналов в Visual Studio с помощью NuGet поставщиков учетных данных

Расширение NuGet Visual Studio 3.6 + поддерживает поставщиков учетных данных, которые позволяют NuGet для работы с проверкой подлинности веб-каналов.
После установки поставщика учетных данных NuGet для Visual Studio, расширение NuGet для Visual Studio автоматически получить и обновите учетные данные для прошедших проверку подлинности веб-каналы, при необходимости.

Образец реализации можно найти в [пример VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

> [!Note]
> Поставщики учетных данных NuGet для Visual Studio, должен быть установлен как регулярное расширение Visual Studio и потребует [2017 г. Visual Studio](https://aka.ms/vs/15/preview/vs_enterprise) (в настоящее время в предварительной версии) или более поздней версии.
>
> Поставщики учетных данных NuGet для Visual Studio работает только в Visual Studio (не в dotnet восстановления или nuget.exe). Поставщики учетных данных с nuget.exe, в разделе [nuget.exe поставщиков учетных данных](nuget-exe-Credential-providers.md).

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Доступные поставщики учетных данных NuGet для Visual Studio

Отсутствует поставщик учетных данных, встроенные в расширение Visual Studio NuGet поддержки Visual Studio Team Services.

Расширение NuGet Visual Studio использует внутреннюю `VsCredentialProviderImporter` которого также проверяет наличие поставщиков учетных данных подключаемого модуля. Эти поставщики учетных данных подключаемого модуля должно быть включено обнаружение как MEF экспорта типа `IVsCredentialProvider`.

Поставщики доступных подключаемых модулей учетных данных:

- [Поставщик учетных данных MyGet для Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Создание учетных данных поставщика NuGet для Visual Studio

Расширение NuGet Visual Studio 3.6 + реализует внутренней CredentialService, который используется для получения учетных данных. CredentialService имеет список поставщиков учетных данных встроенной и подключаемый модуль. Каждый поставщик предпринимается попытка последовательно, пока полученные учетные данные.

Во время получения учетных данных службы учетных данных попытается поставщиков учетных данных в следующем порядке, остановка, а полученные учетные данные:

1. Учетные данные будут получены из файлов конфигурации NuGet (с помощью встроенной `SettingsCredentialProvider`).
1. Если источник пакета находится на Visual Studio Team Services `VisualStudioAccountProvider` будет использоваться.
1. Все другие поставщики учетных данных подключаемый модуль будет предпринята последовательно.
1. Если учетные данные не получены, пока пользователя будут запрашиваться учетные данные, используя диалоговое окно стандартных обычной проверки подлинности.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Реализация IVsCredentialProvider.GetCredentialsAsync

Чтобы создать учетные данные поставщика NuGet для Visual Studio, создайте расширения Visual Studio, предоставляющий открытый MEF-Экспорт реализации `IVsCredentialProvider` введите, а также придерживается перечисленным ниже.

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

Образец реализации можно найти в [пример VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Каждый поставщик учетных данных NuGet для Visual Studio необходимо:

1. Определите ли его можно указать учетные данные для целевого URI перед запуском процесса получения учетных данных. Если поставщик не может предоставить учетные данные для источника, то он должен возвращать `null`.
1. Если поставщик обрабатывать запросы для целевой URI, но не может предоставить учетные данные, должно создаваться исключение.

Необходимо реализовать пользовательский поставщик учетных данных NuGet для Visual Studio `IVsCredentialProvider` интерфейса, доступные в [NuGet.VisualStudio пакета](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Входной параметр |Описание|
| ----------------|-----------|
| Uri, URI | Uri исходного пакета, для которого запрашиваются учетные данные.|
| IWebProxy прокси-сервера | Веб-прокси, который используется для связи по сети. Значение NULL, если проверка подлинности прокси-сервер не настроен. |
| bool isProxyRequest | Значение true, если этот запрос для получения учетных данных проверки подлинности прокси-сервера. Если реализация не является допустимым для получения учетных данных прокси-сервера, должно быть возвращено значение null. |
| bool isRetry | Значение true, если для данного Uri ранее запрошенные учетные данные, но предоставленные учетные данные не позволяли авторизованный доступ. |
| Неинтерактивные bool | Значение true, если поставщик учетных данных необходимо отключить все запросы пользователю и вместо этого используйте значения по умолчанию. |
| CancellationToken cancellationToken | Этот токен отмены должен проверяться для определения того, если с запросом учетных данных операция была отменена. |

**Возвращаемое значение**: объект учетных данных, реализующий [ `System.Net.ICredentials` интерфейс](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
