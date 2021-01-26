---
title: Команда спецификации интерфейса командной строки NuGet
description: Справочник по команде nuget.exe Spec
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b7780ee5d2e722da5e1623f44709059dd9aa3d45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779145"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="0687e-103">Команда spec (интерфейс командной строки NuGet)</span><span class="sxs-lookup"><span data-stu-id="0687e-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="0687e-104">Область **применения:** &bullet; **Поддерживаемые версии** для создания пакетов: все</span><span class="sxs-lookup"><span data-stu-id="0687e-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0687e-105">Создает `.nuspec` файл для нового пакета.</span><span class="sxs-lookup"><span data-stu-id="0687e-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="0687e-106">При запуске в той же папке, что и файл проекта ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` создает файл с маркерами `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="0687e-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="0687e-107">Дополнительные сведения см. [в разделе Создание пакета](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="0687e-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="0687e-108">Использование</span><span class="sxs-lookup"><span data-stu-id="0687e-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="0687e-109">где `<packageID>` — это необязательный идентификатор пакета для сохранения в `.nuspec` файле.</span><span class="sxs-lookup"><span data-stu-id="0687e-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="0687e-110">Варианты</span><span class="sxs-lookup"><span data-stu-id="0687e-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="0687e-111">Указывает путь к сборке, используемой для метаданных.</span><span class="sxs-lookup"><span data-stu-id="0687e-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="0687e-112">Перезаписывает существующий `.nuspec` файл.</span><span class="sxs-lookup"><span data-stu-id="0687e-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="0687e-113">*(3.5 +)* Принудительное выполнение nuget.exe с использованием инвариантного языка и региональных параметров, основанных на английском языке.</span><span class="sxs-lookup"><span data-stu-id="0687e-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="0687e-114">Отображает справочные сведения для команды.</span><span class="sxs-lookup"><span data-stu-id="0687e-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="0687e-115">Подавляет запросы на ввод или подтверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="0687e-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="0687e-116">Задает объем сведений, отображаемых в выходных данных: `normal` (по умолчанию), `quiet` или `detailed` .</span><span class="sxs-lookup"><span data-stu-id="0687e-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="0687e-117">См. также [переменные среды](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0687e-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0687e-118">Примеры</span><span class="sxs-lookup"><span data-stu-id="0687e-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
