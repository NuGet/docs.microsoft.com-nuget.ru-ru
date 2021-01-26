---
title: Команда отправки интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Push
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 54a09361173ae10040433b05fcfae7304e39452e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779186"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="5500a-103">команда push (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="5500a-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="5500a-104">Область **применения:** &bullet; **Поддерживаемые версии** публикации пакетов: ALL; 4.1.0 + требуется для NuGet.org</span><span class="sxs-lookup"><span data-stu-id="5500a-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="5500a-105">Чтобы отправить пакеты в nuget.org, необходимо использовать nuget.exe v 4.1.0 +, который реализует необходимые [протоколы NuGet](../../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="5500a-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="5500a-106">Отправляет пакет в источник пакета и публикует его.</span><span class="sxs-lookup"><span data-stu-id="5500a-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="5500a-107">Конфигурация NuGet по умолчанию получается путем загрузки `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), а затем загрузки любых `Nuget.Config` файлов или, `.nuget\Nuget.Config` начиная с корневого диска и заканчивая текущим каталогом (см. раздел [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="5500a-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="5500a-108">Использование</span><span class="sxs-lookup"><span data-stu-id="5500a-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="5500a-109">где `<packagePath>` идентифицирует пакет для отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="5500a-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="5500a-110">Варианты</span><span class="sxs-lookup"><span data-stu-id="5500a-110">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="5500a-111">Ключ API для целевого репозитория.</span><span class="sxs-lookup"><span data-stu-id="5500a-111">The API key for the target repository.</span></span> <span data-ttu-id="5500a-112">Если он отсутствует, используется указанный в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5500a-112">If not present,  the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="5500a-113">Файл конфигурации NuGet, который необходимо применить.</span><span class="sxs-lookup"><span data-stu-id="5500a-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5500a-114">Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5500a-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DisableBuffering`**

  <span data-ttu-id="5500a-115">Отключает буферизацию при принудительной отправке на сервер HTTP (s) для уменьшения использования памяти.</span><span class="sxs-lookup"><span data-stu-id="5500a-115">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="5500a-116">Внимание! при использовании этого параметра встроенная проверка подлинности Windows может не работать.</span><span class="sxs-lookup"><span data-stu-id="5500a-116">Caution: when this option is used, integrated Windows authentication might not work.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="5500a-117">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="5500a-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="5500a-118">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="5500a-118">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="5500a-119">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="5500a-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoServiceEndpoint`**

  <span data-ttu-id="5500a-120">Не добавляет `api/v2/packages` к исходному URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="5500a-120">Does not append `api/v2/packages` to the source URL.</span></span>

- **`-NoSymbols`**

  <span data-ttu-id="5500a-121">*(3.5 +)* Если пакет символов существует, он не будет отправлен на сервер символов.</span><span class="sxs-lookup"><span data-stu-id="5500a-121">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="5500a-122">Определяет URL-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="5500a-122">Specifies the server URL.</span></span> <span data-ttu-id="5500a-123">NuGet определяет источник в формате UNC или локальную папку и просто копирует файл вместо отправки через HTTP.</span><span class="sxs-lookup"><span data-stu-id="5500a-123">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="5500a-124">Кроме того, начиная с NuGet 3.4.2 этот параметр является обязательным, если только в `NuGet.Config` файле не указано значение *дефаултпушсаурце* (см. раздел [Настройка поведения NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="5500a-124">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span>

- **`-SkipDuplicate`**

  <span data-ttu-id="5500a-125">*(5.1 и более поздние версии)* Если пакет и версия уже существуют, пропустите их и продолжайте работу со следующим пакетом в push-уведомлений, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="5500a-125">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span>

- **`-SymbolSource`**

  <span data-ttu-id="5500a-126">*(3.5 +)* Указывает URL-адрес сервера символов; nuget.smbsrc.net используется при принудительной отправке в nuget.org</span><span class="sxs-lookup"><span data-stu-id="5500a-126">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span>

- **`-SymbolApiKey`**

  <span data-ttu-id="5500a-127">*(3.5 +)* Указывает ключ API для URL-адреса, указанного в `-SymbolSource` .</span><span class="sxs-lookup"><span data-stu-id="5500a-127">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span>

- **`-Timeout`**

  <span data-ttu-id="5500a-128">Указывает время ожидания в секундах для отправки на сервер.</span><span class="sxs-lookup"><span data-stu-id="5500a-128">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="5500a-129"> Значение по умолчанию — 300 секунд (5 минут).</span><span class="sxs-lookup"><span data-stu-id="5500a-129">The default is 300 seconds (5 minutes).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="5500a-130">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="5500a-130">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


<span data-ttu-id="5500a-131">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5500a-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5500a-132">Примеры</span><span class="sxs-lookup"><span data-stu-id="5500a-132">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
