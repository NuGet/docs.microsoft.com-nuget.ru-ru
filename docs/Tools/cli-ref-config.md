---
title: Команды NuGet CLI config | Документы Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Ссылка для выполнения команды конфигурации nuget.exe
keywords: Справочник по конфигурации NuGet, команда конфигурации
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e3d08f210bd56fcb8eb701fc9b241a3ab45998ec
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="f1977-104">Команда config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f1977-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="f1977-105">**Применяется к:** все &bullet; **поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="f1977-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="f1977-106">Возвращает или задает значения конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="f1977-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="f1977-107">Дополнительные использования см. [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f1977-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="f1977-108">Дополнительные сведения на допустимые имена ключей [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="f1977-108">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f1977-109">Использование</span><span class="sxs-lookup"><span data-stu-id="f1977-109">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="f1977-110">где `<name>` и `<value>` укажите пару "ключ значение" для установки в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f1977-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="f1977-111">При желании можно указать столько пар.</span><span class="sxs-lookup"><span data-stu-id="f1977-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="f1977-112">Чтобы удалить значение, укажите имя и `=` входа, но нет значения.</span><span class="sxs-lookup"><span data-stu-id="f1977-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="f1977-113">Допустимые имена ключей, в разделе [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="f1977-113">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="f1977-114">В NuGet 3.4 + `<value>` можно использовать [переменных среды](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="f1977-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="f1977-115">Параметры</span><span class="sxs-lookup"><span data-stu-id="f1977-115">Options</span></span>

| <span data-ttu-id="f1977-116">Параметр</span><span class="sxs-lookup"><span data-stu-id="f1977-116">Option</span></span> | <span data-ttu-id="f1977-117">Описание</span><span class="sxs-lookup"><span data-stu-id="f1977-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1977-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="f1977-118">AsPath</span></span> | <span data-ttu-id="f1977-119">Возвращает значение конфигурации как путь, игнорируются, когда `-Set` используется.</span><span class="sxs-lookup"><span data-stu-id="f1977-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="f1977-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f1977-120">ConfigFile</span></span> | <span data-ttu-id="f1977-121">Файл конфигурации NuGet для изменения.</span><span class="sxs-lookup"><span data-stu-id="f1977-121">The NuGet configuration file to modify.</span></span> <span data-ttu-id="f1977-122">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="f1977-122">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f1977-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f1977-123">ForceEnglishOutput</span></span> | <span data-ttu-id="f1977-124">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="f1977-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f1977-125">Справка</span><span class="sxs-lookup"><span data-stu-id="f1977-125">Help</span></span> | <span data-ttu-id="f1977-126">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="f1977-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="f1977-127">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="f1977-127">NonInteractive</span></span> | <span data-ttu-id="f1977-128">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="f1977-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f1977-129">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="f1977-129">Verbosity</span></span> | <span data-ttu-id="f1977-130">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="f1977-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f1977-131">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f1977-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="f1977-132">Примеры</span><span class="sxs-lookup"><span data-stu-id="f1977-132">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
