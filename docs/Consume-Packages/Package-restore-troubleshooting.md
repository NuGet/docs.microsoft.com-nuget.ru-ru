---
title: "Устранение неполадок с восстановлением пакетов NuGet в Visual Studio | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b70326a0-5bfc-4b7c-881d-7a7d5ebeeed5
description: "Описание распространенных ошибок восстановления NuGet в Visual Studio и способов их устранения."
keywords: "восстановление пакетов NuGet, восстановление пакетов, устранение неполадок, устранение ошибок"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c23a9ed2b7cffbf904018a089ccde000adaa517f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Устранение ошибок при восстановлении пакетов в Visual Studio

> [!Note]
> Эта страница посвящена распространенным ошибкам, возникающим при восстановлении пакетов в Visual Studio, и мерам по их устранению. Инструкции по восстановлению пакетов см. в разделе [Восстановление пакета](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).

По умолчанию при сборке проекта в Visual Studio автоматически восстанавливаются пакеты NuGet, на которые он ссылается. Однако сборка завершится неудачей, если восстановление пакетов отключено в параметрах **Сервис > Параметры > Диспетчер пакетов NuGet > Восстановление пакетов**, а необходимые пакеты недоступны на вашем компьютере. В таких ситуациях могут возникнуть следующие ошибки:

```
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

Чтобы включить восстановление пакетов, откройте меню **Сервис > Параметры > Диспетчер пакетов NuGet** и выберите параметры **Разрешить NuGet скачивать отсутствующие пакеты** и **Автоматически проверять отсутствие пакетов при сборке в Visual Studio**:

![включение восстановления пакетов NuGet в меню "Сервис", "Параметры"](../Consume-Packages/media/restore-01-autorestoreoptions.png)

