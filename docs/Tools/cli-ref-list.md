---
title: "NuGet CLI list 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe list 命令的參考"
keywords: "nuget 清單參考，列出封裝命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5a1f68aaffd26a0f903aa3a7a4a450a0121191c3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="58db7-104">列出命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="58db7-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="58db7-105">**適用於：**封裝耗用量、 發行&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="58db7-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="58db7-106">顯示從指定的來源封裝的清單。</span><span class="sxs-lookup"><span data-stu-id="58db7-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="58db7-107">如果未不指定任何來源，所有來源檔案中定義全域設定， `%AppData%\NuGet\NuGet.Config`，所使用。</span><span class="sxs-lookup"><span data-stu-id="58db7-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="58db7-108">如果`NuGet.Config`不指定任何來源，然後`list`會使用預設的摘要 (nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="58db7-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="58db7-109">使用量</span><span class="sxs-lookup"><span data-stu-id="58db7-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="58db7-110">其中選擇性的搜尋詞彙會篩選顯示的清單。</span><span class="sxs-lookup"><span data-stu-id="58db7-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="58db7-111">搜尋字詞會套用至封裝、 標記，以及封裝描述的名稱。</span><span class="sxs-lookup"><span data-stu-id="58db7-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="58db7-112">選項</span><span class="sxs-lookup"><span data-stu-id="58db7-112">Options</span></span>

| <span data-ttu-id="58db7-113">選項</span><span class="sxs-lookup"><span data-stu-id="58db7-113">Option</span></span> | <span data-ttu-id="58db7-114">描述</span><span class="sxs-lookup"><span data-stu-id="58db7-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="58db7-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="58db7-115">AllVersions</span></span> | <span data-ttu-id="58db7-116">列出所有封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="58db7-116">List all versions of a package.</span></span> <span data-ttu-id="58db7-117">根據預設，會顯示只有最新的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="58db7-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="58db7-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="58db7-118">ConfigFile</span></span> | <span data-ttu-id="58db7-119">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="58db7-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="58db7-120">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="58db7-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="58db7-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="58db7-121">ForceEnglishOutput</span></span> | <span data-ttu-id="58db7-122">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="58db7-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="58db7-123">說明</span><span class="sxs-lookup"><span data-stu-id="58db7-123">Help</span></span> | <span data-ttu-id="58db7-124">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="58db7-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="58db7-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="58db7-125">IncludeDelisted</span></span> | <span data-ttu-id="58db7-126">*（3.2 +)*顯示未列出的封裝。</span><span class="sxs-lookup"><span data-stu-id="58db7-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="58db7-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="58db7-127">NonInteractive</span></span> | <span data-ttu-id="58db7-128">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="58db7-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="58db7-129">發行前版本</span><span class="sxs-lookup"><span data-stu-id="58db7-129">PreRelease</span></span> | <span data-ttu-id="58db7-130">在清單中包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="58db7-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="58db7-131">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="58db7-131">Source</span></span> | <span data-ttu-id="58db7-132">指定要搜尋的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="58db7-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="58db7-133">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="58db7-133">Verbosity</span></span> | <span data-ttu-id="58db7-134">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="58db7-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="58db7-135">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="58db7-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="58db7-136">範例</span><span class="sxs-lookup"><span data-stu-id="58db7-136">Examples</span></span>

```cli
nuget list

nuget list -Verbosity detailed -AllVersions
```
