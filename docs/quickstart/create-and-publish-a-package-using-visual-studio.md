---
title: Создание и публикация пакета .NET Standard с помощью Visual Studio в Windows
description: Пошаговое руководство по созданию и публикации пакета NuGet .NET Standard с помощью Visual Studio 2017 в Windows.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: quickstart
ms.openlocfilehash: a0bf174e3e27ad6d8fefe18f6213213a4bc77b53
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548942"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="94ad8-103">Краткое руководство. Создание и публикация пакета NuGet с помощью Visual Studio (.NET Standard, только для Windows)</span><span class="sxs-lookup"><span data-stu-id="94ad8-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="94ad8-104">Создание пакета NuGet из библиотеки классов .NET Standard в Visual Studio в Windows и его публикация на сайте nuget.org с помощью средства интерфейса командной строки выполняются очень просто.</span><span class="sxs-lookup"><span data-stu-id="94ad8-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="94ad8-105">Это краткое руководство относится только к Visual Studio 2017 для Windows.</span><span class="sxs-lookup"><span data-stu-id="94ad8-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="94ad8-106">Visual Studio для Mac не поддерживает описанные здесь функции.</span><span class="sxs-lookup"><span data-stu-id="94ad8-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="94ad8-107">Используйте вместо этого [средства интерфейса командной строки dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="94ad8-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94ad8-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="94ad8-108">Prerequisites</span></span>

1. <span data-ttu-id="94ad8-109">Установите любой выпуск Visual Studio 2017 со страницы [visualstudio.com](https://www.visualstudio.com/) с помощью любой рабочей нагрузки, связанной с .NET.</span><span class="sxs-lookup"><span data-stu-id="94ad8-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="94ad8-110">После установки рабочей нагрузки .NET Visual Studio 2017 автоматически добавит возможности NuGet.</span><span class="sxs-lookup"><span data-stu-id="94ad8-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="94ad8-111">Установите интерфейс командной строки `nuget.exe`, скачав его на сайте [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), и сохраните этот файл `.exe` в подходящую папку. Добавьте эту папку в переменную среды PATH.</span><span class="sxs-lookup"><span data-stu-id="94ad8-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="94ad8-112">Кроме того, если у вас есть установленный [пакет SDK для .NET Core](https://www.microsoft.com/net/download/), можно использовать интерфейс командной строки `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="94ad8-112">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="94ad8-113">[Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее.</span><span class="sxs-lookup"><span data-stu-id="94ad8-113">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="94ad8-114">При создании учетной записи вам направляется сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="94ad8-114">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="94ad8-115">Перед отправкой пакета вам нужно подтвердить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="94ad8-115">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="94ad8-116">Создание проекта библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="94ad8-116">Create a class library project</span></span>

<span data-ttu-id="94ad8-117">Вы можете использовать имеющийся проект библиотеки классов .NET Standard для кода, который нужно упаковать, или же создать простой проект, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="94ad8-117">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="94ad8-118">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > .NET Standard**, выберите шаблон "Библиотека классов (.NET Standard)", назовите проект AppLogger и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="94ad8-118">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="94ad8-119">Щелкните правой кнопкой мыши полученный файл проекта и выберите пункт **Сборка**, чтобы убедиться, что проект создан правильно.</span><span class="sxs-lookup"><span data-stu-id="94ad8-119">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="94ad8-120">Библиотека DLL находится в папке Debug (или папке Release, если вы используете конфигурацию выпуска для сборки).</span><span class="sxs-lookup"><span data-stu-id="94ad8-120">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="94ad8-121">В реальном пакете NuGet вы можете реализовать множество полезных возможностей, с помощью которых другие пользователи могут создавать приложения.</span><span class="sxs-lookup"><span data-stu-id="94ad8-121">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="94ad8-122">Однако в этом пошаговом руководстве вы не будете писать дополнительный код, так как библиотеки классов из шаблона достаточно для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="94ad8-122">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="94ad8-123">Тем не менее, вы можете использовать функциональный код для пакета:</span><span class="sxs-lookup"><span data-stu-id="94ad8-123">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="94ad8-124">Для пакетов NuGet мы рекомендуем использовать целевой объект .NET Standard (если нет причин использовать другое), так как он обеспечивает совместимость с рядом потребляющих проектов.</span><span class="sxs-lookup"><span data-stu-id="94ad8-124">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="94ad8-125">Настройка свойств пакета</span><span class="sxs-lookup"><span data-stu-id="94ad8-125">Configure package properties</span></span>

1. <span data-ttu-id="94ad8-126">Выберите команду меню **Проект > Свойства**, а затем щелкните вкладку **Пакет**. (Вкладка **Пакет** отображается только для проектов библиотек классов .NET Standard. Если вы ориентируетесь на .NET Framework, см. вместо этого раздел [Создание и публикация пакета .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="94ad8-126">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="94ad8-127">Если она не отображается в проекте .NET Standard, может потребоваться обновить Visual Studio 2017 до последней версии.)</span><span class="sxs-lookup"><span data-stu-id="94ad8-127">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Свойства пакета NuGet в проекте Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="94ad8-129">Если пакет будет общедоступным, обратите особое внимание на свойство **Теги**, так как они помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="94ad8-129">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="94ad8-130">Присвойте пакету уникальный идентификатор и заполните нужные свойства.</span><span class="sxs-lookup"><span data-stu-id="94ad8-130">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="94ad8-131">Описание различных свойств см. в [справочнике по NUSPEC-файлу](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="94ad8-131">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="94ad8-132">Все свойства добавляются в манифест `.nuspec`, который Visual Studio создает для проекта.</span><span class="sxs-lookup"><span data-stu-id="94ad8-132">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="94ad8-133">Необходимо присвоить пакету идентификатор, который будет уникальным на сайте nuget.org или другом используемом узле.</span><span class="sxs-lookup"><span data-stu-id="94ad8-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="94ad8-134">При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).</span><span class="sxs-lookup"><span data-stu-id="94ad8-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="94ad8-135">При попытке опубликовать пакет с именем, которое уже занято, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="94ad8-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="94ad8-136">Необязательно. Чтобы просматривать свойства непосредственно в файле проекта, щелкните правой кнопкой мыши проект в обозревателе решений и выберите **Изменить AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="94ad8-136">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="94ad8-137">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="94ad8-137">Run the pack command</span></span>

1. <span data-ttu-id="94ad8-138">Выберите конфигурацию **Выпуск**.</span><span class="sxs-lookup"><span data-stu-id="94ad8-138">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="94ad8-139">Щелкните проект правой кнопкой мыши в окне **обозревателя решений** и выберите команду **Паковать**:</span><span class="sxs-lookup"><span data-stu-id="94ad8-139">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Команда "Паковать" для NuGet в контекстном меню проекта Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="94ad8-141">Visual Studio создаст проект и файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="94ad8-141">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="94ad8-142">Ознакомьтесь с результатами в окне **выходных данных** (пример приведен ниже), где содержится путь к файлу пакета.</span><span class="sxs-lookup"><span data-stu-id="94ad8-142">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="94ad8-143">Обратите внимание, что созданная сборка находится в папке `bin\Release\netstandard2.0`, которая является целевой для .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="94ad8-143">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="94ad8-144">Альтернативный вариант: упаковка с помощью MSBuild</span><span class="sxs-lookup"><span data-stu-id="94ad8-144">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="94ad8-145">В качестве альтернативы команде меню **Pack** в NuGet 4.x+ и MSBuild 15.1+ можно использовать целевой объект `pack`, когда проект содержит необходимые данные о пакете.</span><span class="sxs-lookup"><span data-stu-id="94ad8-145">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="94ad8-146">Откройте командную строку, перейдите в папку проекта и запустите приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="94ad8-146">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="94ad8-147">(В общем случае следует запустить Командную строку разработчика для Visual Studio из меню "Пуск", так как в этом случае настраиваются все необходимые пути для MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="94ad8-147">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="94ad8-148">Этот пакет должен находиться в папке `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="94ad8-148">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="94ad8-149">Дополнительные сведения об использовании `msbuild /t:pack` см. в описании [объектов pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="94ad8-149">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="94ad8-150">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="94ad8-150">Publish the package</span></span>

<span data-ttu-id="94ad8-151">Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя интерфейс командной строки `nuget.exe` или `dotnet.exe`, а также ключ API, полученный на этом сайте.</span><span class="sxs-lookup"><span data-stu-id="94ad8-151">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="94ad8-152">Получение ключа API</span><span class="sxs-lookup"><span data-stu-id="94ad8-152">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="94ad8-153">Публикация с помощью команды nuget push</span><span class="sxs-lookup"><span data-stu-id="94ad8-153">Publish with nuget push</span></span>

<span data-ttu-id="94ad8-154">Эту команду можно использовать вместо `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="94ad8-154">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="94ad8-155">Перейдите в папку, содержащую файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="94ad8-155">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="94ad8-156">Выполните следующую команду, указав имя пакета и заменив значение ключа на ключ API:</span><span class="sxs-lookup"><span data-stu-id="94ad8-156">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="94ad8-157">nuget.exe отображает результаты публикации:</span><span class="sxs-lookup"><span data-stu-id="94ad8-157">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="94ad8-158">Ознакомьтесь со сведениями о [команде nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="94ad8-158">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="94ad8-159">Публикация с помощью команды dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="94ad8-159">Publish with dotnet nuget push</span></span>

<span data-ttu-id="94ad8-160">Эту команду можно использовать вместо `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="94ad8-160">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="94ad8-161">Ошибки публикации</span><span class="sxs-lookup"><span data-stu-id="94ad8-161">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="94ad8-162">Управление опубликованным пакетом</span><span class="sxs-lookup"><span data-stu-id="94ad8-162">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="94ad8-163">Добавление файла сведений и других файлов</span><span class="sxs-lookup"><span data-stu-id="94ad8-163">Adding a readme and other files</span></span>

<span data-ttu-id="94ad8-164">Чтобы напрямую указать файлы, включаемые в пакет, измените файл проекта и используйте свойство `content`:</span><span class="sxs-lookup"><span data-stu-id="94ad8-164">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="94ad8-165">В корень пакета будет включен файл с именем `readme.txt`.</span><span class="sxs-lookup"><span data-stu-id="94ad8-165">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="94ad8-166">Visual Studio отображает содержимое этого файла в виде обычного текста сразу после установки пакета напрямую.</span><span class="sxs-lookup"><span data-stu-id="94ad8-166">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="94ad8-167">(Файлы сведений не отображаются для пакетов, устанавливаемых как зависимости.)</span><span class="sxs-lookup"><span data-stu-id="94ad8-167">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="94ad8-168">Например, вот как выглядит файл сведений для пакета HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="94ad8-168">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Отображение файла сведений для пакета NuGet при установке](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="94ad8-170">Обычное добавление файла readme.txt в корень проекта не приведет к включению его в итоговый пакет.</span><span class="sxs-lookup"><span data-stu-id="94ad8-170">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="94ad8-171">См. также</span><span class="sxs-lookup"><span data-stu-id="94ad8-171">Related topics</span></span>

- [<span data-ttu-id="94ad8-172">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="94ad8-172">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="94ad8-173">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="94ad8-173">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="94ad8-174">Пакеты предварительного выпуска</span><span class="sxs-lookup"><span data-stu-id="94ad8-174">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="94ad8-175">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="94ad8-175">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="94ad8-176">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="94ad8-176">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="94ad8-177">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="94ad8-177">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="94ad8-178">Документация по библиотеке .NET Standard</span><span class="sxs-lookup"><span data-stu-id="94ad8-178">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="94ad8-179">Перенос кода в .NET Core из .NET Framework</span><span class="sxs-lookup"><span data-stu-id="94ad8-179">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
