---
title: "Использование NuGet.Server для размещения веб-каналов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Описывается создание и размещение веб-канала пакетов NuGet на любом сервере со службами IIS с помощью NuGet.Server для предоставления доступа к пакетам по протоколам HTTP и OData."
keywords: "веб-канал NuGet, коллекция NuGet, удаленный веб-канал пакетов, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d85c1ca88ca44c8f8bfa5cb9c453279f65f26f50
ms.sourcegitcommit: 9adf5349eab91bd1d044e11f34836d53cfb115b3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2018
---
# <a name="nugetserver"></a><span data-ttu-id="285ec-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="285ec-104">NuGet.Server</span></span>

<span data-ttu-id="285ec-105">NuGet.Server — это предоставляемый организацией .NET Foundation пакет, который создает приложение ASP.NET для размещения веб-канала пакетов на любом сервере со службами IIS.</span><span class="sxs-lookup"><span data-stu-id="285ec-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="285ec-106">Попросту говоря, NuGet.Server создает на сервере папку, доступную по протоколу HTTP(S) (и, в частности, OData).</span><span class="sxs-lookup"><span data-stu-id="285ec-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="285ec-107">Простота настройки делает это решение оптимальным для несложных сценариев.</span><span class="sxs-lookup"><span data-stu-id="285ec-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="285ec-108">Создайте пустое веб-приложение ASP.NET в Visual Studio и добавьте в него пакет NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="285ec-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="285ec-109">Настройте папку `Packages` в приложении и добавьте пакеты.</span><span class="sxs-lookup"><span data-stu-id="285ec-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="285ec-110">Разверните приложение на подходящем сервере.</span><span class="sxs-lookup"><span data-stu-id="285ec-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="285ec-111">В следующих разделах подробно рассматривается выполнение этого процесса с помощью C#.</span><span class="sxs-lookup"><span data-stu-id="285ec-111">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="285ec-112">Если у вас есть дополнительные вопросы о NuGet.Server, сообщите об этом на [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="285ec-112">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="285ec-113">Создание и развертывание веб-приложения ASP.NET с пакетом NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="285ec-113">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="285ec-114">В Visual Studio последовательно выберите **Файл > Создать > Проект**, выполните поиск по запросу "ASP.NET", и выберите шаблон **Веб-приложение ASP.NET (.NET Framework)** для C# и задайте для параметра **Framework** значение ".NET Framework 4.6".</span><span class="sxs-lookup"><span data-stu-id="285ec-114">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Задание целевой платформы для нового проекта](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="285ec-116">Присвойте приложению подходящее имя, *отличное* от NuGet.Server, нажмите кнопку "ОК", а затем в следующем диалоговом окне выберите **пустой** шаблон и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="285ec-116">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="285ec-117">Щелкните проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="285ec-117">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="285ec-118">В пользовательском интерфейсе диспетчера пакетов откройте вкладку **Обзор**, а затем найдите и установите последнюю версию пакета NuGet.Server, если целевой платформой является .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="285ec-118">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="285ec-119">(Ее также можно установить из консоли диспетчера пакетов с помощью команды `Install-Package NuGet.Server`.) Примите условия лицензионного соглашения при отображении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="285ec-119">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Установка пакета NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="285ec-121">В результате установки NuGet.Server пустое веб-приложение преобразуется в источник пакетов.</span><span class="sxs-lookup"><span data-stu-id="285ec-121">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="285ec-122">При этом устанавливаются разные пакеты, в приложении создается папка `Packages`, а в файл `web.config` добавляются дополнительные параметры (подробные сведения см. в комментариях в этом файле).</span><span class="sxs-lookup"><span data-stu-id="285ec-122">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="285ec-123">Тщательно проверьте `web.config` после того, как пакет NuGet.Server внесет все изменения в этот файл.</span><span class="sxs-lookup"><span data-stu-id="285ec-123">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="285ec-124">NuGet.Server может не перезаписывать имеющиеся элементы, а создавать их дубликаты.</span><span class="sxs-lookup"><span data-stu-id="285ec-124">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="285ec-125">Позднее при попытке запуска проекта эти дубликаты приведут к ошибке "Внутренняя ошибка сервера".</span><span class="sxs-lookup"><span data-stu-id="285ec-125">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="285ec-126">Например, если ваш файл `web.config` содержит `<compilation debug="true" targetFramework="4.5.2" />` до установки NuGet.Server, пакет не перезаписывает его, а вставляет второй экземпляр `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="285ec-126">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="285ec-127">В этом случае удалите элемент с более старой версией платформы.</span><span class="sxs-lookup"><span data-stu-id="285ec-127">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="285ec-128">Чтобы сделать пакеты доступными через веб-канал при публикации приложения на сервере, добавьте файлы каждого `.nupkg` в папку `Packages` в Visual Studio, а затем присвойте свойству **Действие сборки** значение **Содержимое**, а свойству **Копировать в выходной каталог** — значение **Всегда копировать**.</span><span class="sxs-lookup"><span data-stu-id="285ec-128">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Копирование пакетов в папку Packages в проекте](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="285ec-130">Запустите сайт локально в Visual Studio (используя команду **Отладка > Запуск без отладки** или сочетание клавиш CTRL+F5).</span><span class="sxs-lookup"><span data-stu-id="285ec-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="285ec-131">Домашняя страница содержит URL-адреса веб-канала пакетов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="285ec-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="285ec-132">Если возникают ошибки, тщательно изучите `web.config` на наличие повторяющихся элементов, как указано в шаге 5.</span><span class="sxs-lookup"><span data-stu-id="285ec-132">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![Домашняя страница по умолчанию для приложения с пакетом NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="285ec-134">Щелкните ссылку **here** (здесь) в выделенной выше области, чтобы увидеть веб-канал пакетов OData.</span><span class="sxs-lookup"><span data-stu-id="285ec-134">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="285ec-135">При первом запуске приложения пакет NuGet.Server изменяет структуру папки `Packages` так, чтобы она содержала вложенную папку для каждого пакета.</span><span class="sxs-lookup"><span data-stu-id="285ec-135">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="285ec-136">Такая структура соответствует [структуре локального хранилища](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands), представленной в NuGet 3.3, что позволяет повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="285ec-136">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="285ec-137">При добавлении дополнительных пакетов следуйте этой структуре.</span><span class="sxs-lookup"><span data-stu-id="285ec-137">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="285ec-138">Протестировав развертывание в локальной среде, можно развернуть приложение на любом внутреннем или внешней сайте.</span><span class="sxs-lookup"><span data-stu-id="285ec-138">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="285ec-139">При развертывании на сайте `http://<domain>` URL-адрес источника пакетов будет иметь вид `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="285ec-139">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="285ec-140">Настройка папки Packages</span><span class="sxs-lookup"><span data-stu-id="285ec-140">Configuring the Packages folder</span></span>

<span data-ttu-id="285ec-141">В `NuGet.Server` 1.5 или более поздней версии можно более детально настроить папку с пакетами с помощью значения `appSetting/packagesPath` в файле `web.config`.</span><span class="sxs-lookup"><span data-stu-id="285ec-141">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="285ec-142">`packagesPath` может быть абсолютным или виртуальным путем.</span><span class="sxs-lookup"><span data-stu-id="285ec-142">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="285ec-143">Если параметр `packagesPath` опущен или имеет пустое значение, используется папка пакетов по умолчанию `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="285ec-143">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="285ec-144">Добавление пакетов в веб-канал извне</span><span class="sxs-lookup"><span data-stu-id="285ec-144">Adding packages to the feed externally</span></span>

<span data-ttu-id="285ec-145">После запуска сайта NuGet.Server можно добавить пакеты с помощью [nuget push](../tools/cli-ref-push.md) при условии, что в файле `web.config` задано значение ключа API.</span><span class="sxs-lookup"><span data-stu-id="285ec-145">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="285ec-146">После установки пакета NuGet.Server файл `web.config` содержит пустое значение `appSetting/apiKey`.</span><span class="sxs-lookup"><span data-stu-id="285ec-146">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="285ec-147">Если параметр `apiKey` опущен или имеет пустое значение, отправка пакетов в веб-канал отключена.</span><span class="sxs-lookup"><span data-stu-id="285ec-147">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="285ec-148">Чтобы включить эту возможность, присвойте параметру `apiKey` значение (в идеале надежный пароль) и добавьте ключ `appSettings/requireApiKey` со значением `true`.</span><span class="sxs-lookup"><span data-stu-id="285ec-148">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="285ec-149">Если сервер уже защищен или ключ API не требуется по иным причинам (например, при использовании частного сервера в локальной сети рабочей группы), ключу `requireApiKey` можно присвоить значение `false`.</span><span class="sxs-lookup"><span data-stu-id="285ec-149">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="285ec-150">После этого все пользователи, имеющие доступ к серверу, смогут отправлять пакеты.</span><span class="sxs-lookup"><span data-stu-id="285ec-150">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="285ec-151">Удаление пакетов из веб-канала</span><span class="sxs-lookup"><span data-stu-id="285ec-151">Removing packages from the feed</span></span>

<span data-ttu-id="285ec-152">При использовании NuGet.Server команда [nuget delete](../tools/cli-ref-delete.md) удаляет пакет из репозитория при условии, что вы указали ключ API вместе с комментарием.</span><span class="sxs-lookup"><span data-stu-id="285ec-152">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="285ec-153">Если вы хотите изменить поведение, чтобы вместо этого удалить пакет из списка (оставив его доступным для восстановления), измените значение ключа `enableDelisting` в `web.config` на true.</span><span class="sxs-lookup"><span data-stu-id="285ec-153">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="285ec-154">Поддержка NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="285ec-154">NuGet.Server support</span></span>

<span data-ttu-id="285ec-155">Для получения дополнительной помощи по использованию NuGet.Server сообщите о проблеме на сайте [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="285ec-155">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>