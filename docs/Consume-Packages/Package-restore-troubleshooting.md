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
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/14/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Устранение ошибок при восстановлении пакетов в Visual Studio

> [!Note]
> Эта страница посвящена распространенным ошибкам, возникающим при восстановлении пакетов в Visual Studio, и мерам по их устранению. Инструкции по восстановлению пакетов см. в разделе [Восстановление пакета](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

По умолчанию при сборке проекта в Visual Studio автоматически восстанавливаются пакеты NuGet, на которые он ссылается. Однако сборка завершится неудачей, если восстановление пакетов отключено в параметрах **Сервис > Параметры > Диспетчер пакетов NuGet > Восстановление пакетов**, а необходимые пакеты недоступны на вашем компьютере. В таких ситуациях могут возникнуть следующие ошибки:

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

Чтобы включить восстановление пакетов, откройте меню **Сервис > Параметры > Диспетчер пакетов NuGet** и выберите параметры **Разрешить NuGet скачивать отсутствующие пакеты** и **Автоматически проверять отсутствие пакетов при сборке в Visual Studio**:

![включение восстановления пакетов NuGet в меню "Сервис", "Параметры"](../consume-packages/media/restore-01-autorestoreoptions.png)
