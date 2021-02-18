---
title: Ссылка на файл nuget.config
description: Справочник по файлу NuGet.Config, включая разделы config, bindingRedirects, packageRestore, solution и packageSource.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 60626a5a2a261241e0dce34421f73a86d815e454
ms.sourcegitcommit: aeb9072f2fcaca73dc9de05b7fd643f1aa7c5821
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/18/2021
ms.locfileid: "101101353"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="d22d8-103">Справочник по nuget.config</span><span class="sxs-lookup"><span data-stu-id="d22d8-103">nuget.config reference</span></span>

<span data-ttu-id="d22d8-104">Поведение NuGet управляется параметрами в различных `NuGet.Config` файлах или `nuget.config` , как описано в разделе [Общие конфигурации NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="d22d8-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="d22d8-105">`nuget.config` — это XML-файл, содержащий узел `<configuration>` верхнего уровня, который, в свою очередь, содержит элементы разделов, описываемые в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d22d8-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="d22d8-106">Каждый раздел содержит ноль или более элементов.</span><span class="sxs-lookup"><span data-stu-id="d22d8-106">Each section contains zero or more items.</span></span> <span data-ttu-id="d22d8-107">См. [пример файла конфигурации](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="d22d8-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="d22d8-108">В именах регистр символов не учитывается, а в качестве значений могут использоваться [переменные среды](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="d22d8-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="d22d8-109">Раздел config</span><span class="sxs-lookup"><span data-stu-id="d22d8-109">config section</span></span>

<span data-ttu-id="d22d8-110">Содержит прочие параметры конфигурации, которые можно задать с помощью [ `nuget config` команды](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="d22d8-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="d22d8-111">`dependencyVersion` и `repositoryPath` применяются только к проектам с помощью `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="d22d8-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="d22d8-112">`globalPackagesFolder` применяется только к проектам, использующим формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d22d8-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="d22d8-113">Ключ</span><span class="sxs-lookup"><span data-stu-id="d22d8-113">Key</span></span> | <span data-ttu-id="d22d8-114">Значение</span><span class="sxs-lookup"><span data-stu-id="d22d8-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d22d8-115">dependencyVersion (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="d22d8-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="d22d8-116">Значение `DependencyVersion` по умолчанию для установки, восстановления и обновления пакета, если параметр `-DependencyVersion` не указан напрямую.</span><span class="sxs-lookup"><span data-stu-id="d22d8-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="d22d8-117">Это значение также используется в пользовательском интерфейсе диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="d22d8-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="d22d8-118">Возможные значения: `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="d22d8-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="d22d8-119">globalPackagesFolder (проекты, использующие только PackageReference)</span><span class="sxs-lookup"><span data-stu-id="d22d8-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="d22d8-120">Расположение глобальной папки пакетов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d22d8-120">The location of the default global packages folder.</span></span> <span data-ttu-id="d22d8-121">Значение по умолчанию — `%userprofile%\.nuget\packages` (Windows) или `~/.nuget/packages` (Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="d22d8-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="d22d8-122">В файлах `nuget.config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="d22d8-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="d22d8-123">Этот параметр переопределяется `NUGET_PACKAGES` переменной среды, которая имеет приоритет.</span><span class="sxs-lookup"><span data-stu-id="d22d8-123">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="d22d8-124">repositoryPath (только `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="d22d8-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="d22d8-125">Расположение, в котором следует установить пакеты NuGet вместо папки `$(Solutiondir)/packages` по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d22d8-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="d22d8-126">В файлах `nuget.config` для конкретных проектов можно использовать относительный путь.</span><span class="sxs-lookup"><span data-stu-id="d22d8-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="d22d8-127">Этот параметр переопределяется `NUGET_PACKAGES` переменной среды, которая имеет приоритет.</span><span class="sxs-lookup"><span data-stu-id="d22d8-127">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="d22d8-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="d22d8-128">defaultPushSource</span></span> | <span data-ttu-id="d22d8-129">Определяет URL-адрес источника пакета или путь к нему, который следует использовать по умолчанию, если другие источники пакета для операции не обнаружены.</span><span class="sxs-lookup"><span data-stu-id="d22d8-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="d22d8-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="d22d8-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="d22d8-131">Параметры прокси-сервера, которые следует использовать при подключении к источникам пакета; значение `http_proxy` должно иметь формат `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="d22d8-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="d22d8-132">Пароли зашифровываются, и их нельзя добавить вручную.</span><span class="sxs-lookup"><span data-stu-id="d22d8-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="d22d8-133">Значение параметра `no_proxy` представляет собой разделенный запятыми список доменов, для которых производится обход прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="d22d8-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="d22d8-134">В качестве этих значений можно также использовать переменные среды http_proxy и no_proxy.</span><span class="sxs-lookup"><span data-stu-id="d22d8-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="d22d8-135">Дополнительные сведения см. в записи блога [Параметры прокси-сервера в NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="d22d8-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="d22d8-136">сигнатуревалидатионмоде</span><span class="sxs-lookup"><span data-stu-id="d22d8-136">signatureValidationMode</span></span> | <span data-ttu-id="d22d8-137">Указывает режим проверки, используемый для проверки сигнатур пакетов при установке пакета и восстановления.</span><span class="sxs-lookup"><span data-stu-id="d22d8-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="d22d8-138">Значения: `accept` , `require` .</span><span class="sxs-lookup"><span data-stu-id="d22d8-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="d22d8-139">По умолчанию — `accept`.</span><span class="sxs-lookup"><span data-stu-id="d22d8-139">Defaults to `accept`.</span></span>

<span data-ttu-id="d22d8-140">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="d22d8-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="d22d8-141">Раздел bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="d22d8-141">bindingRedirects section</span></span>

<span data-ttu-id="d22d8-142">Определяет то, производится ли в NuGet автоматическая переадресация привязок при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="d22d8-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="d22d8-143">Ключ</span><span class="sxs-lookup"><span data-stu-id="d22d8-143">Key</span></span> | <span data-ttu-id="d22d8-144">Значение</span><span class="sxs-lookup"><span data-stu-id="d22d8-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d22d8-145">skip</span><span class="sxs-lookup"><span data-stu-id="d22d8-145">skip</span></span> | <span data-ttu-id="d22d8-146">Логическое значение, указывающее, следует ли пропустить автоматическую переадресацию привязок.</span><span class="sxs-lookup"><span data-stu-id="d22d8-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="d22d8-147">Значение по умолчанию – false.</span><span class="sxs-lookup"><span data-stu-id="d22d8-147">The default is false.</span></span> |

<span data-ttu-id="d22d8-148">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="d22d8-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="d22d8-149">Раздел packageRestore</span><span class="sxs-lookup"><span data-stu-id="d22d8-149">packageRestore section</span></span>

<span data-ttu-id="d22d8-150">Управляет восстановлением пакета во время сборки.</span><span class="sxs-lookup"><span data-stu-id="d22d8-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="d22d8-151">Ключ</span><span class="sxs-lookup"><span data-stu-id="d22d8-151">Key</span></span> | <span data-ttu-id="d22d8-152">Значение</span><span class="sxs-lookup"><span data-stu-id="d22d8-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d22d8-153">Включено</span><span class="sxs-lookup"><span data-stu-id="d22d8-153">enabled</span></span> | <span data-ttu-id="d22d8-154">Логическое значение, указывающее, может ли NuGet выполнять автоматическое восстановление.</span><span class="sxs-lookup"><span data-stu-id="d22d8-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="d22d8-155">Вы также можете задать переменную среды `EnableNuGetPackageRestore` со значением `True` вместо того, чтобы задавать этот параметр в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d22d8-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="d22d8-156">automatic</span><span class="sxs-lookup"><span data-stu-id="d22d8-156">automatic</span></span> | <span data-ttu-id="d22d8-157">Логическое значение, указывающее, должен ли диспетчер NuGet проверять отсутствие пакетов во время сборки.</span><span class="sxs-lookup"><span data-stu-id="d22d8-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="d22d8-158">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="d22d8-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="d22d8-159">Раздел solution</span><span class="sxs-lookup"><span data-stu-id="d22d8-159">solution section</span></span>

<span data-ttu-id="d22d8-160">Определяет то, включается ли папка `packages` решения в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="d22d8-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="d22d8-161">Этот раздел работает только в файлах `nuget.config` в папке решения.</span><span class="sxs-lookup"><span data-stu-id="d22d8-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="d22d8-162">Ключ</span><span class="sxs-lookup"><span data-stu-id="d22d8-162">Key</span></span> | <span data-ttu-id="d22d8-163">Значение</span><span class="sxs-lookup"><span data-stu-id="d22d8-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d22d8-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="d22d8-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="d22d8-165">Логическое значение, указывающее, следует ли игнорировать папку пакетов при работе с системой управления версиями.</span><span class="sxs-lookup"><span data-stu-id="d22d8-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="d22d8-166">Значением по умолчанию является false.</span><span class="sxs-lookup"><span data-stu-id="d22d8-166">The default value is false.</span></span> |

<span data-ttu-id="d22d8-167">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="d22d8-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="d22d8-168">Разделы источников пакета</span><span class="sxs-lookup"><span data-stu-id="d22d8-168">Package source sections</span></span>

<span data-ttu-id="d22d8-169">`packageSources`Параметры, `packageSourceCredentials` , `apikeys` , `activePackageSource` `disabledPackageSources` и совместно используются `trustedSigners` для настройки способа работы NuGet с репозиториями пакетов во время операций установки, восстановления и обновления.</span><span class="sxs-lookup"><span data-stu-id="d22d8-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="d22d8-170">[ `nuget sources` Команда](../reference/cli-reference/cli-ref-sources.md) обычно используется для управления этими параметрами, за исключением того, `apikeys` что управляется с помощью [ `nuget setapikey` команды](../reference/cli-reference/cli-ref-setapikey.md)и `trustedSigners` управляется с помощью [ `nuget trusted-signers` команды](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="d22d8-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="d22d8-171">Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="d22d8-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="d22d8-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="d22d8-172">packageSources</span></span>

<span data-ttu-id="d22d8-173">Выводит список всех известных источников пакетов.</span><span class="sxs-lookup"><span data-stu-id="d22d8-173">Lists all known package sources.</span></span> <span data-ttu-id="d22d8-174">Порядок пропускается во время операций восстановления и с любым проектом, использующим формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d22d8-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="d22d8-175">NuGet учитывает порядок источников для операций установки и обновления с проектами с помощью `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="d22d8-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="d22d8-176">Ключ</span><span class="sxs-lookup"><span data-stu-id="d22d8-176">Key</span></span> | <span data-ttu-id="d22d8-177">Значение</span><span class="sxs-lookup"><span data-stu-id="d22d8-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d22d8-178">(имя, назначаемое источнику пакета)</span><span class="sxs-lookup"><span data-stu-id="d22d8-178">(name to assign to the package source)</span></span> | <span data-ttu-id="d22d8-179">Путь к источнику пакета или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="d22d8-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="d22d8-180">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="d22d8-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="d22d8-181">Если для заданного узла указан параметр `<clear />`, NuGet игнорирует ранее определенные значения конфигурации для этого узла.</span><span class="sxs-lookup"><span data-stu-id="d22d8-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="d22d8-182">[Узнайте больше о применении параметров](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="d22d8-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="d22d8-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="d22d8-183">packageSourceCredentials</span></span>

<span data-ttu-id="d22d8-184">Содержит имена пользователей и пароли источников, которые, как правило, задаются с помощью параметров `-username` и `-password` команды `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="d22d8-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="d22d8-185">По умолчанию пароли зашифровываются, если также не указан параметр `-storepasswordincleartext`.</span><span class="sxs-lookup"><span data-stu-id="d22d8-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>
<span data-ttu-id="d22d8-186">При необходимости можно указать допустимые типы проверки подлинности с помощью `-validauthenticationtypes` параметра.</span><span class="sxs-lookup"><span data-stu-id="d22d8-186">Optionally, valid authentication types can be specified with the `-validauthenticationtypes` switch.</span></span>

| <span data-ttu-id="d22d8-187">Ключ</span><span class="sxs-lookup"><span data-stu-id="d22d8-187">Key</span></span> | <span data-ttu-id="d22d8-188">Значение</span><span class="sxs-lookup"><span data-stu-id="d22d8-188">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d22d8-189">username</span><span class="sxs-lookup"><span data-stu-id="d22d8-189">username</span></span> | <span data-ttu-id="d22d8-190">Имя пользователя источника в виде обычного текста.</span><span class="sxs-lookup"><span data-stu-id="d22d8-190">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="d22d8-191">password</span><span class="sxs-lookup"><span data-stu-id="d22d8-191">password</span></span> | <span data-ttu-id="d22d8-192">Зашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="d22d8-192">The encrypted password for the source.</span></span> <span data-ttu-id="d22d8-193">Зашифрованные пароли поддерживаются только в Windows и могут быть расшифрованы только при использовании на том же компьютере и с помощью того же пользователя, что и исходное шифрование.</span><span class="sxs-lookup"><span data-stu-id="d22d8-193">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="d22d8-194">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="d22d8-194">cleartextpassword</span></span> | <span data-ttu-id="d22d8-195">Незашифрованный пароль источника.</span><span class="sxs-lookup"><span data-stu-id="d22d8-195">The unencrypted password for the source.</span></span> <span data-ttu-id="d22d8-196">Примечание. переменные среды можно использовать для повышения безопасности.</span><span class="sxs-lookup"><span data-stu-id="d22d8-196">Note: environment variables can be used for improved security.</span></span> |
| <span data-ttu-id="d22d8-197">валидаусентикатионтипес</span><span class="sxs-lookup"><span data-stu-id="d22d8-197">validauthenticationtypes</span></span> | <span data-ttu-id="d22d8-198">Разделенный запятыми список допустимых типов проверки подлинности для этого источника.</span><span class="sxs-lookup"><span data-stu-id="d22d8-198">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="d22d8-199">Задайте значение `basic`, если сервер объявляет NTLM или Negotiate. Ваши учетные данные следует отправлять с помощью базового механизма, например, при использовании PAT с локальным Azure DevOps Server.</span><span class="sxs-lookup"><span data-stu-id="d22d8-199">Set this to `basic` if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server.</span></span> <span data-ttu-id="d22d8-200">К другим допустимым значениям относятся `negotiate`, `kerberos`, `ntlm` и `digest`, но они вряд ли будут полезны.</span><span class="sxs-lookup"><span data-stu-id="d22d8-200">Other valid values include `negotiate`, `kerberos`, `ntlm`, and `digest`, but these values are unlikely to be useful.</span></span> |

<span data-ttu-id="d22d8-201">**Пример.**</span><span class="sxs-lookup"><span data-stu-id="d22d8-201">**Example:**</span></span>

<span data-ttu-id="d22d8-202">В файле конфигурации элемент `<packageSourceCredentials>` содержит дочерние узлы для каждого применимого имени источника (пробелы в имени заменяются на `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="d22d8-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="d22d8-203">То есть для источников с именами Contoso и Test Source файл конфигурации содержит следующие значения при использовании зашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="d22d8-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="d22d8-204">При использовании незашифрованных паролей, хранящихся в переменной среды:</span><span class="sxs-lookup"><span data-stu-id="d22d8-204">When using unencrypted passwords stored in an environment variable:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="d22d8-205">При использовании незашифрованных паролей:</span><span class="sxs-lookup"><span data-stu-id="d22d8-205">When using unencrypted passwords:</span></span>

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

<span data-ttu-id="d22d8-206">Кроме того, можно указать допустимые методы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d22d8-206">Additionally, valid authentication methods can be supplied:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="d22d8-207">apikeys</span><span class="sxs-lookup"><span data-stu-id="d22d8-207">apikeys</span></span>

<span data-ttu-id="d22d8-208">Хранит ключи для источников, использующих проверку подлинности ключа API, как задано с помощью [ `nuget setapikey` команды](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="d22d8-208">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="d22d8-209">Ключ</span><span class="sxs-lookup"><span data-stu-id="d22d8-209">Key</span></span> | <span data-ttu-id="d22d8-210">Значение</span><span class="sxs-lookup"><span data-stu-id="d22d8-210">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d22d8-211">(URL-адрес источника)</span><span class="sxs-lookup"><span data-stu-id="d22d8-211">(source URL)</span></span> | <span data-ttu-id="d22d8-212">Зашифрованный ключ API.</span><span class="sxs-lookup"><span data-stu-id="d22d8-212">The encrypted API key.</span></span> |

<span data-ttu-id="d22d8-213">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="d22d8-213">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="d22d8-214">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="d22d8-214">disabledPackageSources</span></span>

<span data-ttu-id="d22d8-215">Определяет источники, отключенные в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="d22d8-215">Identified currently disabled sources.</span></span> <span data-ttu-id="d22d8-216">Значение может быть пустым.</span><span class="sxs-lookup"><span data-stu-id="d22d8-216">May be empty.</span></span>

| <span data-ttu-id="d22d8-217">Ключ</span><span class="sxs-lookup"><span data-stu-id="d22d8-217">Key</span></span> | <span data-ttu-id="d22d8-218">Значение</span><span class="sxs-lookup"><span data-stu-id="d22d8-218">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d22d8-219">(имя источника)</span><span class="sxs-lookup"><span data-stu-id="d22d8-219">(name of source)</span></span> | <span data-ttu-id="d22d8-220">Логическое значение, указывающее, отключен ли источник.</span><span class="sxs-lookup"><span data-stu-id="d22d8-220">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="d22d8-221">**Пример.**</span><span class="sxs-lookup"><span data-stu-id="d22d8-221">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="d22d8-222">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="d22d8-222">activePackageSource</span></span>

<span data-ttu-id="d22d8-223">*(Только в версиях 2.x; в версиях 3.x и более поздних является нерекомендуемым)*</span><span class="sxs-lookup"><span data-stu-id="d22d8-223">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="d22d8-224">Определяет текущий активный источник или указывает совокупность всех источников.</span><span class="sxs-lookup"><span data-stu-id="d22d8-224">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="d22d8-225">Ключ</span><span class="sxs-lookup"><span data-stu-id="d22d8-225">Key</span></span> | <span data-ttu-id="d22d8-226">Значение</span><span class="sxs-lookup"><span data-stu-id="d22d8-226">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d22d8-227">(имя источника) или `All`</span><span class="sxs-lookup"><span data-stu-id="d22d8-227">(name of source) or `All`</span></span> | <span data-ttu-id="d22d8-228">Если ключ представляет имя источника, значением является путь к источнику или его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="d22d8-228">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="d22d8-229">Если используется ключ `All`, требуется значение `(Aggregate source)`, объединяющее все источники пакетов, которые не отключены.</span><span class="sxs-lookup"><span data-stu-id="d22d8-229">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="d22d8-230">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="d22d8-230">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="d22d8-231">раздел Трустедсигнерс</span><span class="sxs-lookup"><span data-stu-id="d22d8-231">trustedSigners section</span></span>

<span data-ttu-id="d22d8-232">Хранит доверенные подписывающих, используемые для разрешения пакета во время установки или восстановления.</span><span class="sxs-lookup"><span data-stu-id="d22d8-232">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="d22d8-233">Этот список не может быть пустым, если пользователь задает `signatureValidationMode` значение `require` .</span><span class="sxs-lookup"><span data-stu-id="d22d8-233">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="d22d8-234">Этот раздел можно обновить с помощью [ `nuget trusted-signers` команды](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="d22d8-234">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="d22d8-235">**Схема**:</span><span class="sxs-lookup"><span data-stu-id="d22d8-235">**Schema**:</span></span>

<span data-ttu-id="d22d8-236">Доверенный подписывающий имеет коллекцию `certificate` элементов, которые закрепляют все сертификаты, которые обозначают данного подписавший.</span><span class="sxs-lookup"><span data-stu-id="d22d8-236">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="d22d8-237">Доверенный подписывающий может быть либо `Author` `Repository` .</span><span class="sxs-lookup"><span data-stu-id="d22d8-237">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="d22d8-238">В доверенном *репозитории* также указывается `serviceIndex` для репозитория (который должен быть допустимым `https` URI) и при необходимости может указывать список разделенных точкой с запятой списка `owners` для ограничения еще большего числа пользователей, которым доверяет этот конкретный репозиторий.</span><span class="sxs-lookup"><span data-stu-id="d22d8-238">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="d22d8-239">Поддерживаемые алгоритмы хэширования, используемые для отпечатка сертификата, — это `SHA256` , `SHA384` и `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="d22d8-239">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="d22d8-240">Значение, если `certificate` указывает, `allowUntrustedRoot` что `true` данный сертификат может быть связан с недоверенным корнем при построении цепочки сертификатов в ходе проверки подписи.</span><span class="sxs-lookup"><span data-stu-id="d22d8-240">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="d22d8-241">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="d22d8-241">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="d22d8-242">раздел Фаллбаккпаккажефолдерс</span><span class="sxs-lookup"><span data-stu-id="d22d8-242">fallbackPackageFolders section</span></span>

<span data-ttu-id="d22d8-243">*(3.5 +)* Предоставляет способ предварительной установки пакетов, чтобы не выполнять никаких действий, если пакет найден в резервных папках.</span><span class="sxs-lookup"><span data-stu-id="d22d8-243">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="d22d8-244">Папки с резервными пакетами имеют точно такую же структуру файлов, как и папка глобального пакета: *. nupkg* существует, и все файлы извлекаются.</span><span class="sxs-lookup"><span data-stu-id="d22d8-244">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="d22d8-245">Логика поиска для этой конфигурации:</span><span class="sxs-lookup"><span data-stu-id="d22d8-245">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="d22d8-246">Найдите папку Global Package, чтобы узнать, не скачан ли уже пакет или версия.</span><span class="sxs-lookup"><span data-stu-id="d22d8-246">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="d22d8-247">Найдите в папках резервные папки, соответствующие пакету или версии.</span><span class="sxs-lookup"><span data-stu-id="d22d8-247">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="d22d8-248">Если поиск выполнен успешно, загрузка не требуется.</span><span class="sxs-lookup"><span data-stu-id="d22d8-248">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="d22d8-249">Если совпадение не найдено, NuGet проверяет источники файлов, а затем HTTP-источники, а затем загружает пакеты.</span><span class="sxs-lookup"><span data-stu-id="d22d8-249">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="d22d8-250">Ключ</span><span class="sxs-lookup"><span data-stu-id="d22d8-250">Key</span></span> | <span data-ttu-id="d22d8-251">Значение</span><span class="sxs-lookup"><span data-stu-id="d22d8-251">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d22d8-252">(имя резервной папки)</span><span class="sxs-lookup"><span data-stu-id="d22d8-252">(name of fallback folder)</span></span> | <span data-ttu-id="d22d8-253">Путь к резервной папке.</span><span class="sxs-lookup"><span data-stu-id="d22d8-253">Path to fallback folder.</span></span> |

<span data-ttu-id="d22d8-254">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="d22d8-254">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="d22d8-255">раздел packageManagement</span><span class="sxs-lookup"><span data-stu-id="d22d8-255">packageManagement section</span></span>

<span data-ttu-id="d22d8-256">Задает формат управления пакетами по умолчанию: *packages.config* или PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d22d8-256">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="d22d8-257">Проекты в стиле SDK всегда используют PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d22d8-257">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="d22d8-258">Ключ</span><span class="sxs-lookup"><span data-stu-id="d22d8-258">Key</span></span> | <span data-ttu-id="d22d8-259">Значение</span><span class="sxs-lookup"><span data-stu-id="d22d8-259">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d22d8-260">format</span><span class="sxs-lookup"><span data-stu-id="d22d8-260">format</span></span> | <span data-ttu-id="d22d8-261">Логическое значение, указывающее формат управления пакетами по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d22d8-261">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="d22d8-262">Если `1` значение равно, то используется формат PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d22d8-262">If `1`, format is PackageReference.</span></span> <span data-ttu-id="d22d8-263">Если `0` значение, то используется формат *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="d22d8-263">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="d22d8-264">disabled</span><span class="sxs-lookup"><span data-stu-id="d22d8-264">disabled</span></span> | <span data-ttu-id="d22d8-265">Логическое значение, указывающее, следует ли отображать запрос на выбор формата пакета по умолчанию при первом установке пакета.</span><span class="sxs-lookup"><span data-stu-id="d22d8-265">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="d22d8-266">`False` скрывает запрос.</span><span class="sxs-lookup"><span data-stu-id="d22d8-266">`False` hides the prompt.</span></span> |

<span data-ttu-id="d22d8-267">**Пример**:</span><span class="sxs-lookup"><span data-stu-id="d22d8-267">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="d22d8-268">Использование переменных среды</span><span class="sxs-lookup"><span data-stu-id="d22d8-268">Using environment variables</span></span>

<span data-ttu-id="d22d8-269">В значениях `nuget.config` можно использовать переменные среды (в NuGet 3.4 и более поздних версиях) для применения параметров во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="d22d8-269">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="d22d8-270">Например, если переменная среды `HOME` в Windows имеет значение `c:\users\username`, значение параметра `%HOME%\NuGetRepository` в файле конфигурации разрешается в `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="d22d8-270">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="d22d8-271">Обратите внимание, что необходимо использовать переменные среды в стиле Windows (начинается и заканчивается на%) даже в Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="d22d8-271">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="d22d8-272">Наличие `$HOME/NuGetRepository` в файле конфигурации не будет разрешено.</span><span class="sxs-lookup"><span data-stu-id="d22d8-272">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="d22d8-273">В Mac/Linux значение `%HOME%/NuGetRepository` будет разрешаться в `/home/myStuff/NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="d22d8-273">On Mac/Linux the value of `%HOME%/NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="d22d8-274">Если переменная среды не найдена, NuGet использует буквальное значение из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d22d8-274">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span> <span data-ttu-id="d22d8-275">Например `%MY_UNDEFINED_VAR%/NuGetRepository` , будет разрешен как `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span><span class="sxs-lookup"><span data-stu-id="d22d8-275">For example `%MY_UNDEFINED_VAR%/NuGetRepository` will be resolved as `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span></span>

<span data-ttu-id="d22d8-276">В следующей таблице показан синтаксис среде Variable и разделитель пути для файлов NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="d22d8-276">The table below show environnment variable syntax and path separator support for NuGet.Config files.</span></span>

### <a name="nugetconfig-environment-variable-support"></a><span data-ttu-id="d22d8-277">Поддержка переменной среды NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="d22d8-277">NuGet.Config environment variable support</span></span>

| <span data-ttu-id="d22d8-278">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="d22d8-278">Syntax</span></span> | <span data-ttu-id="d22d8-279">Разделитель папок</span><span class="sxs-lookup"><span data-stu-id="d22d8-279">Dir separator</span></span> | <span data-ttu-id="d22d8-280">nuget.exe Windows</span><span class="sxs-lookup"><span data-stu-id="d22d8-280">Windows nuget.exe</span></span> | <span data-ttu-id="d22d8-281">dotnet.exe Windows</span><span class="sxs-lookup"><span data-stu-id="d22d8-281">Windows dotnet.exe</span></span> | <span data-ttu-id="d22d8-282">nuget.exe Mac (в Mono)</span><span class="sxs-lookup"><span data-stu-id="d22d8-282">Mac nuget.exe (in Mono)</span></span> | <span data-ttu-id="d22d8-283">dotnet.exe Mac</span><span class="sxs-lookup"><span data-stu-id="d22d8-283">Mac dotnet.exe</span></span> |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | <span data-ttu-id="d22d8-284">Да</span><span class="sxs-lookup"><span data-stu-id="d22d8-284">Yes</span></span> | <span data-ttu-id="d22d8-285">Да</span><span class="sxs-lookup"><span data-stu-id="d22d8-285">Yes</span></span> | <span data-ttu-id="d22d8-286">Да</span><span class="sxs-lookup"><span data-stu-id="d22d8-286">Yes</span></span> | <span data-ttu-id="d22d8-287">Да</span><span class="sxs-lookup"><span data-stu-id="d22d8-287">Yes</span></span> |
| `%MY_VAR%` | `\`  | <span data-ttu-id="d22d8-288">Да</span><span class="sxs-lookup"><span data-stu-id="d22d8-288">Yes</span></span> | <span data-ttu-id="d22d8-289">Да</span><span class="sxs-lookup"><span data-stu-id="d22d8-289">Yes</span></span> | <span data-ttu-id="d22d8-290">Нет</span><span class="sxs-lookup"><span data-stu-id="d22d8-290">No</span></span> | <span data-ttu-id="d22d8-291">Нет</span><span class="sxs-lookup"><span data-stu-id="d22d8-291">No</span></span> |
| `$MY_VAR` | `/`  | <span data-ttu-id="d22d8-292">Нет</span><span class="sxs-lookup"><span data-stu-id="d22d8-292">No</span></span> | <span data-ttu-id="d22d8-293">Нет</span><span class="sxs-lookup"><span data-stu-id="d22d8-293">No</span></span> | <span data-ttu-id="d22d8-294">Нет</span><span class="sxs-lookup"><span data-stu-id="d22d8-294">No</span></span> | <span data-ttu-id="d22d8-295">Нет</span><span class="sxs-lookup"><span data-stu-id="d22d8-295">No</span></span> |
| `$MY_VAR` | `\`  | <span data-ttu-id="d22d8-296">Нет</span><span class="sxs-lookup"><span data-stu-id="d22d8-296">No</span></span> | <span data-ttu-id="d22d8-297">Нет</span><span class="sxs-lookup"><span data-stu-id="d22d8-297">No</span></span> | <span data-ttu-id="d22d8-298">Нет</span><span class="sxs-lookup"><span data-stu-id="d22d8-298">No</span></span> | <span data-ttu-id="d22d8-299">Нет</span><span class="sxs-lookup"><span data-stu-id="d22d8-299">No</span></span> |


## <a name="example-config-file"></a><span data-ttu-id="d22d8-300">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="d22d8-300">Example config file</span></span>

<span data-ttu-id="d22d8-301">Ниже приведен пример `nuget.config` файла, иллюстрирующий ряд параметров, включая дополнительные.</span><span class="sxs-lookup"><span data-stu-id="d22d8-301">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
