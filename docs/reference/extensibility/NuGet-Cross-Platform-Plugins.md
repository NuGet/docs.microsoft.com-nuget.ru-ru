---
title: Межплатформенные подключаемые модули NuGet
description: Межплатформенные подключаемые модули NuGet для NuGet. exe, DotNet. exe, MSBuild. exe и Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428387"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="3d337-103">Межплатформенные подключаемые модули NuGet</span><span class="sxs-lookup"><span data-stu-id="3d337-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="3d337-104">Добавлена поддержка межплатформенных подключаемых модулей в NuGet 4.8 +.</span><span class="sxs-lookup"><span data-stu-id="3d337-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="3d337-105">Это достигается путем создания новой модели расширяемости подключаемого модуля, которая должна соответствовать определенному набору правил операции.</span><span class="sxs-lookup"><span data-stu-id="3d337-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="3d337-106">Подключаемые модули представляют собой самодостаточные исполняемые файлы (руннаблес в мире .NET Core), которые клиенты NuGet запускают в отдельном процессе.</span><span class="sxs-lookup"><span data-stu-id="3d337-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="3d337-107">Эта однократная запись выполняется один раз, запуская повсеместный подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="3d337-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="3d337-108">Он будет работать со всеми клиентскими средствами NuGet.</span><span class="sxs-lookup"><span data-stu-id="3d337-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="3d337-109">Подключаемые модули могут быть либо .NET Framework (NuGet. exe, MSBuild. exe и Visual Studio), либо .NET Core (DotNet. exe).</span><span class="sxs-lookup"><span data-stu-id="3d337-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="3d337-110">Определена версия протокола связи между клиентом NuGet и подключаемым модулем.</span><span class="sxs-lookup"><span data-stu-id="3d337-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="3d337-111">Во время подтверждения запуска 2 процесса согласовывают версию протокола.</span><span class="sxs-lookup"><span data-stu-id="3d337-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="3d337-112">Чтобы охватить все сценарии клиентских средств NuGet, требуется как .NET Framework, так и подключаемый модуль .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3d337-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="3d337-113">Ниже описаны сочетания подключаемых модулей для клиента и платформы.</span><span class="sxs-lookup"><span data-stu-id="3d337-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="3d337-114">Средство клиента</span><span class="sxs-lookup"><span data-stu-id="3d337-114">Client tool</span></span>  | <span data-ttu-id="3d337-115">Framework</span><span class="sxs-lookup"><span data-stu-id="3d337-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="3d337-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3d337-116">Visual Studio</span></span> | <span data-ttu-id="3d337-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d337-117">.NET Framework</span></span> |
| <span data-ttu-id="3d337-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="3d337-118">dotnet.exe</span></span> | <span data-ttu-id="3d337-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3d337-119">.NET Core</span></span> |
| <span data-ttu-id="3d337-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="3d337-120">NuGet.exe</span></span> | <span data-ttu-id="3d337-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d337-121">.NET Framework</span></span> |
| <span data-ttu-id="3d337-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="3d337-122">MSBuild.exe</span></span> | <span data-ttu-id="3d337-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d337-123">.NET Framework</span></span> |
| <span data-ttu-id="3d337-124">NuGet. exe на Mono</span><span class="sxs-lookup"><span data-stu-id="3d337-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="3d337-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d337-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="3d337-126">Как это работает</span><span class="sxs-lookup"><span data-stu-id="3d337-126">How does it work</span></span>

<span data-ttu-id="3d337-127">Рабочий процесс высокого уровня можно описать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3d337-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="3d337-128">NuGet обнаруживает доступные подключаемые модули.</span><span class="sxs-lookup"><span data-stu-id="3d337-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="3d337-129">Если это применимо, NuGet перебирает подключаемые модули в порядке приоритета и запускает их по одному.</span><span class="sxs-lookup"><span data-stu-id="3d337-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="3d337-130">NuGet будет использовать первый подключаемый модуль, который может обслуживать запрос.</span><span class="sxs-lookup"><span data-stu-id="3d337-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="3d337-131">Подключаемые модули будут закрыты, когда они больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="3d337-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="3d337-132">Общие требования к подключаемому модулю</span><span class="sxs-lookup"><span data-stu-id="3d337-132">General plugin requirements</span></span>

<span data-ttu-id="3d337-133">Текущая версия протокола — *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="3d337-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="3d337-134">Ниже приведены требования к этой версии.</span><span class="sxs-lookup"><span data-stu-id="3d337-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="3d337-135">Иметь действительные доверенные сборки Authenticode-подписи, которые будут выполняться в Windows и Mono.</span><span class="sxs-lookup"><span data-stu-id="3d337-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="3d337-136">Никаких специальных требований к доверию для сборок, работающих в Linux и Mac, пока нет.</span><span class="sxs-lookup"><span data-stu-id="3d337-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="3d337-137">Соответствующая ошибка</span><span class="sxs-lookup"><span data-stu-id="3d337-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="3d337-138">Поддержка запуска без отслеживания состояния в текущем контексте безопасности клиентских средств NuGet.</span><span class="sxs-lookup"><span data-stu-id="3d337-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="3d337-139">Например, клиентские средства NuGet не будут выполнять повышение или дополнительную инициализацию за пределами протокола подключаемого модуля, описанного ниже.</span><span class="sxs-lookup"><span data-stu-id="3d337-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="3d337-140">Быть не интерактивным, если явно не указано иное.</span><span class="sxs-lookup"><span data-stu-id="3d337-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="3d337-141">Придерживайтесь к согласованной версии протокола подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="3d337-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="3d337-142">Отвечать на все запросы в течение разумного периода времени.</span><span class="sxs-lookup"><span data-stu-id="3d337-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="3d337-143">Соблюдайте запросы на отмену для любой выполняющейся операции.</span><span class="sxs-lookup"><span data-stu-id="3d337-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="3d337-144">Техническая спецификация подробно описана в следующих спецификациях:</span><span class="sxs-lookup"><span data-stu-id="3d337-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="3d337-145">Подключаемый модуль скачивания пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="3d337-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="3d337-146">Подключаемый модуль Plat проверки подлинности NuGet</span><span class="sxs-lookup"><span data-stu-id="3d337-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="3d337-147">Взаимодействие с подключаемым модулем клиента</span><span class="sxs-lookup"><span data-stu-id="3d337-147">Client - Plugin interaction</span></span>

<span data-ttu-id="3d337-148">Клиентские средства NuGet и подключаемые модули взаимодействуют с JSON через стандартные потоки (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="3d337-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="3d337-149">Все данные должны быть закодированы в кодировке UTF-8.</span><span class="sxs-lookup"><span data-stu-id="3d337-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="3d337-150">Подключаемые модули запускаются с аргументом "-plugin".</span><span class="sxs-lookup"><span data-stu-id="3d337-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="3d337-151">Если пользователь непосредственно запускает исполняемый файл подключаемого модуля без этого аргумента, подключаемый модуль может предоставить информативное сообщение вместо того, чтобы ждать подтверждения протокола.</span><span class="sxs-lookup"><span data-stu-id="3d337-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="3d337-152">Время ожидания подтверждения протокола — 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="3d337-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="3d337-153">Подключаемый модуль должен завершить установку в как можно меньшее количество.</span><span class="sxs-lookup"><span data-stu-id="3d337-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="3d337-154">Клиентские средства NuGet запрашивают поддерживаемые операции подключаемого модуля, передавая индекс службы для источника NuGet.</span><span class="sxs-lookup"><span data-stu-id="3d337-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="3d337-155">Подключаемый модуль может использовать индекс службы для проверки наличия поддерживаемых типов служб.</span><span class="sxs-lookup"><span data-stu-id="3d337-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="3d337-156">Обмен данными между клиентскими инструментами NuGet и подключаемым модулем осуществляется по двунаправленному соединению.</span><span class="sxs-lookup"><span data-stu-id="3d337-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="3d337-157">Время ожидания каждого запроса составляет 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="3d337-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="3d337-158">Если операции должны занимать больше времени, необходимо отправить сообщение о ходе выполнения, чтобы предотвратить истечение тайм-аута запроса. После 1 минуты бездействия подключаемый модуль считается бездействующим и завершает работу.</span><span class="sxs-lookup"><span data-stu-id="3d337-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="3d337-159">Установка и обнаружение подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="3d337-159">Plugin installation and discovery</span></span>

<span data-ttu-id="3d337-160">Подключаемые модули будут обнаружены с помощью структуры каталогов на основе соглашений.</span><span class="sxs-lookup"><span data-stu-id="3d337-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="3d337-161">Сценарии CI/CD и опытные пользователи могут использовать переменные среды для переопределения поведения.</span><span class="sxs-lookup"><span data-stu-id="3d337-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="3d337-162">При использовании переменных среды разрешены только абсолютные пути.</span><span class="sxs-lookup"><span data-stu-id="3d337-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="3d337-163">Обратите внимание, что `NUGET_NETFX_PLUGIN_PATHS` и `NUGET_NETCORE_PLUGIN_PATHS` доступны только в версии 5.3 + средства NuGet и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="3d337-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="3d337-164">`NUGET_NETFX_PLUGIN_PATHS` — определяет подключаемые модули, которые будут использоваться средствами на основе .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="3d337-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="3d337-165">Имеет приоритет над `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="3d337-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="3d337-166">(Только NuGet версии 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="3d337-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="3d337-167">`NUGET_NETCORE_PLUGIN_PATHS` — определяет подключаемые модули, которые будут использоваться инструментами на основе .NET Core (DotNet. exe).</span><span class="sxs-lookup"><span data-stu-id="3d337-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="3d337-168">Имеет приоритет над `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="3d337-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="3d337-169">(Только NuGet версии 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="3d337-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="3d337-170">`NUGET_PLUGIN_PATHS` — определяет подключаемые модули, которые будут использоваться для этого процесса NuGet, с сохранением приоритета.</span><span class="sxs-lookup"><span data-stu-id="3d337-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="3d337-171">Если эта переменная среды задана, она переопределяет обнаружение на основе соглашения.</span><span class="sxs-lookup"><span data-stu-id="3d337-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="3d337-172">Игнорируется, если указана любая из переменных, определенных для платформы.</span><span class="sxs-lookup"><span data-stu-id="3d337-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="3d337-173">Расположение пользователя, корневое расположение NuGet в `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="3d337-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="3d337-174">Это расположение нельзя переопределить.</span><span class="sxs-lookup"><span data-stu-id="3d337-174">This location cannot be overriden.</span></span> <span data-ttu-id="3d337-175">Для подключаемых модулей .NET Core и .NET Framework будет использоваться другой корневой каталог.</span><span class="sxs-lookup"><span data-stu-id="3d337-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="3d337-176">Framework</span><span class="sxs-lookup"><span data-stu-id="3d337-176">Framework</span></span> | <span data-ttu-id="3d337-177">Расположение корневого обнаружения</span><span class="sxs-lookup"><span data-stu-id="3d337-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="3d337-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3d337-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="3d337-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d337-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="3d337-180">Каждый подключаемый модуль должен быть установлен в отдельную папку.</span><span class="sxs-lookup"><span data-stu-id="3d337-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="3d337-181">Точкой входа подключаемого модуля будет имя установленной папки с расширениями DLL для .NET Core и расширением exe для .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3d337-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="3d337-182">В настоящее время нет пользовательской истории для установки подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="3d337-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="3d337-183">Это так же просто, как перемещение необходимых файлов в предварительно определенное расположение.</span><span class="sxs-lookup"><span data-stu-id="3d337-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="3d337-184">Поддерживаемые операции</span><span class="sxs-lookup"><span data-stu-id="3d337-184">Supported operations</span></span>

<span data-ttu-id="3d337-185">В новом протоколе подключаемого модуля поддерживаются две операции.</span><span class="sxs-lookup"><span data-stu-id="3d337-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="3d337-186">Имя операции</span><span class="sxs-lookup"><span data-stu-id="3d337-186">Operation name</span></span> | <span data-ttu-id="3d337-187">Минимальная версия протокола</span><span class="sxs-lookup"><span data-stu-id="3d337-187">Minimum protocol version</span></span> | <span data-ttu-id="3d337-188">Минимальная версия клиента NuGet</span><span class="sxs-lookup"><span data-stu-id="3d337-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="3d337-189">Скачать пакет</span><span class="sxs-lookup"><span data-stu-id="3d337-189">Download Package</span></span> | <span data-ttu-id="3d337-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3d337-190">1.0.0</span></span> | <span data-ttu-id="3d337-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="3d337-191">4.3.0</span></span> |
| [<span data-ttu-id="3d337-192">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="3d337-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="3d337-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="3d337-193">2.0.0</span></span> | <span data-ttu-id="3d337-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="3d337-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="3d337-195">Запуск подключаемых модулей в правильной среде выполнения</span><span class="sxs-lookup"><span data-stu-id="3d337-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="3d337-196">Для NuGet в сценариях DotNet. exe подключаемые модули должны иметь возможность выполнения в этой конкретной среде выполнения файла DotNet. exe.</span><span class="sxs-lookup"><span data-stu-id="3d337-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="3d337-197">Он находится в поставщике подключаемого модуля и потребителе, чтобы убедиться в том, что используется совместимое сочетание DotNet. exe/plugin.</span><span class="sxs-lookup"><span data-stu-id="3d337-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="3d337-198">При использовании подключаемых модулей пользовательского расположения может возникнуть потенциальная ошибка. Например, DotNet. exe в среде выполнения 2,0 пытается использовать подключаемый модуль, написанный для среды выполнения 2,1.</span><span class="sxs-lookup"><span data-stu-id="3d337-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="3d337-199">Кэширование возможностей</span><span class="sxs-lookup"><span data-stu-id="3d337-199">Capabilities caching</span></span>

<span data-ttu-id="3d337-200">Проверка безопасности и создание экземпляров подключаемых модулей являются дорогостоящими.</span><span class="sxs-lookup"><span data-stu-id="3d337-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="3d337-201">Операция загрузки выполняется чаще, чем операция проверки подлинности, однако средний пользователь NuGet, скорее всего, будет иметь подключаемый модуль проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3d337-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="3d337-202">Чтобы улучшить работу, NuGet кэширует утверждения операций для данного запроса.</span><span class="sxs-lookup"><span data-stu-id="3d337-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="3d337-203">Этот кэш предназначен для каждого подключаемого модуля с ключом подключаемого модуля, который является путем к подключаемому модулю, а срок действия этого кэша возможностей составляет 30 дней.</span><span class="sxs-lookup"><span data-stu-id="3d337-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="3d337-204">Кэш находится в `%LocalAppData%/NuGet/plugins-cache` и может быть переопределен с помощью переменной среды `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="3d337-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="3d337-205">Чтобы очистить этот [кэш](../../consume-packages/managing-the-global-packages-and-cache-folders.md), можно выполнить команду Locals с параметром `plugins-cache`.</span><span class="sxs-lookup"><span data-stu-id="3d337-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="3d337-206">Параметр `all` Locals теперь также будет удалять кэш подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="3d337-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="3d337-207">Индекс сообщений протокола</span><span class="sxs-lookup"><span data-stu-id="3d337-207">Protocol messages index</span></span>

<span data-ttu-id="3d337-208">Сообщения версии протокола *1.0.0* :</span><span class="sxs-lookup"><span data-stu-id="3d337-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="3d337-209">Закрыть</span><span class="sxs-lookup"><span data-stu-id="3d337-209">Close</span></span>
    * <span data-ttu-id="3d337-210">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d337-211">Запрос не будет содержать полезных данных</span><span class="sxs-lookup"><span data-stu-id="3d337-211">The request will contain no payload</span></span>
    * <span data-ttu-id="3d337-212">Ответ не ожидается.</span><span class="sxs-lookup"><span data-stu-id="3d337-212">No response is expected.</span></span>  <span data-ttu-id="3d337-213">Правильный ответ заключается в том, что процесс подключаемого модуля будет быстро выходить из него.</span><span class="sxs-lookup"><span data-stu-id="3d337-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="3d337-214">Копировать файлы в пакет</span><span class="sxs-lookup"><span data-stu-id="3d337-214">Copy files in package</span></span>
    * <span data-ttu-id="3d337-215">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d337-216">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-216">The request will contain:</span></span>
        * <span data-ttu-id="3d337-217">ИДЕНТИФИКАТОР и версия пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-217">the package ID and version</span></span>
        * <span data-ttu-id="3d337-218">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-218">the package source repository location</span></span>
        * <span data-ttu-id="3d337-219">путь к каталогу назначения</span><span class="sxs-lookup"><span data-stu-id="3d337-219">destination directory path</span></span>
        * <span data-ttu-id="3d337-220">перечислимые файлы в пакете, которые будут скопированы в путь к каталогу назначения</span><span class="sxs-lookup"><span data-stu-id="3d337-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="3d337-221">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-221">A response will contain:</span></span>
        * <span data-ttu-id="3d337-222">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d337-223">перечислимые полные пути для скопированных файлов в целевом каталоге, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="3d337-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="3d337-224">Копировать файл пакета (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="3d337-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="3d337-225">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d337-226">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-226">The request will contain:</span></span>
        * <span data-ttu-id="3d337-227">ИДЕНТИФИКАТОР и версия пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-227">the package ID and version</span></span>
        * <span data-ttu-id="3d337-228">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-228">the package source repository location</span></span>
        * <span data-ttu-id="3d337-229">путь к целевому файлу</span><span class="sxs-lookup"><span data-stu-id="3d337-229">the destination file path</span></span>
    * <span data-ttu-id="3d337-230">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-230">A response will contain:</span></span>
        * <span data-ttu-id="3d337-231">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="3d337-232">Получение учетных данных</span><span class="sxs-lookup"><span data-stu-id="3d337-232">Get credentials</span></span>
    * <span data-ttu-id="3d337-233">Направление запроса: подключаемый модуль — > NuGet.</span><span class="sxs-lookup"><span data-stu-id="3d337-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="3d337-234">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-234">The request will contain:</span></span>
        * <span data-ttu-id="3d337-235">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-235">the package source repository location</span></span>
        * <span data-ttu-id="3d337-236">код состояния HTTP, полученный из исходного репозитория пакета с использованием текущих учетных данных</span><span class="sxs-lookup"><span data-stu-id="3d337-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="3d337-237">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-237">A response will contain:</span></span>
        * <span data-ttu-id="3d337-238">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d337-239">имя пользователя, если оно доступно</span><span class="sxs-lookup"><span data-stu-id="3d337-239">a username, if available</span></span>
        * <span data-ttu-id="3d337-240">пароль, если он доступен</span><span class="sxs-lookup"><span data-stu-id="3d337-240">a password, if available</span></span>

5.  <span data-ttu-id="3d337-241">Получение файлов в пакете</span><span class="sxs-lookup"><span data-stu-id="3d337-241">Get files in package</span></span>
    * <span data-ttu-id="3d337-242">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d337-243">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-243">The request will contain:</span></span>
        * <span data-ttu-id="3d337-244">ИДЕНТИФИКАТОР и версия пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-244">the package ID and version</span></span>
        * <span data-ttu-id="3d337-245">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-245">the package source repository location</span></span>
    * <span data-ttu-id="3d337-246">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-246">A response will contain:</span></span>
        * <span data-ttu-id="3d337-247">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d337-248">перечислимые пути к файлам в пакете, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="3d337-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="3d337-249">Получение утверждений операции</span><span class="sxs-lookup"><span data-stu-id="3d337-249">Get operation claims</span></span> 
    * <span data-ttu-id="3d337-250">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d337-251">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-251">The request will contain:</span></span>
        * <span data-ttu-id="3d337-252">Service index. JSON для источника пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="3d337-253">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-253">the package source repository location</span></span>
    * <span data-ttu-id="3d337-254">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-254">A response will contain:</span></span>
        * <span data-ttu-id="3d337-255">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d337-256">перечислимые поддерживаемые операции (например, скачивание пакета), если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="3d337-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="3d337-257">Если подключаемый модуль не поддерживает источник пакета, подключаемый модуль должен вернуть пустой набор поддерживаемых операций.</span><span class="sxs-lookup"><span data-stu-id="3d337-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="3d337-258">Это сообщение было Обновлено в версии *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="3d337-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="3d337-259">Она находится на клиенте для сохранения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="3d337-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="3d337-260">Получить хэш пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-260">Get package hash</span></span>
    * <span data-ttu-id="3d337-261">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d337-262">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-262">The request will contain:</span></span>
        * <span data-ttu-id="3d337-263">ИДЕНТИФИКАТОР и версия пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-263">the package ID and version</span></span>
        * <span data-ttu-id="3d337-264">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-264">the package source repository location</span></span>
        * <span data-ttu-id="3d337-265">хэш-алгоритм</span><span class="sxs-lookup"><span data-stu-id="3d337-265">the hash algorithm</span></span>
    * <span data-ttu-id="3d337-266">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-266">A response will contain:</span></span>
        * <span data-ttu-id="3d337-267">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d337-268">хэш файла пакета с использованием запрошенного хэш-алгоритма, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="3d337-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="3d337-269">Получение версий пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-269">Get package versions</span></span>
    * <span data-ttu-id="3d337-270">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d337-271">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-271">The request will contain:</span></span>
        * <span data-ttu-id="3d337-272">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-272">the package ID</span></span>
        * <span data-ttu-id="3d337-273">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-273">the package source repository location</span></span>
    * <span data-ttu-id="3d337-274">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-274">A response will contain:</span></span>
        * <span data-ttu-id="3d337-275">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d337-276">перечислимые версии пакета, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="3d337-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="3d337-277">Получение индекса службы</span><span class="sxs-lookup"><span data-stu-id="3d337-277">Get service index</span></span>
    * <span data-ttu-id="3d337-278">Направление запроса: подключаемый модуль — > NuGet.</span><span class="sxs-lookup"><span data-stu-id="3d337-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="3d337-279">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-279">The request will contain:</span></span>
        * <span data-ttu-id="3d337-280">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-280">the package source repository location</span></span>
    * <span data-ttu-id="3d337-281">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-281">A response will contain:</span></span>
        * <span data-ttu-id="3d337-282">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d337-283">индекс службы, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="3d337-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="3d337-284">Подтверждения</span><span class="sxs-lookup"><span data-stu-id="3d337-284">Handshake</span></span>
     * <span data-ttu-id="3d337-285">Направление запроса: подключаемый модуль > NuGet <</span><span class="sxs-lookup"><span data-stu-id="3d337-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="3d337-286">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-286">The request will contain:</span></span>
         * <span data-ttu-id="3d337-287">Текущая версия протокола подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="3d337-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="3d337-288">Минимальная поддерживаемая версия протокола подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="3d337-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="3d337-289">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-289">A response will contain:</span></span>
         * <span data-ttu-id="3d337-290">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="3d337-291">согласованная версия протокола, если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="3d337-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="3d337-292">Сбой приведет к завершению работы подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="3d337-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="3d337-293">Инициализация</span><span class="sxs-lookup"><span data-stu-id="3d337-293">Initialize</span></span>
     * <span data-ttu-id="3d337-294">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3d337-295">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-295">The request will contain:</span></span>
         * <span data-ttu-id="3d337-296">версия клиентского средства NuGet</span><span class="sxs-lookup"><span data-stu-id="3d337-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="3d337-297">эффективный язык клиентского средства NuGet.</span><span class="sxs-lookup"><span data-stu-id="3d337-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="3d337-298">При этом учитывается параметр Форцеенглишаутпут, если он используется.</span><span class="sxs-lookup"><span data-stu-id="3d337-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="3d337-299">время ожидания запроса по умолчанию, заменяющее протокол по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3d337-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="3d337-300">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-300">A response will contain:</span></span>
         * <span data-ttu-id="3d337-301">код ответа, указывающий результат операции.</span><span class="sxs-lookup"><span data-stu-id="3d337-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="3d337-302">Сбой приведет к завершению работы подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="3d337-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="3d337-303">Журнал</span><span class="sxs-lookup"><span data-stu-id="3d337-303">Log</span></span>
     * <span data-ttu-id="3d337-304">Направление запроса: подключаемый модуль — > NuGet.</span><span class="sxs-lookup"><span data-stu-id="3d337-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="3d337-305">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-305">The request will contain:</span></span>
         * <span data-ttu-id="3d337-306">уровень ведения журнала для запроса</span><span class="sxs-lookup"><span data-stu-id="3d337-306">the log level for the request</span></span>
         * <span data-ttu-id="3d337-307">сообщение для записи</span><span class="sxs-lookup"><span data-stu-id="3d337-307">a message to log</span></span>
     * <span data-ttu-id="3d337-308">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-308">A response will contain:</span></span>
         * <span data-ttu-id="3d337-309">код ответа, указывающий результат операции.</span><span class="sxs-lookup"><span data-stu-id="3d337-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="3d337-310">Мониторинг завершения процесса NuGet</span><span class="sxs-lookup"><span data-stu-id="3d337-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="3d337-311">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3d337-312">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-312">The request will contain:</span></span>
         * <span data-ttu-id="3d337-313">Идентификатор процесса NuGet</span><span class="sxs-lookup"><span data-stu-id="3d337-313">the NuGet process ID</span></span>
     * <span data-ttu-id="3d337-314">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-314">A response will contain:</span></span>
         * <span data-ttu-id="3d337-315">код ответа, указывающий результат операции.</span><span class="sxs-lookup"><span data-stu-id="3d337-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="3d337-316">Предзагрузка пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-316">Prefetch package</span></span>
     * <span data-ttu-id="3d337-317">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3d337-318">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-318">The request will contain:</span></span>
         * <span data-ttu-id="3d337-319">ИДЕНТИФИКАТОР и версия пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-319">the package ID and version</span></span>
         * <span data-ttu-id="3d337-320">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-320">the package source repository location</span></span>
     * <span data-ttu-id="3d337-321">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-321">A response will contain:</span></span>
         * <span data-ttu-id="3d337-322">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="3d337-323">Настройка учетных данных</span><span class="sxs-lookup"><span data-stu-id="3d337-323">Set credentials</span></span>
     * <span data-ttu-id="3d337-324">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3d337-325">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-325">The request will contain:</span></span>
         * <span data-ttu-id="3d337-326">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-326">the package source repository location</span></span>
         * <span data-ttu-id="3d337-327">Последнее известное имя пользователя источника пакета, если оно доступно</span><span class="sxs-lookup"><span data-stu-id="3d337-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="3d337-328">Последний известный пароль источника пакета, если он доступен</span><span class="sxs-lookup"><span data-stu-id="3d337-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="3d337-329">Последнее известное имя пользователя-посредника, если оно доступно</span><span class="sxs-lookup"><span data-stu-id="3d337-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="3d337-330">Последний известный пароль прокси-сервера, если он доступен</span><span class="sxs-lookup"><span data-stu-id="3d337-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="3d337-331">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-331">A response will contain:</span></span>
         * <span data-ttu-id="3d337-332">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="3d337-333">Задать уровень ведения журнала</span><span class="sxs-lookup"><span data-stu-id="3d337-333">Set log level</span></span>
     * <span data-ttu-id="3d337-334">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3d337-335">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-335">The request will contain:</span></span>
         * <span data-ttu-id="3d337-336">уровень журнала по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3d337-336">the default log level</span></span>
     * <span data-ttu-id="3d337-337">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-337">A response will contain:</span></span>
         * <span data-ttu-id="3d337-338">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="3d337-339">Сообщения версии протокола *2.0.0*</span><span class="sxs-lookup"><span data-stu-id="3d337-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="3d337-340">Получение утверждений операции</span><span class="sxs-lookup"><span data-stu-id="3d337-340">Get Operation Claims</span></span>

* <span data-ttu-id="3d337-341">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3d337-342">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-342">The request will contain:</span></span>
        * <span data-ttu-id="3d337-343">Service index. JSON для источника пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="3d337-344">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="3d337-344">the package source repository location</span></span>
    * <span data-ttu-id="3d337-345">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-345">A response will contain:</span></span>
        * <span data-ttu-id="3d337-346">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="3d337-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3d337-347">перечислимые поддерживаемые операции, если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="3d337-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="3d337-348">Если подключаемый модуль не поддерживает источник пакета, подключаемый модуль должен вернуть пустой набор поддерживаемых операций.</span><span class="sxs-lookup"><span data-stu-id="3d337-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="3d337-349">Если индекс службы и источник пакета имеют значение null, то подключаемый модуль может ответить с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="3d337-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="3d337-350">Получение учетных данных проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="3d337-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="3d337-351">Направление запроса: подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="3d337-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="3d337-352">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="3d337-352">The request will contain:</span></span>
    * <span data-ttu-id="3d337-353">URI</span><span class="sxs-lookup"><span data-stu-id="3d337-353">Uri</span></span>
    * <span data-ttu-id="3d337-354">Повтор</span><span class="sxs-lookup"><span data-stu-id="3d337-354">isRetry</span></span>
    * <span data-ttu-id="3d337-355">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3d337-355">NonInteractive</span></span>
    * <span data-ttu-id="3d337-356">каншовдиалог</span><span class="sxs-lookup"><span data-stu-id="3d337-356">CanShowDialog</span></span>
* <span data-ttu-id="3d337-357">Ответ будет содержать</span><span class="sxs-lookup"><span data-stu-id="3d337-357">A response will contain</span></span>
    * <span data-ttu-id="3d337-358">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="3d337-358">Username</span></span>
    * <span data-ttu-id="3d337-359">Пароль</span><span class="sxs-lookup"><span data-stu-id="3d337-359">Password</span></span>
    * <span data-ttu-id="3d337-360">Message</span><span class="sxs-lookup"><span data-stu-id="3d337-360">Message</span></span>
    * <span data-ttu-id="3d337-361">Список типов проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="3d337-361">List of Auth Types</span></span>
    * <span data-ttu-id="3d337-362">мессажереспонсекоде</span><span class="sxs-lookup"><span data-stu-id="3d337-362">MessageResponseCode</span></span>
