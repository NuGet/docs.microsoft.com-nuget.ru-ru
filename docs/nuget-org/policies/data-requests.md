---
title: Запросы данных пользователей
description: Политики в отношении запросов на удаление и экспорт данных пользователей
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775722"
---
# <a name="user-data-requests"></a><span data-ttu-id="c5867-103">Запросы данных пользователей</span><span class="sxs-lookup"><span data-stu-id="c5867-103">User Data Requests</span></span>

<span data-ttu-id="c5867-104">Пользователи nuget.org могут отправлять запросы на экспорт и удаление сведений через [nuget.org](https://www.nuget.org). Оба типа запросов отправляются в виде запросов на поддержку и подлежат выполнению администраторами nuget.org в течение 30 дней.</span><span class="sxs-lookup"><span data-stu-id="c5867-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="c5867-105">Следующие данные пользователей доступны напрямую через nuget.org:</span><span class="sxs-lookup"><span data-stu-id="c5867-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="c5867-106">данные, связанные с учетной записью, такие как адрес электронной почты, учетная запись для входа, изображение профиля и параметры уведомлений по электронной почте;</span><span class="sxs-lookup"><span data-stu-id="c5867-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="c5867-107">ключи собственных API;</span><span class="sxs-lookup"><span data-stu-id="c5867-107">Owned API Keys</span></span>
* <span data-ttu-id="c5867-108">список принадлежащих пользователю пакетов.</span><span class="sxs-lookup"><span data-stu-id="c5867-108">List of owned packages</span></span>

<span data-ttu-id="c5867-109">Эти данные не включаются в данные, экспортируемые с помощью запроса на поддержку.</span><span class="sxs-lookup"><span data-stu-id="c5867-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="c5867-110">Идентификация данных клиентов</span><span class="sxs-lookup"><span data-stu-id="c5867-110">Identifying customer data</span></span>

<span data-ttu-id="c5867-111">Данные клиента можно идентифицировать по именам учетных записей пользователей nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c5867-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="c5867-112">Удаление данных клиентов</span><span class="sxs-lookup"><span data-stu-id="c5867-112">Deleting customer data</span></span>

<span data-ttu-id="c5867-113">Чтобы запросить удаление данных пользователя из nuget.org, необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c5867-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="c5867-114">Пользователь должен войти в систему [nuget.org](https://www.nuget.org).</span><span class="sxs-lookup"><span data-stu-id="c5867-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="c5867-115">Пользователь должен отправить запрос для удаления своей учетной записи [nuget.org/account/delete](https://www.nuget.org/account/delete).</span><span class="sxs-lookup"><span data-stu-id="c5867-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="c5867-116">Пользователям, являющимся единственными владельцами пакетов, рекомендуется найти новых владельцев перед запросом удаления их учетных записей.</span><span class="sxs-lookup"><span data-stu-id="c5867-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="c5867-117">Если владение пакетом не передается, пакет NuGet исключается из каталога и становится недоступным в поисковых запросах в Visual Studio или на веб-сайте nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c5867-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="c5867-118">Перед удалением учетной записи администраторы nuget.org взаимодействуют с пользователем, чтобы найти новых владельцев для принадлежавших ему пакетов.</span><span class="sxs-lookup"><span data-stu-id="c5867-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="c5867-119">Действие удаления учетной записи выполняется администратором nuget.org в течение 30 дней с даты запроса.</span><span class="sxs-lookup"><span data-stu-id="c5867-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="c5867-120">После удаления учетной записи все данные пользователя удаляются из системы nuget.org и выполняются следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c5867-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="c5867-121">отменяется регистрация удаленной учетной записи в nuget.org;</span><span class="sxs-lookup"><span data-stu-id="c5867-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="c5867-122">все ключи собственных API удаляются;</span><span class="sxs-lookup"><span data-stu-id="c5867-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="c5867-123">все зарезервированные пространства имен освобождаются;</span><span class="sxs-lookup"><span data-stu-id="c5867-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="c5867-124">все права на владение пакетами удаляются.</span><span class="sxs-lookup"><span data-stu-id="c5867-124">Any package ownership are removed</span></span>

<span data-ttu-id="c5867-125">Собственные пакеты *не* удаляются.</span><span class="sxs-lookup"><span data-stu-id="c5867-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="c5867-126">Хотя они удаляются из результатов поиска, эти пакеты остаются доступными через функцию восстановления пакетов в проектах, которые от них зависят.</span><span class="sxs-lookup"><span data-stu-id="c5867-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="c5867-127">Экспорт данных клиентов</span><span class="sxs-lookup"><span data-stu-id="c5867-127">Exporting customer data</span></span>

<span data-ttu-id="c5867-128">Выполнив вход в систему nuget.org, пользователь может оправить запрос на экспорт через [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="c5867-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="c5867-129">Экспортированные данные становятся доступны пользователю для загрузки через BLOB-объект Azure в течение 48 часов.</span><span class="sxs-lookup"><span data-stu-id="c5867-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="c5867-130">Через 48 часов срок доступа истекает, и пользователю потребуется отправить новый запрос на экспорт (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="c5867-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="c5867-131">Экспортированные данные включают:</span><span class="sxs-lookup"><span data-stu-id="c5867-131">The exported data includes:</span></span>

* <span data-ttu-id="c5867-132">запросы на поддержку этого пользователя;</span><span class="sxs-lookup"><span data-stu-id="c5867-132">The user's support requests</span></span>
* <span data-ttu-id="c5867-133">действия пользователя (публикация пакетов, создание учетной записи), которые сохранялись в журналах аудита;</span><span class="sxs-lookup"><span data-stu-id="c5867-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="c5867-134">сведения о пользователях, которые сохранялись в журналах IIS.</span><span class="sxs-lookup"><span data-stu-id="c5867-134">Any user information as persisted in the IIS logs</span></span>
