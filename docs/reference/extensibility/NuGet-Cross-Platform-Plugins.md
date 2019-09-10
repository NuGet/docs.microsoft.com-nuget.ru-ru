---
title: Межплатформенные подключаемые модули NuGet
description: Межплатформенные подключаемые модули NuGet для NuGet. exe, DotNet. exe, MSBuild. exe и Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815305"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="49603-103">Межплатформенные подключаемые модули NuGet</span><span class="sxs-lookup"><span data-stu-id="49603-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="49603-104">Добавлена поддержка межплатформенных подключаемых модулей в NuGet 4.8 +.</span><span class="sxs-lookup"><span data-stu-id="49603-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="49603-105">Это достигается путем создания новой модели расширяемости подключаемого модуля, которая должна соответствовать определенному набору правил операции.</span><span class="sxs-lookup"><span data-stu-id="49603-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="49603-106">Подключаемые модули представляют собой самодостаточные исполняемые файлы (руннаблес в мире .NET Core), которые клиенты NuGet запускают в отдельном процессе.</span><span class="sxs-lookup"><span data-stu-id="49603-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="49603-107">Эта однократная запись выполняется один раз, запуская повсеместный подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="49603-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="49603-108">Он будет работать со всеми клиентскими средствами NuGet.</span><span class="sxs-lookup"><span data-stu-id="49603-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="49603-109">Подключаемые модули могут быть либо .NET Framework (NuGet. exe, MSBuild. exe и Visual Studio), либо .NET Core (DotNet. exe).</span><span class="sxs-lookup"><span data-stu-id="49603-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="49603-110">Определена версия протокола связи между клиентом NuGet и подключаемым модулем.</span><span class="sxs-lookup"><span data-stu-id="49603-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="49603-111">Во время подтверждения запуска 2 процесса согласовывают версию протокола.</span><span class="sxs-lookup"><span data-stu-id="49603-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="49603-112">Чтобы охватить все сценарии клиентских средств NuGet, требуется как .NET Framework, так и подключаемый модуль .NET Core.</span><span class="sxs-lookup"><span data-stu-id="49603-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="49603-113">Ниже описаны сочетания подключаемых модулей для клиента и платформы.</span><span class="sxs-lookup"><span data-stu-id="49603-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="49603-114">Клиентская программа</span><span class="sxs-lookup"><span data-stu-id="49603-114">Client tool</span></span>  | <span data-ttu-id="49603-115">Платформа</span><span class="sxs-lookup"><span data-stu-id="49603-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="49603-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="49603-116">Visual Studio</span></span> | <span data-ttu-id="49603-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="49603-117">.NET Framework</span></span> |
| <span data-ttu-id="49603-118">DotNet. exe</span><span class="sxs-lookup"><span data-stu-id="49603-118">dotnet.exe</span></span> | <span data-ttu-id="49603-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="49603-119">.NET Core</span></span> |
| <span data-ttu-id="49603-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="49603-120">NuGet.exe</span></span> | <span data-ttu-id="49603-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="49603-121">.NET Framework</span></span> |
| <span data-ttu-id="49603-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="49603-122">MSBuild.exe</span></span> | <span data-ttu-id="49603-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="49603-123">.NET Framework</span></span> |
| <span data-ttu-id="49603-124">NuGet. exe на Mono</span><span class="sxs-lookup"><span data-stu-id="49603-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="49603-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="49603-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="49603-126">Как это работает</span><span class="sxs-lookup"><span data-stu-id="49603-126">How does it work</span></span>

<span data-ttu-id="49603-127">Рабочий процесс высокого уровня можно описать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="49603-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="49603-128">NuGet обнаруживает доступные подключаемые модули.</span><span class="sxs-lookup"><span data-stu-id="49603-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="49603-129">Если это применимо, NuGet перебирает подключаемые модули в порядке приоритета и запускает их по одному.</span><span class="sxs-lookup"><span data-stu-id="49603-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="49603-130">NuGet будет использовать первый подключаемый модуль, который может обслуживать запрос.</span><span class="sxs-lookup"><span data-stu-id="49603-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="49603-131">Подключаемые модули будут закрыты, когда они больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="49603-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="49603-132">Общие требования к подключаемому модулю</span><span class="sxs-lookup"><span data-stu-id="49603-132">General plugin requirements</span></span>

<span data-ttu-id="49603-133">Текущая версия протокола — *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="49603-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="49603-134">Ниже приведены требования к этой версии.</span><span class="sxs-lookup"><span data-stu-id="49603-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="49603-135">Иметь действительные доверенные сборки Authenticode-подписи, которые будут выполняться в Windows и Mono.</span><span class="sxs-lookup"><span data-stu-id="49603-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="49603-136">Никаких специальных требований к доверию для сборок, работающих в Linux и Mac, пока нет.</span><span class="sxs-lookup"><span data-stu-id="49603-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="49603-137">Соответствующая ошибка</span><span class="sxs-lookup"><span data-stu-id="49603-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="49603-138">Поддержка запуска без отслеживания состояния в текущем контексте безопасности клиентских средств NuGet.</span><span class="sxs-lookup"><span data-stu-id="49603-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="49603-139">Например, клиентские средства NuGet не будут выполнять повышение или дополнительную инициализацию за пределами протокола подключаемого модуля, описанного ниже.</span><span class="sxs-lookup"><span data-stu-id="49603-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="49603-140">Быть не интерактивным, если явно не указано иное.</span><span class="sxs-lookup"><span data-stu-id="49603-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="49603-141">Придерживайтесь к согласованной версии протокола подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="49603-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="49603-142">Отвечать на все запросы в течение разумного периода времени.</span><span class="sxs-lookup"><span data-stu-id="49603-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="49603-143">Соблюдайте запросы на отмену для любой выполняющейся операции.</span><span class="sxs-lookup"><span data-stu-id="49603-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="49603-144">Техническая спецификация подробно описана в следующих спецификациях:</span><span class="sxs-lookup"><span data-stu-id="49603-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="49603-145">Подключаемый модуль скачивания пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="49603-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="49603-146">Подключаемый модуль Plat проверки подлинности NuGet</span><span class="sxs-lookup"><span data-stu-id="49603-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="49603-147">Взаимодействие с подключаемым модулем клиента</span><span class="sxs-lookup"><span data-stu-id="49603-147">Client - Plugin interaction</span></span>

<span data-ttu-id="49603-148">Клиентские средства NuGet и подключаемые модули взаимодействуют с JSON через стандартные потоки (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="49603-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="49603-149">Все данные должны быть закодированы в кодировке UTF-8.</span><span class="sxs-lookup"><span data-stu-id="49603-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="49603-150">Подключаемые модули запускаются с аргументом "-plugin".</span><span class="sxs-lookup"><span data-stu-id="49603-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="49603-151">Если пользователь непосредственно запускает исполняемый файл подключаемого модуля без этого аргумента, подключаемый модуль может предоставить информативное сообщение вместо того, чтобы ждать подтверждения протокола.</span><span class="sxs-lookup"><span data-stu-id="49603-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="49603-152">Время ожидания подтверждения протокола — 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="49603-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="49603-153">Подключаемый модуль должен завершить установку в как можно меньшее количество.</span><span class="sxs-lookup"><span data-stu-id="49603-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="49603-154">Клиентские средства NuGet запрашивают поддерживаемые операции подключаемого модуля, передавая индекс службы для источника NuGet.</span><span class="sxs-lookup"><span data-stu-id="49603-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="49603-155">Подключаемый модуль может использовать индекс службы для проверки наличия поддерживаемых типов служб.</span><span class="sxs-lookup"><span data-stu-id="49603-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="49603-156">Обмен данными между клиентскими инструментами NuGet и подключаемым модулем осуществляется по двунаправленному соединению.</span><span class="sxs-lookup"><span data-stu-id="49603-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="49603-157">Время ожидания каждого запроса составляет 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="49603-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="49603-158">Если операции должны занимать больше времени, необходимо отправить сообщение о ходе выполнения, чтобы предотвратить истечение тайм-аута запроса. После 1 минуты бездействия подключаемый модуль считается бездействующим и завершает работу.</span><span class="sxs-lookup"><span data-stu-id="49603-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="49603-159">Установка и обнаружение подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="49603-159">Plugin installation and discovery</span></span>

<span data-ttu-id="49603-160">Подключаемые модули будут обнаружены с помощью структуры каталогов на основе соглашений.</span><span class="sxs-lookup"><span data-stu-id="49603-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="49603-161">Сценарии CI/CD и опытные пользователи могут использовать переменные среды для переопределения поведения.</span><span class="sxs-lookup"><span data-stu-id="49603-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="49603-162">Обратите `NUGET_NETFX_PLUGIN_PATHS` внимание `NUGET_NETCORE_PLUGIN_PATHS` , что и доступны только в версии 5.3 + средства NuGet и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="49603-162">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="49603-163">`NUGET_NETFX_PLUGIN_PATHS`— определяет подключаемые модули, которые будут использоваться инструментами на основе .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="49603-163">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="49603-164">Имеет приоритет над `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="49603-164">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="49603-165">(Только NuGet версии 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="49603-165">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="49603-166">`NUGET_NETCORE_PLUGIN_PATHS`— определяет подключаемые модули, которые будут использоваться инструментами на основе .NET Core (DotNet. exe).</span><span class="sxs-lookup"><span data-stu-id="49603-166">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="49603-167">Имеет приоритет над `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="49603-167">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="49603-168">(Только NuGet версии 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="49603-168">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="49603-169">`NUGET_PLUGIN_PATHS`— определяет подключаемые модули, которые будут использоваться для этого процесса NuGet, приоритет зарезервирован.</span><span class="sxs-lookup"><span data-stu-id="49603-169">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="49603-170">Если эта переменная среды задана, она переопределяет обнаружение на основе соглашения.</span><span class="sxs-lookup"><span data-stu-id="49603-170">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="49603-171">Игнорируется, если указана любая из переменных, определенных для платформы.</span><span class="sxs-lookup"><span data-stu-id="49603-171">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="49603-172">Расположение пользователя, корневое расположение NuGet в `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="49603-172">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="49603-173">Это расположение нельзя переопределить.</span><span class="sxs-lookup"><span data-stu-id="49603-173">This location cannot be overriden.</span></span> <span data-ttu-id="49603-174">Для подключаемых модулей .NET Core и .NET Framework будет использоваться другой корневой каталог.</span><span class="sxs-lookup"><span data-stu-id="49603-174">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="49603-175">Платформа</span><span class="sxs-lookup"><span data-stu-id="49603-175">Framework</span></span> | <span data-ttu-id="49603-176">Расположение корневого обнаружения</span><span class="sxs-lookup"><span data-stu-id="49603-176">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="49603-177">.NET Core</span><span class="sxs-lookup"><span data-stu-id="49603-177">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="49603-178">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="49603-178">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="49603-179">Каждый подключаемый модуль должен быть установлен в отдельную папку.</span><span class="sxs-lookup"><span data-stu-id="49603-179">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="49603-180">Точкой входа подключаемого модуля будет имя установленной папки с расширениями DLL для .NET Core и расширением exe для .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="49603-180">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="49603-181">В настоящее время нет пользовательской истории для установки подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="49603-181">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="49603-182">Это так же просто, как перемещение необходимых файлов в предварительно определенное расположение.</span><span class="sxs-lookup"><span data-stu-id="49603-182">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="49603-183">Поддерживаемые операции</span><span class="sxs-lookup"><span data-stu-id="49603-183">Supported operations</span></span>

<span data-ttu-id="49603-184">В новом протоколе подключаемого модуля поддерживаются две операции.</span><span class="sxs-lookup"><span data-stu-id="49603-184">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="49603-185">Имя операции</span><span class="sxs-lookup"><span data-stu-id="49603-185">Operation name</span></span> | <span data-ttu-id="49603-186">Минимальная версия протокола</span><span class="sxs-lookup"><span data-stu-id="49603-186">Minimum protocol version</span></span> | <span data-ttu-id="49603-187">Минимальная версия клиента NuGet</span><span class="sxs-lookup"><span data-stu-id="49603-187">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="49603-188">Скачать пакет</span><span class="sxs-lookup"><span data-stu-id="49603-188">Download Package</span></span> | <span data-ttu-id="49603-189">1.0.0</span><span class="sxs-lookup"><span data-stu-id="49603-189">1.0.0</span></span> | <span data-ttu-id="49603-190">4.3.0</span><span class="sxs-lookup"><span data-stu-id="49603-190">4.3.0</span></span> |
| [<span data-ttu-id="49603-191">Authentication</span><span class="sxs-lookup"><span data-stu-id="49603-191">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="49603-192">2.0.0</span><span class="sxs-lookup"><span data-stu-id="49603-192">2.0.0</span></span> | <span data-ttu-id="49603-193">4.8.0</span><span class="sxs-lookup"><span data-stu-id="49603-193">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="49603-194">Запуск подключаемых модулей в правильной среде выполнения</span><span class="sxs-lookup"><span data-stu-id="49603-194">Running plugins under the correct runtime</span></span>

<span data-ttu-id="49603-195">Для NuGet в сценариях DotNet. exe подключаемые модули должны иметь возможность выполнения в этой конкретной среде выполнения файла DotNet. exe.</span><span class="sxs-lookup"><span data-stu-id="49603-195">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="49603-196">Он находится в поставщике подключаемого модуля и потребителе, чтобы убедиться в том, что используется совместимое сочетание DotNet. exe/plugin.</span><span class="sxs-lookup"><span data-stu-id="49603-196">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="49603-197">При использовании подключаемых модулей пользовательского расположения может возникнуть потенциальная ошибка. Например, DotNet. exe в среде выполнения 2,0 пытается использовать подключаемый модуль, написанный для среды выполнения 2,1.</span><span class="sxs-lookup"><span data-stu-id="49603-197">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="49603-198">Кэширование возможностей</span><span class="sxs-lookup"><span data-stu-id="49603-198">Capabilities caching</span></span>

<span data-ttu-id="49603-199">Проверка безопасности и создание экземпляров подключаемых модулей являются дорогостоящими.</span><span class="sxs-lookup"><span data-stu-id="49603-199">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="49603-200">Операция загрузки выполняется чаще, чем операция проверки подлинности, однако средний пользователь NuGet, скорее всего, будет иметь подключаемый модуль проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="49603-200">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="49603-201">Чтобы улучшить работу, NuGet кэширует утверждения операций для данного запроса.</span><span class="sxs-lookup"><span data-stu-id="49603-201">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="49603-202">Этот кэш предназначен для каждого подключаемого модуля с ключом подключаемого модуля, который является путем к подключаемому модулю, а срок действия этого кэша возможностей составляет 30 дней.</span><span class="sxs-lookup"><span data-stu-id="49603-202">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="49603-203">Кэш находится в `%LocalAppData%/NuGet/plugins-cache` и может быть переопределен с помощью переменной `NUGET_PLUGINS_CACHE_PATH`среды.</span><span class="sxs-lookup"><span data-stu-id="49603-203">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="49603-204">Чтобы очистить этот [кэш](../../consume-packages/managing-the-global-packages-and-cache-folders.md), можно выполнить команду Locals с `plugins-cache` параметром.</span><span class="sxs-lookup"><span data-stu-id="49603-204">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="49603-205">Теперь `all` параметр Locals (локальные) также удаляет кэш подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="49603-205">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="49603-206">Индекс сообщений протокола</span><span class="sxs-lookup"><span data-stu-id="49603-206">Protocol messages index</span></span>

<span data-ttu-id="49603-207">Сообщения версии протокола *1.0.0* :</span><span class="sxs-lookup"><span data-stu-id="49603-207">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="49603-208">Закрыть</span><span class="sxs-lookup"><span data-stu-id="49603-208">Close</span></span>
    * <span data-ttu-id="49603-209">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-209">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="49603-210">Запрос не будет содержать полезных данных</span><span class="sxs-lookup"><span data-stu-id="49603-210">The request will contain no payload</span></span>
    * <span data-ttu-id="49603-211">Ответ не ожидается.</span><span class="sxs-lookup"><span data-stu-id="49603-211">No response is expected.</span></span>  <span data-ttu-id="49603-212">Правильный ответ заключается в том, что процесс подключаемого модуля будет быстро выходить из него.</span><span class="sxs-lookup"><span data-stu-id="49603-212">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="49603-213">Копировать файлы в пакет</span><span class="sxs-lookup"><span data-stu-id="49603-213">Copy files in package</span></span>
    * <span data-ttu-id="49603-214">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-214">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="49603-215">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-215">The request will contain:</span></span>
        * <span data-ttu-id="49603-216">ИДЕНТИФИКАТОР и версия пакета</span><span class="sxs-lookup"><span data-stu-id="49603-216">the package ID and version</span></span>
        * <span data-ttu-id="49603-217">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="49603-217">the package source repository location</span></span>
        * <span data-ttu-id="49603-218">путь к каталогу назначения</span><span class="sxs-lookup"><span data-stu-id="49603-218">destination directory path</span></span>
        * <span data-ttu-id="49603-219">перечислимые файлы в пакете, которые будут скопированы в путь к каталогу назначения</span><span class="sxs-lookup"><span data-stu-id="49603-219">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="49603-220">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-220">A response will contain:</span></span>
        * <span data-ttu-id="49603-221">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-221">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="49603-222">перечислимые полные пути для скопированных файлов в целевом каталоге, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="49603-222">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="49603-223">Копировать файл пакета (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="49603-223">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="49603-224">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-224">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="49603-225">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-225">The request will contain:</span></span>
        * <span data-ttu-id="49603-226">ИДЕНТИФИКАТОР и версия пакета</span><span class="sxs-lookup"><span data-stu-id="49603-226">the package ID and version</span></span>
        * <span data-ttu-id="49603-227">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="49603-227">the package source repository location</span></span>
        * <span data-ttu-id="49603-228">путь к целевому файлу</span><span class="sxs-lookup"><span data-stu-id="49603-228">the destination file path</span></span>
    * <span data-ttu-id="49603-229">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-229">A response will contain:</span></span>
        * <span data-ttu-id="49603-230">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-230">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="49603-231">Получение учетных данных</span><span class="sxs-lookup"><span data-stu-id="49603-231">Get credentials</span></span>
    * <span data-ttu-id="49603-232">Направление запроса: подключаемый модуль — > NuGet.</span><span class="sxs-lookup"><span data-stu-id="49603-232">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="49603-233">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-233">The request will contain:</span></span>
        * <span data-ttu-id="49603-234">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="49603-234">the package source repository location</span></span>
        * <span data-ttu-id="49603-235">код состояния HTTP, полученный из исходного репозитория пакета с использованием текущих учетных данных</span><span class="sxs-lookup"><span data-stu-id="49603-235">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="49603-236">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-236">A response will contain:</span></span>
        * <span data-ttu-id="49603-237">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-237">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="49603-238">имя пользователя, если оно доступно</span><span class="sxs-lookup"><span data-stu-id="49603-238">a username, if available</span></span>
        * <span data-ttu-id="49603-239">пароль, если он доступен</span><span class="sxs-lookup"><span data-stu-id="49603-239">a password, if available</span></span>

5.  <span data-ttu-id="49603-240">Получение файлов в пакете</span><span class="sxs-lookup"><span data-stu-id="49603-240">Get files in package</span></span>
    * <span data-ttu-id="49603-241">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="49603-242">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-242">The request will contain:</span></span>
        * <span data-ttu-id="49603-243">ИДЕНТИФИКАТОР и версия пакета</span><span class="sxs-lookup"><span data-stu-id="49603-243">the package ID and version</span></span>
        * <span data-ttu-id="49603-244">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="49603-244">the package source repository location</span></span>
    * <span data-ttu-id="49603-245">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-245">A response will contain:</span></span>
        * <span data-ttu-id="49603-246">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="49603-247">перечислимые пути к файлам в пакете, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="49603-247">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="49603-248">Получение утверждений операции</span><span class="sxs-lookup"><span data-stu-id="49603-248">Get operation claims</span></span> 
    * <span data-ttu-id="49603-249">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-249">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="49603-250">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-250">The request will contain:</span></span>
        * <span data-ttu-id="49603-251">Service index. JSON для источника пакета</span><span class="sxs-lookup"><span data-stu-id="49603-251">the service index.json for a package source</span></span>
        * <span data-ttu-id="49603-252">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="49603-252">the package source repository location</span></span>
    * <span data-ttu-id="49603-253">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-253">A response will contain:</span></span>
        * <span data-ttu-id="49603-254">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-254">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="49603-255">перечислимые поддерживаемые операции (например, скачивание пакета), если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="49603-255">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="49603-256">Если подключаемый модуль не поддерживает источник пакета, подключаемый модуль должен вернуть пустой набор поддерживаемых операций.</span><span class="sxs-lookup"><span data-stu-id="49603-256">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="49603-257">Это сообщение было Обновлено в версии *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="49603-257">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="49603-258">Она находится на клиенте для сохранения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="49603-258">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="49603-259">Получить хэш пакета</span><span class="sxs-lookup"><span data-stu-id="49603-259">Get package hash</span></span>
    * <span data-ttu-id="49603-260">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-260">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="49603-261">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-261">The request will contain:</span></span>
        * <span data-ttu-id="49603-262">ИДЕНТИФИКАТОР и версия пакета</span><span class="sxs-lookup"><span data-stu-id="49603-262">the package ID and version</span></span>
        * <span data-ttu-id="49603-263">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="49603-263">the package source repository location</span></span>
        * <span data-ttu-id="49603-264">хэш-алгоритм</span><span class="sxs-lookup"><span data-stu-id="49603-264">the hash algorithm</span></span>
    * <span data-ttu-id="49603-265">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-265">A response will contain:</span></span>
        * <span data-ttu-id="49603-266">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="49603-267">хэш файла пакета с использованием запрошенного хэш-алгоритма, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="49603-267">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="49603-268">Получение версий пакета</span><span class="sxs-lookup"><span data-stu-id="49603-268">Get package versions</span></span>
    * <span data-ttu-id="49603-269">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-269">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="49603-270">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-270">The request will contain:</span></span>
        * <span data-ttu-id="49603-271">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="49603-271">the package ID</span></span>
        * <span data-ttu-id="49603-272">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="49603-272">the package source repository location</span></span>
    * <span data-ttu-id="49603-273">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-273">A response will contain:</span></span>
        * <span data-ttu-id="49603-274">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-274">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="49603-275">перечислимые версии пакета, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="49603-275">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="49603-276">Получение индекса службы</span><span class="sxs-lookup"><span data-stu-id="49603-276">Get service index</span></span>
    * <span data-ttu-id="49603-277">Направление запроса: подключаемый модуль — > NuGet.</span><span class="sxs-lookup"><span data-stu-id="49603-277">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="49603-278">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-278">The request will contain:</span></span>
        * <span data-ttu-id="49603-279">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="49603-279">the package source repository location</span></span>
    * <span data-ttu-id="49603-280">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-280">A response will contain:</span></span>
        * <span data-ttu-id="49603-281">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-281">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="49603-282">индекс службы, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="49603-282">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="49603-283">Подтверждения</span><span class="sxs-lookup"><span data-stu-id="49603-283">Handshake</span></span>
     * <span data-ttu-id="49603-284">Направление запроса:  Подключаемый модуль > < NuGet</span><span class="sxs-lookup"><span data-stu-id="49603-284">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="49603-285">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-285">The request will contain:</span></span>
         * <span data-ttu-id="49603-286">Текущая версия протокола подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="49603-286">the current plugin protocol version</span></span>
         * <span data-ttu-id="49603-287">Минимальная поддерживаемая версия протокола подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="49603-287">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="49603-288">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-288">A response will contain:</span></span>
         * <span data-ttu-id="49603-289">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-289">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="49603-290">согласованная версия протокола, если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="49603-290">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="49603-291">Сбой приведет к завершению работы подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="49603-291">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="49603-292">Initialize</span><span class="sxs-lookup"><span data-stu-id="49603-292">Initialize</span></span>
     * <span data-ttu-id="49603-293">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-293">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="49603-294">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-294">The request will contain:</span></span>
         * <span data-ttu-id="49603-295">версия клиентского средства NuGet</span><span class="sxs-lookup"><span data-stu-id="49603-295">the NuGet client tool version</span></span>
         * <span data-ttu-id="49603-296">эффективный язык клиентского средства NuGet.</span><span class="sxs-lookup"><span data-stu-id="49603-296">the NuGet client tool effective language.</span></span>  <span data-ttu-id="49603-297">При этом учитывается параметр Форцеенглишаутпут, если он используется.</span><span class="sxs-lookup"><span data-stu-id="49603-297">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="49603-298">время ожидания запроса по умолчанию, заменяющее протокол по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="49603-298">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="49603-299">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-299">A response will contain:</span></span>
         * <span data-ttu-id="49603-300">код ответа, указывающий результат операции.</span><span class="sxs-lookup"><span data-stu-id="49603-300">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="49603-301">Сбой приведет к завершению работы подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="49603-301">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="49603-302">Журнал</span><span class="sxs-lookup"><span data-stu-id="49603-302">Log</span></span>
     * <span data-ttu-id="49603-303">Направление запроса: подключаемый модуль — > NuGet.</span><span class="sxs-lookup"><span data-stu-id="49603-303">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="49603-304">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-304">The request will contain:</span></span>
         * <span data-ttu-id="49603-305">уровень ведения журнала для запроса</span><span class="sxs-lookup"><span data-stu-id="49603-305">the log level for the request</span></span>
         * <span data-ttu-id="49603-306">сообщение для записи</span><span class="sxs-lookup"><span data-stu-id="49603-306">a message to log</span></span>
     * <span data-ttu-id="49603-307">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-307">A response will contain:</span></span>
         * <span data-ttu-id="49603-308">код ответа, указывающий результат операции.</span><span class="sxs-lookup"><span data-stu-id="49603-308">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="49603-309">Мониторинг завершения процесса NuGet</span><span class="sxs-lookup"><span data-stu-id="49603-309">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="49603-310">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-310">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="49603-311">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-311">The request will contain:</span></span>
         * <span data-ttu-id="49603-312">Идентификатор процесса NuGet</span><span class="sxs-lookup"><span data-stu-id="49603-312">the NuGet process ID</span></span>
     * <span data-ttu-id="49603-313">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-313">A response will contain:</span></span>
         * <span data-ttu-id="49603-314">код ответа, указывающий результат операции.</span><span class="sxs-lookup"><span data-stu-id="49603-314">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="49603-315">Предзагрузка пакета</span><span class="sxs-lookup"><span data-stu-id="49603-315">Prefetch package</span></span>
     * <span data-ttu-id="49603-316">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-316">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="49603-317">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-317">The request will contain:</span></span>
         * <span data-ttu-id="49603-318">ИДЕНТИФИКАТОР и версия пакета</span><span class="sxs-lookup"><span data-stu-id="49603-318">the package ID and version</span></span>
         * <span data-ttu-id="49603-319">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="49603-319">the package source repository location</span></span>
     * <span data-ttu-id="49603-320">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-320">A response will contain:</span></span>
         * <span data-ttu-id="49603-321">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-321">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="49603-322">Настройка учетных данных</span><span class="sxs-lookup"><span data-stu-id="49603-322">Set credentials</span></span>
     * <span data-ttu-id="49603-323">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-323">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="49603-324">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-324">The request will contain:</span></span>
         * <span data-ttu-id="49603-325">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="49603-325">the package source repository location</span></span>
         * <span data-ttu-id="49603-326">Последнее известное имя пользователя источника пакета, если оно доступно</span><span class="sxs-lookup"><span data-stu-id="49603-326">the last known package source username, if available</span></span>
         * <span data-ttu-id="49603-327">Последний известный пароль источника пакета, если он доступен</span><span class="sxs-lookup"><span data-stu-id="49603-327">the last known package source password, if available</span></span>
         * <span data-ttu-id="49603-328">Последнее известное имя пользователя-посредника, если оно доступно</span><span class="sxs-lookup"><span data-stu-id="49603-328">the last known proxy username, if available</span></span>
         * <span data-ttu-id="49603-329">Последний известный пароль прокси-сервера, если он доступен</span><span class="sxs-lookup"><span data-stu-id="49603-329">the last known proxy password, if available</span></span>
     * <span data-ttu-id="49603-330">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-330">A response will contain:</span></span>
         * <span data-ttu-id="49603-331">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-331">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="49603-332">Задать уровень ведения журнала</span><span class="sxs-lookup"><span data-stu-id="49603-332">Set log level</span></span>
     * <span data-ttu-id="49603-333">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-333">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="49603-334">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-334">The request will contain:</span></span>
         * <span data-ttu-id="49603-335">уровень журнала по умолчанию</span><span class="sxs-lookup"><span data-stu-id="49603-335">the default log level</span></span>
     * <span data-ttu-id="49603-336">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-336">A response will contain:</span></span>
         * <span data-ttu-id="49603-337">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-337">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="49603-338">Сообщения версии протокола *2.0.0*</span><span class="sxs-lookup"><span data-stu-id="49603-338">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="49603-339">Получение утверждений операции</span><span class="sxs-lookup"><span data-stu-id="49603-339">Get Operation Claims</span></span>

* <span data-ttu-id="49603-340">Направление запроса:  Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-340">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="49603-341">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-341">The request will contain:</span></span>
        * <span data-ttu-id="49603-342">Service index. JSON для источника пакета</span><span class="sxs-lookup"><span data-stu-id="49603-342">the service index.json for a package source</span></span>
        * <span data-ttu-id="49603-343">расположение исходного репозитория пакета</span><span class="sxs-lookup"><span data-stu-id="49603-343">the package source repository location</span></span>
    * <span data-ttu-id="49603-344">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-344">A response will contain:</span></span>
        * <span data-ttu-id="49603-345">код ответа, указывающий результат операции</span><span class="sxs-lookup"><span data-stu-id="49603-345">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="49603-346">перечислимые поддерживаемые операции, если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="49603-346">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="49603-347">Если подключаемый модуль не поддерживает источник пакета, подключаемый модуль должен вернуть пустой набор поддерживаемых операций.</span><span class="sxs-lookup"><span data-stu-id="49603-347">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="49603-348">Если индекс службы и источник пакета имеют значение null, то подключаемый модуль может ответить с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="49603-348">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="49603-349">Получение учетных данных проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="49603-349">Get Authentication Credentials</span></span>

* <span data-ttu-id="49603-350">Направление запроса: Подключаемый модуль NuGet-></span><span class="sxs-lookup"><span data-stu-id="49603-350">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="49603-351">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="49603-351">The request will contain:</span></span>
    * <span data-ttu-id="49603-352">URI</span><span class="sxs-lookup"><span data-stu-id="49603-352">Uri</span></span>
    * <span data-ttu-id="49603-353">Повтор</span><span class="sxs-lookup"><span data-stu-id="49603-353">isRetry</span></span>
    * <span data-ttu-id="49603-354">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="49603-354">NonInteractive</span></span>
    * <span data-ttu-id="49603-355">каншовдиалог</span><span class="sxs-lookup"><span data-stu-id="49603-355">CanShowDialog</span></span>
* <span data-ttu-id="49603-356">Ответ будет содержать</span><span class="sxs-lookup"><span data-stu-id="49603-356">A response will contain</span></span>
    * <span data-ttu-id="49603-357">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="49603-357">Username</span></span>
    * <span data-ttu-id="49603-358">Пароль</span><span class="sxs-lookup"><span data-stu-id="49603-358">Password</span></span>
    * <span data-ttu-id="49603-359">Сообщение</span><span class="sxs-lookup"><span data-stu-id="49603-359">Message</span></span>
    * <span data-ttu-id="49603-360">Список типов проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="49603-360">List of Auth Types</span></span>
    * <span data-ttu-id="49603-361">мессажереспонсекоде</span><span class="sxs-lookup"><span data-stu-id="49603-361">MessageResponseCode</span></span>
