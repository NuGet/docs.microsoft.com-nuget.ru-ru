---
title: "Справочник по файлу NuGet.Config | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: fbf31530-3bf4-478c-b26c-c2b24dd3406d
description: "Справочник по файлу NuGet.Config, включая разделы config, bindingRedirects, packageRestore, solution и packageSource."
keywords: "файл NuGet.Config, справочник по настройке NuGet, параметры конфигурации NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 830c622f622b894a228b18dfdb3a790bccfde8a3
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="c8309-104">Справочник по NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="c8309-104">NuGet.Config reference</span></span>

<span data-ttu-id="c8309-105">Для управления работой NuGet используются параметры в различных файлах `NuGet.Config`, как описано в разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c8309-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="c8309-106">`NuGet.Config` — это XML-файл, содержащий узел `<configuration>` верхнего уровня, который, в свою очередь, содержит элементы разделов, описываемые в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c8309-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="c8309-107">Каждый раздел содержит ноль или более элементов `<add>` с атрибутами `key` и `value`.</span><span class="sxs-lookup"><span data-stu-id="c8309-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="c8309-108">См. [пример файла конфигурации](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="c8309-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="c8309-109">В именах регистр символов не учитывается, а в качестве значений могут использоваться [переменные среды](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="c8309-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="c8309-110">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="c8309-110">In this topic:</span></span>

- [<span data-ttu-id="c8309-111">Раздел config</span><span class="sxs-lookup"><span data-stu-id="c8309-111">config section</span></span>](#config-section)
- [<span data-ttu-id="c8309-112">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="c8309-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="c8309-113">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="c8309-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="c8309-114">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="c8309-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="c8309-115">[Разделы источников пакетов](#package-source-sections): -[packageSources](#packagesources)</span><span class="sxs-lookup"><span data-stu-id="c8309-115">[Package source sections](#package-source-sections): -[packageSources](#packagesources)</span></span>
  - [<span data-ttu-id="c8309-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="c8309-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="c8309-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="c8309-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="c8309-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="c8309-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="c8309-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="c8309-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="c8309-120">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="c8309-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="c8309-121">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="c8309-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="c8309-122">Раздел config</span><span class="sxs-lookup"><span data-stu-id="c8309-122">config section</span></span>

<span data-ttu-id="c8309-123">Содержит различные параметры конфигурации, которые можно задавать с помощью [команды `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="c8309-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="c8309-124">Примечание. Параметры `dependencyVersion` и `repositoryPath` применяются только к проектам, в которых используется файл `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="c8309-124">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="c8309-125">Параметр `globalPackagesFolder` применяется только к проектам, в которых используются форматы `project.json` и PackageReference.</span><span class="sxs-lookup"><span data-stu-id="c8309-125">`globalPackagesFolder` applies only to projects using `project.json` and PackageReference formats.</span></span>

| <span data-ttu-id="c8309-126">Ключ</span><span class="sxs-lookup"><span data-stu-id="c8309-126">Key</span></span> | <span data-ttu-id="c8309-127">Значение</span><span class="sxs-lookup"><span data-stu-id="c8309-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c8309-128">dependencyVersion (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="c8309-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="c8309-129">Значение `DependencyVersion` по умолчанию для установки, восстановления и обновления пакета, если параметр `-DependencyVersion` не указан напрямую.</span><span class="sxs-lookup"><span data-stu-id="c8309-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="c8309-130">Это значение также используется в пользовательском интерфейсе диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="c8309-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="c8309-131">Возможные значения: `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="c8309-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="c8309-132">globalPackagesFolder (проекты, в которых не используется `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="c8309-132">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="c8309-133">Расположение глобальной папки пакетов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c8309-133">The location of the default global packages folder.</span></span> <span data-ttu-id="c8309-134">Значение по умолчанию — `%USERPROFILE%\.nuget\packages` (Windows) или `~/.nuget/packages` (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="c8309-134">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="c8309-135">В файлах `Nuget.Config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="c8309-135">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="c8309-136">repositoryPath (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="c8309-136">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="c8309-137">Расположение, в котором следует установить пакеты NuGet вместо папки `$(Solutiondir)/packages` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c8309-137">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="c8309-138">В файлах `Nuget.Config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="c8309-138">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="c8309-139">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="c8309-139">defaultPushSource</span></span> | <span data-ttu-id="c8309-140">Определяет URL-адрес источника пакета или путь к нему, который следует использовать по умолчанию, если другие источники пакета для операции не обнаружены.</span><span class="sxs-lookup"><span data-stu-id="c8309-140">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="c8309-141">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="c8309-141">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="c8309-142">Параметры прокси-сервера, которые следует использовать при подключении к источникам пакета; значение `http_proxy` должно иметь формат `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="c8309-142">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="c8309-143">Пароли зашифровываются, и их нельзя добавить вручную.</span><span class="sxs-lookup"><span data-stu-id="c8309-143">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="c8309-144">Значение параметра `no_proxy` представляет собой разделенный запятыми список доменов, для которых производится обход прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c8309-144">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="c8309-145">В качестве этих значений можно также использовать переменные среды http_proxy и no_proxy.</span><span class="sxs-lookup"><span data-stu-id="c8309-145">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="c8309-146">Дополнительные сведения см. в записи блога [Параметры прокси-сервера в NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="c8309-146">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="c8309-147">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="c8309-147">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="c8309-148">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="c8309-148">bindingRedirects section</span></span>

<span data-ttu-id="c8309-149">Определяет то, производится ли в NuGet автоматическая переадресация привязок при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="c8309-149">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="c8309-150">Ключ</span><span class="sxs-lookup"><span data-stu-id="c8309-150">Key</span></span> | <span data-ttu-id="c8309-151">Значение</span><span class="sxs-lookup"><span data-stu-id="c8309-151">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c8309-152">skip</span><span class="sxs-lookup"><span data-stu-id="c8309-152">skip</span></span> | <span data-ttu-id="c8309-153">Логическое значение, указывающее, следует ли пропустить автоматическую переадресацию привязок.</span><span class="sxs-lookup"><span data-stu-id="c8309-153">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="c8309-154">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="c8309-154">The default is false.</span></span> |

<span data-ttu-id="c8309-155">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="c8309-155">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="c8309-156">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="c8309-156">packageRestore section</span></span>

<span data-ttu-id="c8309-157">*Игнорируется в версии 2.7 и более поздних*</span><span class="sxs-lookup"><span data-stu-id="c8309-157">*Ignored in 2.7+*</span></span>

<span data-ttu-id="c8309-158">Управляет восстановлением пакета во время сборки.</span><span class="sxs-lookup"><span data-stu-id="c8309-158">Controls package restore during builds.</span></span>

| <span data-ttu-id="c8309-159">Ключ</span><span class="sxs-lookup"><span data-stu-id="c8309-159">Key</span></span> | <span data-ttu-id="c8309-160">Значение</span><span class="sxs-lookup"><span data-stu-id="c8309-160">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c8309-161">enabled</span><span class="sxs-lookup"><span data-stu-id="c8309-161">enabled</span></span> | <span data-ttu-id="c8309-162">Логическое значение, указывающее, может ли NuGet выполнять автоматическое восстановление.</span><span class="sxs-lookup"><span data-stu-id="c8309-162">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="c8309-163">Вы также можете задать переменную среды `EnableNuGetPackageRestore` со значением `True` вместо того, чтобы задавать этот параметр в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c8309-163">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="c8309-164">автоматическая</span><span class="sxs-lookup"><span data-stu-id="c8309-164">automatic</span></span> | <span data-ttu-id="c8309-165">Логическое значение, указывающее, должен ли диспетчер NuGet проверять отсутствие пакетов во время сборки.</span><span class="sxs-lookup"><span data-stu-id="c8309-165">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="c8309-166">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="c8309-166">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="c8309-167">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="c8309-167">solution section</span></span>

<span data-ttu-id="c8309-168">Определяет то, включается ли папка `packages` решения в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="c8309-168">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="c8309-169">Этот раздел работает только в файлах `Nuget.Config` в папке решения.</span><span class="sxs-lookup"><span data-stu-id="c8309-169">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="c8309-170">Ключ</span><span class="sxs-lookup"><span data-stu-id="c8309-170">Key</span></span> | <span data-ttu-id="c8309-171">Значение</span><span class="sxs-lookup"><span data-stu-id="c8309-171">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c8309-172">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="c8309-172">disableSourceControlIntegration</span></span> | <span data-ttu-id="c8309-173">Логическое значение, указывающее, следует ли игнорировать папку пакетов при работе с системой управления версиями.</span><span class="sxs-lookup"><span data-stu-id="c8309-173">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="c8309-174">Значением по умолчанию является false.</span><span class="sxs-lookup"><span data-stu-id="c8309-174">The default value is false.</span></span> |

<span data-ttu-id="c8309-175">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="c8309-175">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="c8309-176">Разделы источников пакета</span><span class="sxs-lookup"><span data-stu-id="c8309-176">Package source sections</span></span>

<span data-ttu-id="c8309-177">Параметры `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` и `disabledPackageSources` в совокупности определяют то, как NuGet работает с репозиториями пакетов во время операций установки, восстановления и обновления.</span><span class="sxs-lookup"><span data-stu-id="c8309-177">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="c8309-178">Как правило, для управления этими параметрами используется [команда `nuget sources`](../tools/cli-ref-sources.md), за исключением параметра `apikeys`, который настраивается с помощью [команды `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="c8309-178">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="c8309-179">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="c8309-179">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="c8309-180">packageSources</span><span class="sxs-lookup"><span data-stu-id="c8309-180">packageSources</span></span>

<span data-ttu-id="c8309-181">Выводит список всех известных источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="c8309-181">Lists all known package sources.</span></span>

| <span data-ttu-id="c8309-182">Ключ</span><span class="sxs-lookup"><span data-stu-id="c8309-182">Key</span></span> | <span data-ttu-id="c8309-183">Значение</span><span class="sxs-lookup"><span data-stu-id="c8309-183">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c8309-184">(имя, назначаемое источнику пакета)</span><span class="sxs-lookup"><span data-stu-id="c8309-184">(name to assign to the package source)</span></span> | <span data-ttu-id="c8309-185">Путь к источнику пакета или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="c8309-185">The path or URL of the package source.</span></span> |

<span data-ttu-id="c8309-186">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="c8309-186">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="c8309-187">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="c8309-187">packageSourceCredentials</span></span>

<span data-ttu-id="c8309-188">Содержит имена пользователей и пароли источников, которые, как правило, задаются с помощью параметров `-username` и `-password` команды `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="c8309-188">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="c8309-189">По умолчанию пароли зашифровываются, если также не указан параметр `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="c8309-189">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="c8309-190">Ключ</span><span class="sxs-lookup"><span data-stu-id="c8309-190">Key</span></span> | <span data-ttu-id="c8309-191">Значение</span><span class="sxs-lookup"><span data-stu-id="c8309-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c8309-192">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="c8309-192">username</span></span> | <span data-ttu-id="c8309-193">Имя пользователя источника в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="c8309-193">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="c8309-194">пароль</span><span class="sxs-lookup"><span data-stu-id="c8309-194">password</span></span> | <span data-ttu-id="c8309-195">Зашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="c8309-195">The encrypted password for the source.</span></span> |
| <span data-ttu-id="c8309-196">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="c8309-196">cleartextpassword</span></span> | <span data-ttu-id="c8309-197">Незашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="c8309-197">The unencrypted password for the source.</span></span> |

<span data-ttu-id="c8309-198">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="c8309-198">**Example:**</span></span>

<span data-ttu-id="c8309-199">В файле конфигурации элемент `<packageSourceCredentials>` содержит дочерние узлы для каждого применимого имени источника (пробелы в имени заменяются на `_x0020+`).</span><span class="sxs-lookup"><span data-stu-id="c8309-199">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="c8309-200">То есть для источников с именами Contoso и Test Source файл конфигурации содержит следующие значения при использовании зашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="c8309-200">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="c8309-201">При использовании незашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="c8309-201">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="c8309-202">apikeys</span><span class="sxs-lookup"><span data-stu-id="c8309-202">apikeys</span></span>

<span data-ttu-id="c8309-203">Содержит ключи для источников, которые используют проверку подлинности на основе ключей API. Эти ключи задаются с помощью [команды `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="c8309-203">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="c8309-204">Ключ</span><span class="sxs-lookup"><span data-stu-id="c8309-204">Key</span></span> | <span data-ttu-id="c8309-205">Значение</span><span class="sxs-lookup"><span data-stu-id="c8309-205">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c8309-206">(URL-адрес источника)</span><span class="sxs-lookup"><span data-stu-id="c8309-206">(source URL)</span></span> | <span data-ttu-id="c8309-207">Зашифрованный ключ API.</span><span class="sxs-lookup"><span data-stu-id="c8309-207">The encrypted API key.</span></span> |

<span data-ttu-id="c8309-208">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="c8309-208">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="c8309-209">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="c8309-209">disabledPackageSources</span></span>

<span data-ttu-id="c8309-210">Определяет источники, отключенные в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="c8309-210">Identified currently disabled sources.</span></span> <span data-ttu-id="c8309-211">Значение может быть пустым.</span><span class="sxs-lookup"><span data-stu-id="c8309-211">May be empty.</span></span>

| <span data-ttu-id="c8309-212">Ключ</span><span class="sxs-lookup"><span data-stu-id="c8309-212">Key</span></span> | <span data-ttu-id="c8309-213">Значение</span><span class="sxs-lookup"><span data-stu-id="c8309-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c8309-214">(имя источника)</span><span class="sxs-lookup"><span data-stu-id="c8309-214">(name of source)</span></span> | <span data-ttu-id="c8309-215">Логическое значение, указывающее, отключен ли источник.</span><span class="sxs-lookup"><span data-stu-id="c8309-215">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="c8309-216">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="c8309-216">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="c8309-217">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="c8309-217">activePackageSource</span></span>

<span data-ttu-id="c8309-218">*(Только в версиях 2.x; в версиях 3.x и более поздних является нерекомендуемым)*</span><span class="sxs-lookup"><span data-stu-id="c8309-218">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="c8309-219">Определяет текущий активный источник или указывает совокупность всех источников.</span><span class="sxs-lookup"><span data-stu-id="c8309-219">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="c8309-220">Ключ</span><span class="sxs-lookup"><span data-stu-id="c8309-220">Key</span></span> | <span data-ttu-id="c8309-221">Значение</span><span class="sxs-lookup"><span data-stu-id="c8309-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c8309-222">(имя источника) или `All`</span><span class="sxs-lookup"><span data-stu-id="c8309-222">(name of source) or `All`</span></span> | <span data-ttu-id="c8309-223">Если ключ представляет имя источника, значением является путь к источнику или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="c8309-223">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="c8309-224">Если используется ключ `All`, требуется значение `(Aggregate source)`, объединяющее все источники пакетов, которые не отключены.</span><span class="sxs-lookup"><span data-stu-id="c8309-224">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="c8309-225">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="c8309-225">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="c8309-226">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="c8309-226">Using environment variables</span></span>

<span data-ttu-id="c8309-227">В значениях `NuGet.Config` можно использовать переменные среды (в NuGet 3.4 и более поздних версиях) для применения параметров во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c8309-227">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="c8309-228">Например, если переменная среды `HOME` в Windows имеет значение `c:\users\username`, значение параметра `%HOME%\NuGetRepository` в файле конфигурации разрешается в `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="c8309-228">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="c8309-229">Аналогичным образом, если переменная `HOME` в Mac или Linux имеет значение `/home/myStuff`, параметр `$HOME/NuGetRepository` в файле конфигурации разрешается в `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="c8309-229">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="c8309-230">Если переменная среды не найдена, NuGet использует буквальное значение из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c8309-230">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="c8309-231">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="c8309-231">Example config file</span></span>

<span data-ttu-id="c8309-232">Ниже приведен пример файла `NuGet.Config`, в котором демонстрируется ряд параметров.</span><span class="sxs-lookup"><span data-stu-id="c8309-232">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
