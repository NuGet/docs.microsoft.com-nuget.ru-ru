---
title: Создание и публикация пакета .NET Framework с помощью Visual Studio в Windows
description: Пошаговое руководство по созданию и публикации пакета NuGet .NET Framework с помощью Visual Studio 2017 в Windows.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: ba02b53c6ac0b4172b8611958775980ce401bf9b
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/22/2018
ms.locfileid: "34428819"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="ae538-103">Краткое руководство. Создание и публикация пакета с помощью Visual Studio (.NET Framework, Windows)</span><span class="sxs-lookup"><span data-stu-id="ae538-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="ae538-104">Создание пакета NuGet из библиотеки классов .NET Framework включает в себя создание библиотеки DLL в Visual Studio в Windows и последующее использование программы командной строки nuget.exe для создания и публикации пакета.</span><span class="sxs-lookup"><span data-stu-id="ae538-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="ae538-105">Это краткое руководство относится только к Visual Studio 2017 для Windows.</span><span class="sxs-lookup"><span data-stu-id="ae538-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="ae538-106">Visual Studio для Mac не поддерживает описанные здесь функции.</span><span class="sxs-lookup"><span data-stu-id="ae538-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="ae538-107">Используйте вместо этого [средства интерфейса командной строки dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ae538-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae538-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ae538-108">Prerequisites</span></span>

1. <span data-ttu-id="ae538-109">Установите любой выпуск Visual Studio 2017 со страницы [visualstudio.com](https://www.visualstudio.com/) с помощью любой рабочей нагрузки, связанной с .NET.</span><span class="sxs-lookup"><span data-stu-id="ae538-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="ae538-110">После установки рабочей нагрузки .NET Visual Studio 2017 автоматически добавит возможности NuGet.</span><span class="sxs-lookup"><span data-stu-id="ae538-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="ae538-111">Установите интерфейс командной строки `nuget.exe`, скачав его на сайте [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), и сохраните этот файл `.exe` в подходящую папку. Добавьте эту папку в переменную среды PATH.</span><span class="sxs-lookup"><span data-stu-id="ae538-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="ae538-112">[Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее.</span><span class="sxs-lookup"><span data-stu-id="ae538-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="ae538-113">При создании учетной записи вам направляется сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="ae538-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="ae538-114">Перед отправкой пакета вам нужно подтвердить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ae538-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="ae538-115">Создание проекта библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="ae538-115">Create a class library project</span></span>

<span data-ttu-id="ae538-116">Вы можете использовать имеющийся проект библиотеки классов .NET Framework для кода, который нужно упаковать, или же создать простой проект, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ae538-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="ae538-117">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > Windows**, выберите шаблон "Библиотека классов (.NET Framework)", назовите проект "AppLogger" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ae538-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="ae538-118">Щелкните правой кнопкой мыши полученный файл проекта и выберите пункт **Сборка**, чтобы убедиться, что проект создан правильно.</span><span class="sxs-lookup"><span data-stu-id="ae538-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="ae538-119">Библиотека DLL находится в папке Debug (или папке Release, если вы используете конфигурацию выпуска для сборки).</span><span class="sxs-lookup"><span data-stu-id="ae538-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="ae538-120">В реальном пакете NuGet вы можете реализовать множество полезных возможностей, с помощью которых другие пользователи могут создавать приложения.</span><span class="sxs-lookup"><span data-stu-id="ae538-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="ae538-121">Кроме того, вы можете задать любые подходящие требуемые версии .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ae538-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="ae538-122">Например, см. руководства по [UWP](../guides/create-uwp-packages.md) и [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="ae538-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="ae538-123">Однако в этом пошаговом руководстве вы не будете писать дополнительный код, так как библиотеки классов из шаблона достаточно для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="ae538-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="ae538-124">Тем не менее, вы можете использовать функциональный код для пакета:</span><span class="sxs-lookup"><span data-stu-id="ae538-124">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
using System;

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
> <span data-ttu-id="ae538-125">Для пакетов NuGet мы рекомендуем использовать целевой объект .NET Standard (если нет причин использовать другое), так как он обеспечивает совместимость с рядом потребляющих проектов.</span><span class="sxs-lookup"><span data-stu-id="ae538-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="ae538-126">См. раздел [Создание и публикация пакета с помощью Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="ae538-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="ae538-127">Настройка свойств проекта для пакета</span><span class="sxs-lookup"><span data-stu-id="ae538-127">Configure project properties for the package</span></span>

<span data-ttu-id="ae538-128">Пакет NuGet содержит манифест (файл `.nuspec`) с соответствующими метаданными, такими как идентификатор пакета, номер версии, описание и многое другое.</span><span class="sxs-lookup"><span data-stu-id="ae538-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="ae538-129">Некоторые из них могут поступать напрямую из свойств проекта, в результате чего исчезает необходимость изменять их как в проекте, так и в манифесте.</span><span class="sxs-lookup"><span data-stu-id="ae538-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="ae538-130">Этот раздел описывает, где можно задать соответствующие свойства.</span><span class="sxs-lookup"><span data-stu-id="ae538-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="ae538-131">Выберите команду меню **Проект > Свойства**, а затем щелкните вкладку **Приложение**.</span><span class="sxs-lookup"><span data-stu-id="ae538-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="ae538-132">В поле **Имя сборки** укажите уникальный идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="ae538-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="ae538-133">Необходимо присвоить пакету идентификатор, который будет уникальным на сайте nuget.org или другом используемом узле.</span><span class="sxs-lookup"><span data-stu-id="ae538-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="ae538-134">При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).</span><span class="sxs-lookup"><span data-stu-id="ae538-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="ae538-135">При попытке опубликовать пакет с именем, которое уже занято, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="ae538-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="ae538-136">Нажмите кнопку **Сведения о сборке...**, чтобы открыть диалоговое окно, где можно ввести другие свойства, которые переносятся в манифест (см. [описание токенов замены в справочнике по файлу NUSPEC](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="ae538-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="ae538-137">Чаще всего используются поля **Заголовок**, **Описание**, **Компания**, **Авторские права** и **Версия сборки**.</span><span class="sxs-lookup"><span data-stu-id="ae538-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="ae538-138">В конечном счете эти свойства отображаются вместе с пакетом на узле, таком как nuget.org, поэтому задайте для них очевидное и понятное значение.</span><span class="sxs-lookup"><span data-stu-id="ae538-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Сведения о сборке в проекте .NET Framework в Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="ae538-140">Необязательно. Чтобы просмотреть или изменить свойства напрямую, откройте файл `Properties/AssemblyInfo.cs` в проекте.</span><span class="sxs-lookup"><span data-stu-id="ae538-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="ae538-141">Задав свойства, укажите для конфигурацию проекта значение **Выпуск** и перестройте проект для создания обновленной библиотеки DLL.</span><span class="sxs-lookup"><span data-stu-id="ae538-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="ae538-142">Создание начального манифеста</span><span class="sxs-lookup"><span data-stu-id="ae538-142">Generate the initial manifest</span></span>

<span data-ttu-id="ae538-143">Получив библиотеку DLL и задав свойства проекта, вы можете использовать команду `nuget spec`, чтобы создать начальный файл `.nuspec` из проекта.</span><span class="sxs-lookup"><span data-stu-id="ae538-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="ae538-144">Этот шаг включает в себя соответствующие токены замены для получения сведений из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="ae538-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="ae538-145">Запускать `nuget spec` для создания начального манифеста потребуется всего один раз.</span><span class="sxs-lookup"><span data-stu-id="ae538-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="ae538-146">При обновлении пакета нужно либо изменить значения в проекте, либо отредактировать сам файл манифеста.</span><span class="sxs-lookup"><span data-stu-id="ae538-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="ae538-147">Откройте командную строку и перейдите в папку проекта, содержащую файл `AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="ae538-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="ae538-148">Выполните следующую команду: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="ae538-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="ae538-149">После указания проекта NuGet создает манифест с тем же именем, что и проект, в данном случае это `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ae538-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="ae538-150">Он также включает в себя токены замены из манифеста.</span><span class="sxs-lookup"><span data-stu-id="ae538-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="ae538-151">Откройте файл `AppLogger.nuspec` в текстовом редакторе для просмотра его содержимого, которое должно иметь следующий вид.</span><span class="sxs-lookup"><span data-stu-id="ae538-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="ae538-152">Изменение манифеста</span><span class="sxs-lookup"><span data-stu-id="ae538-152">Edit the manifest</span></span>

1. <span data-ttu-id="ae538-153">NuGet выдает ошибку при попытке создать пакет со значениями по умолчанию в вашем файле `.nuspec`, поэтому перед продолжением нужно изменить следующие поля.</span><span class="sxs-lookup"><span data-stu-id="ae538-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="ae538-154">Их использование описано в [разделе об отдельных элементах в справочнике по файлу NUSPEC](../reference/nuspec.md#single-elements).</span><span class="sxs-lookup"><span data-stu-id="ae538-154">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="ae538-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="ae538-155">licenseUrl</span></span>
    - <span data-ttu-id="ae538-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="ae538-156">projectUrl</span></span>
    - <span data-ttu-id="ae538-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="ae538-157">iconUrl</span></span>
    - <span data-ttu-id="ae538-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="ae538-158">releaseNotes</span></span>
    - <span data-ttu-id="ae538-159">теги</span><span class="sxs-lookup"><span data-stu-id="ae538-159">tags</span></span>

1. <span data-ttu-id="ae538-160">Если пакет будет общедоступным, обратите особое внимание на свойство **Теги**, так как они помогают найти ваш пакет в таких источниках, как nuget.org, и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="ae538-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="ae538-161">Кроме того, сейчас можно добавить в манифест любые другие элементы, как описано в разделе [Справочник по файлу NUSPEC](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="ae538-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="ae538-162">Сохраните файл, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="ae538-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="ae538-163">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="ae538-163">Run the pack command</span></span>

1. <span data-ttu-id="ae538-164">Из командной строки перейдите в папку, содержащую файл `.nuspec`, и выполните команду `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="ae538-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="ae538-165">NuGet создает в текущей папке файл `.nupkg` формата *идентификатор-версия.nupkg*.</span><span class="sxs-lookup"><span data-stu-id="ae538-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="ae538-166">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="ae538-166">Publish the package</span></span>

<span data-ttu-id="ae538-167">Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя `nuget.exe`, а также ключ API, полученный на этом сайте. Для nuget.org нужно использовать `nuget.exe` 4.1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ae538-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="ae538-168">Получение ключа API</span><span class="sxs-lookup"><span data-stu-id="ae538-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="ae538-169">Публикация с помощью команды nuget push</span><span class="sxs-lookup"><span data-stu-id="ae538-169">Publish with nuget push</span></span>

1. <span data-ttu-id="ae538-170">Перейдите в папку, содержащую файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ae538-170">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="ae538-171">Выполните следующую команду, указав имя пакета и заменив значение ключа на ключ API:</span><span class="sxs-lookup"><span data-stu-id="ae538-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="ae538-172">nuget.exe отображает результаты публикации:</span><span class="sxs-lookup"><span data-stu-id="ae538-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="ae538-173">Ознакомьтесь со сведениями о [команде nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="ae538-173">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="ae538-174">Ошибки публикации</span><span class="sxs-lookup"><span data-stu-id="ae538-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="ae538-175">Управление опубликованным пакетом</span><span class="sxs-lookup"><span data-stu-id="ae538-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="ae538-176">См. также</span><span class="sxs-lookup"><span data-stu-id="ae538-176">Related topics</span></span>

- [<span data-ttu-id="ae538-177">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="ae538-177">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="ae538-178">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="ae538-178">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="ae538-179">Пакеты предварительного выпуска</span><span class="sxs-lookup"><span data-stu-id="ae538-179">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="ae538-180">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="ae538-180">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="ae538-181">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="ae538-181">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="ae538-182">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="ae538-182">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
