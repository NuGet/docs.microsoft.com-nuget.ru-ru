---
title: Команда проверки интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238144"
---
# <a name="verify-command-nuget-cli"></a>Команда "проверить" (интерфейс командной строки NuGet)

Область **применения:** &bullet; **Поддерживаемые версии** для использования пакетов: 4.6 +

Проверяет пакет.

Проверка подписанных пакетов пока не поддерживается в Mono.

## <a name="usage"></a>Использование

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

где `<package(s)>` — один или несколько `.nupkg` файлов.

## <a name="nuget-verify--all"></a>Проверка NuGet — все

Указывает, что для пакетов нужно выполнить все возможные проверки.

## <a name="nuget-verify--signatures"></a>Проверка NuGet — подписи

Указывает, что необходимо выполнить проверку подписи пакета.

## <a name="options-for-verify--signatures"></a>Параметры для «Verify-Signatures»

- **`-CertificateFingerprint`**

  Указывает один или несколько отпечатков сертификатов SHA-256 сертификатов, которые подписанные пакеты должны быть подписаны. Отпечаток сертификата SHA-256 — это хэш сертификата SHA-256. Несколько входов должны быть разделены точкой с запятой.

## <a name="options"></a>Параметры

- **`-ConfigFile`**

  Файл конфигурации NuGet, который необходимо применить. Если не указано, `%AppData%\NuGet\NuGet.Config` используется (Windows) или `~/.nuget/NuGet/NuGet.Config` или `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.

- **`-?|-help`**

  Отображает справочные сведения для команды.

- **`-NonInteractive`**

  Подавляет запросы на ввод или подтверждение пользователя.

- **`-Verbosity [normal|quiet|detailed]`**

  Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .

## <a name="examples"></a>Примеры

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```