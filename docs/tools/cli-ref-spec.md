---
title: NuGet CLI 規格命令
description: Nuget.exe 規格命令參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817082"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="d6090-103">規格命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d6090-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="d6090-104">**適用於：** 封裝建立&bullet;**支援的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="d6090-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d6090-105">會產生`.nuspec`新套件的檔案。</span><span class="sxs-lookup"><span data-stu-id="d6090-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="d6090-106">如果在專案檔相同資料夾中執行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`建立語彙基元化`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="d6090-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="d6090-107">如需詳細資訊，請參閱[建立封裝](../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="d6090-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d6090-108">使用量</span><span class="sxs-lookup"><span data-stu-id="d6090-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="d6090-109">其中`<packageID>`是選擇性的封裝識別碼儲存在`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="d6090-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="d6090-110">選項</span><span class="sxs-lookup"><span data-stu-id="d6090-110">Options</span></span>

| <span data-ttu-id="d6090-111">選項</span><span class="sxs-lookup"><span data-stu-id="d6090-111">Option</span></span> | <span data-ttu-id="d6090-112">描述</span><span class="sxs-lookup"><span data-stu-id="d6090-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d6090-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="d6090-113">AssemblyPath</span></span> | <span data-ttu-id="d6090-114">指定要用於中繼資料組件的路徑。</span><span class="sxs-lookup"><span data-stu-id="d6090-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="d6090-115">強制</span><span class="sxs-lookup"><span data-stu-id="d6090-115">Force</span></span> | <span data-ttu-id="d6090-116">覆寫任何現有`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="d6090-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="d6090-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d6090-117">ForceEnglishOutput</span></span> | <span data-ttu-id="d6090-118">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="d6090-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d6090-119">說明</span><span class="sxs-lookup"><span data-stu-id="d6090-119">Help</span></span> | <span data-ttu-id="d6090-120">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="d6090-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="d6090-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d6090-121">NonInteractive</span></span> | <span data-ttu-id="d6090-122">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="d6090-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d6090-123">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="d6090-123">Verbosity</span></span> | <span data-ttu-id="d6090-124">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="d6090-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d6090-125">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d6090-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d6090-126">範例</span><span class="sxs-lookup"><span data-stu-id="d6090-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
