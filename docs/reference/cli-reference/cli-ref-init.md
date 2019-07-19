---
title: NuGet CLI init 命令
description: Nuget.exe init 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327775"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="cb4a0-103">init 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cb4a0-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="cb4a0-104">**適用于:** 套件建立&bullet; **支援的版本:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="cb4a0-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="cb4a0-105">使用階層式配置, 將所有封裝從一般資料夾複製到目的地資料夾, 如[add 命令](cli-ref-add.md)所述。</span><span class="sxs-lookup"><span data-stu-id="cb4a0-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="cb4a0-106">也就是說, 使用`init`相當於在資料夾中的`add`每個封裝上使用命令。</span><span class="sxs-lookup"><span data-stu-id="cb4a0-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="cb4a0-107">`add`如同, 目的地必須是本機資料夾或 UNC 路徑;不支援 HTTP 封裝存放庫 (例如 nuget.org 或私用伺服器)。</span><span class="sxs-lookup"><span data-stu-id="cb4a0-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="cb4a0-108">使用量</span><span class="sxs-lookup"><span data-stu-id="cb4a0-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="cb4a0-109">其中`<source>`是包含封裝的資料夾, `<destination>`而是要將封裝複製到其中的本機資料夾或 UNC 路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="cb4a0-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="cb4a0-110">選項</span><span class="sxs-lookup"><span data-stu-id="cb4a0-110">Options</span></span>

| <span data-ttu-id="cb4a0-111">選項</span><span class="sxs-lookup"><span data-stu-id="cb4a0-111">Option</span></span> | <span data-ttu-id="cb4a0-112">說明</span><span class="sxs-lookup"><span data-stu-id="cb4a0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb4a0-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cb4a0-113">ConfigFile</span></span> | <span data-ttu-id="cb4a0-114">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="cb4a0-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cb4a0-115">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="cb4a0-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cb4a0-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cb4a0-116">ForceEnglishOutput</span></span> | <span data-ttu-id="cb4a0-117">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="cb4a0-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cb4a0-118">Expand</span><span class="sxs-lookup"><span data-stu-id="cb4a0-118">Expand</span></span> | <span data-ttu-id="cb4a0-119">新增每個封裝中新增至封裝來源的所有檔案;`-Expand` 與`add`命令相同。</span><span class="sxs-lookup"><span data-stu-id="cb4a0-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="cb4a0-120">Help</span><span class="sxs-lookup"><span data-stu-id="cb4a0-120">Help</span></span> | <span data-ttu-id="cb4a0-121">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="cb4a0-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="cb4a0-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="cb4a0-122">NonInteractive</span></span> | <span data-ttu-id="cb4a0-123">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="cb4a0-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cb4a0-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="cb4a0-124">Verbosity</span></span> | <span data-ttu-id="cb4a0-125">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="cb4a0-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cb4a0-126">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cb4a0-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cb4a0-127">範例</span><span class="sxs-lookup"><span data-stu-id="cb4a0-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
