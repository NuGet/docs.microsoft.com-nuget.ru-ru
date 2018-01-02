---
title: "Управление кэшированием пакетов в NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: "Описание управления разными кэшами пакетов NuGet, присутствующими на компьютере и используемыми при установке или восстановлении пакетов."
keywords: "кэш пакета NuGet, кэширование пакетов, кэши NuGet, управление кэшами, локальный кэш NuGet, глобальный кэш NuGet, команда locals для NuGet, очистка кэша"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="abfbd-104">Управление кэшем NuGet</span><span class="sxs-lookup"><span data-stu-id="abfbd-104">Managing the NuGet cache</span></span>

<span data-ttu-id="abfbd-105">NuGet использует несколько локальных кэшей, чтобы предотвратить скачивание пакетов, которые уже находятся на компьютере, а также для обеспечения поддержки вне сети.</span><span class="sxs-lookup"><span data-stu-id="abfbd-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="abfbd-106">NuGet 2.8+ автоматически переходит обратно к кэшу при установке или переустановке пакетов без сетевого подключения.</span><span class="sxs-lookup"><span data-stu-id="abfbd-106">NuGet 2.8+ automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="abfbd-107">С расположениями кэша можно работать с помощью [команды locals](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="abfbd-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```
nuget locals all -list
```

<span data-ttu-id="abfbd-108">Типичные выходные данные выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="abfbd-108">Typical output is as follows:</span></span>

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

<span data-ttu-id="abfbd-109">Если при установке пакета возникают неполадки или вам по иной причине требуется обеспечить установку пакетов из удаленной коллекции, используйте параметр `locals -clear`:</span><span class="sxs-lookup"><span data-stu-id="abfbd-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="abfbd-110">Обратите внимание, что управление кэшем сейчас поддерживается только в командной строке NuGet, но не в среде Visual Studio или консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="abfbd-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="abfbd-111">Кроме того, управление кэшем 2.x не поддерживается в NuGet 3.6 и более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="abfbd-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="abfbd-112">При использовании `nuget locals` могут возникать следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="abfbd-112">The following errors can occur when using `nuget locals`:</span></span>

* <span data-ttu-id="abfbd-113">**При удалении локальных ресурсов произошел сбой: не удалось удалить один файл (или несколько)**</span><span class="sxs-lookup"><span data-stu-id="abfbd-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
* <span data-ttu-id="abfbd-114">**Каталог не пуст**</span><span class="sxs-lookup"><span data-stu-id="abfbd-114">**The directory is not empty**</span></span>

<span data-ttu-id="abfbd-115">Эти ошибки указывают, что либо у вас нет прав на удаление файлов в кэше, либо один или несколько файлов в кэше используются другим процессом, который нужно закрыть перед удалением файлов.</span><span class="sxs-lookup"><span data-stu-id="abfbd-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the those files can be removed.</span></span>
