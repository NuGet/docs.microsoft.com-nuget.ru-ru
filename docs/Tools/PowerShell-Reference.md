---
title: "Справочник по PowerShell NuGet | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: "Полный справочник команд PowerShell доступны в консоли диспетчера пакетов NuGet в Visual Studio."
keywords: "Консоли пакета NuGet диспетчера, команд NuGet Powershell, справочник по NuGet Powershell"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0da5c88447784fdd49d824bbd03b11f73c22ebc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-reference"></a>Справочник по PowerShell

Консоль диспетчера пакетов предоставляет интерфейс PowerShell в среде Visual Studio в Windows для взаимодействия с помощью NuGet через определенные команды перечисленные ниже. (Консоль недоступна в настоящее время в Visual Studio для Mac.) Руководство по использованию консоли см. в разделе [консоль диспетчера пакетов](../tools/package-manager-console.md) раздела.

> [!Tip]
> Все команды PowerShell относятся только к потребления пакета. Команды PowerShell не связаны с создания и публикации пакеты, за исключением того, при условии, что пакет может быть также потребителя другие пакеты.

> [!Important]
> Команды, перечисленные ниже относятся к консоли диспетчера пакетов в Visual Studio и отличаться от [команды модуля пакета управления](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement) , которые доступны в среде PowerShell Общие. В частности каждая среда имеет команд, которые недоступны в другом, а команды с тем же именем в их конкретных аргументах также могут различаться. При использовании консоли управления пакета в Visual Studio, команды и аргументы, описанные в этом разделе присутствует применяются.

| Стандартные команды | Описание | Версия NuGet |
| --- | --- | --- |
| [Пакет установки](ps-ref-install-package.md) | Устанавливает пакет и его зависимости в проект. | Все |
| [Пакет обновления](ps-ref-update-package.md) | Обновляет пакет и его зависимости, а также все пакеты в проекте. | Все |
| [Find-Package](ps-ref-find-package.md) | Поиск источника пакета, используя идентификатор пакета или ключевые слова. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Возвращает список пакетов, установленных в локальном хранилище или список пакетов из исходного пакета. | Все |

| Дополнительные команды | Описание | Версия NuGet |
| --- | --- | --- |
| [Добавить BindingRedirect](ps-ref-add-bindingredirect.md) | Проверяет все сборки по пути вывода для проекта и добавляет перенаправления привязки `app.config` или `web.config` при необходимости. | Все |
| [Get проект](ps-ref-get-project.md) | Отображает сведения о значения по умолчанию или указанный проект. | 3.0+ |
| [Откройте PackagePage](ps-ref-open-packagepage.md) | Запускает браузер по умолчанию проекта, лицензии или URL-адрес отчетов о нарушении для указанного пакета. | Рекомендуется использовать в 3.0 + |
| [TabExpansion регистра](ps-ref-register-tabexpansion.md) | Регистрирует расширение по клавише tab для параметров команды, что позволяет создавать пользовательские расширения для значения часто используемых параметров. | Все |
| [Синхронизация пакета](ps-ref-sync-package.md) | Get, установленная версия пакета из указанного проекта и синхронизируется с остальными проектами в решении. | 3.0+ |
| [Удаление пакета](ps-ref-uninstall-package.md) | Удаляет пакет из проекта, при необходимости удаления его зависимости. | Все |

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
