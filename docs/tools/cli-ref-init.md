---
title: NuGet CLI init 命令
description: Nuget.exe init 命令參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4fda33aabd51fbbf0e5559baaa42af065366ba4
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817814"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="060d7-103">初始化命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="060d7-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="060d7-104">**適用於：** 封裝建立&bullet;**支援的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="060d7-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="060d7-105">將所有封裝從一般資料夾都複製到目的資料夾，如所述，使用以階層配置[將命令加入](cli-ref-add.md)。</span><span class="sxs-lookup"><span data-stu-id="060d7-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="060d7-106">也就使用`init`相當於使用`add`命令上的資料夾中的每個封裝。</span><span class="sxs-lookup"><span data-stu-id="060d7-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="060d7-107">如同`add`，目的地必須是本機資料夾或 UNC 路徑。不支援 HTTP 封裝儲存機制，例如 nuget.org 或私用的伺服器。</span><span class="sxs-lookup"><span data-stu-id="060d7-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="060d7-108">使用量</span><span class="sxs-lookup"><span data-stu-id="060d7-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="060d7-109">其中`<source>`是包含封裝的資料夾和`<destination>`是本機資料夾或封裝複製到其中的 UNC 路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="060d7-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="060d7-110">選項</span><span class="sxs-lookup"><span data-stu-id="060d7-110">Options</span></span>

| <span data-ttu-id="060d7-111">選項</span><span class="sxs-lookup"><span data-stu-id="060d7-111">Option</span></span> | <span data-ttu-id="060d7-112">描述</span><span class="sxs-lookup"><span data-stu-id="060d7-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="060d7-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="060d7-113">ConfigFile</span></span> | <span data-ttu-id="060d7-114">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="060d7-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="060d7-115">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="060d7-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="060d7-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="060d7-116">ForceEnglishOutput</span></span> | <span data-ttu-id="060d7-117">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="060d7-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="060d7-118">Expand</span><span class="sxs-lookup"><span data-stu-id="060d7-118">Expand</span></span> | <span data-ttu-id="060d7-119">將所有檔案新增至套件來源; 每個封裝中與相同`-Expand`與`add`命令。</span><span class="sxs-lookup"><span data-stu-id="060d7-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="060d7-120">說明</span><span class="sxs-lookup"><span data-stu-id="060d7-120">Help</span></span> | <span data-ttu-id="060d7-121">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="060d7-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="060d7-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="060d7-122">NonInteractive</span></span> | <span data-ttu-id="060d7-123">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="060d7-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="060d7-124">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="060d7-124">Verbosity</span></span> | <span data-ttu-id="060d7-125">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="060d7-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="060d7-126">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="060d7-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="060d7-127">範例</span><span class="sxs-lookup"><span data-stu-id="060d7-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
