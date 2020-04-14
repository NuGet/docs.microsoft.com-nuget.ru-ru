---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860580"
---
Используйте команду [restore](../../reference/cli-reference/cli-ref-restore.md), которая скачивает и устанавливает любые отсутствующие пакеты из папки *packages*.

Для проектов, перенесенных в PackageReference, используйте [msbuild -t:restore](../package-restore.md#restore-using-msbuild) для восстановления пакетов.

Команда `restore` добавляет пакеты на диск, но не изменяет список зависимых компонентов проекта. Чтобы восстановить зависимые компоненты пакета, измените файл `packages.config` и затем выполните команду `restore`.

Как и с другими командами CLI `nuget.exe`, откройте командную строку и перейдите к каталогу, в котором находится файл проекта.

Восстановление пакета с помощью `restore`.

```cli
nuget restore MySolution.sln
```