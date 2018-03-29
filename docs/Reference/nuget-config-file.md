---
title: Справочник по файлу NuGet.Config | Документы Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Справочник по файлу NuGet.Config, включая разделы config, bindingRedirects, packageRestore, solution и packageSource.
keywords: файл NuGet.Config, справочник по настройке NuGet, параметры конфигурации NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e2a9d4f10ac6af4e5bc7386d4f78e18c2a5752c4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="8e72b-104">Справочник по NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="8e72b-104">NuGet.Config reference</span></span>

<span data-ttu-id="8e72b-105">Для управления работой NuGet используются параметры в различных файлах `NuGet.Config`, как описано в разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8e72b-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="8e72b-106">`NuGet.Config` — это XML-файл, содержащий узел `<configuration>` верхнего уровня, который, в свою очередь, содержит элементы разделов, описываемые в этой статье.</span><span class="sxs-lookup"><span data-stu-id="8e72b-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="8e72b-107">Каждый раздел содержит ноль или более элементов `<add>` с атрибутами `key` и `value`.</span><span class="sxs-lookup"><span data-stu-id="8e72b-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="8e72b-108">См. [пример файла конфигурации](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="8e72b-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="8e72b-109">В именах регистр символов не учитывается, а в качестве значений могут использоваться [переменные среды](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="8e72b-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="8e72b-110">Содержание раздела</span><span class="sxs-lookup"><span data-stu-id="8e72b-110">In this topic:</span></span>

- [<span data-ttu-id="8e72b-111">Раздел config</span><span class="sxs-lookup"><span data-stu-id="8e72b-111">config section</span></span>](#config-section)
- [<span data-ttu-id="8e72b-112">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="8e72b-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="8e72b-113">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="8e72b-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="8e72b-114">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="8e72b-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="8e72b-115">[Разделы источников пакета](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="8e72b-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="8e72b-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="8e72b-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="8e72b-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="8e72b-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="8e72b-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="8e72b-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="8e72b-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="8e72b-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="8e72b-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="8e72b-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="8e72b-121">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="8e72b-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="8e72b-122">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="8e72b-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="8e72b-123">Раздел config</span><span class="sxs-lookup"><span data-stu-id="8e72b-123">config section</span></span>

<span data-ttu-id="8e72b-124">Содержит различные параметры конфигурации, которые можно задавать с помощью [команды `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="8e72b-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="8e72b-125">`dependencyVersion` и `repositoryPath` применяются только к проектам с помощью `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8e72b-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="8e72b-126">`globalPackagesFolder` применяется только к проектам, используя формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="8e72b-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="8e72b-127">Ключ</span><span class="sxs-lookup"><span data-stu-id="8e72b-127">Key</span></span> | <span data-ttu-id="8e72b-128">Значение</span><span class="sxs-lookup"><span data-stu-id="8e72b-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8e72b-129">dependencyVersion (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="8e72b-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="8e72b-130">Значение `DependencyVersion` по умолчанию для установки, восстановления и обновления пакета, если параметр `-DependencyVersion` не указан напрямую.</span><span class="sxs-lookup"><span data-stu-id="8e72b-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="8e72b-131">Это значение также используется в пользовательском интерфейсе диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="8e72b-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="8e72b-132">Возможные значения: `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="8e72b-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="8e72b-133">параметр globalPackagesFolder (только с помощью PackageReference проекты)</span><span class="sxs-lookup"><span data-stu-id="8e72b-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="8e72b-134">Расположение глобальной папки пакетов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8e72b-134">The location of the default global packages folder.</span></span> <span data-ttu-id="8e72b-135">Значение по умолчанию — `%userprofile%\.nuget\packages` (Windows) или `~/.nuget/packages` (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="8e72b-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="8e72b-136">В файлах `Nuget.Config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="8e72b-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="8e72b-137">Этот параметр может переопределяться переменную среды NUGET_PACKAGES имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="8e72b-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="8e72b-138">repositoryPath (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="8e72b-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="8e72b-139">Расположение, в котором следует установить пакеты NuGet вместо папки `$(Solutiondir)/packages` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8e72b-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="8e72b-140">В файлах `Nuget.Config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="8e72b-140">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="8e72b-141">Этот параметр может переопределяться переменную среды NUGET_PACKAGES имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="8e72b-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="8e72b-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="8e72b-142">defaultPushSource</span></span> | <span data-ttu-id="8e72b-143">Определяет URL-адрес источника пакета или путь к нему, который следует использовать по умолчанию, если другие источники пакета для операции не обнаружены.</span><span class="sxs-lookup"><span data-stu-id="8e72b-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="8e72b-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="8e72b-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="8e72b-145">Параметры прокси-сервера, которые следует использовать при подключении к источникам пакета; значение `http_proxy` должно иметь формат `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="8e72b-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="8e72b-146">Пароли зашифровываются, и их нельзя добавить вручную.</span><span class="sxs-lookup"><span data-stu-id="8e72b-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="8e72b-147">Значение параметра `no_proxy` представляет собой разделенный запятыми список доменов, для которых производится обход прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="8e72b-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="8e72b-148">В качестве этих значений можно также использовать переменные среды http_proxy и no_proxy.</span><span class="sxs-lookup"><span data-stu-id="8e72b-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="8e72b-149">Дополнительные сведения см. в записи блога [Параметры прокси-сервера в NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="8e72b-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="8e72b-150">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8e72b-150">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="8e72b-151">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="8e72b-151">bindingRedirects section</span></span>

<span data-ttu-id="8e72b-152">Определяет то, производится ли в NuGet автоматическая переадресация привязок при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="8e72b-152">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="8e72b-153">Ключ</span><span class="sxs-lookup"><span data-stu-id="8e72b-153">Key</span></span> | <span data-ttu-id="8e72b-154">Значение</span><span class="sxs-lookup"><span data-stu-id="8e72b-154">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8e72b-155">skip</span><span class="sxs-lookup"><span data-stu-id="8e72b-155">skip</span></span> | <span data-ttu-id="8e72b-156">Логическое значение, указывающее, следует ли пропустить автоматическую переадресацию привязок.</span><span class="sxs-lookup"><span data-stu-id="8e72b-156">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="8e72b-157">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="8e72b-157">The default is false.</span></span> |

<span data-ttu-id="8e72b-158">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8e72b-158">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="8e72b-159">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="8e72b-159">packageRestore section</span></span>

<span data-ttu-id="8e72b-160">Управляет восстановлением пакета во время сборки.</span><span class="sxs-lookup"><span data-stu-id="8e72b-160">Controls package restore during builds.</span></span>

| <span data-ttu-id="8e72b-161">Ключ</span><span class="sxs-lookup"><span data-stu-id="8e72b-161">Key</span></span> | <span data-ttu-id="8e72b-162">Значение</span><span class="sxs-lookup"><span data-stu-id="8e72b-162">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8e72b-163">enabled</span><span class="sxs-lookup"><span data-stu-id="8e72b-163">enabled</span></span> | <span data-ttu-id="8e72b-164">Логическое значение, указывающее, может ли NuGet выполнять автоматическое восстановление.</span><span class="sxs-lookup"><span data-stu-id="8e72b-164">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="8e72b-165">Вы также можете задать переменную среды `EnableNuGetPackageRestore` со значением `True` вместо того, чтобы задавать этот параметр в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8e72b-165">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="8e72b-166">автоматическая</span><span class="sxs-lookup"><span data-stu-id="8e72b-166">automatic</span></span> | <span data-ttu-id="8e72b-167">Логическое значение, указывающее, должен ли диспетчер NuGet проверять отсутствие пакетов во время сборки.</span><span class="sxs-lookup"><span data-stu-id="8e72b-167">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="8e72b-168">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8e72b-168">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="8e72b-169">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="8e72b-169">solution section</span></span>

<span data-ttu-id="8e72b-170">Определяет то, включается ли папка `packages` решения в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="8e72b-170">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="8e72b-171">Этот раздел работает только в файлах `Nuget.Config` в папке решения.</span><span class="sxs-lookup"><span data-stu-id="8e72b-171">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="8e72b-172">Ключ</span><span class="sxs-lookup"><span data-stu-id="8e72b-172">Key</span></span> | <span data-ttu-id="8e72b-173">Значение</span><span class="sxs-lookup"><span data-stu-id="8e72b-173">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8e72b-174">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="8e72b-174">disableSourceControlIntegration</span></span> | <span data-ttu-id="8e72b-175">Логическое значение, указывающее, следует ли игнорировать папку пакетов при работе с системой управления версиями.</span><span class="sxs-lookup"><span data-stu-id="8e72b-175">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="8e72b-176">Значением по умолчанию является false.</span><span class="sxs-lookup"><span data-stu-id="8e72b-176">The default value is false.</span></span> |

<span data-ttu-id="8e72b-177">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8e72b-177">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="8e72b-178">Разделы источников пакета</span><span class="sxs-lookup"><span data-stu-id="8e72b-178">Package source sections</span></span>

<span data-ttu-id="8e72b-179">Параметры `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` и `disabledPackageSources` в совокупности определяют то, как NuGet работает с репозиториями пакетов во время операций установки, восстановления и обновления.</span><span class="sxs-lookup"><span data-stu-id="8e72b-179">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="8e72b-180">Как правило, для управления этими параметрами используется [команда `nuget sources`](../tools/cli-ref-sources.md), за исключением параметра `apikeys`, который настраивается с помощью [команды `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="8e72b-180">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="8e72b-181">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="8e72b-181">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="8e72b-182">packageSources</span><span class="sxs-lookup"><span data-stu-id="8e72b-182">packageSources</span></span>

<span data-ttu-id="8e72b-183">Выводит список всех известных источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="8e72b-183">Lists all known package sources.</span></span> <span data-ttu-id="8e72b-184">Во время операций восстановления и с любой проект в формате PackageReference, порядок учитывается.</span><span class="sxs-lookup"><span data-stu-id="8e72b-184">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="8e72b-185">NuGet нарушать порядок источников для установки и обновления с проектами с помощью `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8e72b-185">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="8e72b-186">Ключ</span><span class="sxs-lookup"><span data-stu-id="8e72b-186">Key</span></span> | <span data-ttu-id="8e72b-187">Значение</span><span class="sxs-lookup"><span data-stu-id="8e72b-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8e72b-188">(имя, назначаемое источнику пакета)</span><span class="sxs-lookup"><span data-stu-id="8e72b-188">(name to assign to the package source)</span></span> | <span data-ttu-id="8e72b-189">Путь к источнику пакета или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="8e72b-189">The path or URL of the package source.</span></span> |

<span data-ttu-id="8e72b-190">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8e72b-190">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="8e72b-191">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="8e72b-191">packageSourceCredentials</span></span>

<span data-ttu-id="8e72b-192">Содержит имена пользователей и пароли источников, которые, как правило, задаются с помощью параметров `-username` и `-password` команды `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="8e72b-192">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="8e72b-193">По умолчанию пароли зашифровываются, если также не указан параметр `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="8e72b-193">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="8e72b-194">Ключ</span><span class="sxs-lookup"><span data-stu-id="8e72b-194">Key</span></span> | <span data-ttu-id="8e72b-195">Значение</span><span class="sxs-lookup"><span data-stu-id="8e72b-195">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8e72b-196">username</span><span class="sxs-lookup"><span data-stu-id="8e72b-196">username</span></span> | <span data-ttu-id="8e72b-197">Имя пользователя источника в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="8e72b-197">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="8e72b-198">пароль</span><span class="sxs-lookup"><span data-stu-id="8e72b-198">password</span></span> | <span data-ttu-id="8e72b-199">Зашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="8e72b-199">The encrypted password for the source.</span></span> |
| <span data-ttu-id="8e72b-200">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="8e72b-200">cleartextpassword</span></span> | <span data-ttu-id="8e72b-201">Незашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="8e72b-201">The unencrypted password for the source.</span></span> |

<span data-ttu-id="8e72b-202">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="8e72b-202">**Example:**</span></span>

<span data-ttu-id="8e72b-203">В файле конфигурации элемент `<packageSourceCredentials>` содержит дочерние узлы для каждого применимого имени источника (пробелы в имени заменяются на `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="8e72b-203">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="8e72b-204">То есть для источников с именами Contoso и Test Source файл конфигурации содержит следующие значения при использовании зашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="8e72b-204">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="8e72b-205">При использовании незашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="8e72b-205">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="8e72b-206">apikeys</span><span class="sxs-lookup"><span data-stu-id="8e72b-206">apikeys</span></span>

<span data-ttu-id="8e72b-207">Содержит ключи для источников, которые используют проверку подлинности на основе ключей API. Эти ключи задаются с помощью [команды `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="8e72b-207">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="8e72b-208">Ключ</span><span class="sxs-lookup"><span data-stu-id="8e72b-208">Key</span></span> | <span data-ttu-id="8e72b-209">Значение</span><span class="sxs-lookup"><span data-stu-id="8e72b-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8e72b-210">(URL-адрес источника)</span><span class="sxs-lookup"><span data-stu-id="8e72b-210">(source URL)</span></span> | <span data-ttu-id="8e72b-211">Зашифрованный ключ API.</span><span class="sxs-lookup"><span data-stu-id="8e72b-211">The encrypted API key.</span></span> |

<span data-ttu-id="8e72b-212">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8e72b-212">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="8e72b-213">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="8e72b-213">disabledPackageSources</span></span>

<span data-ttu-id="8e72b-214">Определяет источники, отключенные в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="8e72b-214">Identified currently disabled sources.</span></span> <span data-ttu-id="8e72b-215">Значение может быть пустым.</span><span class="sxs-lookup"><span data-stu-id="8e72b-215">May be empty.</span></span>

| <span data-ttu-id="8e72b-216">Ключ</span><span class="sxs-lookup"><span data-stu-id="8e72b-216">Key</span></span> | <span data-ttu-id="8e72b-217">Значение</span><span class="sxs-lookup"><span data-stu-id="8e72b-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8e72b-218">(имя источника)</span><span class="sxs-lookup"><span data-stu-id="8e72b-218">(name of source)</span></span> | <span data-ttu-id="8e72b-219">Логическое значение, указывающее, отключен ли источник.</span><span class="sxs-lookup"><span data-stu-id="8e72b-219">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="8e72b-220">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="8e72b-220">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="8e72b-221">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="8e72b-221">activePackageSource</span></span>

<span data-ttu-id="8e72b-222">*(Только в версиях 2.x; в версиях 3.x и более поздних является нерекомендуемым)*</span><span class="sxs-lookup"><span data-stu-id="8e72b-222">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="8e72b-223">Определяет текущий активный источник или указывает совокупность всех источников.</span><span class="sxs-lookup"><span data-stu-id="8e72b-223">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="8e72b-224">Ключ</span><span class="sxs-lookup"><span data-stu-id="8e72b-224">Key</span></span> | <span data-ttu-id="8e72b-225">Значение</span><span class="sxs-lookup"><span data-stu-id="8e72b-225">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8e72b-226">(имя источника) или `All`</span><span class="sxs-lookup"><span data-stu-id="8e72b-226">(name of source) or `All`</span></span> | <span data-ttu-id="8e72b-227">Если ключ представляет имя источника, значением является путь к источнику или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="8e72b-227">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="8e72b-228">Если используется ключ `All`, требуется значение `(Aggregate source)`, объединяющее все источники пакетов, которые не отключены.</span><span class="sxs-lookup"><span data-stu-id="8e72b-228">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="8e72b-229">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8e72b-229">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="8e72b-230">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="8e72b-230">Using environment variables</span></span>

<span data-ttu-id="8e72b-231">В значениях `NuGet.Config` можно использовать переменные среды (в NuGet 3.4 и более поздних версиях) для применения параметров во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="8e72b-231">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="8e72b-232">Например, если переменная среды `HOME` в Windows имеет значение `c:\users\username`, значение параметра `%HOME%\NuGetRepository` в файле конфигурации разрешается в `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="8e72b-232">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="8e72b-233">Аналогичным образом, если переменная `HOME` в Mac или Linux имеет значение `/home/myStuff`, параметр `$HOME/NuGetRepository` в файле конфигурации разрешается в `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="8e72b-233">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="8e72b-234">Если переменная среды не найдена, NuGet использует буквальное значение из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8e72b-234">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="8e72b-235">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="8e72b-235">Example config file</span></span>

<span data-ttu-id="8e72b-236">Ниже приведен пример файла `NuGet.Config`, в котором демонстрируется ряд параметров.</span><span class="sxs-lookup"><span data-stu-id="8e72b-236">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>
</configuration>
```
