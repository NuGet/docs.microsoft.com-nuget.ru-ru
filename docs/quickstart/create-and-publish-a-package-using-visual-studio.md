---
title: Создание и публикация пакета NuGet .NET Standard с помощью Visual Studio в Windows
description: Пошаговое руководство по созданию и публикации пакета NuGet .NET Standard с помощью Visual Studio в Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 86e71460094de9b799384db83456a68db57647af
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419926"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Краткое руководство. Создание и публикация пакета NuGet с помощью Visual Studio (.NET Standard, только для Windows)

Создание пакета NuGet из библиотеки классов .NET Standard в Visual Studio в Windows и его публикация на сайте nuget.org с помощью средства интерфейса командной строки выполняются очень просто.

> [!Note]
> Если вы используете Visual Studio для Mac, ознакомьтесь с [этими сведениями](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) о создании пакета NuGet или примените [средства CLI dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Предварительные требования

1. Установите любой выпуск Visual Studio 2017 или более поздней версии со страницы [visualstudio.com](https://www.visualstudio.com/) с помощью рабочей нагрузки, связанной с .NET. Core.

1. При необходимости установите CLI `dotnet`.

   Для CLI `dotnet` начиная с версии Visual Studio 2017 CLI `dotnet` автоматически устанавливается вместе с любыми рабочими нагрузками, связанными с .NET Core. При использовании другой версии установите [пакет SDK для .NET Core](https://www.microsoft.com/net/download/), чтобы получить CLI `dotnet`. CLI `dotnet` является обязательным для проектов .NET Standard с [форматом в стиле пакета SDK](../resources/check-project-format.md) (атрибут SDK). Шаблон библиотеки классов по умолчанию в Visual Studio 2017 и более поздних версий, который применяется в рамках этой статьи, использует атрибут пакета SDK.
   
   > [!Important]
   > В рамках этой статьи рекомендуем использовать CLI `dotnet`. Любой пакет NuGet можно опубликовать с помощью CLI `nuget.exe`. Но некоторые действия, описанные в этой статье, относятся к проектам в стиле пакета SDK и CLI dotnet. CLI nuget.exe используется для [проектов не в стиле пакета SDK](../resources/check-project-format.md) (в основном для проектов .NET Framework). Если вы работаете с проектом не в стиле SDK, выполните инструкции по [созданию и публикации пакета .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md).

1. [Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account), если вы не сделали этого ранее. При создании учетной записи вам направляется сообщение электронной почты с подтверждением. Перед отправкой пакета вам нужно подтвердить учетную запись.

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

1. Щелкните правой кнопкой мыши проект в обозреватель решений и выберите команду меню **Свойства**, а затем выберите вкладку **Пакет**.

   Вкладка **Пакет** отображается только для проектов в стиле SDK в Visual Studio, в основном для проектов .NET Standard или библиотеки классов .NET Core. Если вы используете проект не в стиле SDK (например, проект .NET Framework), [перенесите проект](../reference/migrate-packages-config-to-package-reference.md) и используйте CLI `dotnet`. Или ознакомьтесь с пошаговыми инструкциями по [созданию и публикации пакета .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md)[.](create-and-publish-a-package-using-visual-studio-net-framework.md)

    ![Свойства пакета NuGet в проекте Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Если пакет будет общедоступным, обратите особое внимание на свойство **Теги**, так как они помогают найти ваш пакет и понять его назначение.

1. Присвойте пакету уникальный идентификатор и заполните нужные свойства. Описание различных свойств см. в [справочнике по NUSPEC-файлу](../reference/nuspec.md). Все свойства добавляются в манифест `.nuspec`, который Visual Studio создает для проекта.

    > [!Important]
    > Необходимо присвоить пакету идентификатор, который будет уникальным на сайте nuget.org или другом используемом узле. При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).
    >
    > При попытке опубликовать пакет с именем, которое уже занято, появится сообщение об ошибке.

1. Необязательно. Чтобы просматривать свойства непосредственно в файле проекта, щелкните правой кнопкой мыши проект в обозревателе решений и выберите **Изменить AppLogger.csproj**.

   Этот параметр доступен для проектов, использующих атрибут стиля пакета SDK, только в версиях начиная с Visual Studio 2017. Если у вас другой сценарий, щелкните проект правой кнопкой мыши и выберите пункт **Выгрузить проект**. Затем щелкните правой кнопкой мыши выгруженный проект и выберите команду **изменения AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Выполнение команды pack

1. Выберите конфигурацию **Выпуск**.

1. Щелкните проект правой кнопкой мыши в окне **обозревателя решений** и выберите команду **Паковать**:

    ![Команда "Паковать" для NuGet в контекстном меню проекта Visual Studio](media/qs_create-vs-02-pack-command.png)

    Если команда **Pack** не отображается, проект, скорее всего, не разработан в стиле SDK. В таком случае нужно использовать CLI `nuget.exe`. [Перенесите проект](../reference/migrate-packages-config-to-package-reference.md) и используйте CLI `dotnet`, или ознакомьтесь с пошаговыми инструкциями по [созданию и публикации пакета .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md).

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

Этот шаг — рекомендуемая альтернатива использования `nuget.exe`.

Перед публикацией пакета сначала нужно открыть командную строку.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a>Публикация с помощью команды nuget push (CLI nuget.exe)

Эту команду можно использовать вместо `dotnet.exe`.

1. Откройте командную строку и перейдите к папке с файлом `.nupkg`.

1. Выполните следующую команду, указав имя пакета (уникальный идентификатор пакета) и заменив значение ключа ключом API:

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

Ознакомьтесь со сведениями о [команде nuget push](../reference/cli-reference/cli-ref-push.md).

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
- [Публикация пакета](../nuget-org/publish-a-package.md)
- [Пакеты предварительного выпуска](../create-packages/Prerelease-Packages.md)
- [Поддержка нескольких целевых платформ](../create-packages/multiple-target-frameworks-project-file.md)
- [Управление версиями пакета](../reference/package-versioning.md)
- [Создание локализованных пакетов](../create-packages/creating-localized-packages.md)
- [Документация по библиотеке .NET Standard](/dotnet/articles/standard/library)
- [Перенос кода в .NET Core из .NET Framework](/dotnet/articles/core/porting/index)
