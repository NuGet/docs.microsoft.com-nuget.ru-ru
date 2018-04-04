---
title: Управление кэшированием пакетов в NuGet | Документы Майкрософт
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Описание управления разными кэшами пакетов NuGet, присутствующими на компьютере и используемыми при установке или восстановлении пакетов.
keywords: кэш пакета NuGet, кэширование пакетов, кэши NuGet, управление кэшами, локальный кэш NuGet, глобальный кэш NuGet, команда locals для NuGet, очистка кэша
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09b3560d67ff8a38677dd1e27d85cdf234495aae
ms.sourcegitcommit: 718e6cb88e45fa07c85d653f216bf92eaaf81625
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2018
---
# <a name="managing-the-nuget-cache"></a>Управление кэшем NuGet

NuGet использует несколько локальных кэшей, чтобы предотвратить скачивание пакетов, которые уже находятся на компьютере, а также для обеспечения поддержки вне сети. NuGet автоматически переходит обратно к кэшу при установке или переустановке пакетов без сетевого подключения.

С расположениями кэша можно работать с помощью [команды locals](../tools/cli-ref-locals.md):

```cli
nuget locals all -list
```

Типичные выходные данные выглядят следующим образом:

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

Если при установке пакета возникают неполадки или вам по иной причине требуется обеспечить установку пакетов из удаленной коллекции, используйте параметр `locals -clear`:

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

Обратите внимание, что управление кэшем сейчас поддерживается только в командной строке NuGet, но не в среде Visual Studio или консоли диспетчера пакетов. Кроме того, управление кэшем 2.x не поддерживается в NuGet 3.6 и более поздних версиях.

При использовании `nuget locals` могут возникать следующие ошибки:

- **При удалении локальных ресурсов произошел сбой: не удалось удалить один файл (или несколько)**
- **Каталог не пуст**

Эти ошибки указывают, что либо у вас нет прав на удаление файлов в кэше, либо один или несколько файлов в кэше используются другим процессом, который нужно закрыть перед удалением файлов.
