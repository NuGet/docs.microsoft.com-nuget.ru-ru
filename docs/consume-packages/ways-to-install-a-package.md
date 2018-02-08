---
title: "Способы установки пакетов NuGet | Документация Майкрософт"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/30/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "В этой статье описывается процесс установки пакетов NuGet в проект, включая процессы на диске и все происходящее с применимыми файлами проекта."
keywords: "установка NuGet, использование пакета NuGet, установка пакетов NuGet, ссылки на пакеты NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e48bbe813168e773bc46b7fe25af29785ff75df
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Способы установки пакета NuGet

Пакеты NuGet можно загрузить и установить с помощью любого из методов ниже (если клиентские инструменты NuGet не установлены, [ознакомьтесь с инструкциями по их установке](../install-nuget-client-tools.md)).

| Метод | Описание: |
| --- | --- |
| Интерфейс командной строки dotnet.exe<br/>`dotnet install <package_name>` | (Для всех платформ.) Скачивает пакет, определенный атрибутом \<package_name\>, и развертывает его содержимое в папку в текущем каталоге, а затем добавляет ссылку в файл проекта. Кроме того, скачивает и устанавливает зависимости.<ul><li>[Установка и использование пакета (dotnet CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[Команды dotnet](../tools/dotnet-commands.md)</li></ul> |
| Пользовательский интерфейс диспетчера пакетов (Visual Studio) | (Для компьютеров с Windows и Mac.) Пользовательский интерфейс для обзора, выбора и установки пакетов и их зависимостей в проект. Добавляет ссылки на установленные пакеты в файл проекта.<ul><li>[Установка и использование пакета (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Справочник по пользовательскому интерфейсу диспетчера пакетов для компьютеров с Windows](../tools/package-manager-ui.md)</li><li>[Включение пакета NuGet в проект](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Консоль диспетчера пакетов (Visual Studio)<br/>`Install-Package <package_name>` | (Только для компьютеров с Windows.) Загружает и устанавливает пакет, определенный атрибутом \<package_name\>, в указанный проект в решении, а затем добавляет ссылку в файл проекта. Кроме того, скачивает и устанавливает зависимости.<ul><li>[Установка и использование пакета (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Руководство по консоли диспетчера пакетов](../tools/package-manager-console.md)</li></ul> |
| Интерфейс командной строки nuget.exe<br/>`nuget install <package_name>` | (Для всех платформ.) Скачивает пакет, определенный атрибутом \<package_name\>, и развертывает его содержимое в папку в текущем каталоге. Может также скачивать все пакеты, перечисленные в файле `packages.config`. Загружает и устанавливает зависимости, но не вносит никаких изменений в файлы проекта.<ul><li>[Команда install](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>Общий процесс установки

В целом при запросе установить пакет NuGet выполняет следующее:

1. Получает сам пакет:
    - Проверяет наличие запрошенного пакета в кэше (сведения см. в статье [Управление кэшем NuGet](managing-the-nuget-cache.md)).
    - Если пакета нет в кэше, предпринимается попытка загрузить его из источников, перечисленных в файлах конфигурации, начиная с первого в списке. Такое поведение позволит использовать закрытые каналы пакета перед его поиском на nuget.org (сведения см. в статье [Настройка поведения NuGet](configuring-nuget-behavior.md)).
    - При успешном получении пакета из одного из источников NuGet добавит его в кэш. В противном случае установка завершится ошибкой.

1. Развертывает пакет в проект.
    - Развертывание означает распаковку содержимого пакета в соответствующую вложенную папку. Копия самого файла `.nupkg` также помещается во вложенную папку.
    - Если пакет устанавливается в проект Visual Studio или .NET Core, развертываются только файлы, относящиеся к требуемой версии .NET Framework проекта. При установке с помощью командной строки nuget.exe развертываются все сборки.

1. При установке пакета в Visual Studio или интерфейс командной строки dotnet ссылка добавляется в соответствующий файл проекта (или файл `packages.config` для некоторых типов проектов в Visual Studio).

## <a name="related-topics"></a>См. также

- [Общие сведения и процесс использования пакетов](../consume-packages/overview-and-workflow.md)
- [Поиск и выбор пакетов](../consume-packages/finding-and-choosing-packages.md)
- [Настройка поведения NuGet](../consume-packages/configuring-nuget-behavior.md)
- [Управление кэшем NuGet](managing-the-nuget-cache.md)
