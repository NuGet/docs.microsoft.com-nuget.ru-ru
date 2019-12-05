---
title: Справочник по файлу NuGet. config
description: Справочник по файлу NuGet.Config, включая разделы config, bindingRedirects, packageRestore, solution и packageSource.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 0b052bd03625172f1b941c365cbedf7629809d6f
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825200"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="3eb16-103">Справочник по NuGet. config</span><span class="sxs-lookup"><span data-stu-id="3eb16-103">nuget.config reference</span></span>

<span data-ttu-id="3eb16-104">Поведение NuGet управляется параметрами в различных `NuGet.Config` или `nuget.config` файлах, как описано в разделе [Общие конфигурации NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="3eb16-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="3eb16-105">`nuget.config` — это XML-файл, содержащий узел `<configuration>` верхнего уровня, который, в свою очередь, содержит элементы разделов, описываемые в этой статье.</span><span class="sxs-lookup"><span data-stu-id="3eb16-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="3eb16-106">Каждый раздел содержит ноль или более элементов.</span><span class="sxs-lookup"><span data-stu-id="3eb16-106">Each section contains zero or more items.</span></span> <span data-ttu-id="3eb16-107">См. [пример файла конфигурации](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="3eb16-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="3eb16-108">В именах регистр символов не учитывается, а в качестве значений могут использоваться [переменные среды](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="3eb16-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="3eb16-109">Раздел config</span><span class="sxs-lookup"><span data-stu-id="3eb16-109">config section</span></span>

<span data-ttu-id="3eb16-110">Содержит различные параметры конфигурации, которые можно задавать с помощью [команды `nuget config`](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="3eb16-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="3eb16-111">`dependencyVersion` и `repositoryPath` применяются только к проектам, использующим `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="3eb16-112">`globalPackagesFolder` применяется только к проектам, использующим формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3eb16-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="3eb16-113">Key</span><span class="sxs-lookup"><span data-stu-id="3eb16-113">Key</span></span> | <span data-ttu-id="3eb16-114">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3eb16-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3eb16-115">dependencyVersion (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="3eb16-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="3eb16-116">Значение `DependencyVersion` по умолчанию для установки, восстановления и обновления пакета, если параметр `-DependencyVersion` не указан напрямую.</span><span class="sxs-lookup"><span data-stu-id="3eb16-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="3eb16-117">Это значение также используется в пользовательском интерфейсе диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="3eb16-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="3eb16-118">Возможные значения: `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="3eb16-119">globalPackagesFolder (проекты, использующие только PackageReference)</span><span class="sxs-lookup"><span data-stu-id="3eb16-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="3eb16-120">Расположение глобальной папки пакетов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3eb16-120">The location of the default global packages folder.</span></span> <span data-ttu-id="3eb16-121">Значение по умолчанию — `%userprofile%\.nuget\packages` (Windows) или `~/.nuget/packages` (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="3eb16-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="3eb16-122">В файлах `nuget.config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="3eb16-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="3eb16-123">Этот параметр переопределяется переменной среды NUGET_PACKAGES, которая имеет приоритет.</span><span class="sxs-lookup"><span data-stu-id="3eb16-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="3eb16-124">repositoryPath (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="3eb16-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="3eb16-125">Расположение, в котором следует установить пакеты NuGet вместо папки `$(Solutiondir)/packages` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3eb16-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="3eb16-126">В файлах `nuget.config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="3eb16-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="3eb16-127">Этот параметр переопределяется переменной среды NUGET_PACKAGES, которая имеет приоритет.</span><span class="sxs-lookup"><span data-stu-id="3eb16-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="3eb16-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="3eb16-128">defaultPushSource</span></span> | <span data-ttu-id="3eb16-129">Определяет URL-адрес источника пакета или путь к нему, который следует использовать по умолчанию, если другие источники пакета для операции не обнаружены.</span><span class="sxs-lookup"><span data-stu-id="3eb16-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="3eb16-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="3eb16-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="3eb16-131">Параметры прокси-сервера, которые следует использовать при подключении к источникам пакета; значение `http_proxy` должно иметь формат `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="3eb16-132">Пароли зашифровываются, и их нельзя добавить вручную.</span><span class="sxs-lookup"><span data-stu-id="3eb16-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="3eb16-133">Значение параметра `no_proxy` представляет собой разделенный запятыми список доменов, для которых производится обход прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="3eb16-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="3eb16-134">В качестве этих значений можно также использовать переменные среды http_proxy и no_proxy.</span><span class="sxs-lookup"><span data-stu-id="3eb16-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="3eb16-135">Дополнительные сведения см. в записи блога [Параметры прокси-сервера в NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="3eb16-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="3eb16-136">сигнатуревалидатионмоде</span><span class="sxs-lookup"><span data-stu-id="3eb16-136">signatureValidationMode</span></span> | <span data-ttu-id="3eb16-137">Указывает режим проверки, используемый для проверки сигнатур пакетов при установке пакета и восстановления.</span><span class="sxs-lookup"><span data-stu-id="3eb16-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="3eb16-138">Значения: `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="3eb16-139">По умолчанию — `accept`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-139">Defaults to `accept`.</span></span>

<span data-ttu-id="3eb16-140">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="3eb16-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="3eb16-141">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="3eb16-141">bindingRedirects section</span></span>

<span data-ttu-id="3eb16-142">Определяет то, производится ли в NuGet автоматическая переадресация привязок при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="3eb16-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="3eb16-143">Key</span><span class="sxs-lookup"><span data-stu-id="3eb16-143">Key</span></span> | <span data-ttu-id="3eb16-144">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3eb16-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3eb16-145">skip</span><span class="sxs-lookup"><span data-stu-id="3eb16-145">skip</span></span> | <span data-ttu-id="3eb16-146">Логическое значение, указывающее, следует ли пропустить автоматическую переадресацию привязок.</span><span class="sxs-lookup"><span data-stu-id="3eb16-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="3eb16-147">Значение по умолчанию: false.</span><span class="sxs-lookup"><span data-stu-id="3eb16-147">The default is false.</span></span> |

<span data-ttu-id="3eb16-148">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="3eb16-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="3eb16-149">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="3eb16-149">packageRestore section</span></span>

<span data-ttu-id="3eb16-150">Управляет восстановлением пакета во время сборки.</span><span class="sxs-lookup"><span data-stu-id="3eb16-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="3eb16-151">Key</span><span class="sxs-lookup"><span data-stu-id="3eb16-151">Key</span></span> | <span data-ttu-id="3eb16-152">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3eb16-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3eb16-153">включен</span><span class="sxs-lookup"><span data-stu-id="3eb16-153">enabled</span></span> | <span data-ttu-id="3eb16-154">Логическое значение, указывающее, может ли NuGet выполнять автоматическое восстановление.</span><span class="sxs-lookup"><span data-stu-id="3eb16-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="3eb16-155">Вы также можете задать переменную среды `EnableNuGetPackageRestore` со значением `True` вместо того, чтобы задавать этот параметр в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3eb16-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="3eb16-156">автоматическая</span><span class="sxs-lookup"><span data-stu-id="3eb16-156">automatic</span></span> | <span data-ttu-id="3eb16-157">Логическое значение, указывающее, должен ли диспетчер NuGet проверять отсутствие пакетов во время сборки.</span><span class="sxs-lookup"><span data-stu-id="3eb16-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="3eb16-158">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="3eb16-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="3eb16-159">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="3eb16-159">solution section</span></span>

<span data-ttu-id="3eb16-160">Определяет то, включается ли папка `packages` решения в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="3eb16-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="3eb16-161">Этот раздел работает только в файлах `nuget.config` в папке решения.</span><span class="sxs-lookup"><span data-stu-id="3eb16-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="3eb16-162">Key</span><span class="sxs-lookup"><span data-stu-id="3eb16-162">Key</span></span> | <span data-ttu-id="3eb16-163">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3eb16-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3eb16-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="3eb16-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="3eb16-165">Логическое значение, указывающее, следует ли игнорировать папку пакетов при работе с системой управления версиями.</span><span class="sxs-lookup"><span data-stu-id="3eb16-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="3eb16-166">Значение по умолчанию — false.</span><span class="sxs-lookup"><span data-stu-id="3eb16-166">The default value is false.</span></span> |

<span data-ttu-id="3eb16-167">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="3eb16-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="3eb16-168">Разделы источников пакета</span><span class="sxs-lookup"><span data-stu-id="3eb16-168">Package source sections</span></span>

<span data-ttu-id="3eb16-169">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` и `trustedSigners` все работают вместе, чтобы настроить способ работы NuGet с репозиториями пакетов во время операций установки, восстановления и обновления.</span><span class="sxs-lookup"><span data-stu-id="3eb16-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="3eb16-170">[Команда`nuget sources`](../reference/cli-reference/cli-ref-sources.md) обычно используется для управления этими параметрами, за исключением `apikeys`, которые управляются с помощью [команды`nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md), и `trustedSigners`, управляемой с помощью [команды`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="3eb16-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="3eb16-171">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="3eb16-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="3eb16-172">packageSources</span></span>

<span data-ttu-id="3eb16-173">Выводит список всех известных источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="3eb16-173">Lists all known package sources.</span></span> <span data-ttu-id="3eb16-174">Порядок пропускается во время операций восстановления и с любым проектом, использующим формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3eb16-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="3eb16-175">NuGet учитывает порядок источников для операций установки и обновления проектов, использующих `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="3eb16-176">Key</span><span class="sxs-lookup"><span data-stu-id="3eb16-176">Key</span></span> | <span data-ttu-id="3eb16-177">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3eb16-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3eb16-178">(имя, назначаемое источнику пакета)</span><span class="sxs-lookup"><span data-stu-id="3eb16-178">(name to assign to the package source)</span></span> | <span data-ttu-id="3eb16-179">Путь к источнику пакета или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3eb16-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="3eb16-180">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="3eb16-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="3eb16-181">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="3eb16-181">packageSourceCredentials</span></span>

<span data-ttu-id="3eb16-182">Содержит имена пользователей и пароли источников, которые, как правило, задаются с помощью параметров `-username` и `-password` команды `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-182">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="3eb16-183">По умолчанию пароли зашифровываются, если также не указан параметр `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-183">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="3eb16-184">Key</span><span class="sxs-lookup"><span data-stu-id="3eb16-184">Key</span></span> | <span data-ttu-id="3eb16-185">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3eb16-185">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3eb16-186">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="3eb16-186">username</span></span> | <span data-ttu-id="3eb16-187">Имя пользователя источника в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="3eb16-187">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="3eb16-188">пароль .</span><span class="sxs-lookup"><span data-stu-id="3eb16-188">password</span></span> | <span data-ttu-id="3eb16-189">Зашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="3eb16-189">The encrypted password for the source.</span></span> |
| <span data-ttu-id="3eb16-190">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="3eb16-190">cleartextpassword</span></span> | <span data-ttu-id="3eb16-191">Незашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="3eb16-191">The unencrypted password for the source.</span></span> |

<span data-ttu-id="3eb16-192">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="3eb16-192">**Example:**</span></span>

<span data-ttu-id="3eb16-193">В файле конфигурации элемент `<packageSourceCredentials>` содержит дочерние узлы для каждого применимого имени источника (пробелы в имени заменяются на `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="3eb16-193">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="3eb16-194">То есть для источников с именами Contoso и Test Source файл конфигурации содержит следующие значения при использовании зашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="3eb16-194">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="3eb16-195">При использовании незашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="3eb16-195">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="3eb16-196">apikeys</span><span class="sxs-lookup"><span data-stu-id="3eb16-196">apikeys</span></span>

<span data-ttu-id="3eb16-197">Содержит ключи для источников, которые используют проверку подлинности на основе ключей API. Эти ключи задаются с помощью [команды `nuget setapikey`](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="3eb16-197">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="3eb16-198">Key</span><span class="sxs-lookup"><span data-stu-id="3eb16-198">Key</span></span> | <span data-ttu-id="3eb16-199">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3eb16-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3eb16-200">(URL-адрес источника)</span><span class="sxs-lookup"><span data-stu-id="3eb16-200">(source URL)</span></span> | <span data-ttu-id="3eb16-201">Зашифрованный ключ API.</span><span class="sxs-lookup"><span data-stu-id="3eb16-201">The encrypted API key.</span></span> |

<span data-ttu-id="3eb16-202">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="3eb16-202">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="3eb16-203">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="3eb16-203">disabledPackageSources</span></span>

<span data-ttu-id="3eb16-204">Определяет источники, отключенные в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="3eb16-204">Identified currently disabled sources.</span></span> <span data-ttu-id="3eb16-205">Значение может быть пустым.</span><span class="sxs-lookup"><span data-stu-id="3eb16-205">May be empty.</span></span>

| <span data-ttu-id="3eb16-206">Key</span><span class="sxs-lookup"><span data-stu-id="3eb16-206">Key</span></span> | <span data-ttu-id="3eb16-207">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3eb16-207">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3eb16-208">(имя источника)</span><span class="sxs-lookup"><span data-stu-id="3eb16-208">(name of source)</span></span> | <span data-ttu-id="3eb16-209">Логическое значение, указывающее, отключен ли источник.</span><span class="sxs-lookup"><span data-stu-id="3eb16-209">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="3eb16-210">**Пример:**</span><span class="sxs-lookup"><span data-stu-id="3eb16-210">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="3eb16-211">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="3eb16-211">activePackageSource</span></span>

<span data-ttu-id="3eb16-212">*(Только в версиях 2.x; в версиях 3.x и более поздних является нерекомендуемым)*</span><span class="sxs-lookup"><span data-stu-id="3eb16-212">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="3eb16-213">Определяет текущий активный источник или указывает совокупность всех источников.</span><span class="sxs-lookup"><span data-stu-id="3eb16-213">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="3eb16-214">Key</span><span class="sxs-lookup"><span data-stu-id="3eb16-214">Key</span></span> | <span data-ttu-id="3eb16-215">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3eb16-215">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3eb16-216">(имя источника) или `All`</span><span class="sxs-lookup"><span data-stu-id="3eb16-216">(name of source) or `All`</span></span> | <span data-ttu-id="3eb16-217">Если ключ представляет имя источника, значением является путь к источнику или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3eb16-217">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="3eb16-218">Если используется ключ `All`, требуется значение `(Aggregate source)`, объединяющее все источники пакетов, которые не отключены.</span><span class="sxs-lookup"><span data-stu-id="3eb16-218">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="3eb16-219">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="3eb16-219">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="3eb16-220">Раздел trustedSigners</span><span class="sxs-lookup"><span data-stu-id="3eb16-220">trustedSigners section</span></span>

<span data-ttu-id="3eb16-221">Хранит доверенные подписывающих, используемые для разрешения пакета во время установки или восстановления.</span><span class="sxs-lookup"><span data-stu-id="3eb16-221">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="3eb16-222">Этот список не может быть пустым, когда пользователь задает `signatureValidationMode` для `require`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-222">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="3eb16-223">Этот раздел можно обновить с помощью [команды`nuget trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="3eb16-223">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="3eb16-224">**Схема**.</span><span class="sxs-lookup"><span data-stu-id="3eb16-224">**Schema**:</span></span>

<span data-ttu-id="3eb16-225">Доверенный подписывающий имеет коллекцию элементов `certificate`, которые закрепляют все сертификаты, которые обозначают данного подписавший.</span><span class="sxs-lookup"><span data-stu-id="3eb16-225">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="3eb16-226">Доверенный подписывающий может быть либо `Author`, либо `Repository`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-226">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="3eb16-227">В доверенном *репозитории* также указывается `serviceIndex` для репозитория (который должен быть допустимым `https` URI). при необходимости можно указать список `owners`, разделенных точкой с запятой, чтобы ограничить число пользователей, которым доверяет этот конкретный репозиторий.</span><span class="sxs-lookup"><span data-stu-id="3eb16-227">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="3eb16-228">Поддерживаемые алгоритмы хэширования, используемые для отпечатка сертификата, — это `SHA256`, `SHA384` и `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-228">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="3eb16-229">Если `certificate` указывает `allowUntrustedRoot` как `true` данный сертификат может быть связан с недоверенным корнем при создании цепочки сертификатов в ходе проверки подписи.</span><span class="sxs-lookup"><span data-stu-id="3eb16-229">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="3eb16-230">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="3eb16-230">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="3eb16-231">Раздел fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="3eb16-231">fallbackPackageFolders section</span></span>

<span data-ttu-id="3eb16-232">*(3.5 +)* Предоставляет способ предварительной установки пакетов, чтобы не выполнять никаких действий, если пакет найден в резервных папках.</span><span class="sxs-lookup"><span data-stu-id="3eb16-232">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="3eb16-233">Папки с резервными пакетами имеют точно такую же структуру файлов, как и папка глобального пакета: *. nupkg* существует, и все файлы извлекаются.</span><span class="sxs-lookup"><span data-stu-id="3eb16-233">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="3eb16-234">Логика поиска для этой конфигурации:</span><span class="sxs-lookup"><span data-stu-id="3eb16-234">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="3eb16-235">Найдите папку Global Package, чтобы узнать, не скачан ли уже пакет или версия.</span><span class="sxs-lookup"><span data-stu-id="3eb16-235">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="3eb16-236">Найдите в папках резервные папки, соответствующие пакету или версии.</span><span class="sxs-lookup"><span data-stu-id="3eb16-236">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="3eb16-237">Если поиск выполнен успешно, загрузка не требуется.</span><span class="sxs-lookup"><span data-stu-id="3eb16-237">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="3eb16-238">Если совпадение не найдено, NuGet проверяет источники файлов, а затем HTTP-источники, а затем загружает пакеты.</span><span class="sxs-lookup"><span data-stu-id="3eb16-238">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="3eb16-239">Key</span><span class="sxs-lookup"><span data-stu-id="3eb16-239">Key</span></span> | <span data-ttu-id="3eb16-240">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3eb16-240">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3eb16-241">(имя резервной папки)</span><span class="sxs-lookup"><span data-stu-id="3eb16-241">(name of fallback folder)</span></span> | <span data-ttu-id="3eb16-242">Путь к резервной папке.</span><span class="sxs-lookup"><span data-stu-id="3eb16-242">Path to fallback folder.</span></span> |

<span data-ttu-id="3eb16-243">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="3eb16-243">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="3eb16-244">Раздел packageManagement</span><span class="sxs-lookup"><span data-stu-id="3eb16-244">packageManagement section</span></span>

<span data-ttu-id="3eb16-245">Задает формат управления пакетами по умолчанию: *Packages. config* или PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3eb16-245">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="3eb16-246">Проекты в стиле SDK всегда используют PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3eb16-246">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="3eb16-247">Key</span><span class="sxs-lookup"><span data-stu-id="3eb16-247">Key</span></span> | <span data-ttu-id="3eb16-248">{2&gt;Value&lt;2}</span><span class="sxs-lookup"><span data-stu-id="3eb16-248">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3eb16-249">формат</span><span class="sxs-lookup"><span data-stu-id="3eb16-249">format</span></span> | <span data-ttu-id="3eb16-250">Логическое значение, указывающее формат управления пакетами по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3eb16-250">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="3eb16-251">Если `1`, то используется формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3eb16-251">If `1`, format is PackageReference.</span></span> <span data-ttu-id="3eb16-252">Если `0`, то format имеет формат *Packages. config*.</span><span class="sxs-lookup"><span data-stu-id="3eb16-252">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="3eb16-253">отключенные</span><span class="sxs-lookup"><span data-stu-id="3eb16-253">disabled</span></span> | <span data-ttu-id="3eb16-254">Логическое значение, указывающее, следует ли отображать запрос на выбор формата пакета по умолчанию при первом установке пакета.</span><span class="sxs-lookup"><span data-stu-id="3eb16-254">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="3eb16-255">`False` скрывает запрос.</span><span class="sxs-lookup"><span data-stu-id="3eb16-255">`False` hides the prompt.</span></span> |

<span data-ttu-id="3eb16-256">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="3eb16-256">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="3eb16-257">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="3eb16-257">Using environment variables</span></span>

<span data-ttu-id="3eb16-258">В значениях `nuget.config` можно использовать переменные среды (в NuGet 3.4 и более поздних версиях) для применения параметров во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="3eb16-258">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="3eb16-259">Например, если переменная среды `HOME` в Windows имеет значение `c:\users\username`, значение параметра `%HOME%\NuGetRepository` в файле конфигурации разрешается в `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-259">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="3eb16-260">Аналогичным образом, если переменная `HOME` в Mac или Linux имеет значение `/home/myStuff`, параметр `%HOME%/NuGetRepository` в файле конфигурации разрешается в `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="3eb16-260">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="3eb16-261">Если переменная среды не найдена, NuGet использует буквальное значение из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3eb16-261">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="3eb16-262">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="3eb16-262">Example config file</span></span>

<span data-ttu-id="3eb16-263">Ниже приведен пример файла `nuget.config`, в котором демонстрируется ряд параметров.</span><span class="sxs-lookup"><span data-stu-id="3eb16-263">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
