---
title: "NuGet CLI list 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Nuget.exe list 命令的參考"
keywords: "nuget 清單參考，列出封裝命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="ef538-104">列出命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ef538-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="ef538-105">**適用於：**封裝耗用量、 發行&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="ef538-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ef538-106">顯示從指定的來源封裝的清單。</span><span class="sxs-lookup"><span data-stu-id="ef538-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="ef538-107">如果未不指定任何來源，所有來源檔案中定義全域設定， `%AppData%\NuGet\NuGet.Config`，所使用。</span><span class="sxs-lookup"><span data-stu-id="ef538-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="ef538-108">如果`NuGet.Config`不指定任何來源，然後`list`會使用預設的摘要 (nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="ef538-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="ef538-109">使用方式</span><span class="sxs-lookup"><span data-stu-id="ef538-109">Usage</span></span>

```
nuget list [search terms] [options]
```

<span data-ttu-id="ef538-110">其中選擇性的搜尋詞彙會篩選顯示的清單。</span><span class="sxs-lookup"><span data-stu-id="ef538-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="ef538-111">搜尋字詞會套用至封裝、 標記，以及封裝描述的名稱。</span><span class="sxs-lookup"><span data-stu-id="ef538-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="ef538-112">選項</span><span class="sxs-lookup"><span data-stu-id="ef538-112">Options</span></span>
| <span data-ttu-id="ef538-113">選項</span><span class="sxs-lookup"><span data-stu-id="ef538-113">Option</span></span> | <span data-ttu-id="ef538-114">說明</span><span class="sxs-lookup"><span data-stu-id="ef538-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef538-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="ef538-115">AllVersions</span></span> | <span data-ttu-id="ef538-116">列出所有封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="ef538-116">List all versions of a package.</span></span> <span data-ttu-id="ef538-117">根據預設，會顯示只有最新的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="ef538-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="ef538-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ef538-118">ConfigFile</span></span> | <span data-ttu-id="ef538-119">*（2.5 +)* NuGet 組態檔來套用。</span><span class="sxs-lookup"><span data-stu-id="ef538-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="ef538-120">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="ef538-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ef538-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ef538-121">ForceEnglishOutput</span></span> | <span data-ttu-id="ef538-122">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="ef538-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ef538-123">說明</span><span class="sxs-lookup"><span data-stu-id="ef538-123">Help</span></span> | <span data-ttu-id="ef538-124">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="ef538-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="ef538-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="ef538-125">IncludeDelisted</span></span> | <span data-ttu-id="ef538-126">*（3.2 +)*顯示未列出的封裝。</span><span class="sxs-lookup"><span data-stu-id="ef538-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="ef538-127">非互動式</span><span class="sxs-lookup"><span data-stu-id="ef538-127">NonInteractive</span></span> | <span data-ttu-id="ef538-128">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="ef538-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ef538-129">發行前版本</span><span class="sxs-lookup"><span data-stu-id="ef538-129">PreRelease</span></span> | <span data-ttu-id="ef538-130">在清單中包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="ef538-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="ef538-131">來源</span><span class="sxs-lookup"><span data-stu-id="ef538-131">Source</span></span> | <span data-ttu-id="ef538-132">指定要搜尋的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="ef538-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="ef538-133">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="ef538-133">Verbosity</span></span> | <span data-ttu-id="ef538-134">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="ef538-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="ef538-135">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ef538-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ef538-136">範例</span><span class="sxs-lookup"><span data-stu-id="ef538-136">Examples</span></span>

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
