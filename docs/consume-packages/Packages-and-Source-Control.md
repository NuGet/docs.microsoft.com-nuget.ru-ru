---
title: Пакеты NuGet и система управления версиями
description: Вопросы, касающиеся обработки пакетов NuGet в системах управления версиями и исходным кодом, а также пропуска пакетов с TFVC и GIT.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 0338c3445b2a3d8169158171d97d1e874533a80a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551803"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Пропуск пакетов NuGet в системах управления исходным кодом

Разработчики обычно пропускают пакеты NuGet из своих репозиториев управления исходным кодом и вместо этого полагаются на [восстановление пакетов](package-restore.md) для переустановки зависимостей проекта перед сборкой.

К причинам использования восстановления пакетов относятся следующие:

1. Распределенные системы управления версиями, такие как Git, включают полные копии каждой версии каждого файла в репозитории. Часто обновляемые двоичные файлы приводят к значительному раздуванию и увеличивают время, необходимое для клонирования репозитория.
1. При включении пакетов в репозиторий разработчики должны добавлять ссылки непосредственно на содержимое пакета на диске, а не ссылаться на пакеты с помощью NuGet, что может привести к наличию в проекте жестко заданных путей.
1. Становится все труднее очистить решение от неиспользуемых папок пакетов, так как при этом нужно не удалить используемые папки пакетов.
1. Опуская пакеты, вы обеспечиваете четкие границы владения между вашим кодом и чужими пакетами, от которых вы зависите. Многие пакеты NuGet уже находятся в их собственных репозиториях управления исходным кодом.

Несмотря на то, что NuGet восстанавливает пакеты по умолчанию, чтобы пропустить некоторые из них, а именно папки `packages` в проекте, в системе управления исходным кодом требуется выполнить некоторые операции вручную, как описано в этой статье.

## <a name="omitting-packages-with-git"></a>Пропуск пакетов в Git

Используйте файл [.gitignore ](https://git-scm.com/docs/gitignore), чтобы игнорировать пакеты NuGet (`.nupkg`) `packages` папки и `project.assets.json`, среди прочего. Для справки см. [ образец `.gitignore` для проектов Visual Studio ](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

Далее приведены важные части файла `.gitignore`:

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>Пропуск пакетов в системе управления версиями Team Foundation

> [!Note]
> По возможности выполните эти инструкции *перед* добавлением проекта в систему управления исходным кодом. В противном случае вручную удалите папку `packages` из репозитория и верните это изменение, прежде чем продолжить.

Отключение интеграции системы управления исходным кодом с TFVC для выбранных файлов:

1. Создайте папку с именем `.nuget` в папке решения (где находится файл `.sln`).
    - Совет. Чтобы создать эту папку в проводнике Windows, используйте имя `.nuget.` *с* конечной точкой.

1. В этой папке создайте файл с именем `NuGet.Config` и откройте его для редактирования.

1. Добавьте хотя бы следующий текст, где параметр [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) предписывает Visual Studio пропустить все содержимое папки `packages`:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. Если вы используете TFS 2010 или более ранней версии, замаскируйте папку `packages` в сопоставлениях рабочей области.

1. В TFS 2012 и более поздней версии или Visual Studio Team Services создайте файл `.tfignore`, как описано в статье [Добавление файлов на сервер](/vsts/tfvc/add-files-server.md?view=vsts#tfignore). Включите в этот файл приведенное ниже содержимое, чтобы явно игнорировать изменения в папке `\packages` на уровне репозитория и нескольких других промежуточных файлах. (Вы можете создать файл в проводнике Windows, используя имя `.tfignore.` с конечной точкой, но сначала вам может потребоваться отключить параметр "Hide known file extensions" (Скрыть известные расширения файлов).)

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Добавьте `NuGet.Config` и `.tfignore` в систему управления исходным кодом и верните изменения.
