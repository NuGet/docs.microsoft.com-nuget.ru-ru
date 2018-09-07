---
title: Управление глобальными пакетами, кэшем и временными папками в NuGet
description: Сведения об управлении папкой установки глобальных пакетов, кэшем и временными папками на компьютере, которые используются при установке, восстановлении и обновлении пакетов.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: c547ae1d46079d040d7c3aa4c7678e70cd199dce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548017"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Управление папкой установки глобальных пакетов, кэшем и временными папками

После каждой установки, обновления или восстановления NuGet управляет пакетами и сведениями о них в нескольких папках за пределами структуры проекта:

| name | Описание и расположение (в зависимости от пользователя)|
| --- | --- |
| global&#8209;packages | В папку *global-packages* NuGet устанавливает любой загруженный пакет. Каждый пакет полностью развертывается во вложенную папку, соответствующую идентификатору пакета и номеру версии. Проекты в формате PackageReference всегда используют пакеты непосредственно из этой папки. При использовании `packages.config` пакеты устанавливаются в папку *global-packages*, а затем копируются папку проекта `packages`.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Переопределяет с помощью переменной среды NUGET_PACKAGES [параметры конфигурации](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` или `repositoryPath` (при использовании PackageReference и `packages.config` соответственно) или свойство MSBuild `RestorePackagesPath` (только MSBuild). Переменная среды имеет приоритет над параметром конфигурации.</li></ul> |
| http&#8209;cache | Диспетчер пакетов Visual Studio (NuGet 3.x +) и `dotnet` инструмент хранят копии загруженных пакетов в этом кеше (сохраненные как `.dat` файла), организованные в подпапки для каждого источника пакета. Пакеты не развернуты. Срок действия кэша составляет 30 минут.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Переопределяет с помощью переменной среды NUGET_HTTP_CACHE_PATH.</li></ul> |
| temp | Папка, в которой NuGet хранит временные файлы, используемые в различных операциях.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| plugins-cache **4.8+** | Папка, в которой NuGet хранит результаты запросов на утверждение операций.<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>Переопределите с помощью переменной среды NUGET_PLUGINS_CACHE_PATH.</li></ul> |

> [!Note]
> NuGet 3.5 и более ранних версий использует папку *packages-cache* вместо *http-cache*, которая находится по следующему пути: `%localappdata%\NuGet\Cache`.

Использование кэша и папок *global-packages* позволяет NuGet избежать скачивания пакетов, хранящихся на компьютере, что в свою очередь улучшает производительность операций установки, обновления и восстановления. При использовании формата PackageReference папка *global-packages* также позволяет избежать хранения скачанных пакетов в папках проектов, откуда их можно случайно добавить в систему управления версиями. Кроме того, это снижает общее влияние NuGet на ресурсы хранилища компьютера.

При запросе на извлечение пакета NuGet в первую очередь проверяет папку *global-packages*. Если не удается найти точную версию пакета, NuGet проверяет все источники пакетов, отличные от HTTP. Если пакет отсутствует и там, NuGet ищет его в папке *http-cache*, если вы не указали с помощью команды `dotnet.exe` параметр `--no-cache` или с помощью команды `nuget.exe` параметр `-NoCache`. Если пакет отсутствует в кэше или кэш не используется, NuGet извлекает пакет по протоколу HTTP.

Дополнительные сведения см. в разделе [Процесс установки пакета](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).

## <a name="viewing-folder-locations"></a>Просмотр расположения папок

Расположение можно просмотреть с помощью команды [nuget locals](../tools/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Типичные выходные данные выглядят следующим образом (Windows; user1 —это имя текущего пользователя):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(Папка `package-cache` используется в NuGet 2.x. Ее содержимое можно посмотреть с помощью NuGet 3.5 и более ранних версий.)

Расположения папок можно также просмотреть с помощью команды [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):

```cli
dotnet nuget locals all --list
```

Типичные выходные данные выглядят следующим образом (Mac/Linux; user1 —это имя текущего пользователя):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Чтобы отобразить расположение отдельной папки, используйте `http-cache`, `global-packages`, `temp` или `plugins-cache`, а не `all`.

## <a name="clearing-local-folders"></a>Очистка локальных папок

Если при установке пакета возникают неполадки или вы по иной причине хотите обеспечить установку пакетов из удаленной коллекции, используйте параметр `locals --clear` (dotnet.exe) или `locals -clear` (nuget.exe), с помощью которых можно указать конкретную папку, которую нужно очистить, или параметр `all`, чтобы очистить все папки:

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

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Все пакеты, которые в настоящее время открыты в проектах Visual Studio, нельзя удалить из папки *global-packages*.

В Visual Studio 2017 в меню **Инструменты > Диспетчер пакетов NuGet > Параметры диспетчера пакетов** выберите **Clear All NuGet Cache(s)** (Очистить весь кэш NuGet). Сейчас управлять кэшем через консоль диспетчера пакетов нельзя. В Visual Studio 2015 используйте вместо этого команды CLI.

![Команды очистки кэша NuGet](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Ошибки и способы их устранения

При использовании `nuget locals` или `dotnet nuget locals` могут возникать следующие ошибки:

- *Ошибка: процесс не может получить доступ к файлу <package>, поскольку этот файл используется другим процессом* или *При удалении локальных ресурсов произошел сбой: не удалось удалить один файл (или несколько)*

    Один или несколько файлов в папке используются другим процессом, например открыт проект Visual Studio, который ссылается на пакеты в папке *global-packages*. Закройте эти процессы и повторите попытку.

- *Ошибка: доступ к пути "<path>" запрещен* или *Каталог не пуст*

    Отсутствуют разрешения на удаление файлов в кэше. Измените разрешения папки, если это возможно, и повторите попытку. В противном случае обратитесь к системному администратору.

- *Ошибка: указанный путь, имя файла или оба значения имеют слишком большую длину. Полное имя файла должно содержать меньше 260 символов, а имя каталога — меньше 248 символов*

    Сократите имена папок и повторите попытку.
