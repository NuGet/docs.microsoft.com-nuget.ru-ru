---
title: "Вводное руководство по созданию и публикации пакета NuGet .NET Framework с помощью Visual Studio | Документация Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Пошаговое руководство по созданию и публикации пакета NuGet .NET Framework с помощью Visual Studio 2017."
keywords: NuGet package creation, NuGet package publishing, NuGet tutorial, Visual Studio create NuGet package, msbuild pack
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 613cb6e8cf5762f354d69aa271c1e2f0d4851c97
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-framework"></a><span data-ttu-id="09649-104">Создание и публикация пакета с помощью Visual Studio (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="09649-104">Create and publish a package using Visual Studio (.NET Framework)</span></span>

<span data-ttu-id="09649-105">Создание пакета NuGet из библиотеки классов .NET Framework включает в себя создание библиотеки DLL в Visual Studio и последующее использование программы командной строки nuget.exe для создания и публикации пакета.</span><span class="sxs-lookup"><span data-stu-id="09649-105">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio, then using the nuget.exe command line tool to create and publish the package.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09649-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="09649-106">Prerequisites</span></span>

1. <span data-ttu-id="09649-107">Установите любой выпуск Visual Studio 2017 со страницы [visualstudio.com](https://www.visualstudio.com/) с помощью любой рабочей нагрузки, связанной с .NET.</span><span class="sxs-lookup"><span data-stu-id="09649-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="09649-108">После установки рабочей нагрузки .NET Visual Studio 2017 автоматически добавит возможности NuGet.</span><span class="sxs-lookup"><span data-stu-id="09649-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="09649-109">Установите интерфейс командной строки `nuget.exe`, скачав его на сайте [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), и сохраните этот файл `.exe` в подходящую папку. Добавьте эту папку в переменную среды PATH.</span><span class="sxs-lookup"><span data-stu-id="09649-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="09649-110">[Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее.</span><span class="sxs-lookup"><span data-stu-id="09649-110">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="09649-111">При создании учетной записи вам направляется сообщение электронной почты с подтверждением.</span><span class="sxs-lookup"><span data-stu-id="09649-111">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="09649-112">Перед отправкой пакета вам нужно подтвердить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="09649-112">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="09649-113">Создание проекта библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="09649-113">Create a class library project</span></span>

<span data-ttu-id="09649-114">Вы можете использовать имеющийся проект библиотеки классов .NET Framework для кода, который нужно упаковать, или же создать простой проект, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="09649-114">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="09649-115">В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > Windows**, выберите шаблон "Библиотека классов (.NET Framework)", назовите проект "AppLogger" и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="09649-115">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="09649-116">Щелкните правой кнопкой мыши полученный файл проекта и выберите пункт **Сборка**, чтобы убедиться, что проект создан правильно.</span><span class="sxs-lookup"><span data-stu-id="09649-116">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="09649-117">Библиотека DLL находится в папке Debug (или папке Release, если вы используете конфигурацию выпуска для сборки).</span><span class="sxs-lookup"><span data-stu-id="09649-117">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="09649-118">В реальном пакете NuGet вы можете реализовать множество полезных возможностей, с помощью которых другие пользователи могут создавать приложения.</span><span class="sxs-lookup"><span data-stu-id="09649-118">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="09649-119">Кроме того, вы можете задать любые подходящие требуемые версии .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="09649-119">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="09649-120">Например, см. руководства по [UWP](../guides/create-uwp-packages.md) и [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="09649-120">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="09649-121">Однако в этом пошаговом руководстве вы не будете писать дополнительный код, так как библиотеки классов из шаблона достаточно для создания пакета.</span><span class="sxs-lookup"><span data-stu-id="09649-121">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="09649-122">Тем не менее, вы можете использовать функциональный код для пакета:</span><span class="sxs-lookup"><span data-stu-id="09649-122">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="09649-123">Для пакетов NuGet мы рекомендуем использовать целевой объект .NET Standard (если нет причин использовать другое), так как он обеспечивает совместимость с рядом потребляющих проектов.</span><span class="sxs-lookup"><span data-stu-id="09649-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="09649-124">См. раздел [Создание и публикация пакета с помощью Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="09649-124">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="09649-125">Настройка свойств проекта для пакета</span><span class="sxs-lookup"><span data-stu-id="09649-125">Configure project properties for the package</span></span>

<span data-ttu-id="09649-126">Пакет NuGet содержит манифест (файл `.nuspec`) с соответствующими метаданными, такими как идентификатор пакета, номер версии, описание и многое другое.</span><span class="sxs-lookup"><span data-stu-id="09649-126">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="09649-127">Некоторые из них могут поступать напрямую из свойств проекта, в результате чего исчезает необходимость изменять их как в проекте, так и в манифесте.</span><span class="sxs-lookup"><span data-stu-id="09649-127">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="09649-128">Этот раздел описывает, где можно задать соответствующие свойства.</span><span class="sxs-lookup"><span data-stu-id="09649-128">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="09649-129">Выберите команду меню **Проект > Свойства**, а затем щелкните вкладку **Приложение**.</span><span class="sxs-lookup"><span data-stu-id="09649-129">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="09649-130">В поле **Имя сборки** укажите уникальный идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="09649-130">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="09649-131">Необходимо присвоить пакету идентификатор, который будет уникальным на сайте nuget.org или другом используемом узле.</span><span class="sxs-lookup"><span data-stu-id="09649-131">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="09649-132">При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).</span><span class="sxs-lookup"><span data-stu-id="09649-132">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="09649-133">При попытке опубликовать пакет с именем, которое уже занято, появится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="09649-133">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="09649-134">Нажмите кнопку **Сведения о сборке...**, чтобы открыть диалоговое окно, где можно ввести другие свойства, которые переносятся в манифест (см. [описание токенов замены в справочнике по файлу NUSPEC](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="09649-134">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="09649-135">Чаще всего используются поля **Заголовок**, **Описание**, **Компания**, **Авторские права** и **Версия сборки**.</span><span class="sxs-lookup"><span data-stu-id="09649-135">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="09649-136">В конечном счете эти свойства отображаются вместе с пакетом на узле, таком как nuget.org, поэтому задайте для них очевидное и понятное значение.</span><span class="sxs-lookup"><span data-stu-id="09649-136">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Сведения о сборке в проекте .NET Framework в Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="09649-138">Необязательно. Чтобы просмотреть или изменить свойства напрямую, откройте файл `Properties/AssemblyInfo.cs` в проекте.</span><span class="sxs-lookup"><span data-stu-id="09649-138">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="09649-139">Задав свойства, укажите для конфигурацию проекта значение **Выпуск** и перестройте проект для создания обновленной библиотеки DLL.</span><span class="sxs-lookup"><span data-stu-id="09649-139">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="09649-140">Создание начального манифеста</span><span class="sxs-lookup"><span data-stu-id="09649-140">Generate the initial manifest</span></span>

<span data-ttu-id="09649-141">Получив библиотеку DLL и задав свойства проекта, вы можете использовать команду `nuget spec`, чтобы создать начальный файл `.nuspec` из проекта.</span><span class="sxs-lookup"><span data-stu-id="09649-141">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="09649-142">Этот шаг включает в себя соответствующие токены замены для получения сведений из файла проекта.</span><span class="sxs-lookup"><span data-stu-id="09649-142">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="09649-143">Запускать `nuget spec` для создания начального манифеста потребуется всего один раз.</span><span class="sxs-lookup"><span data-stu-id="09649-143">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="09649-144">При обновлении пакета нужно либо изменить значения в проекте, либо отредактировать сам файл манифеста.</span><span class="sxs-lookup"><span data-stu-id="09649-144">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="09649-145">Откройте командную строку и перейдите в папку проекта, содержащую файл `AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="09649-145">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="09649-146">Выполните следующую команду: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="09649-146">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="09649-147">После указания проекта NuGet создает манифест с тем же именем, что и проект, в данном случае это `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="09649-147">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="09649-148">Он также включает в себя токены замены из манифеста.</span><span class="sxs-lookup"><span data-stu-id="09649-148">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="09649-149">Откройте файл `AppLogger.nuspec` в текстовом редакторе для просмотра его содержимого, которое должно иметь следующий вид.</span><span class="sxs-lookup"><span data-stu-id="09649-149">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

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

## <a name="edit-the-manifest"></a><span data-ttu-id="09649-150">Изменение манифеста</span><span class="sxs-lookup"><span data-stu-id="09649-150">Edit the manifest</span></span>

1. <span data-ttu-id="09649-151">NuGet выдает ошибку при попытке создать пакет со значениями по умолчанию в вашем файле `.nuspec`, поэтому перед продолжением нужно изменить следующие поля.</span><span class="sxs-lookup"><span data-stu-id="09649-151">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="09649-152">Их использование описано в [разделе об отдельных элементах в справочнике по файлу NUSPEC](../reference/nuspec.md#single-elements).</span><span class="sxs-lookup"><span data-stu-id="09649-152">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="09649-153">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="09649-153">licenseUrl</span></span>
    - <span data-ttu-id="09649-154">projectUrl</span><span class="sxs-lookup"><span data-stu-id="09649-154">projectUrl</span></span>
    - <span data-ttu-id="09649-155">iconUrl</span><span class="sxs-lookup"><span data-stu-id="09649-155">iconUrl</span></span>
    - <span data-ttu-id="09649-156">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="09649-156">releaseNotes</span></span>
    - <span data-ttu-id="09649-157">теги</span><span class="sxs-lookup"><span data-stu-id="09649-157">tags</span></span>

1. <span data-ttu-id="09649-158">Если пакет будет общедоступным, обратите особое внимание на свойство **Теги**, так как они помогают найти ваш пакет в таких источниках, как nuget.org, и понять его назначение.</span><span class="sxs-lookup"><span data-stu-id="09649-158">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="09649-159">Кроме того, сейчас можно добавить в манифест любые другие элементы, как описано в разделе [Справочник по файлу NUSPEC](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="09649-159">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="09649-160">Сохраните файл, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="09649-160">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="09649-161">Выполнение команды pack</span><span class="sxs-lookup"><span data-stu-id="09649-161">Run the pack command</span></span>

1. <span data-ttu-id="09649-162">Из командной строки перейдите в папку, содержащую файл `.nuspec`, и выполните команду `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="09649-162">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="09649-163">NuGet создает в текущей папке файл `.nupkg` формата *идентификатор-версия.nupkg*.</span><span class="sxs-lookup"><span data-stu-id="09649-163">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="09649-164">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="09649-164">Publish the package</span></span>

<span data-ttu-id="09649-165">Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя `nuget.exe`, а также ключ API, полученный на этом сайте. Для nuget.org нужно использовать `nuget.exe` 4.1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="09649-165">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="09649-166">Получение ключа API</span><span class="sxs-lookup"><span data-stu-id="09649-166">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="09649-167">Публикация с помощью команды nuget push</span><span class="sxs-lookup"><span data-stu-id="09649-167">Publish with nuget push</span></span>

1. <span data-ttu-id="09649-168">Перейдите в папку, содержащую файл `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="09649-168">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="09649-169">Выполните следующую команду, указав имя пакета и заменив значение ключа на ключ API:</span><span class="sxs-lookup"><span data-stu-id="09649-169">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="09649-170">nuget.exe отображает результаты публикации:</span><span class="sxs-lookup"><span data-stu-id="09649-170">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="09649-171">Ознакомьтесь со сведениями о [команде nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="09649-171">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="09649-172">Ошибки публикации</span><span class="sxs-lookup"><span data-stu-id="09649-172">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="09649-173">Управление опубликованным пакетом</span><span class="sxs-lookup"><span data-stu-id="09649-173">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="09649-174">См. также</span><span class="sxs-lookup"><span data-stu-id="09649-174">Related topics</span></span>

- [<span data-ttu-id="09649-175">Создание пакета</span><span class="sxs-lookup"><span data-stu-id="09649-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="09649-176">Публикация пакета</span><span class="sxs-lookup"><span data-stu-id="09649-176">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="09649-177">Поддержка нескольких целевых платформ</span><span class="sxs-lookup"><span data-stu-id="09649-177">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="09649-178">Управление версиями пакета</span><span class="sxs-lookup"><span data-stu-id="09649-178">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="09649-179">Создание локализованных пакетов</span><span class="sxs-lookup"><span data-stu-id="09649-179">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
