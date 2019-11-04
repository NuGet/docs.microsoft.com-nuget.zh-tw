---
title: NuGet CLI 清單命令
description: Nuget.exe list 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327735"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="f7ee5-103">list 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f7ee5-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="f7ee5-104">**適用物件:** 套件耗用量、 &bullet;發行**支援的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="f7ee5-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f7ee5-105">顯示來自指定來源的封裝清單。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="f7ee5-106">如果未指定來源, 則會使用全域設定檔`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`中定義的所有來源。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="f7ee5-107">如果`NuGet.Config`未指定來源, 則`list`會使用預設摘要 (nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="f7ee5-108">使用量</span><span class="sxs-lookup"><span data-stu-id="f7ee5-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="f7ee5-109">選擇性搜尋詞彙會在其中篩選所顯示的清單。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="f7ee5-110">搜尋詞彙會套用至封裝、標記和封裝描述的名稱, 就如同在 nuget.org 上使用它們一樣。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="f7ee5-111">選項</span><span class="sxs-lookup"><span data-stu-id="f7ee5-111">Options</span></span>

| <span data-ttu-id="f7ee5-112">選項</span><span class="sxs-lookup"><span data-stu-id="f7ee5-112">Option</span></span> | <span data-ttu-id="f7ee5-113">說明</span><span class="sxs-lookup"><span data-stu-id="f7ee5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f7ee5-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="f7ee5-114">AllVersions</span></span> | <span data-ttu-id="f7ee5-115">列出封裝的所有版本。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-115">List all versions of a package.</span></span> <span data-ttu-id="f7ee5-116">根據預設, 只會顯示最新的套件版本。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="f7ee5-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f7ee5-117">ConfigFile</span></span> | <span data-ttu-id="f7ee5-118">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f7ee5-119">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f7ee5-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f7ee5-120">ForceEnglishOutput</span></span> | <span data-ttu-id="f7ee5-121">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f7ee5-122">Help</span><span class="sxs-lookup"><span data-stu-id="f7ee5-122">Help</span></span> | <span data-ttu-id="f7ee5-123">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="f7ee5-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="f7ee5-124">IncludeDelisted</span></span> | <span data-ttu-id="f7ee5-125">*(3.2 +)* 顯示未列出的套件。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="f7ee5-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f7ee5-126">NonInteractive</span></span> | <span data-ttu-id="f7ee5-127">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f7ee5-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="f7ee5-128">PreRelease</span></span> | <span data-ttu-id="f7ee5-129">包含清單中的發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="f7ee5-130">Source</span><span class="sxs-lookup"><span data-stu-id="f7ee5-130">Source</span></span> | <span data-ttu-id="f7ee5-131">指定要搜尋的封裝來源清單。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="f7ee5-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f7ee5-132">Verbosity</span></span> | <span data-ttu-id="f7ee5-133">指定輸出中顯示的詳細資料量: [*一般*]、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="f7ee5-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f7ee5-134">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f7ee5-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f7ee5-135">範例</span><span class="sxs-lookup"><span data-stu-id="f7ee5-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
