---
title: NuGet CLI 區域變數命令 |Microsoft 文件
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 區域變數命令參考
keywords: nuget 區域變數的參考，[區域變數] 命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="c43b4-104">[區域變數] 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c43b4-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="c43b4-105">**適用於：**封裝耗用量&bullet;**支援的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="c43b4-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="c43b4-106">清除或列出本機 NuGet 資源，例如*http 快取*，*全域封裝*資料夾以及暫存資料夾。</span><span class="sxs-lookup"><span data-stu-id="c43b4-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="c43b4-107">`locals`命令也可用來顯示這些位置的清單。</span><span class="sxs-lookup"><span data-stu-id="c43b4-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="c43b4-108">如需詳細資訊，請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="c43b4-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c43b4-109">使用量</span><span class="sxs-lookup"><span data-stu-id="c43b4-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="c43b4-110">其中`<folder>`是其中一個`all`， `http-cache`， `packages-cache` *（3.5 及更早版本）*， `global-packages`，和`temp` *（3.4 +）*。</span><span class="sxs-lookup"><span data-stu-id="c43b4-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="c43b4-111">選項</span><span class="sxs-lookup"><span data-stu-id="c43b4-111">Options</span></span>

| <span data-ttu-id="c43b4-112">選項</span><span class="sxs-lookup"><span data-stu-id="c43b4-112">Option</span></span> | <span data-ttu-id="c43b4-113">描述</span><span class="sxs-lookup"><span data-stu-id="c43b4-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c43b4-114">清除</span><span class="sxs-lookup"><span data-stu-id="c43b4-114">Clear</span></span> | <span data-ttu-id="c43b4-115">清除指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c43b4-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="c43b4-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c43b4-116">ConfigFile</span></span> | <span data-ttu-id="c43b4-117">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="c43b4-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c43b4-118">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="c43b4-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c43b4-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c43b4-119">ForceEnglishOutput</span></span> | <span data-ttu-id="c43b4-120">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="c43b4-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c43b4-121">說明</span><span class="sxs-lookup"><span data-stu-id="c43b4-121">Help</span></span> | <span data-ttu-id="c43b4-122">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="c43b4-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="c43b4-123">清單</span><span class="sxs-lookup"><span data-stu-id="c43b4-123">List</span></span> | <span data-ttu-id="c43b4-124">列出指定的資料夾位置或搭配使用時的所有資料夾的位置*所有*。</span><span class="sxs-lookup"><span data-stu-id="c43b4-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="c43b4-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c43b4-125">NonInteractive</span></span> | <span data-ttu-id="c43b4-126">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="c43b4-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c43b4-127">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="c43b4-127">Verbosity</span></span> | <span data-ttu-id="c43b4-128">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="c43b4-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c43b4-129">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c43b4-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c43b4-130">範例</span><span class="sxs-lookup"><span data-stu-id="c43b4-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="c43b4-131">如需其他範例，請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="c43b4-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
