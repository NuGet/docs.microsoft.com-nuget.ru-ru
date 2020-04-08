---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496062"
---
<span data-ttu-id="0fb78-101">Ошибки в результатах выполнения команды `push` обычно указывают на неполадку.</span><span class="sxs-lookup"><span data-stu-id="0fb78-101">Errors from the `push` command typically indicate the problem.</span></span> <span data-ttu-id="0fb78-102">Например, вы забыли обновить номер версии проекта и пытаетесь опубликовать пакет, который уже существует.</span><span class="sxs-lookup"><span data-stu-id="0fb78-102">For example, you may have forgotten to update the version number in your project and are therefore trying to publish a package that already exists.</span></span>

<span data-ttu-id="0fb78-103">Ошибки также возникают при попытке опубликовать пакет с использованием идентификатора, который уже имеется на узле.</span><span class="sxs-lookup"><span data-stu-id="0fb78-103">You also see errors when trying to publish a package using an identifier that already exists on the host.</span></span> <span data-ttu-id="0fb78-104">Например, имя AppLogger уже существует.</span><span class="sxs-lookup"><span data-stu-id="0fb78-104">The name "AppLogger", for example, already exists.</span></span> <span data-ttu-id="0fb78-105">В этом случае команда `push` выдает следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="0fb78-105">In such a case, the `push` command gives the following error:</span></span>

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

<span data-ttu-id="0fb78-106">Если вы используете только что созданный допустимый ключ API, это сообщение означает, что возник конфликт имен, что не совсем понятно из части касательно разрешения в ошибке.</span><span class="sxs-lookup"><span data-stu-id="0fb78-106">If you're using a valid API key that you just created, then this message indicates a naming conflict, which isn't entirely clear from the "permission" part of the error.</span></span> <span data-ttu-id="0fb78-107">Измените идентификатор пакета, перестройте проект, повторно создайте файл `.nupkg`, а затем повторите команду `push`.</span><span class="sxs-lookup"><span data-stu-id="0fb78-107">Change the package identifier, rebuild the project, recreate the `.nupkg` file, and retry the `push` command.</span></span>