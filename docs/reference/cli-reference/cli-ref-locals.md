---
title: NuGet CLI 區域變數命令
description: Nuget.exe 區域變數命令的參考
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327805"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="b44dc-103">locals 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b44dc-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="b44dc-104">**適用于:** 套件耗&bullet;用量**支援的版本:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="b44dc-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="b44dc-105">清除或列出本機 NuGet 資源, 例如*HTTP*快取、*全域封裝*資料夾和 temp 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b44dc-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="b44dc-106">`locals`命令也可以用來顯示這些位置的清單。</span><span class="sxs-lookup"><span data-stu-id="b44dc-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="b44dc-107">如需詳細資訊, 請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="b44dc-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="b44dc-108">使用量</span><span class="sxs-lookup"><span data-stu-id="b44dc-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="b44dc-109">其中`<folder>` `all`, 是`plugins-cache` 、 `global-packages` `temp`    、(3.5 和更早版本)、、(3.4 +) 和 (4.8 +) 其中之一。 `packages-cache` `http-cache`</span><span class="sxs-lookup"><span data-stu-id="b44dc-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="b44dc-110">選項</span><span class="sxs-lookup"><span data-stu-id="b44dc-110">Options</span></span>

| <span data-ttu-id="b44dc-111">選項</span><span class="sxs-lookup"><span data-stu-id="b44dc-111">Option</span></span> | <span data-ttu-id="b44dc-112">說明</span><span class="sxs-lookup"><span data-stu-id="b44dc-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b44dc-113">清除</span><span class="sxs-lookup"><span data-stu-id="b44dc-113">Clear</span></span> | <span data-ttu-id="b44dc-114">清除指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="b44dc-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="b44dc-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b44dc-115">ConfigFile</span></span> | <span data-ttu-id="b44dc-116">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="b44dc-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b44dc-117">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="b44dc-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b44dc-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b44dc-118">ForceEnglishOutput</span></span> | <span data-ttu-id="b44dc-119">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="b44dc-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b44dc-120">Help</span><span class="sxs-lookup"><span data-stu-id="b44dc-120">Help</span></span> | <span data-ttu-id="b44dc-121">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="b44dc-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="b44dc-122">清單</span><span class="sxs-lookup"><span data-stu-id="b44dc-122">List</span></span> | <span data-ttu-id="b44dc-123">列出指定之資料夾的位置, 或所有資料夾與*all*一起使用時的位置。</span><span class="sxs-lookup"><span data-stu-id="b44dc-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="b44dc-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b44dc-124">NonInteractive</span></span> | <span data-ttu-id="b44dc-125">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="b44dc-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b44dc-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b44dc-126">Verbosity</span></span> | <span data-ttu-id="b44dc-127">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="b44dc-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b44dc-128">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b44dc-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b44dc-129">範例</span><span class="sxs-lookup"><span data-stu-id="b44dc-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="b44dc-130">如需其他範例, 請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="b44dc-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
