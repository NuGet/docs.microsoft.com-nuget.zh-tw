---
title: "NuGet CLI 規格命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 規格命令參考"
keywords: "nuget 規格的參考，規格命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="4d9f9-104">規格命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4d9f9-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="4d9f9-105">**適用於：**封裝建立&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="4d9f9-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="4d9f9-106">會產生`.nuspec`新套件的檔案。</span><span class="sxs-lookup"><span data-stu-id="4d9f9-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="4d9f9-107">如果在專案檔相同資料夾中執行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`建立語彙基元化`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="4d9f9-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="4d9f9-108">如需詳細資訊，請參閱[建立封裝](../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="4d9f9-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="4d9f9-109">使用量</span><span class="sxs-lookup"><span data-stu-id="4d9f9-109">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="4d9f9-110">其中`<packageID>`是選擇性的封裝識別碼儲存在`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="4d9f9-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="4d9f9-111">選項</span><span class="sxs-lookup"><span data-stu-id="4d9f9-111">Options</span></span>

| <span data-ttu-id="4d9f9-112">選項</span><span class="sxs-lookup"><span data-stu-id="4d9f9-112">Option</span></span> | <span data-ttu-id="4d9f9-113">描述</span><span class="sxs-lookup"><span data-stu-id="4d9f9-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4d9f9-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="4d9f9-114">AssemblyPath</span></span> | <span data-ttu-id="4d9f9-115">指定要用於中繼資料組件的路徑。</span><span class="sxs-lookup"><span data-stu-id="4d9f9-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="4d9f9-116">強制</span><span class="sxs-lookup"><span data-stu-id="4d9f9-116">Force</span></span> | <span data-ttu-id="4d9f9-117">覆寫任何現有`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="4d9f9-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="4d9f9-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4d9f9-118">ForceEnglishOutput</span></span> | <span data-ttu-id="4d9f9-119">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="4d9f9-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4d9f9-120">說明</span><span class="sxs-lookup"><span data-stu-id="4d9f9-120">Help</span></span> | <span data-ttu-id="4d9f9-121">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="4d9f9-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="4d9f9-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4d9f9-122">NonInteractive</span></span> | <span data-ttu-id="4d9f9-123">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="4d9f9-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4d9f9-124">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="4d9f9-124">Verbosity</span></span> | <span data-ttu-id="4d9f9-125">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="4d9f9-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4d9f9-126">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4d9f9-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4d9f9-127">範例</span><span class="sxs-lookup"><span data-stu-id="4d9f9-127">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
