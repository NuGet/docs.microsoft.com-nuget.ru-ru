---
title: Вводное руководство по созданию и публикации пакета NuGet .NET Standard с помощью Visual Studio
description: Пошаговое руководство по созданию и публикации пакета NuGet .NET Standard с помощью Visual Studio 2017.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/18/2018
ms.topic: quickstart
ms.openlocfilehash: c5d58aa6312eae801607ca44a81bc092a7a7c15f
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard"></a><span data-ttu-id="999d8-103">Краткое руководство. Создание и публикация пакета NuGet с помощью Visual Studio (.NET Standard)</span><span class="sxs-lookup"><span data-stu-id="999d8-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard)</span></span>

<span data-ttu-id="999d8-104">Создание пакета NuGet из библиотеки классов .NET Standard в Visual Studio и его публикация на сайте nuget.org с помощью инструмента CLI выполняются очень просто.</span><span class="sxs-lookup"><span data-stu-id="999d8-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="999d8-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="999d8-105">Prerequisites</span></span>

1. <span data-ttu-id="999d8-106">Установите любой выпуск Visual Studio 2017 со страницы [visualstudio.com](https://www.visualstudio.com/) с помощью любой рабочей нагрузки, связанной с .NET.</span><span class="sxs-lookup"><span data-stu-id="999d8-106">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="999d8-107">После установки рабочей нагрузки .NET Visual Studio 2017 автоматически добавит возможности NuGet.</span><span class="sxs-lookup"><span data-stu-id="999d8-107">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="999d8-108">Установите интерфейс командной строки `nuget.exe`, скачав его на сайте [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), и сохраните этот файл `.exe` в подходящую папку. Добавьте эту папку в переменную среды PATH.</span><span class="sxs-lookup"><span data-stu-id="999d8-108">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="999d8-109">Кроме того, если у вас есть установленный [пакет SDK для .NET Core](https://www.microsoft.com/net/download/), можно использовать интерфейс командной строки `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="999d8-109">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="999d8-110">[Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее.</span><span class="sxs-lookup"><span data-stu-id="999d8-110">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="999d8-111">При создании учетной записи вам направляется сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="999d8-111">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="999d8-112">Перед отправкой пакета вам нужно подтвердить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="999d8-112">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="999d8-113">Создание проекта библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="999d8-113">Create a class library project</span></span>

<span data-ttu-id="999d8-114">Вы можете использовать имеющийся проект библиотеки классов .NET Standard для кода, который нужно упаковать, или же создать простой проект, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="999d8-114">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="999d8-115">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > .NET Standard**, выберите шаблон "Библиотека классов (.NET Standard)", назовите проект AppLogger и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="999d8-115">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="999d8-116">Щелкните правой кнопкой мыши полученный файл проекта и выберите пункт **Сборка**, чтобы убедиться, что проект создан правильно.</span><span class="sxs-lookup"><span data-stu-id="999d8-116">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="999d8-117">Библиотека DLL находится в папке Debug (или папке Release, если вы используете конфигурацию выпуска для сборки).</span><span class="sxs-lookup"><span data-stu-id="999d8-117">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="999d8-118">В реальном пакете NuGet вы можете реализовать множество полезных возможностей, с помощью которых другие пользователи могут создавать приложения.</span><span class="sxs-lookup"><span data-stu-id="999d8-118">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="999d8-119">Однако в этом пошаговом руководстве вы не будете писать дополнительный код, так как библиотеки классов из шаблона достаточно для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="999d8-119">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="999d8-120">Тем не менее, вы можете использовать функциональный код для пакета:</span><span class="sxs-lookup"><span data-stu-id="999d8-120">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> <span data-ttu-id="999d8-121">Для пакетов NuGet мы рекомендуем использовать целевой объект .NET Standard (если нет причин использовать другое), так как он обеспечивает совместимость с рядом потребляющих проектов.</span><span class="sxs-lookup"><span data-stu-id="999d8-121">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="999d8-122">Настройка свойств пакета</span><span class="sxs-lookup"><span data-stu-id="999d8-122">Configure package properties</span></span>

1. <span data-ttu-id="999d8-123">Выберите команду меню **Проект > Свойства**, а затем щелкните вкладку **Пакет**. (Вкладка **Пакет** отображается только для проектов библиотек классов .NET Standard. Если вы ориентируетесь на .NET Framework, см. вместо этого раздел [Создание и публикация пакета .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="999d8-123">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="999d8-124">Если она не отображается в проекте .NET Standard, может потребоваться обновить Visual Studio 2017 до последней версии.)</span><span class="sxs-lookup"><span data-stu-id="999d8-124">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Свойства пакета NuGet в проекте Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="999d8-126">Если пакет будет общедоступным, обратите особое внимание на свойство **Теги**, так как они помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="999d8-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="999d8-127">Присвойте пакету уникальный идентификатор и заполните нужные свойства.</span><span class="sxs-lookup"><span data-stu-id="999d8-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="999d8-128">Описание различных свойств см. в [справочнике по NUSPEC-файлу](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="999d8-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="999d8-129">Все свойства добавляются в манифест `.nuspec`, который Visual Studio создает для проекта.</span><span class="sxs-lookup"><span data-stu-id="999d8-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="999d8-130">Необходимо присвоить пакету идентификатор, который будет уникальным на сайте nuget.org или другом используемом узле.</span><span class="sxs-lookup"><span data-stu-id="999d8-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="999d8-131">При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).</span><span class="sxs-lookup"><span data-stu-id="999d8-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="999d8-132">При попытке опубликовать пакет с именем, которое уже занято, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="999d8-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="999d8-133">Необязательно. Чтобы просматривать свойства непосредственно в файле проекта, щелкните правой кнопкой мыши проект в обозревателе решений и выберите **Изменить AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="999d8-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="999d8-134">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="999d8-134">Run the pack command</span></span>

1. <span data-ttu-id="999d8-135">Выберите конфигурацию **Выпуск**.</span><span class="sxs-lookup"><span data-stu-id="999d8-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="999d8-136">Щелкните проект правой кнопкой мыши в окне **обозревателя решений** и выберите команду **Паковать**:</span><span class="sxs-lookup"><span data-stu-id="999d8-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Команда "Паковать" для NuGet в контекстном меню проекта Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="999d8-138">Visual Studio создаст проект и файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="999d8-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="999d8-139">Ознакомьтесь с результатами в окне **выходных данных** (пример приведен ниже), где содержится путь к файлу пакета.</span><span class="sxs-lookup"><span data-stu-id="999d8-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="999d8-140">Обратите внимание, что созданная сборка находится в папке `bin\Release\netstandard2.0`, которая является целевой для .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="999d8-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="999d8-141">Альтернативный вариант: упаковка с помощью MSBuild</span><span class="sxs-lookup"><span data-stu-id="999d8-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="999d8-142">В качестве альтернативы команде меню **Pack** в NuGet 4.x+ и MSBuild 15.1+ можно использовать целевой объект `pack`, когда проект содержит необходимые данные о пакете.</span><span class="sxs-lookup"><span data-stu-id="999d8-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="999d8-143">Откройте командную строку, перейдите в папку проекта и запустите приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="999d8-143">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="999d8-144">(В общем случае следует запустить Командную строку разработчика для Visual Studio из меню "Пуск", так как в этом случае настраиваются все необходимые пути для MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="999d8-144">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="999d8-145">Этот пакет должен находиться в папке `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="999d8-145">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="999d8-146">Дополнительные сведения об использовании `msbuild /t:pack` см. в описании [объектов pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="999d8-146">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="999d8-147">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="999d8-147">Publish the package</span></span>

<span data-ttu-id="999d8-148">Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя интерфейс командной строки `nuget.exe` или `dotnet.exe`, а также ключ API, полученный на этом сайте.</span><span class="sxs-lookup"><span data-stu-id="999d8-148">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="999d8-149">Получение ключа API</span><span class="sxs-lookup"><span data-stu-id="999d8-149">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="999d8-150">Публикация с помощью команды nuget push</span><span class="sxs-lookup"><span data-stu-id="999d8-150">Publish with nuget push</span></span>

<span data-ttu-id="999d8-151">Эту команду можно использовать вместо `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="999d8-151">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="999d8-152">Перейдите в папку, содержащую файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="999d8-152">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="999d8-153">Выполните следующую команду, указав имя пакета и заменив значение ключа на ключ API:</span><span class="sxs-lookup"><span data-stu-id="999d8-153">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="999d8-154">nuget.exe отображает результаты публикации:</span><span class="sxs-lookup"><span data-stu-id="999d8-154">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="999d8-155">Ознакомьтесь со сведениями о [команде nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="999d8-155">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="999d8-156">Публикация с помощью команды dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="999d8-156">Publish with dotnet nuget push</span></span>

<span data-ttu-id="999d8-157">Эту команду можно использовать вместо `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="999d8-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="999d8-158">Ошибки публикации</span><span class="sxs-lookup"><span data-stu-id="999d8-158">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="999d8-159">Управление опубликованным пакетом</span><span class="sxs-lookup"><span data-stu-id="999d8-159">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="999d8-160">См. также</span><span class="sxs-lookup"><span data-stu-id="999d8-160">Related topics</span></span>

- [<span data-ttu-id="999d8-161">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="999d8-161">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="999d8-162">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="999d8-162">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="999d8-163">Пакеты предварительного выпуска</span><span class="sxs-lookup"><span data-stu-id="999d8-163">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="999d8-164">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="999d8-164">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="999d8-165">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="999d8-165">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="999d8-166">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="999d8-166">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="999d8-167">Документация по библиотеке .NET Standard</span><span class="sxs-lookup"><span data-stu-id="999d8-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="999d8-168">Перенос кода в .NET Core из .NET Framework</span><span class="sxs-lookup"><span data-stu-id="999d8-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
