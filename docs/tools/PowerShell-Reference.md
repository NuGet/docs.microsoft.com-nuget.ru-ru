---
title: Справочник по PowerShell NuGet
description: Полный справочник команд PowerShell, доступных в консоли диспетчера пакетов NuGet в Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 45c8be9956ceaab844bdcd89f1b96adc256f805c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546668"
---
# <a name="powershell-reference"></a>Справочник по PowerShell

Консоль диспетчера пакетов предоставляет интерфейс PowerShell в Visual Studio для Windows для взаимодействия с NuGet через определенные команды перечисленные ниже. (Консоль не является в настоящее время доступен в Visual Studio для Mac.) Руководство по использованию консоли, см. в разделе [консоль диспетчера пакетов](../tools/package-manager-console.md) раздела.

> [!Tip]
> Все команды PowerShell относятся только к использование пакета. Команды PowerShell, не связаны с создания и публикации пакетов, за исключением того, при условии, что пакет также может быть объект-получатель другие пакеты.

> [!Important]
> Команды, перечисленные ниже относятся к консоли диспетчера пакетов в Visual Studio и отличаться от [команды модуля пакета управления](/powershell/module/packagemanagement/?view=powershell-6) , доступные в общей среде PowerShell. В частности каждая среда имеет команд, которые недоступны в другой, и команды с одинаковым именем также может отличаться в их определенных аргументов. При использовании консоли управления пакетами в Visual Studio, применить команды и аргументы, описанные в этом разделе.

| Общие команды | Описание | Версия NuGet |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Устанавливает пакет и его зависимости в проект. | Все |
| [Update-Package](ps-ref-update-package.md) | Обновляет пакет и его зависимостей или все пакеты в проекте. | Все |
| [Find-Package](ps-ref-find-package.md) | Выполняет поиск источника пакета, используя ключевые слова или идентификатор пакета. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Извлекает список пакетов, установленных в локальном репозитории, или список пакетов из источника пакета. | Все |

| Дополнительные команды | Описание | Версия NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Проверяет все сборки по пути вывода проекта и добавляет переадресацию привязок к `app.config` или `web.config` там, где необходимо. | Все |
| [Get-Project](ps-ref-get-project.md) | Отображает сведения о по умолчанию или указанный проект. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Запускает браузер по умолчанию проекта, лицензий или URL-адрес отчета о нарушении для указанного пакета. | Рекомендуется использовать в 3.0 + |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | Регистрирует расширение функций клавиши tab для параметров команды, что позволяет создавать настраиваемые расширения для значения часто используемых параметров. | Все |
| [Sync-Package](ps-ref-sync-package.md) | Get, установленная версия пакета из указанного проекта и синхронизирует версии для остальных проектов в решении. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Удаляет пакет из проекта, при необходимости удаления его зависимости. | Все |

Исчерпывающую получить справку по любой из этих команд в консоли просто выполните следующую команду с именем команды в вопросе.

```ps
Get-Help <command> -full
```

Все команды консоли диспетчера пакетов поддерживают следующие [Общие параметры PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):

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
