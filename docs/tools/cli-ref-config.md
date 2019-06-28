---
title: Команды интерфейса командной строки NuGet config
description: Справочник по командам config nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426078"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="b3880-103">команды config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b3880-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="b3880-104">**Применяется к:** все &bullet; **поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="b3880-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="b3880-105">Возвращает или задает значения конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="b3880-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="b3880-106">Избыточное использование см. в разделе [NuGet распространенных конфигураций](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="b3880-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="b3880-107">Дополнительные сведения о допустимых именах, см. [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="b3880-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="b3880-108">Использование</span><span class="sxs-lookup"><span data-stu-id="b3880-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="b3880-109">где `<name>` и `<value>` укажите пару "ключ значение" для задания в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b3880-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="b3880-110">При необходимости можно указать любое количество пар.</span><span class="sxs-lookup"><span data-stu-id="b3880-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="b3880-111">Чтобы удалить значение, укажите имя и `=` входа, но без значения.</span><span class="sxs-lookup"><span data-stu-id="b3880-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="b3880-112">Допустимые имена ключей, см. в разделе [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="b3880-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="b3880-113">В NuGet 3.4 + `<value>` можно использовать [переменные среды](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="b3880-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="b3880-114">Параметры</span><span class="sxs-lookup"><span data-stu-id="b3880-114">Options</span></span>

| <span data-ttu-id="b3880-115">Параметр</span><span class="sxs-lookup"><span data-stu-id="b3880-115">Option</span></span> | <span data-ttu-id="b3880-116">Описание</span><span class="sxs-lookup"><span data-stu-id="b3880-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b3880-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="b3880-117">AsPath</span></span> | <span data-ttu-id="b3880-118">Возвращает значение конфигурации как путь, игнорируются, когда `-Set` используется.</span><span class="sxs-lookup"><span data-stu-id="b3880-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="b3880-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b3880-119">ConfigFile</span></span> | <span data-ttu-id="b3880-120">Чтобы изменить файл конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="b3880-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="b3880-121">Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="b3880-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b3880-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b3880-122">ForceEnglishOutput</span></span> | <span data-ttu-id="b3880-123">*(3.5 и более поздние)*  Заставляет nuget.exe для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры.</span><span class="sxs-lookup"><span data-stu-id="b3880-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b3880-124">Help</span><span class="sxs-lookup"><span data-stu-id="b3880-124">Help</span></span> | <span data-ttu-id="b3880-125">Отображает справку для команды.</span><span class="sxs-lookup"><span data-stu-id="b3880-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="b3880-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b3880-126">NonInteractive</span></span> | <span data-ttu-id="b3880-127">Подавление для пользователя данные или подтверждения.</span><span class="sxs-lookup"><span data-stu-id="b3880-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b3880-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b3880-128">Verbosity</span></span> | <span data-ttu-id="b3880-129">Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*.</span><span class="sxs-lookup"><span data-stu-id="b3880-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b3880-130">Также см. в разделе [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b3880-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="b3880-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="b3880-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
