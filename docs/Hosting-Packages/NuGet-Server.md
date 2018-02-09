---
title: "Использование NuGet.Server для размещения веб-каналов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Описывается создание и размещение веб-канала пакетов NuGet на любом сервере со службами IIS с помощью NuGet.Server для предоставления доступа к пакетам по протоколам HTTP и OData."
keywords: "веб-канал NuGet, коллекция NuGet, удаленный веб-канал пакетов, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="nugetserver"></a><span data-ttu-id="a0497-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="a0497-104">NuGet.Server</span></span>

<span data-ttu-id="a0497-105">NuGet.Server — это предоставляемый организацией .NET Foundation пакет, который создает приложение ASP.NET для размещения веб-канала пакетов на любом сервере со службами IIS.</span><span class="sxs-lookup"><span data-stu-id="a0497-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="a0497-106">Попросту говоря, NuGet.Server создает на сервере папку, доступную по протоколу HTTP(S) (и, в частности, OData).</span><span class="sxs-lookup"><span data-stu-id="a0497-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="a0497-107">Простота настройки делает это решение оптимальным для несложных сценариев.</span><span class="sxs-lookup"><span data-stu-id="a0497-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="a0497-108">Создайте пустое веб-приложение ASP.NET в Visual Studio и добавьте в него пакет NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="a0497-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="a0497-109">Настройте папку `Packages` в приложении и добавьте пакеты.</span><span class="sxs-lookup"><span data-stu-id="a0497-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="a0497-110">Разверните приложение на подходящем сервере.</span><span class="sxs-lookup"><span data-stu-id="a0497-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="a0497-111">В следующих разделах подробно рассматривается выполнение этого процесса с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="a0497-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="a0497-112">Создание и развертывание веб-приложения ASP.NET с пакетом NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="a0497-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="a0497-113">В Visual Studio последовательно выберите **Файл > Создать > Проект**, выберите целевую платформу .NET Framework 4.6 (см. ниже), выполните поиск по запросу "ASP.NET" и выберите шаблон **Веб-приложение ASP.NET (.NET Framework)** для C#.</span><span class="sxs-lookup"><span data-stu-id="a0497-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![Выбор целевой платформы .NET Framework 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="a0497-115">Присвойте приложению подходящее имя, *отличное* от NuGet.Server, нажмите кнопку "ОК", а затем в следующем диалоговом окне выберите **пустой** шаблон и нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="a0497-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="a0497-116">Щелкните проект правой кнопкой мыши, выберите пункт **Управление пакетами NuGet**, а затем в пользовательском интерфейсе диспетчера пакетов найдите и установите последнюю версию пакета NuGet.Server, если целевой платформой является .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="a0497-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="a0497-117">(Ее также можно установить из консоли диспетчера пакетов с помощью команды `Install-Package NuGet.Server`.)</span><span class="sxs-lookup"><span data-stu-id="a0497-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![Установка пакета NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="a0497-119">Если веб-приложение предназначено для платформы .NET Framework 4.5.2, необходимо вместо этого установить версию NuGet Server **2.10.3**.</span><span class="sxs-lookup"><span data-stu-id="a0497-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="a0497-120">В результате установки NuGet.Server пустое веб-приложение преобразуется в источник пакетов.</span><span class="sxs-lookup"><span data-stu-id="a0497-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="a0497-121">В приложении создается папка `Packages`, а файл `web.config` перезаписывается для добавления дополнительных параметров (подробные сведения см. в комментариях в этом файле).</span><span class="sxs-lookup"><span data-stu-id="a0497-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="a0497-122">Чтобы сделать пакеты доступными через веб-канал при публикации приложения на сервере, добавьте их файлы `.nupkg` в папку `Packages` в Visual Studio, а затем присвойте свойству **Действие сборки** значение **Содержимое**, а свойству **Копировать в выходной каталог** — значение **Всегда копировать**.</span><span class="sxs-lookup"><span data-stu-id="a0497-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Копирование пакетов в папку Packages в проекте](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="a0497-124">Запустите сайт локально в Visual Studio (без отладки, то есть с помощью клавиш CTRL+F5).</span><span class="sxs-lookup"><span data-stu-id="a0497-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="a0497-125">На домашней странице приводятся URL-адреса веб-канала пакетов.</span><span class="sxs-lookup"><span data-stu-id="a0497-125">The home page provides the package feed URLs:</span></span>

    ![Домашняя страница по умолчанию для приложения с пакетом NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="a0497-127">Щелкните ссылку **here** (здесь) в выделенной выше области, чтобы увидеть веб-канал пакетов OData.</span><span class="sxs-lookup"><span data-stu-id="a0497-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="a0497-128">При первом запуске приложения пакет NuGet.Server изменяет структуру папки `Packages` так, чтобы она содержала вложенную папку для каждого пакета.</span><span class="sxs-lookup"><span data-stu-id="a0497-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="a0497-129">Такая структура соответствует [структуре локального хранилища](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands), представленной в NuGet 3.3, что позволяет повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="a0497-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="a0497-130">При добавлении дополнительных пакетов следуйте этой структуре.</span><span class="sxs-lookup"><span data-stu-id="a0497-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="a0497-131">Протестировав развертывание в локальной среде, можно развернуть приложение на любом внутреннем или внешней сайте.</span><span class="sxs-lookup"><span data-stu-id="a0497-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="a0497-132">При развертывании на сайте `http://<domain>` URL-адрес источника пакетов будет иметь вид `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="a0497-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="a0497-133">Настройка папки Packages</span><span class="sxs-lookup"><span data-stu-id="a0497-133">Configuring the Packages folder</span></span>

<span data-ttu-id="a0497-134">В `NuGet.Server` 1.5 или более поздней версии можно более детально настроить папку с пакетами с помощью значения `appSetting/packagesPath` в файле `web.config`.</span><span class="sxs-lookup"><span data-stu-id="a0497-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="a0497-135">`packagesPath` может быть абсолютным или виртуальным путем.</span><span class="sxs-lookup"><span data-stu-id="a0497-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="a0497-136">Если параметр `packagesPath` опущен или имеет пустое значение, используется папка пакетов по умолчанию `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="a0497-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="a0497-137">Добавление пакетов в веб-канал извне</span><span class="sxs-lookup"><span data-stu-id="a0497-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="a0497-138">После запуска сайта NuGet.Server можно добавлять и удалять пакеты с помощью программы nuget.exe при условии, что в файле `web.config` задано значение ключа API.</span><span class="sxs-lookup"><span data-stu-id="a0497-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="a0497-139">После установки пакета NuGet.Server файл `web.config` содержит пустое значение `appSetting/apiKey`.</span><span class="sxs-lookup"><span data-stu-id="a0497-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="a0497-140">Если параметр `apiKey` опущен или имеет пустое значение, отправка пакетов в веб-канал отключена.</span><span class="sxs-lookup"><span data-stu-id="a0497-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="a0497-141">Чтобы включить эту возможность, присвойте параметру `apiKey` значение (в идеале надежный пароль) и добавьте ключ `appSettings/requireApiKey` со значением `true`.</span><span class="sxs-lookup"><span data-stu-id="a0497-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="a0497-142">Если сервер уже защищен или ключ API не требуется по иным причинам (например, при использовании частного сервера в локальной сети рабочей группы), ключу `requireApiKey` можно присвоить значение `false`.</span><span class="sxs-lookup"><span data-stu-id="a0497-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="a0497-143">После этого все пользователи, имеющие доступ к серверу, смогут отправлять или удалять пакеты.</span><span class="sxs-lookup"><span data-stu-id="a0497-143">All users with access to the server can then push or delete packages.</span></span>