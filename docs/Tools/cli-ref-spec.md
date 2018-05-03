---
title: NuGet CLI 規格命令
description: Nuget.exe 規格命令參考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68d661030ce7bcff7d7a3a1c96c07e149ad4ffea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="32df3-103">規格命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="32df3-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="32df3-104">**適用於：**封裝建立&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="32df3-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="32df3-105">會產生`.nuspec`新套件的檔案。</span><span class="sxs-lookup"><span data-stu-id="32df3-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="32df3-106">如果在專案檔相同資料夾中執行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`建立語彙基元化`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="32df3-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="32df3-107">如需詳細資訊，請參閱[建立封裝](../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="32df3-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="32df3-108">使用量</span><span class="sxs-lookup"><span data-stu-id="32df3-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="32df3-109">其中`<packageID>`是選擇性的封裝識別碼儲存在`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="32df3-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="32df3-110">選項</span><span class="sxs-lookup"><span data-stu-id="32df3-110">Options</span></span>

| <span data-ttu-id="32df3-111">選項</span><span class="sxs-lookup"><span data-stu-id="32df3-111">Option</span></span> | <span data-ttu-id="32df3-112">描述</span><span class="sxs-lookup"><span data-stu-id="32df3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="32df3-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="32df3-113">AssemblyPath</span></span> | <span data-ttu-id="32df3-114">指定要用於中繼資料組件的路徑。</span><span class="sxs-lookup"><span data-stu-id="32df3-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="32df3-115">強制</span><span class="sxs-lookup"><span data-stu-id="32df3-115">Force</span></span> | <span data-ttu-id="32df3-116">覆寫任何現有`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="32df3-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="32df3-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="32df3-117">ForceEnglishOutput</span></span> | <span data-ttu-id="32df3-118">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="32df3-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="32df3-119">說明</span><span class="sxs-lookup"><span data-stu-id="32df3-119">Help</span></span> | <span data-ttu-id="32df3-120">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="32df3-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="32df3-121">非互動式</span><span class="sxs-lookup"><span data-stu-id="32df3-121">NonInteractive</span></span> | <span data-ttu-id="32df3-122">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="32df3-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="32df3-123">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="32df3-123">Verbosity</span></span> | <span data-ttu-id="32df3-124">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="32df3-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="32df3-125">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="32df3-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="32df3-126">範例</span><span class="sxs-lookup"><span data-stu-id="32df3-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
