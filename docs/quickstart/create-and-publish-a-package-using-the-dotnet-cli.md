---
title: Создание и публикация пакета NuGet с помощью CLI dotnet
description: Пошаговое руководство по созданию и публикации пакета NuGet с помощью .NET Core CLI — dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: c0e6de2c3b9978538d504f4af6e744ece43b4a4d
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488936"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Краткое руководство. Создание и публикация пакета (dotnet CLI)

Создание пакета NuGet из библиотеки классов .NET и его публикация на сайте nuget.org выполняются очень просто с помощью интерфейса командной строки (CLI) `dotnet`.

## <a name="prerequisites"></a>Предварительные требования

1. Установите [пакет SDK для .NET Core](https://www.microsoft.com/net/download/), содержащий CLI `dotnet`. Начиная с версии Visual Studio 2017, средство CLI dotnet автоматически устанавливается вместе с любыми рабочими нагрузками, связанными с .NET Core.

1. [Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее. При создании учетной записи вам направляется сообщение электронной почты с подтверждением. Перед отправкой пакета вам нужно подтвердить учетную запись.

## <a name="create-a-class-library-project"></a>Создание проекта библиотеки классов

Вы можете использовать имеющийся проект библиотеки классов .NET для кода, который нужно упаковать, или же создать простой проект, как показано ниже:

1. Создайте папку с именем `AppLogger`.

1. Откройте командную строку и перейдите в папку `AppLogger`.

1. Введите `dotnet new classlib`; команда использует имя текущей папки для проекта.

   Будет создан новый проект.

1. Чтобы проверить, что приложение создано правильно, используйте команду `dotnet run`.

## <a name="add-package-metadata-to-the-project-file"></a>Добавление метаданных пакета в файл проекта

Каждому пакету NuGet нужен манифест, описывающий его содержимое и зависимости. В итоговом пакете манифестом является файл `.nuspec`, созданный из свойств метаданных NuGet, включенных в файл проекта.

1. Откройте файл проекта (`.csproj`) и добавьте внутри тега `<PropertyGroup>` следующие минимальные свойства. При этом измените значения соответствующим образом.

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Присвойте пакету идентификатор, уникальный на сайте nuget.org или в другом используемом узле. При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).

1. Укажите любые дополнительные свойства, описанные в разделе [Свойства метаданных NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > Если пакет будет общедоступным, обратите особое внимание на свойство **PackageTags**, так как теги помогают найти ваш пакет и понять его назначение.

## <a name="run-the-pack-command"></a>Выполнение команды pack

Чтобы создать пакет NuGet (`.nupkg` файл) из проекта, запустите команду `dotnet pack`, которая также автоматически построит проект:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

На выходе показан путь к `.nupkg` файлу:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Автоматическое создание пакета при сборке

Чтобы автоматически выполнить команду `dotnet pack` вместе с командой `dotnet build`, в разделе `<PropertyGroup>` файла проекта добавьте следующую строку:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Публикация пакета

Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя команду `dotnet nuget push`, а также ключ API, полученный на этом сайте.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Получение ключа API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Публикация с помощью команды dotnet nuget push

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Ошибки публикации

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Управление опубликованным пакетом

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Следующие шаги

Поздравляем! Вы создали пакет NuGet.

> [!div class="nextstepaction"]
> [Создание пакета](../create-packages/creating-a-package-dotnet-cli.md)

См. подробнее о возможностях NuGet по приведенным ниже ссылкам.

- [Публикация пакета](../nuget-org/publish-a-package.md)
- [Пакеты предварительного выпуска](../create-packages/Prerelease-Packages.md)
- [Поддержка нескольких целевых платформ](../create-packages/multiple-target-frameworks-project-file.md)
- [Управление версиями пакета](../concepts/package-versioning.md)
- [Создание локализованных пакетов](../create-packages/creating-localized-packages.md)
- [Создание пакетов символов](../create-packages/symbol-packages-snupkg.md)
- [Подписывание пакетов](../create-packages/Sign-a-package.md)
