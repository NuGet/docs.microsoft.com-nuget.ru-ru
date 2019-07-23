---
title: Определение формата проекта
description: Описание способов определения формата проекта
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843446"
---
# <a name="identify-the-project-format"></a>Определение формата проекта

NuGet работает со всеми проектами .NET. Но формат проекта (в стиле пакета SDK или не в стиле пакета SDK) определяет некоторые средства и методы, которые необходимо применять для использования и создания пакетов NuGet. В проектах в стиле пакета SDK используется атрибут [пакета SDK](/dotnet/core/tools/csproj#additions). Важно указать тип проекта, так как методы и средства, применяемые для использования и создания пакетов NuGet, зависят от формата проекта. Для проектов не в стиле пакета SDK методы и средства зависят также от того, преобразован ли проект в формат `PackageReference`.

Стиль проекта не зависит от метода, используемого для создания проекта. В следующей таблице представлен формат проекта по умолчанию и связанный с ним инструмент CLI, используемый при создании проекта с помощью Visual Studio 2017 и более поздних версий.

| Проект&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Формат проекта по умолчанию | Средство CLI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Примечания |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | Стиль пакета SDK | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Проекты, созданные в версиях, которые выпущены до Visual Studio 2017, разработаны не в стиле пакета SDK. Используйте CLI `nuget.exe`. |
| .NET Core | Стиль пакета SDK | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Проекты, созданные в версиях, которые выпущены до Visual Studio 2017, разработаны не в стиле пакета SDK. Используйте CLI `nuget.exe`. |
| .NET Framework | Проекты не в стиле пакета SDK | [Интерфейс командной строки nuget.exe](../install-nuget-client-tools.md#nugetexe-cli) | Проекты .NET Framework, созданные с помощью других методов, можно преобразовать в стиль пакета SDK. Для этого воспользуйтесь [CLI dotnet](../install-nuget-client-tools.md#dotnetexe-cli). |
| [Перенесенный](../reference/migrate-packages-config-to-package-reference.md) проект .NET | Проекты не в стиле пакета SDK| Создавайте пакеты с помощью [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration). | Для создания пакетов рекомендуем использовать `msbuild -t:pack`. Для других целей используйте [CLI dotnet](../install-nuget-client-tools.md#dotnetexe-cli). Перенесенные проекты не разработаны не в стиле SDK. |

## <a name="check-the-project-format"></a>Проверка формата проекта

Если вы не знаете, разработан ли проект в стиле пакета SDK, найдите атрибут SDK в элементе `<Project>` в файле проекта (для C# это файл *.csproj). Если такой атрибут есть, проект разработан в стиле пакета SDK.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>Проверка формата проекта в Visual Studio

При работе в Visual Studio можно быстро проверить формат проекта с помощью одного из следующих методов:

- В обозревателе решений щелкните проект правой кнопкой мыши и выберите команду **изменения имя_проекта.csproj**.

   Этот параметр доступен для проектов, использующих атрибут стиля пакета SDK, только в версиях начиная с Visual Studio 2017. При использовании других версий применяйте другой метод.

   ![Изменение файла проекта](media/edit-project-file.png)

   В файле проекта в стиле SDK отображается [атрибут пакета SDK](/dotnet/core/tools/csproj#additions).
   
- В меню **Проект** выберите команду **Выгрузить проект** (или щелкните проект правой кнопкой мыши и выберите команду **Выгрузить проект**).

   В файле этого проекта не будет отображаться атрибут пакета SDK. Значит, проект разработан не в стиле пакета SDK.

   ![Выгрузка проекта](media/unload-project.png)

   Затем щелкните правой кнопкой мыши выгруженный проект и выберите команду **изменения имя_проекта. csproj.**

## <a name="see-also"></a>См. также

- [Создание пакетов .NET Standard с помощью CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Создание пакетов .NET Standard с помощью Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Создание и публикация пакета .NET Framework (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [Объекты pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md)
