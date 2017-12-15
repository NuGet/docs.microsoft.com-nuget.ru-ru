---
title: "Поставщики учетных данных NuGet.exe | Документы Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3cf592de-39f2-4e7f-a597-62635fdcedfa
description: "NuGet.exe поставщиков учетных данных проверки подлинности в веб-канала и реализуются как исполняемые файлы командной строки, соблюдать определенные соглашения."
keywords: "поставщики учетных данных NuGet.exe, API-Интерфейс, поставщика учетных данных проверки подлинности в веб-канала, проверки подлинности в коллекции"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82ab4d6e9be0736e008f5bd27d46e1db166d7bb4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="ab127-104">Проверка подлинности веб-каналы через поставщиков учетных данных nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ab127-104">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="ab127-105">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="ab127-105">*NuGet 3.3+*</span></span>

<span data-ttu-id="ab127-106">Когда `nuget.exe` требуются учетные данные для проверки подлинности для веб-канал, он ищет их следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ab127-106">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ab127-107">NuGet сначала ищет учетные данные в `Nuget.Config` файлов.</span><span class="sxs-lookup"><span data-stu-id="ab127-107">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="ab127-108">Затем NuGet использует поставщики подключаемый модуль учетных данных, может быть порядке, указанном ниже.</span><span class="sxs-lookup"><span data-stu-id="ab127-108">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="ab127-109">(И пример является [Visual Studio Team Services учетных данных Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="ab127-109">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="ab127-110">Затем NuGet запрашивает у пользователя учетные данные в командной строке.</span><span class="sxs-lookup"><span data-stu-id="ab127-110">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="ab127-111">Обратите внимание, что поставщики учетных данных описанные здесь работает только в `nuget.exe` , а не в Visual Studio или «dotnet восстановления».</span><span class="sxs-lookup"><span data-stu-id="ab127-111">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="ab127-112">Поставщики учетных данных с помощью Visual Studio, в разделе [nuget.exe поставщиков учетных данных для Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="ab127-112">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="ab127-113">NuGet.exe поставщиков учетных данных можно использовать в тремя способами:</span><span class="sxs-lookup"><span data-stu-id="ab127-113">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="ab127-114">**Глобально**: чтобы сделать доступными для всех экземпляров поставщика учетных данных `nuget.exe` запустите профиля текущего пользователя, добавьте ее в `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="ab127-114">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="ab127-115">Может потребоваться создать `CredentialProviders` папку.</span><span class="sxs-lookup"><span data-stu-id="ab127-115">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="ab127-116">Поставщики учетных данных можно установить в корне `CredentialProviders` папки или вложенной папки.</span><span class="sxs-lookup"><span data-stu-id="ab127-116">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="ab127-117">Если поставщик учетных данных содержит несколько файлов и сборок, можно использовать вложенные папки для сохранения организованы поставщиков.</span><span class="sxs-lookup"><span data-stu-id="ab127-117">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="ab127-118">**Из переменной среды**: поставщиков учетных данных можно хранить в любом месте и получить доступ к ним `nuget.exe` , установив `%NUGET_CREDENTIALPROVIDERS_PATH%` переменную среды, чтобы расположение поставщика.</span><span class="sxs-lookup"><span data-stu-id="ab127-118">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="ab127-119">Эта переменная может быть список разделенных точкой с запятой (например, `path1;path2`) Если у вас есть несколько расположений.</span><span class="sxs-lookup"><span data-stu-id="ab127-119">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="ab127-120">**Наряду с nuget.exe**: nuget.exe поставщиков учетных данных может размещаться в той же папке, что `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ab127-120">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="ab127-121">При загрузке поставщиков учетных данных, `nuget.exe` поиск вышеуказанных местах в указанном порядке, для любого файла с именем `credentialprovider*.exe`, затем загружает их в порядке, они были найдены.</span><span class="sxs-lookup"><span data-stu-id="ab127-121">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="ab127-122">Если несколько поставщиков учетных данных в той же папке, они загружаются в алфавитном порядке.</span><span class="sxs-lookup"><span data-stu-id="ab127-122">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="ab127-123">Создание поставщика учетных данных nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ab127-123">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="ab127-124">Поставщик учетных данных — исполняемый файл командной строки с именем в форме `CredentialProvider*.exe`, собирает входных данных получает учетные данные, соответствующие и затем возвращает код состояния соответствующие выхода и стандартные выходные данные.</span><span class="sxs-lookup"><span data-stu-id="ab127-124">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="ab127-125">Поставщик должен выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="ab127-125">A provider must do the following:</span></span>

- <span data-ttu-id="ab127-126">Определите ли его можно указать учетные данные для целевого URI перед запуском процесса получения учетных данных.</span><span class="sxs-lookup"><span data-stu-id="ab127-126">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="ab127-127">В противном случае возвращается код состояния 1 без учетных данных.</span><span class="sxs-lookup"><span data-stu-id="ab127-127">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="ab127-128">Не изменяйте `Nuget.Config` (например, существует задание учетных данных).</span><span class="sxs-lookup"><span data-stu-id="ab127-128">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="ab127-129">Конфигурация прокси-сервера HTTP дескриптор в себе, как NuGet не предоставляет сведения о прокси подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="ab127-129">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="ab127-130">Возвращает учетные данные или сведения об ошибке для `nuget.exe` путем написания объект ответа JSON (см. ниже) в stdout, в кодировке UTF-8.</span><span class="sxs-lookup"><span data-stu-id="ab127-130">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="ab127-131">При необходимости выдает ведения журнала трассировки дополнительных в stderr.</span><span class="sxs-lookup"><span data-stu-id="ab127-131">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="ab127-132">Не секреты никогда не должны быть написаны в stderr, так как на уровнях детализации «нормальный» или «подробный» такие трассировки передаются по NuGet консоль.</span><span class="sxs-lookup"><span data-stu-id="ab127-132">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="ab127-133">Неожиданных значений параметров можно пропустить, предоставляя прямой совместимости с будущими версиями NuGet.</span><span class="sxs-lookup"><span data-stu-id="ab127-133">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ab127-134">Входные параметры</span><span class="sxs-lookup"><span data-stu-id="ab127-134">Input parameters</span></span>

| <span data-ttu-id="ab127-135">Параметр переключатель /</span><span class="sxs-lookup"><span data-stu-id="ab127-135">Parameter/Switch</span></span> |<span data-ttu-id="ab127-136">Описание</span><span class="sxs-lookup"><span data-stu-id="ab127-136">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="ab127-137">URI {value}</span><span class="sxs-lookup"><span data-stu-id="ab127-137">Uri {value}</span></span> | <span data-ttu-id="ab127-138">Требовать учетные данные URI источника пакета.</span><span class="sxs-lookup"><span data-stu-id="ab127-138">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="ab127-139">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="ab127-139">NonInteractive</span></span> | <span data-ttu-id="ab127-140">Если он имеется, поставщик не выдает интерактивные запросы.</span><span class="sxs-lookup"><span data-stu-id="ab127-140">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="ab127-141">IsRetry</span><span class="sxs-lookup"><span data-stu-id="ab127-141">IsRetry</span></span> | <span data-ttu-id="ab127-142">Если он присутствует, указывает эта попытка повтора ранее неудавшихся попыток.</span><span class="sxs-lookup"><span data-stu-id="ab127-142">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="ab127-143">Поставщики обычно используют этот флаг, чтобы они обхода любого существующего кэша и запрашивать новые учетные данные, если это возможно.</span><span class="sxs-lookup"><span data-stu-id="ab127-143">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="ab127-144">Уровень детализации {value}</span><span class="sxs-lookup"><span data-stu-id="ab127-144">Verbosity {value}</span></span> | <span data-ttu-id="ab127-145">Если он имеется, одно из следующих значений: «обычный», «тихом» или «подробно».</span><span class="sxs-lookup"><span data-stu-id="ab127-145">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="ab127-146">Если значение не указано, по умолчанию на «normal».</span><span class="sxs-lookup"><span data-stu-id="ab127-146">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="ab127-147">Поставщики должны использовать это как значение, указывающее уровень ведения журнала необязательно для вывода стандартный поток ошибок.</span><span class="sxs-lookup"><span data-stu-id="ab127-147">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="ab127-148">Коды завершения</span><span class="sxs-lookup"><span data-stu-id="ab127-148">Exit codes</span></span>

| <span data-ttu-id="ab127-149">Код</span><span class="sxs-lookup"><span data-stu-id="ab127-149">Code</span></span> |<span data-ttu-id="ab127-150">Результат</span><span class="sxs-lookup"><span data-stu-id="ab127-150">Result</span></span> | <span data-ttu-id="ab127-151">Описание</span><span class="sxs-lookup"><span data-stu-id="ab127-151">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="ab127-152">0</span><span class="sxs-lookup"><span data-stu-id="ab127-152">0</span></span> | <span data-ttu-id="ab127-153">Success</span><span class="sxs-lookup"><span data-stu-id="ab127-153">Success</span></span> | <span data-ttu-id="ab127-154">Учетные данные были успешно получены и были записаны в stdout.</span><span class="sxs-lookup"><span data-stu-id="ab127-154">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="ab127-155">1</span><span class="sxs-lookup"><span data-stu-id="ab127-155">1</span></span> | <span data-ttu-id="ab127-156">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="ab127-156">ProviderNotApplicable</span></span> | <span data-ttu-id="ab127-157">Текущий поставщик не предоставляет учетные данные для указанного URI.</span><span class="sxs-lookup"><span data-stu-id="ab127-157">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="ab127-158">2</span><span class="sxs-lookup"><span data-stu-id="ab127-158">2</span></span> | <span data-ttu-id="ab127-159">Failure</span><span class="sxs-lookup"><span data-stu-id="ab127-159">Failure</span></span> | <span data-ttu-id="ab127-160">Поставщик — это правильный поставщик для заданного URI, но не может предоставить учетные данные.</span><span class="sxs-lookup"><span data-stu-id="ab127-160">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="ab127-161">В этом случае nuget.exe не повторяет проверку подлинности и завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="ab127-161">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="ab127-162">Типичный пример — когда пользователь отменяет интерактивного входа в систему.</span><span class="sxs-lookup"><span data-stu-id="ab127-162">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="ab127-163">Стандартный вывод</span><span class="sxs-lookup"><span data-stu-id="ab127-163">Standard output</span></span>

| <span data-ttu-id="ab127-164">Свойство</span><span class="sxs-lookup"><span data-stu-id="ab127-164">Property</span></span> |<span data-ttu-id="ab127-165">Примечания</span><span class="sxs-lookup"><span data-stu-id="ab127-165">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="ab127-166">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="ab127-166">Username</span></span> | <span data-ttu-id="ab127-167">Имя пользователя для запросов проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ab127-167">Username for authenticated requests.</span></span>|
| <span data-ttu-id="ab127-168">Пароль</span><span class="sxs-lookup"><span data-stu-id="ab127-168">Password</span></span> | <span data-ttu-id="ab127-169">Пароль для запросов проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ab127-169">Password for authenticated requests.</span></span>|
| <span data-ttu-id="ab127-170">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ab127-170">Message</span></span> | <span data-ttu-id="ab127-171">Дополнительные сведения об ответе, используется только для отображения дополнительных сведений в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="ab127-171">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="ab127-172">Пример stdout:</span><span class="sxs-lookup"><span data-stu-id="ab127-172">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="ab127-173">Устранение неполадок поставщика учетных данных</span><span class="sxs-lookup"><span data-stu-id="ab127-173">Troubleshooting a credential provider</span></span>

<span data-ttu-id="ab127-174">В настоящее NuGet не поддерживает много непосредственно для отладки поставщики пользовательских учетных данных; [выдавать 4598](https://github.com/NuGet/Home/issues/4598) отслеживает эту работу.</span><span class="sxs-lookup"><span data-stu-id="ab127-174">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="ab127-175">Можно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ab127-175">You can also do the following:</span></span>

- <span data-ttu-id="ab127-176">Запустите nuget.exe с `-verbosity` коммутатора, чтобы просмотреть подробные выходные данные.</span><span class="sxs-lookup"><span data-stu-id="ab127-176">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="ab127-177">Добавлять сообщения отладки `stdout` в соответствующих местах.</span><span class="sxs-lookup"><span data-stu-id="ab127-177">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="ab127-178">Убедитесь, что вы используете nuget.exe 3.3 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ab127-178">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="ab127-179">Присоедините отладчик при запуске следующим фрагментом кода:</span><span class="sxs-lookup"><span data-stu-id="ab127-179">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="ab127-180">Для получения дополнительных сведений [отправить запрос на поддержку nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="ab127-180">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
