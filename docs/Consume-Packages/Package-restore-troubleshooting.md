---
title: "Устранение неполадок с восстановлением пакетов NuGet в Visual Studio | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Описание распространенных ошибок восстановления NuGet в Visual Studio и способов их устранения."
keywords: "восстановление пакетов NuGet, восстановление пакетов, устранение неполадок, устранение ошибок"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0993e2585452e3c64da28d14bb1bbe1bea27768
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="e93d9-104">Устранение ошибок при восстановлении пакетов в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e93d9-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="e93d9-105">Эта страница посвящена распространенным ошибкам, возникающим при восстановлении пакетов в Visual Studio, и мерам по их устранению.</span><span class="sxs-lookup"><span data-stu-id="e93d9-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="e93d9-106">Инструкции по восстановлению пакетов см. в разделе [Восстановление пакета](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="e93d9-106">For how-to restore packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="e93d9-107">По умолчанию при сборке проекта в Visual Studio автоматически восстанавливаются пакеты NuGet, на которые он ссылается.</span><span class="sxs-lookup"><span data-stu-id="e93d9-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="e93d9-108">Однако сборка завершится неудачей, если восстановление пакетов отключено в параметрах **Сервис > Параметры > Диспетчер пакетов NuGet > Восстановление пакетов**, а необходимые пакеты недоступны на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="e93d9-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="e93d9-109">В таких ситуациях могут возникнуть следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="e93d9-109">In these cases you may see the following errors:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

<span data-ttu-id="e93d9-110">Чтобы включить восстановление пакетов, откройте меню **Сервис > Параметры > Диспетчер пакетов NuGet** и выберите параметры **Разрешить NuGet скачивать отсутствующие пакеты** и **Автоматически проверять отсутствие пакетов при сборке в Visual Studio**:</span><span class="sxs-lookup"><span data-stu-id="e93d9-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![включение восстановления пакетов NuGet в меню "Сервис", "Параметры"](../consume-packages/media/restore-01-autorestoreoptions.png)
