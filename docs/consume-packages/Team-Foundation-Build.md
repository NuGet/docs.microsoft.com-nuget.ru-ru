---
title: Пошаговое руководство по восстановлению пакетов NuGet с помощью сборки Team Foundation
description: Пошаговое руководство по восстановлению пакетов NuGet с помощью сборки Team Foundation (Team Foundation Server и Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "73611001"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Настройка восстановления пакетов с помощью сборки Team Foundation

В этой статье приводится подробное пошаговое руководство по восстановлению пакетов в рамках [сборки Team Services](/vsts/build-release/index) как для Git, так и для управления версиями Team Services.

Хотя это руководство относится к сценарию использования Visual Studio Team Services, основные принципы также применимы к другим системам управления версиями и сборки.

Область применения:

- пользовательским проектам MSBuild, выполняющимся в любой версии Team Foundation Server;
- Team Foundation Server 2012 или более ранней версии;
- пользовательским шаблонам процесса сборки Team Foundation, перенесенным в Team Foundation Server 2013 или более поздней версии;
- шаблонам процесса сборки с удаленными возможностями восстановления NuGet.

Если вы используете службы Visual Studio Team Services или сервер Team Foundation Server 2013 с шаблонами процесса сборки, автоматическое восстановление пакетов производится в рамках процесса сборки.

## <a name="the-general-approach"></a>Общий подход

Преимущество использования NuGet в том, что вы можете избежать возврата двоичных файлов в систему управления версиями.

Это особенно полезно в том случае, если вы применяете [распределенную систему управления версиями](https://en.wikipedia.org/wiki/Distributed_revision_control), такую как GIT, так как в этом случае разработчикам приходится клонировать весь репозиторий, включая полный журнал, прежде чем приступать к работе на локальных компьютерах. Возврат двоичных файлов может привести к существенному раздуванию репозитория, так как двоичные файлы обычно хранятся без разностного сжатия.

В NuGet уже давно поддерживается [восстановление пакетов](../consume-packages/package-restore.md) в процессе сборки. В предыдущих реализациях возникала дилемма курицы и яйца в случае, если пакетам необходимо было расширить процесс сборки, так как в NuGet пакеты восстанавливались во время сборки проекта. Платформа MSBuild не позволяет расширять сборку во время ее выполнения. Кто-то может посчитать это недостатком MSBuild, однако это спорный вопрос. В зависимости от аспекта, который необходимо расширить, к моменту восстановления пакета регистрировать его может быть уже слишком поздно.

Решением этой проблемы может быть восстановление пакетов на первом этапе процесса сборки.

```cli
nuget restore path\to\solution.sln
```

Если пакеты восстанавливаются перед сборкой кода, вам не нужно возвращать файлы `.targets`.

> [!Note]
> Пакеты должны быть созданы так, чтобы их можно было загружать в Visual Studio. В противном случае может потребоваться возвращать файлы `.targets`, чтобы другие разработчики могли просто открывать решение, предварительно не восстанавливая пакеты.

В приведенном ниже демонстрационном проекте показано, как настроить сборку таким образом, чтобы папки `packages` и файлы `.targets` не нужно было возвращать. Кроме того, показано, как настроить автоматическую сборку в Team Foundation Service для этого образца проекта.

## <a name="repository-structure"></a>Структура репозитория

Демонстрационный проект представляет собой простую программу командной строки, которая использует аргумент командной строки для запроса Bing. Он предназначен для платформы .NET Framework 4 и использует многие [пакеты библиотеки BCL](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async) и [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).

Репозиторий имеет следующую структуру:

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

Как вы видите, мы не вернули папку `packages` и файлы `.targets`.

Однако мы вернули файл `nuget.exe`, так как он нужен во время сборки. Согласно общепринятым соглашениям мы вернули его в общую папку `tools`.

Исходный код находится в папке `src`. Хотя в примере используется только одно решение, можно легко представить себе, что эта папка содержит несколько решений.

### <a name="ignore-files"></a>Пропуск файлов

> [!Note]
> В клиенте NuGet в настоящее время есть [известная ошибка](https://nuget.codeplex.com/workitem/4072), из-за которой клиент все же добавляет папку `packages` в систему управления версиями. Обходным решением является отключение интеграции с системой управления версиями. Для этого в папке `Nuget.Config `, которая находится в том же каталоге, что и решение, должен быть файл `.nuget`. Если этой папки еще нет, создайте ее. В файл [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) добавьте следующее содержимое:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Чтобы сообщить системе управления версиями, что мы не намереваемся возвращать папки **пакетов**, мы также добавили файлы игнорирования как для GIT (`.gitignore`), так и для системы управления версиями Team Foundation (`.tfignore`). В этих файлах описываются шаблоны файлов, которые не нужно возвращать.

Файл `.gitignore` выглядит следующим образом:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

Возможности файла `.gitignore`[весьма широки](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Например, если вы не хотите возвращать все содержимое папки `packages`, но хотите вернуть файлы `.targets`, можно вместо этого использовать следующее правило:

    packages
    !packages/**/*.targets

При этом исключаются все папки `packages`, но включаются все содержащиеся в них файлы `.targets`. Кстати, шаблон файлов `.gitignore`, специально предназначенный для потребностей разработчиков Visual Studio, можно найти [здесь](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Система управления версиями Team Foundation поддерживает очень похожий механизм посредством файлов [TFIGNORE](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control). Синтаксис практически такой же:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

В примере процесс сборки будет достаточно прост. Мы создадим проект MSBuild, который будет выполнять сборку всех решений, проверяя перед этим, восстановлены ли пакеты.

Этот проект будет иметь три стандартные цели: `Clean`, `Build` и `Rebuild`, а также новую цель `RestorePackages`.

- Цели `Build` и `Rebuild` зависят от `RestorePackages`. Таким образом, вы сможете выполнять `Build` и `Rebuild`, будучи уверенными в том, что пакеты восстановлены.
- `Clean`, `Build` и `Rebuild` вызывают соответствующую цель MSBuild для всех файлов решения.
- Цель `RestorePackages` вызывает программу `nuget.exe` для каждого файла решения. Для этого применяется [функция пакетной обработки MSBuild](/visualstudio/msbuild/msbuild-batching).

Результат выглядит следующим образом:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a>Настройка Team Build

Team Build предлагает различные шаблоны процессов. Для этой демонстрации мы используем Team Foundation Service. В локальных установках Team Foundation Server процесс очень похож.

Шаблоны Team Build для GIT и системы управления версиями Team Foundation различаются, поэтому дальнейшие действия зависят от того, какую из этих систем вы используете. В обоих случаях вам просто нужно выбрать build.proj в качестве проекта, сборку которого требуется выполнить.

Сначала рассмотрим шаблон процесса для GIT. В шаблоне на основе GIT сборка выбирается с помощью свойства `Solution to build`.

![Процесс сборки для GIT](media/PackageRestoreTeamBuildGit.png)

Имейте в виду, что это свойство указывает на расположение в вашем репозитории. Так как в нашем случае файл `build.proj` находится в корневой папке, мы просто использовали значение `build.proj`. Если бы файл сборки находился в папке `tools`, значение было бы `tools\build.proj`.

В шаблоне для системы управления версиями Team Foundation проект выбирается с помощью свойства `Projects`.

![Процесс сборки для системы управления версиями Team Foundation](media/PackageRestoreTeamBuildTFVC.png)

В отличие от шаблона на основе GIT, система управления версиями Team Foundation поддерживает средство выбора (кнопка с многоточием справа). Поэтому, чтобы избежать ошибок при вводе, мы рекомендуем воспользоваться им для выбора проекта.
