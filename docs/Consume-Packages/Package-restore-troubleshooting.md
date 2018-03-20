---
title: "Устранение неполадок с восстановлением пакетов NuGet в Visual Studio | Документы Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Описание распространенных ошибок восстановления NuGet в Visual Studio и способов их устранения."
keywords: "восстановление пакетов NuGet, восстановление пакетов, устранение неполадок, устранение ошибок"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a>Устранение ошибок при восстановлении пакетов

Эта статья посвящена распространенным ошибкам, возникающим при восстановлении пакетов, и мерам по их устранению. Дополнительные сведения о восстановлении пакетов см. в разделе [Восстановление пакета](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Если приведенные здесь инструкции не работают, [сообщите о проблеме на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли тщательнее изучить ваш случай. Не используйте элемент управления "Была ли эта страница полезной?", который может отображаться на этой странице, так как это не позволяет нам связаться с вами для получения дополнительной информации.

## <a name="quick-solution-for-visual-studio-users"></a>Быстрое решение для пользователей Visual Studio

Если вы используете Visual Studio, сначала включите восстановление пакета, как описано ниже. В противном случае перейдите к приведенным далее разделам.

1. Выберите команду **Сервис > Диспетчер пакетов NuGet > Параметры диспетчера пакетов**.
1. Задайте оба параметра в разделе **Восстановление пакета**.
1. Нажмите кнопку **ОК**.
1. Повторите сборку проекта.

![Включите восстановление пакетов NuGet в меню "Сервис", "Параметры".](../consume-packages/media/restore-01-autorestoreoptions.png)

Эти параметры также можно изменить в файле `NuGet.config`; см раздел о [согласии](#consent).

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Данный проект ссылается на пакеты NuGet, отсутствующие на этом компьютере

Полное сообщение об ошибке.

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Эта ошибка возникает при попытке выполнить сборку проекта, содержащего ссылки на один пакет NuGet ли несколько, которые сейчас не кэшированы в проекте. (Пакеты кэшируются в папке `packages` в корне решения, если проект использует `packages.config`, или в файле `obj/project.assets.json`, если проект использует формат PackageReference.)

Обычно такая ситуация возникает при получении исходного кода проекта из системы управления версиями или другого скачанного файла. Пакеты обычно исключаются из системы управления версиями или скачиваемых файлов, так как их можно восстановить из веб-каналов пакета, например nuget.org (см. раздел [Пакеты и система управления версиями](Packages-and-Source-Control.md)). Их включение приведет к раздуванию репозитория или созданию слишком больших ZIP-файлов.

Для восстановления пакетов используйте один из следующих методов.

- В Visual Studio включите восстановление пакетов, выбрав команду **Сервис > Диспетчер пакетов NuGet > Параметры диспетчера пакета**, задав оба параметра в разделе **Восстановление пакета** и нажав кнопку **ОК**. Выполните сборку решения еще раз.
- Для проектов .NET Core запустите `dotnet restore` или `dotnet build` (при этом восстановление запускается автоматически).
- В командной строке запустите `nuget restore` (за исключением проектов, созданных с помощью `dotnet`, для них используйте `dotnet restore`).
- В командной строке с проектами, использующими формат PackageReference, запустите `msbuild /t:restore`.

После успешного восстановления вы должны увидеть либо папку `packages` (при использовании `packages.config`), либо файл `obj/project.assets.json` (при использовании PackageReference). Теперь сборка проекта должна пройти без ошибок. В противном случае [сообщите о проблеме на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли связаться с вами.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Файл ресурсов project.assets.json не найден

Полное сообщение об ошибке.

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Эта ошибка возникает по тем же причинам, которые описаны в [предыдущем разделе](#missing), и устраняется теми же способами. Например, если запустить `msbuild` для проекта .NET Core, который не был получен из системы управления версиями, пакеты не восстанавливаются автоматически. В этом случае запустите `msbuild /t:restore` и затем `msbuild` или используйте `dotnet build` (при этом пакеты восстанавливаются автоматически).

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

Обратите внимание, что при изменении параметров `packageRestore` прямо в `nuget.config` нужно перезапустить Visual Studio, чтобы диалоговое окно параметров отображало текущие значения.

## <a name="other-potential-conditions"></a>Другие потенциальные условия

- Могут возникнуть ошибки сборки, связанные с отсутствием файлов и указывающие, что для их скачивания следует использовать NuGet restore. Но при выполнении команды restore может появиться сообщение "Все пакеты уже установлены, и элементы для восстановления отсутствуют". В этом случае удалите папку `packages` (при использовании `packages.config`) или файл `obj/project.assets.json` (при использовании PackageReference) и запустите restore еще раз.

- При получении проекта из системы управления версиями папки вашего проекта могут быть сделаны доступными только для чтения. Измените разрешения для папок и попробуйте восстановить пакеты еще раз.

- Возможно, вы используете старую версию NuGet. Ознакомьтесь с последними рекомендуемыми версиями на странице [nuget.org/downloads](https://www.nuget.org/downloads). Для Visual Studio 2015 рекомендуется версия 3.6.0.

При возникновении других проблем [сообщите о них на GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues), чтобы мы могли получить у вас дополнительные сведения.