---
title: Запрос всех пакетов, опубликованных на сайте nuget.org | Документы Майкрософт
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/02/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: С помощью API NuGet вы можете запросить все пакеты, опубликованные на сайте nuget.org, и быть в курсе последних событий.
keywords: перечисление всех пакетов API NuGet, репликация пакетов API NuGet, самые новые пакеты на сайте nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5ea11e1b4edd87b6d30d3838986ca60aaa77870f
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Запрос всех пакетов, опубликованных на сайте nuget.org

Типичным шаблоном запроса для устаревшего OData V2 API было перечисление всех пакетов, опубликованных на сайте nuget.org, с сортировкой по времени публикации. Подобный запрос к сайту nuget.org может потребоваться в самых разных ситуациях:

- Репликация всего сайта nuget.org
- Проверка на наличие новых версий для пакетов
- Поиск пакетов, зависящих от вашего пакета

Ранее для этого обычно выполнялась сортировка сущности пакета OData по метке времени и просмотр огромного результирующего набора с помощью параметров `skip` и `top` (размер страницы). К сожалению, у этого способа есть несколько недостатков:

- Возможность отсутствия пакетов, так как запросы выполняются для данных, которые часто меняют порядок.
- Большое время отклика запроса, так как запросы не оптимизируются (лучше всего оптимизированы запросы, поддерживающие основной сценарий для официального клиента NuGet).
- Использование нерекомендуемого и незадокументированного API, из-за чего не гарантируется поддержка этих запросов в будущем.
- Неспособность воспроизвести журнал в том порядке, в котором он формировался.

По этой причине можно воспользоваться приведенным ниже руководством, чтобы обеспечить более надежную и прогнозируемую работу в вышеупомянутых сценариях.

## <a name="overview"></a>Обзор

Центральной точкой этого руководства является ресурс в [API NuGet](../../api/overview.md), называемый **каталогом**. Каталог — это доступный только для добавления API, который позволяет вызывающему объекту просмотреть полный журнал пакетов, добавленных, измененных и удаленных на сайте nuget.org. Если вас интересуют все пакеты, опубликованные на сайте nuget.org, или их подмножество, каталог отлично подходит для того, чтобы оставаться в курсе актуального набора доступных пакетов.

Это руководство имеет общий характер. Если вы хотите получить более подробные сведения о каталоге, см. соответствующий [справочник по API](../../api/catalog-resource.md).

Приведенные ниже шаги можно реализовать на любом языке программирования. Если вам нужен полноценный рабочий пример, обратите внимание на указанный ниже [пример на C#](#c-sample-code).

В противном случае выполните приведенные ниже инструкции, чтобы создать надежное средство чтения каталога.

## <a name="initialize-a-cursor"></a>Инициализация курсора

Первым шагом в создании надежного средства чтения каталога является реализация курсора. Полные сведения о проектировании курсора каталога см. в [справочном документе по каталогу](../../api/catalog-resource.md#cursor). Если кратко, курсор является точкой во времени, до которой вы обработали события в каталоге. События в каталоге представляют публикации пакетов и другие их изменения. Если вас интересуют все пакеты, когда-либо опубликованные в NuGet (с самого его появления), нужно инициализировать курсор с минимальной меткой времени (например, `DateTime.MinValue` в .NET). Если вам нужны только пакеты, опубликованные с текущего момента, нужно использовать текущую метку времени в качестве начального значения курсора.

В этом руководстве мы инициализируем курсор с меткой времени на час раньше текущего момента. Пока просто сохраните метку времени в памяти.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Определение URL-адреса индекса каталога

Нужно определить расположение каждого ресурса (конечная точка) в API NuGet с помощью [индекса службы](../../api/service-index.md). Так как это руководство ориентировано на сайт nuget.org, мы будем использовать индекс службы для nuget.org.

    GET https://api.nuget.org/v3/index.json

Документ службы представляет собой документ JSON, содержащий все ресурсы на сайте nuget.org. Выполните поиск ресурса, у которого свойство `@type` имеет значение `Catalog/3.0.0`. Соответствующее значение свойства `@id` является URL-адресом для самого индекса каталога. 

## <a name="find-new-catalog-leaves"></a>Поиск новых конечных объектов каталога

Используя значение свойства `@id`, найденное на предыдущем шаге, скачайте индекс каталога:

    GET https://api.nuget.org/v3/catalog0/index.json

Десериализуйте [индекс каталога](../../api/catalog-resource.md#catalog-index). Отфильтруйте все [объекты страниц каталога](../../api/catalog-resource.md#catalog-page-object-in-the-index), у которых `commitTimeStamp` меньше или равен текущему значению курсора.

Для каждой из оставшихся страниц каталога скачайте полный документ, используя свойство `@id`.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Десериализуйте [страницу каталога](../../api/catalog-resource.md#catalog-page). Отфильтруйте все [конечные объекты каталога](../../api/catalog-resource.md#catalog-item-object-in-a-page), у которых `commitTimeStamp` меньше или равен текущему значению курсора.

Скачав все неотфильтрованные страницы каталога, вы получите набор конечных объектов каталога, представляющих пакеты, которые были опубликованы, исключены из списка, добавлены в список или удалены за период между меткой времени вашего курсора и текущим моментом.

## <a name="process-catalog-leaves"></a>Обработка конечных объектов каталога

На этом этапе вы можете выполнить любую пользовательскую обработку элементов каталога. Если вам нужны только идентификатор и версия пакета, можно просмотреть свойства `nuget:id` и `nuget:version` для объектов элементов каталога, найденных на этих страницах. Обязательно просмотрите свойство `@type`, чтобы узнать, касается ли элемент каталога существующего или удаленного пакета.

Если вас интересуют метаданные о пакете (например, описание, зависимости, размер, файла NUPKG и т. д), можно извлечь [документ конечного объекта каталога](../../api/catalog-resource.md#catalog-leaf) с помощью свойства `@id`.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Этот документ содержит все метаданные, входящие в [ресурс метаданных пакета](../../api/registration-base-url-resource.md), и многое другое.

На этом этапе вы реализуете настраиваемую логику. Другие действия в этом руководстве реализуются аналогичным образом, независимо от конкретных действий с конечными объектами каталога.

### <a name="downloading-the-nupkg"></a>Скачивание файла NUPKG

Если вы хотите скачать файл NUPKG для найденных в каталоге пакетов, можно использовать [ресурс содержимого пакета](../../api/package-base-address-resource.md). Но нужно учитывать, что при обнаружении пакета в каталоге он станет доступен в ресурсе содержимого пакета с небольшой задержкой. Поэтому если при попытке скачать файл NUPKG для найденного в каталоге пакета возникает `404 Not Found`, просто повторите попытку немного позднее. Исправлению этой задержки посвящен вопрос GitHub [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Перемещение курсора вперед

После успешной обработки элементов каталога нужно определить новое значение курсора. Для этого найдите максимальное значение (последнее в хронологическом порядке) `commitTimeStamp` для всех обработанных элементов каталога. Это и есть новое значение курсора. Сохраните его в постоянном хранилище, таком как база данных, файловая система или хранилище BLOB-объектов. Если вам нужно получить дополнительные элементы каталога, просто начните с [первого шага](#initialize-a-cursor), инициализировав значение курсора из этого постоянного хранилища.

Если приложение вызывает исключения или завершается со сбоем, не перемещайте курсор вперед. Перемещение курсора вперед означает, что вам больше никогда не потребуется снова обработать элементы каталога, предшествующие курсору.

Если по некоторым причинам у вас возникает ошибка при обработке конечных объектов каталога, можете просто переместить курсор назад и позволить коду повторно обработать старые элементы каталога.

## <a name="c-sample-code"></a>Пример кода на C#

Так как каталог представляет собой набор документов JSON, доступных по протоколу HTTP, с ним можно взаимодействовать с помощью любого языка программирования, имеющего HTTP-клиент и десериализатор JSON.

Примеры на C# доступны в [репозитории NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>Пакет SDK каталога

Для работы с каталогом проще всего использовать предварительную версию пакета SDK для каталога .NET: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog). Этот пакет доступен в веб-канале `nuget-build` MyGet, для которого используется URL-адрес источника пакетов NuGet `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.

Вы можете установить этот пакет в проект, совместимый с `netstandard1.3` или более поздней версии (например, .NET Framework 4.6).

Пример использования этого пакета можно найти на сайте GitHub в [проекте NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

#### <a name="sample-output"></a>Пример полученных результатов

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a>Минималистичный пример

Пример с меньшим числом зависимостей, более подробно демонстрирующий взаимодействие с каталогом, см. в [проекте примера CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Этот проект ориентирован на `netcoreapp2.0` и зависит от [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (для разрешения индекса службы) и [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (для десериализации JSON).

Основная логика кода видна в [файле Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

#### <a name="sample-output"></a>Пример полученных результатов

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
