---
title: Создание и публикация пакета NuGet .NET Framework с помощью Visual Studio в Windows
description: Пошаговое руководство по созданию и публикации пакета NuGet .NET Framework с помощью Visual Studio в Windows.
author: JonDouglas
ms.author: jodou
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 7c030db769973e3b3c41da6523d57ab2cd769a9d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775749"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Краткое руководство. Создание и публикация пакета с помощью Visual Studio (.NET Framework, Windows)

Создание пакета NuGet из библиотеки классов .NET Framework включает в себя создание библиотеки DLL в Visual Studio в Windows и последующее использование программы командной строки nuget.exe для создания и публикации пакета.

> [!Note]
> Это краткое руководство относится только к Visual Studio 2017 для Windows и более поздним версиям. Visual Studio для Mac не поддерживает описанные здесь функции. Используйте вместо этого [средства интерфейса командной строки dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Предварительные требования

1. Установите любой выпуск Visual Studio 2017 или более поздней версии со страницы [visualstudio.com](https://www.visualstudio.com/) с помощью любой рабочей нагрузки, связанной с .NET. После установки рабочей нагрузки .NET Visual Studio 2017 автоматически добавит возможности NuGet.

1. Установите интерфейс командной строки `nuget.exe`, скачав его на сайте [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), и сохраните этот файл `.exe` в подходящую папку. Добавьте эту папку в переменную среды PATH.

1. [Зарегистрируйтесь для получения бесплатной учетной записи на nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), если вы не сделали этого ранее. При создании учетной записи вам направляется сообщение электронной почты с подтверждением. Перед отправкой пакета вам нужно подтвердить учетную запись.

## <a name="create-a-class-library-project"></a>Создание проекта библиотеки классов

Вы можете использовать имеющийся проект библиотеки классов .NET Framework для кода, который нужно упаковать, или же создать простой проект, как показано ниже.

1. В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > Windows**, выберите шаблон "Библиотека классов (.NET Framework)", назовите проект "AppLogger" и нажмите кнопку **ОК**.

1. Щелкните правой кнопкой мыши полученный файл проекта и выберите пункт **Сборка**, чтобы убедиться, что проект создан правильно. Библиотека DLL находится в папке Debug (или папке Release, если вы используете конфигурацию выпуска для сборки).

В реальном пакете NuGet вы можете реализовать множество полезных возможностей, с помощью которых другие пользователи могут создавать приложения. Кроме того, вы можете задать любые подходящие требуемые версии .NET Framework. Например, см. руководства по [UWP](../guides/create-uwp-packages.md) и [Xamarin](../guides/create-packages-for-xamarin.md).

Однако в этом пошаговом руководстве вы не будете писать дополнительный код, так как библиотеки классов из шаблона достаточно для создания пакета. Тем не менее, вы можете использовать функциональный код для пакета:

```cs
using System;

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
> Для пакетов NuGet мы рекомендуем использовать целевой объект .NET Standard (если нет причин использовать другое), так как он обеспечивает совместимость с рядом потребляющих проектов. См. раздел [Создание и публикация пакета с помощью Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Настройка свойств проекта для пакета

Пакет NuGet содержит манифест (файл `.nuspec`) с соответствующими метаданными, такими как идентификатор пакета, номер версии, описание и многое другое. Некоторые из них могут поступать напрямую из свойств проекта, в результате чего исчезает необходимость изменять их как в проекте, так и в манифесте. Этот раздел описывает, где можно задать соответствующие свойства.

1. Выберите команду меню **Проект > Свойства**, а затем щелкните вкладку **Приложение**.

1. В поле **Имя сборки** укажите уникальный идентификатор пакета.

    > [!Important]
    > Необходимо присвоить пакету идентификатор, который будет уникальным на сайте nuget.org или другом используемом узле. При работе с этим руководством мы рекомендуем добавить к имени слово "Sample" или "Test", так как позже, после публикации, пакет станет общедоступным (хотя маловероятно, что кто-то будет его использовать).
    >
    > При попытке опубликовать пакет с именем, которое уже занято, появится сообщение об ошибке.

1. Нажмите кнопку **Сведения о сборке...** , чтобы открыть диалоговое окно, где можно ввести другие свойства, которые переносятся в манифест (см. [описание токенов замены в справочнике по файлу NUSPEC](../reference/nuspec.md#replacement-tokens)). Чаще всего используются поля **Заголовок**, **Описание**, **Компания**, **Авторские права** и **Версия сборки**. В конечном счете эти свойства отображаются вместе с пакетом на узле, таком как nuget.org, поэтому задайте для них очевидное и понятное значение.

    ![Сведения о сборке в проекте .NET Framework в Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Необязательно. Чтобы просмотреть или изменить свойства напрямую, откройте файл `Properties/AssemblyInfo.cs` в проекте.

1. Задав свойства, укажите для конфигурацию проекта значение **Выпуск** и перестройте проект для создания обновленной библиотеки DLL.

## <a name="generate-the-initial-manifest"></a>Создание начального манифеста

Получив библиотеку DLL и задав свойства проекта, вы можете использовать команду `nuget spec`, чтобы создать начальный файл `.nuspec` из проекта. Этот шаг включает в себя соответствующие токены замены для получения сведений из файла проекта.

Запускать `nuget spec` для создания начального манифеста потребуется всего один раз. При обновлении пакета нужно либо изменить значения в проекте, либо отредактировать сам файл манифеста.

1. Откройте командную строку и перейдите в папку проекта, содержащую файл `AppLogger.csproj`.

1. Выполните следующую команду: `nuget spec AppLogger.csproj`. После указания проекта NuGet создает манифест с тем же именем, что и проект, в данном случае это `AppLogger.nuspec`. Он также включает в себя токены замены из манифеста.

1. Откройте файл `AppLogger.nuspec` в текстовом редакторе для просмотра его содержимого, которое должно иметь следующий вид.

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>Package</id>
        <version>1.0.0</version>
        <authors>YourUsername</authors>
        <owners>YourUsername</owners>
        <license type="expression">MIT</license>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Package description</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2019</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>Изменение манифеста

1. NuGet выдает ошибку при попытке создать пакет со значениями по умолчанию в вашем файле `.nuspec`, поэтому перед продолжением нужно изменить следующие поля. Их использование описано в [разделе о необязательных элементах метаданных в справочнике по файлу NUSPEC](../reference/nuspec.md#optional-metadata-elements).

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - теги

1. Если пакет будет общедоступным, обратите особое внимание на свойство **Теги**, так как они помогают найти ваш пакет в таких источниках, как nuget.org, и понять его назначение.

1. Кроме того, сейчас можно добавить в манифест любые другие элементы, как описано в разделе [Справочник по файлу NUSPEC](../reference/nuspec.md).

1. Сохраните файл, прежде чем продолжить.

## <a name="run-the-pack-command"></a>Выполнение команды pack

1. Из командной строки перейдите в папку, содержащую файл `.nuspec`, и выполните команду `nuget pack`.

1. NuGet создает в текущей папке файл `.nupkg` формата *идентификатор-версия.nupkg*.

## <a name="publish-the-package"></a>Публикация пакета

Получив файл `.nupkg`, опубликуйте его на сайте nuget.org, используя `nuget.exe`, а также ключ API, полученный на этом сайте. Для nuget.org нужно использовать `nuget.exe` 4.1.0 или более поздней версии.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Получение ключа API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Публикация с помощью команды nuget push

1. Откройте командную строку и перейдите к папке с файлом `.nupkg`.

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

Ознакомьтесь со сведениями о [команде nuget push](../reference/cli-reference/cli-ref-push.md).

### <a name="publish-errors"></a>Ошибки публикации

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Управление опубликованным пакетом

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Следующие шаги

Поздравляем! Вы создали пакет NuGet.

> [!div class="nextstepaction"]
> [Создание пакета](../create-packages/creating-a-package.md)

См. подробнее о возможностях NuGet по приведенным ниже ссылкам.

- [Публикация пакета](../nuget-org/publish-a-package.md)
- [Пакеты предварительного выпуска](../create-packages/Prerelease-Packages.md)
- [Поддержка нескольких целевых платформ](../create-packages/supporting-multiple-target-frameworks.md)
- [Управление версиями пакета](../concepts/package-versioning.md)
- [Создание локализованных пакетов](../create-packages/creating-localized-packages.md)
