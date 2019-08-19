---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860580"
---
<span data-ttu-id="9d913-101">Используйте команду [restore](../../reference/cli-reference/cli-ref-restore.md), которая скачивает и устанавливает любые отсутствующие пакеты из папки *packages*.</span><span class="sxs-lookup"><span data-stu-id="9d913-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="9d913-102">Для проектов, перенесенных в PackageReference, используйте [msbuild -t:restore](../package-restore.md#restore-using-msbuild) для восстановления пакетов.</span><span class="sxs-lookup"><span data-stu-id="9d913-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="9d913-103">Команда `restore` добавляет пакеты на диск, но не изменяет список зависимых компонентов проекта.</span><span class="sxs-lookup"><span data-stu-id="9d913-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="9d913-104">Чтобы восстановить зависимые компоненты пакета, измените файл `packages.config` и затем выполните команду `restore`.</span><span class="sxs-lookup"><span data-stu-id="9d913-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="9d913-105">Как и с другими командами CLI `nuget.exe`, откройте командную строку и перейдите к каталогу, в котором находится файл проекта.</span><span class="sxs-lookup"><span data-stu-id="9d913-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="9d913-106">Восстановление пакета с помощью `restore`.</span><span class="sxs-lookup"><span data-stu-id="9d913-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```