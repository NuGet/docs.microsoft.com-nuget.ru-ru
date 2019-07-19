---
title: Команда настройки интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 51c4c9937483e7f8a57356515c06a60c0f9e6f62
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327851"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="5b8b6-103">Команда config (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="5b8b6-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="5b8b6-104">**Применимо к:** &bullet; все **Поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="5b8b6-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="5b8b6-105">Возвращает или задает значения конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="5b8b6-106">Дополнительные сведения об использовании см. в разделе [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="5b8b6-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="5b8b6-107">Дополнительные сведения о допустимых именах ключей см. в [справочнике по файлу конфигурации NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="5b8b6-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="5b8b6-108">Использование</span><span class="sxs-lookup"><span data-stu-id="5b8b6-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="5b8b6-109">где `<name>` и`<value>` укажите пару "ключ-значение", которая должна быть задана в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="5b8b6-110">При необходимости можно указать столько пар.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="5b8b6-111">Чтобы удалить значение, укажите имя и `=` знак, но не значение.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="5b8b6-112">Сведения о допустимых именах ключей см. в справочнике по [файлу конфигурации NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="5b8b6-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="5b8b6-113">В NuGet 3.4 + `<value>` может использовать [переменные среды](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="5b8b6-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="5b8b6-114">Параметры</span><span class="sxs-lookup"><span data-stu-id="5b8b6-114">Options</span></span>

| <span data-ttu-id="5b8b6-115">Параметр</span><span class="sxs-lookup"><span data-stu-id="5b8b6-115">Option</span></span> | <span data-ttu-id="5b8b6-116">Описание</span><span class="sxs-lookup"><span data-stu-id="5b8b6-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5b8b6-117">аспас</span><span class="sxs-lookup"><span data-stu-id="5b8b6-117">AsPath</span></span> | <span data-ttu-id="5b8b6-118">Возвращает значение конфигурации в виде пути, которое игнорируется `-Set` , если используется.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="5b8b6-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5b8b6-119">ConfigFile</span></span> | <span data-ttu-id="5b8b6-120">Файл конфигурации NuGet для изменения.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="5b8b6-121">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) `~/.nuget/NuGet/NuGet.Config` или (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5b8b6-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5b8b6-122">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="5b8b6-122">ForceEnglishOutput</span></span> | <span data-ttu-id="5b8b6-123">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5b8b6-124">Help</span><span class="sxs-lookup"><span data-stu-id="5b8b6-124">Help</span></span> | <span data-ttu-id="5b8b6-125">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="5b8b6-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5b8b6-126">NonInteractive</span></span> | <span data-ttu-id="5b8b6-127">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5b8b6-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="5b8b6-128">Verbosity</span></span> | <span data-ttu-id="5b8b6-129">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5b8b6-130">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5b8b6-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="5b8b6-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="5b8b6-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
