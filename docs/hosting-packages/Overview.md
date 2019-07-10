---
title: Общие сведения о размещении собственных веб-каналов NuGet
description: Общие сведения о локальном или удаленном размещении своих веб-каналов пакетов NuGet или коллекций.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: f05c3a7a51bdc0760097422004cfc4339bf9ee2c
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426610"
---
# <a name="hosting-your-own-nuget-feeds"></a>Размещение своих веб-каналов NuGet

Вместо того, чтобы делать пакеты общедоступными, вам может потребоваться выпустить их лишь для ограниченного круга пользователей, например вашей организации или рабочей группы. Кроме того, некоторым организациям может потребоваться ограничить доступные их разработчикам сторонние библиотеки, то есть предоставить в их распоряжение ограниченный источник пакетов, а не весь сайт nuget.org.

Для этого NuGet позволяет настроить частные источники пакетов одним из следующих способов:

- Локальный веб-канал: пакеты просто помещаются в подходящую сетевую общую папку. Оптимальнее всего для этого использовать `nuget init` и `nuget add`, чтобы создать иерархическую структуру папок (NuGet 3.3+). Дополнительные сведения см. в разделе [Локальные веб-каналы](../hosting-packages/local-feeds.md).
- NuGet.Server: пакеты предоставляются через локальный HTTP-сервер. Дополнительные сведения см. в разделе [NuGet.Server](../hosting-packages/nuget-server.md).
- Коллекция NuGet: пакеты размещаются на интернет-сервере с помощью [проекта коллекции NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). Коллекция NuGet позволяет управлять пользователями и предоставляет такие функции, как расширенный пользовательский веб-интерфейс, позволяющий искать и просматривать пакеты с помощью браузера, аналогично nuget.org.

Существует несколько других продуктов для размещения NuGet, которые поддерживают удаленные закрытые веб-каналы, включая следующие:

- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), доступные также в Team Foundation Server 2017 и более поздних версий.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) от Inedo
- [Реестр пакетов GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [Сервер NuGet](http://nugetserver.net/) — проект сообщества от Inedo
- [Сервер NuGet (открытый исходный код)](http://nuget-server.net) — реализация, аналогичная серверу NuGet от Inedo, с открытым исходным кодом
- [LiGet](https://github.com/ai-traders/liget) — реализация с открытым исходным кодом для сервера NuGet V2, на котором выполняется Kestrel в Docker
- [BaGet](https://github.com/loic-sharma/BaGet) — реализация для сервера NuGet V3 с открытым кодом на платформе ASP.NET Core
- [Sleet](https://github.com/emgarten/sleet) —статический генератор веб-канала NuGet V3 с открытым исходным кодом.
- [Artifactory](https://www.jfrog.com/artifactory/) от JFrog.
- [Nexus](http://www.sonatype.org/nexus/) от Sonatype.
- [TeamCity](https://www.jetbrains.com/teamcity/) от JetBrains.

Независимо от способа размещения пакетов доступ к ним осуществляется путем добавления их в список доступных источников в `NuGet.Config`. Это можно сделать в Visual Studio, как описано в разделе [Источники пакетов](../tools/package-manager-ui.md#package-sources), или из командной строки с помощью [`nuget sources`](../tools/cli-ref-sources.md). Путь к источнику может быть путем к локальной папке, сетевым именем или URL-адресом.
