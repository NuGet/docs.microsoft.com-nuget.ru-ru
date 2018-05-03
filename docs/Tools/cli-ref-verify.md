---
title: Команда проверьте NuGet CLI
description: Справочник по nuget.exe проверьте команды
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c2c31b71358bc50a1fb9aab8905c279cd1235b07
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2018
---
# <a name="verify-command-nuget-cli"></a>Проверьте команду (NuGet CLI)

**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 4.6 +

Проверка пакета.

Проверка подписанных пакетов еще не поддерживается в .NET Core в Mono, так и на платформах, отличных от Windows.

## <a name="usage"></a>Использование

```cli
nuget verify <package(s)> [options]
```

где `<package(s)>` одной или нескольких `.nupkg` файлов.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| Все | Указывает, что все проверки на возможные должна быть выполнена на пакетов. |
| CertificateFingerprint | Указывает один или несколько отпечатки сертификата SHA-256, какие знаком должен быть подписан с помощью сертификатов (s). Отпечаток сертификата SHA-256 является хэш сертификата SHA-256. Несколько входов должно быть разделенных точкой с запятой. |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac и Linux).|
| ForceEnglishOutput | Принудительно nuget.exe выполняется с использованием инвариантных, на основе английского языка и региональных параметров. |
| Справка | Отображает справку по команде. |
| Неинтерактивные | Подавление для ввода данных и подтверждений. |
| Сигнатуры | Указывает, что должна быть выполнена проверка подписи пакета. |
| Уровень детализации | Указывает объем сведений в выходных данных: *обычного*, *тихий*, *подробные*. |

## <a name="examples"></a>Примеры

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```