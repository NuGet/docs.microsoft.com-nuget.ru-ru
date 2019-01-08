---
title: Заметки о выпуске NuGet 4.9 RTM
description: 'Заметки о выпуске NuGet 4.9: известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.'
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 7dcb2e430ad80815f716f5567b511ff08acfe31b
ms.sourcegitcommit: a9babe261f67da0f714d168d04ea54a66628974b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2018
ms.locfileid: "53735140"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="9a56d-103">Заметки о выпуске NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="9a56d-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="9a56d-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="9a56d-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="9a56d-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="9a56d-105">NuGet version</span></span> | <span data-ttu-id="9a56d-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9a56d-106">Available in Visual Studio version</span></span>| <span data-ttu-id="9a56d-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="9a56d-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| <span data-ttu-id="9a56d-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="9a56d-108">**4.9.0**</span></span> | <span data-ttu-id="9a56d-109">Visual Studio 2017 версии 15.9.0</span><span class="sxs-lookup"><span data-stu-id="9a56d-109">Visual Studio 2017 version 15.9.0</span></span> | <span data-ttu-id="9a56d-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="9a56d-110">2.1.500, 2.2.100</span></span> |
| <span data-ttu-id="9a56d-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="9a56d-111">**4.9.1**</span></span> | <span data-ttu-id="9a56d-112">Н/Д</span><span class="sxs-lookup"><span data-stu-id="9a56d-112">n/a</span></span> | <span data-ttu-id="9a56d-113">Н/Д</span><span class="sxs-lookup"><span data-stu-id="9a56d-113">n/a</span></span> |
| [<span data-ttu-id="9a56d-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="9a56d-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="9a56d-115">Visual Studio 2017 версии 15.9.4</span><span class="sxs-lookup"><span data-stu-id="9a56d-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="9a56d-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="9a56d-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |

## <a name="summary-whats-new-in-490"></a><span data-ttu-id="9a56d-117">Сводка: Новые возможности версии 4.9.0</span><span class="sxs-lookup"><span data-stu-id="9a56d-117">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="9a56d-118">Подписи. Включение ClientPolicies для настройки требования использовать набор доверенных авторов и репозиториев, перечисленных в NuGet.Config, — [#6961](https://github.com/NuGet/Home/issues/6961), [запись блога](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html).</span><span class="sxs-lookup"><span data-stu-id="9a56d-118">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="9a56d-119">Создание файлов с расширением .snupkg для включения символов в пакет и оптимизация отправки для принятия протоколом NuGet файлов .snupkg для сервера символов — [#6878](https://github.com/NuGet/Home/issues/6878), [запись блога](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html).</span><span class="sxs-lookup"><span data-stu-id="9a56d-119">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="9a56d-120">Подключаемый модуль учетных данных версии 2 для NuGet — [#6642](https://github.com/NuGet/Home/issues/6642).</span><span class="sxs-lookup"><span data-stu-id="9a56d-120">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="9a56d-121">Автономные пакеты NuGet — лицензия — [#4628](https://github.com/NuGet/Home/issues/4628), [объявление](https://github.com/NuGet/Announcements/issues/32).</span><span class="sxs-lookup"><span data-stu-id="9a56d-121">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="9a56d-122">Включение согласия для метаданных GeneratePathProperty в PackageReference для создания свойства MSBuild для каждого пакета в каталоге Foo.Bar\1.0\" — [#6949](https://github.com/NuGet/Home/issues/6949).</span><span class="sxs-lookup"><span data-stu-id="9a56d-122">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="9a56d-123">Улучшение опыта использования NuGet клиентами — [#7108](https://github.com/NuGet/Home/issues/7108).</span><span class="sxs-lookup"><span data-stu-id="9a56d-123">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="9a56d-124">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="9a56d-124">Issues fixed in this release</span></span>

* <span data-ttu-id="9a56d-125">После предупреждений, преобразованных в ошибки (с помощью WarnAsErrors) и вызываемых PackageExtraction, не должен оставаться извлеченный пакет — [#7445](https://github.com/NuGet/Home/issues/7445).</span><span class="sxs-lookup"><span data-stu-id="9a56d-125">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="9a56d-126">Неправильно подписанные пакеты не должны попадать в папку установки глобальных пакетов — [#7423](https://github.com/NuGet/Home/issues/7423).</span><span class="sxs-lookup"><span data-stu-id="9a56d-126">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="9a56d-127">Привязка поколения перенаправления не должна пропускать фасадные сборки — [#7393](https://github.com/NuGet/Home/issues/7393).</span><span class="sxs-lookup"><span data-stu-id="9a56d-127">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="9a56d-128">VersionRange Equals не сравнивает плавающие диапазоны — [#7324](https://github.com/NuGet/Home/issues/7324).</span><span class="sxs-lookup"><span data-stu-id="9a56d-128">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="9a56d-129">Восстановление. Снижение производительности при использовании HTTP-стека .NET Core 2.1 — [#7314](https://github.com/NuGet/Home/issues/7314).</span><span class="sxs-lookup"><span data-stu-id="9a56d-129">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="9a56d-130">Обновление пакета не должно изменять PrivateAssets в PackageReference — [#7285](https://github.com/NuGet/Home/issues/7285).</span><span class="sxs-lookup"><span data-stu-id="9a56d-130">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="9a56d-131">Подписи. Подписывание не выполняется, если в пакете содержится слишком много записей пакета (> 65 534) — [#7248](https://github.com/NuGet/Home/issues/7248).</span><span class="sxs-lookup"><span data-stu-id="9a56d-131">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="9a56d-132">Путь к коду dotnet nuget push должен поддерживать новый поставщик учетных данных — [#7233](https://github.com/NuGet/Home/issues/7233).</span><span class="sxs-lookup"><span data-stu-id="9a56d-132">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="9a56d-133">Поддержка выполнения подключаемых модулей с помощью инвариантного языка и региональных параметров (как в Docker) — [#7223](https://github.com/NuGet/Home/issues/7223).</span><span class="sxs-lookup"><span data-stu-id="9a56d-133">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="9a56d-134">При добавлении источников NuGet не должны удаляться учетные данные из NuGet.config — [#7200](https://github.com/NuGet/Home/issues/7200).</span><span class="sxs-lookup"><span data-stu-id="9a56d-134">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="9a56d-135">Установка devDependency PackageReference по умолчанию должна происходить в excludeassets=compile — [#7084](https://github.com/NuGet/Home/issues/7084).</span><span class="sxs-lookup"><span data-stu-id="9a56d-135">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="9a56d-136">Отображение средства переноса для всех проектов и сообщения об ошибке при несовместимости проекта — [#6958](https://github.com/NuGet/Home/issues/6958).</span><span class="sxs-lookup"><span data-stu-id="9a56d-136">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="9a56d-137">Dotnet add package должен фиксировать восстановления, выполняемые для файла ресурсов — [#6928](https://github.com/NuGet/Home/issues/6928).</span><span class="sxs-lookup"><span data-stu-id="9a56d-137">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="9a56d-138">Подписи. Улучшены сообщения об ошибках, связанные с подписями, — [#6906](https://github.com/NuGet/Home/issues/6906).</span><span class="sxs-lookup"><span data-stu-id="9a56d-138">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="9a56d-139">[Сбой теста][zh-TW]. Строка Package Manager Console не локализована в консоли диспетчера пакетов — [#6381](https://github.com/NuGet/Home/issues/6381).</span><span class="sxs-lookup"><span data-stu-id="9a56d-139">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="9a56d-140">Сообщение об ошибке Unable to find project information (Не удалось найти сведения о проекте) должно быть более информативным в VS — [#5350](https://github.com/NuGet/Home/issues/5350).</span><span class="sxs-lookup"><span data-stu-id="9a56d-140">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="9a56d-141">Неинформативное сообщение об ошибке при неправильном использовании тега версии nuspec пакета NuGet — [#2714](https://github.com/NuGet/Home/issues/2714).</span><span class="sxs-lookup"><span data-stu-id="9a56d-141">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="9a56d-142">DCR — подписи. Поддержка протокола NuGet: ресурс RepositorySignatures/4.9.0 — [#7421](https://github.com/NuGet/Home/issues/7421).</span><span class="sxs-lookup"><span data-stu-id="9a56d-142">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="9a56d-143">DCR — во время извлечения пакета теперь будет создаваться файл метаданных .nupkg с хэш-кодом содержимого — [#7283](https://github.com/NuGet/Home/issues/7283).</span><span class="sxs-lookup"><span data-stu-id="9a56d-143">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="9a56d-144">DCR — пропуск проверки аутентичности кода подключаемых модулей при выполнении в Mono — [#7222](https://github.com/NuGet/Home/issues/7222).</span><span class="sxs-lookup"><span data-stu-id="9a56d-144">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="9a56d-145">Список всех проблем, исправленных в выпуске 4.9.0</span><span class="sxs-lookup"><span data-stu-id="9a56d-145">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="9a56d-146">Сводка: Новые возможности версии 4.9.1</span><span class="sxs-lookup"><span data-stu-id="9a56d-146">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="9a56d-147">Добавлена поддержка чтения записи в файл nuget.config с помощью новой команды trusted-signers — [#7480](https://github.com/NuGet/Home/issues/7480).</span><span class="sxs-lookup"><span data-stu-id="9a56d-147">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="9a56d-148">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="9a56d-148">Issues fixed in this release</span></span>

* <span data-ttu-id="9a56d-149">Исправлена функция создания ссылок лицензии — [#7515](https://github.com/NuGet/Home/issues/7515).</span><span class="sxs-lookup"><span data-stu-id="9a56d-149">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="9a56d-150">Коды ошибок регрессии для проверки подписей — [#7492](https://github.com/NuGet/Home/issues/7492).</span><span class="sxs-lookup"><span data-stu-id="9a56d-150">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="9a56d-151">Пакет NuGet.Build.Tasks.Pack не включает сведения о лицензиях — [#7379](https://github.com/NuGet/Home/issues/7379).</span><span class="sxs-lookup"><span data-stu-id="9a56d-151">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="9a56d-152">Список всех проблем, исправленных в выпуске 4.9.1</span><span class="sxs-lookup"><span data-stu-id="9a56d-152">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="9a56d-153">Сводка: Новые возможности версии 4.9.2</span><span class="sxs-lookup"><span data-stu-id="9a56d-153">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="9a56d-154">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="9a56d-154">Issues fixed in this release</span></span>

* <span data-ttu-id="9a56d-155">VS/dotnet.exe/nuget.exe/msbuild.exe (восстановление) не использует учетные данные, если имя источника содержит пробел, — [#7517](https://github.com/NuGet/Home/issues/7517).</span><span class="sxs-lookup"><span data-stu-id="9a56d-155">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="9a56d-156">Проблемы с доступом к LicenseAcceptanceWindow и LicenseFileWindow — [#7452](https://github.com/NuGet/Home/issues/7452).</span><span class="sxs-lookup"><span data-stu-id="9a56d-156">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="9a56d-157">Исправлено FormatException в DateTime.Parse из DateTimeConverter — [#7539](https://github.com/NuGet/Home/issues/7539).</span><span class="sxs-lookup"><span data-stu-id="9a56d-157">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="9a56d-158">Список всех проблем, исправленных в выпуске 4.9.2</span><span class="sxs-lookup"><span data-stu-id="9a56d-158">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="known-issues"></a><span data-ttu-id="9a56d-159">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="9a56d-159">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="9a56d-160">Выполнение команды dotnet nuget push с параметром --interactive выдает сообщение об ошибке на компьютере Mac.</span><span class="sxs-lookup"><span data-stu-id="9a56d-160">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="9a56d-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="9a56d-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="9a56d-162">Проблемы</span><span class="sxs-lookup"><span data-stu-id="9a56d-162">Issue</span></span>
<span data-ttu-id="9a56d-163">Аргумент `--interactive` не перенаправляется интерфейсом командной строки dotnet, что приводит к ошибке `error: Missing value for option 'interactive'`.</span><span class="sxs-lookup"><span data-stu-id="9a56d-163">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="9a56d-164">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="9a56d-164">Workaround</span></span>
<span data-ttu-id="9a56d-165">Выполните любую другую команду dotnet с параметром interactive, например `dotnet restore --interactive`, и пройдите проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="9a56d-165">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="9a56d-166">Результат проверки подлинности затем может быть кэширован поставщиком учетных данных.</span><span class="sxs-lookup"><span data-stu-id="9a56d-166">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="9a56d-167">Затем выполните `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="9a56d-167">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="9a56d-168">Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи.</span><span class="sxs-lookup"><span data-stu-id="9a56d-168">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="9a56d-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="9a56d-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="9a56d-170">Проблемы</span><span class="sxs-lookup"><span data-stu-id="9a56d-170">Issue</span></span>
<span data-ttu-id="9a56d-171">При использовании dotnet.exe 2.x для восстановления проекта с несколькими целевыми объектами (netcoreapp 1.x и netcoreapp 2.x) резервная папка обрабатывается как веб-канал файла.</span><span class="sxs-lookup"><span data-stu-id="9a56d-171">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="9a56d-172">Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="9a56d-172">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="9a56d-173">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="9a56d-173">Workaround</span></span>
<span data-ttu-id="9a56d-174">Отключите использование резервной папки, очистив значение для `RestoreAdditionalProjectSources`.</span><span class="sxs-lookup"><span data-stu-id="9a56d-174">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="9a56d-175">`<RestoreAdditionalProjectSources/>` Соблюдайте при этом осторожность, так как это приведет к скачиванию большого количества пакетов с NuGet.org, которые иначе были бы восстановлены из резервной папки.</span><span class="sxs-lookup"><span data-stu-id="9a56d-175">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
