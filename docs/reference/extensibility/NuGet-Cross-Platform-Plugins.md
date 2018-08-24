---
title: NuGet кросс-подключаемые модули платформы
description: NuGet cross платформы подключаемые модули для NuGet.exe, dotnet.exe, msbuild.exe и Visual Studio
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794184"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="8a4fb-103">NuGet кросс-подключаемые модули платформы</span><span class="sxs-lookup"><span data-stu-id="8a4fb-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="8a4fb-104">В NuGet 4.8 + добавлена поддержка между подключаемыми модулями платформы.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="8a4fb-105">Это было достигнуто с путем построения новой модели расширяемости подключаемый модуль, который должен соответствовать строгому набору правил операции.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="8a4fb-106">Подключаемые модули являются самодостаточные исполняемые файлы (runnables в мире .NET Core), который клиенты NuGet запуска в отдельном процессе.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="8a4fb-107">Это true записи один раз, везде запуска подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="8a4fb-108">Он будет работать со все клиентские средства NuGet.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="8a4fb-109">Подключаемые модули могут быть .NET Framework (NuGet.exe, MSBuild.exe и Visual Studio) или .NET Core (dotnet.exe).</span><span class="sxs-lookup"><span data-stu-id="8a4fb-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="8a4fb-110">Протокол с версиями связи между клиентом NuGet и подключаемый модуль определен.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="8a4fb-111">Во время подтверждения запуска 2 процессы согласование версии протокола.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="8a4fb-112">Чтобы охватить все сценарии средства клиента NuGet, один потребуется .NET Framework и .NET Core подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="8a4fb-113">Ниже описаны сочетания клиента/framework подключаемые модули.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="8a4fb-114">Клиентская программа</span><span class="sxs-lookup"><span data-stu-id="8a4fb-114">Client tool</span></span>  | <span data-ttu-id="8a4fb-115">Платформа</span><span class="sxs-lookup"><span data-stu-id="8a4fb-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="8a4fb-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8a4fb-116">Visual Studio</span></span> | <span data-ttu-id="8a4fb-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="8a4fb-117">.NET Framework</span></span> |
| <span data-ttu-id="8a4fb-118">DotNet.exe</span><span class="sxs-lookup"><span data-stu-id="8a4fb-118">dotnet.exe</span></span> | <span data-ttu-id="8a4fb-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="8a4fb-119">.NET Core</span></span> |
| <span data-ttu-id="8a4fb-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="8a4fb-120">NuGet.exe</span></span> | <span data-ttu-id="8a4fb-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="8a4fb-121">.NET Framework</span></span> |
| <span data-ttu-id="8a4fb-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="8a4fb-122">MSBuild.exe</span></span> | <span data-ttu-id="8a4fb-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="8a4fb-123">.NET Framework</span></span> |
| <span data-ttu-id="8a4fb-124">NuGet.exe в Mono</span><span class="sxs-lookup"><span data-stu-id="8a4fb-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="8a4fb-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="8a4fb-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="8a4fb-126">Как это работает</span><span class="sxs-lookup"><span data-stu-id="8a4fb-126">How does it work</span></span>

<span data-ttu-id="8a4fb-127">Верхнего уровня рабочего процесса можно описать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="8a4fb-128">NuGet обнаруживает доступных подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="8a4fb-129">Если это применимо, NuGet переберет все подключаемые модули в порядке приоритета и начинает их один за другим.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="8a4fb-130">NuGet будет использовать первый подключаемый модуль, который может обработать запрос.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="8a4fb-131">Подключаемые модули будет завершена, когда они больше не требуются.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="8a4fb-132">Подключаемый модуль общие требования</span><span class="sxs-lookup"><span data-stu-id="8a4fb-132">General plugin requirements</span></span>

<span data-ttu-id="8a4fb-133">Текущая версия протокола — *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="8a4fb-134">В данной версии действуют следующие требования:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="8a4fb-135">Имеют допустимый, доверенных Authenticode подпись сборки, которые будут выполняться в Windows и Mono.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="8a4fb-136">Для сборок, под управлением Linux и Mac еще не требуется специальных доверия.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="8a4fb-137">Важным проблемам</span><span class="sxs-lookup"><span data-stu-id="8a4fb-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="8a4fb-138">Поддержка запуска в текущем контексте безопасности клиентских средств NuGet без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="8a4fb-139">Например клиентские средства NuGet не выполняет повышение уровня или дополнительную инициализацию за пределами протокола подключаемый модуль, описанным ниже.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="8a4fb-140">Быть неинтерактивной, если не указано явным образом.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="8a4fb-141">Соответствовать версии протокола в согласованном подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="8a4fb-142">Отвечать на все запросы в течение разумного периода.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="8a4fb-143">Удовлетворять запросы отмены для любой выполняемой операции.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="8a4fb-144">Техническая спецификация описан более подробно в следующих спецификациях:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="8a4fb-145">Подключаемый модуль для загрузки пакета NuGet</span><span class="sxs-lookup"><span data-stu-id="8a4fb-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="8a4fb-146">NuGet кросс-Платформенная надстройка проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="8a4fb-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="8a4fb-147">Клиент — подключаемый модуль взаимодействия</span><span class="sxs-lookup"><span data-stu-id="8a4fb-147">Client - Plugin interaction</span></span>

<span data-ttu-id="8a4fb-148">Клиентские средства NuGet и подключаемые модули взаимодействуют с JSON, через стандартные потоки (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="8a4fb-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="8a4fb-149">Все данные должны быть в кодировке UTF-8.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="8a4fb-150">Подключаемые модули запускаются с аргументом «-подключаемый модуль».</span><span class="sxs-lookup"><span data-stu-id="8a4fb-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="8a4fb-151">В случае, если пользователь напрямую запускает исполняемый файл без этот аргумент подключаемого модуля, подключаемый модуль можно предоставить информационное сообщение, а не ждать подтверждения протокола.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="8a4fb-152">Время ожидания подтверждения протокола — 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="8a4fb-153">Подключаемый модуль следует выполнить настройки в качестве хватает сумму максимально.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="8a4fb-154">Клиентские средства NuGet будет запрашивать поддерживаемые операции подключаемый модуль, передавая индекс службы для источника NuGet.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="8a4fb-155">Подключаемый модуль может использовать индекс службы для проверки на наличие поддерживаемых типов служб.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="8a4fb-156">Обмен данными между клиентских средств NuGet и подключаемый модуль является двунаправленным.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="8a4fb-157">Каждый запрос имеет время ожидания 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="8a4fb-158">Если операции должны займет больше времени, процесс соответствующей должны отправлять сообщения о ходе выполнения для предотвращения превышения времени ожидания запроса. Через 1 минуту бездействия подключаемый модуль считается бездействующим и завершает работу.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="8a4fb-159">Установка подключаемого модуля и обнаружения</span><span class="sxs-lookup"><span data-stu-id="8a4fb-159">Plugin installation and discovery</span></span>

<span data-ttu-id="8a4fb-160">Подключаемые модули будут обнаружены через структуру каталогов на основе соглашения.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="8a4fb-161">Непрерывной интеграции и сценариев и Опытные пользователи могут использовать переменную среды для переопределения поведения.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="8a4fb-162">`NUGET_PLUGIN_PATHS` -Определяет подключаемых модулей, который будет использоваться для этого процесса NuGet, приоритет зарезервировано.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="8a4fb-163">Если эта переменная среды, оно переопределяет соглашение на основе обнаружения.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="8a4fb-164">Расположение пользователя, расположения домашней NuGet в `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="8a4fb-165">Это расположение не может быть переопределены.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-165">This location cannot be overriden.</span></span> <span data-ttu-id="8a4fb-166">Другой корневой каталог будет использоваться для подключаемых модулей .NET Core и .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="8a4fb-167">Платформа</span><span class="sxs-lookup"><span data-stu-id="8a4fb-167">Framework</span></span> | <span data-ttu-id="8a4fb-168">Корневое расположение обнаружения</span><span class="sxs-lookup"><span data-stu-id="8a4fb-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="8a4fb-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="8a4fb-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="8a4fb-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="8a4fb-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="8a4fb-171">Каждый подключаемый модуль должен быть установлен в его собственной папке.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="8a4fb-172">Точка входа подключаемый модуль будет имя установленного папки, с расширением DLL для .NET Core и расширением .exe для платформы .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="8a4fb-173">В данный момент нет описания функциональности пользователя для установки подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="8a4fb-174">Это всего лишь переместить необходимые файлы в заранее определенное место.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="8a4fb-175">Поддерживаемые операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-175">Supported operations</span></span>

<span data-ttu-id="8a4fb-176">Две операции поддерживаются в разделе нового протокола подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="8a4fb-177">Имя операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-177">Operation name</span></span> | <span data-ttu-id="8a4fb-178">Минимальное семейству.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-178">Minimum protocol version</span></span> | <span data-ttu-id="8a4fb-179">Минимальная версия клиента NuGet</span><span class="sxs-lookup"><span data-stu-id="8a4fb-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="8a4fb-180">Загрузить пакет</span><span class="sxs-lookup"><span data-stu-id="8a4fb-180">Download Package</span></span> | <span data-ttu-id="8a4fb-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="8a4fb-181">1.0.0</span></span> | <span data-ttu-id="8a4fb-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="8a4fb-182">4.3.0</span></span> |
| [<span data-ttu-id="8a4fb-183">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="8a4fb-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="8a4fb-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="8a4fb-184">2.0.0</span></span> | <span data-ttu-id="8a4fb-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="8a4fb-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="8a4fb-186">Запуск подключаемых модулей под нужная среда выполнения</span><span class="sxs-lookup"><span data-stu-id="8a4fb-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="8a4fb-187">Для NuGet в сценариях dotnet.exe подключаемые модули должны иметь возможность выполнения в группе, определенную среду выполнения из dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="8a4fb-188">Именно поставщик подключаемого модуля и производитель, чтобы убедиться в том, что используется сочетание совместимых dotnet.exe/plugin.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="8a4fb-189">Потенциальная проблема может возникнуть с подключаемыми модулями расположения пользователя, когда, например, dotnet.exe в разделе среды выполнения 2.0 пытается использовать подключаемый модуль для 2.1 среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="8a4fb-190">Возможности кэширования</span><span class="sxs-lookup"><span data-stu-id="8a4fb-190">Capabilities caching</span></span>

<span data-ttu-id="8a4fb-191">Проверка безопасности и создание подключаемых модулей является дорогостоящим.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="8a4fb-192">Операции загрузки происходит так чаще, чем операции проверки подлинности, однако только средний пользователь NuGet может работать подключаемый модуль проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="8a4fb-193">Чтобы упростить работу, NuGet будет кэшировать утверждения операции для указанного запроса.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="8a4fb-194">Этот кэш является одного подключаемого модуля с ключом подключаемого модуля, что путь подключаемого модуля и истечения срока действия для этого возможности кэша составляет 30 дней.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="8a4fb-195">Кэш находится в `%LocalAppData%/NuGet/plugins-cache` и будет заменена с переменной среды `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="8a4fb-196">Снимите этот [кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md), "Локальные" можно запускать с `plugins-cache` параметр.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="8a4fb-197">`all` Параметр "Локальные" теперь также удалит кэша подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="8a4fb-198">Индекс сообщений протокола</span><span class="sxs-lookup"><span data-stu-id="8a4fb-198">Protocol messages index</span></span>

<span data-ttu-id="8a4fb-199">Версия протокола *1.0.0* сообщений:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="8a4fb-200">Закрыть</span><span class="sxs-lookup"><span data-stu-id="8a4fb-200">Close</span></span>
    * <span data-ttu-id="8a4fb-201">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="8a4fb-202">Запрос будет содержать полезные данные не найдены</span><span class="sxs-lookup"><span data-stu-id="8a4fb-202">The request will contain no payload</span></span>
    * <span data-ttu-id="8a4fb-203">Ответ не ожидается.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-203">No response is expected.</span></span>  <span data-ttu-id="8a4fb-204">Адекватный ответ касается незамедлительно завершения процесса подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="8a4fb-205">Скопируйте файлы в пакете</span><span class="sxs-lookup"><span data-stu-id="8a4fb-205">Copy files in package</span></span>
    * <span data-ttu-id="8a4fb-206">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="8a4fb-207">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-207">The request will contain:</span></span>
        * <span data-ttu-id="8a4fb-208">ИД пакета и версии</span><span class="sxs-lookup"><span data-stu-id="8a4fb-208">the package ID and version</span></span>
        * <span data-ttu-id="8a4fb-209">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-209">the package source repository location</span></span>
        * <span data-ttu-id="8a4fb-210">путь к целевому каталогу</span><span class="sxs-lookup"><span data-stu-id="8a4fb-210">destination directory path</span></span>
        * <span data-ttu-id="8a4fb-211">Перечисление файлов в пакете для копирования конечный каталог</span><span class="sxs-lookup"><span data-stu-id="8a4fb-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="8a4fb-212">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-212">A response will contain:</span></span>
        * <span data-ttu-id="8a4fb-213">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="8a4fb-214">Перечисление полные пути для копирования файлов в каталоге назначения, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="8a4fb-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="8a4fb-215">Скопируйте файл пакета (файла nupkg)</span><span class="sxs-lookup"><span data-stu-id="8a4fb-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="8a4fb-216">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="8a4fb-217">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-217">The request will contain:</span></span>
        * <span data-ttu-id="8a4fb-218">ИД пакета и версии</span><span class="sxs-lookup"><span data-stu-id="8a4fb-218">the package ID and version</span></span>
        * <span data-ttu-id="8a4fb-219">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-219">the package source repository location</span></span>
        * <span data-ttu-id="8a4fb-220">путь к конечному файлу</span><span class="sxs-lookup"><span data-stu-id="8a4fb-220">the destination file path</span></span>
    * <span data-ttu-id="8a4fb-221">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-221">A response will contain:</span></span>
        * <span data-ttu-id="8a4fb-222">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="8a4fb-223">Получение учетных данных</span><span class="sxs-lookup"><span data-stu-id="8a4fb-223">Get credentials</span></span>
    * <span data-ttu-id="8a4fb-224">Запросить направление: подключаемый модуль "->" NuGet</span><span class="sxs-lookup"><span data-stu-id="8a4fb-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="8a4fb-225">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-225">The request will contain:</span></span>
        * <span data-ttu-id="8a4fb-226">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-226">the package source repository location</span></span>
        * <span data-ttu-id="8a4fb-227">Код состояния HTTP, полученный из репозитория источника пакетов с помощью текущих учетных данных</span><span class="sxs-lookup"><span data-stu-id="8a4fb-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="8a4fb-228">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-228">A response will contain:</span></span>
        * <span data-ttu-id="8a4fb-229">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="8a4fb-230">имя пользователя, если он доступен</span><span class="sxs-lookup"><span data-stu-id="8a4fb-230">a username, if available</span></span>
        * <span data-ttu-id="8a4fb-231">пароль, если он доступен</span><span class="sxs-lookup"><span data-stu-id="8a4fb-231">a password, if available</span></span>

5.  <span data-ttu-id="8a4fb-232">Получить файлы в пакете</span><span class="sxs-lookup"><span data-stu-id="8a4fb-232">Get files in package</span></span>
    * <span data-ttu-id="8a4fb-233">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="8a4fb-234">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-234">The request will contain:</span></span>
        * <span data-ttu-id="8a4fb-235">ИД пакета и версии</span><span class="sxs-lookup"><span data-stu-id="8a4fb-235">the package ID and version</span></span>
        * <span data-ttu-id="8a4fb-236">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-236">the package source repository location</span></span>
    * <span data-ttu-id="8a4fb-237">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-237">A response will contain:</span></span>
        * <span data-ttu-id="8a4fb-238">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="8a4fb-239">Перечислимый объект путей к файлам в пакете, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="8a4fb-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="8a4fb-240">Получить операции утверждения</span><span class="sxs-lookup"><span data-stu-id="8a4fb-240">Get operation claims</span></span> 
    * <span data-ttu-id="8a4fb-241">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="8a4fb-242">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-242">The request will contain:</span></span>
        * <span data-ttu-id="8a4fb-243">index.json службы для источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="8a4fb-244">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-244">the package source repository location</span></span>
    * <span data-ttu-id="8a4fb-245">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-245">A response will contain:</span></span>
        * <span data-ttu-id="8a4fb-246">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="8a4fb-247">Перечисление поддерживаемые операции (например: загрузка пакета), если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="8a4fb-248">Если подключаемый модуль не поддерживает источник, подключаемый модуль должен возвращать пустой набор поддерживаемых операций.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="8a4fb-249">Это сообщение была обновлена в версии *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="8a4fb-250">Это на стороне клиента для сохранения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="8a4fb-251">Получить хэш пакета.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-251">Get package hash</span></span>
    * <span data-ttu-id="8a4fb-252">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="8a4fb-253">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-253">The request will contain:</span></span>
        * <span data-ttu-id="8a4fb-254">ИД пакета и версии</span><span class="sxs-lookup"><span data-stu-id="8a4fb-254">the package ID and version</span></span>
        * <span data-ttu-id="8a4fb-255">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-255">the package source repository location</span></span>
        * <span data-ttu-id="8a4fb-256">хэш-алгоритм</span><span class="sxs-lookup"><span data-stu-id="8a4fb-256">the hash algorithm</span></span>
    * <span data-ttu-id="8a4fb-257">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-257">A response will contain:</span></span>
        * <span data-ttu-id="8a4fb-258">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="8a4fb-259">Хэш файла пакета, используя запрошенный хэш-алгоритм, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="8a4fb-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="8a4fb-260">Получение версий пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-260">Get package versions</span></span>
    * <span data-ttu-id="8a4fb-261">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="8a4fb-262">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-262">The request will contain:</span></span>
        * <span data-ttu-id="8a4fb-263">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-263">the package ID</span></span>
        * <span data-ttu-id="8a4fb-264">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-264">the package source repository location</span></span>
    * <span data-ttu-id="8a4fb-265">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-265">A response will contain:</span></span>
        * <span data-ttu-id="8a4fb-266">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="8a4fb-267">Перечисление версий пакета, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="8a4fb-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="8a4fb-268">Получите индекс службы</span><span class="sxs-lookup"><span data-stu-id="8a4fb-268">Get service index</span></span>
    * <span data-ttu-id="8a4fb-269">Запросить направление: подключаемый модуль "->" NuGet</span><span class="sxs-lookup"><span data-stu-id="8a4fb-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="8a4fb-270">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-270">The request will contain:</span></span>
        * <span data-ttu-id="8a4fb-271">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-271">the package source repository location</span></span>
    * <span data-ttu-id="8a4fb-272">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-272">A response will contain:</span></span>
        * <span data-ttu-id="8a4fb-273">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="8a4fb-274">Индекс службы, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="8a4fb-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="8a4fb-275">Подтверждение</span><span class="sxs-lookup"><span data-stu-id="8a4fb-275">Handshake</span></span>
     * <span data-ttu-id="8a4fb-276">Запросить направление: подключаемого модуля NuGet <> –</span><span class="sxs-lookup"><span data-stu-id="8a4fb-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="8a4fb-277">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-277">The request will contain:</span></span>
         * <span data-ttu-id="8a4fb-278">Текущая версия протокола подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="8a4fb-279">Минимальная поддерживаемая версия протокола подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="8a4fb-280">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-280">A response will contain:</span></span>
         * <span data-ttu-id="8a4fb-281">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="8a4fb-282">версия согласованный протокол, если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="8a4fb-283">Сбой приведет к завершению работы подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="8a4fb-284">Инициализация</span><span class="sxs-lookup"><span data-stu-id="8a4fb-284">Initialize</span></span>
     * <span data-ttu-id="8a4fb-285">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="8a4fb-286">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-286">The request will contain:</span></span>
         * <span data-ttu-id="8a4fb-287">версия средства клиента NuGet</span><span class="sxs-lookup"><span data-stu-id="8a4fb-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="8a4fb-288">NuGet средство эффективный язык клиента.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="8a4fb-289">Это учитывает параметр ForceEnglishOutput, если используется.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="8a4fb-290">по умолчанию время ожидания запроса, который заменяет значение по умолчанию протокол.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="8a4fb-291">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-291">A response will contain:</span></span>
         * <span data-ttu-id="8a4fb-292">код ответа, указывающее результат операции.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="8a4fb-293">Сбой приведет к завершению работы подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="8a4fb-294">Журнал</span><span class="sxs-lookup"><span data-stu-id="8a4fb-294">Log</span></span>
     * <span data-ttu-id="8a4fb-295">Запросить направление: подключаемый модуль "->" NuGet</span><span class="sxs-lookup"><span data-stu-id="8a4fb-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="8a4fb-296">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-296">The request will contain:</span></span>
         * <span data-ttu-id="8a4fb-297">уровень ведения журнала для запроса</span><span class="sxs-lookup"><span data-stu-id="8a4fb-297">the log level for the request</span></span>
         * <span data-ttu-id="8a4fb-298">в журнал сообщения</span><span class="sxs-lookup"><span data-stu-id="8a4fb-298">a message to log</span></span>
     * <span data-ttu-id="8a4fb-299">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-299">A response will contain:</span></span>
         * <span data-ttu-id="8a4fb-300">код ответа, указывающее результат операции.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="8a4fb-301">Отслеживать завершения работы процесса NuGet</span><span class="sxs-lookup"><span data-stu-id="8a4fb-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="8a4fb-302">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="8a4fb-303">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-303">The request will contain:</span></span>
         * <span data-ttu-id="8a4fb-304">Идентификатор процесса NuGet</span><span class="sxs-lookup"><span data-stu-id="8a4fb-304">the NuGet process ID</span></span>
     * <span data-ttu-id="8a4fb-305">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-305">A response will contain:</span></span>
         * <span data-ttu-id="8a4fb-306">код ответа, указывающее результат операции.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="8a4fb-307">Предварительная загрузка пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-307">Prefetch package</span></span>
     * <span data-ttu-id="8a4fb-308">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="8a4fb-309">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-309">The request will contain:</span></span>
         * <span data-ttu-id="8a4fb-310">ИД пакета и версии</span><span class="sxs-lookup"><span data-stu-id="8a4fb-310">the package ID and version</span></span>
         * <span data-ttu-id="8a4fb-311">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-311">the package source repository location</span></span>
     * <span data-ttu-id="8a4fb-312">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-312">A response will contain:</span></span>
         * <span data-ttu-id="8a4fb-313">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="8a4fb-314">Задание учетных данных</span><span class="sxs-lookup"><span data-stu-id="8a4fb-314">Set credentials</span></span>
     * <span data-ttu-id="8a4fb-315">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="8a4fb-316">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-316">The request will contain:</span></span>
         * <span data-ttu-id="8a4fb-317">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-317">the package source repository location</span></span>
         * <span data-ttu-id="8a4fb-318">последний username источника пакетов, если он доступен</span><span class="sxs-lookup"><span data-stu-id="8a4fb-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="8a4fb-319">Последний пароль источника пакетов, если он доступен</span><span class="sxs-lookup"><span data-stu-id="8a4fb-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="8a4fb-320">последние известные прокси-сервер имя пользователя, если он доступен</span><span class="sxs-lookup"><span data-stu-id="8a4fb-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="8a4fb-321">Последний пароль известных прокси-сервера, если он доступен</span><span class="sxs-lookup"><span data-stu-id="8a4fb-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="8a4fb-322">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-322">A response will contain:</span></span>
         * <span data-ttu-id="8a4fb-323">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="8a4fb-324">Уровень ведения журнала набора</span><span class="sxs-lookup"><span data-stu-id="8a4fb-324">Set log level</span></span>
     * <span data-ttu-id="8a4fb-325">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="8a4fb-326">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-326">The request will contain:</span></span>
         * <span data-ttu-id="8a4fb-327">уровень ведения журнала по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8a4fb-327">the default log level</span></span>
     * <span data-ttu-id="8a4fb-328">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-328">A response will contain:</span></span>
         * <span data-ttu-id="8a4fb-329">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="8a4fb-330">Версия протокола *2.0.0* сообщений</span><span class="sxs-lookup"><span data-stu-id="8a4fb-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="8a4fb-331">Получить операции утверждения</span><span class="sxs-lookup"><span data-stu-id="8a4fb-331">Get Operation Claims</span></span>

* <span data-ttu-id="8a4fb-332">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="8a4fb-333">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-333">The request will contain:</span></span>
        * <span data-ttu-id="8a4fb-334">index.json службы для источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="8a4fb-335">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="8a4fb-335">the package source repository location</span></span>
    * <span data-ttu-id="8a4fb-336">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-336">A response will contain:</span></span>
        * <span data-ttu-id="8a4fb-337">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="8a4fb-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="8a4fb-338">Перечислимый объект по поддерживаемым операциям, если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="8a4fb-339">Если подключаемый модуль не поддерживает источник, подключаемый модуль должен возвращать пустой набор поддерживаемых операций.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="8a4fb-340">Если источник индекса и пакета службы имеют значение null, подключаемый модуль можно ответить с помощью проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8a4fb-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="8a4fb-341">Получить учетные данные проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="8a4fb-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="8a4fb-342">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="8a4fb-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="8a4fb-343">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="8a4fb-343">The request will contain:</span></span>
    * <span data-ttu-id="8a4fb-344">URI</span><span class="sxs-lookup"><span data-stu-id="8a4fb-344">Uri</span></span>
    * <span data-ttu-id="8a4fb-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="8a4fb-345">isRetry</span></span>
    * <span data-ttu-id="8a4fb-346">Неинтерактивная</span><span class="sxs-lookup"><span data-stu-id="8a4fb-346">NonInteractive</span></span>
    * <span data-ttu-id="8a4fb-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="8a4fb-347">CanShowDialog</span></span>
* <span data-ttu-id="8a4fb-348">Ответ будет содержать</span><span class="sxs-lookup"><span data-stu-id="8a4fb-348">A response will contain</span></span>
    * <span data-ttu-id="8a4fb-349">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="8a4fb-349">Username</span></span>
    * <span data-ttu-id="8a4fb-350">Пароль</span><span class="sxs-lookup"><span data-stu-id="8a4fb-350">Password</span></span>
    * <span data-ttu-id="8a4fb-351">Сообщение</span><span class="sxs-lookup"><span data-stu-id="8a4fb-351">Message</span></span>
    * <span data-ttu-id="8a4fb-352">Список типов проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="8a4fb-352">List of Auth Types</span></span>
    * <span data-ttu-id="8a4fb-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="8a4fb-353">MessageResponseCode</span></span>