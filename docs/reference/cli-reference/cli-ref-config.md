---
title: Команда настройки интерфейса командной строки NuGet
description: Справочник по команде NuGet. exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433317"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="df9de-103">Команда config (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="df9de-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="df9de-104">**Применимо к:** &bullet; все **Поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="df9de-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="df9de-105">Возвращает или задает значения конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="df9de-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="df9de-106">Дополнительные сведения об использовании см. в разделе [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="df9de-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="df9de-107">Дополнительные сведения о допустимых именах ключей см. в [справочнике по файлу конфигурации NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="df9de-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="df9de-108">Использование</span><span class="sxs-lookup"><span data-stu-id="df9de-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="df9de-109">где `<name>` и`<value>` укажите пару "ключ-значение", которая должна быть задана в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="df9de-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="df9de-110">При необходимости можно указать столько пар.</span><span class="sxs-lookup"><span data-stu-id="df9de-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="df9de-111">Чтобы удалить значение, укажите имя и `=` знак, но не значение.</span><span class="sxs-lookup"><span data-stu-id="df9de-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="df9de-112">Сведения о допустимых именах ключей см. в справочнике по [файлу конфигурации NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="df9de-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="df9de-113">В NuGet 3.4 + `<value>` может использовать [переменные среды](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="df9de-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="df9de-114">Параметры</span><span class="sxs-lookup"><span data-stu-id="df9de-114">Options</span></span>

| <span data-ttu-id="df9de-115">Параметр</span><span class="sxs-lookup"><span data-stu-id="df9de-115">Option</span></span> | <span data-ttu-id="df9de-116">Описание</span><span class="sxs-lookup"><span data-stu-id="df9de-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="df9de-117">аспас</span><span class="sxs-lookup"><span data-stu-id="df9de-117">AsPath</span></span> | <span data-ttu-id="df9de-118">Возвращает значение конфигурации в виде пути, которое игнорируется `-Set` , если используется.</span><span class="sxs-lookup"><span data-stu-id="df9de-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="df9de-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="df9de-119">ConfigFile</span></span> | <span data-ttu-id="df9de-120">Файл конфигурации NuGet для изменения.</span><span class="sxs-lookup"><span data-stu-id="df9de-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="df9de-121">Если этот параметр не указан, используется файл по умолчанию —`%AppData%\NuGet\NuGet.Config` (Windows) или `~/.config/NuGet/NuGet.Config` (Mac/Linux `~/.nuget/NuGet/NuGet.Config` ) или (зависит от дистрибутива ОС).</span><span class="sxs-lookup"><span data-stu-id="df9de-121">If not specified, the default file is used -`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.config/NuGet/NuGet.Config`  (Mac/Linux) or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution).</span></span>|
| <span data-ttu-id="df9de-122">форцеенглишаутпут</span><span class="sxs-lookup"><span data-stu-id="df9de-122">ForceEnglishOutput</span></span> | <span data-ttu-id="df9de-123">*(3.5 +)* Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="df9de-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="df9de-124">Help</span><span class="sxs-lookup"><span data-stu-id="df9de-124">Help</span></span> | <span data-ttu-id="df9de-125">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="df9de-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="df9de-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="df9de-126">NonInteractive</span></span> | <span data-ttu-id="df9de-127">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="df9de-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="df9de-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="df9de-128">Verbosity</span></span> | <span data-ttu-id="df9de-129">Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*.</span><span class="sxs-lookup"><span data-stu-id="df9de-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="df9de-130">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="df9de-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="df9de-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="df9de-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
