---
title: Заметки о выпуске версии NuGet 4.7 RTM
description: Заметки о выпуске для NuGet 4.7.0, включая известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 2290025d42dcd5704b6b019c17346201fe6a990d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "76813797"
---
# <a name="nuget-47-release-notes"></a>Заметки о выпуске NuGet 4.7

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает в себя [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-470"></a>Сводка: Новые возможности версии 4.7.0

* Усовершенствовано подписывание пакетов: теперь поддерживаются [пакеты с подписями репозитория](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* В Visual Studio версии 15.7 мы реализовали возможность [переноса существующих проектов, которые используют формат packages.config вместо PackageReference](../consume-packages/migrate-packages-config-to-package-reference.md).

## <a name="summary-whats-new-in-472"></a>Сводка: Новые возможности версии 4.7.2

* Исправление безопасности: разрешения на файлы, созданные внутри ~/.nuget, слишком открыты [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-473"></a>Сводка: Новые возможности версии 4.7.3

* Исправление безопасности: файлы внутри NUPKG могут иметь относительный путь выше каталога NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Известные проблемы

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>Параметр `Migrate packages.config to PackageReference...` недоступен в контекстном меню, которое открывается по щелчку правой кнопкой мыши

#### <a name="issue"></a>Проблемы

При первом открытии проект NuGet не удается инициализировать до выполнения операции NuGet. В результате параметр миграции не отображается в контекстном меню, которое открывается по щелчку правой кнопкой мыши `packages.config` или `References`.

#### <a name="workaround"></a>Возможное решение

Выполните одно из следующих действий NuGet:
* Откройте пользовательский интерфейс диспетчера пакетов. Для этого щелкните правой кнопкой мыши `References` и выберите `Manage NuGet Packages...`.
* Откройте консоль диспетчера пакетов. В `Tools > NuGet Package Manager` выберите `Package Manager Console`.
* Запустите восстановление NuGet. Для этого щелкните правой кнопкой мыши узел решения в обозревателе решений и выберите `Restore NuGet Packages`.
* Создайте проект, активизирующий восстановление NuGet.

Теперь параметр миграции должен отобразиться. Обратите внимание, что этот параметр не поддерживается и не будет отображаться для типов проектов ASP.NET и C++.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Проблемы с .NET Standard 2.0, связанные с .NET Framework и NuGet

Платформа .NET Standard и ее инструментарий были разработаны таким образом, чтобы проекты, предназначенные для .NET Framework 4.6.1, могли использовать пакеты NuGet и проекты, предназначенные для .NET Standard 2.0 или более ранних версий. [В этом документе](https://github.com/dotnet/standard/issues/481) кратко описаны проблемы, связанные с таким сценарием, план их решения, а также обходные пути, которые можно применить в текущем состоянии.

## <a name="top-issues-fixed-in-this-release"></a>Основные ошибки, исправленные в этом выпуске

### <a name="bugs"></a>Ошибки

* NuGet достигает взаимоблокировки в системе проектов .Net Core (новая регрессия). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Пакет: PackagePath создается неправильно при использовании TfmSpecificPackageFile с путями глобализации — [#6726](https://github.com/NuGet/Home/issues/6726)
* Пакет: проект веб-API не может создать пакет, если явно не указать ispackable. - [#6156](https://github.com/NuGet/Home/issues/6156)
* Пользовательский интерфейс VS и PMC отображает новый пакет через 30 минут (nuget.exe отображает его сразу) — [#6657](https://github.com/NuGet/Home/issues/6657)
* Подписи.  SignatureUtility.GetCertificateChain(...) не проверяет все состояния цепочки — [#6565](https://github.com/NuGet/Home/issues/6565)
* Подписи: улучшение обработки DER GeneralizedTime — [#6564](https://github.com/NuGet/Home/issues/6564)
* Подписи. VS не отображает ошибку NU3002 при установке подделанного пакета — [#6337](https://github.com/NuGet/Home/issues/6337)
* Для lockFile.GetLibrary учитывается регистр — [#6500](https://github.com/NuGet/Home/issues/6500)
* Операции установки или обновления кода восстановления и восстановления путей кода не соответствуют — [#3471](https://github.com/NuGet/Home/issues/3471)
* ComboBox версии решения PackageManager поддерживает выбор разделителя с помощью клавиатуры — [#2606](https://github.com/NuGet/Home/issues/2606)
* Не удалось загрузить индекс службы для источника `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: код состояния ответа не указывает на успешное выполнение: 403 (Запрещено) — [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>Запросы на изменение структуры

* Выведение заголовка X-NuGet-Session-Id для обеспечения корреляции между запросами [предлагаемая функция] — [#5330](https://github.com/NuGet/Home/issues/5330)
* Раскрытие способа ожидания выполнения операции восстановления, запущенной в Visual Studio через интерфейс API векторов инициализации. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe: -NoServiceEndpoint позволяет избежать добавления суффикса URL-адреса службы — [#6586](https://github.com/NuGet/Home/issues/6586)
* Добавление хэша фиксации к информационной версии — [#6492](https://github.com/NuGet/Home/issues/6492)
* Подписи: включение удаления подписи или подписи другой стороны репозитория — [#6646](https://github.com/NuGet/Home/issues/6646)
* Подписи.  API для удаления подписи или подписи другой стороны репозитория — [#6589](https://github.com/NuGet/Home/issues/6589)
* Включение в журнал сведений об источнике в VS — [#6527](https://github.com/NuGet/Home/issues/6527)
* Фильтрация для папки /tools только в TFM и RID, чтобы параметры XML можно было включить в папку /tools — [#6197](https://github.com/NuGet/Home/issues/6197)
* Предупреждение, когда команда упаковывания исключает файл, который начинается с .  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Список всех ошибок, исправленных в этом выпуске](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
