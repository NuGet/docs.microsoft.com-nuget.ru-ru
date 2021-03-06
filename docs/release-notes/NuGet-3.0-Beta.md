---
title: Заметки о бета-версии NuGet 3,0
description: Заметки о выпуске для бета-версии NuGet 3,0, включая известные проблемы, исправления ошибок, добавленные функции и DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776631"
---
# <a name="nuget-30-beta-release-notes"></a>Заметки о бета-версии NuGet 3,0

[Заметки о](../release-notes/nuget-3.0-preview.md)  |  выпуске NuGet 3,0 Preview [Заметки о выпуске для версии-кандидата NuGet 3,0](../release-notes/nuget-3.0-rc.md)

Бета-версия NuGet 3,0 была выпущена 23 февраля 2015 для выпуска Visual Studio 2015 CTP 6. Этот выпуск имеет большое значение для нашей группы, так как у нас есть ряд улучшений архитектуры и производительности, и мы рады начать настройку параметров производительности в нашей службе nuget.org.

Перед установкой новой версии настоятельно рекомендуется удалить все предыдущие версии расширения NuGet для Visual Studio 2015.  Если у вас возникли проблемы с этой версией расширения, мы рекомендуем вернуться к [предыдущей версии](http://nuget.codeplex.com/downloads/get/909582) для использования с предварительной версией Visual Studio 2015.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Эту бета-версию NuGet 3,0 можно установить в галерее расширений Visual Studio 2015 CTP 6. Мы работаем над тем, чтобы получить предварительную версию Visual Studio 2012 и Visual Studio 2013 в ближайшее время. Мы уже использовали нашу цель для [прекращения обновлений для Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), и мы сделали это сложное решение.

## <a name="new-clientserver-api"></a>Новый API клиента/сервера

Мы работаем над некоторыми деталями реализации протокола клиента/сервера NuGet. Работа, которую мы сделали, — это создать "API V3" для NuGet, который разработан для обеспечения высокого уровня доступности для критически важных сценариев, таких как восстановление пакетов и установка пакетов. Новый API основан на функциях RESTFUL и Media, и мы выбрали [JSON-LD](http://json-ld.org) в качестве формата ресурсов.

В битах бета-версии NuGet 3,0 вы увидите новый источник пакета с именем "api.nuget.org" в раскрывающемся списке Источник пакета.   Если выбрать этот источник пакета, мы будем использовать наш новый API вместо подключения к nuget.org. В версии-КАНДИДАТе NuGet 3,0 этот новый источник пакетов на основе API V3 заменит источник пакета nuget.org на основе v2.  Рекомендуется отключить все другие общедоступные источники пакетов и оставить только api.nuget.org в качестве единственного репозитория пакетов.

Мы собрали много времени на создание нашего API V3 и продолжате обслуживание стандартного API v2 для старых клиентов, которые ищут доступ к общедоступному репозиторию.

## <a name="updated-ui"></a>Обновленный пользовательский интерфейс

Мы улучшили пользовательский интерфейс в этом выпуске, включив в него поле со списком, которое позволит выбрать действие, выполняемое с пакетом, и перейти на кнопку Предварительный просмотр в область параметров экрана.  Область параметров больше не является сворачиваемой и теперь содержит ссылку на справку, описывающую доступные параметры.

![Новый пользовательский интерфейс NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Ведение журнала операций

Мы удалили модальное окно с данными журнала, которые быстро отображались и скрываются во время установки или удаления.  Это окно не добавило никакого значения, если вы действительно хотите просмотреть сведения или скопировать и вставить его из него.  Вместо этого мы перенаправлены все выходные данные журнала в область диспетчер пакетов окна вывод.  Мы думаем, что это более удобно и похоже на типичный отчет о сборке, который нужно изучить.


### <a name="focus-on-performance"></a>Сосредоточьтесь на производительности

Мы внесли множество изменений в имена, повышающие производительность поиска NuGet и выбирали их.  Это был наш номер, один из наших клиентов, и мы хотели убедиться, что он был решен в этом выпуске.  Мы настроили наши серверы, создали новую сеть CDN и улучшили логику сопоставления запросов, чтобы вы получили более актуальные и более эффективные результаты поиска пакетов.

По мере выполнения этого этапа разработки NuGet 3,0 мы будем настраивать и отслеживать службу nuget.org, чтобы обеспечить улучшенную работу.  Мы не планируем использовать время простоя, но будут добавлять и изменять ресурсы в службе.  Следите за веб- [каналом Twitter](http://twitter.com/nuget) , чтобы получить подробные сведения об изменении конфигурации службы.

## <a name="building-nuget-with-nuget"></a>Сборка NuGet с помощью NuGet

Теперь мы перестроили клиенты NuGet на несколько компонентов, которые встроены в пакеты NuGet. Это повторное использование собственных библиотек заставляет нас создавать компоненты, которые можно использовать повторно, а также упаковываться должным образом.  Мы смогли устранить дублирование кода и узнали, как лучше настроить наш процесс разработки для поддержки создания пакетов на всех наших решениях.  Вскоре мы будем говорить о том, как структурированы проекты кода и как работает наш процесс сборки.

## <a name="stay-tuned"></a>Оставайтесь в курсе

Следите за [нашим блогом](http://blog.nuget.org) , чтобы получить дополнительные сведения о ходе и объявлениях для NuGet 3,0!
