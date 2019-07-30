---
title: Создание и публикация пакета NuGet .NET Standard с помощью Visual Studio в Windows
description: Пошаговое руководство по созданию и публикации пакета NuGet .NET Standard с помощью Visual Studio в Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 86e71460094de9b799384db83456a68db57647af
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419926"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="b04ae-103">Краткое руководство. Создание и публикация пакета NuGet с помощью Visual Studio (.NET Standard, только для Windows)</span><span class="sxs-lookup"><span data-stu-id="b04ae-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="b04ae-104">Создание пакета NuGet из библиотеки классов .NET Standard в Visual Studio в Windows и его публикация на сайте nuget.org с помощью средства интерфейса командной строки выполняются очень просто.</span><span class="sxs-lookup"><span data-stu-id="b04ae-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="b04ae-105">Если вы используете Visual Studio для Mac, ознакомьтесь с [этими сведениями](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) о создании пакета NuGet или примените [средства CLI dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b04ae-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b04ae-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b04ae-106">Prerequisites</span></span>

1. <span data-ttu-id="b04ae-107">Установите любой выпуск Visual Studio 2017 или более поздней версии со страницы [visualstudio.com](https://www.visualstudio.com/) с помощью рабочей нагрузки, связанной с .NET. Core.</span><span class="sxs-lookup"><span data-stu-id="b04ae-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="b04ae-108">При необходимости установите CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="b04ae-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="b04ae-109">Для CLI `dotnet` начиная с версии Visual Studio 2017 CLI `dotnet` автоматически устанавливается вместе с любыми рабочими нагрузками, связанными с .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b04ae-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="b04ae-110">При использовании другой версии установите [пакет SDK для .NET Core](https://www.microsoft.com/net/download/), чтобы получить CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="b04ae-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="b04ae-111">CLI `dotnet` является обязательным для проектов .NET Standard с [форматом в стиле пакета SDK](../resources/check-project-format.md) (атрибут SDK).</span><span class="sxs-lookup"><span data-stu-id="b04ae-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="b04ae-112">Шаблон библиотеки классов по умолчанию в Visual Studio 2017 и более поздних версий, который применяется в рамках этой статьи, использует атрибут пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="b04ae-112">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="b04ae-113">В рамках этой статьи рекомендуем использовать CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="b04ae-113">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="b04ae-114">Любой пакет NuGet можно опубликовать с помощью CLI `nuget.exe`. Но некоторые действия, описанные в этой статье, относятся к проектам в стиле пакета SDK и CLI dotnet.</span><span class="sxs-lookup"><span data-stu-id="b04ae-114">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="b04ae-115">CLI nuget.exe используется для [проектов не в стиле пакета SDK](../resources/check-project-format.md) (в основном для проектов .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="b04ae-115">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="b04ae-116">Если вы работаете с проектом не в стиле SDK, выполните инструкции по [созданию и публикации пакета .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="b04ae-116">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="b04ae-117">[Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account), если вы не сделали этого ранее.</span><span class="sxs-lookup"><span data-stu-id="b04ae-117">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="b04ae-118">При создании учетной записи вам направляется сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="b04ae-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="b04ae-119">Перед отправкой пакета вам нужно подтвердить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="b04ae-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="b04ae-120">Создание проекта библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="b04ae-120">Create a class library project</span></span>

<span data-ttu-id="b04ae-121">Вы можете использовать имеющийся проект библиотеки классов .NET Standard для кода, который нужно упаковать, или же создать простой проект, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b04ae-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="b04ae-122">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > .NET Standard**, выберите шаблон "Библиотека классов (.NET Standard)", назовите проект AppLogger и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b04ae-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="b04ae-123">Щелкните правой кнопкой мыши полученный файл проекта и выберите пункт **Сборка**, чтобы убедиться, что проект создан правильно.</span><span class="sxs-lookup"><span data-stu-id="b04ae-123">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="b04ae-124">Библиотека DLL находится в папке Debug (или папке Release, если вы используете конфигурацию выпуска для сборки).</span><span class="sxs-lookup"><span data-stu-id="b04ae-124">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="b04ae-125">В реальном пакете NuGet вы можете реализовать множество полезных возможностей, с помощью которых другие пользователи могут создавать приложения.</span><span class="sxs-lookup"><span data-stu-id="b04ae-125">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="b04ae-126">Однако в этом пошаговом руководстве вы не будете писать дополнительный код, так как библиотеки классов из шаблона достаточно для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="b04ae-126">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="b04ae-127">Тем не менее, вы можете использовать функциональный код для пакета:</span><span class="sxs-lookup"><span data-stu-id="b04ae-127">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="b04ae-128">Для пакетов NuGet мы рекомендуем использовать целевой объект .NET Standard (если нет причин использовать другое), так как он обеспечивает совместимость с рядом потребляющих проектов.</span><span class="sxs-lookup"><span data-stu-id="b04ae-128">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="b04ae-129">Настройка свойств пакета</span><span class="sxs-lookup"><span data-stu-id="b04ae-129">Configure package properties</span></span>

1. <span data-ttu-id="b04ae-130">Щелкните правой кнопкой мыши проект в обозреватель решений и выберите команду меню **Свойства**, а затем выберите вкладку **Пакет**.</span><span class="sxs-lookup"><span data-stu-id="b04ae-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="b04ae-131">Вкладка **Пакет** отображается только для проектов в стиле SDK в Visual Studio, в основном для проектов .NET Standard или библиотеки классов .NET Core. Если вы используете проект не в стиле SDK (например, проект .NET Framework), [перенесите проект](../reference/migrate-packages-config-to-package-reference.md) и используйте CLI `dotnet`. Или ознакомьтесь с пошаговыми инструкциями по [созданию и публикации пакета .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md)[.](create-and-publish-a-package-using-visual-studio-net-framework.md)</span><span class="sxs-lookup"><span data-stu-id="b04ae-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Свойства пакета NuGet в проекте Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="b04ae-133">Если пакет будет общедоступным, обратите особое внимание на свойство **Теги**, так как они помогают найти ваш пакет и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="b04ae-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="b04ae-134">Присвойте пакету уникальный идентификатор и заполните нужные свойства.</span><span class="sxs-lookup"><span data-stu-id="b04ae-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="b04ae-135">Описание различных свойств см. в [справочнике по NUSPEC-файлу](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="b04ae-135">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="b04ae-136">Все свойства добавляются в манифест `.nuspec`, который Visual Studio создает для проекта.</span><span class="sxs-lookup"><span data-stu-id="b04ae-136">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="b04ae-137">Необходимо присвоить пакету идентификатор, который будет уникальным на сайте nuget.org или другом используемом узле.</span><span class="sxs-lookup"><span data-stu-id="b04ae-137">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="b04ae-138">При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).</span><span class="sxs-lookup"><span data-stu-id="b04ae-138">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="b04ae-139">При попытке опубликовать пакет с именем, которое уже занято, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="b04ae-139">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="b04ae-140">Необязательно. Чтобы просматривать свойства непосредственно в файле проекта, щелкните правой кнопкой мыши проект в обозревателе решений и выберите **Изменить AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="b04ae-140">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="b04ae-141">Этот параметр доступен для проектов, использующих атрибут стиля пакета SDK, только в версиях начиная с Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b04ae-141">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="b04ae-142">Если у вас другой сценарий, щелкните проект правой кнопкой мыши и выберите пункт **Выгрузить проект**.</span><span class="sxs-lookup"><span data-stu-id="b04ae-142">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="b04ae-143">Затем щелкните правой кнопкой мыши выгруженный проект и выберите команду **изменения AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="b04ae-143">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="b04ae-144">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="b04ae-144">Run the pack command</span></span>

1. <span data-ttu-id="b04ae-145">Выберите конфигурацию **Выпуск**.</span><span class="sxs-lookup"><span data-stu-id="b04ae-145">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="b04ae-146">Щелкните проект правой кнопкой мыши в окне **обозревателя решений** и выберите команду **Паковать**:</span><span class="sxs-lookup"><span data-stu-id="b04ae-146">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Команда "Паковать" для NuGet в контекстном меню проекта Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="b04ae-148">Если команда **Pack** не отображается, проект, скорее всего, не разработан в стиле SDK. В таком случае нужно использовать CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="b04ae-148">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="b04ae-149">[Перенесите проект](../reference/migrate-packages-config-to-package-reference.md) и используйте CLI `dotnet`, или ознакомьтесь с пошаговыми инструкциями по [созданию и публикации пакета .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="b04ae-149">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="b04ae-150">Visual Studio создаст проект и файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="b04ae-150">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="b04ae-151">Ознакомьтесь с результатами в окне **выходных данных** (пример приведен ниже), где содержится путь к файлу пакета.</span><span class="sxs-lookup"><span data-stu-id="b04ae-151">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="b04ae-152">Обратите внимание, что созданная сборка находится в папке `bin\Release\netstandard2.0`, которая является целевой для .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="b04ae-152">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="b04ae-153">Альтернативный вариант: упаковка с помощью MSBuild</span><span class="sxs-lookup"><span data-stu-id="b04ae-153">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="b04ae-154">В качестве альтернативы команде меню **Pack** в NuGet 4.x+ и MSBuild 15.1+ можно использовать целевой объект `pack`, когда проект содержит необходимые данные о пакете.</span><span class="sxs-lookup"><span data-stu-id="b04ae-154">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="b04ae-155">Откройте командную строку, перейдите в папку проекта и запустите приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="b04ae-155">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="b04ae-156">(В общем случае следует запустить Командную строку разработчика для Visual Studio из меню "Пуск", так как в этом случае настраиваются все необходимые пути для MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="b04ae-156">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="b04ae-157">Этот пакет должен находиться в папке `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="b04ae-157">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="b04ae-158">Дополнительные сведения об использовании `msbuild -t:pack` см. в описании [объектов pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="b04ae-158">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="b04ae-159">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="b04ae-159">Publish the package</span></span>

<span data-ttu-id="b04ae-160">Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя интерфейс командной строки `nuget.exe` или `dotnet.exe`, а также ключ API, полученный на этом сайте.</span><span class="sxs-lookup"><span data-stu-id="b04ae-160">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="b04ae-161">Получение ключа API</span><span class="sxs-lookup"><span data-stu-id="b04ae-161">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="b04ae-162">Публикация с помощью команды dotnet nuget push (CLI для .NET)</span><span class="sxs-lookup"><span data-stu-id="b04ae-162">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="b04ae-163">Этот шаг — рекомендуемая альтернатива использования `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="b04ae-163">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="b04ae-164">Перед публикацией пакета сначала нужно открыть командную строку.</span><span class="sxs-lookup"><span data-stu-id="b04ae-164">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="b04ae-165">Публикация с помощью команды nuget push (CLI nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="b04ae-165">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="b04ae-166">Эту команду можно использовать вместо `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="b04ae-166">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="b04ae-167">Откройте командную строку и перейдите к папке с файлом `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="b04ae-167">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="b04ae-168">Выполните следующую команду, указав имя пакета (уникальный идентификатор пакета) и заменив значение ключа ключом API:</span><span class="sxs-lookup"><span data-stu-id="b04ae-168">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="b04ae-169">nuget.exe отображает результаты публикации:</span><span class="sxs-lookup"><span data-stu-id="b04ae-169">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="b04ae-170">Ознакомьтесь со сведениями о [команде nuget push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="b04ae-170">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="b04ae-171">Ошибки публикации</span><span class="sxs-lookup"><span data-stu-id="b04ae-171">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="b04ae-172">Управление опубликованным пакетом</span><span class="sxs-lookup"><span data-stu-id="b04ae-172">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="b04ae-173">Добавление файла сведений и других файлов</span><span class="sxs-lookup"><span data-stu-id="b04ae-173">Adding a readme and other files</span></span>

<span data-ttu-id="b04ae-174">Чтобы напрямую указать файлы, включаемые в пакет, измените файл проекта и используйте свойство `content`:</span><span class="sxs-lookup"><span data-stu-id="b04ae-174">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="b04ae-175">В корень пакета будет включен файл с именем `readme.txt`.</span><span class="sxs-lookup"><span data-stu-id="b04ae-175">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="b04ae-176">Visual Studio отображает содержимое этого файла в виде обычного текста сразу после установки пакета напрямую.</span><span class="sxs-lookup"><span data-stu-id="b04ae-176">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="b04ae-177">(Файлы сведений не отображаются для пакетов, устанавливаемых как зависимости.)</span><span class="sxs-lookup"><span data-stu-id="b04ae-177">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="b04ae-178">Например, вот как выглядит файл сведений для пакета HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="b04ae-178">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Отображение файла сведений для пакета NuGet при установке](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="b04ae-180">Обычное добавление файла readme.txt в корень проекта не приведет к включению его в итоговый пакет.</span><span class="sxs-lookup"><span data-stu-id="b04ae-180">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="b04ae-181">См. также</span><span class="sxs-lookup"><span data-stu-id="b04ae-181">Related topics</span></span>

- [<span data-ttu-id="b04ae-182">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="b04ae-182">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="b04ae-183">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="b04ae-183">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="b04ae-184">Пакеты предварительного выпуска</span><span class="sxs-lookup"><span data-stu-id="b04ae-184">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="b04ae-185">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="b04ae-185">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="b04ae-186">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="b04ae-186">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="b04ae-187">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="b04ae-187">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="b04ae-188">Документация по библиотеке .NET Standard</span><span class="sxs-lookup"><span data-stu-id="b04ae-188">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="b04ae-189">Перенос кода в .NET Core из .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b04ae-189">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
