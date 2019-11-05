---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610534"
---
#### <a name="windows"></a><span data-ttu-id="e54c8-101">Windows</span><span class="sxs-lookup"><span data-stu-id="e54c8-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="e54c8-102">Для выполнения NuGet.exe 5.0 и более поздних версий требуется .NET Framework 4.7.2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e54c8-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="e54c8-103">Перейдите к странице [nuget.org/downloads](https://nuget.org/downloads) и выберите NuGet 3.3 или более поздней версии (версия 2.8.6 не совместима с Mono).</span><span class="sxs-lookup"><span data-stu-id="e54c8-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="e54c8-104">Рекомендуем всегда использовать последнюю версию. Кроме того, для публикации пакетов на nuget.org требуется версия 4.1.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="e54c8-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="e54c8-105">Для каждой версии непосредственно скачивается файл `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="e54c8-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="e54c8-106">Укажите браузеру сохранять файл в выбранную вами папку.</span><span class="sxs-lookup"><span data-stu-id="e54c8-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="e54c8-107">Этот файл *не является* установщиком. Если запустить его непосредственно из браузера, ничего не отображается.</span><span class="sxs-lookup"><span data-stu-id="e54c8-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="e54c8-108">Добавьте папку с `nuget.exe` в переменную среды PATH, чтобы использовать средство CLI из любого расположения.</span><span class="sxs-lookup"><span data-stu-id="e54c8-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="e54c8-109">Mac OS и Linux</span><span class="sxs-lookup"><span data-stu-id="e54c8-109">macOS/Linux</span></span>

<span data-ttu-id="e54c8-110">Поведение для этих ОС может несколько различаться.</span><span class="sxs-lookup"><span data-stu-id="e54c8-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="e54c8-111">Установите [Mono 4.4.2 или более поздней версии](https://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="e54c8-111">Install [Mono 4.4.2 or later](https://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="e54c8-112">В командной строке оболочки введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e54c8-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="e54c8-113">Создайте псевдоним, добавив следующий скрипт к соответствующему файлу для вашей операционной системы (обычно `~/.bash_aliases` или `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="e54c8-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="e54c8-114">Перезагрузите оболочку.</span><span class="sxs-lookup"><span data-stu-id="e54c8-114">Reload the shell.</span></span>  <span data-ttu-id="e54c8-115">Проверьте установку. Для этого введите `nuget` без параметров.</span><span class="sxs-lookup"><span data-stu-id="e54c8-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="e54c8-116">Должно отобразиться окно справки NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="e54c8-116">NuGet CLI help should display.</span></span>
