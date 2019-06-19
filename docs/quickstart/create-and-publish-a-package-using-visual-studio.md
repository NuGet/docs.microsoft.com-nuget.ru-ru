---
title: Создание и публикация пакета .NET Standard с помощью Visual Studio в Windows
description: Пошаговое руководство по созданию и публикации пакета NuGet .NET Standard с помощью Visual Studio 2017 в Windows.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: d30e89473b5f00895136b75a90d8d95b7645a100
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812979"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Краткое руководство. Создание и публикация пакета NuGet с помощью Visual Studio (.NET Standard, только для Windows)

Создание пакета NuGet из библиотеки классов .NET Standard в Visual Studio в Windows и его публикация на сайте nuget.org с помощью средства интерфейса командной строки выполняются очень просто.

> [!Note]
> Это краткое руководство относится только к Visual Studio 2017 для Windows. Visual Studio для Mac не поддерживает описанные здесь функции. Используйте вместо этого [средства интерфейса командной строки dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Предварительные требования

1. Установите любой выпуск Visual Studio 2017 со страницы [visualstudio.com](https://www.visualstudio.com/) с помощью любой рабочей нагрузки, связанной с .NET. После установки рабочей нагрузки .NET Visual Studio 2017 автоматически добавит возможности NuGet.

1. Установите одно из средств CLI.

   * Для средства CLI `dotnet` установите [пакет SDK для .NET Core](https://www.microsoft.com/net/download/). CLI для .NET является обязательным для проектов .NET Standard с форматом в стиле пакета SDK (атрибут SDK).

   * Установите средство CLI `nuget.exe`, скачав его на сайте [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), и сохраните этот файл `.exe` в подходящую папку. Добавьте эту папку в переменную среды PATH. CLI nuget.exe используется для библиотек .NET Standard в формате со стилем, отличным от пакета SDK.

1. [Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее. При создании учетной записи вам направляется сообщение электронной почты с подтверждением. Перед отправкой пакета вам нужно подтвердить учетную запись.

## <a name="create-a-class-library-project"></a>Создание проекта библиотеки классов

Вы можете использовать имеющийся проект библиотеки классов .NET Standard для кода, который нужно упаковать, или же создать простой проект, как показано ниже.

1. В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > .NET Standard**, выберите шаблон "Библиотека классов (.NET Standard)", назовите проект AppLogger и нажмите кнопку **ОК**.

1. Щелкните правой кнопкой мыши полученный файл проекта и выберите пункт **Сборка**, чтобы убедиться, что проект создан правильно. Библиотека DLL находится в папке Debug (или папке Release, если вы используете конфигурацию выпуска для сборки).

В реальном пакете NuGet вы можете реализовать множество полезных возможностей, с помощью которых другие пользователи могут создавать приложения. Однако в этом пошаговом руководстве вы не будете писать дополнительный код, так как библиотеки классов из шаблона достаточно для создания пакета. Тем не менее, вы можете использовать функциональный код для пакета:

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> Для пакетов NuGet мы рекомендуем использовать целевой объект .NET Standard (если нет причин использовать другое), так как он обеспечивает совместимость с рядом потребляющих проектов.

## <a name="configure-package-properties"></a>Настройка свойств пакета

1. Выберите команду меню **Проект > Свойства**, а затем щелкните вкладку **Пакет**. (Вкладка **Пакет** отображается только для проектов библиотек классов .NET Standard. Если вы ориентируетесь на .NET Framework, см. вместо этого раздел [Создание и публикация пакета .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md). Если она не отображается в проекте .NET Standard, может потребоваться обновить Visual Studio 2017 до последней версии.)

    ![Свойства пакета NuGet в проекте Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Если пакет будет общедоступным, обратите особое внимание на свойство **Теги**, так как они помогают найти ваш пакет и понять его назначение.

1. Присвойте пакету уникальный идентификатор и заполните нужные свойства. Описание различных свойств см. в [справочнике по NUSPEC-файлу](../reference/nuspec.md). Все свойства добавляются в манифест `.nuspec`, который Visual Studio создает для проекта.

    > [!Important]
    > Необходимо присвоить пакету идентификатор, который будет уникальным на сайте nuget.org или другом используемом узле. При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).
    >
    > При попытке опубликовать пакет с именем, которое уже занято, появится сообщение об ошибке.

1. Необязательно. Чтобы просматривать свойства непосредственно в файле проекта, щелкните правой кнопкой мыши проект в обозревателе решений и выберите **Изменить AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Выполнение команды pack

1. Выберите конфигурацию **Выпуск**.

1. Щелкните проект правой кнопкой мыши в окне **обозревателя решений** и выберите команду **Паковать**:

    ![Команда "Паковать" для NuGet в контекстном меню проекта Visual Studio](media/qs_create-vs-02-pack-command.png)

1. Visual Studio создаст проект и файл `.nupkg`. Ознакомьтесь с результатами в окне **выходных данных** (пример приведен ниже), где содержится путь к файлу пакета. Обратите внимание, что созданная сборка находится в папке `bin\Release\netstandard2.0`, которая является целевой для .NET Standard 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Альтернативный вариант: упаковка с помощью MSBuild

В качестве альтернативы команде меню **Pack** в NuGet 4.x+ и MSBuild 15.1+ можно использовать целевой объект `pack`, когда проект содержит необходимые данные о пакете. Откройте командную строку, перейдите в папку проекта и запустите приведенную ниже команду. (В общем случае следует запустить Командную строку разработчика для Visual Studio из меню "Пуск", так как в этом случае настраиваются все необходимые пути для MSBuild.)

```cli
msbuild -t:pack -p:Configuration=Release
```

Этот пакет должен находиться в папке `bin\Release`.

Дополнительные сведения об использовании `msbuild -t:pack` см. в описании [объектов pack и restore NuGet в качестве целевых объектов MSBuild](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Публикация пакета

Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя интерфейс командной строки `nuget.exe` или `dotnet.exe`, а также ключ API, полученный на этом сайте.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Получение ключа API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a>Публикация с помощью команды dotnet nuget push (CLI для .NET)

Эту команду можно использовать вместо `nuget.exe`.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a>Публикация с помощью команды nuget push (CLI nuget.exe)

Эту команду можно использовать вместо `dotnet.exe`.

1. Перейдите в папку, содержащую файл `.nupkg`.

1. Выполните следующую команду, указав имя пакета и заменив значение ключа на ключ API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe отображает результаты публикации:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Ознакомьтесь со сведениями о [команде nuget push](../tools/cli-ref-push.md).

### <a name="publish-errors"></a>Ошибки публикации

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Управление опубликованным пакетом

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Добавление файла сведений и других файлов

Чтобы напрямую указать файлы, включаемые в пакет, измените файл проекта и используйте свойство `content`:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

В корень пакета будет включен файл с именем `readme.txt`. Visual Studio отображает содержимое этого файла в виде обычного текста сразу после установки пакета напрямую. (Файлы сведений не отображаются для пакетов, устанавливаемых как зависимости.) Например, вот как выглядит файл сведений для пакета HtmlAgilityPack:

![Отображение файла сведений для пакета NuGet при установке](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Обычное добавление файла readme.txt в корень проекта не приведет к включению его в итоговый пакет.

## <a name="related-topics"></a>См. также

- [Создание пакета](../create-packages/creating-a-package.md)
- [Публикация пакета](../create-packages/publish-a-package.md)
- [Пакеты предварительного выпуска](../create-packages/Prerelease-Packages.md)
- [Поддержка нескольких целевых платформ](../create-packages/supporting-multiple-target-frameworks.md)
- [Управление версиями пакета](../reference/package-versioning.md)
- [Создание локализованных пакетов](../create-packages/creating-localized-packages.md)
- [Документация по библиотеке .NET Standard](/dotnet/articles/standard/library)
- [Перенос кода в .NET Core из .NET Framework](/dotnet/articles/core/porting/index)
