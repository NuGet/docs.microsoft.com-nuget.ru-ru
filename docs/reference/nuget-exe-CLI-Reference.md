---
title: Справочник по интерфейсу командной строки (CLI) NuGet
description: Указатель ссылок командной строки для CLI NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 52aa2c533a8b67ae10455888a34a7ac9767fd0e3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327471"
---
# <a name="nuget-cli-reference"></a>Справочник по CLI NuGet

Интерфейс командной строки NuGet (CLI) `nuget.exe`предоставляет полную область функций NuGet для установки, создания, публикации пакетов и управления ими без внесения изменений в файлы проекта.

Чтобы использовать любую команду, Откройте командное окно или оболочку Bash, затем `nuget` выполните команду, а затем выберите соответствующие параметры, `nuget help pack` например (для просмотра справки по команде Pack).

В этой документации отражается последняя версия интерфейса командной строки NuGet. Для получения точных сведений о любой конкретной версии, которую вы используете, `nuget help` выполните команду для нужной команды.

Сведения об использовании основных команд с CLI `nuget.exe` см. в статье [Установка и использование пакета с помощью CLI nuget.exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Установка NuGet. exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Сведения о том, как сделать интерфейс командной строки NuGet доступным в консоли диспетчера пакетов в Visual Studio, см. [в разделе Использование интерфейса командной строки NuGet. exe в консоли](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Доступность

Точные сведения см. в разделе [доступность функций](../install-nuget-client-tools.md#feature-availability) .

- Все команды доступны в Windows.
- Все команды работают с NuGet. exe, работающей на Mono, за `pack`исключением тех `update`случаев, когда указаны для, `restore`и.
- `pack`Команды, `restore`, `delete` ,и`push` также доступны в Mac и Linux с помощью интерфейса командной строки DotNet. `locals`

## <a name="commands-and-applicability"></a>Команды и применимость

Доступные команды и применимость для создания пакета, потребления пакетов и (или) публикации пакета на узле:

| Общие команды | Применимые роли | Версия NuGet | Описание |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | Создать | 2.7+ | Создает пакет NuGet из `.nuspec` файла проекта или. При выполнении на Mono создание пакета из файла проекта не поддерживается. |
| [push](cli-reference/cli-ref-push.md) | Публикация | Все | Публикует пакет в источнике пакета. |
| [config](cli-reference/cli-ref-config.md) | Все | Все | Возвращает или задает значения конфигурации NuGet. |
| [help or ?](cli-reference/cli-ref-help.md) | Все | Все | Отображает справочные сведения или справку для команды. |
| [locals](cli-reference/cli-ref-locals.md) | Потребление | 3.3+ | Перечисляет расположения папок *Global-Packages*, *HTTP-Cache*и *TEMP* и очищает содержимое этих папок. |
| [restore](cli-reference/cli-ref-restore.md) | Потребление | 2.7+ | Восстанавливает все пакеты, на которые ссылается используемый формат управления пакетами. При выполнении на Mono восстановление пакетов с использованием формата PackageReference не поддерживается. |
| [setapikey](cli-reference/cli-ref-setapikey.md) | Публикация, использование | Все | Сохраняет ключ API для данного источника пакета, если для этого источника пакета требуется ключ для доступа. |
| [spec](cli-reference/cli-ref-spec.md) | Создать | Все | `.nuspec` Создает файл, используя токены при создании файла из проекта Visual Studio. |

| Вторичные команды | Применимые роли | Версия NuGet | Описание |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | Публикация | 3.3+ | Добавляет пакет в источник пакета, отличный от HTTP, с помощью иерархического макета. Для источников HTTP используйте *Push*. |
| [delete](cli-reference/cli-ref-delete.md) | Публикация | Все | Удаляет пакет из источника пакета или выводит из него список. |
| [init](cli-reference/cli-ref-init.md) | Создать | 3.3+ | Добавляет пакеты из папки в источник пакета с помощью иерархического макета. |
| [install](cli-reference/cli-ref-install.md) | Потребление | Все | Устанавливает пакет в текущий проект, но не изменяет проекты или справочные файлы. |
| [list](cli-reference/cli-ref-list.md) | Потребление, возможно, публикация | Все | Отображает пакеты из заданного источника. |
| [mirror](cli-reference/cli-ref-mirror.md) | Публикация | Не рекомендуется в 3.2 + | Отражает пакет и его зависимости от источника к целевому репозиторию. |
| [sources](cli-reference/cli-ref-sources.md) | Потребление, публикация | Все | Управляет источниками пакетов в файлах конфигурации. |
| [update](cli-reference/cli-ref-update.md) | Потребление | Все | Обновляет пакеты проекта до последних доступных версий. Не поддерживается при выполнении на Mono. |

Различные команды используют различные [переменные среды](cli-reference/cli-ref-environment-variables.md).

Команды интерфейса командной строки NuGet по применимым ролям:

| Роль | Команды |
| --- | --- |
| Потребление | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Создать | `config`, `help`, `init`, `pack`, `spec` |
| Публикация | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Разработчики, заинтересованные только в использовании пакетов, например, должны понимать только подмножество команд NuGet.

> [!Note]
> В именах параметров команд регистр не учитывается. Нерекомендуемые параметры не включаются в `NoPrompt` эту ссылку, например (заменены на `NonInteractive`) и `Verbose` (заменены на `Verbosity`).
