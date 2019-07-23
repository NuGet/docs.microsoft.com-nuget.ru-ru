---
title: Устранение неполадок с восстановлением пакетов NuGet в Visual Studio
description: Описание распространенных ошибок восстановления NuGet в Visual Studio и способов их устранения.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 287237cf4041870c562a6a7f48f233d8fdc8ef33
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842388"
---
# <a name="troubleshooting-package-restore-errors"></a>Устранение ошибок при восстановлении пакетов

Эта статья посвящена распространенным ошибкам, возникающим при восстановлении пакетов, и мерам по их устранению. Дополнительные сведения о восстановлении пакетов см. в разделе [Восстановление пакета](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).

Если приведенные здесь инструкции не работают, [сообщите о проблеме на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли тщательнее изучить ваш случай. Не используйте элемент управления "Была ли эта страница полезной?", который может отображаться на этой странице, так как это не позволяет нам связаться с вами для получения дополнительной информации.

## <a name="quick-solution-for-visual-studio-users"></a>Быстрое решение для пользователей Visual Studio

Если вы используете Visual Studio, сначала включите восстановление пакета, как описано ниже. В противном случае перейдите к приведенным далее разделам.

1. Выберите команду **Сервис > Диспетчер пакетов NuGet > Параметры диспетчера пакетов**.
1. Задайте оба параметра в разделе **Восстановление пакета**.
1. Нажмите кнопку **ОК**.
1. Повторите сборку проекта.

![Включите восстановление пакетов NuGet в меню "Сервис", "Параметры".](../consume-packages/media/restore-01-autorestoreoptions.png)

Эти параметры также можно изменить в файле `NuGet.config`; см раздел о [согласии](#consent). Для достаточно ранних проектов, использующих встроенную в MSBuild функцию восстановление пакетов, возможно, потребуется [перейти](package-restore.md#migrate-to-automatic-package-restore-visual-studio) на автоматическое восстановление пакетов.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Данный проект ссылается на пакеты NuGet, отсутствующие на этом компьютере

Полное сообщение об ошибке.

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Эта ошибка возникает при попытке выполнить сборку проекта, содержащего ссылки на один или несколько пакетов NuGet, которые сейчас не установлены на компьютере или в проекте.

- Если используется формат управления PackageReference, эта ошибка означает, что пакет не установлен в папке *global-packages*, как описано в статье [Управление папкой установки глобальных пакетов, кэшем и временными папками](managing-the-global-packages-and-cache-folders.md).
- Если используется файл `packages.config`, эта ошибка означает, что пакет не установлен в папке `packages` в корневом узле решения.

Обычно такая ситуация возникает при получении исходного кода проекта из системы управления версиями или другого скачанного файла. Пакеты обычно исключаются из системы управления версиями или скачиваемых файлов, так как их можно восстановить из веб-каналов пакета, например nuget.org (см. раздел [Пакеты и система управления версиями](Packages-and-Source-Control.md)). Их включение приведет к раздуванию репозитория или созданию слишком больших ZIP-файлов.

Эта ошибка также может возникнуть, если файл проекта содержит абсолютные пути для расположений пакетов и вы перемещаете этот проект.

Для восстановления пакетов используйте один из следующих методов.

- После перемещения файла проекта отредактируйте его напрямую, чтобы обновить ссылки на пакеты.
- Visual Studio — включите восстановление пакетов. Для этого выберите команду меню **Сервис > Диспетчер пакетов NuGet > Параметры диспетчера пакета**, задайте оба параметра в разделе **Восстановление пакета** и нажмите кнопку **ОК**. Выполните сборку решения еще раз.
- CLI dotnet — в командной строке перейдите к папке с проектом, а затем выполните `dotnet restore` или `dotnet build` (автоматический запуск восстановления).
- CLI NuGet. exe — в командной строке перейдите к папке с проектом, а затем выполните команду `nuget restore` (за исключением проектов, созданных с помощью CLI `dotnet`; в этом случае используйте `dotnet restore`).
- Проекты перенесенные в PackageReference — в командной строке выполните команду `msbuild -t:restore`.

После восстановления пакет должен присутствовать в папке *global-packages*. В проектах, использующих формат PackageReference, в процессе восстановления повторно создается файл `obj/project.assets.json`, а в проектах, использующих файл `packages.config`, пакет должен появиться в папке `packages`. Теперь сборка проекта должна пройти без ошибок. В противном случае [сообщите о проблеме на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли связаться с вами.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Файл ресурсов project.assets.json не найден

Полное сообщение об ошибке.

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Если используется формат управления PackageReference, который проверяет, установлены ли на компьютере все необходимые пакеты, в файле `project.assets.json` определена схема зависимостей проекта. Этот файл создается динамически во время восстановления пакета. Поэтому он обычно не добавляется в систему управления версиями. В результате эта ошибка возникает при попытке выполнить сборку проекта с помощью такого средства, как `msbuild`, которое не восстанавливает пакеты автоматически.

В этом случае запустите `msbuild -t:restore` и затем `msbuild` или используйте `dotnet build` (при этом пакеты восстанавливаются автоматически). Кроме того, вы можете использовать любой из методов восстановления пакетов, описанных в [предыдущем разделе](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Необходимо восстановить один пакет NuGet или несколько, но это не удалось выполнить, так как не было получено согласие

Полное сообщение об ошибке.

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Эта ошибка означает, что восстановление пакета отключено в конфигурации NuGet.

Вы можете изменить подходящие параметры в Visual Studio, как описано выше в разделе [Быстрое решение для пользователей Visual Studio](#quick-solution-for-visual-studio-users).

Можно также изменить эти параметры напрямую в соответствующем файле `nuget.config` (обычно это `%AppData%\NuGet\NuGet.Config` в Windows и `~/.nuget/NuGet/NuGet.Config` в Mac и Linux). Убедитесь, что для ключей `enabled` и `automatic` в разделе `packageRestore` задано значение True.

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> При изменении параметров `packageRestore` прямо в `nuget.config` нужно перезапустить Visual Studio, чтобы диалоговое окно параметров отображало текущие значения.

## <a name="other-potential-conditions"></a>Другие потенциальные условия

- Могут возникнуть ошибки сборки, связанные с отсутствием файлов и указывающие, что для их скачивания следует использовать NuGet restore. Но при выполнении команды restore может появиться сообщение "Все пакеты уже установлены, и элементы для восстановления отсутствуют". В этом случае удалите папку `packages` (при использовании `packages.config`) или файл `obj/project.assets.json` (при использовании PackageReference) и запустите restore еще раз. Если это не помогло решить проблему, очистите папку *global-packages* и кэш, выполнив в окне командной строки команду `nuget locals all -clear` или `dotnet locals all --clear`. Дополнительные сведения см. в статье [Управление папкой установки глобальных пакетов, кэшем и временными папками](managing-the-global-packages-and-cache-folders.md).

- При получении проекта из системы управления версиями папки вашего проекта могут быть сделаны доступными только для чтения. Измените разрешения для папок и попробуйте восстановить пакеты еще раз.

- Возможно, вы используете старую версию NuGet. Ознакомьтесь с последними рекомендуемыми версиями на странице [nuget.org/downloads](https://www.nuget.org/downloads). Для Visual Studio 2015 рекомендуется версия 3.6.0.

При возникновении других проблем [сообщите о них на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли получить у вас дополнительные сведения.
