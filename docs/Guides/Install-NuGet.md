---
title: "Установка клиентских средств NuGet | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Рекомендации по установке клиентских средств, интерфейса командной строки (CLI) и диспетчера пакетов для Visual Studio."
keywords: "интерфейс командной строки nuget.exe, клиентские средства NuGet, диспетчер пакетов NuGet, консоль диспетчера пакетов NuGet, NuGet для Visual Studio, бета-канал NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a>Установка клиентских средств NuGet

> [!Tip]
> **Хотите установить пакет? См. раздел [Краткое руководство. Использование пакета](../Quickstart/Use-a-Package.md).**

Существует два основных средства для создания, публикации и использования пакетов NuGet:

1. [**NuGet CLI**](#nuget-cli) — это программа командной строки для Windows, которая предоставляет все возможности NuGet. Ее также можно запустить на Mac OSX и Linux с помощью Mono либо интерфейса командной строки .NET Core (`dotnet`).
1. [**Диспетчер пакетов NuGet в Visual Studio**](#nuget-package-manager-in-visual-studio) (только Windows) — это средство с графическим интерфейсом для управления пакетами. Оно включает в себя консоль PowerShell, позволяющую использовать некоторые команды NuGet прямо в Visual Studio. Пользовательский интерфейс и консоль диспетчера пакетов входят в состав Visual Studio 2012 и более поздних версий (в Windows), а для более ранних версий их можно установить вручную.

    В Visual Studio для Mac функции NuGet встроены напрямую. Пошаговое руководство см. в разделе [Включение пакета NuGet в проект](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).

    Сейчас Visual Studio Code не имеет встроенной поддержки NuGet. Используйте NuGet CLI или [dotnet CLI](../Tools/dotnet-Commands.md).

Как NuGet CLI, так и диспетчер пакетов поддерживают следующие операции:

- Поиск пакетов
- Установка пакетов
- Обновление пакетов
- Удаление пакетов
- Восстановление пакетов (только в пользовательском интерфейсе диспетчера пакетов)
- Управление источниками NuGet

Следующие возможности поддерживаются только в NuGet CLI:

- Управление пакетами (nuget.org или закрытый веб-канал)
- Создание пакетов 
- Публикация пакетов
- Управление Nuget.Config
- Управление кэшем NuGet
- Репликация пакета

> [!Note]
> Другим хорошим средством является автономный [обозреватель пакетов NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) с открытым исходным кодом, позволяющий визуально изучать, создавать и изменять пакеты NuGet. Это очень удобно, например, для внесения экспериментальных изменений в структуру пакета без необходимости его перестроения.
> Кроссплатформенная цепочка инструментов [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation), используемая для разработки приложений .NET Core, поддерживает несколько команд NuGet, таких как delete, locals, push, pack и restore. 

## <a name="nuget-cli"></a>NuGet CLI

Интерфейс командной строки NuGet предоставляет доступ ко всем возможностям NuGet и может выполняться в Windows, Mac OSX и Linux, как описано в следующих разделах.

### <a name="windows"></a>Windows

**Прямое скачивание:**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> С помощью NuGet 1.4+ вы можете использовать `nuget update -self` для обновления существующего nuget.exe до последней версии.

**Другие методы:**

- **Chocolatey**: установите пакет Chocolatey [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) с помощью клиента [Chocolatey](http://chocolatey.org). 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**: установите пакет [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) из консоли диспетчера пакетов в Visual Studio.

    > [!Note]
    > **Для пользователей NuGet 2.x**: в связи с критическими изменениями в NuGet 3.2 [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) указывает на последний стабильный выпуск NuGet 2.x во избежание потенциальных неполадок в системах непрерывной интеграции.

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX и Linux

В Mac OSX и Linux запустить NuGet CLI можно двумя способами:

- Установите [пакет SDK для .NET Core](https://www.microsoft.com/net/download/core), содержащий основные возможности NuGet. Файлы для скачивания также указаны на странице [github.com/dotnet/cli](https://github.com/dotnet/cli). Если вам нужны более развернутые возможности, используйте описанный ниже второй вариант использования `nuget.exe` с помощью Mono.

- Установите [Mono](http://www.mono-project.com/docs/getting-started/install/), а затем используйте исполняемый файл командной строки `nuget.exe` для Windows (версии 3.2 и более поздней) из [nuget.org/downloads](https://nuget.org/downloads). На запуск NuGet в Mono накладываются следующие ограничения:

    - Команды, работоспособность которых проверяется:
        - config
        - удалить
        - help
        - install
        - список
        - push
        - setApiKey
        - sources
        - spec

    - Частично работающие команды:
        - pack: работает с файлами `.nuspec`, но не с файлами проекта.
        - restore: работает с файлами `packages.config` и `project.json`, но не с файлами решения (`.sln`).

    - Неработающие команды:
        - обновить

### <a name="related-topics"></a>См. также

- [Справочник по интерфейсу командной строки NuGet](../tools/nuget-exe-cli-reference.md)
- [Создание пакета](../create-packages/creating-a-package.md)
- [Публикация пакета](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Диспетчер пакетов NuGet в Visual Studio

Диспетчер пакетов NuGet включен во все выпуски Visual Studio 2012 и более поздней версии для Windows. Он содержит пользовательский интерфейс диспетчера пакетов ([ссылка](../tools/package-manager-ui.md)) и консоль диспетчера пакетов, через которую осуществляется доступ к средствам, входящим в состав определенных пакетов ([ссылка](../tools/package-manager-console.md)).

Установщик Visual Studio 2017 содержит диспетчер пакетов NuGet с любой рабочей нагрузкой, использующей .NET. Чтобы проверить, установлен ли диспетчер пакетов, или установить его отдельно, запустите установщик Visual Studio 2017 и установите флажок **Отдельные компоненты > Средства для работы с кодом > Диспетчер пакетов NuGet**.

> [!Note]
> Консоли требуется [PowerShell 2.0](http://support.microsoft.com/kb/968929), который уже установлен в Windows 7 или более поздней версии и Windows Server 2008 R2 или более поздней версии.
>
> Команды консоли диспетчера пакетов работают только в Visual Studio для Windows. За пределами этой среды, включая Visual Studio для Mac и Visual Studio Code, используйте NuGet CLI.

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Установка диспетчера пакетов для Visual Studio 2010 и более ранних версий

*Эти действия не требуются для Visual Studio 2012 и более поздних версий, которые уже содержат диспетчер пакетов.*

1. В Visual Studio 2010 и более ранних версий выберите **Сервис > Расширения и обновления**.
1. Перейдите к полю **В сети**, выполните поиск фразы "диспетчер пакетов NuGet для Visual Studio" и нажмите кнопку **Скачать**.
1. В диалоговом окне установщика нажмите кнопку **Установить**.
1. После завершения установки перезапустите Visual Studio.

> [!Tip]
> Если вам не удается воспользоваться диалоговым окном **Расширения и обновления** в Visual Studio (например, его блокирует прокси-сервер), вы можете скачать расширения для Visual Studio 2013 и 2015 по адресу [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

### <a name="updating-the-package-manager"></a>Обновление диспетчера пакетов

Для Visual Studio 2015 с обновлением 2 и более поздних версий диспетчер пакетов автоматически обновляется до последнего стабильного выпуска.

Для Visual Studio 2015 с обновлением 1 и более ранних версий выберите **Сервис > Расширения и обновления** и откройте вкладку **Обновления**, чтобы узнать, доступна ли новая версия диспетчера пакетов.  

### <a name="nuget-previews"></a>Предварительные версии NuGet

Если вы хотите заранее оценить предстоящие возможности NuGet, установите предварительную версию [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), которая работает параллельно со стабильными выпусками Visual Studio.

Обратите внимание, что предыдущий бета-канал NuGet (`https://dotnet.myget.org/F/nuget-beta/vsix/`) для Visual Studio 2015 больше не используется.

Чтобы сообщить о проблемах с любым из выпусков NuGet или обменяться идеями, откройте вопрос в [репозитории NuGet GitHub](https://github.com/Nuget/Home).

### <a name="related-topics"></a>См. также

- [Справочник по пользовательскому интерфейсу диспетчера пакетов](../tools/package-manager-ui.md)
- [Справочник по консоли диспетчера пакетов](../tools/package-manager-console.md)
- [Справочник по PowerShell для консоли диспетчера пакетов](../tools/powershell-reference.md)