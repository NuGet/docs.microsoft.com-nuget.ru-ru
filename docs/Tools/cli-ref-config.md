---
title: "Команды NuGet CLI config | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: "Ссылка для выполнения команды конфигурации nuget.exe"
keywords: "Справочник по конфигурации NuGet, команда конфигурации"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 12a8b51dd11b9bc3a496e02e869cdeb95e67b9e3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="ab204-104">Команда config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ab204-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="ab204-105">**Применяется к:** все &bullet; **поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="ab204-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="ab204-106">Возвращает или задает значения конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="ab204-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="ab204-107">Дополнительные использования см. [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ab204-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="ab204-108">Дополнительные сведения на допустимые имена ключей [ссылку на файл конфигурации NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="ab204-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ab204-109">Использование</span><span class="sxs-lookup"><span data-stu-id="ab204-109">Usage</span></span>

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="ab204-110">где `<name>` и `<value>` укажите пару "ключ значение" для установки в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ab204-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="ab204-111">При желании можно указать столько пар.</span><span class="sxs-lookup"><span data-stu-id="ab204-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="ab204-112">Чтобы удалить значение, укажите имя и `=` входа, но нет значения.</span><span class="sxs-lookup"><span data-stu-id="ab204-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="ab204-113">В NuGet 3.4 + `<value>` можно использовать [переменных среды](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="ab204-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="ab204-114">Параметры</span><span class="sxs-lookup"><span data-stu-id="ab204-114">Options</span></span>

| <span data-ttu-id="ab204-115">Параметр</span><span class="sxs-lookup"><span data-stu-id="ab204-115">Option</span></span> | <span data-ttu-id="ab204-116">Описание</span><span class="sxs-lookup"><span data-stu-id="ab204-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab204-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="ab204-117">AsPath</span></span> | <span data-ttu-id="ab204-118">Возвращает значение конфигурации как путь, игнорируются, когда `-Set` используется.</span><span class="sxs-lookup"><span data-stu-id="ab204-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="ab204-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ab204-119">ConfigFile</span></span> | <span data-ttu-id="ab204-120">*(2.5 +)*  NuGet файл конфигурации для изменения.</span><span class="sxs-lookup"><span data-stu-id="ab204-120">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="ab204-121">Если не указан, *%AppData%\NuGet\NuGet.Config* используется.</span><span class="sxs-lookup"><span data-stu-id="ab204-121">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ab204-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ab204-122">ForceEnglishOutput</span></span> | <span data-ttu-id="ab204-123">*(3.5 +)*  Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="ab204-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ab204-124">Справка</span><span class="sxs-lookup"><span data-stu-id="ab204-124">Help</span></span> | <span data-ttu-id="ab204-125">Отображает справку по команде.</span><span class="sxs-lookup"><span data-stu-id="ab204-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="ab204-126">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="ab204-126">NonInteractive</span></span> | <span data-ttu-id="ab204-127">Подавление для ввода данных и подтверждений.</span><span class="sxs-lookup"><span data-stu-id="ab204-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ab204-128">Уровень детализации</span><span class="sxs-lookup"><span data-stu-id="ab204-128">Verbosity</span></span> | <span data-ttu-id="ab204-129">Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="ab204-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="ab204-130">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ab204-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="ab204-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="ab204-131">Examples</span></span>

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
