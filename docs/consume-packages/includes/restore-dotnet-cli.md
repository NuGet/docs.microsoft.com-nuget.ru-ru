---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825165"
---
С помощью команды [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) вы можете восстановить пакеты, включенные в файл проекта (см. [PackageReference](../../consume-packages/package-references-in-project-files.md)). При использовании .NET Core версии 2.0 и более поздней автоматическое восстановление доступно с помощью команд `dotnet build` и `dotnet run`. В версии NuGet 4.0 при этом выполняется тот же код, что и для команды `nuget restore`.

Как и с другими командами CLI `dotnet`, откройте командную строку и перейдите к каталогу, в котором находится файл проекта.

Восстановление пакета с помощью `dotnet restore`.

```dotnetcli
dotnet restore 
```