---
title: NuGet CLI init 命令
description: Nuget.exe init 命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551406"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="f1deb-103">init 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f1deb-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="f1deb-104">**適用於：** 封裝建立&bullet;**支援的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="f1deb-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="f1deb-105">所有的封裝複製到如所述，使用以階層配置的目的地資料夾的一般資料夾[將命令加入](cli-ref-add.md)。</span><span class="sxs-lookup"><span data-stu-id="f1deb-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="f1deb-106">也就使用`init`相當於使用`add`命令的資料夾中的每個套件。</span><span class="sxs-lookup"><span data-stu-id="f1deb-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="f1deb-107">如同`add`，目的地必須是本機資料夾或 UNC 路徑;不支援 HTTP 套件存放庫，例如 nuget.org 或私用的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f1deb-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="f1deb-108">使用量</span><span class="sxs-lookup"><span data-stu-id="f1deb-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="f1deb-109">何處`<source>`是包含封裝的資料夾和`<destination>`是本機資料夾或封裝複製到其中的 UNC 路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="f1deb-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="f1deb-110">選項</span><span class="sxs-lookup"><span data-stu-id="f1deb-110">Options</span></span>

| <span data-ttu-id="f1deb-111">選項</span><span class="sxs-lookup"><span data-stu-id="f1deb-111">Option</span></span> | <span data-ttu-id="f1deb-112">描述</span><span class="sxs-lookup"><span data-stu-id="f1deb-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1deb-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f1deb-113">ConfigFile</span></span> | <span data-ttu-id="f1deb-114">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="f1deb-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f1deb-115">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="f1deb-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f1deb-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f1deb-116">ForceEnglishOutput</span></span> | <span data-ttu-id="f1deb-117">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="f1deb-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f1deb-118">Expand</span><span class="sxs-lookup"><span data-stu-id="f1deb-118">Expand</span></span> | <span data-ttu-id="f1deb-119">將所有檔案新增至套件來源; 每個封裝中與相同`-Expand`與`add`命令。</span><span class="sxs-lookup"><span data-stu-id="f1deb-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="f1deb-120">說明</span><span class="sxs-lookup"><span data-stu-id="f1deb-120">Help</span></span> | <span data-ttu-id="f1deb-121">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="f1deb-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="f1deb-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f1deb-122">NonInteractive</span></span> | <span data-ttu-id="f1deb-123">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="f1deb-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f1deb-124">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="f1deb-124">Verbosity</span></span> | <span data-ttu-id="f1deb-125">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="f1deb-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f1deb-126">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f1deb-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f1deb-127">範例</span><span class="sxs-lookup"><span data-stu-id="f1deb-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
