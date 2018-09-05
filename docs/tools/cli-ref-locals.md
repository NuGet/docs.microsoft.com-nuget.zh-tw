---
title: NuGet CLI locals 命令
description: Nuget.exe locals 命令參考
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545024"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="a8ef6-103">locals 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a8ef6-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="a8ef6-104">**適用於：** 套件耗用量&bullet;**支援的版本：** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="a8ef6-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="a8ef6-105">清除或列出本機 NuGet 資源，例如*http 快取*，*全域套件*資料夾，然後 [temp] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="a8ef6-106">`locals`命令也可用來顯示這些位置的清單。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="a8ef6-107">如需詳細資訊，請參閱 <<c0> [ 管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a8ef6-108">使用量</span><span class="sxs-lookup"><span data-stu-id="a8ef6-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="a8ef6-109">何處`<folder>`是其中一個`all`， `http-cache`， `packages-cache` *（3.5 和更早版本）*， `global-packages`， `temp` *（3.4 +）*，以及`plugins-cache` *（4.8 +）*。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="a8ef6-110">選項</span><span class="sxs-lookup"><span data-stu-id="a8ef6-110">Options</span></span>

| <span data-ttu-id="a8ef6-111">選項</span><span class="sxs-lookup"><span data-stu-id="a8ef6-111">Option</span></span> | <span data-ttu-id="a8ef6-112">描述</span><span class="sxs-lookup"><span data-stu-id="a8ef6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a8ef6-113">清除</span><span class="sxs-lookup"><span data-stu-id="a8ef6-113">Clear</span></span> | <span data-ttu-id="a8ef6-114">清除指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="a8ef6-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a8ef6-115">ConfigFile</span></span> | <span data-ttu-id="a8ef6-116">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a8ef6-117">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a8ef6-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a8ef6-118">ForceEnglishOutput</span></span> | <span data-ttu-id="a8ef6-119">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a8ef6-120">說明</span><span class="sxs-lookup"><span data-stu-id="a8ef6-120">Help</span></span> | <span data-ttu-id="a8ef6-121">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="a8ef6-122">清單</span><span class="sxs-lookup"><span data-stu-id="a8ef6-122">List</span></span> | <span data-ttu-id="a8ef6-123">列出指定的資料夾的位置或搭配使用時的所有資料夾的位置*所有*。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="a8ef6-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a8ef6-124">NonInteractive</span></span> | <span data-ttu-id="a8ef6-125">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a8ef6-126">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="a8ef6-126">Verbosity</span></span> | <span data-ttu-id="a8ef6-127">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a8ef6-128">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a8ef6-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a8ef6-129">範例</span><span class="sxs-lookup"><span data-stu-id="a8ef6-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="a8ef6-130">如需其他範例，請參閱 <<c0> [ 管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="a8ef6-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
