---
title: Использование NuGet.Server для размещения веб-каналов NuGet
description: Описывается создание и размещение веб-канала пакетов NuGet на любом сервере со службами IIS с помощью NuGet.Server для предоставления доступа к пакетам по протоколам HTTP и OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/10/2020
ms.locfileid: "79059572"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server — это предоставляемый организацией .NET Foundation пакет, который создает приложение ASP.NET для размещения веб-канала пакетов на любом сервере со службами IIS. Попросту говоря, NuGet.Server создает на сервере папку, доступную по протоколу HTTP(S) (и, в частности, OData). Простота настройки делает это решение оптимальным для несложных сценариев.

1. Создайте пустое веб-приложение ASP.NET в Visual Studio и добавьте в него пакет NuGet.Server.
1. Настройте папку `Packages` в приложении и добавьте пакеты.
1. Разверните приложение на подходящем сервере.

В следующих разделах подробно рассматривается выполнение этого процесса с помощью C#.

Если у вас есть дополнительные вопросы о NuGet.Server, сообщите об этом на [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Создание и развертывание веб-приложения ASP.NET с пакетом NuGet.Server

1. В Visual Studio последовательно выберите **Файл > Создать > Проект**, а затем найдите и выберите шаблон "Веб-приложение ASP.NET (.NET Framework)" для C#.

    ![Выбор шаблона веб-проекта .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. Задайте для параметра **Framework** значение ".NET Framework 4.6".

    ![Задание целевой платформы для нового проекта](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Присвойте приложению подходящее имя, *отличное* от NuGet.Server, нажмите кнопку "ОК", а затем в следующем диалоговом окне выберите **пустой** шаблон и нажмите кнопку **ОК**.

    ![Выбор пустого веб-проекта](media/Hosting_02-NuGet.Server-Empty.png)

1. Щелкните проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.

1. В пользовательском интерфейсе диспетчера пакетов откройте вкладку **Обзор**, а затем найдите и установите последнюю версию пакета NuGet.Server, если целевой платформой является .NET Framework 4.6. (Ее также можно установить из консоли диспетчера пакетов с помощью команды `Install-Package NuGet.Server`.) Примите условия лицензионного соглашения при отображении соответствующего запроса.

    ![Установка пакета NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. В результате установки NuGet.Server пустое веб-приложение преобразуется в источник пакетов. При этом устанавливаются разные пакеты, в приложении создается папка `Packages`, а в файл `web.config` добавляются дополнительные параметры (подробные сведения см. в комментариях в этом файле).

    > [!Important]
    > Тщательно проверьте `web.config` после того, как пакет NuGet.Server внесет все изменения в этот файл. NuGet.Server может не перезаписывать имеющиеся элементы, а создавать их дубликаты. Позднее при попытке запуска проекта эти дубликаты приведут к ошибке "Внутренняя ошибка сервера". Например, если ваш файл `web.config` содержит `<compilation debug="true" targetFramework="4.5.2" />` до установки NuGet.Server, пакет не перезаписывает его, а вставляет второй экземпляр `<compilation debug="true" targetFramework="4.6" />`. В этом случае удалите элемент с более старой версией платформы.

1. Запустите сайт локально в Visual Studio (используя команду **Отладка > Запуск без отладки** или сочетание клавиш CTRL+F5). Домашняя страница содержит URL-адреса веб-канала пакетов, как показано ниже. Если возникают ошибки, тщательно изучите `web.config` на наличие повторяющихся элементов.

    ![Домашняя страница по умолчанию для приложения с пакетом NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  При первом запуске приложения пакет NuGet.Server изменяет структуру папки `Packages` так, чтобы она содержала вложенную папку для каждого пакета. Такая структура соответствует [структуре локального хранилища](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands), представленной в NuGet 3.3, что позволяет повысить производительность. При добавлении дополнительных пакетов следуйте этой структуре.

1. Протестировав развертывание в локальной среде, можно развернуть приложение на любом внутреннем или внешней сайте.

1. При развертывании на сайте `http://<domain>` URL-адрес источника пакетов будет иметь вид `http://<domain>/nuget`.

## <a name="adding-packages-to-the-feed-externally"></a>Добавление пакетов в веб-канал извне

После запуска сайта NuGet.Server можно добавить пакеты с помощью [nuget push](../reference/cli-reference/cli-ref-push.md) при условии, что в файле `web.config` задано значение ключа API.

После установки пакета NuGet.Server файл `web.config` содержит пустое значение `appSetting/apiKey`.

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Если параметр `apiKey` опущен или имеет пустое значение, отправка пакетов в веб-канал отключена.

Чтобы включить эту возможность, присвойте параметру `apiKey` значение (в идеале надежный пароль) и добавьте ключ `appSettings/requireApiKey` со значением `true`.

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Если сервер уже защищен или ключ API не требуется по иным причинам (например, при использовании частного сервера в локальной сети рабочей группы), ключу `requireApiKey` можно присвоить значение `false`. После этого все пользователи, имеющие доступ к серверу, смогут отправлять пакеты.

Начиная с версии NuGet.Server 3.0.0, URL-адрес для отправки пакетов изменился на `http://<domain>/nuget`. До версии 3.0.0 использовался URL-адрес для отправки `http://<domain>/api/v2/package`.

В версии NuGet 3.2.1 и более поздних устаревший URL-адрес `/api/v2/package` по умолчанию включен в дополнение к `/nuget` посредством параметра `enableLegacyPushRoute: true` в конфигурации запуска (по умолчанию `NuGetODataConfig.cs`). Обратите внимание, что эта функция не работает при размещении нескольких веб-каналов в одном проекте.

## <a name="removing-packages-from-the-feed"></a>Удаление пакетов из веб-канала

При использовании NuGet.Server команда [nuget delete](../reference/cli-reference/cli-ref-delete.md) удаляет пакет из репозитория при условии, что вы указали ключ API вместе с комментарием.

Если вы хотите изменить поведение, чтобы вместо этого удалить пакет из списка (оставив его доступным для восстановления), измените значение ключа `enableDelisting` в `web.config` на true.

## <a name="configuring-the-packages-folder"></a>Настройка папки Packages

В `NuGet.Server` 1.5 или более поздней версии можно настроить папку с пакетами с помощью значения `appSettings/packagesPath` в файле `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` может быть абсолютным или виртуальным путем.

Если параметр `packagesPath` опущен или имеет пустое значение, используется папка пакетов по умолчанию `~/Packages`.

## <a name="making-packages-available-when-you-publish-the-web-app"></a>Предоставление доступа к пакетам при публикации веб-приложения

Чтобы сделать пакеты доступными через веб-канал при публикации приложения на сервере, добавьте файлы каждого `.nupkg` в папку `Packages` в Visual Studio, а затем присвойте свойству **Действие сборки** значение **Содержимое**, а свойству **Копировать в выходной каталог** — значение **Всегда копировать**.

![Копирование пакетов в папку Packages в проекте](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>Заметки о выпуске

Заметки о выпуске NuGet.Server доступны на посвященной выпуску [странице GitHub](https://github.com/NuGet/NuGet.Server/releases).
В заметках приводятся сведения об исправленных ошибках и добавленных функциях.

## <a name="nugetserver-support"></a>Поддержка NuGet.Server

Для получения дополнительной помощи по использованию NuGet.Server сообщите о проблеме на сайте [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).
