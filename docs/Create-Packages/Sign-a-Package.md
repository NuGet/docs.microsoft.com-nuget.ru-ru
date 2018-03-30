---
title: Подписывание пакетов NuGet | Документы Майкрософт
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Описание того, как подписанные пакеты можно использовать, чтобы включить проверку целостности содержимого.
keywords: Подписывание пакетов NuGet, безопасность NuGet, создание подписанных пакетов
ms.reviewer:
- karann-msft
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61d90066e8cf75c8f49c7cc9390d45e1cd8afd0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="signing-nuget-packages"></a>Подписывание пакетов NuGet

Подписывание пакета — это процесс, который гарантирует, что пакет не был изменен с момента создания.

## <a name="prerequisites"></a>Предварительные требования

1. Пакет (файл `.nupkg`) для подписывания. См. статью [Создание пакета](creating-a-package.md).

1. nuget.exe 4.6.0 или более поздней версии. См. статью [Установка интерфейса командной строки NuGet](../install-nuget-client-tools.md#nugetexe-cli).

1. [Сертификат подписывания кода](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

> [!Warning]
> Сейчас nuget.org не принимает подписанные пакеты. Вы можете подписывать пакеты для публикации в пользовательских веб-каналах.

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
