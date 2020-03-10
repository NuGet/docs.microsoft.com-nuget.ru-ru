---
ms.openlocfilehash: fadb6091f9f1e4f380c3896f790fd61ce80e9683
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230591"
---
Необязательное описание пакета, отображаемое на странице NuGet.org пакета, получается из `<description></description`, используемого в файле `.csproj`, или через `$description` в [файле NUSPEC](../../reference/nuspec.md).

Пример поля _Description_ показан в следующем XML-коде файла `.csproj` для пакета .NET:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <PackageId>Azure.Storage.Blobs</PackageId>
    <Version>12.4.0</Version>
    <PackageTags>Microsoft Azure Storage Blobs;Microsoft;Azure;Blobs;Blob;Storage;StorageScalable</PackageTags>
    <Description>
      This client library enables working with the Microsoft Azure Storage Blob service for storing binary and text data.
      For this release see notes - https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/README.md and https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/CHANGELOG.md
      in addition to the breaking changes https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/BreakingChanges.txt
      Microsoft Azure Storage quickstarts and tutorials - https://docs.microsoft.com/en-us/azure/storage/
      Microsoft Azure Storage REST API Reference - https://docs.microsoft.com/en-us/rest/api/storageservices/
      REST API Reference for Blob Service - https://docs.microsoft.com/en-us/rest/api/storageservices/blob-service-rest-api
    </Description>
  </PropertyGroup>
</PropertyGroup>
```
