---
title: Управление глобальными пакетами, кэшем и временными папками в NuGet
description: Сведения об управлении папкой установки глобальных пакетов, кэшем и временными папками на компьютере, которые используются при установке, восстановлении и обновлении пакетов.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: 354a8ec80e2ba20abe27746dec8c8aaae9b6c96c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="2af99-103">Управление папкой установки глобальных пакетов, кэшем и временными папками</span><span class="sxs-lookup"><span data-stu-id="2af99-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="2af99-104">После каждой установки, обновления или восстановления NuGet управляет пакетами и сведениями о них в нескольких папках за пределами структуры проекта:</span><span class="sxs-lookup"><span data-stu-id="2af99-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="2af99-105">name</span><span class="sxs-lookup"><span data-stu-id="2af99-105">Name</span></span> | <span data-ttu-id="2af99-106">Описание и расположение (в зависимости от пользователя)</span><span class="sxs-lookup"><span data-stu-id="2af99-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="2af99-107">global&#8209;packages</span><span class="sxs-lookup"><span data-stu-id="2af99-107">global&#8209;packages</span></span> | <span data-ttu-id="2af99-108">В папку *global-packages* NuGet устанавливает любой загруженный пакет.</span><span class="sxs-lookup"><span data-stu-id="2af99-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="2af99-109">Каждый пакет полностью развертывается во вложенную папку, соответствующую идентификатору пакета и номеру версии.</span><span class="sxs-lookup"><span data-stu-id="2af99-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="2af99-110">Проекты в формате PackageReference всегда используют пакеты непосредственно из этой папки.</span><span class="sxs-lookup"><span data-stu-id="2af99-110">Projects using the PackageReference format always use packages directly from this folder.</span></span> <span data-ttu-id="2af99-111">При использовании `packages.config` пакеты устанавливаются в папку *global-packages*, а затем копируются папку проекта `packages`.</span><span class="sxs-lookup"><span data-stu-id="2af99-111">When using the `packages.config`, packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="2af99-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="2af99-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="2af99-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="2af99-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="2af99-114">Переопределяет с помощью переменной среды NUGET_PACKAGES [параметры конфигурации](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` или `repositoryPath` (при использовании PackageReference и `packages.config` соответственно) или свойство MSBuild `RestorePackagesPath` (только MSBuild).</span><span class="sxs-lookup"><span data-stu-id="2af99-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="2af99-115">Переменная среды имеет приоритет над параметром конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2af99-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="2af99-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="2af99-116">http&#8209;cache</span></span> | <span data-ttu-id="2af99-117">Диспетчер пакетов Visual Studio (NuGet 3.x +) и `dotnet` инструмент хранят копии загруженных пакетов в этом кеше (сохраненные как `.dat` файла), организованные в подпапки для каждого источника пакета.</span><span class="sxs-lookup"><span data-stu-id="2af99-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="2af99-118">Пакеты не развернуты. Срок действия кэша составляет 30 минут.</span><span class="sxs-lookup"><span data-stu-id="2af99-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="2af99-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="2af99-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="2af99-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="2af99-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="2af99-121">Переопределяет с помощью переменной среды NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="2af99-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="2af99-122">temp</span><span class="sxs-lookup"><span data-stu-id="2af99-122">temp</span></span> | <span data-ttu-id="2af99-123">Папка, в которой NuGet хранит временные файлы, используемые в различных операциях.</span><span class="sxs-lookup"><span data-stu-id="2af99-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="2af99-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="2af99-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="2af99-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="2af99-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="2af99-126">NuGet 3.5 и более ранних версий использует папку *packages-cache* вместо *http-cache*, которая находится по следующему пути: `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="2af99-126">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="2af99-127">Использование кэша и папок *global-packages* позволяет NuGet избежать скачивания пакетов, хранящихся на компьютере, что в свою очередь улучшает производительность операций установки, обновления и восстановления.</span><span class="sxs-lookup"><span data-stu-id="2af99-127">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="2af99-128">При использовании формата PackageReference папка *global-packages* также позволяет избежать хранения скачанных пакетов в папках проектов, откуда их можно случайно добавить в систему управления версиями. Кроме того, это снижает общее влияние NuGet на ресурсы хранилища компьютера.</span><span class="sxs-lookup"><span data-stu-id="2af99-128">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="2af99-129">При запросе на извлечение пакета NuGet в первую очередь проверяет папку *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="2af99-129">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="2af99-130">Если не удается найти точную версию пакета, NuGet проверяет все источники пакетов, отличные от HTTP.</span><span class="sxs-lookup"><span data-stu-id="2af99-130">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="2af99-131">Если пакет отсутствует и там, NuGet ищет его в папке *http-cache*, если вы не указали с помощью команды `dotnet.exe` параметр `--no-cache` или с помощью команды `nuget.exe` параметр `-NoCache`.</span><span class="sxs-lookup"><span data-stu-id="2af99-131">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="2af99-132">Если пакет отсутствует в кэше или кэш не используется, NuGet извлекает пакет по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="2af99-132">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="2af99-133">Дополнительные сведения см. в разделе [Процесс установки пакета](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span><span class="sxs-lookup"><span data-stu-id="2af99-133">For more information, see [What happens when a package is installed](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="2af99-134">Просмотр расположения папок</span><span class="sxs-lookup"><span data-stu-id="2af99-134">Viewing folder locations</span></span>

<span data-ttu-id="2af99-135">Расположения папок можно просмотреть с помощью команды [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="2af99-135">You can view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="2af99-136">Типичные выходные данные выглядят следующим образом (Mac/Linux; user1 —это имя текущего пользователя):</span><span class="sxs-lookup"><span data-stu-id="2af99-136">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
```

<span data-ttu-id="2af99-137">Чтобы отобразить расположение отдельной папки, используйте `http-cache`, `global-packages` или `temp`, а не `all`.</span><span class="sxs-lookup"><span data-stu-id="2af99-137">To display the location of a single folder, use `http-cache`, `global-packages`, or `temp` instead of `all`.</span></span> 

<span data-ttu-id="2af99-138">Расположение можно также просмотреть с помощью команды [nuget locals](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="2af99-138">You also view locations using the [nuget locals command](../tools/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, cache, and temp
nuget locals all -list
```

<span data-ttu-id="2af99-139">Типичные выходные данные выглядят следующим образом (Windows; user1 —это имя текущего пользователя):</span><span class="sxs-lookup"><span data-stu-id="2af99-139">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
```

<span data-ttu-id="2af99-140">(Папка `package-cache` используется в NuGet 2.x. Ее содержимое можно посмотреть с помощью NuGet 3.5 и более ранних версий.)</span><span class="sxs-lookup"><span data-stu-id="2af99-140">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="2af99-141">Очистка локальных папок</span><span class="sxs-lookup"><span data-stu-id="2af99-141">Clearing local folders</span></span>

<span data-ttu-id="2af99-142">Если при установке пакета возникают неполадки или вы по иной причине хотите обеспечить установку пакетов из удаленной коллекции, используйте параметр `locals --clear` (dotnet.exe) или `locals -clear` (nuget.exe), с помощью которых можно указать конкретную папку, которую нужно очистить, или параметр `all`, чтобы очистить все папки:</span><span class="sxs-lookup"><span data-stu-id="2af99-142">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="2af99-143">Все пакеты, которые в настоящее время открыты в проектах Visual Studio, нельзя удалить из папки *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="2af99-143">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="2af99-144">В Visual Studio 2017 в меню **Инструменты > Диспетчер пакетов NuGet > Параметры диспетчера пакетов** выберите **Clear All NuGet Cache(s)** (Очистить весь кэш NuGet).</span><span class="sxs-lookup"><span data-stu-id="2af99-144">In Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="2af99-145">Сейчас управлять кэшем через консоль диспетчера пакетов нельзя.</span><span class="sxs-lookup"><span data-stu-id="2af99-145">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="2af99-146">В Visual Studio 2015 используйте вместо этого команды CLI.</span><span class="sxs-lookup"><span data-stu-id="2af99-146">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Команды очистки кэша NuGet](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="2af99-148">Ошибки и способы их устранения</span><span class="sxs-lookup"><span data-stu-id="2af99-148">Troubleshooting errors</span></span>

<span data-ttu-id="2af99-149">При использовании `nuget locals` или `dotnet nuget locals` могут возникать следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="2af99-149">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="2af99-150">*Ошибка: процесс не может получить доступ к файлу <package>, поскольку этот файл используется другим процессом* или *При удалении локальных ресурсов произошел сбой: не удалось удалить один файл (или несколько)*</span><span class="sxs-lookup"><span data-stu-id="2af99-150">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="2af99-151">Один или несколько файлов в папке используются другим процессом, например открыт проект Visual Studio, который ссылается на пакеты в папке *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="2af99-151">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="2af99-152">Закройте эти процессы и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="2af99-152">Close those processes and try again.</span></span>

- <span data-ttu-id="2af99-153">*Ошибка: доступ к пути "<path>" запрещен* или *Каталог не пуст*</span><span class="sxs-lookup"><span data-stu-id="2af99-153">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="2af99-154">Отсутствуют разрешения на удаление файлов в кэше.</span><span class="sxs-lookup"><span data-stu-id="2af99-154">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="2af99-155">Измените разрешения папки, если это возможно, и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="2af99-155">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="2af99-156">В противном случае обратитесь к системному администратору.</span><span class="sxs-lookup"><span data-stu-id="2af99-156">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="2af99-157">*Ошибка: указанный путь, имя файла или оба значения имеют слишком большую длину. Полное имя файла должно содержать меньше 260 символов, а имя каталога — меньше 248 символов*</span><span class="sxs-lookup"><span data-stu-id="2af99-157">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="2af99-158">Сократите имена папок и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="2af99-158">Shorten the folder names and try again.</span></span>
