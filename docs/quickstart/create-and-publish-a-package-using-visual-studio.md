---
title: Создание и публикация пакета .NET Standard с помощью Visual Studio в Windows
description: Пошаговое руководство по созданию и публикации пакета NuGet .NET Standard с помощью Visual Studio 2017 в Windows.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: d30e89473b5f00895136b75a90d8d95b7645a100
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812979"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="799da-103">Краткое руководство. Создание и публикация пакета NuGet с помощью Visual Studio (.NET Standard, только для Windows)</span><span class="sxs-lookup"><span data-stu-id="799da-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="799da-104">Создание пакета NuGet из библиотеки классов .NET Standard в Visual Studio в Windows и его публикация на сайте nuget.org с помощью средства интерфейса командной строки выполняются очень просто.</span><span class="sxs-lookup"><span data-stu-id="799da-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="799da-105">Это краткое руководство относится только к Visual Studio 2017 для Windows.</span><span class="sxs-lookup"><span data-stu-id="799da-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="799da-106">Visual Studio для Mac не поддерживает описанные здесь функции.</span><span class="sxs-lookup"><span data-stu-id="799da-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="799da-107">Используйте вместо этого [средства интерфейса командной строки dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="799da-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="799da-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="799da-108">Prerequisites</span></span>

1. <span data-ttu-id="799da-109">Установите любой выпуск Visual Studio 2017 со страницы [visualstudio.com](https://www.visualstudio.com/) с помощью любой рабочей нагрузки, связанной с .NET.</span><span class="sxs-lookup"><span data-stu-id="799da-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="799da-110">После установки рабочей нагрузки .NET Visual Studio 2017 автоматически добавит возможности NuGet.</span><span class="sxs-lookup"><span data-stu-id="799da-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="799da-111">Установите одно из средств CLI.</span><span class="sxs-lookup"><span data-stu-id="799da-111">Install one of the CLI tools.</span></span>

   * <span data-ttu-id="799da-112">Для средства CLI `dotnet` установите [пакет SDK для .NET Core](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="799da-112">For the `dotnet` CLI, install the [.NET Core SDK](https://www.microsoft.com/net/download/).</span></span> <span data-ttu-id="799da-113">CLI для .NET является обязательным для проектов .NET Standard с форматом в стиле пакета SDK (атрибут SDK).</span><span class="sxs-lookup"><span data-stu-id="799da-113">The dotnet CLI is required for .NET Standard projects that use the SDK-style format (SDK attribute).</span></span>

   * <span data-ttu-id="799da-114">Установите средство CLI `nuget.exe`, скачав его на сайте [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), и сохраните этот файл `.exe` в подходящую папку. Добавьте эту папку в переменную среды PATH.</span><span class="sxs-lookup"><span data-stu-id="799da-114">For the `nuget.exe` CLI, download it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving the `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span> <span data-ttu-id="799da-115">CLI nuget.exe используется для библиотек .NET Standard в формате со стилем, отличным от пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="799da-115">The nuget.exe CLI is used for .NET Standard libraries in the non-SDK-style format.</span></span>

1. <span data-ttu-id="799da-116">[Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее.</span><span class="sxs-lookup"><span data-stu-id="799da-116">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="799da-117">При создании учетной записи вам направляется сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="799da-117">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="799da-118">Перед отправкой пакета вам нужно подтвердить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="799da-118">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="799da-119">Создание проекта библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="799da-119">Create a class library project</span></span>

<span data-ttu-id="799da-120">Вы можете использовать имеющийся проект библиотеки классов .NET Standard для кода, который нужно упаковать, или же создать простой проект, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="799da-120">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="799da-121">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > .NET Standard**, выберите шаблон "Библиотека классов (.NET Standard)", назовите проект AppLogger и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="799da-121">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="799da-122">Щелкните правой кнопкой мыши полученный файл проекта и выберите пункт **Сборка**, чтобы убедиться, что проект создан правильно.</span><span class="sxs-lookup"><span data-stu-id="799da-122">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="799da-123">Библиотека DLL находится в папке Debug (или папке Release, если вы используете конфигурацию выпуска для сборки).</span><span class="sxs-lookup"><span data-stu-id="799da-123">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="799da-124">В реальном пакете NuGet вы можете реализовать множество полезных возможностей, с помощью которых другие пользователи могут создавать приложения.</span><span class="sxs-lookup"><span data-stu-id="799da-124">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="799da-125">Однако в этом пошаговом руководстве вы не будете писать дополнительный код, так как библиотеки классов из шаблона достаточно для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="799da-125">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="799da-126">Тем не менее, вы можете использовать функциональный код для пакета:</span><span class="sxs-lookup"><span data-stu-id="799da-126">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="799da-127">Для пакетов NuGet мы рекомендуем использовать целевой объект .NET Standard (если нет причин использовать другое), так как он обеспечивает совместимость с рядом потребляющих проектов.</span><span class="sxs-lookup"><span data-stu-id="799da-127">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="799da-128">Настройка свойств пакета</span><span class="sxs-lookup"><span data-stu-id="799da-128">Configure package properties</span></span>

1. <span data-ttu-id="799da-129">Выберите команду меню **Проект > Свойства**, а затем щелкните вкладку **Пакет**. (Вкладка **Пакет** отображается только для проектов библиотек классов .NET Standard. Если вы ориентируетесь на .NET Framework, см. вместо этого раздел [Создание и публикация пакета .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="799da-129">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="799da-130">Если она не отображается в проекте .NET Standard, может потребоваться обновить Visual Studio 2017 до последней версии.)</span><span class="sxs-lookup"><span data-stu-id="799da-130">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Свойства пакета NuGet в проекте Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="799da-132">Если пакет будет общедоступным, обратите особое внимание на свойство **Теги**, так как они помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="799da-132">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="799da-133">Присвойте пакету уникальный идентификатор и заполните нужные свойства.</span><span class="sxs-lookup"><span data-stu-id="799da-133">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="799da-134">Описание различных свойств см. в [справочнике по NUSPEC-файлу](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="799da-134">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="799da-135">Все свойства добавляются в манифест `.nuspec`, который Visual Studio создает для проекта.</span><span class="sxs-lookup"><span data-stu-id="799da-135">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="799da-136">Необходимо присвоить пакету идентификатор, который будет уникальным на сайте nuget.org или другом используемом узле.</span><span class="sxs-lookup"><span data-stu-id="799da-136">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="799da-137">При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).</span><span class="sxs-lookup"><span data-stu-id="799da-137">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="799da-138">При попытке опубликовать пакет с именем, которое уже занято, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="799da-138">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="799da-139">Необязательно. Чтобы просматривать свойства непосредственно в файле проекта, щелкните правой кнопкой мыши проект в обозревателе решений и выберите **Изменить AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="799da-139">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="799da-140">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="799da-140">Run the pack command</span></span>

1. <span data-ttu-id="799da-141">Выберите конфигурацию **Выпуск**.</span><span class="sxs-lookup"><span data-stu-id="799da-141">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="799da-142">Щелкните проект правой кнопкой мыши в окне **обозревателя решений** и выберите команду **Паковать**:</span><span class="sxs-lookup"><span data-stu-id="799da-142">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Команда "Паковать" для NuGet в контекстном меню проекта Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="799da-144">Visual Studio создаст проект и файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="799da-144">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="799da-145">Ознакомьтесь с результатами в окне **выходных данных** (пример приведен ниже), где содержится путь к файлу пакета.</span><span class="sxs-lookup"><span data-stu-id="799da-145">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="799da-146">Обратите внимание, что созданная сборка находится в папке `bin\Release\netstandard2.0`, которая является целевой для .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="799da-146">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="799da-147">Альтернативный вариант: упаковка с помощью MSBuild</span><span class="sxs-lookup"><span data-stu-id="799da-147">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="799da-148">В качестве альтернативы команде меню **Pack** в NuGet 4.x+ и MSBuild 15.1+ можно использовать целевой объект `pack`, когда проект содержит необходимые данные о пакете.</span><span class="sxs-lookup"><span data-stu-id="799da-148">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="799da-149">Откройте командную строку, перейдите в папку проекта и запустите приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="799da-149">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="799da-150">(В общем случае следует запустить Командную строку разработчика для Visual Studio из меню "Пуск", так как в этом случае настраиваются все необходимые пути для MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="799da-150">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="799da-151">Этот пакет должен находиться в папке `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="799da-151">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="799da-152">Дополнительные сведения об использовании `msbuild -t:pack` см. в описании [объектов pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="799da-152">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="799da-153">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="799da-153">Publish the package</span></span>

<span data-ttu-id="799da-154">Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя интерфейс командной строки `nuget.exe` или `dotnet.exe`, а также ключ API, полученный на этом сайте.</span><span class="sxs-lookup"><span data-stu-id="799da-154">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="799da-155">Получение ключа API</span><span class="sxs-lookup"><span data-stu-id="799da-155">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="799da-156">Публикация с помощью команды dotnet nuget push (CLI для .NET)</span><span class="sxs-lookup"><span data-stu-id="799da-156">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="799da-157">Эту команду можно использовать вместо `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="799da-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="799da-158">Публикация с помощью команды nuget push (CLI nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="799da-158">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="799da-159">Эту команду можно использовать вместо `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="799da-159">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="799da-160">Перейдите в папку, содержащую файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="799da-160">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="799da-161">Выполните следующую команду, указав имя пакета и заменив значение ключа на ключ API:</span><span class="sxs-lookup"><span data-stu-id="799da-161">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="799da-162">nuget.exe отображает результаты публикации:</span><span class="sxs-lookup"><span data-stu-id="799da-162">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="799da-163">Ознакомьтесь со сведениями о [команде nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="799da-163">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="799da-164">Ошибки публикации</span><span class="sxs-lookup"><span data-stu-id="799da-164">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="799da-165">Управление опубликованным пакетом</span><span class="sxs-lookup"><span data-stu-id="799da-165">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="799da-166">Добавление файла сведений и других файлов</span><span class="sxs-lookup"><span data-stu-id="799da-166">Adding a readme and other files</span></span>

<span data-ttu-id="799da-167">Чтобы напрямую указать файлы, включаемые в пакет, измените файл проекта и используйте свойство `content`:</span><span class="sxs-lookup"><span data-stu-id="799da-167">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="799da-168">В корень пакета будет включен файл с именем `readme.txt`.</span><span class="sxs-lookup"><span data-stu-id="799da-168">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="799da-169">Visual Studio отображает содержимое этого файла в виде обычного текста сразу после установки пакета напрямую.</span><span class="sxs-lookup"><span data-stu-id="799da-169">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="799da-170">(Файлы сведений не отображаются для пакетов, устанавливаемых как зависимости.)</span><span class="sxs-lookup"><span data-stu-id="799da-170">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="799da-171">Например, вот как выглядит файл сведений для пакета HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="799da-171">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Отображение файла сведений для пакета NuGet при установке](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="799da-173">Обычное добавление файла readme.txt в корень проекта не приведет к включению его в итоговый пакет.</span><span class="sxs-lookup"><span data-stu-id="799da-173">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="799da-174">См. также</span><span class="sxs-lookup"><span data-stu-id="799da-174">Related topics</span></span>

- [<span data-ttu-id="799da-175">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="799da-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="799da-176">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="799da-176">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="799da-177">Пакеты предварительного выпуска</span><span class="sxs-lookup"><span data-stu-id="799da-177">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="799da-178">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="799da-178">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="799da-179">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="799da-179">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="799da-180">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="799da-180">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="799da-181">Документация по библиотеке .NET Standard</span><span class="sxs-lookup"><span data-stu-id="799da-181">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="799da-182">Перенос кода в .NET Core из .NET Framework</span><span class="sxs-lookup"><span data-stu-id="799da-182">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
