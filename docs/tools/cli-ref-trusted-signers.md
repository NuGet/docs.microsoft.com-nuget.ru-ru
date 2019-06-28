---
title: Доверенные подписавших команды интерфейса командной строки NuGet
description: Справочник по командам доверенные подписавших nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c22c7f0a6b6878bec4f8396e02e2d97998170455
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425985"
---
# <a name="trusted-signers-command-nuget-cli"></a>Команда доверенного подписавших (NuGet CLI)

**Применяется к:** упаковать потребления &bullet; **поддерживаемые версии:** 4.9.1+

Возвращает или задает доверенных подписавших конфигурации NuGet. Избыточное использование см. в разделе [NuGet распространенных конфигураций](../consume-packages/configuring-nuget-behavior.md). Дополнительные сведения о как схема nuget.config, как выглядит, см. [ссылку на файл конфигурации NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Использование

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Если ни один из `list|add|remove|sync` указан, команда по умолчанию будет `list`.

## <a name="nuget-trusted-signers-list"></a>список доверенных подписавших NuGet

Список всех доверенных авторов в конфигурации. Этот параметр будет включать все сертификаты (с помощью отпечатков пальцев и алгоритм отпечатков пальцев) у каждого подписывающего. Если сертификат имеет предшествующий `[U]`, это означает, что запись сертификат имеет `allowUntrustedRoot` задать в качестве `true`.

Ниже приведен пример выходных данных этой команды:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>доверенные подписавших NuGet add [параметры]

Добавляет доверенным лицом, с заданным именем в файле конфигурации. Этот параметр может иметь разные жесты Добавление доверенных автора или репозитория.

## <a name="options-for-add-based-on-a-package"></a>Параметры установки, на основе пакета

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

где `<package(s)>` — это один или несколько `.nupkg` файлов.

| Параметр | Описание |
| --- | --- |
| Дизайнер | Указывает, что автор подписи пакетов должен быть доверенным. |
| WMI | Указывает, что репозиторий подпись или скрепляющая подпись из пакетов должен быть доверенным. |
| AllowUntrustedRoot | Указывает, если сертификат доверенным лицом должны создать недоверенный корневой цепочку. |
| Владельцы | Разделенный точками с запятой список доверенных владельцев для дальнейшего ограничения доверительные отношения с репозиторием. Допустимо только при использовании `-Repository` параметр. |

Одновременное предоставление `-Author` и `-Repository` в то же время не поддерживается.

## <a name="options-for-add-based-on-a-service-index"></a>Параметры установки, на основе индекса службы

```cli
nuget trusted-signers add -Name <name> [options]
```

_Примечание_. Этот параметр будет добавлять только доверенных репозиториев. 

| Параметр | Описание |
| --- | --- |
| ServiceIndex | Указывает индекс службы V3 репозитория доверенными. Этот репозиторий содержит для поддержки ресурса подписи репозитория. Если не указано, команда будет искать источник пакета с тем же `-Name` и получить индекс службы оттуда. |
| AllowUntrustedRoot | Указывает, если сертификат доверенным лицом должны создать недоверенный корневой цепочку. |
| Владельцы | Разделенный точками с запятой список доверенных владельцев для дальнейшего ограничения доверительные отношения с репозиторием. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Параметры установки, в зависимости от сведений о сертификате

```cli
nuget trusted-signers add -Name <name> [options]
```

_Примечание_. Если доверенным лицом, с заданным именем уже существует, будет добавлен элемент сертификат для этого подписавшего. В противном случае будет создан доверенным автора с элементом сертификата из определенных сведений о сертификате.

| Параметр | Описание |
| --- | --- |
| CertificateFingerprint | Указывает сертификат, который должен быть подписан отпечатков сертификата, который подписанных пакетов. Отпечаток сертификата — это хэш сертификата. Задает алгоритм хэширования, используемый для вычисления этого хэш-кода должен быть в `FingerprintAlgorithm` параметр. |
| FingerprintAlgorithm | Задает алгоритм хэширования, используемый для вычисления отпечаток сертификата. По умолчанию — `SHA256`. Поддерживаемые значения `SHA256`, `SHA384` и `SHA512` |
| AllowUntrustedRoot | Указывает, если сертификат доверенным лицом должны создать недоверенный корневой цепочку. |

## <a name="nuget-trusted-signers-remove--name-name"></a>удалить доверенный подписавших NuGet - имя <name>

Удаляет все доверенных авторов, которые соответствуют заданному имени.

## <a name="nuget-trusted-signers-sync--name-name"></a>синхронизировать доверенные подписавших NuGet - имя <name>

Запрашивает обновленный список сертификатов, используемых в настоящее время доверенного хранилища для обновления существующего списка сертификатов в доверенным лицом.

_Примечание_. Этот жест будет удалить текущий список сертификатов и замените их список актуальных из репозитория.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Чтобы применить файл конфигурации NuGet. Если не указан, `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` используется (Mac/Linux).|
| ForceEnglishOutput | Nuget.exe силы для выполнения с помощью инвариантный, основанное на английский язык и региональные параметры. |
| Help | Отображает справку для команды. |
| Verbosity | Указывает объем сведений, в выходных данных: *обычный*, *quiet*, *подробные*. |

## <a name="examples"></a>Примеры

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
