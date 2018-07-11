#### <a name="windows"></a><span data-ttu-id="3d3d3-101">Windows</span><span class="sxs-lookup"><span data-stu-id="3d3d3-101">Windows</span></span>

1. <span data-ttu-id="3d3d3-102">Перейдите к странице [nuget.org/downloads](https://nuget.org/downloads) и выберите NuGet 3.3 или более поздней версии (версия 2.8.6 не совместима с Mono).</span><span class="sxs-lookup"><span data-stu-id="3d3d3-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="3d3d3-103">Рекомендуем всегда использовать последнюю версию. Кроме того, для публикации пакетов на nuget.org требуется версия 4.1.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="3d3d3-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="3d3d3-104">Для каждой версии непосредственно скачивается файл `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="3d3d3-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="3d3d3-105">Укажите браузеру сохранять файл в выбранную вами папку.</span><span class="sxs-lookup"><span data-stu-id="3d3d3-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="3d3d3-106">Этот файл *не является* установщиком. Если запустить его непосредственно из браузера, ничего не отображается.</span><span class="sxs-lookup"><span data-stu-id="3d3d3-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="3d3d3-107">Добавьте папку с `nuget.exe` в переменную среды PATH, чтобы использовать средство CLI из любого расположения.</span><span class="sxs-lookup"><span data-stu-id="3d3d3-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="3d3d3-108">Mac OS и Linux</span><span class="sxs-lookup"><span data-stu-id="3d3d3-108">macOS/Linux</span></span>

<span data-ttu-id="3d3d3-109">Поведение для этих ОС может несколько различаться.</span><span class="sxs-lookup"><span data-stu-id="3d3d3-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="3d3d3-110">Установите [Mono 4.4.2 или более поздней версии](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="3d3d3-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="3d3d3-111">В командной строке оболочки введите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="3d3d3-111">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="3d3d3-112">Создайте псевдоним, добавив следующий скрипт к соответствующему файлу для вашей операционной системы (обычно `~/.bash_aliases` или `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="3d3d3-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="3d3d3-113">Перезагрузите оболочку.</span><span class="sxs-lookup"><span data-stu-id="3d3d3-113">Reload the shell.</span></span>  <span data-ttu-id="3d3d3-114">Проверьте установку. Для этого введите `nuget` без параметров.</span><span class="sxs-lookup"><span data-stu-id="3d3d3-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="3d3d3-115">Должно отобразиться окно справки NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="3d3d3-115">NuGet CLI help should display.</span></span>
