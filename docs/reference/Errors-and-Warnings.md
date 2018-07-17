---
title: NuGet ошибки и предупреждения ссылку
description: Полный справочник для предупреждения и ошибки, выданные NuGet при выполнении различных операций NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: a787d036f7682b54adb30140152655fe165ee161
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39069665"
---
# <a name="errors-and-warnings"></a>Ошибки и предупреждения

В NuGet 4.3.0+ ошибки и предупреждения нумеруются, как описано в этом разделе и предоставляют подробные сведения помогут вам решить проблемы, связанные.

Ошибки и предупреждения, перечисленные здесь доступны только с [на базе PackageReference](../consume-packages/package-references-in-project-files.md) проектов и NuGet 4.3.0+. NuGet также учитывает свойства MSBuild для подавления предупреждений или повысить их уровень до ошибок. Дополнительные сведения см. в разделе [как: отключение предупреждений компилятора](/visualstudio/ide/how-to-suppress-compiler-warnings) в документации по Visual Studio.

**Ошибки**

| Группа | Номера ошибок |
| --- | --- |
| Недопустимый ошибки ввода | [NU1001](./errors-and-warnings/NU1001.md), [NU1002](./errors-and-warnings/NU1002.md), [NU1003](./errors-and-warnings/NU1003.md) |
| Отсутствуют ошибки пакетов и проектов | [NU1100](./errors-and-warnings/NU1100.md), [NU1101](./errors-and-warnings/NU1101.md), [NU1102](./errors-and-warnings/NU1102.md), [NU1103](./errors-and-warnings/NU1103.md), [NU1104](./errors-and-warnings/NU1104.md), [NU1105](./errors-and-warnings/NU1105.md), [NU1106](./errors-and-warnings/NU1106.md), [NU1107](./errors-and-warnings/NU1107.md), [NU1108](./errors-and-warnings/NU1108.md) |
| Ошибки совместимости | [NU1201](./errors-and-warnings/NU1201.md), [NU1202](./errors-and-warnings/NU1202.md), [NU1203](./errors-and-warnings/NU1203.md), [NU1401](./errors-and-warnings/NU1401.md) |
| Внутренние ошибки NuGet | [NU1000](./errors-and-warnings/NU1000.md) |
| Ошибки подписанные пакеты (создания и проверки) | [NU3000](./errors-and-warnings/NU3000.md), [NU3001](./errors-and-warnings/NU3001.md), [NU3004](./errors-and-warnings/NU3004.md), [NU3008](./errors-and-warnings/NU3008.md) |

**Предупреждения**

| Группа | Номера предупреждений |
| --- | --- |
| Недопустимый входной предупреждения | [NU1501](./errors-and-warnings/NU1501.md), [NU1502](./errors-and-warnings/NU1502.md), [NU1503](./errors-and-warnings/NU1503.md) |
| Непредвиденная пакета версии предупреждения | [NU1601](./errors-and-warnings/NU1601.md), [NU1602](./errors-and-warnings/NU1602.md), [NU1603](./errors-and-warnings/NU1603.md), [NU1604](./errors-and-warnings/NU1604.md), [NU1605](./errors-and-warnings/NU1605.md), [NU1606](./errors-and-warnings/NU1108.md), [NU1607](./errors-and-warnings/NU1107.md) |
| Сопоставитель конфликтов предупреждения | [NU1608](./errors-and-warnings/NU1608.md) |
| Резервный предупреждения пакетов | [NU1701](./errors-and-warnings/NU1701.md) |
| Предупреждения веб-канала | [NU1801](./errors-and-warnings/NU1801.md) |
| Внутренние предупреждения; NuGet | [NU1500](./errors-and-warnings/NU1500.md) |
| Подписанные пакеты предупреждения (создания и проверки) | [NU3002](./errors-and-warnings/NU3002.md), [NU3018](./errors-and-warnings/NU3018.md), [NU3028](./errors-and-warnings/NU3028.md) |
