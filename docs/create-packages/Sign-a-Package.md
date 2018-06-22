---
title: Подписывание пакетов NuGet
description: Описание того, как подписанные пакеты можно использовать, чтобы включить проверку целостности содержимого.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9900db1970a89de129d9074e5900e0aa048101de
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449608"
---
# <a name="signing-nuget-packages"></a>Подписывание пакетов NuGet

Подписывание пакета — это процесс, который гарантирует, что пакет не был изменен с момента создания.

## <a name="prerequisites"></a>Предварительные требования

1. Пакет (файл `.nupkg`) для подписывания. См. статью [Создание пакета](creating-a-package.md).

1. nuget.exe 4.6.0 или более поздней версии. См. статью [Установка интерфейса командной строки NuGet](../install-nuget-client-tools.md#nugetexe-cli).

1. [Сертификат подписывания кода](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

## <a name="sign-a-package"></a>Подписывание пакета

Чтобы подписать пакет, используйте [nuget sign](../tools/cli-ref-sign.md).

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Как описано в справочнике по командам, можно использовать сертификат, доступный в хранилище сертификатов, или сертификат из файла.

### <a name="common-problems-when-signing-a-package"></a>Распространенные проблемы при подписывании пакета

- Недопустимый сертификат для подписывания кода. Убедитесь, что указанный сертификат имеет подходящее расширенное использование ключа (EKU 1.3.6.1.5.5.7.3.3).
- Сертификат не удовлетворяет базовым требованиям, таким как алгоритм подписи RSA SHA-256 или открытый ключ размером 2048 бит или больше.
- Сертификат устарел или отозван.
- Сервера меток времени не удовлетворяет требованиям к сертификату.

> [!Note]
> Подписанные пакеты должны включать метку времени, чтобы подпись оставалась действительной после истечения срока действия сертификата для подписывания. При подписывании без метки времени операция sign вызывает [предупреждение NU3002](../reference/Errors-and-Warnings.md#nu3002).

## <a name="verify-a-signed-package"></a>Проверка подписанного пакета

Используйте [nuget verify](../tools/cli-ref-verify.md), чтобы просмотреть сведения о подписи заданного пакета.

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>Установка подписанного пакета

Для установки подписанных пакетов не требуются какие-либо специальные действия.Но если содержимое было изменено с момента подписания, установка блокируется и выдается [ошибка NU3008](../reference/Errors-and-Warnings.md#nu3008).

> [!Warning]
> Пакеты, подписанные с использованием недоверенных сертификатов, считаются неподписанными и устанавливаются без предупреждений или ошибок, как и любой другой неподписанный пакет.

## <a name="see-also"></a>См. также

[Справочник по подписанным пакетам](../reference/Signed-Packages-Reference.md)
