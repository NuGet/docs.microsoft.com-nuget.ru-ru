---
title: Пакеты NuGet в шаблонах Visual Studio
description: Инструкции по включению пакетов NuGet в состав шаблонов проектов и элементов Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: 2dfbd793eee05169f051d9c8943bc065945b92da
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622646"
---
# <a name="packages-in-visual-studio-templates"></a>Пакеты в шаблонах Visual Studio

Шаблонам проектов и элементов Visual Studio часто требуется обеспечить установку определенных пакетов при создании проекта или элемента. Например, шаблон ASP.NET MVC 3 устанавливает jQuery, Modernizr и другие пакеты.

Для этого авторы шаблонов могут настроить NuGet для установки необходимых пакетов, а не отдельных библиотек. Позднее разработчики могут в любое время легко обновить эти пакеты.

Дополнительные сведения о создании шаблонов см. в разделе [Практическое руководство. Создание шаблонов проектов](/visualstudio/ide/how-to-create-project-templates) и [Создание настраиваемых шаблонов проектов и элементов](/visualstudio/extensibility/creating-custom-project-and-item-templates).

Оставшаяся часть этого раздела посвящена конкретным шагам, которые следует предпринять при создании шаблона, чтобы правильно включить пакеты NuGet.

- [Добавление пакетов в шаблон](#adding-packages-to-a-template)
- [Рекомендации](#best-practices)

Например, ознакомьтесь с [примером NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Добавление пакетов в шаблон

При создании шаблона вызывается [мастер шаблонов](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) для загрузки списка устанавливаемых пакетов, а также сведений об их расположении. Пакеты могут быть внедрены в VSIX, в шаблон или расположены на локальном жестком диске, в случае чего вы используете раздел реестра, чтобы сослаться на путь к файлу. Сведения об этих расположениях приведены ниже в этом разделе.

Предустановленные пакеты используют для работы [мастеры шаблонов](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Специальный мастер вызывается при создании экземпляра шаблона. Он загружает список пакетов, которые нужно установить, и передает эти сведения соответствующим API NuGet.

Шаги по включению пакетов в шаблон:

1. Добавьте в свой файл `vstemplate` ссылку на мастер шаблонов NuGet, добавив элемент [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates):

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` — это сборка, содержащая только класс`TemplateWizard`, который представляет собой простую программу-оболочку, вызывающую фактическую реализацию в `NuGet.VisualStudio.dll`. Версия сборки не изменится, поэтому эти шаблоны проектов и элементов продолжат работать с новыми версиями NuGet.

1. Добавьте список устанавливаемых пакетов в проект:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Мастер поддерживает несколько элементов `<package>`, что обеспечивает поддержку нескольких источников пакетов. Требуются оба атрибута `id` и `version`, то есть эта конкретная версия пакета будет установлена, даже если доступна более новая версия. Это не позволяет обновлениям пакета нарушить работу шаблона и предоставляет возможность обновить пакет разработчику, использующему шаблон.

1. Укажите репозиторий, где NuGet может найти пакеты, как описано в следующих разделах.

### <a name="vsix-package-repository"></a>Репозиторий пакетов VSIX

Для развертывания шаблонов проектов и элементов Visual Studio рекомендуется использовать [расширение VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions), так как оно дает возможность упаковать вместе несколько шаблонов проектов или элементов и позволяет разработчикам легко находить ваши шаблоны с помощью диспетчера расширений VS или коллекции Visual Studio. Обновления для этого расширения также легко развернуть с помощью [механизма автоматического обновления в диспетчере расширений Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

Сам VSIX может служить источником необходимых шаблону пакетов:

1. Измените элемент `<packages>` в файле `.vstemplate` следующим образом:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    Атрибут `repository` задает тип репозитория как `extension`, а `repositoryId` является уникальным идентификатором самого VSIX (это значение атрибута `ID` в файле `vsixmanifest` расширения, см. [Справочник по схеме 2.0 расширения VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Поместите файлы `nupkg` в папку `Packages` внутри VSIX.

1. Добавьте нужные файлы пакетов как `<Asset>` в файл `vsixmanifest` (см. [Справочник по схеме 2.0 расширения VSIX](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Обратите внимание, что можно доставить пакеты в тот же VSIX, что и шаблоны проекта, либо поместить их в отдельный VSIX, если это лучше подходит для вашего сценария. Однако не следует ссылаться на любой VSIX, которым вы не управляете, так как изменения в этом расширении могут нарушить работу шаблона.

### <a name="template-package-repository"></a>Репозиторий пакетов шаблонов

Если вы распространяете только один шаблон проектов или элементов и вам не нужно паковать вместе несколько шаблонов, можно использовать более простой, хотя и ограниченный, подход, включающий пакеты непосредственно в ZIP-файл шаблона проектов или элементов:

1. Измените элемент `<packages>` в файле `.vstemplate` следующим образом:

    ```xml
    <packages repository="template">
        <!-- ... -->
    </packages>
    ```

    Атрибут `repository` имеет значение `template`, а атрибут `repositoryId` не является обязательным.

1. Поместите пакеты в корневую папку в ZIP-файле шаблона проектов или элементов.

Обратите внимание, что применение такого подхода для VSIX, содержащего несколько шаблонов, приводит к ненужному раздуванию, когда один или несколько пакетов являются общими для шаблонов. В таких случаях используйте [VSIX в качестве репозитория](#vsix-package-repository), как описано в предыдущем разделе.

### <a name="registry-specified-folder-path"></a>Путь к папке, указанный для реестра

Пакеты SDK, устанавливаемые с помощью MSI, могут устанавливать пакеты NuGet непосредственно на компьютере разработчика. В результате их не требуется извлекать при использовании шаблона проектов или элементов, они доступны сразу же. Этот подход используется в шаблонах ASP.NET.

1. Позвольте MSI установить пакеты на компьютере. Вы можете установить файлы `.nupkg` отдельно либо вместе с расширенным содержимым, которое позволяет пропустить один из шагов при использовании шаблона. В этом случае следуйте стандартной структуре папок NuGet, когда файлы `.nupkg` находятся в корневой папке, а каждый пакет имеет вложенную папку, имя которой состоит из пары идентификатора и версии.

1. Запишите раздел реестра для определения расположения пакета:

    - Расположение ключа: либо на уровне компьютера `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository`, либо, если шаблоны и пакеты установлены для конкретного пользователя, можно также использовать `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`.
    - Имя ключа: используйте уникальное имя. Например, шаблоны ASP.NET MVC 4 для Visual Studio 2012 используют `AspNetMvc4VS11`.
    - Значения: полный путь к папке пакетов.

1. Добавьте в элемент `<packages>` в файле `.vstemplate` атрибут `repository="registry"` и укажите имя раздела реестра в атрибуте `keyName`.

    - Если вы заранее распаковали пакеты, используйте атрибут `isPreunzipped="true"`.
    - *(NuGet 3.2+)* Если вы хотите принудительно выполнить сборку времени разработки в конце установки пакета, добавьте атрибут `forceDesignTimeBuild="true"`.
    - Для оптимизации добавьте `skipAssemblyReferences="true"`, так как шаблон уже включает в себя необходимые ссылки.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Рекомендации

1. Объявите о зависимости от NuGet VSIX, добавив ссылку на него в манифесте VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Настройте сохранение шаблонов проектов и элементов при их создании, включив [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) в файл `.vstemplate`.

1. Шаблоны не содержат файл `packages.config`, а также ссылки или содержимое, которое следует добавить при установке пакетов NuGet.
