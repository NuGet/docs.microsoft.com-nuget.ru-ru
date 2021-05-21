---
title: Файл сведений о пакете на NuGet.org
description: Подробное описание того, как отображаются файлы сведений на NuGet.org и что делать при возникновении проблем.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902230"
---
# <a name="package-readme-on-nugetorg"></a>Файл сведений о пакете на NuGet.org

[Добавьте в пакет NuGet файл сведений](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile), чтобы предоставить пользователям более детальные сведения о пакете.

Скорее всего, это один из первых элементов, которые пользователи увидят при просмотре страницы сведений о пакете на NuGet.org. Он очень важен для создания хорошего впечатления!

> [!IMPORTANT]
> NuGet.org поддерживает только файлы сведений в формате [Markdown](https://daringfireball.net/projects/markdown/) и изображения из ограниченного набора доменов. Ознакомьтесь с [разрешенными доменами для изображений](#allowed-domains-for-images-and-badges) и [поддерживаемыми функциями Markdown](#supported-markdown-features), чтобы убедиться, что файл сведений правильно отображается на NuGet.org.

## <a name="what-should-my-readme-include"></a>Что необходимо включить в файл сведений?

Рассмотрите возможность включения следующих элементов в файл сведений:
* Общие сведения о том, что представляет собой пакет, и какие проблемы он решает.
* Инструкции по началу работы с пакетом и особые требования (при наличии).
* Ссылки на более подробную документацию, если она не включена в сам файл сведений.
* По крайней мере несколько фрагментов кода, примеров или изображений.
* Где и как оставить отзыв, например ссылка на проблемы проекта, Twitter, средство отслеживания ошибок или другую платформу.
* Как помочь разработке, если применимо.

Учтите, что качественные файлы сведений бывают самых разных форматов, форм и размеров. Если у вас уже есть пакет, доступный на NuGet.org, вероятно, у вас есть `readme.md` или другой файл документации в репозитории, который будет отличным дополнением к странице сведений на NuGet.org.

## <a name="preview-your-readme"></a>Предварительный просмотр файла сведений

Чтобы просмотреть файл сведений перед его публикацией на NuGet.org, отправьте пакет с помощью [веб-портала отправки пакетов на NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) и прокрутите вниз до раздела Readme File (Файл сведений) на странице предварительного просмотра метаданных. Должно отобразиться примерно следующее:

![Предварительный просмотр файла сведений](media\readme-upload-preview.PNG)

Рекомендуем воспользоваться предварительным просмотром и проверить файл сведений, чтобы обеспечить соответствие требованиям к [изображениям](#allowed-domains-for-images-and-badges) и [форматированию](#supported-markdown-features). Это поможет произвести отличное первое впечатление на потенциальных пользователей! Чтобы исправить ошибки в файле сведений о пакете после его публикации на NuGet.org, необходимо отправить обновленную версию пакета с исправлением. Если вы сразу убедитесь, что все выглядит хорошо, то сможете сэкономить время.
## <a name="allowed-domains-for-images-and-badges"></a>Разрешенные домены для изображений и эмблем

По соображениям безопасности и конфиденциальности NuGet.org поддерживает только ограниченный набор доменов, из которых можно отображать изображения и эмблемы на доверенных узлах. 

NuGet.org позволяет отображать все изображения, в том числе эмблемы, из следующих доверенных доменов:
* api.bintray.com
* api.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Если вы считаете, что в список разрешений нужно добавить домен, вы можете [сообщить о проблеме](https://github.com/NuGet/NuGetGallery/issues), и она будет рассмотрена нашей командой специалистов по обеспечению конфиденциальности и безопасности. Изображения с относительными локальными путями и изображения, размещенные в неподдерживаемых доменах, не будут отображаться. На странице предварительного просмотра файла сведений о пакете будет предупреждение, которое смогут увидеть только владельцы пакета.

## <a name="supported-markdown-features"></a>Поддерживаемые возможности Markdown
[Markdown](https://daringfireball.net/projects/markdown/) — это облегченный язык разметки с синтаксисом форматирования обычного текста. Файл сведений на NuGet.org поддерживает совместимый с [CommonMark](https://commonmark.org/) язык Markdown, на основе подсистемы анализа [Markdig](https://github.com/lunet-io/markdig).

В настоящее время NuGet.org поддерживает следующие возможности Markdown:
* [Заголовки](https://spec.commonmark.org/0.29/#atx-headings)
* [Изображения](https://spec.commonmark.org/0.29/#images)
* [Дополнительное выделение текста](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [Списки](https://spec.commonmark.org/0.29/#lists)
* [Ссылки](https://spec.commonmark.org/0.29/#links)
* [Цитаты](https://spec.commonmark.org/0.29/#block-quotes)
* [Обратная косая черта в качестве escape-символа](https://spec.commonmark.org/0.29/#backslash-escapes)
* [Диапазоны кода](https://spec.commonmark.org/0.29/#code-spans)
* [Списки задач](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [Таблицы](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [Эмодзи](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [Автоматические ссылки](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

