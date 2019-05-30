---
ms.openlocfilehash: 1f65939493cf423a76c024607264acee6c7e9050
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/28/2019
ms.locfileid: "66271521"
---
#### <a name="windows"></a>Windows

> [!Note]
> Для выполнения NuGet.exe 5.0 и более поздних версий требуется .NET Framework 4.7.2 или более поздней версии.

1. Перейдите к странице [nuget.org/downloads](https://nuget.org/downloads) и выберите NuGet 3.3 или более поздней версии (версия 2.8.6 не совместима с Mono). Рекомендуем всегда использовать последнюю версию. Кроме того, для публикации пакетов на nuget.org требуется версия 4.1.0 и выше.
1. Для каждой версии непосредственно скачивается файл `nuget.exe`. Укажите браузеру сохранять файл в выбранную вами папку. Этот файл *не является* установщиком. Если запустить его непосредственно из браузера, ничего не отображается.
1. Добавьте папку с `nuget.exe` в переменную среды PATH, чтобы использовать средство CLI из любого расположения.

#### <a name="macoslinux"></a>Mac OS и Linux

Поведение для этих ОС может несколько различаться.

1. Установите [Mono 4.4.2 или более поздней версии](http://www.mono-project.com/docs/getting-started/install/).

1. В командной строке оболочки введите следующие команды:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Создайте псевдоним, добавив следующий скрипт к соответствующему файлу для вашей операционной системы (обычно `~/.bash_aliases` или `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Перезагрузите оболочку.  Проверьте установку. Для этого введите `nuget` без параметров. Должно отобразиться окно справки NuGet CLI.
