---
title: "Вводное руководство по созданию и публикации пакета NuGet с помощью Visual Studio | Документация Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Пошаговое руководство по созданию и публикации пакета NuGet с помощью Visual Studio 2017."
keywords: NuGet package creation, NuGet package publishing, NuGet tutorial, Visual Studio create NuGet package, msbuild pack
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a4d60fdc0f27f9c4080266e212ac1cfe470ba925
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package-using-visual-studio"></a><span data-ttu-id="f83f6-104">Создание и публикация пакета с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f83f6-104">Create and publish a package using Visual Studio</span></span>

<span data-ttu-id="f83f6-105">Создание пакета NuGet из библиотеки классов .NET в Visual Studio и его публикация на сайте nuget.org с помощью инструмента CLI выполняются очень просто.</span><span class="sxs-lookup"><span data-stu-id="f83f6-105">It's a simple process to create a NuGet package from a .NET Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="f83f6-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f83f6-106">Pre-requisites</span></span>

1. <span data-ttu-id="f83f6-107">Установите любой выпуск Visual Studio 2017 со страницы [visualstudio.com](https://www.visualstudio.com/) с помощью любой рабочей нагрузки, связанной с .NET.</span><span class="sxs-lookup"><span data-stu-id="f83f6-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="f83f6-108">После установки рабочей нагрузки .NET Visual Studio 2017 автоматически добавит возможности NuGet.</span><span class="sxs-lookup"><span data-stu-id="f83f6-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="f83f6-109">Установите интерфейс командной строки `nuget.exe`, скачав его на сайте [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), и сохраните этот файл `.exe` в подходящую папку. Добавьте эту папку в переменную среды PATH.</span><span class="sxs-lookup"><span data-stu-id="f83f6-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="f83f6-110">Кроме того, если у вас есть установленный [пакет SDK для .NET Core](https://www.microsoft.com/net/download/), можно использовать интерфейс командной строки `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="f83f6-110">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="f83f6-111">[Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее.</span><span class="sxs-lookup"><span data-stu-id="f83f6-111">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="f83f6-112">При создании учетной записи вам направляется сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="f83f6-112">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="f83f6-113">Перед отправкой пакета вам нужно подтвердить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="f83f6-113">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="f83f6-114">Создание проекта библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="f83f6-114">Create a class library project</span></span>

<span data-ttu-id="f83f6-115">Вы можете использовать имеющийся проект библиотеки классов .NET для кода, который нужно упаковать, или же создать простой проект, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="f83f6-115">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="f83f6-116">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > .NET Standard**, выберите шаблон "Библиотека классов (.NET Standard)", назовите проект AppLogger и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f83f6-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="f83f6-117">Щелкните правой кнопкой мыши полученный файл проекта и выберите пункт **Сборка**, чтобы убедиться, что проект создан правильно.</span><span class="sxs-lookup"><span data-stu-id="f83f6-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="f83f6-118">Библиотека DLL находится в папке Debug (или папке Release, если вы используете конфигурацию выпуска для сборки).</span><span class="sxs-lookup"><span data-stu-id="f83f6-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="f83f6-119">В реальном пакете NuGet вы можете реализовать множество полезных возможностей, с помощью которых другие пользователи могут создавать приложения.</span><span class="sxs-lookup"><span data-stu-id="f83f6-119">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="f83f6-120">Однако в этом пошаговом руководстве вы не будете писать дополнительный код, так как библиотеки классов из шаблона достаточно для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="f83f6-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="f83f6-121">Тем не менее, вы можете использовать функциональный код для пакета:</span><span class="sxs-lookup"><span data-stu-id="f83f6-121">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="f83f6-122">Для пакетов NuGet мы рекомендуем использовать целевой объект .NET Standard (если нет причин использовать другое), так как он обеспечивает совместимость с рядом потребляющих проектов.</span><span class="sxs-lookup"><span data-stu-id="f83f6-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="f83f6-123">Настройка свойств пакета</span><span class="sxs-lookup"><span data-stu-id="f83f6-123">Configure package properties</span></span>

1. <span data-ttu-id="f83f6-124">Выберите команду меню **Проект > Свойства**, а затем щелкните вкладку **Пакет**.</span><span class="sxs-lookup"><span data-stu-id="f83f6-124">Select the **Project > Properties** menu command, then select the **Package** tab:</span></span>

    ![Свойства пакета NuGet в проекте Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="f83f6-126">Если пакет будет общедоступным, обратите особое внимание на свойство **Теги**, так как они помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="f83f6-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="f83f6-127">Присвойте пакету уникальный идентификатор и заполните нужные свойства.</span><span class="sxs-lookup"><span data-stu-id="f83f6-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="f83f6-128">Описание различных свойств см. в [справочнике по NUSPEC-файлу](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="f83f6-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="f83f6-129">Все свойства добавляются в манифест `.nuspec`, который Visual Studio создает для проекта.</span><span class="sxs-lookup"><span data-stu-id="f83f6-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="f83f6-130">Необходимо присвоить пакету идентификатор, который будет уникальным на сайте nuget.org или другом используемом узле.</span><span class="sxs-lookup"><span data-stu-id="f83f6-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="f83f6-131">При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).</span><span class="sxs-lookup"><span data-stu-id="f83f6-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="f83f6-132">При попытке опубликовать пакет с именем, которое уже занято, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="f83f6-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="f83f6-133">Необязательно. Чтобы просматривать свойства непосредственно в файле проекта, щелкните правой кнопкой мыши проект в обозревателе решений и выберите **Изменить AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="f83f6-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="f83f6-134">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="f83f6-134">Run the pack command</span></span>

1. <span data-ttu-id="f83f6-135">Выберите конфигурацию **Выпуск**.</span><span class="sxs-lookup"><span data-stu-id="f83f6-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="f83f6-136">Щелкните проект правой кнопкой мыши в окне **обозревателя решений** и выберите команду **Паковать**:</span><span class="sxs-lookup"><span data-stu-id="f83f6-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Команда "Паковать" для NuGet в контекстном меню проекта Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="f83f6-138">Visual Studio создаст проект и файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="f83f6-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="f83f6-139">Ознакомьтесь с результатами в окне **выходных данных** (пример приведен ниже), где содержится путь к файлу пакета.</span><span class="sxs-lookup"><span data-stu-id="f83f6-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="f83f6-140">Обратите внимание, что созданная сборка находится в папке `bin\Release\netstandard2.0`, которая является целевой для .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="f83f6-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="f83f6-141">Альтернативный вариант: упаковка с помощью MSBuild</span><span class="sxs-lookup"><span data-stu-id="f83f6-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="f83f6-142">В качестве альтернативы команде меню с помощью **Pack** в NuGet 4.x+ и MSBuild 15.1+ можно использовать целевой объект `pack`, когда проект содержит необходимые данные о пакете:</span><span class="sxs-lookup"><span data-stu-id="f83f6-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data:</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="f83f6-143">Этот пакет должен находиться в папке `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="f83f6-143">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="f83f6-144">Дополнительные сведения об использовании `msbuild /t:pack` см. в описании [объектов pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="f83f6-144">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="f83f6-145">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="f83f6-145">Publish the package</span></span>

<span data-ttu-id="f83f6-146">Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя интерфейс командной строки `nuget.exe` или `dotnet.exe`, а также ключ API, полученный на этом сайте.</span><span class="sxs-lookup"><span data-stu-id="f83f6-146">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="f83f6-147">Получение ключа API</span><span class="sxs-lookup"><span data-stu-id="f83f6-147">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="f83f6-148">Публикация с помощью команды nuget push</span><span class="sxs-lookup"><span data-stu-id="f83f6-148">Publish with nuget push</span></span>

<span data-ttu-id="f83f6-149">Эту команду можно использовать вместо `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="f83f6-149">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="f83f6-150">Перейдите в папку, содержащую файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="f83f6-150">Change to the folder containing the `.nupkg` file..</span></span>

1. <span data-ttu-id="f83f6-151">Выполните следующую команду, указав имя пакета и заменив значение ключа на ключ API:</span><span class="sxs-lookup"><span data-stu-id="f83f6-151">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="f83f6-152">nuget.exe отображает результаты публикации:</span><span class="sxs-lookup"><span data-stu-id="f83f6-152">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="f83f6-153">Ознакомьтесь со сведениями о [команде nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="f83f6-153">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="f83f6-154">Публикация с помощью команды dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="f83f6-154">Publish with dotnet nuget push</span></span>

<span data-ttu-id="f83f6-155">Эту команду можно использовать вместо `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="f83f6-155">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="f83f6-156">Ошибки публикации</span><span class="sxs-lookup"><span data-stu-id="f83f6-156">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="f83f6-157">Управление опубликованным пакетом</span><span class="sxs-lookup"><span data-stu-id="f83f6-157">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="f83f6-158">См. также</span><span class="sxs-lookup"><span data-stu-id="f83f6-158">Related topics</span></span>

- [<span data-ttu-id="f83f6-159">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="f83f6-159">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="f83f6-160">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="f83f6-160">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="f83f6-161">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="f83f6-161">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="f83f6-162">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="f83f6-162">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="f83f6-163">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="f83f6-163">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="f83f6-164">Документация по библиотеке .NET Standard</span><span class="sxs-lookup"><span data-stu-id="f83f6-164">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="f83f6-165">Перенос кода в .NET Core из .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f83f6-165">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)