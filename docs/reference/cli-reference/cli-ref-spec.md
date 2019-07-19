---
title: NuGet CLI 規格命令
description: Nuget.exe 規格命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327565"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="c28dd-103">spec 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c28dd-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="c28dd-104">**適用于:** 套件建立&bullet; **支援的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="c28dd-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c28dd-105">`.nuspec`為新封裝產生檔案。</span><span class="sxs-lookup"><span data-stu-id="c28dd-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="c28dd-106">如果在與專案檔相同的資料夾中執行 (`.csproj`、 `.vbproj`、 `.fsproj`), `spec`則會建立`.nuspec`已標記化的檔案。</span><span class="sxs-lookup"><span data-stu-id="c28dd-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="c28dd-107">如需其他資訊, 請參閱[建立封裝](../../create-packages/creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="c28dd-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c28dd-108">使用量</span><span class="sxs-lookup"><span data-stu-id="c28dd-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="c28dd-109">其中`<packageID>`是要儲存`.nuspec`在檔案中的選擇性套件識別碼。</span><span class="sxs-lookup"><span data-stu-id="c28dd-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="c28dd-110">選項</span><span class="sxs-lookup"><span data-stu-id="c28dd-110">Options</span></span>

| <span data-ttu-id="c28dd-111">選項</span><span class="sxs-lookup"><span data-stu-id="c28dd-111">Option</span></span> | <span data-ttu-id="c28dd-112">說明</span><span class="sxs-lookup"><span data-stu-id="c28dd-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c28dd-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="c28dd-113">AssemblyPath</span></span> | <span data-ttu-id="c28dd-114">指定要用於中繼資料之元件的路徑。</span><span class="sxs-lookup"><span data-stu-id="c28dd-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="c28dd-115">使</span><span class="sxs-lookup"><span data-stu-id="c28dd-115">Force</span></span> | <span data-ttu-id="c28dd-116">覆寫任何`.nuspec`現有的檔案。</span><span class="sxs-lookup"><span data-stu-id="c28dd-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="c28dd-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c28dd-117">ForceEnglishOutput</span></span> | <span data-ttu-id="c28dd-118">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="c28dd-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c28dd-119">Help</span><span class="sxs-lookup"><span data-stu-id="c28dd-119">Help</span></span> | <span data-ttu-id="c28dd-120">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="c28dd-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="c28dd-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c28dd-121">NonInteractive</span></span> | <span data-ttu-id="c28dd-122">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="c28dd-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c28dd-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="c28dd-123">Verbosity</span></span> | <span data-ttu-id="c28dd-124">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="c28dd-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c28dd-125">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c28dd-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c28dd-126">範例</span><span class="sxs-lookup"><span data-stu-id="c28dd-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
