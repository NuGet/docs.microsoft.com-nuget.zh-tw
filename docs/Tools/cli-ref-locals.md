---
title: "NuGet CLI 區域變數命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 區域變數命令參考"
keywords: "nuget 區域變數的參考，[區域變數] 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="c67df-104">[區域變數] 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c67df-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="c67df-105">**適用於：**封裝耗用量&bullet;**支援的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="c67df-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="c67df-106">清除或列出本機 NuGet 資源，例如 http 要求的快取、 封裝快取，而 [全機器全域 packages] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c67df-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="c67df-107">`locals`命令也可用來顯示這些位置的清單。</span><span class="sxs-lookup"><span data-stu-id="c67df-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="c67df-108">如需詳細資訊，請參閱[管理 NuGet 快取](../consume-packages/managing-the-nuget-cache.md)。</span><span class="sxs-lookup"><span data-stu-id="c67df-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c67df-109">使用量</span><span class="sxs-lookup"><span data-stu-id="c67df-109">Usage</span></span>

```cli
nuget locals <cache> [options]
```

<span data-ttu-id="c67df-110">其中`<cache>`是其中一個`all`， `http-cache`， `packages-cache`， `global-packages`，和`temp` *（3.4 +）*。</span><span class="sxs-lookup"><span data-stu-id="c67df-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="c67df-111">選項</span><span class="sxs-lookup"><span data-stu-id="c67df-111">Options</span></span>

| <span data-ttu-id="c67df-112">選項</span><span class="sxs-lookup"><span data-stu-id="c67df-112">Option</span></span> | <span data-ttu-id="c67df-113">描述</span><span class="sxs-lookup"><span data-stu-id="c67df-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c67df-114">清除</span><span class="sxs-lookup"><span data-stu-id="c67df-114">Clear</span></span> | <span data-ttu-id="c67df-115">清除指定的快取。</span><span class="sxs-lookup"><span data-stu-id="c67df-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="c67df-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c67df-116">ConfigFile</span></span> | <span data-ttu-id="c67df-117">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="c67df-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c67df-118">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="c67df-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="c67df-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c67df-119">ForceEnglishOutput</span></span> | <span data-ttu-id="c67df-120">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="c67df-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c67df-121">說明</span><span class="sxs-lookup"><span data-stu-id="c67df-121">Help</span></span> | <span data-ttu-id="c67df-122">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="c67df-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="c67df-123">清單</span><span class="sxs-lookup"><span data-stu-id="c67df-123">List</span></span> | <span data-ttu-id="c67df-124">列出指定的快取的位置或搭配使用時，所有快取位置*所有*。</span><span class="sxs-lookup"><span data-stu-id="c67df-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="c67df-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c67df-125">NonInteractive</span></span> | <span data-ttu-id="c67df-126">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="c67df-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c67df-127">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="c67df-127">Verbosity</span></span> | <span data-ttu-id="c67df-128">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="c67df-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c67df-129">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c67df-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c67df-130">範例</span><span class="sxs-lookup"><span data-stu-id="c67df-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```
