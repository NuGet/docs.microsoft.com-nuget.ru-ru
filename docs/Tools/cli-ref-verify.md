---
title: "NuGet CLI проверьте команду | Документы Microsoft"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Справочник по nuget.exe проверьте команды"
keywords: "NuGet проверить ссылку, проверьте команды"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 2747491eb35d8685a44e86fcc1b572013982c754
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/08/2018
---
# <a name="verify-command-nuget-cli"></a>Проверьте команду (NuGet CLI)

**Применяется к:** пакета потребления &bullet; **поддерживаемые версии:** 4.6 +

Проверка пакета.

## <a name="usage"></a>Использование

```cli
nuget verify <package(s)> [options]
```

где `<package(s)>` одной или нескольких `.nupkg` файлов.

## <a name="options"></a>Параметры

| Параметр | Описание: |
| --- | --- |
| Все | Указывает, что все проверки на возможные должна быть выполнена на пакетов. |
| CertificateFingerprint | Указывает один или несколько отпечатки сертификата SHA-256, какие знаком должен быть подписан с помощью сертификатов (s). Отпечаток сертификата SHA-256 является хэш сертификата SHA-256. Несколько входов должно быть разделенных точкой с запятой. |
| ConfigFile | Файл конфигурации NuGet вступили в силу. Если не указан, *%AppData%\NuGet\NuGet.Config* используется. |
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