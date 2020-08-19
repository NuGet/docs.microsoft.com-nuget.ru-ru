---
title: Команда настройки интерфейса командной строки NuGet
description: Справочник по команде nuget.exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622880"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="99264-103">Команда config (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="99264-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="99264-104">**Применимо к:** все &bullet; **Поддерживаемые версии**: все</span><span class="sxs-lookup"><span data-stu-id="99264-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="99264-105">Возвращает или задает значения конфигурации NuGet.</span><span class="sxs-lookup"><span data-stu-id="99264-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="99264-106">Дополнительные сведения об использовании см. в разделе [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="99264-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="99264-107">Дополнительные сведения о допустимых именах ключей см. в [справочнике по файлу конфигурации NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="99264-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="99264-108">Использование</span><span class="sxs-lookup"><span data-stu-id="99264-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="99264-109">где `<name>` и `<value>` Укажите пару "ключ-значение", которая должна быть задана в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="99264-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="99264-110">При необходимости можно указать столько пар.</span><span class="sxs-lookup"><span data-stu-id="99264-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="99264-111">Чтобы удалить значение, укажите имя и `=` знак, но не значение.</span><span class="sxs-lookup"><span data-stu-id="99264-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="99264-112">Сведения о допустимых именах ключей см. в [справочнике по файлу конфигурации NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="99264-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="99264-113">В NuGet 3.4 + `<value>` может использовать [переменные среды](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="99264-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="99264-114">Параметры</span><span class="sxs-lookup"><span data-stu-id="99264-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="99264-115">Возвращает значение конфигурации в виде пути, которое игнорируется, если `-Set` используется.</span><span class="sxs-lookup"><span data-stu-id="99264-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="99264-116">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="99264-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="99264-117">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="99264-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="99264-118">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="99264-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="99264-119">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="99264-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="99264-120">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="99264-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="99264-121">Один для нескольких пар "ключ-значение", которые должны быть установлены в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="99264-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="99264-122">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="99264-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="99264-123">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="99264-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="99264-124">Примеры</span><span class="sxs-lookup"><span data-stu-id="99264-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
