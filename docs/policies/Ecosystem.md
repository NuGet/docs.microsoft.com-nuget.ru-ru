---
title: Общие сведения об экосистеме NuGet
description: Полноценный набор ресурсов в экосистеме NuGet, включая источники NuGet, проекты NuGet сторонних поставщиков, служебные программы и учебные материалы.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 57fa8e5683e687aab3022ebc77d7e69a61615877
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775600"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>Общие сведения об экосистеме NuGet

С момента своего появления в 2010 году NuGet позволил значительно улучшить и автоматизировать различные аспекты процессов разработки.

Так как NuGet представляет собой проект с открытым исходным кодом, регулируемый [свободной лицензией Apache версии 2](http://choosealicense.com/licenses/apache/), он может использоваться в других проектах, а организации могут реализовывать его поддержку в своих продуктах. Как для проектов с открытым кодом, так и для разработки корпоративных приложений NuGet и другие основанные на нем приложения предоставляют обширную экосистему средств для улучшения процесса разработки программного обеспечения.

Все эти проекты продвигаются вперед благодаря вкладу разработчиков. Если вы работаете над NuGet, внесите вклад и в эти проекты, по мере возможности сообщая о дефектах, делясь идеями по улучшению продукта, оставляя отзывы, составляя документацию и дополняя код.

## <a name="net-foundation-projects"></a>Проекты .NET Foundation

NuGet предоставляет бесплатную систему управления пакетами с открытым исходным кодом для платформы разработки Майкрософт. Она состоит из нескольких клиентских средств, а также набора служб, составляющих [официальную коллекцию NuGet](http://www.nuget.org). Вместе они образуют проект NuGet, управляемый [.NET Foundation](http://www.dotnetfoundation.org/).

Организация NuGet имеет различные репозитории на сайте GitHub. [https://github.com/Nuget/Home](https://github.com/Nuget/Home) предоставляет общие сведения о всех репозиториях и том, где можно найти различные компоненты NuGet.

## <a name="microsoft-projects"></a>Проекты Майкрософт

Корпорация Майкрософт внесла значительный вклад в разработку NuGet. Все внесенные сотрудниками корпорации Майкрософт дополнения также имеют открытый исходный код и переданы в дар (включая авторские права) .NET Foundation.

## <a name="non-microsoft-projects"></a>Сторонние проекты

Значительный вклад в экосистему NuGet внесли многие люди и организации. Каждый из перечисленных здесь проектов может иметь не такие условия лицензии, как основные компоненты NuGet, поэтому перед использованием убедитесь, что эти условия приемлемы для вас:

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/);
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (или NuGet-as-a-service)](http://www.myget.org/)
- [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet Server](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin и MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Другие служебные программы на основе NuGet

Эти средства и служебные программы основаны на NuGet:

- [Glimpse Extensions](http://getglimpse.com/Packages) (подключаемые модули являются пакетами)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (модули CMS получены из веб-канала NuGet версии v1, размещенного в коллекции Orchard Gallery)
- [Реализация сервера NuGet на языке Java](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (бот в Twitter, публикующий данные о новых пакетах)
- [DefinitelyTyped](http://definitelytyped.org/) ([автоматическая](https://github.com/DefinitelyTyped/NugetAutomation/) публикация определений типа TypeScript [в NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Учебные материалы и справочники

Внедрение нового инструмента или технологии обычно требуют времени на изучение. К счастью, с NuGet дело обстоит совсем не так. Фактически, любой человек может быстро [приступить к использованию пакетов](../quickstart/install-and-use-a-package-in-visual-studio.md).

Однако для создания пакетов, особенно хорошего качества, с сопутствующим кодом NuGet в рамках автоматических процессов сборки и развертывания вам потребуется уделить немного больше времени изучению следующих ресурсов:

- [Блог по NuGet](http://blog.nuget.org/)
- [Команда разработчиков NuGet в Twitter, @nuget](http://twitter.com/nuget)
- Книги:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 Essentials](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Документация для отдельных пакетов

[NuDoq](http://nudoq.org) обеспечивает простой доступ, обновления и документацию для пакетов NuGet.

NuDoq регулярно опрашивает сервер коллекции nuget.org на наличие последних обновлений пакетов, распаковывает и обрабатывает файлы документации библиотек и соответствующим образом обновляет сайт.

## <a name="adding-your-project"></a>Добавление своего проекта

Если у вас есть проект экосистемы NuGet, который может стать ценным дополнением для этой страницы, отправьте запрос на вытягивание с изменением на эту страницу.