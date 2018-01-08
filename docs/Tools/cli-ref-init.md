---
title: "NuGet CLI init 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Nuget.exe init 命令參考"
keywords: "nuget init 參考，初始化命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="3afa1-104">初始化命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3afa1-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="3afa1-105">**適用於：**封裝建立&bullet;**支援的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="3afa1-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="3afa1-106">將所有封裝從一般資料夾都複製到目的資料夾，如所述，使用以階層配置[將命令加入](#add)上方。</span><span class="sxs-lookup"><span data-stu-id="3afa1-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](#add) above.</span></span> <span data-ttu-id="3afa1-107">也就使用`init`相當於使用`add`命令上的資料夾中的每個封裝。</span><span class="sxs-lookup"><span data-stu-id="3afa1-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="3afa1-108">如同`add`，目的地必須是本機資料夾或 UNC 路徑。不支援 HTTP 封裝儲存機制，例如 nuget.org 或私用的伺服器。</span><span class="sxs-lookup"><span data-stu-id="3afa1-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="3afa1-109">使用方式</span><span class="sxs-lookup"><span data-stu-id="3afa1-109">Usage</span></span>

```
nuget init <source> <destination> [options]
```

<span data-ttu-id="3afa1-110">其中`<source>`是包含封裝的資料夾和`<destination>`是本機資料夾或封裝複製到其中的 UNC 路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="3afa1-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages will be copied.</span></span>

## <a name="options"></a><span data-ttu-id="3afa1-111">選項</span><span class="sxs-lookup"><span data-stu-id="3afa1-111">Options</span></span>

| <span data-ttu-id="3afa1-112">選項</span><span class="sxs-lookup"><span data-stu-id="3afa1-112">Option</span></span> | <span data-ttu-id="3afa1-113">說明</span><span class="sxs-lookup"><span data-stu-id="3afa1-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3afa1-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3afa1-114">ConfigFile</span></span> | <span data-ttu-id="3afa1-115">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="3afa1-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3afa1-116">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="3afa1-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="3afa1-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3afa1-117">ForceEnglishOutput</span></span> | <span data-ttu-id="3afa1-118">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="3afa1-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3afa1-119">Expand</span><span class="sxs-lookup"><span data-stu-id="3afa1-119">Expand</span></span> | <span data-ttu-id="3afa1-120">將所有檔案新增至套件來源; 每個封裝中與相同`-Expand`與`add`命令。</span><span class="sxs-lookup"><span data-stu-id="3afa1-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="3afa1-121">說明</span><span class="sxs-lookup"><span data-stu-id="3afa1-121">Help</span></span> | <span data-ttu-id="3afa1-122">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="3afa1-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="3afa1-123">非互動式</span><span class="sxs-lookup"><span data-stu-id="3afa1-123">NonInteractive</span></span> | <span data-ttu-id="3afa1-124">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="3afa1-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3afa1-125">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="3afa1-125">Verbosity</span></span> | <span data-ttu-id="3afa1-126">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="3afa1-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="3afa1-127">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3afa1-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3afa1-128">範例</span><span class="sxs-lookup"><span data-stu-id="3afa1-128">Examples</span></span>

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```