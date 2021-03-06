---
title: Заметки о выпуске NuGet 1,2
description: Заметки о выпуске NuGet 1,2, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: af2248a41800f7641be9b77d7bb72e2a94d4ce47
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777199"
---
# <a name="nuget-12-release-notes"></a>Заметки о выпуске NuGet 1,2

[Заметки о](../release-notes/nuget-1.1.md)  |  выпуске NuGet 1,0 и 1,1 [Заметки о выпуске NuGet 1,3](../release-notes/nuget-1.3.md)

Версия NuGet 1,2 была выпущена 30 марта 2011 г.

## <a name="new-features"></a>Новые возможности

### <a name="framework-profile-support"></a>Поддержка профиля платформы

С самого начала поддерживаемые NuGet библиотеки имеют различные платформы. Но теперь пакеты могут содержать сборки, предназначенные для конкретных профилей, таких как профиль Windows Phone. Чтобы ориентироваться на конкретный профиль платформы, добавьте тире, за которым следует сокращение профиля. Например, чтобы запустить SilverLight на Windows Phone (то есть Windows Phone 7), можно разместить сборку в папке SL3-WP, как показано на следующем снимке экрана.

![Макет папки профиля платформы](./media/framework-profile-support.png)

Вы можете спросить, почему мы не решили использовать "WP7" в качестве моникера. Мы ожидаем, что Windows Phone 7 может запустить более новую версию Silverlight в будущем. в этом случае может потребоваться более подробная информация о том, какой профиль платформы вы предназначенных.

### <a name="automatically-add-binding-redirects"></a>Автоматически добавлять перенаправления привязок

При установке пакета со сборками со строгими именами NuGet теперь может определять случаи, когда для проекта требуется добавить перенаправления привязок в файл конфигурации, чтобы проект был скомпилирован и добавлен автоматически. В части 3 из статьи блога Дэвид Эббо, посвященной использованию управления версиями NuGet "[унификация с помощью перенаправлений привязки](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)", описывается назначение этой функции в разделе более подробно.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Указание ссылок на сборки платформы (GAC)

В некоторых случаях пакет может зависеть от сборки, которая находится в платформа .NET Framework. Строго говоря, не всегда требуется, чтобы потребитель пакета ссылался на сборку платформы. Но в некоторых случаях это важно, например, когда разработчику требуется код для работы с типами в этой сборке, чтобы использовать пакет. Новый `frameworkAssemblies` элемент, дочерний элемент элемента метаданных, позволяет указать набор `frameworkAssembly` элементов, указывающих на сборку платформы в GAC. Обратите особое внимание на сборку платформы.
Эти сборки не включаются в пакет, так как предполагается, что они находятся на каждом компьютере как часть платформа .NET Framework. В следующей таблице перечислены атрибуты `frameworkAssembly` элемента.


|attribute |Описание|
|----------------|-----------|
|**имя_сборки**|*Обязательно*. Имя сборки, например `System.Net` .|
|**targetFramework**|*Необязательно*. Позволяет указать платформу и имя профиля (или псевдонима), к которым применяется эта сборка платформы, например "net40" или "SL4". Использует тот же формат, который описан в разделе [Поддержка нескольких целевых платформ](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe теперь может хранить учетные данные ключа API

При использовании программы командной строки nuget.exe теперь можно использовать команду Сетапикэй для хранения ключа API. Таким образом, вам не потребуется указывать его каждый раз при передаче пакета. Дополнительные сведения о сохранении ключа API с nuget.exe см. [в документации по публикации пакета](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Обозреватель пакетов
Обозреватель пакетов был обновлен для поддержки NuGet 1,2. Дополнительные сведения см. в [заметках о выпуске обозревателя пакетов](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Другие функции и исправления

Предыдущий список был наиболее заметным из многих реализованных нами функций и исправленных ошибок. В этом выпуске мы реализовали и предустранили [59 рабочих элементов](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) .

## <a name="known-issues"></a>Известные проблемы

* **1,2**. пакеты, созданные с помощью последней версии средства командной строки, nuget.exe (> 1,2) не будут работать с более старыми версиями НАДСТРОЙКи VS для NuGet (например, 1,1). При возникновении сообщения об ошибке, сообщающего о несовместимости схемы, вы запустили эту ошибку. Обновите NuGet до последней версии.
* **Несовместимость с NuGet. Server**. Если вы размещаете внутренний веб-канал NuGet с помощью проекта NuGet. Server, необходимо обновить этот проект с помощью последней версии NuGet. Server.
* **Ошибка несоответствия подписи**: Если при обновлении возникла ошибка с сообщением о несоответствии подписи, необходимо сначала удалить NuGet, а затем установить его. Он указан на [странице известных проблем](../release-notes/known-issues.md) , где содержатся дополнительные сведения. Проблема касается только тех, которые работают под управлением Visual Studio 2010 с пакетом обновления 1 (SP1) и установлена версия NuGet 1,0, которая была неправильно подписана. Эта версия была доступна только на веб-сайте CodePlex в течение короткого периода, поэтому эта проблема не должна затрагивать слишком много людей.