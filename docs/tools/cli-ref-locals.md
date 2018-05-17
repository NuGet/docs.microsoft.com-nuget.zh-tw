---
title: NuGet CLI [區域變數] 命令
description: Nuget.exe 區域變數命令參考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="7dea3-103">locals 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7dea3-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="7dea3-104">**適用於：** 封裝耗用量&bullet;**支援的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="7dea3-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="7dea3-105">清除或列出本機 NuGet 資源，例如*http 快取*，*全域封裝*資料夾以及暫存資料夾。</span><span class="sxs-lookup"><span data-stu-id="7dea3-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="7dea3-106">`locals`命令也可用來顯示這些位置的清單。</span><span class="sxs-lookup"><span data-stu-id="7dea3-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="7dea3-107">如需詳細資訊，請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="7dea3-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7dea3-108">使用量</span><span class="sxs-lookup"><span data-stu-id="7dea3-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="7dea3-109">其中`<folder>`是其中一個`all`， `http-cache`， `packages-cache` *（3.5 及更早版本）*， `global-packages`，和`temp` *（3.4 +）*。</span><span class="sxs-lookup"><span data-stu-id="7dea3-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="7dea3-110">選項</span><span class="sxs-lookup"><span data-stu-id="7dea3-110">Options</span></span>

| <span data-ttu-id="7dea3-111">選項</span><span class="sxs-lookup"><span data-stu-id="7dea3-111">Option</span></span> | <span data-ttu-id="7dea3-112">描述</span><span class="sxs-lookup"><span data-stu-id="7dea3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7dea3-113">清除</span><span class="sxs-lookup"><span data-stu-id="7dea3-113">Clear</span></span> | <span data-ttu-id="7dea3-114">清除指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7dea3-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="7dea3-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7dea3-115">ConfigFile</span></span> | <span data-ttu-id="7dea3-116">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="7dea3-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7dea3-117">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="7dea3-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7dea3-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7dea3-118">ForceEnglishOutput</span></span> | <span data-ttu-id="7dea3-119">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="7dea3-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7dea3-120">說明</span><span class="sxs-lookup"><span data-stu-id="7dea3-120">Help</span></span> | <span data-ttu-id="7dea3-121">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="7dea3-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="7dea3-122">清單</span><span class="sxs-lookup"><span data-stu-id="7dea3-122">List</span></span> | <span data-ttu-id="7dea3-123">列出指定的資料夾位置或搭配使用時的所有資料夾的位置*所有*。</span><span class="sxs-lookup"><span data-stu-id="7dea3-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="7dea3-124">非互動式</span><span class="sxs-lookup"><span data-stu-id="7dea3-124">NonInteractive</span></span> | <span data-ttu-id="7dea3-125">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="7dea3-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7dea3-126">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="7dea3-126">Verbosity</span></span> | <span data-ttu-id="7dea3-127">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="7dea3-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7dea3-128">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7dea3-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7dea3-129">範例</span><span class="sxs-lookup"><span data-stu-id="7dea3-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="7dea3-130">如需其他範例，請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="7dea3-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
