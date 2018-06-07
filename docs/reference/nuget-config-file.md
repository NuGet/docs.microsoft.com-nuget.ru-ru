---
title: Ссылка на файл NuGet.config
description: Справочник по файлу NuGet.Config, включая разделы config, bindingRedirects, packageRestore, solution и packageSource.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 3d6741b2d724b967e76ba65547e84adcd461a521
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818405"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="75cf5-103">Справочник по NuGet.config</span><span class="sxs-lookup"><span data-stu-id="75cf5-103">nuget.config reference</span></span>

<span data-ttu-id="75cf5-104">Для управления работой NuGet используются параметры в различных файлах `NuGet.Config`, как описано в разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="75cf5-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="75cf5-105">`nuget.config` — это XML-файл, содержащий узел `<configuration>` верхнего уровня, который, в свою очередь, содержит элементы разделов, описываемые в этой статье.</span><span class="sxs-lookup"><span data-stu-id="75cf5-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="75cf5-106">Каждый раздел содержит ноль или более элементов `<add>` с атрибутами `key` и `value`.</span><span class="sxs-lookup"><span data-stu-id="75cf5-106">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="75cf5-107">См. [пример файла конфигурации](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="75cf5-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="75cf5-108">В именах регистр символов не учитывается, а в качестве значений могут использоваться [переменные среды](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="75cf5-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="75cf5-109">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="75cf5-109">In this topic:</span></span>

- [<span data-ttu-id="75cf5-110">Раздел config</span><span class="sxs-lookup"><span data-stu-id="75cf5-110">config section</span></span>](#config-section)
- [<span data-ttu-id="75cf5-111">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="75cf5-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="75cf5-112">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="75cf5-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="75cf5-113">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="75cf5-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="75cf5-114">[Разделы источников пакета](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="75cf5-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="75cf5-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="75cf5-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="75cf5-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="75cf5-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="75cf5-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="75cf5-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="75cf5-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="75cf5-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="75cf5-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="75cf5-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="75cf5-120">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="75cf5-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="75cf5-121">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="75cf5-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="75cf5-122">Раздел config</span><span class="sxs-lookup"><span data-stu-id="75cf5-122">config section</span></span>

<span data-ttu-id="75cf5-123">Содержит различные параметры конфигурации, которые можно задавать с помощью [команды `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="75cf5-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="75cf5-124">`dependencyVersion` и `repositoryPath` применяются только к проектам с помощью `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="75cf5-124">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="75cf5-125">`globalPackagesFolder` применяется только к проектам, используя формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="75cf5-125">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="75cf5-126">Ключ</span><span class="sxs-lookup"><span data-stu-id="75cf5-126">Key</span></span> | <span data-ttu-id="75cf5-127">Значение</span><span class="sxs-lookup"><span data-stu-id="75cf5-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="75cf5-128">dependencyVersion (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="75cf5-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="75cf5-129">Значение `DependencyVersion` по умолчанию для установки, восстановления и обновления пакета, если параметр `-DependencyVersion` не указан напрямую.</span><span class="sxs-lookup"><span data-stu-id="75cf5-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="75cf5-130">Это значение также используется в пользовательском интерфейсе диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="75cf5-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="75cf5-131">Возможные значения: `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="75cf5-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="75cf5-132">параметр globalPackagesFolder (только с помощью PackageReference проекты)</span><span class="sxs-lookup"><span data-stu-id="75cf5-132">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="75cf5-133">Расположение глобальной папки пакетов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="75cf5-133">The location of the default global packages folder.</span></span> <span data-ttu-id="75cf5-134">Значение по умолчанию — `%userprofile%\.nuget\packages` (Windows) или `~/.nuget/packages` (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="75cf5-134">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="75cf5-135">В файлах `nuget.config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="75cf5-135">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="75cf5-136">Этот параметр может переопределяться переменную среды NUGET_PACKAGES имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="75cf5-136">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="75cf5-137">repositoryPath (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="75cf5-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="75cf5-138">Расположение, в котором следует установить пакеты NuGet вместо папки `$(Solutiondir)/packages` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="75cf5-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="75cf5-139">В файлах `nuget.config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="75cf5-139">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="75cf5-140">Этот параметр может переопределяться переменную среды NUGET_PACKAGES имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="75cf5-140">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="75cf5-141">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="75cf5-141">defaultPushSource</span></span> | <span data-ttu-id="75cf5-142">Определяет URL-адрес источника пакета или путь к нему, который следует использовать по умолчанию, если другие источники пакета для операции не обнаружены.</span><span class="sxs-lookup"><span data-stu-id="75cf5-142">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="75cf5-143">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="75cf5-143">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="75cf5-144">Параметры прокси-сервера, которые следует использовать при подключении к источникам пакета; значение `http_proxy` должно иметь формат `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="75cf5-144">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="75cf5-145">Пароли зашифровываются, и их нельзя добавить вручную.</span><span class="sxs-lookup"><span data-stu-id="75cf5-145">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="75cf5-146">Значение параметра `no_proxy` представляет собой разделенный запятыми список доменов, для которых производится обход прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="75cf5-146">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="75cf5-147">В качестве этих значений можно также использовать переменные среды http_proxy и no_proxy.</span><span class="sxs-lookup"><span data-stu-id="75cf5-147">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="75cf5-148">Дополнительные сведения см. в записи блога [Параметры прокси-сервера в NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="75cf5-148">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="75cf5-149">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="75cf5-149">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="75cf5-150">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="75cf5-150">bindingRedirects section</span></span>

<span data-ttu-id="75cf5-151">Определяет то, производится ли в NuGet автоматическая переадресация привязок при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="75cf5-151">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="75cf5-152">Ключ</span><span class="sxs-lookup"><span data-stu-id="75cf5-152">Key</span></span> | <span data-ttu-id="75cf5-153">Значение</span><span class="sxs-lookup"><span data-stu-id="75cf5-153">Value</span></span> |
| --- | --- |
| <span data-ttu-id="75cf5-154">skip</span><span class="sxs-lookup"><span data-stu-id="75cf5-154">skip</span></span> | <span data-ttu-id="75cf5-155">Логическое значение, указывающее, следует ли пропустить автоматическую переадресацию привязок.</span><span class="sxs-lookup"><span data-stu-id="75cf5-155">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="75cf5-156">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="75cf5-156">The default is false.</span></span> |

<span data-ttu-id="75cf5-157">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="75cf5-157">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="75cf5-158">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="75cf5-158">packageRestore section</span></span>

<span data-ttu-id="75cf5-159">Управляет восстановлением пакета во время сборки.</span><span class="sxs-lookup"><span data-stu-id="75cf5-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="75cf5-160">Ключ</span><span class="sxs-lookup"><span data-stu-id="75cf5-160">Key</span></span> | <span data-ttu-id="75cf5-161">Значение</span><span class="sxs-lookup"><span data-stu-id="75cf5-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="75cf5-162">enabled</span><span class="sxs-lookup"><span data-stu-id="75cf5-162">enabled</span></span> | <span data-ttu-id="75cf5-163">Логическое значение, указывающее, может ли NuGet выполнять автоматическое восстановление.</span><span class="sxs-lookup"><span data-stu-id="75cf5-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="75cf5-164">Вы также можете задать переменную среды `EnableNuGetPackageRestore` со значением `True` вместо того, чтобы задавать этот параметр в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="75cf5-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="75cf5-165">автоматическая</span><span class="sxs-lookup"><span data-stu-id="75cf5-165">automatic</span></span> | <span data-ttu-id="75cf5-166">Логическое значение, указывающее, должен ли диспетчер NuGet проверять отсутствие пакетов во время сборки.</span><span class="sxs-lookup"><span data-stu-id="75cf5-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="75cf5-167">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="75cf5-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="75cf5-168">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="75cf5-168">solution section</span></span>

<span data-ttu-id="75cf5-169">Определяет то, включается ли папка `packages` решения в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="75cf5-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="75cf5-170">Этот раздел работает только в файлах `nuget.config` в папке решения.</span><span class="sxs-lookup"><span data-stu-id="75cf5-170">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="75cf5-171">Ключ</span><span class="sxs-lookup"><span data-stu-id="75cf5-171">Key</span></span> | <span data-ttu-id="75cf5-172">Значение</span><span class="sxs-lookup"><span data-stu-id="75cf5-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="75cf5-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="75cf5-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="75cf5-174">Логическое значение, указывающее, следует ли игнорировать папку пакетов при работе с системой управления версиями.</span><span class="sxs-lookup"><span data-stu-id="75cf5-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="75cf5-175">Значением по умолчанию является false.</span><span class="sxs-lookup"><span data-stu-id="75cf5-175">The default value is false.</span></span> |

<span data-ttu-id="75cf5-176">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="75cf5-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="75cf5-177">Разделы источников пакета</span><span class="sxs-lookup"><span data-stu-id="75cf5-177">Package source sections</span></span>

<span data-ttu-id="75cf5-178">Параметры `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource` и `disabledPackageSources` в совокупности определяют то, как NuGet работает с репозиториями пакетов во время операций установки, восстановления и обновления.</span><span class="sxs-lookup"><span data-stu-id="75cf5-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="75cf5-179">Как правило, для управления этими параметрами используется [команда `nuget sources`](../tools/cli-ref-sources.md), за исключением параметра `apikeys`, который настраивается с помощью [команды `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="75cf5-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="75cf5-180">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="75cf5-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="75cf5-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="75cf5-181">packageSources</span></span>

<span data-ttu-id="75cf5-182">Выводит список всех известных источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="75cf5-182">Lists all known package sources.</span></span> <span data-ttu-id="75cf5-183">Во время операций восстановления и с любой проект в формате PackageReference, порядок учитывается.</span><span class="sxs-lookup"><span data-stu-id="75cf5-183">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="75cf5-184">NuGet нарушать порядок источников для установки и обновления с проектами с помощью `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="75cf5-184">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="75cf5-185">Ключ</span><span class="sxs-lookup"><span data-stu-id="75cf5-185">Key</span></span> | <span data-ttu-id="75cf5-186">Значение</span><span class="sxs-lookup"><span data-stu-id="75cf5-186">Value</span></span> |
| --- | --- |
| <span data-ttu-id="75cf5-187">(имя, назначаемое источнику пакета)</span><span class="sxs-lookup"><span data-stu-id="75cf5-187">(name to assign to the package source)</span></span> | <span data-ttu-id="75cf5-188">Путь к источнику пакета или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="75cf5-188">The path or URL of the package source.</span></span> |

<span data-ttu-id="75cf5-189">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="75cf5-189">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="75cf5-190">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="75cf5-190">packageSourceCredentials</span></span>

<span data-ttu-id="75cf5-191">Содержит имена пользователей и пароли источников, которые, как правило, задаются с помощью параметров `-username` и `-password` команды `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="75cf5-191">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="75cf5-192">По умолчанию пароли зашифровываются, если также не указан параметр `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="75cf5-192">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="75cf5-193">Ключ</span><span class="sxs-lookup"><span data-stu-id="75cf5-193">Key</span></span> | <span data-ttu-id="75cf5-194">Значение</span><span class="sxs-lookup"><span data-stu-id="75cf5-194">Value</span></span> |
| --- | --- |
| <span data-ttu-id="75cf5-195">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="75cf5-195">username</span></span> | <span data-ttu-id="75cf5-196">Имя пользователя источника в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="75cf5-196">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="75cf5-197">пароль</span><span class="sxs-lookup"><span data-stu-id="75cf5-197">password</span></span> | <span data-ttu-id="75cf5-198">Зашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="75cf5-198">The encrypted password for the source.</span></span> |
| <span data-ttu-id="75cf5-199">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="75cf5-199">cleartextpassword</span></span> | <span data-ttu-id="75cf5-200">Незашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="75cf5-200">The unencrypted password for the source.</span></span> |

<span data-ttu-id="75cf5-201">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="75cf5-201">**Example:**</span></span>

<span data-ttu-id="75cf5-202">В файле конфигурации элемент `<packageSourceCredentials>` содержит дочерние узлы для каждого применимого имени источника (пробелы в имени заменяются на `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="75cf5-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="75cf5-203">То есть для источников с именами Contoso и Test Source файл конфигурации содержит следующие значения при использовании зашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="75cf5-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="75cf5-204">При использовании незашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="75cf5-204">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="75cf5-205">apikeys</span><span class="sxs-lookup"><span data-stu-id="75cf5-205">apikeys</span></span>

<span data-ttu-id="75cf5-206">Содержит ключи для источников, которые используют проверку подлинности на основе ключей API. Эти ключи задаются с помощью [команды `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="75cf5-206">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="75cf5-207">Ключ</span><span class="sxs-lookup"><span data-stu-id="75cf5-207">Key</span></span> | <span data-ttu-id="75cf5-208">Значение</span><span class="sxs-lookup"><span data-stu-id="75cf5-208">Value</span></span> |
| --- | --- |
| <span data-ttu-id="75cf5-209">(URL-адрес источника)</span><span class="sxs-lookup"><span data-stu-id="75cf5-209">(source URL)</span></span> | <span data-ttu-id="75cf5-210">Зашифрованный ключ API.</span><span class="sxs-lookup"><span data-stu-id="75cf5-210">The encrypted API key.</span></span> |

<span data-ttu-id="75cf5-211">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="75cf5-211">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="75cf5-212">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="75cf5-212">disabledPackageSources</span></span>

<span data-ttu-id="75cf5-213">Определяет источники, отключенные в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="75cf5-213">Identified currently disabled sources.</span></span> <span data-ttu-id="75cf5-214">Значение может быть пустым.</span><span class="sxs-lookup"><span data-stu-id="75cf5-214">May be empty.</span></span>

| <span data-ttu-id="75cf5-215">Ключ</span><span class="sxs-lookup"><span data-stu-id="75cf5-215">Key</span></span> | <span data-ttu-id="75cf5-216">Значение</span><span class="sxs-lookup"><span data-stu-id="75cf5-216">Value</span></span> |
| --- | --- |
| <span data-ttu-id="75cf5-217">(имя источника)</span><span class="sxs-lookup"><span data-stu-id="75cf5-217">(name of source)</span></span> | <span data-ttu-id="75cf5-218">Логическое значение, указывающее, отключен ли источник.</span><span class="sxs-lookup"><span data-stu-id="75cf5-218">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="75cf5-219">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="75cf5-219">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="75cf5-220">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="75cf5-220">activePackageSource</span></span>

<span data-ttu-id="75cf5-221">*(Только в версиях 2.x; в версиях 3.x и более поздних является нерекомендуемым)*</span><span class="sxs-lookup"><span data-stu-id="75cf5-221">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="75cf5-222">Определяет текущий активный источник или указывает совокупность всех источников.</span><span class="sxs-lookup"><span data-stu-id="75cf5-222">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="75cf5-223">Ключ</span><span class="sxs-lookup"><span data-stu-id="75cf5-223">Key</span></span> | <span data-ttu-id="75cf5-224">Значение</span><span class="sxs-lookup"><span data-stu-id="75cf5-224">Value</span></span> |
| --- | --- |
| <span data-ttu-id="75cf5-225">(имя источника) или `All`</span><span class="sxs-lookup"><span data-stu-id="75cf5-225">(name of source) or `All`</span></span> | <span data-ttu-id="75cf5-226">Если ключ представляет имя источника, значением является путь к источнику или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="75cf5-226">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="75cf5-227">Если используется ключ `All`, требуется значение `(Aggregate source)`, объединяющее все источники пакетов, которые не отключены.</span><span class="sxs-lookup"><span data-stu-id="75cf5-227">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="75cf5-228">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="75cf5-228">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="75cf5-229">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="75cf5-229">Using environment variables</span></span>

<span data-ttu-id="75cf5-230">В значениях `nuget.config` можно использовать переменные среды (в NuGet 3.4 и более поздних версиях) для применения параметров во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="75cf5-230">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="75cf5-231">Например, если переменная среды `HOME` в Windows имеет значение `c:\users\username`, значение параметра `%HOME%\NuGetRepository` в файле конфигурации разрешается в `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="75cf5-231">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="75cf5-232">Аналогичным образом, если переменная `HOME` в Mac или Linux имеет значение `/home/myStuff`, параметр `%HOME%/NuGetRepository` в файле конфигурации разрешается в `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="75cf5-232">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="75cf5-233">Если переменная среды не найдена, NuGet использует буквальное значение из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="75cf5-233">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="75cf5-234">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="75cf5-234">Example config file</span></span>

<span data-ttu-id="75cf5-235">Ниже приведен пример файла `nuget.config`, в котором демонстрируется ряд параметров.</span><span class="sxs-lookup"><span data-stu-id="75cf5-235">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
