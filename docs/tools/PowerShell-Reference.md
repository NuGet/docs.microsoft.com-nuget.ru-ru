---
title: Справочник по PowerShell NuGet
description: Полный справочник команд PowerShell доступны в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: ba9f5dc2b570298d9011f62a081631ec31623701
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817007"
---
# <a name="powershell-reference"></a>Справочник по PowerShell

Консоль диспетчера пакетов предоставляет интерфейс PowerShell в среде Visual Studio в Windows для взаимодействия с помощью NuGet через определенные команды перечисленные ниже. (Консоль недоступна в настоящее время в Visual Studio для Mac.) Руководство по использованию консоли см. в разделе [консоль диспетчера пакетов](../tools/package-manager-console.md) раздела.

> [!Tip]
> Все команды PowerShell относятся только к потребления пакета. Команды PowerShell не связаны с создания и публикации пакеты, за исключением того, при условии, что пакет может быть также потребителя другие пакеты.

> [!Important]
> Команды, перечисленные ниже относятся к консоли диспетчера пакетов в Visual Studio и отличаться от [команды модуля пакета управления](/powershell/module/packagemanagement/?view=powershell-6) , которые доступны в среде PowerShell Общие. В частности каждая среда имеет команд, которые недоступны в другом, а команды с тем же именем в их конкретных аргументах также могут различаться. При использовании консоли управления пакета в Visual Studio, команды и аргументы, описанные в этом разделе присутствует применяются.

| Стандартные команды | Описание: | Версия NuGet |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Устанавливает пакет и его зависимости в проект. | Все |
| [Update-Package](ps-ref-update-package.md) | Обновляет пакет и его зависимости, а также все пакеты в проекте. | Все |
| [Find-Package](ps-ref-find-package.md) | Поиск источника пакета, используя идентификатор пакета или ключевые слова. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Возвращает список пакетов, установленных в локальном хранилище или список пакетов из исходного пакета. | Все |

| Дополнительные команды | Описание: | Версия NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Проверяет все сборки по пути вывода для проекта и добавляет перенаправления привязки `app.config` или `web.config` при необходимости. | Все |
| [Get-Project](ps-ref-get-project.md) | Отображает сведения о значения по умолчанию или указанный проект. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Запускает браузер по умолчанию проекта, лицензии или URL-адрес отчетов о нарушении для указанного пакета. | Рекомендуется использовать в 3.0 + |
| [TabExpansion регистра](ps-ref-register-tabexpansion.md) | Регистрирует расширение по клавише tab для параметров команды, что позволяет создавать пользовательские расширения для значения часто используемых параметров. | Все |
| [Sync-Package](ps-ref-sync-package.md) | Get, установленная версия пакета из указанного проекта и синхронизируется с остальными проектами в решении. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Удаляет пакет из проекта, при необходимости удаления его зависимости. | Все |

Полные и подробные справочные сведения о любой из этих команд в консоли выполните следующую команду с именем команды в вопросе.

```ps
Get-Help <command> -full
```

Все консоли диспетчера пакетов команды поддерживает следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):

- Отладка
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Verbose
- WarningAction
- WarningVariable

Дополнительные сведения см. в [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) в документации по PowerShell.
