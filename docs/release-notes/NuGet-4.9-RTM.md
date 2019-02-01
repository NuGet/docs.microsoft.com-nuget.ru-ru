---
title: Заметки о выпуске NuGet 4.9 RTM
description: 'Заметки о выпуске NuGet 4.9: известные проблемы, исправления ошибок, добавленные функции и запросы на изменение структуры.'
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 99578c5ed7e88b7269872bf88c465bbda462870a
ms.sourcegitcommit: 585394f063e95dcbc24d7ac0ce07de643eaf6f4d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2019
ms.locfileid: "55045112"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="d9713-103">Заметки о выпуске NuGet 4.9</span><span class="sxs-lookup"><span data-stu-id="d9713-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="d9713-104">Средства распространения NuGet:</span><span class="sxs-lookup"><span data-stu-id="d9713-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d9713-105">Версия NuGet</span><span class="sxs-lookup"><span data-stu-id="d9713-105">NuGet version</span></span> | <span data-ttu-id="d9713-106">Доступно в версии Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d9713-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d9713-107">Доступно в пакетах SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="d9713-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d9713-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="d9713-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d9713-109">Visual Studio 2017 версии 15.9.0</span><span class="sxs-lookup"><span data-stu-id="d9713-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="d9713-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="d9713-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="d9713-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="d9713-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="d9713-112">Н/Д</span><span class="sxs-lookup"><span data-stu-id="d9713-112">n/a</span></span> | <span data-ttu-id="d9713-113">Н/Д</span><span class="sxs-lookup"><span data-stu-id="d9713-113">n/a</span></span> |
| [<span data-ttu-id="d9713-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="d9713-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="d9713-115">Visual Studio 2017 версии 15.9.4</span><span class="sxs-lookup"><span data-stu-id="d9713-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="d9713-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="d9713-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="d9713-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="d9713-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="d9713-118">Visual Studio 2017 версии 15.9.6</span><span class="sxs-lookup"><span data-stu-id="d9713-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d9713-119">Н/Д</span><span class="sxs-lookup"><span data-stu-id="d9713-119">n/a</span></span> |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="d9713-120">Сводка: Новые возможности версии 4.9.0</span><span class="sxs-lookup"><span data-stu-id="d9713-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="d9713-121">Подписи. Включение ClientPolicies для настройки требования использовать набор доверенных авторов и репозиториев, перечисленных в NuGet.Config, — [#6961](https://github.com/NuGet/Home/issues/6961), [запись блога](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html).</span><span class="sxs-lookup"><span data-stu-id="d9713-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="d9713-122">Создание файлов с расширением .snupkg для включения символов в пакет и оптимизация отправки для принятия протоколом NuGet файлов .snupkg для сервера символов — [#6878](https://github.com/NuGet/Home/issues/6878), [запись блога](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html).</span><span class="sxs-lookup"><span data-stu-id="d9713-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="d9713-123">Подключаемый модуль учетных данных версии 2 для NuGet — [#6642](https://github.com/NuGet/Home/issues/6642).</span><span class="sxs-lookup"><span data-stu-id="d9713-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="d9713-124">Автономные пакеты NuGet — лицензия — [#4628](https://github.com/NuGet/Home/issues/4628), [объявление](https://github.com/NuGet/Announcements/issues/32).</span><span class="sxs-lookup"><span data-stu-id="d9713-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="d9713-125">Включение согласия для метаданных GeneratePathProperty в PackageReference для создания свойства MSBuild для каждого пакета в каталоге Foo.Bar\1.0\" — [#6949](https://github.com/NuGet/Home/issues/6949).</span><span class="sxs-lookup"><span data-stu-id="d9713-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="d9713-126">Улучшение опыта использования NuGet клиентами — [#7108](https://github.com/NuGet/Home/issues/7108).</span><span class="sxs-lookup"><span data-stu-id="d9713-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="d9713-127">Включение многократного восстановления пакетов с помощью файла блокировки — [#5602](https://github.com/NuGet/Home/issues/5602), [объявление](https://github.com/NuGet/Announcements/issues/28), [запись блога](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="d9713-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d9713-128">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="d9713-128">Issues fixed in this release</span></span>

* <span data-ttu-id="d9713-129">После предупреждений, преобразованных в ошибки (с помощью WarnAsErrors) и вызываемых PackageExtraction, не должен оставаться извлеченный пакет — [#7445](https://github.com/NuGet/Home/issues/7445).</span><span class="sxs-lookup"><span data-stu-id="d9713-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="d9713-130">Неправильно подписанные пакеты не должны попадать в папку установки глобальных пакетов — [#7423](https://github.com/NuGet/Home/issues/7423).</span><span class="sxs-lookup"><span data-stu-id="d9713-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="d9713-131">Привязка поколения перенаправления не должна пропускать фасадные сборки — [#7393](https://github.com/NuGet/Home/issues/7393).</span><span class="sxs-lookup"><span data-stu-id="d9713-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="d9713-132">VersionRange Equals не сравнивает плавающие диапазоны — [#7324](https://github.com/NuGet/Home/issues/7324).</span><span class="sxs-lookup"><span data-stu-id="d9713-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="d9713-133">Восстановление. Снижение производительности при использовании HTTP-стека .NET Core 2.1 — [#7314](https://github.com/NuGet/Home/issues/7314).</span><span class="sxs-lookup"><span data-stu-id="d9713-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="d9713-134">Обновление пакета не должно изменять PrivateAssets в PackageReference — [#7285](https://github.com/NuGet/Home/issues/7285).</span><span class="sxs-lookup"><span data-stu-id="d9713-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="d9713-135">Подписи. Подписывание не выполняется, если в пакете содержится слишком много записей пакета (> 65 534) — [#7248](https://github.com/NuGet/Home/issues/7248).</span><span class="sxs-lookup"><span data-stu-id="d9713-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="d9713-136">Путь к коду dotnet nuget push должен поддерживать новый поставщик учетных данных — [#7233](https://github.com/NuGet/Home/issues/7233).</span><span class="sxs-lookup"><span data-stu-id="d9713-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="d9713-137">Поддержка выполнения подключаемых модулей с помощью инвариантного языка и региональных параметров (как в Docker) — [#7223](https://github.com/NuGet/Home/issues/7223).</span><span class="sxs-lookup"><span data-stu-id="d9713-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="d9713-138">При добавлении источников NuGet не должны удаляться учетные данные из NuGet.config — [#7200](https://github.com/NuGet/Home/issues/7200).</span><span class="sxs-lookup"><span data-stu-id="d9713-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="d9713-139">Установка devDependency PackageReference по умолчанию должна происходить в excludeassets=compile — [#7084](https://github.com/NuGet/Home/issues/7084).</span><span class="sxs-lookup"><span data-stu-id="d9713-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="d9713-140">Отображение средства переноса для всех проектов и сообщения об ошибке при несовместимости проекта — [#6958](https://github.com/NuGet/Home/issues/6958).</span><span class="sxs-lookup"><span data-stu-id="d9713-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="d9713-141">Dotnet add package должен фиксировать восстановления, выполняемые для файла ресурсов — [#6928](https://github.com/NuGet/Home/issues/6928).</span><span class="sxs-lookup"><span data-stu-id="d9713-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="d9713-142">Подписи. Улучшены сообщения об ошибках, связанные с подписями, — [#6906](https://github.com/NuGet/Home/issues/6906).</span><span class="sxs-lookup"><span data-stu-id="d9713-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="d9713-143">[Сбой теста][zh-TW]. Строка Package Manager Console не локализована в консоли диспетчера пакетов — [#6381](https://github.com/NuGet/Home/issues/6381).</span><span class="sxs-lookup"><span data-stu-id="d9713-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="d9713-144">Сообщение об ошибке Unable to find project information (Не удалось найти сведения о проекте) должно быть более информативным в VS — [#5350](https://github.com/NuGet/Home/issues/5350).</span><span class="sxs-lookup"><span data-stu-id="d9713-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="d9713-145">Неинформативное сообщение об ошибке при неправильном использовании тега версии nuspec пакета NuGet — [#2714](https://github.com/NuGet/Home/issues/2714).</span><span class="sxs-lookup"><span data-stu-id="d9713-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="d9713-146">DCR — подписи. Поддержка протокола NuGet: ресурс RepositorySignatures/4.9.0 — [#7421](https://github.com/NuGet/Home/issues/7421).</span><span class="sxs-lookup"><span data-stu-id="d9713-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="d9713-147">DCR — во время извлечения пакета теперь будет создаваться файл метаданных .nupkg с хэш-кодом содержимого — [#7283](https://github.com/NuGet/Home/issues/7283).</span><span class="sxs-lookup"><span data-stu-id="d9713-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="d9713-148">DCR — пропуск проверки аутентичности кода подключаемых модулей при выполнении в Mono — [#7222](https://github.com/NuGet/Home/issues/7222).</span><span class="sxs-lookup"><span data-stu-id="d9713-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="d9713-149">Список всех проблем, исправленных в выпуске 4.9.0</span><span class="sxs-lookup"><span data-stu-id="d9713-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="d9713-150">Сводка: Новые возможности версии 4.9.1</span><span class="sxs-lookup"><span data-stu-id="d9713-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="d9713-151">Добавлена поддержка чтения записи в файл nuget.config с помощью новой команды trusted-signers — [#7480](https://github.com/NuGet/Home/issues/7480).</span><span class="sxs-lookup"><span data-stu-id="d9713-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d9713-152">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="d9713-152">Issues fixed in this release</span></span>

* <span data-ttu-id="d9713-153">Исправлена функция создания ссылок лицензии — [#7515](https://github.com/NuGet/Home/issues/7515).</span><span class="sxs-lookup"><span data-stu-id="d9713-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="d9713-154">Коды ошибок регрессии для проверки подписей — [#7492](https://github.com/NuGet/Home/issues/7492).</span><span class="sxs-lookup"><span data-stu-id="d9713-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="d9713-155">Пакет NuGet.Build.Tasks.Pack не включает сведения о лицензиях — [#7379](https://github.com/NuGet/Home/issues/7379).</span><span class="sxs-lookup"><span data-stu-id="d9713-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="d9713-156">Список всех проблем, исправленных в выпуске 4.9.1</span><span class="sxs-lookup"><span data-stu-id="d9713-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="d9713-157">Сводка: Новые возможности версии 4.9.2</span><span class="sxs-lookup"><span data-stu-id="d9713-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d9713-158">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="d9713-158">Issues fixed in this release</span></span>

* <span data-ttu-id="d9713-159">VS/dotnet.exe/nuget.exe/msbuild.exe (восстановление) не использует учетные данные, если имя источника содержит пробел, — [#7517](https://github.com/NuGet/Home/issues/7517).</span><span class="sxs-lookup"><span data-stu-id="d9713-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="d9713-160">Проблемы с доступом к LicenseAcceptanceWindow и LicenseFileWindow — [#7452](https://github.com/NuGet/Home/issues/7452).</span><span class="sxs-lookup"><span data-stu-id="d9713-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="d9713-161">Исправлено FormatException в DateTime.Parse из DateTimeConverter — [#7539](https://github.com/NuGet/Home/issues/7539).</span><span class="sxs-lookup"><span data-stu-id="d9713-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="d9713-162">Список всех проблем, исправленных в выпуске 4.9.2</span><span class="sxs-lookup"><span data-stu-id="d9713-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="d9713-163">Сводка: Новые возможности версии 4.9.3</span><span class="sxs-lookup"><span data-stu-id="d9713-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d9713-164">Исправленные ошибки в этом выпуске</span><span class="sxs-lookup"><span data-stu-id="d9713-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="d9713-165">Проблемы с многократным восстановлением пакетов с помощью файла блокировки</span><span class="sxs-lookup"><span data-stu-id="d9713-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="d9713-166">Режим блокировки не работает из-за неправильного вычисления хэша для кэшированных пакетов — [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="d9713-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="d9713-167">Восстановление разрешается для другой версии, отличной от указанной в файле `packages.lock.json` — [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="d9713-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="d9713-168">--locked-mode / RestoreLockedMode вызывает ложные ошибки восстановления при использовании ProjectReferences — [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="d9713-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="d9713-169">Сопоставитель пакетов SDK MSBuild пытается проверить агент работоспособности системы для пакета SDK, который не удалось восстановить с использованием файла packages.lock.json — [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="d9713-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="d9713-170">Проблемы с блокировкой зависимостей с помощью настраиваемых политик доверия</span><span class="sxs-lookup"><span data-stu-id="d9713-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="d9713-171">Инструмент dotnet.exe не должен проверять доверенную подписывающую сторону, так как подписанные пакеты не поддерживаются — [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="d9713-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="d9713-172">Порядок объектов trustedSigners в файле конфигурации влияет на проверку доверия — [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="d9713-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="d9713-173">Невозможно реализовать ISettings [из-за рефакторинга API-интерфейсов параметров для поддержки функции политики доверия] — [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="d9713-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="d9713-174">Проблемы, связанные с улучшением процесса отладки</span><span class="sxs-lookup"><span data-stu-id="d9713-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="d9713-175">Не удается опубликовать пакет символов для глобального средства .NET Core — [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="d9713-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="d9713-176">Проблемы с автономными пакетами NuGet — лицензия</span><span class="sxs-lookup"><span data-stu-id="d9713-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="d9713-177">Ошибка при создании пакета символов с расширением .snupkg при использовании встроенного файла лицензии — [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="d9713-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="d9713-178">Список всех проблем, исправленных в выпуске 4.9.3</span><span class="sxs-lookup"><span data-stu-id="d9713-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")
## <a name="known-issues"></a><span data-ttu-id="d9713-179">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="d9713-179">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="d9713-180">Выполнение команды dotnet nuget push с параметром --interactive выдает сообщение об ошибке на компьютере Mac.</span><span class="sxs-lookup"><span data-stu-id="d9713-180">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="d9713-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="d9713-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="d9713-182">Проблемы</span><span class="sxs-lookup"><span data-stu-id="d9713-182">Issue</span></span>
<span data-ttu-id="d9713-183">Аргумент `--interactive` не перенаправляется интерфейсом командной строки dotnet, что приводит к ошибке `error: Missing value for option 'interactive'`.</span><span class="sxs-lookup"><span data-stu-id="d9713-183">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="d9713-184">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="d9713-184">Workaround</span></span>
<span data-ttu-id="d9713-185">Выполните любую другую команду dotnet с параметром interactive, например `dotnet restore --interactive`, и пройдите проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="d9713-185">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="d9713-186">Результат проверки подлинности затем может быть кэширован поставщиком учетных данных.</span><span class="sxs-lookup"><span data-stu-id="d9713-186">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="d9713-187">Затем выполните `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="d9713-187">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="d9713-188">Пакеты в FallbackFolders, устанавливаемые пакетом SDK для .NET Core, являются пользовательской установкой и не проходят проверку подписи.</span><span class="sxs-lookup"><span data-stu-id="d9713-188">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="d9713-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="d9713-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="d9713-190">Проблемы</span><span class="sxs-lookup"><span data-stu-id="d9713-190">Issue</span></span>
<span data-ttu-id="d9713-191">При использовании dotnet.exe 2.x для восстановления проекта с несколькими целевыми объектами (netcoreapp 1.x и netcoreapp 2.x) резервная папка обрабатывается как веб-канал файла.</span><span class="sxs-lookup"><span data-stu-id="d9713-191">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="d9713-192">Это значит, что при восстановлении NuGet пытается установить пакет из резервной папки в папку глобальных пакетов и выполнить обычную проверки подписи, что приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="d9713-192">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="d9713-193">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="d9713-193">Workaround</span></span>
<span data-ttu-id="d9713-194">Отключите использование резервной папки, очистив значение для `RestoreAdditionalProjectSources`.</span><span class="sxs-lookup"><span data-stu-id="d9713-194">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="d9713-195">`<RestoreAdditionalProjectSources/>` Соблюдайте при этом осторожность, так как это приведет к скачиванию большого количества пакетов с NuGet.org, которые иначе были бы восстановлены из резервной папки.</span><span class="sxs-lookup"><span data-stu-id="d9713-195">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
