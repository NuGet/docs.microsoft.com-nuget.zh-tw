---
title: NuGet CLI 搜尋命令
description: nuget.exe 搜尋命令的參考
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 35e4906960534299418cb2a17c190476708b2634
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623264"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="9c019-103"> (NuGet CLI 的搜尋命令) </span><span class="sxs-lookup"><span data-stu-id="9c019-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="9c019-104">**適用物件：** 套件耗用量 &bullet; **支援的版本：** 5.8 +</span><span class="sxs-lookup"><span data-stu-id="9c019-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="9c019-105">使用提供的查詢字串來搜尋指定的來源。</span><span class="sxs-lookup"><span data-stu-id="9c019-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="9c019-106">如果未指定任何來源，則會使用% AppData% \NuGet\NuGet.config 中定義的所有來源。</span><span class="sxs-lookup"><span data-stu-id="9c019-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="9c019-107">使用方式</span><span class="sxs-lookup"><span data-stu-id="9c019-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="9c019-108">搜尋詞彙會套用至套件、標籤和套件描述的名稱，就像在 nuget.org 上使用它們時一樣。</span><span class="sxs-lookup"><span data-stu-id="9c019-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="9c019-109">選項。</span><span class="sxs-lookup"><span data-stu-id="9c019-109">Options</span></span>

| <span data-ttu-id="9c019-110">名稱</span><span class="sxs-lookup"><span data-stu-id="9c019-110">Name</span></span> | <span data-ttu-id="9c019-111">描述</span><span class="sxs-lookup"><span data-stu-id="9c019-111">Description</span></span> | <span data-ttu-id="9c019-112">使用方式</span><span class="sxs-lookup"><span data-stu-id="9c019-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="9c019-113">發佈</span><span class="sxs-lookup"><span data-stu-id="9c019-113">PreRelease</span></span> | <span data-ttu-id="9c019-114">預設不會包含發行前版本的封裝，但可以使用此引數來包含</span><span class="sxs-lookup"><span data-stu-id="9c019-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="9c019-115">-發行前版本</span><span class="sxs-lookup"><span data-stu-id="9c019-115">-PreRelease</span></span> |
| <span data-ttu-id="9c019-116">來源</span><span class="sxs-lookup"><span data-stu-id="9c019-116">Source</span></span> | <span data-ttu-id="9c019-117">特定套件來源 (s) 進行搜尋，而不是在__nuget.config__中查詢預設來源</span><span class="sxs-lookup"><span data-stu-id="9c019-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="9c019-118">-來源 `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="9c019-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="9c019-119">Take</span><span class="sxs-lookup"><span data-stu-id="9c019-119">Take</span></span> | <span data-ttu-id="9c019-120">要傳回的結果數目。</span><span class="sxs-lookup"><span data-stu-id="9c019-120">The number of results to return.</span></span> <span data-ttu-id="9c019-121">預設值為 20。</span><span class="sxs-lookup"><span data-stu-id="9c019-121">The default value is 20.</span></span> | <span data-ttu-id="9c019-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="9c019-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="9c019-123">詳細程度</span><span class="sxs-lookup"><span data-stu-id="9c019-123">Verbosity</span></span> | <span data-ttu-id="9c019-124">要在輸出中顯示的詳細資料層級。</span><span class="sxs-lookup"><span data-stu-id="9c019-124">The level of detail to display in the output.</span></span> <span data-ttu-id="9c019-125">預設值為 _normal_。</span><span class="sxs-lookup"><span data-stu-id="9c019-125">The default is _normal_.</span></span> <span data-ttu-id="9c019-126"> (請參閱下面的附注) </span><span class="sxs-lookup"><span data-stu-id="9c019-126">(See the note below)</span></span>  | <span data-ttu-id="9c019-127">-詳細資訊 `<quiet\|normal\|detailed>`</span><span class="sxs-lookup"><span data-stu-id="9c019-127">-Verbosity `<quiet\|normal\|detailed>`</span></span> |
| <span data-ttu-id="9c019-128">説明</span><span class="sxs-lookup"><span data-stu-id="9c019-128">Help</span></span> | <span data-ttu-id="9c019-129">顯示命令的說明資訊</span><span class="sxs-lookup"><span data-stu-id="9c019-129">Displays help information for the command</span></span> | <span data-ttu-id="9c019-130">-Help</span><span class="sxs-lookup"><span data-stu-id="9c019-130">-Help</span></span> |

<span data-ttu-id="9c019-131">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9c019-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

<span data-ttu-id="9c019-132">__注意__</span><span class="sxs-lookup"><span data-stu-id="9c019-132">__NOTE__</span></span>

<span data-ttu-id="9c019-133">詳細資訊層級：</span><span class="sxs-lookup"><span data-stu-id="9c019-133">Verbosity Levels:</span></span>

* <span data-ttu-id="9c019-134">_quiet_無訊息套件識別碼，版本</span><span class="sxs-lookup"><span data-stu-id="9c019-134">_quiet_ - Package ID, Version</span></span>
* <span data-ttu-id="9c019-135">_一般_ 套件識別碼、版本、下載、描述預覽</span><span class="sxs-lookup"><span data-stu-id="9c019-135">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
* <span data-ttu-id="9c019-136">_詳細_ 封裝識別碼、版本、下載、完整描述、其他資訊（例如查詢 URL）</span><span class="sxs-lookup"><span data-stu-id="9c019-136">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="9c019-137">範例</span><span class="sxs-lookup"><span data-stu-id="9c019-137">Examples</span></span>

<span data-ttu-id="9c019-138">從預設來源搜尋 *記錄*相關的套件：</span><span class="sxs-lookup"><span data-stu-id="9c019-138">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="9c019-139">使用詳細的詳細資訊搜尋 *記錄*相關套件：</span><span class="sxs-lookup"><span data-stu-id="9c019-139">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="9c019-140">搜尋 *記錄*相關的套件，並只顯示前5個結果：</span><span class="sxs-lookup"><span data-stu-id="9c019-140">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="9c019-141">從指定的來源/摘要搜尋 *JSON*相關封裝，包括發行前版本：</span><span class="sxs-lookup"><span data-stu-id="9c019-141">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="9c019-142">從多個來源/摘要搜尋 *JSON*相關套件：</span><span class="sxs-lookup"><span data-stu-id="9c019-142">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
