---
title: NuGet CLI 規格命令
description: Nuget.exe 規格命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546445"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="c266a-103">規格的命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c266a-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="c266a-104">**適用於：** 封裝建立&bullet;**支援的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="c266a-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c266a-105">會產生`.nuspec`新封裝的檔案。</span><span class="sxs-lookup"><span data-stu-id="c266a-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="c266a-106">如果在專案檔相同的資料夾中執行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`建立語彙基元化`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="c266a-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="c266a-107">如需詳細資訊，請參閱[建立套件](../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="c266a-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c266a-108">使用量</span><span class="sxs-lookup"><span data-stu-id="c266a-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="c266a-109">何處`<packageID>`是選擇性的套件識別碼儲存在`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="c266a-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="c266a-110">選項</span><span class="sxs-lookup"><span data-stu-id="c266a-110">Options</span></span>

| <span data-ttu-id="c266a-111">選項</span><span class="sxs-lookup"><span data-stu-id="c266a-111">Option</span></span> | <span data-ttu-id="c266a-112">描述</span><span class="sxs-lookup"><span data-stu-id="c266a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c266a-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="c266a-113">AssemblyPath</span></span> | <span data-ttu-id="c266a-114">指定要用於中繼資料的組件的路徑。</span><span class="sxs-lookup"><span data-stu-id="c266a-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="c266a-115">強制</span><span class="sxs-lookup"><span data-stu-id="c266a-115">Force</span></span> | <span data-ttu-id="c266a-116">覆寫任何現有`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="c266a-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="c266a-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c266a-117">ForceEnglishOutput</span></span> | <span data-ttu-id="c266a-118">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="c266a-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c266a-119">說明</span><span class="sxs-lookup"><span data-stu-id="c266a-119">Help</span></span> | <span data-ttu-id="c266a-120">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="c266a-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="c266a-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c266a-121">NonInteractive</span></span> | <span data-ttu-id="c266a-122">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="c266a-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c266a-123">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="c266a-123">Verbosity</span></span> | <span data-ttu-id="c266a-124">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="c266a-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c266a-125">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c266a-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c266a-126">範例</span><span class="sxs-lookup"><span data-stu-id="c266a-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
