---
title: Поставщики учетных данных NuGet.exe
description: NuGet.exe поставщиков учетных данных проверки подлинности в веб-канала и реализуются как исполняемые файлы командной строки, соблюдать определенные соглашения.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: ebd3354c298eae8bc8158a987327374ac4a8d4f0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818764"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="ac63a-103">Проверка подлинности веб-каналы через поставщиков учетных данных nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ac63a-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="ac63a-104">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="ac63a-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="ac63a-105">Когда `nuget.exe` требуются учетные данные для проверки подлинности для веб-канал, он ищет их следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ac63a-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ac63a-106">NuGet сначала ищет учетные данные в `Nuget.Config` файлов.</span><span class="sxs-lookup"><span data-stu-id="ac63a-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="ac63a-107">Затем NuGet использует поставщики подключаемый модуль учетных данных, может быть порядке, указанном ниже.</span><span class="sxs-lookup"><span data-stu-id="ac63a-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="ac63a-108">(И пример является [Visual Studio Team Services учетных данных Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="ac63a-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="ac63a-109">Затем NuGet запрашивает у пользователя учетные данные в командной строке.</span><span class="sxs-lookup"><span data-stu-id="ac63a-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="ac63a-110">Обратите внимание, что поставщики учетных данных описанные здесь работает только в `nuget.exe` , а не в Visual Studio или «dotnet восстановления».</span><span class="sxs-lookup"><span data-stu-id="ac63a-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="ac63a-111">Поставщики учетных данных с помощью Visual Studio, в разделе [nuget.exe поставщиков учетных данных для Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="ac63a-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="ac63a-112">NuGet.exe поставщиков учетных данных можно использовать в тремя способами:</span><span class="sxs-lookup"><span data-stu-id="ac63a-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="ac63a-113">**Глобально**: чтобы сделать доступными для всех экземпляров поставщика учетных данных `nuget.exe` запустите профиля текущего пользователя, добавьте ее в `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="ac63a-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="ac63a-114">Может потребоваться создать `CredentialProviders` папку.</span><span class="sxs-lookup"><span data-stu-id="ac63a-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="ac63a-115">Поставщики учетных данных можно установить в корне `CredentialProviders` папки или вложенной папки.</span><span class="sxs-lookup"><span data-stu-id="ac63a-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="ac63a-116">Если поставщик учетных данных содержит несколько файлов и сборок, можно использовать вложенные папки для сохранения организованы поставщиков.</span><span class="sxs-lookup"><span data-stu-id="ac63a-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="ac63a-117">**Из переменной среды**: поставщиков учетных данных можно хранить в любом месте и получить доступ к ним `nuget.exe` , установив `%NUGET_CREDENTIALPROVIDERS_PATH%` переменную среды, чтобы расположение поставщика.</span><span class="sxs-lookup"><span data-stu-id="ac63a-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="ac63a-118">Эта переменная может быть список разделенных точкой с запятой (например, `path1;path2`) Если у вас есть несколько расположений.</span><span class="sxs-lookup"><span data-stu-id="ac63a-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="ac63a-119">**Наряду с nuget.exe**: nuget.exe поставщиков учетных данных может размещаться в той же папке, что `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ac63a-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="ac63a-120">При загрузке поставщиков учетных данных, `nuget.exe` поиск вышеуказанных местах в указанном порядке, для любого файла с именем `credentialprovider*.exe`, затем загружает их в порядке, они были найдены.</span><span class="sxs-lookup"><span data-stu-id="ac63a-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="ac63a-121">Если несколько поставщиков учетных данных в той же папке, они загружаются в алфавитном порядке.</span><span class="sxs-lookup"><span data-stu-id="ac63a-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="ac63a-122">Создание поставщика учетных данных nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ac63a-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="ac63a-123">Поставщик учетных данных — исполняемый файл командной строки с именем в форме `CredentialProvider*.exe`, собирает входных данных получает учетные данные, соответствующие и затем возвращает код состояния соответствующие выхода и стандартные выходные данные.</span><span class="sxs-lookup"><span data-stu-id="ac63a-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="ac63a-124">Поставщик должен выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="ac63a-124">A provider must do the following:</span></span>

- <span data-ttu-id="ac63a-125">Определите ли его можно указать учетные данные для целевого URI перед запуском процесса получения учетных данных.</span><span class="sxs-lookup"><span data-stu-id="ac63a-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="ac63a-126">В противном случае возвращается код состояния 1 без учетных данных.</span><span class="sxs-lookup"><span data-stu-id="ac63a-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="ac63a-127">Не изменяйте `Nuget.Config` (например, существует задание учетных данных).</span><span class="sxs-lookup"><span data-stu-id="ac63a-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="ac63a-128">Конфигурация прокси-сервера HTTP дескриптор в себе, как NuGet не предоставляет сведения о прокси подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="ac63a-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="ac63a-129">Возвращает учетные данные или сведения об ошибке для `nuget.exe` путем написания объект ответа JSON (см. ниже) в stdout, в кодировке UTF-8.</span><span class="sxs-lookup"><span data-stu-id="ac63a-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="ac63a-130">При необходимости выдает ведения журнала трассировки дополнительных в stderr.</span><span class="sxs-lookup"><span data-stu-id="ac63a-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="ac63a-131">Не секреты никогда не должны быть написаны в stderr, так как на уровнях детализации «нормальный» или «подробный» такие трассировки передаются по NuGet консоль.</span><span class="sxs-lookup"><span data-stu-id="ac63a-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="ac63a-132">Неожиданных значений параметров можно пропустить, предоставляя прямой совместимости с будущими версиями NuGet.</span><span class="sxs-lookup"><span data-stu-id="ac63a-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ac63a-133">Входные параметры</span><span class="sxs-lookup"><span data-stu-id="ac63a-133">Input parameters</span></span>

| <span data-ttu-id="ac63a-134">Параметр переключатель /</span><span class="sxs-lookup"><span data-stu-id="ac63a-134">Parameter/Switch</span></span> |<span data-ttu-id="ac63a-135">Описание:</span><span class="sxs-lookup"><span data-stu-id="ac63a-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="ac63a-136">URI {value}</span><span class="sxs-lookup"><span data-stu-id="ac63a-136">Uri {value}</span></span> | <span data-ttu-id="ac63a-137">Требовать учетные данные URI источника пакета.</span><span class="sxs-lookup"><span data-stu-id="ac63a-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="ac63a-138">Неинтерактивные</span><span class="sxs-lookup"><span data-stu-id="ac63a-138">NonInteractive</span></span> | <span data-ttu-id="ac63a-139">Если он имеется, поставщик не выдает интерактивные запросы.</span><span class="sxs-lookup"><span data-stu-id="ac63a-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="ac63a-140">IsRetry</span><span class="sxs-lookup"><span data-stu-id="ac63a-140">IsRetry</span></span> | <span data-ttu-id="ac63a-141">Если он присутствует, указывает эта попытка повтора ранее неудавшихся попыток.</span><span class="sxs-lookup"><span data-stu-id="ac63a-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="ac63a-142">Поставщики обычно используют этот флаг, чтобы они обхода любого существующего кэша и запрашивать новые учетные данные, если это возможно.</span><span class="sxs-lookup"><span data-stu-id="ac63a-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="ac63a-143">Уровень детализации {value}</span><span class="sxs-lookup"><span data-stu-id="ac63a-143">Verbosity {value}</span></span> | <span data-ttu-id="ac63a-144">Если он имеется, одно из следующих значений: «обычный», «тихом» или «подробно».</span><span class="sxs-lookup"><span data-stu-id="ac63a-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="ac63a-145">Если значение не указано, по умолчанию на «normal».</span><span class="sxs-lookup"><span data-stu-id="ac63a-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="ac63a-146">Поставщики должны использовать это как значение, указывающее уровень ведения журнала необязательно для вывода стандартный поток ошибок.</span><span class="sxs-lookup"><span data-stu-id="ac63a-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="ac63a-147">Коды выхода</span><span class="sxs-lookup"><span data-stu-id="ac63a-147">Exit codes</span></span>

| <span data-ttu-id="ac63a-148">Код</span><span class="sxs-lookup"><span data-stu-id="ac63a-148">Code</span></span> |<span data-ttu-id="ac63a-149">Результат</span><span class="sxs-lookup"><span data-stu-id="ac63a-149">Result</span></span> | <span data-ttu-id="ac63a-150">Описание:</span><span class="sxs-lookup"><span data-stu-id="ac63a-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="ac63a-151">0</span><span class="sxs-lookup"><span data-stu-id="ac63a-151">0</span></span> | <span data-ttu-id="ac63a-152">Success</span><span class="sxs-lookup"><span data-stu-id="ac63a-152">Success</span></span> | <span data-ttu-id="ac63a-153">Учетные данные были успешно получены и были записаны в stdout.</span><span class="sxs-lookup"><span data-stu-id="ac63a-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="ac63a-154">1</span><span class="sxs-lookup"><span data-stu-id="ac63a-154">1</span></span> | <span data-ttu-id="ac63a-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="ac63a-155">ProviderNotApplicable</span></span> | <span data-ttu-id="ac63a-156">Текущий поставщик не предоставляет учетные данные для указанного URI.</span><span class="sxs-lookup"><span data-stu-id="ac63a-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="ac63a-157">2</span><span class="sxs-lookup"><span data-stu-id="ac63a-157">2</span></span> | <span data-ttu-id="ac63a-158">Failure</span><span class="sxs-lookup"><span data-stu-id="ac63a-158">Failure</span></span> | <span data-ttu-id="ac63a-159">Поставщик — это правильный поставщик для заданного URI, но не может предоставить учетные данные.</span><span class="sxs-lookup"><span data-stu-id="ac63a-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="ac63a-160">В этом случае nuget.exe не повторяет проверку подлинности и завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="ac63a-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="ac63a-161">Типичный пример — когда пользователь отменяет интерактивного входа в систему.</span><span class="sxs-lookup"><span data-stu-id="ac63a-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="ac63a-162">Стандартный вывод</span><span class="sxs-lookup"><span data-stu-id="ac63a-162">Standard output</span></span>

| <span data-ttu-id="ac63a-163">Свойство.</span><span class="sxs-lookup"><span data-stu-id="ac63a-163">Property</span></span> |<span data-ttu-id="ac63a-164">Примечания</span><span class="sxs-lookup"><span data-stu-id="ac63a-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="ac63a-165">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="ac63a-165">Username</span></span> | <span data-ttu-id="ac63a-166">Имя пользователя для запросов проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ac63a-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="ac63a-167">Пароль</span><span class="sxs-lookup"><span data-stu-id="ac63a-167">Password</span></span> | <span data-ttu-id="ac63a-168">Пароль для запросов проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ac63a-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="ac63a-169">Сообщение</span><span class="sxs-lookup"><span data-stu-id="ac63a-169">Message</span></span> | <span data-ttu-id="ac63a-170">Дополнительные сведения об ответе, используется только для отображения дополнительных сведений в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="ac63a-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="ac63a-171">Пример stdout:</span><span class="sxs-lookup"><span data-stu-id="ac63a-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="ac63a-172">Устранение неполадок поставщика учетных данных</span><span class="sxs-lookup"><span data-stu-id="ac63a-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="ac63a-173">В настоящее NuGet не поддерживает много непосредственно для отладки поставщики пользовательских учетных данных; [выдавать 4598](https://github.com/NuGet/Home/issues/4598) отслеживает эту работу.</span><span class="sxs-lookup"><span data-stu-id="ac63a-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="ac63a-174">Можно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ac63a-174">You can also do the following:</span></span>

- <span data-ttu-id="ac63a-175">Запустите nuget.exe с `-verbosity` коммутатора, чтобы просмотреть подробные выходные данные.</span><span class="sxs-lookup"><span data-stu-id="ac63a-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="ac63a-176">Добавлять сообщения отладки `stdout` в соответствующих местах.</span><span class="sxs-lookup"><span data-stu-id="ac63a-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="ac63a-177">Убедитесь, что вы используете nuget.exe 3.3 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="ac63a-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="ac63a-178">Присоедините отладчик при запуске следующим фрагментом кода:</span><span class="sxs-lookup"><span data-stu-id="ac63a-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="ac63a-179">Для получения дополнительных сведений [отправить запрос на поддержку nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="ac63a-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
