#### <a name="windows"></a><span data-ttu-id="df29b-101">Windows</span><span class="sxs-lookup"><span data-stu-id="df29b-101">Windows</span></span>
1. <span data-ttu-id="df29b-102">Посетите [nuget.org/downloads](https://nuget.org/downloads) и выберите NuGet 3.3 или более поздней версии (2.8.6 не совместим с моно).</span><span class="sxs-lookup"><span data-stu-id="df29b-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="df29b-103">Рекомендуется всегда использовать последнюю версию, и 4.1.0+ требуется для публикации пакеты в nuget.org.</span><span class="sxs-lookup"><span data-stu-id="df29b-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
2. <span data-ttu-id="df29b-104">Каждый загрузки `nuget.exe` непосредственно.</span><span class="sxs-lookup"><span data-stu-id="df29b-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="df29b-105">Настроить браузер, чтобы сохранить файл в папку по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="df29b-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="df29b-106">Файл *не* в установщик; ничего не отображается, если запустить его непосредственно из браузера.</span><span class="sxs-lookup"><span data-stu-id="df29b-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
3. <span data-ttu-id="df29b-107">Добавить папку, в котором размещена `nuget.exe` в переменную среды PATH использовать средство CLI из любого места.</span><span class="sxs-lookup"><span data-stu-id="df29b-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="df29b-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="df29b-108">macOS/Linux</span></span>
<span data-ttu-id="df29b-109">Поведение может несколько отличаться по распределению ОС.</span><span class="sxs-lookup"><span data-stu-id="df29b-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="df29b-110">Установка [моно 4.4.2 или более поздней версии](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="df29b-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>
2. <span data-ttu-id="df29b-111">Выполните следующие команды в командную строку:</span><span class="sxs-lookup"><span data-stu-id="df29b-111">Execute the following commands at a shell prompt:</span></span>
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. <span data-ttu-id="df29b-112">Создать псевдоним, добавив следующий скрипт к соответствующему файлу для вашей операционной системы (обычно `~/.bash_aliases` или `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="df29b-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. <span data-ttu-id="df29b-113">Перезагрузите оболочки.</span><span class="sxs-lookup"><span data-stu-id="df29b-113">Reload the shell.</span></span>  <span data-ttu-id="df29b-114">Проверьте установку, введя `nuget` без параметров.</span><span class="sxs-lookup"><span data-stu-id="df29b-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="df29b-115">Отображать справку NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="df29b-115">NuGet CLI help should display.</span></span>