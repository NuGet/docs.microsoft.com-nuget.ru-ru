---
title: Заметки о выпуске версии 1.7 NuGet
description: Заметки о выпуске для NuGet 1.7, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551471"
---
# <a name="nuget-17-release-notes"></a>Заметки о выпуске версии 1.7 NuGet

[Заметки о выпуске NuGet 1.6](../release-notes/nuget-1.6.md) | [заметки о выпуске NuGet 1.8](../release-notes/nuget-1.8.md)

NuGet 1.7 было выпущено 4 апреля 2012 г.

## <a name="known-installation-issue"></a>Известные проблемы
Если вы используете VS 2010 SP1, вы можете столкнуться ошибка установки при попытке обновить NuGet, если у вас установлена более ранняя версия.

Обойти это просто удалить диспетчер NuGet, а затем установить его из коллекции расширений VS.  Дополнительные сведения см. в разделе [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

Примечание: Если Visual Studio не позволяют удалить расширение (кнопка "Удалить" отключена), скорее всего, потребуется перезапустить Visual Studio, используя «Запуск от имени администратора».

## <a name="features"></a>Функции

### <a name="support-opening-readmetxt-file-after-installation"></a>Поддержка открытия файла readme.txt после установки
Новые возможности в 1.7, если пакет содержит `readme.txt` файл в корне пакета, NuGet автоматически откроется в этот файл после завершения установки пакета.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Показать пакеты предварительного выпуска в диалоговом окне пакеты NuGet, управление
Диалоговое окно Управление пакетами NuGet теперь включает раскрывающийся список, который предоставляет параметр, чтобы показать пакеты предварительного выпуска.

![Отображаются пакеты предварительного выпуска](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Показать кнопку восстановить пакет, если отсутствуют файлы пакета
При открытии консоли диспетчера пакетов или пакетов Manager NuGet диалоговое окно, NuGet будет проверять, если текущее решение включил режим восстановление пакета, и если все файлы пакета отсутствуют `packages` папки. Если эти два условия выполняются, NuGet уведомим вас и покажет удобный кнопки "Восстановить". После нажатия этой кнопки будет активировать NuGet восстановить все отсутствующие пакеты.

![Кнопка восстановления пакета в диалоговом окне](./media/packagerestore-dialog.png)

![Кнопка восстановления пакета на консоли](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Добавьте файл packages.config уровня решения
В предыдущих версиях NuGet, каждый проект имеет `packages.config` файл, который отслеживает установки пакетов NuGet в этом проекте. Тем не менее возникла не похожих файлов на уровне решения для отслеживания пакеты уровня решения. Таким образом нельзя было восстановить пакеты уровня решения.
Эта функция теперь реализована в NuGet 1.7. Уровня решения `packages.config` файл помещается в `.nuget` папки в рамках решения root и сохранит только решение на уровне пакетов.

### <a name="remove-new-package-command"></a>Удалить команду New-Package
Из-за низкой загрузке удалена команда New-Package. Разработчикам рекомендуется использовать nuget.exe или под рукой обозреватель пакетов NuGet для создания пакетов.

## <a name="bug-fixes"></a>Исправления ошибок
NuGet 1.7 исправил множество ошибок вокруг восстановление пакета рабочих процессов и сценариев сети или системы управления версиями.

Полный список рабочих элементов исправленные в NuGet 1.7, пожалуйста представление [Issue Tracker NuGet для этого выпуска](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
