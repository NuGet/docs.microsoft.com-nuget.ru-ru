---
title: "Вводное руководство по созданию и публикации пакета NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Пошаговый учебник по созданию и публикации пакета NuGet с помощью интерфейса командной строки nuget.exe и Visual Studio."
keywords: "создание пакетов NuGet, публикация пакетов NuGet, учебник NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/31/2018
---
# <a name="create-and-publish-a-package"></a>Создание и публикация пакета

Создание пакета NuGet из библиотеки классов .NET и его публикация на сайте nuget.org выполняются очень просто. В этой статье показано, как сделать это с помощью интерфейса командной строки NuGet и Visual Studio.

## <a name="pre-requisites"></a>Предварительные требования

1. Установите любой выпуск Visual Studio 2017 со страницы [visualstudio.com](https://www.visualstudio.com/).

1. Установите средство интерфейса командной строки NuGet `nuget.exe`, скачав последнюю версию `nuget.exe` со страницы [nuget.org/downloads](https://nuget.org/downloads) и сохранив `.exe` в расположении, указанном в переменной PATH. Обратите внимание, что скачивается *само* средство, а не установщик.

1. Создайте подходящий проект библиотеки классов .NET для кода, который нужно упаковать. Если у вас еще нет проекта, вы можете создать его следующим образом:
    1. В Visual Studio выберите **Файл > Создать > Проект**, разверните узел **Visual C# > Windows**, выберите шаблон "Библиотека классов", назовите проект "AppLogger" и нажмите кнопку **ОК**.
    1. Щелкните правой кнопкой мыши полученный файл проекта и выберите пункт **Сборка**, чтобы убедиться, что проект создан правильно. Библиотека DLL находится в папке Debug (или папке Release, если вы используете конфигурацию выпуска для сборки).

    В реальном пакете NuGet вы, конечно же, реализовали бы множество полезных возможностей, с помощью которых другие пользователи могли бы создавать приложения. Однако в этом пошаговом руководстве вы не будете писать дополнительный код, так как библиотеки классов из шаблона достаточно для создания пакета.

## <a name="create-the-nuspec-package-manifest-file"></a>Создание файла манифеста пакета NUSPEC

Каждому пакету NuGet нужен манифест &mdash; файл `.nuspec` &mdash; для описания его содержимого и зависимостей. Команда `nuget spec` создает этот файл, который затем можно настроить. В этом примере вы создаете `.nuspec` из файла проекта. Манифест можно создать и другими средствами, как описано в статье [Создание пакета](../create-packages/creating-a-package.md).

1. Откройте командную строку и перейдите в папку, содержащую файл проекта (`.csproj`).

1. Запустите команду `spec` интерфейса командной строки NuGet, чтобы создать манифест, которому присваивается имя проекта, то есть `AppLogger.nuspec`:

    ```cli
    nuget spec
    ```

1. Откройте файл в текстовом редакторе. Манифест похож на приведенный ниже код, где токены вида `<token>` (такие, как `$id$`) в процессе упаковки заменяются на значения из файла Properties/AssemblyInfo.cs проекта. Дополнительные сведения о токенах см. в разделе [Создание файла NUSPEC](../create-packages/creating-a-package.md#creating-the-nuspec-file).

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. Выберите идентификатор пакета, который уникален в пределах сайта nuget.org. Мы рекомендуем использовать соглашения об именовании, описанные в разделе [Создание пакета](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Обновите теги автора и описания, в противном случае на следующем шаге возникнет ошибка. Вот пример обновленного файла `.nuspec`:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Если пакет будет общедоступным, обратите особое внимание на элемент `<tags>`, так как эти теги помогают найти ваш пакет и понять его назначение.

## <a name="run-the-pack-command"></a>Выполнение команды pack

Чтобы выполнить сборку пакета NuGet (файла `.nupkg`) из проекта, запустите команду `pack`:

```cli
nuget pack AppLogger.csproj
```

Она создает `AppLogger.1.0.0.0.nupkg` с помощью имени пакета и номера версии из файла `.nuspec`. Эта команда выдает предупреждения, если вы еще не изменили значения по умолчанию в различных полях файла `.nuspec`.

## <a name="publish-the-package"></a>Публикация пакета

Получив файл `.nupkg`, вы публикуете его на сайте nuget.org с помощью команды `push`. (Кроме того, можно использовать [рабочий процесс публикации nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg).

> [!Warning]
> Пакеты, публикуемые на сайте nuget.org, видны всем другим разработчикам. Чтобы разместить пакеты частным образом, см. раздел [Размещение пакетов](../hosting-packages/overview.md).

1. Создайте бесплатную учетную запись на сайте [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) или войдите, если она у вас уже есть. При создании учетной записи вам направляется сообщение электронной почты с подтверждением. Перед отправкой пакета вам нужно подтвердить учетную запись.

1. После входа выберите свое имя пользователя (в правом верхнем углу) и затем пункт **Ключи API**.

1. Выберите **Создать**, укажите имя для ключа, выберите **Выбрать области > Push** (Отправить) в области **Ключ API**, введите * в поле **Glob pattern** (Стандартная маска), а затем выберите **Создать**.

1. После создания ключа выберите **Копировать** для получения ключа доступа, который потребуется в интерфейсе командной строки:

    ![Копирование ключа API в буфер обмена](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > Сохраните ключ в безопасном месте и не сообщайте его никому. Если ваш ключ будет случайно раскрыт, вы можете создать его повторно в любое время. Вы также можете удалить ключ API, если больше не хотите отправлять пакеты через интерфейс командной строки.

1. В командной строке выполните следующую команду, указав имя пакета и заменив ключ на значение, скопированное на шаге 4:

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe отображает результаты публикации:

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. В своем профиле на сайте nuget.org выберите **Управление пакетами**, чтобы отобразить опубликованный вами пакет. Вы также получите подтверждение по электронной почте. Обратите внимание, что пакет индексируется и будет появляться в результатах поиска для других пользователей спустя определенное время. В этот период на странице вашего пакета отображается следующее сообщение:

    ![This package has not been indexed yet. It will appear in search results and will be available for install/restore after indexing is complete (Этот пакет еще не проиндексирован. Он появится в результатах поиска и будет доступен для установки и восстановления после завершения индексирования).](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **Проверка на вирусы**: перед публикацией все пакеты, загружаемые на веб-сайт nuget.org, проверяются на вирусы, и в случае обнаружения вирусов отклоняются. Кроме того, периодическую проверку проходят все пакеты, представленные на веб-сайте nuget.org.

Вот и все! Вы только что опубликовали на сайте [nuget.org](https://www.nuget.org/) свой первый пакет NuGet, который другие разработчики могут использовать в своих собственных проектах.

## <a name="related-topics"></a>См. также

- [Создание пакета](../create-packages/creating-a-package.md)
- [Публикация пакета](../create-packages/publish-a-package.md)
- [Поддержка нескольких целевых платформ](../create-packages/supporting-multiple-target-frameworks.md)
- [Управление версиями пакета](../reference/package-versioning.md)
- [Создание локализованных пакетов](../create-packages/creating-localized-packages.md)
