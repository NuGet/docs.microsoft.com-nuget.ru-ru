---
title: Заметки о выпуске NuGet 4.9 RTM
description: 'Заметки о выпуске NuGet 4.9: известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.'
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453780"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="74244-103">Заметки о выпуске NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="74244-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="74244-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) включает в себя функции NuGet 4.9.0.</span><span class="sxs-lookup"><span data-stu-id="74244-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.9.0 functionality.</span></span>


<span data-ttu-id="74244-105">Также доступны версии этого компонента для командной строки:</span><span class="sxs-lookup"><span data-stu-id="74244-105">Command line versions of the same functionality are also available:</span></span>
* <span data-ttu-id="74244-106">NuGet.exe 4.9 — [nuget.org/downloads](https://nuget.org/downloads);</span><span class="sxs-lookup"><span data-stu-id="74244-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span></span>
* <span data-ttu-id="74244-107">DotNet.exe — [пакет SDK 2.1.500 для .NET Core](https://www.microsoft.com/net/download/visual-studio-sdks).</span><span class="sxs-lookup"><span data-stu-id="74244-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span></span>


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="74244-108">Сводка. Новые возможности версии 4.9.0</span><span class="sxs-lookup"><span data-stu-id="74244-108">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="74244-109">Подписи. Включение ClientPolicies для настройки требования использовать набор доверенных авторов и репозиториев, перечисленных в NuGet.Config, — [#6961](https://github.com/NuGet/Home/issues/6961).</span><span class="sxs-lookup"><span data-stu-id="74244-109">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span></span>

* <span data-ttu-id="74244-110">Создание файлов с расширением .snupkg для включения символов в пакет и оптимизация отправки для принятия протоколом NuGet файлов .snupkg для сервера символов — [#6878](https://github.com/NuGet/Home/issues/6878).</span><span class="sxs-lookup"><span data-stu-id="74244-110">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878)</span></span>

* <span data-ttu-id="74244-111">Подключаемый модуль учетных данных версии 2 для NuGet — [#6642](https://github.com/NuGet/Home/issues/6642).</span><span class="sxs-lookup"><span data-stu-id="74244-111">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="74244-112">Автономные пакеты NuGet — лицензия — [#4628](https://github.com/NuGet/Home/issues/4628).</span><span class="sxs-lookup"><span data-stu-id="74244-112">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628)</span></span>

* <span data-ttu-id="74244-113">Включение согласия для метаданных GeneratePathProperty в PackageReference для создания свойства MSBuild для каждого пакета в каталоге Foo.Bar\1.0\" — [#6949](https://github.com/NuGet/Home/issues/6949).</span><span class="sxs-lookup"><span data-stu-id="74244-113">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="74244-114">Улучшение опыта использования NuGet клиентами — [#7108](https://github.com/NuGet/Home/issues/7108).</span><span class="sxs-lookup"><span data-stu-id="74244-114">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="74244-115">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="74244-115">Issues fixed in this release</span></span>

* <span data-ttu-id="74244-116">После предупреждений, преобразованных в ошибки (с помощью WarnAsErrors) и вызываемых PackageExtraction, не должен оставаться извлеченный пакет — [#7445](https://github.com/NuGet/Home/issues/7445).</span><span class="sxs-lookup"><span data-stu-id="74244-116">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="74244-117">Неправильно подписанные пакеты не должны попадать в папку установки глобальных пакетов — [#7423](https://github.com/NuGet/Home/issues/7423).</span><span class="sxs-lookup"><span data-stu-id="74244-117">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="74244-118">Привязка поколения перенаправления не должна пропускать фасадные сборки — [#7393](https://github.com/NuGet/Home/issues/7393).</span><span class="sxs-lookup"><span data-stu-id="74244-118">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="74244-119">VersionRange Equals не сравнивает плавающие диапазоны — [#7324](https://github.com/NuGet/Home/issues/7324).</span><span class="sxs-lookup"><span data-stu-id="74244-119">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="74244-120">Восстановление. Снижение производительности при использовании HTTP-стека .NET Core 2.1 — [#7314](https://github.com/NuGet/Home/issues/7314).</span><span class="sxs-lookup"><span data-stu-id="74244-120">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="74244-121">Обновление пакета не должно изменять PrivateAssets в PackageReference — [#7285](https://github.com/NuGet/Home/issues/7285).</span><span class="sxs-lookup"><span data-stu-id="74244-121">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="74244-122">Подписи. Подписывание не выполняется, если в пакете содержится слишком много записей пакета (> 65 534) — [#7248](https://github.com/NuGet/Home/issues/7248).</span><span class="sxs-lookup"><span data-stu-id="74244-122">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="74244-123">Путь к коду dotnet nuget push должен поддерживать новый поставщик учетных данных — [#7233](https://github.com/NuGet/Home/issues/7233).</span><span class="sxs-lookup"><span data-stu-id="74244-123">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="74244-124">Поддержка выполнения подключаемых модулей с помощью инвариантного языка и региональных параметров (как в Docker) — [#7223](https://github.com/NuGet/Home/issues/7223).</span><span class="sxs-lookup"><span data-stu-id="74244-124">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="74244-125">При добавлении источников NuGet не должны удаляться учетные данные из NuGet.config — [#7200](https://github.com/NuGet/Home/issues/7200).</span><span class="sxs-lookup"><span data-stu-id="74244-125">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="74244-126">Установка devDependency PackageReference по умолчанию должна происходить в excludeassets=compile — [#7084](https://github.com/NuGet/Home/issues/7084).</span><span class="sxs-lookup"><span data-stu-id="74244-126">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="74244-127">Отображение средства переноса для всех проектов и сообщения об ошибке при несовместимости проекта — [#6958](https://github.com/NuGet/Home/issues/6958).</span><span class="sxs-lookup"><span data-stu-id="74244-127">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="74244-128">Dotnet add package должен фиксировать восстановления, выполняемые для файла ресурсов — [#6928](https://github.com/NuGet/Home/issues/6928).</span><span class="sxs-lookup"><span data-stu-id="74244-128">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="74244-129">Подписи. Улучшены сообщения об ошибках, связанные с подписями, — [#6906](https://github.com/NuGet/Home/issues/6906).</span><span class="sxs-lookup"><span data-stu-id="74244-129">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="74244-130">[Сбой теста][zh-TW]. Строка Package Manager Console не локализована в консоли диспетчера пакетов — [#6381](https://github.com/NuGet/Home/issues/6381).</span><span class="sxs-lookup"><span data-stu-id="74244-130">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="74244-131">Сообщение об ошибке Unable to find project information (Не удалось найти сведения о проекте) должно быть более информативным в VS — [#5350](https://github.com/NuGet/Home/issues/5350).</span><span class="sxs-lookup"><span data-stu-id="74244-131">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="74244-132">Неинформативное сообщение об ошибке при неправильном использовании тега версии nuspec пакета NuGet — [#2714](https://github.com/NuGet/Home/issues/2714).</span><span class="sxs-lookup"><span data-stu-id="74244-132">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="74244-133">DCR — подписи. Поддержка протокола NuGet: RepositorySignatures/4.9.0 — [#7421](https://github.com/NuGet/Home/issues/7421).</span><span class="sxs-lookup"><span data-stu-id="74244-133">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="74244-134">DCR — во время извлечения пакета теперь будет создаваться файл метаданных .nupkg с хэш-кодом содержимого — [#7283](https://github.com/NuGet/Home/issues/7283).</span><span class="sxs-lookup"><span data-stu-id="74244-134">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="74244-135">DCR — пропуск проверки аутентичности кода подключаемых модулей при выполнении в Mono — [#7222](https://github.com/NuGet/Home/issues/7222).</span><span class="sxs-lookup"><span data-stu-id="74244-135">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="74244-136">Список всех проблем, исправленных в выпуске 4.9.0</span><span class="sxs-lookup"><span data-stu-id="74244-136">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="74244-137">Сводка. Новые возможности версии 4.9.1</span><span class="sxs-lookup"><span data-stu-id="74244-137">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="74244-138">Добавлена поддержка чтения записи в файл nuget.config с помощью новой команды trusted-signers — [#7480](https://github.com/NuGet/Home/issues/7480).</span><span class="sxs-lookup"><span data-stu-id="74244-138">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="74244-139">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="74244-139">Issues fixed in this release</span></span>

* <span data-ttu-id="74244-140">Исправлена функция создания ссылок лицензии — [#7515](https://github.com/NuGet/Home/issues/7515).</span><span class="sxs-lookup"><span data-stu-id="74244-140">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="74244-141">Коды ошибок регрессии для проверки подписей — [#7492](https://github.com/NuGet/Home/issues/7492).</span><span class="sxs-lookup"><span data-stu-id="74244-141">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="74244-142">Пакет NuGet.Build.Tasks.Pack не включает сведения о лицензиях — [#7379](https://github.com/NuGet/Home/issues/7379).</span><span class="sxs-lookup"><span data-stu-id="74244-142">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="74244-143">Список всех проблем, исправленных в выпуске 4.9.1</span><span class="sxs-lookup"><span data-stu-id="74244-143">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a><span data-ttu-id="74244-144">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="74244-144">Known issues</span></span>

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a><span data-ttu-id="74244-145">Dotnet.exe/nuget.exe не использует учетные данные, если имя источника содержит пробел — [#7517](https://github.com/NuGet/Home/issues/7517).</span><span class="sxs-lookup"><span data-stu-id="74244-145">dotnet.exe/nuget.exe doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

#### <a name="issue"></a><span data-ttu-id="74244-146">Проблемы</span><span class="sxs-lookup"><span data-stu-id="74244-146">Issue</span></span>
<span data-ttu-id="74244-147">При наличии пробела в имени источника nuget.exe выдает примерно такое сообщение об ошибке: `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`.</span><span class="sxs-lookup"><span data-stu-id="74244-147">When there is a whitespace in the source name, nuget.exe throws an error like `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span></span>

#### <a name="workaround"></a><span data-ttu-id="74244-148">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="74244-148">Workaround</span></span>
<span data-ttu-id="74244-149">Измените имя источника, исключив из него пробел.</span><span class="sxs-lookup"><span data-stu-id="74244-149">Change the name of the source to not contain a whitespace.</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="74244-150">Выполнение команды dotnet nuget push с параметром --interactive выдает сообщение об ошибке на компьютере Mac.</span><span class="sxs-lookup"><span data-stu-id="74244-150">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="74244-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="74244-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="74244-152">Проблемы</span><span class="sxs-lookup"><span data-stu-id="74244-152">Issue</span></span>
<span data-ttu-id="74244-153">Аргумент `--interactive` не перенаправляется интерфейсом командной строки dotnet, что приводит к ошибке `error: Missing value for option 'interactive'`.</span><span class="sxs-lookup"><span data-stu-id="74244-153">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="74244-154">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="74244-154">Workaround</span></span>
<span data-ttu-id="74244-155">Выполните любую другую команду dotnet с параметром interactive, например `dotnet restore --interactive`, и пройдите проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="74244-155">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="74244-156">Результат проверки подлинности затем может быть кэширован поставщиком учетных данных.</span><span class="sxs-lookup"><span data-stu-id="74244-156">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="74244-157">Затем выполните `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="74244-157">Then run `dotnet nuget push`.</span></span>

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a><span data-ttu-id="74244-158">Проблемы с доступом к LicenseAcceptanceWindow и LicenseFileWindow — [#7452](https://github.com/NuGet/Home/issues/7452).</span><span class="sxs-lookup"><span data-stu-id="74244-158">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

#### <a name="issue"></a><span data-ttu-id="74244-159">Проблемы</span><span class="sxs-lookup"><span data-stu-id="74244-159">Issue</span></span>
<span data-ttu-id="74244-160">Окна принятия условий лицензии и отображения файла лицензии не поддерживают доступ с помощью клавиатуры и речевого ввода при использовании средства чтения с экрана и JAWS.</span><span class="sxs-lookup"><span data-stu-id="74244-160">The license acceptance window and license file window have accessibility issues with keyboard navigation and narration with screen reader and JAWS.</span></span>

#### <a name="workaround"></a><span data-ttu-id="74244-161">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="74244-161">Workaround</span></span>
<span data-ttu-id="74244-162">Обходное решение отсутствует.</span><span class="sxs-lookup"><span data-stu-id="74244-162">No workaround.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="74244-163">Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи.</span><span class="sxs-lookup"><span data-stu-id="74244-163">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="74244-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="74244-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="74244-165">Проблемы</span><span class="sxs-lookup"><span data-stu-id="74244-165">Issue</span></span>
<span data-ttu-id="74244-166">При использовании dotnet.exe 2.x для восстановления проекта с несколькими целевыми объектами (netcoreapp 1.x и netcoreapp 2.x) резервная папка обрабатывается как веб-канал файла.</span><span class="sxs-lookup"><span data-stu-id="74244-166">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="74244-167">Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="74244-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="74244-168">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="74244-168">Workaround</span></span>
<span data-ttu-id="74244-169">Отключите использование резервной папки, очистив значение для `RestoreAdditionalProjectSources`.</span><span class="sxs-lookup"><span data-stu-id="74244-169">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="74244-170">`<RestoreAdditionalProjectSources/>` Соблюдайте при этом осторожность, так как это приведет к скачиванию большого количества пакетов с NuGet.org, которые иначе были бы восстановлены из резервной папки.</span><span class="sxs-lookup"><span data-stu-id="74244-170">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
