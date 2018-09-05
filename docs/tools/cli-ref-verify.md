---
title: Интерфейс командной строки NuGet проверьте команду
description: Справочник по nuget.exe проверьте команду
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545217"
---
# <a name="verify-command-nuget-cli"></a>Команда verify (NuGet CLI)

**Применяется к:** упаковать потребления &bullet; **поддерживаемые версии:** 4.6 или более поздней

Проверяет ли пакет.

Проверка подписанных пакетов еще не поддерживается в .NET Core, в рамках проекта Mono или на платформах, отличных от Windows.

## <a name="usage"></a>Использование

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

где `<package(s)>` — это один или несколько `.nupkg` файлов.

## <a name="nuget-verify--all"></a>проверить NuGet — все

Указывает, что все возможные проверки, необходимые должна выполняться на пакеты.

## <a name="nuget-verify--signatures"></a>NuGet проверки - сигнатур

Указывает, что должна быть выполнена проверка подписи пакета.

## <a name="options-for-verify--signatures"></a>Параметры для «verify - подписей»

| Параметр | Описание |
| --- | --- |
| CertificateFingerprint | Указывает один или несколько отпечатков сертификата SHA-256, какие подписанные пакеты должны быть подписаны с помощью сертификатов (s). Отпечаток сертификата SHA-256 — это хэш SHA-256 сертификата. Несколько наборов входных данных должно быть разделенных точкой с запятой. |

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Чтобы применить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| ForceEnglishOutput | Nuget.exe силы для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Справка | Отображает справку для команды. |
| Уровень детализации | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

## <a name="examples"></a>Примеры

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```