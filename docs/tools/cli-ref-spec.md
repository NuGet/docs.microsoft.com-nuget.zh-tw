---
title: NuGet CLI 規格命令
description: Nuget.exe 規格命令參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794147"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="25887-103">規格的命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="25887-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="25887-104">**適用於：** 封裝建立&bullet;**支援的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="25887-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="25887-105">會產生`.nuspec`新封裝的檔案。</span><span class="sxs-lookup"><span data-stu-id="25887-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="25887-106">如果在專案檔相同的資料夾中執行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`建立語彙基元化`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="25887-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="25887-107">如需詳細資訊，請參閱[建立套件](../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="25887-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="25887-108">使用量</span><span class="sxs-lookup"><span data-stu-id="25887-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="25887-109">何處`<packageID>`是選擇性的套件識別碼儲存在`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="25887-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="25887-110">選項</span><span class="sxs-lookup"><span data-stu-id="25887-110">Options</span></span>

| <span data-ttu-id="25887-111">選項</span><span class="sxs-lookup"><span data-stu-id="25887-111">Option</span></span> | <span data-ttu-id="25887-112">描述</span><span class="sxs-lookup"><span data-stu-id="25887-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="25887-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="25887-113">AssemblyPath</span></span> | <span data-ttu-id="25887-114">指定要用於中繼資料的組件的路徑。</span><span class="sxs-lookup"><span data-stu-id="25887-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="25887-115">強制</span><span class="sxs-lookup"><span data-stu-id="25887-115">Force</span></span> | <span data-ttu-id="25887-116">覆寫任何現有`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="25887-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="25887-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="25887-117">ForceEnglishOutput</span></span> | <span data-ttu-id="25887-118">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="25887-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="25887-119">說明</span><span class="sxs-lookup"><span data-stu-id="25887-119">Help</span></span> | <span data-ttu-id="25887-120">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="25887-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="25887-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="25887-121">NonInteractive</span></span> | <span data-ttu-id="25887-122">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="25887-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="25887-123">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="25887-123">Verbosity</span></span> | <span data-ttu-id="25887-124">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="25887-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="25887-125">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="25887-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="25887-126">範例</span><span class="sxs-lookup"><span data-stu-id="25887-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
