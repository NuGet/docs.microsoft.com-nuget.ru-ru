---
title: Использование NuGet.Server для размещения веб-каналов NuGet
description: Описывается создание и размещение веб-канала пакетов NuGet на любом сервере со службами IIS с помощью NuGet.Server для предоставления доступа к пакетам по протоколам HTTP и OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "79059572"
---
# <a name="nugetserver"></a><span data-ttu-id="939c7-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="939c7-103">NuGet.Server</span></span>

<span data-ttu-id="939c7-104">NuGet.Server — это предоставляемый организацией .NET Foundation пакет, который создает приложение ASP.NET для размещения веб-канала пакетов на любом сервере со службами IIS.</span><span class="sxs-lookup"><span data-stu-id="939c7-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="939c7-105">Попросту говоря, NuGet.Server создает на сервере папку, доступную по протоколу HTTP(S) (и, в частности, OData).</span><span class="sxs-lookup"><span data-stu-id="939c7-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="939c7-106">Простота настройки делает это решение оптимальным для несложных сценариев.</span><span class="sxs-lookup"><span data-stu-id="939c7-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="939c7-107">Создайте пустое веб-приложение ASP.NET в Visual Studio и добавьте в него пакет NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="939c7-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="939c7-108">Настройте папку `Packages` в приложении и добавьте пакеты.</span><span class="sxs-lookup"><span data-stu-id="939c7-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="939c7-109">Разверните приложение на подходящем сервере.</span><span class="sxs-lookup"><span data-stu-id="939c7-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="939c7-110">В следующих разделах подробно рассматривается выполнение этого процесса с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="939c7-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="939c7-111">Если у вас есть дополнительные вопросы о NuGet.Server, сообщите об этом на [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="939c7-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="939c7-112">Создание и развертывание веб-приложения ASP.NET с пакетом NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="939c7-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="939c7-113">В Visual Studio последовательно выберите **Файл > Создать > Проект**, а затем найдите и выберите шаблон "Веб-приложение ASP.NET (.NET Framework)" для C#.</span><span class="sxs-lookup"><span data-stu-id="939c7-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for C#.</span></span>

    ![Выбор шаблона веб-проекта .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="939c7-115">Задайте для параметра **Framework** значение ".NET Framework 4.6".</span><span class="sxs-lookup"><span data-stu-id="939c7-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![Задание целевой платформы для нового проекта](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="939c7-117">Присвойте приложению подходящее имя, *отличное* от NuGet.Server, нажмите кнопку "ОК", а затем в следующем диалоговом окне выберите **пустой** шаблон и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="939c7-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![Выбор пустого веб-проекта](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="939c7-119">Щелкните проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="939c7-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="939c7-120">В пользовательском интерфейсе диспетчера пакетов откройте вкладку **Обзор**, а затем найдите и установите последнюю версию пакета NuGet.Server, если целевой платформой является .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="939c7-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="939c7-121">(Ее также можно установить из консоли диспетчера пакетов с помощью команды `Install-Package NuGet.Server`.) Примите условия лицензионного соглашения при отображении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="939c7-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Установка пакета NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="939c7-123">В результате установки NuGet.Server пустое веб-приложение преобразуется в источник пакетов.</span><span class="sxs-lookup"><span data-stu-id="939c7-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="939c7-124">При этом устанавливаются разные пакеты, в приложении создается папка `Packages`, а в файл `web.config` добавляются дополнительные параметры (подробные сведения см. в комментариях в этом файле).</span><span class="sxs-lookup"><span data-stu-id="939c7-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="939c7-125">Тщательно проверьте `web.config` после того, как пакет NuGet.Server внесет все изменения в этот файл.</span><span class="sxs-lookup"><span data-stu-id="939c7-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="939c7-126">NuGet.Server может не перезаписывать имеющиеся элементы, а создавать их дубликаты.</span><span class="sxs-lookup"><span data-stu-id="939c7-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="939c7-127">Позднее при попытке запуска проекта эти дубликаты приведут к ошибке "Внутренняя ошибка сервера".</span><span class="sxs-lookup"><span data-stu-id="939c7-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="939c7-128">Например, если ваш файл `web.config` содержит `<compilation debug="true" targetFramework="4.5.2" />` до установки NuGet.Server, пакет не перезаписывает его, а вставляет второй экземпляр `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="939c7-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="939c7-129">В этом случае удалите элемент с более старой версией платформы.</span><span class="sxs-lookup"><span data-stu-id="939c7-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="939c7-130">Запустите сайт локально в Visual Studio (используя команду **Отладка > Запуск без отладки** или сочетание клавиш CTRL+F5).</span><span class="sxs-lookup"><span data-stu-id="939c7-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="939c7-131">Домашняя страница содержит URL-адреса веб-канала пакетов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="939c7-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="939c7-132">Если возникают ошибки, тщательно изучите `web.config` на наличие повторяющихся элементов.</span><span class="sxs-lookup"><span data-stu-id="939c7-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![Домашняя страница по умолчанию для приложения с пакетом NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="939c7-134">При первом запуске приложения пакет NuGet.Server изменяет структуру папки `Packages` так, чтобы она содержала вложенную папку для каждого пакета.</span><span class="sxs-lookup"><span data-stu-id="939c7-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="939c7-135">Такая структура соответствует [структуре локального хранилища](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands), представленной в NuGet 3.3, что позволяет повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="939c7-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="939c7-136">При добавлении дополнительных пакетов следуйте этой структуре.</span><span class="sxs-lookup"><span data-stu-id="939c7-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="939c7-137">Протестировав развертывание в локальной среде, можно развернуть приложение на любом внутреннем или внешней сайте.</span><span class="sxs-lookup"><span data-stu-id="939c7-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="939c7-138">При развертывании на сайте `http://<domain>` URL-адрес источника пакетов будет иметь вид `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="939c7-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="939c7-139">Добавление пакетов в веб-канал извне</span><span class="sxs-lookup"><span data-stu-id="939c7-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="939c7-140">После запуска сайта NuGet.Server можно добавить пакеты с помощью [nuget push](../reference/cli-reference/cli-ref-push.md) при условии, что в файле `web.config` задано значение ключа API.</span><span class="sxs-lookup"><span data-stu-id="939c7-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="939c7-141">После установки пакета NuGet.Server файл `web.config` содержит пустое значение `appSetting/apiKey`.</span><span class="sxs-lookup"><span data-stu-id="939c7-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="939c7-142">Если параметр `apiKey` опущен или имеет пустое значение, отправка пакетов в веб-канал отключена.</span><span class="sxs-lookup"><span data-stu-id="939c7-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="939c7-143">Чтобы включить эту возможность, присвойте параметру `apiKey` значение (в идеале надежный пароль) и добавьте ключ `appSettings/requireApiKey` со значением `true`.</span><span class="sxs-lookup"><span data-stu-id="939c7-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="939c7-144">Если сервер уже защищен или ключ API не требуется по иным причинам (например, при использовании частного сервера в локальной сети рабочей группы), ключу `requireApiKey` можно присвоить значение `false`.</span><span class="sxs-lookup"><span data-stu-id="939c7-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="939c7-145">После этого все пользователи, имеющие доступ к серверу, смогут отправлять пакеты.</span><span class="sxs-lookup"><span data-stu-id="939c7-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="939c7-146">Начиная с версии NuGet.Server 3.0.0, URL-адрес для отправки пакетов изменился на `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="939c7-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="939c7-147">До версии 3.0.0 использовался URL-адрес для отправки `http://<domain>/api/v2/package`.</span><span class="sxs-lookup"><span data-stu-id="939c7-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="939c7-148">В версии NuGet 3.2.1 и более поздних устаревший URL-адрес `/api/v2/package` по умолчанию включен в дополнение к `/nuget` посредством параметра `enableLegacyPushRoute: true` в конфигурации запуска (по умолчанию `NuGetODataConfig.cs`).</span><span class="sxs-lookup"><span data-stu-id="939c7-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="939c7-149">Обратите внимание, что эта функция не работает при размещении нескольких веб-каналов в одном проекте.</span><span class="sxs-lookup"><span data-stu-id="939c7-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="939c7-150">Удаление пакетов из веб-канала</span><span class="sxs-lookup"><span data-stu-id="939c7-150">Removing packages from the feed</span></span>

<span data-ttu-id="939c7-151">При использовании NuGet.Server команда [nuget delete](../reference/cli-reference/cli-ref-delete.md) удаляет пакет из репозитория при условии, что вы указали ключ API вместе с комментарием.</span><span class="sxs-lookup"><span data-stu-id="939c7-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="939c7-152">Если вы хотите изменить поведение, чтобы вместо этого удалить пакет из списка (оставив его доступным для восстановления), измените значение ключа `enableDelisting` в `web.config` на true.</span><span class="sxs-lookup"><span data-stu-id="939c7-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="939c7-153">Настройка папки Packages</span><span class="sxs-lookup"><span data-stu-id="939c7-153">Configuring the Packages folder</span></span>

<span data-ttu-id="939c7-154">В `NuGet.Server` 1.5 или более поздней версии можно настроить папку с пакетами с помощью значения `appSettings/packagesPath` в файле `web.config`:</span><span class="sxs-lookup"><span data-stu-id="939c7-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="939c7-155">`packagesPath` может быть абсолютным или виртуальным путем.</span><span class="sxs-lookup"><span data-stu-id="939c7-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="939c7-156">Если параметр `packagesPath` опущен или имеет пустое значение, используется папка пакетов по умолчанию `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="939c7-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="939c7-157">Предоставление доступа к пакетам при публикации веб-приложения</span><span class="sxs-lookup"><span data-stu-id="939c7-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="939c7-158">Чтобы сделать пакеты доступными через веб-канал при публикации приложения на сервере, добавьте файлы каждого `.nupkg` в папку `Packages` в Visual Studio, а затем присвойте свойству **Действие сборки** значение **Содержимое**, а свойству **Копировать в выходной каталог** — значение **Всегда копировать**.</span><span class="sxs-lookup"><span data-stu-id="939c7-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![Копирование пакетов в папку Packages в проекте](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="939c7-160">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="939c7-160">Release Notes</span></span>

<span data-ttu-id="939c7-161">Заметки о выпуске NuGet.Server доступны на посвященной выпуску [странице GitHub](https://github.com/NuGet/NuGet.Server/releases).</span><span class="sxs-lookup"><span data-stu-id="939c7-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="939c7-162">В заметках приводятся сведения об исправленных ошибках и добавленных функциях.</span><span class="sxs-lookup"><span data-stu-id="939c7-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="939c7-163">Поддержка NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="939c7-163">NuGet.Server support</span></span>

<span data-ttu-id="939c7-164">Для получения дополнительной помощи по использованию NuGet.Server сообщите о проблеме на сайте [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="939c7-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
