---
title: "Справочник по файлу NuGet.Config | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по файлу NuGet.Config, включая разделы config, bindingRedirects, packageRestore, solution и packageSource."
keywords: "файл NuGet.Config, справочник по настройке NuGet, параметры конфигурации NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a5be1ebcca0accafcdaf32f0b1b7ca66ec53425
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="8b98a-104">Справочник по NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="8b98a-104">NuGet.Config reference</span></span>

<span data-ttu-id="8b98a-105">Для управления работой NuGet используются параметры в различных файлах `NuGet.Config`, как описано в разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8b98a-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="8b98a-106">`NuGet.Config` — это XML-файл, содержащий узел `<configuration>` верхнего уровня, который, в свою очередь, содержит элементы разделов, описываемые в этой статье.</span><span class="sxs-lookup"><span data-stu-id="8b98a-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="8b98a-107">Каждый раздел содержит ноль или более элементов `<add>` с атрибутами `key` и `value`.</span><span class="sxs-lookup"><span data-stu-id="8b98a-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="8b98a-108">См. [пример файла конфигурации](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="8b98a-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="8b98a-109">В именах регистр символов не учитывается, а в качестве значений могут использоваться [переменные среды](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="8b98a-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="8b98a-110">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="8b98a-110">In this topic:</span></span>

- [<span data-ttu-id="8b98a-111">Раздел config</span><span class="sxs-lookup"><span data-stu-id="8b98a-111">config section</span></span>](#config-section)
- [<span data-ttu-id="8b98a-112">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="8b98a-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="8b98a-113">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="8b98a-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="8b98a-114">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="8b98a-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="8b98a-115">[Разделы источников пакета](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="8b98a-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="8b98a-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="8b98a-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="8b98a-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="8b98a-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="8b98a-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="8b98a-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="8b98a-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="8b98a-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="8b98a-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="8b98a-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="8b98a-121">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="8b98a-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="8b98a-122">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="8b98a-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="8b98a-123">Раздел config</span><span class="sxs-lookup"><span data-stu-id="8b98a-123">config section</span></span>

<span data-ttu-id="8b98a-124">Содержит различные параметры конфигурации, которые можно задавать с помощью [команды `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="8b98a-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="8b98a-125">Примечание. Параметры `dependencyVersion` и `repositoryPath` применяются только к проектам, в которых используется файл `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8b98a-125">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="8b98a-126">`globalPackagesFolder` применяется только к проектам, используя формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="8b98a-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="8b98a-127">Ключ</span><span class="sxs-lookup"><span data-stu-id="8b98a-127">Key</span></span> | <span data-ttu-id="8b98a-128">Значение</span><span class="sxs-lookup"><span data-stu-id="8b98a-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8b98a-129">dependencyVersion (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="8b98a-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="8b98a-130">Значение `DependencyVersion` по умолчанию для установки, восстановления и обновления пакета, если параметр `-DependencyVersion` не указан напрямую.</span><span class="sxs-lookup"><span data-stu-id="8b98a-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="8b98a-131">Это значение также используется в пользовательском интерфейсе диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="8b98a-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="8b98a-132">Возможные значения: `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="8b98a-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="8b98a-133">globalPackagesFolder (проекты, в которых не используется `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="8b98a-133">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="8b98a-134">Расположение глобальной папки пакетов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8b98a-134">The location of the default global packages folder.</span></span> <span data-ttu-id="8b98a-135">Значение по умолчанию — `%USERPROFILE%\.nuget\packages` (Windows) или `~/.nuget/packages` (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="8b98a-135">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="8b98a-136">В файлах `Nuget.Config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="8b98a-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="8b98a-137">repositoryPath (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="8b98a-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="8b98a-138">Расположение, в котором следует установить пакеты NuGet вместо папки `$(Solutiondir)/packages` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8b98a-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="8b98a-139">В файлах `Nuget.Config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="8b98a-139">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="8b98a-140">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="8b98a-140">defaultPushSource</span></span> | <span data-ttu-id="8b98a-141">Определяет URL-адрес источника пакета или путь к нему, который следует использовать по умолчанию, если другие источники пакета для операции не обнаружены.</span><span class="sxs-lookup"><span data-stu-id="8b98a-141">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="8b98a-142">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="8b98a-142">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="8b98a-143">Параметры прокси-сервера, которые следует использовать при подключении к источникам пакета; значение `http_proxy` должно иметь формат `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="8b98a-143">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="8b98a-144">Пароли зашифровываются, и их нельзя добавить вручную.</span><span class="sxs-lookup"><span data-stu-id="8b98a-144">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="8b98a-145">Значение параметра `no_proxy` представляет собой разделенный запятыми список доменов, для которых производится обход прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="8b98a-145">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="8b98a-146">В качестве этих значений можно также использовать переменные среды http_proxy и no_proxy.</span><span class="sxs-lookup"><span data-stu-id="8b98a-146">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="8b98a-147">Дополнительные сведения см. в записи блога [Параметры прокси-сервера в NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="8b98a-147">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="8b98a-148">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8b98a-148">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="8b98a-149">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="8b98a-149">bindingRedirects section</span></span>

<span data-ttu-id="8b98a-150">Определяет то, производится ли в NuGet автоматическая переадресация привязок при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="8b98a-150">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="8b98a-151">Ключ</span><span class="sxs-lookup"><span data-stu-id="8b98a-151">Key</span></span> | <span data-ttu-id="8b98a-152">Значение</span><span class="sxs-lookup"><span data-stu-id="8b98a-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8b98a-153">skip</span><span class="sxs-lookup"><span data-stu-id="8b98a-153">skip</span></span> | <span data-ttu-id="8b98a-154">Логическое значение, указывающее, следует ли пропустить автоматическую переадресацию привязок.</span><span class="sxs-lookup"><span data-stu-id="8b98a-154">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="8b98a-155">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="8b98a-155">The default is false.</span></span> |

<span data-ttu-id="8b98a-156">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8b98a-156">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="8b98a-157">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="8b98a-157">packageRestore section</span></span>

<span data-ttu-id="8b98a-158">Управляет восстановлением пакета во время сборки.</span><span class="sxs-lookup"><span data-stu-id="8b98a-158">Controls package restore during builds.</span></span>

| <span data-ttu-id="8b98a-159">Ключ</span><span class="sxs-lookup"><span data-stu-id="8b98a-159">Key</span></span> | <span data-ttu-id="8b98a-160">Значение</span><span class="sxs-lookup"><span data-stu-id="8b98a-160">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8b98a-161">enabled</span><span class="sxs-lookup"><span data-stu-id="8b98a-161">enabled</span></span> | <span data-ttu-id="8b98a-162">Логическое значение, указывающее, может ли NuGet выполнять автоматическое восстановление.</span><span class="sxs-lookup"><span data-stu-id="8b98a-162">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="8b98a-163">Вы также можете задать переменную среды `EnableNuGetPackageRestore` со значением `True` вместо того, чтобы задавать этот параметр в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8b98a-163">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="8b98a-164">автоматическая</span><span class="sxs-lookup"><span data-stu-id="8b98a-164">automatic</span></span> | <span data-ttu-id="8b98a-165">Логическое значение, указывающее, должен ли диспетчер NuGet проверять отсутствие пакетов во время сборки.</span><span class="sxs-lookup"><span data-stu-id="8b98a-165">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="8b98a-166">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8b98a-166">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="8b98a-167">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="8b98a-167">solution section</span></span>

<span data-ttu-id="8b98a-168">Определяет то, включается ли папка `packages` решения в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="8b98a-168">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="8b98a-169">Этот раздел работает только в файлах `Nuget.Config` в папке решения.</span><span class="sxs-lookup"><span data-stu-id="8b98a-169">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="8b98a-170">Ключ</span><span class="sxs-lookup"><span data-stu-id="8b98a-170">Key</span></span> | <span data-ttu-id="8b98a-171">Значение</span><span class="sxs-lookup"><span data-stu-id="8b98a-171">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8b98a-172">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="8b98a-172">disableSourceControlIntegration</span></span> | <span data-ttu-id="8b98a-173">Логическое значение, указывающее, следует ли игнорировать папку пакетов при работе с системой управления версиями.</span><span class="sxs-lookup"><span data-stu-id="8b98a-173">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="8b98a-174">Значением по умолчанию является false.</span><span class="sxs-lookup"><span data-stu-id="8b98a-174">The default value is false.</span></span> |

<span data-ttu-id="8b98a-175">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8b98a-175">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="8b98a-176">Разделы источников пакета</span><span class="sxs-lookup"><span data-stu-id="8b98a-176">Package source sections</span></span>

<span data-ttu-id="8b98a-177">Параметры `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` и `disabledPackageSources` в совокупности определяют то, как NuGet работает с репозиториями пакетов во время операций установки, восстановления и обновления.</span><span class="sxs-lookup"><span data-stu-id="8b98a-177">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="8b98a-178">Как правило, для управления этими параметрами используется [команда `nuget sources`](../tools/cli-ref-sources.md), за исключением параметра `apikeys`, который настраивается с помощью [команды `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="8b98a-178">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="8b98a-179">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="8b98a-179">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="8b98a-180">packageSources</span><span class="sxs-lookup"><span data-stu-id="8b98a-180">packageSources</span></span>

<span data-ttu-id="8b98a-181">Выводит список всех известных источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="8b98a-181">Lists all known package sources.</span></span> <span data-ttu-id="8b98a-182">Во время операций восстановления и с любой проект в формате PackageReference, порядок учитывается.</span><span class="sxs-lookup"><span data-stu-id="8b98a-182">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="8b98a-183">NuGet нарушать порядок источников для установки и обновления с проектами с помощью `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8b98a-183">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="8b98a-184">Ключ</span><span class="sxs-lookup"><span data-stu-id="8b98a-184">Key</span></span> | <span data-ttu-id="8b98a-185">Значение</span><span class="sxs-lookup"><span data-stu-id="8b98a-185">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8b98a-186">(имя, назначаемое источнику пакета)</span><span class="sxs-lookup"><span data-stu-id="8b98a-186">(name to assign to the package source)</span></span> | <span data-ttu-id="8b98a-187">Путь к источнику пакета или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="8b98a-187">The path or URL of the package source.</span></span> |

<span data-ttu-id="8b98a-188">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8b98a-188">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="8b98a-189">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="8b98a-189">packageSourceCredentials</span></span>

<span data-ttu-id="8b98a-190">Содержит имена пользователей и пароли источников, которые, как правило, задаются с помощью параметров `-username` и `-password` команды `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="8b98a-190">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="8b98a-191">По умолчанию пароли зашифровываются, если также не указан параметр `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="8b98a-191">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="8b98a-192">Ключ</span><span class="sxs-lookup"><span data-stu-id="8b98a-192">Key</span></span> | <span data-ttu-id="8b98a-193">Значение</span><span class="sxs-lookup"><span data-stu-id="8b98a-193">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8b98a-194">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="8b98a-194">username</span></span> | <span data-ttu-id="8b98a-195">Имя пользователя источника в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="8b98a-195">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="8b98a-196">пароль</span><span class="sxs-lookup"><span data-stu-id="8b98a-196">password</span></span> | <span data-ttu-id="8b98a-197">Зашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="8b98a-197">The encrypted password for the source.</span></span> |
| <span data-ttu-id="8b98a-198">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="8b98a-198">cleartextpassword</span></span> | <span data-ttu-id="8b98a-199">Незашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="8b98a-199">The unencrypted password for the source.</span></span> |

<span data-ttu-id="8b98a-200">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="8b98a-200">**Example:**</span></span>

<span data-ttu-id="8b98a-201">В файле конфигурации элемент `<packageSourceCredentials>` содержит дочерние узлы для каждого применимого имени источника (пробелы в имени заменяются на `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="8b98a-201">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="8b98a-202">То есть для источников с именами Contoso и Test Source файл конфигурации содержит следующие значения при использовании зашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="8b98a-202">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="8b98a-203">При использовании незашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="8b98a-203">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="8b98a-204">apikeys</span><span class="sxs-lookup"><span data-stu-id="8b98a-204">apikeys</span></span>

<span data-ttu-id="8b98a-205">Содержит ключи для источников, которые используют проверку подлинности на основе ключей API. Эти ключи задаются с помощью [команды `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="8b98a-205">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="8b98a-206">Ключ</span><span class="sxs-lookup"><span data-stu-id="8b98a-206">Key</span></span> | <span data-ttu-id="8b98a-207">Значение</span><span class="sxs-lookup"><span data-stu-id="8b98a-207">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8b98a-208">(URL-адрес источника)</span><span class="sxs-lookup"><span data-stu-id="8b98a-208">(source URL)</span></span> | <span data-ttu-id="8b98a-209">Зашифрованный ключ API.</span><span class="sxs-lookup"><span data-stu-id="8b98a-209">The encrypted API key.</span></span> |

<span data-ttu-id="8b98a-210">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8b98a-210">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="8b98a-211">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="8b98a-211">disabledPackageSources</span></span>

<span data-ttu-id="8b98a-212">Определяет источники, отключенные в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="8b98a-212">Identified currently disabled sources.</span></span> <span data-ttu-id="8b98a-213">Значение может быть пустым.</span><span class="sxs-lookup"><span data-stu-id="8b98a-213">May be empty.</span></span>

| <span data-ttu-id="8b98a-214">Ключ</span><span class="sxs-lookup"><span data-stu-id="8b98a-214">Key</span></span> | <span data-ttu-id="8b98a-215">Значение</span><span class="sxs-lookup"><span data-stu-id="8b98a-215">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8b98a-216">(имя источника)</span><span class="sxs-lookup"><span data-stu-id="8b98a-216">(name of source)</span></span> | <span data-ttu-id="8b98a-217">Логическое значение, указывающее, отключен ли источник.</span><span class="sxs-lookup"><span data-stu-id="8b98a-217">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="8b98a-218">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="8b98a-218">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="8b98a-219">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="8b98a-219">activePackageSource</span></span>

<span data-ttu-id="8b98a-220">*(Только в версиях 2.x; в версиях 3.x и более поздних является нерекомендуемым)*</span><span class="sxs-lookup"><span data-stu-id="8b98a-220">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="8b98a-221">Определяет текущий активный источник или указывает совокупность всех источников.</span><span class="sxs-lookup"><span data-stu-id="8b98a-221">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="8b98a-222">Ключ</span><span class="sxs-lookup"><span data-stu-id="8b98a-222">Key</span></span> | <span data-ttu-id="8b98a-223">Значение</span><span class="sxs-lookup"><span data-stu-id="8b98a-223">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8b98a-224">(имя источника) или `All`</span><span class="sxs-lookup"><span data-stu-id="8b98a-224">(name of source) or `All`</span></span> | <span data-ttu-id="8b98a-225">Если ключ представляет имя источника, значением является путь к источнику или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="8b98a-225">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="8b98a-226">Если используется ключ `All`, требуется значение `(Aggregate source)`, объединяющее все источники пакетов, которые не отключены.</span><span class="sxs-lookup"><span data-stu-id="8b98a-226">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="8b98a-227">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="8b98a-227">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="8b98a-228">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="8b98a-228">Using environment variables</span></span>

<span data-ttu-id="8b98a-229">В значениях `NuGet.Config` можно использовать переменные среды (в NuGet 3.4 и более поздних версиях) для применения параметров во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="8b98a-229">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="8b98a-230">Например, если переменная среды `HOME` в Windows имеет значение `c:\users\username`, значение параметра `%HOME%\NuGetRepository` в файле конфигурации разрешается в `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="8b98a-230">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="8b98a-231">Аналогичным образом, если переменная `HOME` в Mac или Linux имеет значение `/home/myStuff`, параметр `$HOME/NuGetRepository` в файле конфигурации разрешается в `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="8b98a-231">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="8b98a-232">Если переменная среды не найдена, NuGet использует буквальное значение из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8b98a-232">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="8b98a-233">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="8b98a-233">Example config file</span></span>

<span data-ttu-id="8b98a-234">Ниже приведен пример файла `NuGet.Config`, в котором демонстрируется ряд параметров.</span><span class="sxs-lookup"><span data-stu-id="8b98a-234">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
