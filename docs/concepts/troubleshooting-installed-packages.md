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
# <a name="troubleshooting-installed-packages"></a>Устранение неполадок с установленными пакетами

Иногда может потребоваться проверить, из какого источника был установлен определенный пакет. Ниже описано несколько способов такой проверки.

> [!Note]
> Некоторые источники пакетов поддерживают такое понятие, как вышестоящие источники. Например, [вышестоящие источники Azure Artifacts](/azure/devops/artifacts/concepts/upstream-sources). Клиенты NuGet не знают, поступил ли пакет из вышестоящего источника. Таким образом, любые журналы источника пакетов будут содержать сведения о настроенном источнике, а не о вышестоящем источнике.

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>Файл `.nupkg.metadata` в папке глобальных пакетов

При извлечении пакета в папку *global-packages* записывается файл `.nupkg.metadata`. Начиная с версии NuGet 5.9.0, NuGet будет добавлять источник пакетов. Ниже приведены сведения о сопоставлении версий NuGet с версиями пакета SDK для Visual Studio и .NET. Пример:

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> Если папка *global-packages* содержит пакеты, извлеченные перед обновлением до более новой версии средств с NuGet 5.9.0, файл `.nupkg.metadata` будет иметь версию 1 и не будет содержать источник пакетов. Можно [очистить папку *global-packages*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders), чтобы все пакеты содержали источник пакетов.

> [!Tip]
> NuGet записывает файл `.nupkg.metadata` только в папку *global-packages*. Проекты, использующие `packages.config`, обращаются к папке пакетов решений, для которой не создается файл `.nupkg.metadata`.

## <a name="installed-package-log-message"></a>Сообщение журнала установленного пакета

Начиная с версии NuGet 5.9.0, NuGet выводит сведения об источнике пакетов в сообщении о восстановлении, информирующем о том, что пакет был установлен. Пример:

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> Это сообщение выводится со стандартным или информационным уровнем детализации. Visual Studio и `dotnet` CLI по умолчанию имеют минимальный уровень детализации, поэтому это сообщение не будет отображаться по умолчанию. Средства `msbuild` и `nuget` CLI по умолчанию имеют стандартный уровень детализации, поэтому это сообщение будет отображаться по умолчанию.

## <a name="http-log-message"></a>Сообщение журнала HTTP

Если пакет недоступен локально или в папке *global-packages*, а также в резервной папке или локальном источнике файлов, NuGet скачает его из любого настроенного источника пакетов по протоколу HTTP. HTTP-запросы и ответы записываются со стандартным уровнем детализации, и вы должны увидеть только один запрос и ответ для каждой версии пакета. Пример:

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

Если файлы были недавно скачаны, их можно получить из *http-cache* в NuGet.

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

Формат URL-адреса может отличаться для разных реализаций HTTP-сервера NuGet, а также для реализации протокола HTTP NuGet версии 2 или 3.

Если для `nuget.config` определено несколько источников HTTP, вы увидите несколько запросов к файлу `index.json` каждого пакета, по одному для каждого источника. Но для каждой версии пакета будет скачан только один экземпляр `nupkg`.

## <a name="package-signature-log-message"></a>Сообщение журнала о подписи пакета

Если скачиваемый пакет подписан, NuGet проверит подпись и зарегистрирует следующее сообщение с подробным уровнем детализации:

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

Это сообщение будет информировать о том, был ли пакет скачан из источника пакетов HTTP или скопирован из локального источника пакетов. Оно не будет выводиться, если пакет уже доступен в папке *global-packages* или резервной папке.

> [!Important]
> Из-за [удаления отношения доверия с центром сертификации VeriSign](https://github.com/dotnet/announcements/issues/180) в NuGet отключена проверка подписанного пакета на определенных платформах в определенных версиях NuGet и пакета SDK для .NET. Поэтому в одних и тех же пакетах могут быть журналы `PackageSignatureVerificationLog` или эти журналы могут отсутствовать в зависимости от того, на какой платформе выполняется восстановление и какая версия .NET или NuGet используется.

## <a name="nuget-version-map"></a>Сопоставление версий NuGet

Следующие версии NuGet имеют важные изменения в отношении ведения журнала источника пакетов:

|Версия NuGet|Версия Visual Studio|Версия пакета SDK для .NET|
|---|---|---|
|NuGet 5.9.0|Visual Studio 2019 16.9.0|Пакет SDK 5.0.200 для .NET 5|
