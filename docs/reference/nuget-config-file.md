---
title: Ссылка на файл nuget.config
description: Справочник по файлу NuGet.Config, включая разделы config, bindingRedirects, packageRestore, solution и packageSource.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: afc06c81bf0344f2086efd19111cc60d24d7f723
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859516"
---
# <a name="nugetconfig-reference"></a>Справочник по nuget.config

Поведение NuGet управляется параметрами в различных `NuGet.Config` файлах или `nuget.config` , как описано в разделе [Общие конфигурации NuGet](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` — это XML-файл, содержащий узел `<configuration>` верхнего уровня, который, в свою очередь, содержит элементы разделов, описываемые в этой статье. Каждый раздел содержит ноль или более элементов. См. [пример файла конфигурации](#example-config-file). В именах регистр символов не учитывается, а в качестве значений могут использоваться [переменные среды](#using-environment-variables).

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Раздел config

Содержит прочие параметры конфигурации, которые можно задать с помощью [ `nuget config` команды](../reference/cli-reference/cli-ref-config.md).

`dependencyVersion` и `repositoryPath` применяются только к проектам с помощью `packages.config` . `globalPackagesFolder` применяется только к проектам, использующим формат PackageReference.

| Ключ | Значение |
| --- | --- |
| dependencyVersion (только `packages.config`) | Значение `DependencyVersion` по умолчанию для установки, восстановления и обновления пакета, если параметр `-DependencyVersion` не указан напрямую. Это значение также используется в пользовательском интерфейсе диспетчера пакетов NuGet. Возможные значения: `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (проекты, использующие только PackageReference) | Расположение глобальной папки пакетов по умолчанию. Значение по умолчанию — `%userprofile%\.nuget\packages` (Windows) или `~/.nuget/packages` (Mac и Linux). В файлах `nuget.config` для конкретных проектов можно использовать относительный путь. Этот параметр переопределяется `NUGET_PACKAGES` переменной среды, которая имеет приоритет. |
| repositoryPath (только `packages.config`) | Расположение, в котором следует установить пакеты NuGet вместо папки `$(Solutiondir)/packages` по умолчанию. В файлах `nuget.config` для конкретных проектов можно использовать относительный путь. Этот параметр переопределяется `NUGET_PACKAGES` переменной среды, которая имеет приоритет. |
| defaultPushSource | Определяет URL-адрес источника пакета или путь к нему, который следует использовать по умолчанию, если другие источники пакета для операции не обнаружены. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Параметры прокси-сервера, которые следует использовать при подключении к источникам пакета; значение `http_proxy` должно иметь формат `http://<username>:<password>@<domain>`. Пароли зашифровываются, и их нельзя добавить вручную. Значение параметра `no_proxy` представляет собой разделенный запятыми список доменов, для которых производится обход прокси-сервера. В качестве этих значений можно также использовать переменные среды http_proxy и no_proxy. Дополнительные сведения см. в записи блога [Параметры прокси-сервера в NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| сигнатуревалидатионмоде | Указывает режим проверки, используемый для проверки сигнатур пакетов при установке пакета и восстановления. Значения: `accept` , `require` . По умолчанию — `accept`.

**Пример**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a>Раздел bindingRedirects

Определяет то, производится ли в NuGet автоматическая переадресация привязок при установке пакета.

| Ключ | Значение |
| --- | --- |
| skip | Логическое значение, указывающее, следует ли пропустить автоматическую переадресацию привязок. Значение по умолчанию – false. |

**Пример**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Раздел packageRestore

Управляет восстановлением пакета во время сборки.

| Ключ | Значение |
| --- | --- |
| Включено | Логическое значение, указывающее, может ли NuGet выполнять автоматическое восстановление. Вы также можете задать переменную среды `EnableNuGetPackageRestore` со значением `True` вместо того, чтобы задавать этот параметр в файле конфигурации. |
| automatic | Логическое значение, указывающее, должен ли диспетчер NuGet проверять отсутствие пакетов во время сборки. |

**Пример**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Раздел solution

Определяет то, включается ли папка `packages` решения в систему управления версиями. Этот раздел работает только в файлах `nuget.config` в папке решения.

| Ключ | Значение |
| --- | --- |
| disableSourceControlIntegration | Логическое значение, указывающее, следует ли игнорировать папку пакетов при работе с системой управления версиями. Значением по умолчанию является false. |

**Пример**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Разделы источников пакета

`packageSources`Параметры, `packageSourceCredentials` , `apikeys` , `activePackageSource` `disabledPackageSources` и совместно используются `trustedSigners` для настройки способа работы NuGet с репозиториями пакетов во время операций установки, восстановления и обновления.

[ `nuget sources` Команда](../reference/cli-reference/cli-ref-sources.md) обычно используется для управления этими параметрами, за исключением того, `apikeys` что управляется с помощью [ `nuget setapikey` команды](../reference/cli-reference/cli-ref-setapikey.md)и `trustedSigners` управляется с помощью [ `nuget trusted-signers` команды](../reference/cli-reference/cli-ref-trusted-signers.md).

Обратите внимание, что URL-адрес источника для nuget.org — `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Выводит список всех известных источников пакетов. Порядок пропускается во время операций восстановления и с любым проектом, использующим формат PackageReference. NuGet учитывает порядок источников для операций установки и обновления с проектами с помощью `packages.config` .

| Ключ | Значение |
| --- | --- |
| (имя, назначаемое источнику пакета) | Путь к источнику пакета или его URL-адрес. |

**Пример**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> Если для заданного узла указан параметр `<clear />`, NuGet игнорирует ранее определенные значения конфигурации для этого узла. [Узнайте больше о применении параметров](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Содержит имена пользователей и пароли источников, которые, как правило, задаются с помощью параметров `-username` и `-password` команды `nuget sources`. По умолчанию пароли зашифровываются, если также не указан параметр `-storepasswordincleartext`.
При необходимости можно указать допустимые типы проверки подлинности с помощью `-validauthenticationtypes` параметра.

| Ключ | Значение |
| --- | --- |
| username | Имя пользователя источника в виде обычного текста. |
| password | Зашифрованный пароль источника. Зашифрованные пароли поддерживаются только в Windows и могут быть расшифрованы только при использовании на том же компьютере и с помощью того же пользователя, что и исходное шифрование. |
| cleartextpassword | Незашифрованный пароль источника. Примечание. переменные среды можно использовать для повышения безопасности. |
| валидаусентикатионтипес | Разделенный запятыми список допустимых типов проверки подлинности для этого источника. Задайте значение `basic`, если сервер объявляет NTLM или Negotiate. Ваши учетные данные следует отправлять с помощью базового механизма, например, при использовании PAT с локальным Azure DevOps Server. К другим допустимым значениям относятся `negotiate`, `kerberos`, `ntlm` и `digest`, но они вряд ли будут полезны. |

**Пример**.

В файле конфигурации элемент `<packageSourceCredentials>` содержит дочерние узлы для каждого применимого имени источника (пробелы в имени заменяются на `_x0020_`). То есть для источников с именами Contoso и Test Source файл конфигурации содержит следующие значения при использовании зашифрованных паролей:

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

При использовании незашифрованных паролей, хранящихся в переменной среды:

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

При использовании незашифрованных паролей:

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

Кроме того, можно указать допустимые методы проверки подлинности.

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

### <a name="apikeys"></a>apikeys

Хранит ключи для источников, использующих проверку подлинности ключа API, как задано с помощью [ `nuget setapikey` команды](../reference/cli-reference/cli-ref-setapikey.md).

| Ключ | Значение |
| --- | --- |
| (URL-адрес источника) | Зашифрованный ключ API. |

**Пример**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Определяет источники, отключенные в настоящее время. Значение может быть пустым.

| Ключ | Значение |
| --- | --- |
| (имя источника) | Логическое значение, указывающее, отключен ли источник. |

**Пример**.

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(Только в версиях 2.x; в версиях 3.x и более поздних является нерекомендуемым)*

Определяет текущий активный источник или указывает совокупность всех источников.

| Ключ | Значение |
| --- | --- |
| (имя источника) или `All` | Если ключ представляет имя источника, значением является путь к источнику или его URL-адрес. Если используется ключ `All`, требуется значение `(Aggregate source)`, объединяющее все источники пакетов, которые не отключены. |

**Пример**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a>раздел Трустедсигнерс

Хранит доверенные подписывающих, используемые для разрешения пакета во время установки или восстановления. Этот список не может быть пустым, если пользователь задает `signatureValidationMode` значение `require` . 

Этот раздел можно обновить с помощью [ `nuget trusted-signers` команды](../reference/cli-reference/cli-ref-trusted-signers.md).

**Схема**:

Доверенный подписывающий имеет коллекцию `certificate` элементов, которые закрепляют все сертификаты, которые обозначают данного подписавший. Доверенный подписывающий может быть либо `Author` `Repository` .

В доверенном *репозитории* также указывается `serviceIndex` для репозитория (который должен быть допустимым `https` URI) и при необходимости может указывать список разделенных точкой с запятой списка `owners` для ограничения еще большего числа пользователей, которым доверяет этот конкретный репозиторий.

Поддерживаемые алгоритмы хэширования, используемые для отпечатка сертификата, — это `SHA256` , `SHA384` и `SHA512` .

Значение, если `certificate` указывает, `allowUntrustedRoot` что `true` данный сертификат может быть связан с недоверенным корнем при построении цепочки сертификатов в ходе проверки подписи.

**Пример**:

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a>раздел Фаллбаккпаккажефолдерс

*(3.5 +)* Предоставляет способ предварительной установки пакетов, чтобы не выполнять никаких действий, если пакет найден в резервных папках. Папки с резервными пакетами имеют точно такую же структуру файлов, как и папка глобального пакета: *. nupkg* существует, и все файлы извлекаются.

Логика поиска для этой конфигурации:

- Найдите папку Global Package, чтобы узнать, не скачан ли уже пакет или версия.

- Найдите в папках резервные папки, соответствующие пакету или версии.

Если поиск выполнен успешно, загрузка не требуется.

Если совпадение не найдено, NuGet проверяет источники файлов, а затем HTTP-источники, а затем загружает пакеты.

| Ключ | Значение |
| --- | --- |
| (имя резервной папки) | Путь к резервной папке. |

**Пример**:

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>раздел packageManagement

Задает формат управления пакетами по умолчанию: *packages.config* или PackageReference. Проекты в стиле SDK всегда используют PackageReference.

| Ключ | Значение |
| --- | --- |
| format | Логическое значение, указывающее формат управления пакетами по умолчанию. Если `1` значение равно, то используется формат PackageReference. Если `0` значение, то используется формат *packages.config*. |
| disabled | Логическое значение, указывающее, следует ли отображать запрос на выбор формата пакета по умолчанию при первом установке пакета. `False` скрывает запрос. |

**Пример**:

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>Использование переменных среды

В значениях `nuget.config` можно использовать переменные среды (в NuGet 3.4 и более поздних версиях) для применения параметров во время выполнения.

Например, если переменная среды `HOME` в Windows имеет значение `c:\users\username`, значение параметра `%HOME%\NuGetRepository` в файле конфигурации разрешается в `c:\users\username\NuGetRepository`.

Обратите внимание, что необходимо использовать переменные среды в стиле Windows (начинается и заканчивается на%) даже в Mac/Linux. Наличие `$HOME/NuGetRepository` в файле конфигурации не будет разрешено. В Mac/Linux значение `%HOME%/NuGetRepository` будет разрешаться в `/home/myStuff/NuGetRepository` .

Если переменная среды не найдена, NuGet использует буквальное значение из файла конфигурации. Например `%MY_UNDEFINED_VAR%/NuGetRepository` , будет разрешен как `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

В следующей таблице показан синтаксис среде Variable и разделитель пути для файлов NuGet.Config.

### <a name="nugetconfig-environment-variable-support"></a>Поддержка переменной среды NuGet.Config

| Синтаксис | Разделитель папок | nuget.exe Windows | dotnet.exe Windows | nuget.exe Mac (в Mono) | dotnet.exe Mac |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | Да | Да | Да | Да |
| `%MY_VAR%` | `\`  | Да | Да | Нет | Нет |
| `$MY_VAR` | `/`  | Нет | Нет | Нет | Нет |
| `$MY_VAR` | `\`  | Нет | Нет | Нет | Нет |


## <a name="example-config-file"></a>Пример файла конфигурации

Ниже приведен пример `nuget.config` файла, иллюстрирующий ряд параметров, включая дополнительные.

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
            <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
