---
title: Устранение неполадок с установленными пакетами
description: Определение того, какой источник пакетов использовался для отдельных пакетов
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387535"
---
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="697c1-103">Устранение неполадок с установленными пакетами</span><span class="sxs-lookup"><span data-stu-id="697c1-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="697c1-104">Иногда может потребоваться проверить, из какого источника был установлен определенный пакет.</span><span class="sxs-lookup"><span data-stu-id="697c1-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="697c1-105">Ниже описано несколько способов такой проверки.</span><span class="sxs-lookup"><span data-stu-id="697c1-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="697c1-106">Некоторые источники пакетов поддерживают такое понятие, как вышестоящие источники.</span><span class="sxs-lookup"><span data-stu-id="697c1-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="697c1-107">Например, [вышестоящие источники Azure Artifacts](/azure/devops/artifacts/concepts/upstream-sources).</span><span class="sxs-lookup"><span data-stu-id="697c1-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="697c1-108">Клиенты NuGet не знают, поступил ли пакет из вышестоящего источника.</span><span class="sxs-lookup"><span data-stu-id="697c1-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="697c1-109">Таким образом, любые журналы источника пакетов будут содержать сведения о настроенном источнике, а не о вышестоящем источнике.</span><span class="sxs-lookup"><span data-stu-id="697c1-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="697c1-110">Файл `.nupkg.metadata` в папке глобальных пакетов</span><span class="sxs-lookup"><span data-stu-id="697c1-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="697c1-111">При извлечении пакета в папку *global-packages* записывается файл `.nupkg.metadata`.</span><span class="sxs-lookup"><span data-stu-id="697c1-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="697c1-112">Начиная с версии NuGet 5.9.0, NuGet будет добавлять источник пакетов.</span><span class="sxs-lookup"><span data-stu-id="697c1-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="697c1-113">Ниже приведены сведения о сопоставлении версий NuGet с версиями пакета SDK для Visual Studio и .NET.</span><span class="sxs-lookup"><span data-stu-id="697c1-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="697c1-114">Пример:</span><span class="sxs-lookup"><span data-stu-id="697c1-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="697c1-115">Если папка *global-packages* содержит пакеты, извлеченные перед обновлением до более новой версии средств с NuGet 5.9.0, файл `.nupkg.metadata` будет иметь версию 1 и не будет содержать источник пакетов.</span><span class="sxs-lookup"><span data-stu-id="697c1-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="697c1-116">Можно [очистить папку *global-packages*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders), чтобы все пакеты содержали источник пакетов.</span><span class="sxs-lookup"><span data-stu-id="697c1-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="697c1-117">NuGet записывает файл `.nupkg.metadata` только в папку *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="697c1-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="697c1-118">Проекты, использующие `packages.config`, обращаются к папке пакетов решений, для которой не создается файл `.nupkg.metadata`.</span><span class="sxs-lookup"><span data-stu-id="697c1-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="697c1-119">Сообщение журнала установленного пакета</span><span class="sxs-lookup"><span data-stu-id="697c1-119">Installed package log message</span></span>

<span data-ttu-id="697c1-120">Начиная с версии NuGet 5.9.0, NuGet выводит сведения об источнике пакетов в сообщении о восстановлении, информирующем о том, что пакет был установлен.</span><span class="sxs-lookup"><span data-stu-id="697c1-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="697c1-121">Пример:</span><span class="sxs-lookup"><span data-stu-id="697c1-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="697c1-122">Это сообщение выводится со стандартным или информационным уровнем детализации.</span><span class="sxs-lookup"><span data-stu-id="697c1-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="697c1-123">Visual Studio и `dotnet` CLI по умолчанию имеют минимальный уровень детализации, поэтому это сообщение не будет отображаться по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="697c1-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="697c1-124">Средства `msbuild` и `nuget` CLI по умолчанию имеют стандартный уровень детализации, поэтому это сообщение будет отображаться по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="697c1-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="697c1-125">Сообщение журнала HTTP</span><span class="sxs-lookup"><span data-stu-id="697c1-125">HTTP log message</span></span>

<span data-ttu-id="697c1-126">Если пакет недоступен локально или в папке *global-packages*, а также в резервной папке или локальном источнике файлов, NuGet скачает его из любого настроенного источника пакетов по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="697c1-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="697c1-127">HTTP-запросы и ответы записываются со стандартным уровнем детализации, и вы должны увидеть только один запрос и ответ для каждой версии пакета.</span><span class="sxs-lookup"><span data-stu-id="697c1-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="697c1-128">Пример:</span><span class="sxs-lookup"><span data-stu-id="697c1-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="697c1-129">Если файлы были недавно скачаны, их можно получить из *http-cache* в NuGet.</span><span class="sxs-lookup"><span data-stu-id="697c1-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="697c1-130">Формат URL-адреса может отличаться для разных реализаций HTTP-сервера NuGet, а также для реализации протокола HTTP NuGet версии 2 или 3.</span><span class="sxs-lookup"><span data-stu-id="697c1-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="697c1-131">Если для `nuget.config` определено несколько источников HTTP, вы увидите несколько запросов к файлу `index.json` каждого пакета, по одному для каждого источника.</span><span class="sxs-lookup"><span data-stu-id="697c1-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="697c1-132">Но для каждой версии пакета будет скачан только один экземпляр `nupkg`.</span><span class="sxs-lookup"><span data-stu-id="697c1-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="697c1-133">Сообщение журнала о подписи пакета</span><span class="sxs-lookup"><span data-stu-id="697c1-133">Package signature log message</span></span>

<span data-ttu-id="697c1-134">Если скачиваемый пакет подписан, NuGet проверит подпись и зарегистрирует следующее сообщение с подробным уровнем детализации:</span><span class="sxs-lookup"><span data-stu-id="697c1-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="697c1-135">Это сообщение будет информировать о том, был ли пакет скачан из источника пакетов HTTP или скопирован из локального источника пакетов.</span><span class="sxs-lookup"><span data-stu-id="697c1-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="697c1-136">Оно не будет выводиться, если пакет уже доступен в папке *global-packages* или резервной папке.</span><span class="sxs-lookup"><span data-stu-id="697c1-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="697c1-137">Из-за [удаления отношения доверия с центром сертификации VeriSign](https://github.com/dotnet/announcements/issues/180) в NuGet отключена проверка подписанного пакета на определенных платформах в определенных версиях NuGet и пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="697c1-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="697c1-138">Поэтому в одних и тех же пакетах могут быть журналы `PackageSignatureVerificationLog` или эти журналы могут отсутствовать в зависимости от того, на какой платформе выполняется восстановление и какая версия .NET или NuGet используется.</span><span class="sxs-lookup"><span data-stu-id="697c1-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="697c1-139">Сопоставление версий NuGet</span><span class="sxs-lookup"><span data-stu-id="697c1-139">NuGet Version Map</span></span>

<span data-ttu-id="697c1-140">Следующие версии NuGet имеют важные изменения в отношении ведения журнала источника пакетов:</span><span class="sxs-lookup"><span data-stu-id="697c1-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="697c1-141">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="697c1-141">NuGet Version</span></span>|<span data-ttu-id="697c1-142">Версия Visual Studio</span><span class="sxs-lookup"><span data-stu-id="697c1-142">Visual Studio Version</span></span>|<span data-ttu-id="697c1-143">Версия пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="697c1-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="697c1-144">NuGet 5.9.0</span><span class="sxs-lookup"><span data-stu-id="697c1-144">NuGet 5.9.0</span></span>|<span data-ttu-id="697c1-145">Visual Studio 2019 16.9.0</span><span class="sxs-lookup"><span data-stu-id="697c1-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="697c1-146">Пакет SDK 5.0.200 для .NET 5</span><span class="sxs-lookup"><span data-stu-id="697c1-146">.NET 5 SDK 5.0.200</span></span>|
