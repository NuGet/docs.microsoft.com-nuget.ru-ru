---
title: "Создание собственных пакетов NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Сведения о создании собственных пакетов NuGet, которые содержат код C++ вместо управляемого кода, для использования в проектах C++."
keywords: "собственные пакеты NuGet, пакеты NuGet C++, пакеты с машинным кодом, ориентация на проекты C++"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 71f4eca411d520630ca7d77165b8f03cd32af290
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2018
---
# <a name="creating-native-packages"></a><span data-ttu-id="d84e3-104">Создание собственных пакетов</span><span class="sxs-lookup"><span data-stu-id="d84e3-104">Creating native packages</span></span>

<span data-ttu-id="d84e3-105">Собственный пакет содержит машинный код C++, а не управляемый код, что позволяет использовать его в проектах C++.</span><span class="sxs-lookup"><span data-stu-id="d84e3-105">A native package contains native C++ code instead of managed code, allowing it to be used within C++ projects.</span></span> <span data-ttu-id="d84e3-106">(См. [Собственные пакеты C++](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) в разделе "Использование".)</span><span class="sxs-lookup"><span data-stu-id="d84e3-106">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) in the Consume section.)</span></span>

<span data-ttu-id="d84e3-107">Для использования в проекте C++ пакет должен быть ориентирован на платформу `native`.</span><span class="sxs-lookup"><span data-stu-id="d84e3-107">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="d84e3-108">Сейчас нет номеров версий, связанных с этой платформой, так как NuGet обрабатывает все проекты C++ одинаково.</span><span class="sxs-lookup"><span data-stu-id="d84e3-108">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="d84e3-109">Не забудьте включить *native* в раздел `<tags>` вашего `.nuspec`, чтобы помочь другим разработчикам найти ваш пакет по этому тегу.</span><span class="sxs-lookup"><span data-stu-id="d84e3-109">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="d84e3-110">Собственные пакеты NuGet, ориентированные на `native`, предоставляют файлы в папках `\build`, `\content` и `\tools`; `\lib` в этом случае не используется (NuGet не может добавлять ссылки непосредственно на проект C++).</span><span class="sxs-lookup"><span data-stu-id="d84e3-110">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="d84e3-111">Пакет может также содержать целевые объекты и файлы свойств в `\build`, которые NuGet автоматически импортирует в проекты, использующие этот пакет.</span><span class="sxs-lookup"><span data-stu-id="d84e3-111">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="d84e3-112">Эти файлы должны называться так же, как и идентификатор пакета, и иметь расширения `.targets` и (или) `.props`.</span><span class="sxs-lookup"><span data-stu-id="d84e3-112">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="d84e3-113">Например, пакет [cpprestsdk](https://nuget.org/packages/cpprestsdk/) содержит файл `cpprestsdk.targets` в своей папке `\build`.</span><span class="sxs-lookup"><span data-stu-id="d84e3-113">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="d84e3-114">Папку `\build` можно использовать для всех пакетов NuGet, а не только для собственных пакетов.</span><span class="sxs-lookup"><span data-stu-id="d84e3-114">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="d84e3-115">Папка `\build` учитывает целевые платформы так же, как и папки `\content`, `\lib` и `\tools`.</span><span class="sxs-lookup"><span data-stu-id="d84e3-115">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="d84e3-116">Это означает, что вы можете создать папку `\build\net40` и папку `\build\net45`, и NuGet импортирует необходимые файлы свойств и целевых объектов в проект.</span><span class="sxs-lookup"><span data-stu-id="d84e3-116">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="d84e3-117">(Использовать скрипты PowerShell для импорта целевых объектов MSBuild не требуется.)</span><span class="sxs-lookup"><span data-stu-id="d84e3-117">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
