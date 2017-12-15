---
title: "NuGet CLI 規格命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Nuget.exe 規格命令參考"
keywords: "nuget 規格的參考，規格命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="69116-104">規格命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="69116-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="69116-105">**適用於：**封裝建立&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="69116-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="69116-106">會產生`.nuspec`新套件的檔案。</span><span class="sxs-lookup"><span data-stu-id="69116-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="69116-107">如果在專案檔相同資料夾中執行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`建立語彙基元化`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="69116-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="69116-108">如需詳細資訊，請參閱[建立封裝](../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="69116-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="69116-109">使用方式</span><span class="sxs-lookup"><span data-stu-id="69116-109">Usage</span></span>

```
nuget spec [<packageID>] [options]
```

<span data-ttu-id="69116-110">其中`<packageID>`是選擇性的封裝識別碼儲存在`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="69116-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="69116-111">選項</span><span class="sxs-lookup"><span data-stu-id="69116-111">Options</span></span>

| <span data-ttu-id="69116-112">選項</span><span class="sxs-lookup"><span data-stu-id="69116-112">Option</span></span> | <span data-ttu-id="69116-113">說明</span><span class="sxs-lookup"><span data-stu-id="69116-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69116-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="69116-114">AssemblyPath</span></span> | <span data-ttu-id="69116-115">指定要用於中繼資料組件的路徑。</span><span class="sxs-lookup"><span data-stu-id="69116-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="69116-116">強制</span><span class="sxs-lookup"><span data-stu-id="69116-116">Force</span></span> | <span data-ttu-id="69116-117">覆寫任何現有`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="69116-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="69116-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="69116-118">ForceEnglishOutput</span></span> | <span data-ttu-id="69116-119">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="69116-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="69116-120">說明</span><span class="sxs-lookup"><span data-stu-id="69116-120">Help</span></span> | <span data-ttu-id="69116-121">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="69116-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="69116-122">非互動式</span><span class="sxs-lookup"><span data-stu-id="69116-122">NonInteractive</span></span> | <span data-ttu-id="69116-123">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="69116-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="69116-124">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="69116-124">Verbosity</span></span> | <span data-ttu-id="69116-125">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="69116-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="69116-126">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="69116-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="69116-127">範例</span><span class="sxs-lookup"><span data-stu-id="69116-127">Examples</span></span>

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
