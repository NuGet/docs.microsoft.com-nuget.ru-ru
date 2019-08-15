---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860609"
---
С помощью команды [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) вы можете восстановить пакеты, включенные в файл проекта (см. [PackageReference](../../consume-packages/package-references-in-project-files.md)). При использовании .NET Core версии 2.0 и более поздней автоматическое восстановление доступно с помощью команд `dotnet build` и `dotnet run`. В версии NuGet 4.0 при этом выполняется тот же код, что и для команды `nuget restore`.

Как и с другими командами CLI `dotnet`, откройте командную строку и перейдите к каталогу, в котором находится файл проекта.

Восстановление пакета с помощью `dotnet restore`.

```cli
dotnet restore 
```