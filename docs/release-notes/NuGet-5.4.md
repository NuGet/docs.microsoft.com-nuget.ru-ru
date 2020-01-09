---
title: Заметки о выпуске NuGet 5,4
description: Заметки о выпуске NuGet 5,4, включая новые функции, исправления ошибок и DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384115"
---
# <a name="nuget-54-release-notes"></a>Заметки о выпуске NuGet 5,4

Средства распространения NuGet:

| Версия NuGet | Доступно в версии Visual Studio| Доступно в пакетах SDK для .NET|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 версии 16,4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Устанавливается вместе с Visual Studio 2019 с рабочей нагрузкой .NET Core

## <a name="summary-whats-new-in-54"></a>Сводка: новые возможности в 5,4

* Более быстрое время загрузки решения — накладные расходы на выполнение кода NuGet во время первой загрузки решения были сокращены с помощью частичного генератора NGen для сокращения затрат на JIT- [#6007](https://github.com/NuGet/Home/issues/6007)

* Новая вспомогательная функция — для получения списка идентификаторов пакетов и версий следует получить вероятные пакеты верхнего уровня. - [#8316](https://github.com/NuGet/Home/issues/8316)

* Новое [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) действие для установки и настройки NuGet. exe в [действиях GitHub](https://github.com/features/actions). - [#8818](https://github.com/NuGet/Home/issues/8818)

### <a name="issues-fixed-in-this-release"></a>Исправленные ошибки в этом выпуске

**Ошибки**

* Подключаемый модуль: неправильное время ведения журнала в Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)

* Удаление подключаемого модуля иногда может вызвать и завершить всю операцию. - [#8732](https://github.com/NuGet/Home/issues/8732)

* Больше не отображать дубликаты версий в списке разрешенных и заблокированных версий в ПМУИ- [#8679](https://github.com/NuGet/Home/issues/8679)

* Файл блокировки создан неправильно. Упорядочивание платформы не должно влиять на восстановление с помощью локкедмоде- [#8645](https://github.com/NuGet/Home/issues/8645)

* Сбой проверки Локкфиле для проектов с набором <RuntimeIdentifiers> в пакете SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)

* Теперь при проверке подписи будут правильно отклоняться подписи с метками времени, которые имеют 2 значения в одном OID- [#8629](https://github.com/NuGet/Home/issues/8629)

* Обновление списка лицензий — [#8544](https://github.com/NuGet/Home/issues/8544)

**DCR**

* Адаптация файлов диагностики в Ифидбаккдиагностикфилепровидер — [#8535](https://github.com/NuGet/Home/issues/8535)

**[Список всех проблем, исправленных в этом выпуске — 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
