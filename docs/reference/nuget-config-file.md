---
title: Справочник по файлу NuGet.config
description: Справочник по файлу NuGet.Config, включая разделы config, bindingRedirects, packageRestore, solution и packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: c294e4c188db2e90e6bcb62b60f71ed5529977fe
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303523"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="6382f-103">Справочник по NuGet.config</span><span class="sxs-lookup"><span data-stu-id="6382f-103">nuget.config reference</span></span>

<span data-ttu-id="6382f-104">Для управления работой NuGet используются параметры в различных файлах `NuGet.Config`, как описано в разделе [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6382f-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="6382f-105">`nuget.config` — это XML-файл, содержащий узел `<configuration>` верхнего уровня, который, в свою очередь, содержит элементы разделов, описываемые в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6382f-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="6382f-106">Каждый раздел содержит ноль или более элементов.</span><span class="sxs-lookup"><span data-stu-id="6382f-106">Each section contains zero or more items.</span></span> <span data-ttu-id="6382f-107">См. [пример файла конфигурации](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="6382f-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="6382f-108">В именах регистр символов не учитывается, а в качестве значений могут использоваться [переменные среды](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="6382f-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="6382f-109">В этом разделе.</span><span class="sxs-lookup"><span data-stu-id="6382f-109">In this topic:</span></span>

- [<span data-ttu-id="6382f-110">Раздел config</span><span class="sxs-lookup"><span data-stu-id="6382f-110">config section</span></span>](#config-section)
- [<span data-ttu-id="6382f-111">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="6382f-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="6382f-112">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="6382f-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="6382f-113">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="6382f-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="6382f-114">[Разделы источников пакета](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="6382f-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="6382f-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="6382f-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="6382f-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="6382f-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="6382f-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="6382f-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="6382f-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="6382f-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="6382f-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="6382f-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="6382f-120">раздел trustedSigners</span><span class="sxs-lookup"><span data-stu-id="6382f-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="6382f-121">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="6382f-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="6382f-122">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="6382f-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="6382f-123">Раздел config</span><span class="sxs-lookup"><span data-stu-id="6382f-123">config section</span></span>

<span data-ttu-id="6382f-124">Содержит различные параметры конфигурации, которые можно задавать с помощью [команды `nuget config`](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="6382f-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="6382f-125">`dependencyVersion` и `repositoryPath` применяются только к проектам с помощью `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="6382f-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="6382f-126">`globalPackagesFolder` применяется только к проектам, в формате PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6382f-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="6382f-127">Ключ</span><span class="sxs-lookup"><span data-stu-id="6382f-127">Key</span></span> | <span data-ttu-id="6382f-128">Значение</span><span class="sxs-lookup"><span data-stu-id="6382f-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6382f-129">dependencyVersion (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="6382f-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="6382f-130">Значение `DependencyVersion` по умолчанию для установки, восстановления и обновления пакета, если параметр `-DependencyVersion` не указан напрямую.</span><span class="sxs-lookup"><span data-stu-id="6382f-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="6382f-131">Это значение также используется в пользовательском интерфейсе диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="6382f-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="6382f-132">Возможные значения: `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="6382f-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="6382f-133">globalPackagesFolder (проекты только с помощью PackageReference)</span><span class="sxs-lookup"><span data-stu-id="6382f-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="6382f-134">Расположение глобальной папки пакетов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6382f-134">The location of the default global packages folder.</span></span> <span data-ttu-id="6382f-135">Значение по умолчанию — `%userprofile%\.nuget\packages` (Windows) или `~/.nuget/packages` (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="6382f-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="6382f-136">В файлах `nuget.config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="6382f-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="6382f-137">Чтобы переопределить этот параметр, в переменной среды NUGET_PACKAGES, который имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="6382f-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="6382f-138">repositoryPath (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="6382f-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="6382f-139">Расположение, в котором следует установить пакеты NuGet вместо папки `$(Solutiondir)/packages` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6382f-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="6382f-140">В файлах `nuget.config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="6382f-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="6382f-141">Чтобы переопределить этот параметр, в переменной среды NUGET_PACKAGES, который имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="6382f-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="6382f-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="6382f-142">defaultPushSource</span></span> | <span data-ttu-id="6382f-143">Определяет URL-адрес источника пакета или путь к нему, который следует использовать по умолчанию, если другие источники пакета для операции не обнаружены.</span><span class="sxs-lookup"><span data-stu-id="6382f-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="6382f-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="6382f-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="6382f-145">Параметры прокси-сервера, которые следует использовать при подключении к источникам пакета; значение `http_proxy` должно иметь формат `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="6382f-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="6382f-146">Пароли зашифровываются, и их нельзя добавить вручную.</span><span class="sxs-lookup"><span data-stu-id="6382f-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="6382f-147">Значение параметра `no_proxy` представляет собой разделенный запятыми список доменов, для которых производится обход прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="6382f-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="6382f-148">В качестве этих значений можно также использовать переменные среды http_proxy и no_proxy.</span><span class="sxs-lookup"><span data-stu-id="6382f-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="6382f-149">Дополнительные сведения см. в записи блога [Параметры прокси-сервера в NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="6382f-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="6382f-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="6382f-150">signatureValidationMode</span></span> | <span data-ttu-id="6382f-151">Указывает режим проверки, используемый для проверки подписи пакетов для установки и восстановления.</span><span class="sxs-lookup"><span data-stu-id="6382f-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="6382f-152">Значения: `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="6382f-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="6382f-153">По умолчанию — `accept`.</span><span class="sxs-lookup"><span data-stu-id="6382f-153">Defaults to `accept`.</span></span>

<span data-ttu-id="6382f-154">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6382f-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="6382f-155">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="6382f-155">bindingRedirects section</span></span>

<span data-ttu-id="6382f-156">Определяет то, производится ли в NuGet автоматическая переадресация привязок при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="6382f-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="6382f-157">Ключ</span><span class="sxs-lookup"><span data-stu-id="6382f-157">Key</span></span> | <span data-ttu-id="6382f-158">Значение</span><span class="sxs-lookup"><span data-stu-id="6382f-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6382f-159">skip</span><span class="sxs-lookup"><span data-stu-id="6382f-159">skip</span></span> | <span data-ttu-id="6382f-160">Логическое значение, указывающее, следует ли пропустить автоматическую переадресацию привязок.</span><span class="sxs-lookup"><span data-stu-id="6382f-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="6382f-161">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="6382f-161">The default is false.</span></span> |

<span data-ttu-id="6382f-162">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6382f-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="6382f-163">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="6382f-163">packageRestore section</span></span>

<span data-ttu-id="6382f-164">Управляет восстановлением пакета во время сборки.</span><span class="sxs-lookup"><span data-stu-id="6382f-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="6382f-165">Ключ</span><span class="sxs-lookup"><span data-stu-id="6382f-165">Key</span></span> | <span data-ttu-id="6382f-166">Значение</span><span class="sxs-lookup"><span data-stu-id="6382f-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6382f-167">enabled</span><span class="sxs-lookup"><span data-stu-id="6382f-167">enabled</span></span> | <span data-ttu-id="6382f-168">Логическое значение, указывающее, может ли NuGet выполнять автоматическое восстановление.</span><span class="sxs-lookup"><span data-stu-id="6382f-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="6382f-169">Вы также можете задать переменную среды `EnableNuGetPackageRestore` со значением `True` вместо того, чтобы задавать этот параметр в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6382f-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="6382f-170">автоматическая</span><span class="sxs-lookup"><span data-stu-id="6382f-170">automatic</span></span> | <span data-ttu-id="6382f-171">Логическое значение, указывающее, должен ли диспетчер NuGet проверять отсутствие пакетов во время сборки.</span><span class="sxs-lookup"><span data-stu-id="6382f-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="6382f-172">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6382f-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="6382f-173">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="6382f-173">solution section</span></span>

<span data-ttu-id="6382f-174">Определяет то, включается ли папка `packages` решения в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="6382f-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="6382f-175">Этот раздел работает только в файлах `nuget.config` в папке решения.</span><span class="sxs-lookup"><span data-stu-id="6382f-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="6382f-176">Ключ</span><span class="sxs-lookup"><span data-stu-id="6382f-176">Key</span></span> | <span data-ttu-id="6382f-177">Значение</span><span class="sxs-lookup"><span data-stu-id="6382f-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6382f-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="6382f-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="6382f-179">Логическое значение, указывающее, следует ли игнорировать папку пакетов при работе с системой управления версиями.</span><span class="sxs-lookup"><span data-stu-id="6382f-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="6382f-180">Значением по умолчанию является false.</span><span class="sxs-lookup"><span data-stu-id="6382f-180">The default value is false.</span></span> |

<span data-ttu-id="6382f-181">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6382f-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="6382f-182">Разделы источников пакета</span><span class="sxs-lookup"><span data-stu-id="6382f-182">Package source sections</span></span>

<span data-ttu-id="6382f-183">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` И `trustedSigners` все работают вместе, чтобы настроить, как NuGet работает с репозиториями пакетов во время установки, восстановления и операций обновления.</span><span class="sxs-lookup"><span data-stu-id="6382f-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="6382f-184">[ `nuget sources` Команда](../tools/cli-ref-sources.md) обычно используется для управления этими параметрами, за исключением `apikeys` который настраивается с помощью [ `nuget setapikey` команда](../tools/cli-ref-setapikey.md), и `trustedSigners` управляемых с помощью [ `nuget trusted-signers` команда](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="6382f-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="6382f-185">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="6382f-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="6382f-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="6382f-186">packageSources</span></span>

<span data-ttu-id="6382f-187">Выводит список всех известных источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="6382f-187">Lists all known package sources.</span></span> <span data-ttu-id="6382f-188">Порядок игнорируется во время операций восстановления, а также для любого проекта, в формате PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6382f-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="6382f-189">NuGet учитывает порядок источников для установки и операции обновления с проектами, использующими `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="6382f-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="6382f-190">Ключ</span><span class="sxs-lookup"><span data-stu-id="6382f-190">Key</span></span> | <span data-ttu-id="6382f-191">Значение</span><span class="sxs-lookup"><span data-stu-id="6382f-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6382f-192">(имя, назначаемое источнику пакета)</span><span class="sxs-lookup"><span data-stu-id="6382f-192">(name to assign to the package source)</span></span> | <span data-ttu-id="6382f-193">Путь к источнику пакета или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="6382f-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="6382f-194">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6382f-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="6382f-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="6382f-195">packageSourceCredentials</span></span>

<span data-ttu-id="6382f-196">Содержит имена пользователей и пароли источников, которые, как правило, задаются с помощью параметров `-username` и `-password` команды `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="6382f-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="6382f-197">По умолчанию пароли зашифровываются, если также не указан параметр `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="6382f-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="6382f-198">Ключ</span><span class="sxs-lookup"><span data-stu-id="6382f-198">Key</span></span> | <span data-ttu-id="6382f-199">Значение</span><span class="sxs-lookup"><span data-stu-id="6382f-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6382f-200">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="6382f-200">username</span></span> | <span data-ttu-id="6382f-201">Имя пользователя источника в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="6382f-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="6382f-202">пароль</span><span class="sxs-lookup"><span data-stu-id="6382f-202">password</span></span> | <span data-ttu-id="6382f-203">Зашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="6382f-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="6382f-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="6382f-204">cleartextpassword</span></span> | <span data-ttu-id="6382f-205">Незашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="6382f-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="6382f-206">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="6382f-206">**Example:**</span></span>

<span data-ttu-id="6382f-207">В файле конфигурации элемент `<packageSourceCredentials>` содержит дочерние узлы для каждого применимого имени источника (пробелы в имени заменяются на `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="6382f-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="6382f-208">То есть для источников с именами Contoso и Test Source файл конфигурации содержит следующие значения при использовании зашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="6382f-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="6382f-209">При использовании незашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="6382f-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="6382f-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="6382f-210">apikeys</span></span>

<span data-ttu-id="6382f-211">Содержит ключи для источников, которые используют проверку подлинности на основе ключей API. Эти ключи задаются с помощью [команды `nuget setapikey`](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="6382f-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="6382f-212">Ключ</span><span class="sxs-lookup"><span data-stu-id="6382f-212">Key</span></span> | <span data-ttu-id="6382f-213">Значение</span><span class="sxs-lookup"><span data-stu-id="6382f-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6382f-214">(URL-адрес источника)</span><span class="sxs-lookup"><span data-stu-id="6382f-214">(source URL)</span></span> | <span data-ttu-id="6382f-215">Зашифрованный ключ API.</span><span class="sxs-lookup"><span data-stu-id="6382f-215">The encrypted API key.</span></span> |

<span data-ttu-id="6382f-216">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6382f-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="6382f-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="6382f-217">disabledPackageSources</span></span>

<span data-ttu-id="6382f-218">Определяет источники, отключенные в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="6382f-218">Identified currently disabled sources.</span></span> <span data-ttu-id="6382f-219">Значение может быть пустым.</span><span class="sxs-lookup"><span data-stu-id="6382f-219">May be empty.</span></span>

| <span data-ttu-id="6382f-220">Ключ</span><span class="sxs-lookup"><span data-stu-id="6382f-220">Key</span></span> | <span data-ttu-id="6382f-221">Значение</span><span class="sxs-lookup"><span data-stu-id="6382f-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6382f-222">(имя источника)</span><span class="sxs-lookup"><span data-stu-id="6382f-222">(name of source)</span></span> | <span data-ttu-id="6382f-223">Логическое значение, указывающее, отключен ли источник.</span><span class="sxs-lookup"><span data-stu-id="6382f-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="6382f-224">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="6382f-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="6382f-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="6382f-225">activePackageSource</span></span>

<span data-ttu-id="6382f-226">*(Только в версиях 2.x; в версиях 3.x и более поздних является нерекомендуемым)*</span><span class="sxs-lookup"><span data-stu-id="6382f-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="6382f-227">Определяет текущий активный источник или указывает совокупность всех источников.</span><span class="sxs-lookup"><span data-stu-id="6382f-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="6382f-228">Ключ</span><span class="sxs-lookup"><span data-stu-id="6382f-228">Key</span></span> | <span data-ttu-id="6382f-229">Значение</span><span class="sxs-lookup"><span data-stu-id="6382f-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6382f-230">(имя источника) или `All`</span><span class="sxs-lookup"><span data-stu-id="6382f-230">(name of source) or `All`</span></span> | <span data-ttu-id="6382f-231">Если ключ представляет имя источника, значением является путь к источнику или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="6382f-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="6382f-232">Если используется ключ `All`, требуется значение `(Aggregate source)`, объединяющее все источники пакетов, которые не отключены.</span><span class="sxs-lookup"><span data-stu-id="6382f-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="6382f-233">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6382f-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="6382f-234">раздел trustedSigners</span><span class="sxs-lookup"><span data-stu-id="6382f-234">trustedSigners section</span></span>

<span data-ttu-id="6382f-235">Хранилища доверенных подписавших, используемый для обеспечения пакета при установке или восстановлении.</span><span class="sxs-lookup"><span data-stu-id="6382f-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="6382f-236">Этот список не может быть пустым, когда пользователь устанавливает `signatureValidationMode` для `require`.</span><span class="sxs-lookup"><span data-stu-id="6382f-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="6382f-237">В этом разделе можно обновить с помощью [ `nuget trusted-signers` команда](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="6382f-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="6382f-238">**Схемы**:</span><span class="sxs-lookup"><span data-stu-id="6382f-238">**Schema**:</span></span>

<span data-ttu-id="6382f-239">Доверенным лицом имеет коллекцию `certificate` элементы, которые прикрепить все сертификаты, которые идентифицируют заданного подписавшего.</span><span class="sxs-lookup"><span data-stu-id="6382f-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="6382f-240">Доверенным лицом может быть либо `Author` или `Repository`.</span><span class="sxs-lookup"><span data-stu-id="6382f-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="6382f-241">Доверенная *репозитория* также указывает `serviceIndex` для репозитория (которого должен быть допустимым `https` uri) и при необходимости можно указать точку с запятой список с разделителями `owners` ограничить еще более, является доверенным из этого конкретного репозитория.</span><span class="sxs-lookup"><span data-stu-id="6382f-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="6382f-242">Поддерживаемые алгоритмы хэширования для отпечаток сертификата, `SHA256`, `SHA384` и `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="6382f-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="6382f-243">Если `certificate` указывает `allowUntrustedRoot` как `true` заданного сертификата может создать недоверенный корневой цепочку при построении цепочки сертификатов, как часть проверки подписи.</span><span class="sxs-lookup"><span data-stu-id="6382f-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="6382f-244">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="6382f-244">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a><span data-ttu-id="6382f-245">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="6382f-245">Using environment variables</span></span>

<span data-ttu-id="6382f-246">В значениях `nuget.config` можно использовать переменные среды (в NuGet 3.4 и более поздних версиях) для применения параметров во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="6382f-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="6382f-247">Например, если переменная среды `HOME` в Windows имеет значение `c:\users\username`, значение параметра `%HOME%\NuGetRepository` в файле конфигурации разрешается в `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="6382f-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="6382f-248">Аналогичным образом, если переменная `HOME` в Mac или Linux имеет значение `/home/myStuff`, параметр `%HOME%/NuGetRepository` в файле конфигурации разрешается в `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="6382f-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="6382f-249">Если переменная среды не найдена, NuGet использует буквальное значение из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6382f-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="6382f-250">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="6382f-250">Example config file</span></span>

<span data-ttu-id="6382f-251">Ниже приведен пример файла `nuget.config`, в котором демонстрируется ряд параметров.</span><span class="sxs-lookup"><span data-stu-id="6382f-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
