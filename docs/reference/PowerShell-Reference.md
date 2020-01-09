---
title: Справочник по PowerShell для NuGet
description: Полный справочник по командам PowerShell, доступным в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 2a82b1977265a8f8a15247759bc3de80a5efe228
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385347"
---
# <a name="powershell-reference"></a>Справочник по PowerShell

Консоль диспетчера пакетов предоставляет интерфейс PowerShell в Visual Studio для Windows для взаимодействия с NuGet с помощью указанных ниже команд. (Консоль в настоящее время недоступна в Visual Studio для Mac.) Инструкции по использованию консоли см. в разделе [Установка пакетов и управление ими с помощью консоли диспетчера пакетов](../consume-packages/install-use-packages-powershell.md) .

> [!Tip]
> Все команды PowerShell относятся только к потреблению пакетов. Команды PowerShell не связаны с созданием и публикацией пакетов, за исключением того, что пакет также может быть потребителем других пакетов.

> [!Important]
> Приведенные здесь команды относятся только к консоли диспетчера пакетов в Visual Studio и отличаются от [команд модуля Управление пакетами](/powershell/module/packagemanagement/?view=powershell-6) , доступных в общей среде PowerShell. В частности, в каждой среде есть команды, недоступные в другой, а команды с тем же именем могут отличаться в отдельных аргументах. При использовании консоли Управление пакетами в Visual Studio применяются команды и аргументы, описанные в этой статье.

| Общие команды | Описание | Версия NuGet |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Устанавливает пакет и его зависимости в проект. | Все . |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Обновляет пакет и его зависимости или все пакеты в проекте. | Все . |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Выполняет поиск в источнике пакета с помощью идентификатора или ключевых слов. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Возвращает список пакетов, установленных в локальном репозитории, или список пакетов, доступных из источника пакета. | Все . |

| Вторичные команды | Описание | Версия NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Проверяет все сборки в пути вывода для проекта и добавляет перенаправления привязок в `app.config` или `web.config`, если это необходимо. | Все . |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Отображает сведения об указанном по умолчанию или проекте. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Запускает браузер по умолчанию с проектом, лицензией или URL-адресом сообщения о нарушении для указанного пакета. | Не рекомендуется в 3.0 + |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Регистрирует расширение вкладки для параметров команды, позволяя создавать настраиваемые расширения для часто используемых значений параметров. | Все . |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Получение версии установленного пакета из указанного проекта и синхронизация версии с остальными проектами в решении. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Удаляет пакет из проекта, при необходимости удаляя его зависимости. | Все . |

Для получения полной справки по любой из этих команд в консоли просто выполните следующую команду с именем команды.

```ps
Get-Help <command> -full
```

Все команды консоли диспетчера пакетов поддерживают следующие [Общие параметры PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216):

- Отладка
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Подробные сведения
- WarningAction
- WarningVariable

Дополнительные сведения см. в [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216) документации по PowerShell.
