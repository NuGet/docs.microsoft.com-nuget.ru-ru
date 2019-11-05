---
title: Команда NuGet CLI Trusted-Signs
description: Справочные сведения для команды NuGet. exe Trusted-Signs
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610336"
---
# <a name="trusted-signers-command-nuget-cli"></a>Команда Trusted-Signs (интерфейс командной строки NuGet)

Область **применения:** использование пакетов &bullet; **Поддерживаемые версии:** 4.9.1 +

Возвращает или задает доверенных подписывающих для конфигурации NuGet. Дополнительные сведения об использовании см. в разделе [Общие конфигурации NuGet](../../consume-packages/configuring-nuget-behavior.md). Дополнительные сведения о том, как выглядит схема NuGet. config, см. в [справочнике по файлу конфигурации NuGet](../nuget-config-file.md).

## <a name="usage"></a>Использование

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Если ни один из `list|add|remove|sync` не указан, команда по умолчанию будет `list`.

## <a name="nuget-trusted-signers-list"></a>список доверенных-подписывающихй NuGet

Список всех доверенных подписывающих удостоверений в конфигурации. Этот параметр будет включать все сертификаты (с использованием отпечатка пальца и алгоритма отпечатков пальцев) для каждого знака. Если сертификат имеет предыдущее `[U]`, это означает, что запись сертификата `allowUntrustedRoot` задана как `true`.

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

## <a name="nuget-trusted-signers-add-options"></a>NuGet Trusted-Signs Add [параметры]

Добавляет доверенный подписывающий с заданным именем в конфигурацию. Этот параметр имеет разные жесты для добавления доверенного автора или репозитория.

## <a name="options-for-add-based-on-a-package"></a>Параметры для добавления на основе пакета

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

где `<package(s)>` — один или несколько файлов `.nupkg`.

| Параметр | Описание |
| --- | --- |
| Дизайнер | Указывает, что подпись автора пакетов должна быть доверенной. |
| WMI | Указывает, что подпись репозитория или подпись другой стороны пакетов должны быть доверенными. |
| алловунтрустедрут | Указывает, следует ли разрешить сертификату доверенного пользователя связываться с корнем без доверия. |
| Владельцы | Разделенный точками с запятой список доверенных владельцев для дальнейшего ограничения доверия репозитория. Допустимо только при использовании параметра `-Repository`. |

Одновременное предоставление одновременно `-Author` и `-Repository` не поддерживается.

## <a name="options-for-add-based-on-a-service-index"></a>Параметры для добавления на основе индекса службы

```cli
nuget trusted-signers add -Name <name> [options]
```

_Примечание_. при выборе этого варианта будут добавлены только доверенные репозитории. 

| Параметр | Описание |
| --- | --- |
| сервицеиндекс | Указывает индекс службы для доверенного репозитория версии 3. Этот репозиторий должен поддерживать ресурс подписей репозитория. Если этот параметр не указан, команда будет искать источник пакета с тем же `-Name` и получить индекс службы. |
| алловунтрустедрут | Указывает, следует ли разрешить сертификату доверенного пользователя связываться с корнем без доверия. |
| Владельцы | Разделенный точками с запятой список доверенных владельцев для дальнейшего ограничения доверия репозитория. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Параметры для добавления на основе сведений о сертификате

```cli
nuget trusted-signers add -Name <name> [options]
```

_Примечание_. Если доверенный подписывающий с данным именем уже существует, элемент сертификата будет добавлен в этот подписывающий. В противном случае доверенный автор будет создан с помощью элемента сертификата из указанных сведений о сертификате.

| Параметр | Описание |
| --- | --- |
| CertificateFingerprint | Указывает отпечатки сертификата сертификата, для которого подписанные пакеты должны быть подписаны. Отпечаток сертификата — это хэш сертификата. Хэш-алгоритм, используемый для вычисления этого хэша, должен быть указан в параметре `FingerprintAlgorithm`. |
| финжерпринталгорисм | Указывает хэш-алгоритм, используемый для вычисления отпечатка сертификата. По умолчанию — `SHA256`. Поддерживаются значения `SHA256`, `SHA384` и `SHA512` |
| алловунтрустедрут | Указывает, следует ли разрешить сертификату доверенного пользователя связываться с корнем без доверия. |

## <a name="nuget-trusted-signers-remove--name-name"></a>NuGet Trusted-подписывающийs удалите-Name \<имя\>

Удаляет все доверенные подписывающих, соответствующие заданному имени.

## <a name="nuget-trusted-signers-sync--name-name"></a>имя \<доверенных подписывающих NuGet-имя\>

Запрашивает последний список сертификатов, используемых в доверенном репозитории, чтобы обновить существующий список сертификатов в доверенном подписавшем.

_Примечание_. Этот жест удалит текущий список сертификатов и заменит их актуальным списком из репозитория.

## <a name="options"></a>Параметры

| Параметр | Описание |
| --- | --- |
| ConfigFile | Файл конфигурации NuGet, который необходимо применить. Если не указано, используется `%AppData%\NuGet\NuGet.Config` (Windows) или `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| форцеенглишаутпут | Принудительное выполнение NuGet. exe с использованием инвариантного языка и региональных параметров, основанных на английском языке. |
| Справка | Отображает справочные сведения для команды. |
| Уровень детализации | Задает объем сведений, отображаемых в выходных данных: *нормальный*, *тихий*, *подробный*. |

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
