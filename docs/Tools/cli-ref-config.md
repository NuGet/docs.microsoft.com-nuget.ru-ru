---
title: Команда config NuGet CLI
description: Ссылка для выполнения команды конфигурации nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 414eb8386f949347772f33170de881534dc71482
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="27b20-103">Команда config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="27b20-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="27b20-104">**Применяется к:** все &bullet; **поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="27b20-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="27b20-105">Возвращает или задает значения конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="27b20-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="27b20-106">Дополнительные использования см. [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="27b20-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="27b20-107">Дополнительные сведения на допустимые имена ключей [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="27b20-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="27b20-108">Использование</span><span class="sxs-lookup"><span data-stu-id="27b20-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="27b20-109">где `<name>` и `<value>` укажите пару "ключ значение" для установки в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="27b20-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="27b20-110">При желании можно указать столько пар.</span><span class="sxs-lookup"><span data-stu-id="27b20-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="27b20-111">Чтобы удалить значение, укажите имя и `=` входа, но нет значения.</span><span class="sxs-lookup"><span data-stu-id="27b20-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="27b20-112">Допустимые имена ключей, в разделе [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="27b20-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="27b20-113">В NuGet 3.4 + `<value>` можно использовать [переменных среды](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="27b20-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="27b20-114">Параметры</span><span class="sxs-lookup"><span data-stu-id="27b20-114">Options</span></span>

| <span data-ttu-id="27b20-115">Параметр</span><span class="sxs-lookup"><span data-stu-id="27b20-115">Option</span></span> | <span data-ttu-id="27b20-116">Описание</span><span class="sxs-lookup"><span data-stu-id="27b20-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="27b20-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="27b20-117">AsPath</span></span> | <span data-ttu-id="27b20-118">Возвращает значение конфигурации как путь, игнорируются, когда `-Set` используется.</span><span class="sxs-lookup"><span data-stu-id="27b20-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="27b20-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="27b20-119">ConfigFile</span></span> | <span data-ttu-id="27b20-120">Файл конфигурации NuGet для изменения.</span><span class="sxs-lookup"><span data-stu-id="27b20-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="27b20-121">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="27b20-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="27b20-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="27b20-122">ForceEnglishOutput</span></span> | <span data-ttu-id="27b20-123">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="27b20-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="27b20-124">Справка</span><span class="sxs-lookup"><span data-stu-id="27b20-124">Help</span></span> | <span data-ttu-id="27b20-125">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="27b20-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="27b20-126">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="27b20-126">NonInteractive</span></span> | <span data-ttu-id="27b20-127">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="27b20-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="27b20-128">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="27b20-128">Verbosity</span></span> | <span data-ttu-id="27b20-129">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="27b20-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="27b20-130">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="27b20-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="27b20-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="27b20-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
