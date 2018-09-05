---
title: NuGet кросс-подключаемые модули платформы
description: NuGet cross платформы подключаемые модули для NuGet.exe, dotnet.exe, msbuild.exe и Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: fdefc5b6189051fd83b2de644080284c09dd85f4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548210"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="5be20-103">NuGet кросс-подключаемые модули платформы</span><span class="sxs-lookup"><span data-stu-id="5be20-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="5be20-104">В NuGet 4.8 + добавлена поддержка между подключаемыми модулями платформы.</span><span class="sxs-lookup"><span data-stu-id="5be20-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="5be20-105">Это было достигнуто с путем построения новой модели расширяемости подключаемый модуль, который должен соответствовать строгому набору правил операции.</span><span class="sxs-lookup"><span data-stu-id="5be20-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="5be20-106">Подключаемые модули являются самодостаточные исполняемые файлы (runnables в мире .NET Core), который клиенты NuGet запуска в отдельном процессе.</span><span class="sxs-lookup"><span data-stu-id="5be20-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="5be20-107">Это true записи один раз, везде запуска подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="5be20-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="5be20-108">Он будет работать со все клиентские средства NuGet.</span><span class="sxs-lookup"><span data-stu-id="5be20-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="5be20-109">Подключаемые модули могут быть .NET Framework (NuGet.exe, MSBuild.exe и Visual Studio) или .NET Core (dotnet.exe).</span><span class="sxs-lookup"><span data-stu-id="5be20-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="5be20-110">Протокол с версиями связи между клиентом NuGet и подключаемый модуль определен.</span><span class="sxs-lookup"><span data-stu-id="5be20-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="5be20-111">Во время подтверждения запуска 2 процессы согласование версии протокола.</span><span class="sxs-lookup"><span data-stu-id="5be20-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="5be20-112">Чтобы охватить все сценарии средства клиента NuGet, один потребуется .NET Framework и .NET Core подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="5be20-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="5be20-113">Ниже описаны сочетания клиента/framework подключаемые модули.</span><span class="sxs-lookup"><span data-stu-id="5be20-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="5be20-114">Клиентская программа</span><span class="sxs-lookup"><span data-stu-id="5be20-114">Client tool</span></span>  | <span data-ttu-id="5be20-115">Платформа</span><span class="sxs-lookup"><span data-stu-id="5be20-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="5be20-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5be20-116">Visual Studio</span></span> | <span data-ttu-id="5be20-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5be20-117">.NET Framework</span></span> |
| <span data-ttu-id="5be20-118">DotNet.exe</span><span class="sxs-lookup"><span data-stu-id="5be20-118">dotnet.exe</span></span> | <span data-ttu-id="5be20-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="5be20-119">.NET Core</span></span> |
| <span data-ttu-id="5be20-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="5be20-120">NuGet.exe</span></span> | <span data-ttu-id="5be20-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5be20-121">.NET Framework</span></span> |
| <span data-ttu-id="5be20-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="5be20-122">MSBuild.exe</span></span> | <span data-ttu-id="5be20-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5be20-123">.NET Framework</span></span> |
| <span data-ttu-id="5be20-124">NuGet.exe в Mono</span><span class="sxs-lookup"><span data-stu-id="5be20-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="5be20-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5be20-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="5be20-126">Как это работает</span><span class="sxs-lookup"><span data-stu-id="5be20-126">How does it work</span></span>

<span data-ttu-id="5be20-127">Верхнего уровня рабочего процесса можно описать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5be20-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="5be20-128">NuGet обнаруживает доступных подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="5be20-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="5be20-129">Если это применимо, NuGet переберет все подключаемые модули в порядке приоритета и начинает их один за другим.</span><span class="sxs-lookup"><span data-stu-id="5be20-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="5be20-130">NuGet будет использовать первый подключаемый модуль, который может обработать запрос.</span><span class="sxs-lookup"><span data-stu-id="5be20-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="5be20-131">Подключаемые модули будет завершена, когда они больше не требуются.</span><span class="sxs-lookup"><span data-stu-id="5be20-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="5be20-132">Подключаемый модуль общие требования</span><span class="sxs-lookup"><span data-stu-id="5be20-132">General plugin requirements</span></span>

<span data-ttu-id="5be20-133">Текущая версия протокола — *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="5be20-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="5be20-134">В данной версии действуют следующие требования:</span><span class="sxs-lookup"><span data-stu-id="5be20-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="5be20-135">Имеют допустимый, доверенных Authenticode подпись сборки, которые будут выполняться в Windows и Mono.</span><span class="sxs-lookup"><span data-stu-id="5be20-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="5be20-136">Для сборок, под управлением Linux и Mac еще не требуется специальных доверия.</span><span class="sxs-lookup"><span data-stu-id="5be20-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="5be20-137">Важным проблемам</span><span class="sxs-lookup"><span data-stu-id="5be20-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="5be20-138">Поддержка запуска в текущем контексте безопасности клиентских средств NuGet без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="5be20-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="5be20-139">Например клиентские средства NuGet не выполняет повышение уровня или дополнительную инициализацию за пределами протокола подключаемый модуль, описанным ниже.</span><span class="sxs-lookup"><span data-stu-id="5be20-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="5be20-140">Быть неинтерактивной, если не указано явным образом.</span><span class="sxs-lookup"><span data-stu-id="5be20-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="5be20-141">Соответствовать версии протокола в согласованном подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="5be20-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="5be20-142">Отвечать на все запросы в течение разумного периода.</span><span class="sxs-lookup"><span data-stu-id="5be20-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="5be20-143">Удовлетворять запросы отмены для любой выполняемой операции.</span><span class="sxs-lookup"><span data-stu-id="5be20-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="5be20-144">Техническая спецификация описан более подробно в следующих спецификациях:</span><span class="sxs-lookup"><span data-stu-id="5be20-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="5be20-145">Подключаемый модуль для загрузки пакета NuGet</span><span class="sxs-lookup"><span data-stu-id="5be20-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="5be20-146">NuGet кросс-Платформенная надстройка проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="5be20-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="5be20-147">Клиент — подключаемый модуль взаимодействия</span><span class="sxs-lookup"><span data-stu-id="5be20-147">Client - Plugin interaction</span></span>

<span data-ttu-id="5be20-148">Клиентские средства NuGet и подключаемые модули взаимодействуют с JSON, через стандартные потоки (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="5be20-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="5be20-149">Все данные должны быть в кодировке UTF-8.</span><span class="sxs-lookup"><span data-stu-id="5be20-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="5be20-150">Подключаемые модули запускаются с аргументом «-подключаемый модуль».</span><span class="sxs-lookup"><span data-stu-id="5be20-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="5be20-151">В случае, если пользователь напрямую запускает исполняемый файл без этот аргумент подключаемого модуля, подключаемый модуль можно предоставить информационное сообщение, а не ждать подтверждения протокола.</span><span class="sxs-lookup"><span data-stu-id="5be20-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="5be20-152">Время ожидания подтверждения протокола — 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="5be20-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="5be20-153">Подключаемый модуль следует выполнить настройки в качестве хватает сумму максимально.</span><span class="sxs-lookup"><span data-stu-id="5be20-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="5be20-154">Клиентские средства NuGet будет запрашивать поддерживаемые операции подключаемый модуль, передавая индекс службы для источника NuGet.</span><span class="sxs-lookup"><span data-stu-id="5be20-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="5be20-155">Подключаемый модуль может использовать индекс службы для проверки на наличие поддерживаемых типов служб.</span><span class="sxs-lookup"><span data-stu-id="5be20-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="5be20-156">Обмен данными между клиентских средств NuGet и подключаемый модуль является двунаправленным.</span><span class="sxs-lookup"><span data-stu-id="5be20-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="5be20-157">Каждый запрос имеет время ожидания 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="5be20-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="5be20-158">Если операции должны займет больше времени, процесс соответствующей должны отправлять сообщения о ходе выполнения для предотвращения превышения времени ожидания запроса. Через 1 минуту бездействия подключаемый модуль считается бездействующим и завершает работу.</span><span class="sxs-lookup"><span data-stu-id="5be20-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="5be20-159">Установка подключаемого модуля и обнаружения</span><span class="sxs-lookup"><span data-stu-id="5be20-159">Plugin installation and discovery</span></span>

<span data-ttu-id="5be20-160">Подключаемые модули будут обнаружены через структуру каталогов на основе соглашения.</span><span class="sxs-lookup"><span data-stu-id="5be20-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="5be20-161">Непрерывной интеграции и сценариев и Опытные пользователи могут использовать переменную среды для переопределения поведения.</span><span class="sxs-lookup"><span data-stu-id="5be20-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="5be20-162">`NUGET_PLUGIN_PATHS` -Определяет подключаемых модулей, который будет использоваться для этого процесса NuGet, приоритет зарезервировано.</span><span class="sxs-lookup"><span data-stu-id="5be20-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="5be20-163">Если эта переменная среды, оно переопределяет соглашение на основе обнаружения.</span><span class="sxs-lookup"><span data-stu-id="5be20-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="5be20-164">Расположение пользователя, расположения домашней NuGet в `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="5be20-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="5be20-165">Это расположение не может быть переопределены.</span><span class="sxs-lookup"><span data-stu-id="5be20-165">This location cannot be overriden.</span></span> <span data-ttu-id="5be20-166">Другой корневой каталог будет использоваться для подключаемых модулей .NET Core и .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5be20-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="5be20-167">Платформа</span><span class="sxs-lookup"><span data-stu-id="5be20-167">Framework</span></span> | <span data-ttu-id="5be20-168">Корневое расположение обнаружения</span><span class="sxs-lookup"><span data-stu-id="5be20-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="5be20-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="5be20-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="5be20-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="5be20-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="5be20-171">Каждый подключаемый модуль должен быть установлен в его собственной папке.</span><span class="sxs-lookup"><span data-stu-id="5be20-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="5be20-172">Точка входа подключаемый модуль будет имя установленного папки, с расширением DLL для .NET Core и расширением .exe для платформы .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5be20-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="5be20-173">В данный момент нет описания функциональности пользователя для установки подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="5be20-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="5be20-174">Это всего лишь переместить необходимые файлы в заранее определенное место.</span><span class="sxs-lookup"><span data-stu-id="5be20-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="5be20-175">Поддерживаемые операции</span><span class="sxs-lookup"><span data-stu-id="5be20-175">Supported operations</span></span>

<span data-ttu-id="5be20-176">Две операции поддерживаются в разделе нового протокола подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="5be20-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="5be20-177">Имя операции</span><span class="sxs-lookup"><span data-stu-id="5be20-177">Operation name</span></span> | <span data-ttu-id="5be20-178">Минимальное семейству.</span><span class="sxs-lookup"><span data-stu-id="5be20-178">Minimum protocol version</span></span> | <span data-ttu-id="5be20-179">Минимальная версия клиента NuGet</span><span class="sxs-lookup"><span data-stu-id="5be20-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="5be20-180">Загрузить пакет</span><span class="sxs-lookup"><span data-stu-id="5be20-180">Download Package</span></span> | <span data-ttu-id="5be20-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="5be20-181">1.0.0</span></span> | <span data-ttu-id="5be20-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="5be20-182">4.3.0</span></span> |
| [<span data-ttu-id="5be20-183">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="5be20-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="5be20-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="5be20-184">2.0.0</span></span> | <span data-ttu-id="5be20-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="5be20-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="5be20-186">Запуск подключаемых модулей под нужная среда выполнения</span><span class="sxs-lookup"><span data-stu-id="5be20-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="5be20-187">Для NuGet в сценариях dotnet.exe подключаемые модули должны иметь возможность выполнения в группе, определенную среду выполнения из dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="5be20-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="5be20-188">Именно поставщик подключаемого модуля и производитель, чтобы убедиться в том, что используется сочетание совместимых dotnet.exe/plugin.</span><span class="sxs-lookup"><span data-stu-id="5be20-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="5be20-189">Потенциальная проблема может возникнуть с подключаемыми модулями расположения пользователя, когда, например, dotnet.exe в разделе среды выполнения 2.0 пытается использовать подключаемый модуль для 2.1 среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="5be20-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="5be20-190">Возможности кэширования</span><span class="sxs-lookup"><span data-stu-id="5be20-190">Capabilities caching</span></span>

<span data-ttu-id="5be20-191">Проверка безопасности и создание подключаемых модулей является дорогостоящим.</span><span class="sxs-lookup"><span data-stu-id="5be20-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="5be20-192">Операции загрузки происходит так чаще, чем операции проверки подлинности, однако только средний пользователь NuGet может работать подключаемый модуль проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5be20-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="5be20-193">Чтобы упростить работу, NuGet будет кэшировать утверждения операции для указанного запроса.</span><span class="sxs-lookup"><span data-stu-id="5be20-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="5be20-194">Этот кэш является одного подключаемого модуля с ключом подключаемого модуля, что путь подключаемого модуля и истечения срока действия для этого возможности кэша составляет 30 дней.</span><span class="sxs-lookup"><span data-stu-id="5be20-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="5be20-195">Кэш находится в `%LocalAppData%/NuGet/plugins-cache` и будет заменена с переменной среды `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="5be20-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="5be20-196">Снимите этот [кэша](../../consume-packages/managing-the-global-packages-and-cache-folders.md), "Локальные" можно запускать с `plugins-cache` параметр.</span><span class="sxs-lookup"><span data-stu-id="5be20-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="5be20-197">`all` Параметр "Локальные" теперь также удалит кэша подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="5be20-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="5be20-198">Индекс сообщений протокола</span><span class="sxs-lookup"><span data-stu-id="5be20-198">Protocol messages index</span></span>

<span data-ttu-id="5be20-199">Версия протокола *1.0.0* сообщений:</span><span class="sxs-lookup"><span data-stu-id="5be20-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="5be20-200">Закрыть</span><span class="sxs-lookup"><span data-stu-id="5be20-200">Close</span></span>
    * <span data-ttu-id="5be20-201">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5be20-202">Запрос будет содержать полезные данные не найдены</span><span class="sxs-lookup"><span data-stu-id="5be20-202">The request will contain no payload</span></span>
    * <span data-ttu-id="5be20-203">Ответ не ожидается.</span><span class="sxs-lookup"><span data-stu-id="5be20-203">No response is expected.</span></span>  <span data-ttu-id="5be20-204">Адекватный ответ касается незамедлительно завершения процесса подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="5be20-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="5be20-205">Скопируйте файлы в пакете</span><span class="sxs-lookup"><span data-stu-id="5be20-205">Copy files in package</span></span>
    * <span data-ttu-id="5be20-206">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5be20-207">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-207">The request will contain:</span></span>
        * <span data-ttu-id="5be20-208">ИД пакета и версии</span><span class="sxs-lookup"><span data-stu-id="5be20-208">the package ID and version</span></span>
        * <span data-ttu-id="5be20-209">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-209">the package source repository location</span></span>
        * <span data-ttu-id="5be20-210">путь к целевому каталогу</span><span class="sxs-lookup"><span data-stu-id="5be20-210">destination directory path</span></span>
        * <span data-ttu-id="5be20-211">Перечисление файлов в пакете для копирования конечный каталог</span><span class="sxs-lookup"><span data-stu-id="5be20-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="5be20-212">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-212">A response will contain:</span></span>
        * <span data-ttu-id="5be20-213">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5be20-214">Перечисление полные пути для копирования файлов в каталоге назначения, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="5be20-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="5be20-215">Скопируйте файл пакета (файла nupkg)</span><span class="sxs-lookup"><span data-stu-id="5be20-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="5be20-216">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5be20-217">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-217">The request will contain:</span></span>
        * <span data-ttu-id="5be20-218">ИД пакета и версии</span><span class="sxs-lookup"><span data-stu-id="5be20-218">the package ID and version</span></span>
        * <span data-ttu-id="5be20-219">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-219">the package source repository location</span></span>
        * <span data-ttu-id="5be20-220">путь к конечному файлу</span><span class="sxs-lookup"><span data-stu-id="5be20-220">the destination file path</span></span>
    * <span data-ttu-id="5be20-221">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-221">A response will contain:</span></span>
        * <span data-ttu-id="5be20-222">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="5be20-223">Получение учетных данных</span><span class="sxs-lookup"><span data-stu-id="5be20-223">Get credentials</span></span>
    * <span data-ttu-id="5be20-224">Запросить направление: подключаемый модуль "->" NuGet</span><span class="sxs-lookup"><span data-stu-id="5be20-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="5be20-225">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-225">The request will contain:</span></span>
        * <span data-ttu-id="5be20-226">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-226">the package source repository location</span></span>
        * <span data-ttu-id="5be20-227">Код состояния HTTP, полученный из репозитория источника пакетов с помощью текущих учетных данных</span><span class="sxs-lookup"><span data-stu-id="5be20-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="5be20-228">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-228">A response will contain:</span></span>
        * <span data-ttu-id="5be20-229">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5be20-230">имя пользователя, если он доступен</span><span class="sxs-lookup"><span data-stu-id="5be20-230">a username, if available</span></span>
        * <span data-ttu-id="5be20-231">пароль, если он доступен</span><span class="sxs-lookup"><span data-stu-id="5be20-231">a password, if available</span></span>

5.  <span data-ttu-id="5be20-232">Получить файлы в пакете</span><span class="sxs-lookup"><span data-stu-id="5be20-232">Get files in package</span></span>
    * <span data-ttu-id="5be20-233">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5be20-234">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-234">The request will contain:</span></span>
        * <span data-ttu-id="5be20-235">ИД пакета и версии</span><span class="sxs-lookup"><span data-stu-id="5be20-235">the package ID and version</span></span>
        * <span data-ttu-id="5be20-236">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-236">the package source repository location</span></span>
    * <span data-ttu-id="5be20-237">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-237">A response will contain:</span></span>
        * <span data-ttu-id="5be20-238">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5be20-239">Перечислимый объект путей к файлам в пакете, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="5be20-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="5be20-240">Получить операции утверждения</span><span class="sxs-lookup"><span data-stu-id="5be20-240">Get operation claims</span></span> 
    * <span data-ttu-id="5be20-241">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5be20-242">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-242">The request will contain:</span></span>
        * <span data-ttu-id="5be20-243">index.json службы для источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="5be20-244">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-244">the package source repository location</span></span>
    * <span data-ttu-id="5be20-245">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-245">A response will contain:</span></span>
        * <span data-ttu-id="5be20-246">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5be20-247">Перечисление поддерживаемые операции (например: загрузка пакета), если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="5be20-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="5be20-248">Если подключаемый модуль не поддерживает источник, подключаемый модуль должен возвращать пустой набор поддерживаемых операций.</span><span class="sxs-lookup"><span data-stu-id="5be20-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="5be20-249">Это сообщение была обновлена в версии *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="5be20-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="5be20-250">Это на стороне клиента для сохранения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="5be20-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="5be20-251">Получить хэш пакета.</span><span class="sxs-lookup"><span data-stu-id="5be20-251">Get package hash</span></span>
    * <span data-ttu-id="5be20-252">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5be20-253">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-253">The request will contain:</span></span>
        * <span data-ttu-id="5be20-254">ИД пакета и версии</span><span class="sxs-lookup"><span data-stu-id="5be20-254">the package ID and version</span></span>
        * <span data-ttu-id="5be20-255">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-255">the package source repository location</span></span>
        * <span data-ttu-id="5be20-256">хэш-алгоритм</span><span class="sxs-lookup"><span data-stu-id="5be20-256">the hash algorithm</span></span>
    * <span data-ttu-id="5be20-257">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-257">A response will contain:</span></span>
        * <span data-ttu-id="5be20-258">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5be20-259">Хэш файла пакета, используя запрошенный хэш-алгоритм, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="5be20-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="5be20-260">Получение версий пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-260">Get package versions</span></span>
    * <span data-ttu-id="5be20-261">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5be20-262">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-262">The request will contain:</span></span>
        * <span data-ttu-id="5be20-263">Идентификатор пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-263">the package ID</span></span>
        * <span data-ttu-id="5be20-264">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-264">the package source repository location</span></span>
    * <span data-ttu-id="5be20-265">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-265">A response will contain:</span></span>
        * <span data-ttu-id="5be20-266">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5be20-267">Перечисление версий пакета, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="5be20-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="5be20-268">Получите индекс службы</span><span class="sxs-lookup"><span data-stu-id="5be20-268">Get service index</span></span>
    * <span data-ttu-id="5be20-269">Запросить направление: подключаемый модуль "->" NuGet</span><span class="sxs-lookup"><span data-stu-id="5be20-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="5be20-270">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-270">The request will contain:</span></span>
        * <span data-ttu-id="5be20-271">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-271">the package source repository location</span></span>
    * <span data-ttu-id="5be20-272">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-272">A response will contain:</span></span>
        * <span data-ttu-id="5be20-273">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5be20-274">Индекс службы, если операция выполнена успешно</span><span class="sxs-lookup"><span data-stu-id="5be20-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="5be20-275">Подтверждение</span><span class="sxs-lookup"><span data-stu-id="5be20-275">Handshake</span></span>
     * <span data-ttu-id="5be20-276">Запросить направление: подключаемого модуля NuGet <> –</span><span class="sxs-lookup"><span data-stu-id="5be20-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="5be20-277">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-277">The request will contain:</span></span>
         * <span data-ttu-id="5be20-278">Текущая версия протокола подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="5be20-279">Минимальная поддерживаемая версия протокола подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="5be20-280">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-280">A response will contain:</span></span>
         * <span data-ttu-id="5be20-281">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="5be20-282">версия согласованный протокол, если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="5be20-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="5be20-283">Сбой приведет к завершению работы подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="5be20-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="5be20-284">Инициализация</span><span class="sxs-lookup"><span data-stu-id="5be20-284">Initialize</span></span>
     * <span data-ttu-id="5be20-285">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="5be20-286">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-286">The request will contain:</span></span>
         * <span data-ttu-id="5be20-287">версия средства клиента NuGet</span><span class="sxs-lookup"><span data-stu-id="5be20-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="5be20-288">NuGet средство эффективный язык клиента.</span><span class="sxs-lookup"><span data-stu-id="5be20-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="5be20-289">Это учитывает параметр ForceEnglishOutput, если используется.</span><span class="sxs-lookup"><span data-stu-id="5be20-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="5be20-290">по умолчанию время ожидания запроса, который заменяет значение по умолчанию протокол.</span><span class="sxs-lookup"><span data-stu-id="5be20-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="5be20-291">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-291">A response will contain:</span></span>
         * <span data-ttu-id="5be20-292">код ответа, указывающее результат операции.</span><span class="sxs-lookup"><span data-stu-id="5be20-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="5be20-293">Сбой приведет к завершению работы подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="5be20-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="5be20-294">Журнал</span><span class="sxs-lookup"><span data-stu-id="5be20-294">Log</span></span>
     * <span data-ttu-id="5be20-295">Запросить направление: подключаемый модуль "->" NuGet</span><span class="sxs-lookup"><span data-stu-id="5be20-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="5be20-296">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-296">The request will contain:</span></span>
         * <span data-ttu-id="5be20-297">уровень ведения журнала для запроса</span><span class="sxs-lookup"><span data-stu-id="5be20-297">the log level for the request</span></span>
         * <span data-ttu-id="5be20-298">в журнал сообщения</span><span class="sxs-lookup"><span data-stu-id="5be20-298">a message to log</span></span>
     * <span data-ttu-id="5be20-299">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-299">A response will contain:</span></span>
         * <span data-ttu-id="5be20-300">код ответа, указывающее результат операции.</span><span class="sxs-lookup"><span data-stu-id="5be20-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="5be20-301">Отслеживать завершения работы процесса NuGet</span><span class="sxs-lookup"><span data-stu-id="5be20-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="5be20-302">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="5be20-303">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-303">The request will contain:</span></span>
         * <span data-ttu-id="5be20-304">Идентификатор процесса NuGet</span><span class="sxs-lookup"><span data-stu-id="5be20-304">the NuGet process ID</span></span>
     * <span data-ttu-id="5be20-305">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-305">A response will contain:</span></span>
         * <span data-ttu-id="5be20-306">код ответа, указывающее результат операции.</span><span class="sxs-lookup"><span data-stu-id="5be20-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="5be20-307">Предварительная загрузка пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-307">Prefetch package</span></span>
     * <span data-ttu-id="5be20-308">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="5be20-309">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-309">The request will contain:</span></span>
         * <span data-ttu-id="5be20-310">ИД пакета и версии</span><span class="sxs-lookup"><span data-stu-id="5be20-310">the package ID and version</span></span>
         * <span data-ttu-id="5be20-311">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-311">the package source repository location</span></span>
     * <span data-ttu-id="5be20-312">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-312">A response will contain:</span></span>
         * <span data-ttu-id="5be20-313">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="5be20-314">Задание учетных данных</span><span class="sxs-lookup"><span data-stu-id="5be20-314">Set credentials</span></span>
     * <span data-ttu-id="5be20-315">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="5be20-316">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-316">The request will contain:</span></span>
         * <span data-ttu-id="5be20-317">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-317">the package source repository location</span></span>
         * <span data-ttu-id="5be20-318">последний username источника пакетов, если он доступен</span><span class="sxs-lookup"><span data-stu-id="5be20-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="5be20-319">Последний пароль источника пакетов, если он доступен</span><span class="sxs-lookup"><span data-stu-id="5be20-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="5be20-320">последние известные прокси-сервер имя пользователя, если он доступен</span><span class="sxs-lookup"><span data-stu-id="5be20-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="5be20-321">Последний пароль известных прокси-сервера, если он доступен</span><span class="sxs-lookup"><span data-stu-id="5be20-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="5be20-322">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-322">A response will contain:</span></span>
         * <span data-ttu-id="5be20-323">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="5be20-324">Уровень ведения журнала набора</span><span class="sxs-lookup"><span data-stu-id="5be20-324">Set log level</span></span>
     * <span data-ttu-id="5be20-325">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="5be20-326">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-326">The request will contain:</span></span>
         * <span data-ttu-id="5be20-327">уровень ведения журнала по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5be20-327">the default log level</span></span>
     * <span data-ttu-id="5be20-328">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-328">A response will contain:</span></span>
         * <span data-ttu-id="5be20-329">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="5be20-330">Версия протокола *2.0.0* сообщений</span><span class="sxs-lookup"><span data-stu-id="5be20-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="5be20-331">Получить операции утверждения</span><span class="sxs-lookup"><span data-stu-id="5be20-331">Get Operation Claims</span></span>

* <span data-ttu-id="5be20-332">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="5be20-333">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-333">The request will contain:</span></span>
        * <span data-ttu-id="5be20-334">index.json службы для источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="5be20-335">расположение репозитория источника пакета</span><span class="sxs-lookup"><span data-stu-id="5be20-335">the package source repository location</span></span>
    * <span data-ttu-id="5be20-336">Ответ будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-336">A response will contain:</span></span>
        * <span data-ttu-id="5be20-337">код ответа, указывающее результат операции</span><span class="sxs-lookup"><span data-stu-id="5be20-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="5be20-338">Перечислимый объект по поддерживаемым операциям, если операция выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="5be20-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="5be20-339">Если подключаемый модуль не поддерживает источник, подключаемый модуль должен возвращать пустой набор поддерживаемых операций.</span><span class="sxs-lookup"><span data-stu-id="5be20-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="5be20-340">Если источник индекса и пакета службы имеют значение null, подключаемый модуль можно ответить с помощью проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5be20-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="5be20-341">Получить учетные данные проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="5be20-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="5be20-342">Запросить направление: NuGet -> подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="5be20-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="5be20-343">Запрос будет содержать:</span><span class="sxs-lookup"><span data-stu-id="5be20-343">The request will contain:</span></span>
    * <span data-ttu-id="5be20-344">URI</span><span class="sxs-lookup"><span data-stu-id="5be20-344">Uri</span></span>
    * <span data-ttu-id="5be20-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="5be20-345">isRetry</span></span>
    * <span data-ttu-id="5be20-346">Неинтерактивная</span><span class="sxs-lookup"><span data-stu-id="5be20-346">NonInteractive</span></span>
    * <span data-ttu-id="5be20-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="5be20-347">CanShowDialog</span></span>
* <span data-ttu-id="5be20-348">Ответ будет содержать</span><span class="sxs-lookup"><span data-stu-id="5be20-348">A response will contain</span></span>
    * <span data-ttu-id="5be20-349">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="5be20-349">Username</span></span>
    * <span data-ttu-id="5be20-350">Пароль</span><span class="sxs-lookup"><span data-stu-id="5be20-350">Password</span></span>
    * <span data-ttu-id="5be20-351">Сообщение</span><span class="sxs-lookup"><span data-stu-id="5be20-351">Message</span></span>
    * <span data-ttu-id="5be20-352">Список типов проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="5be20-352">List of Auth Types</span></span>
    * <span data-ttu-id="5be20-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="5be20-353">MessageResponseCode</span></span>