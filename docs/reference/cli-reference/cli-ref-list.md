---
title: NuGet CLI 清單命令
description: nuget.exe list 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780059"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="1bf67-103">列出命令 (NuGet CLI) </span><span class="sxs-lookup"><span data-stu-id="1bf67-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="1bf67-104">**適用于：** 套件耗用量、發佈 &bullet; **支援的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="1bf67-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1bf67-105">顯示指定來源的套件清單。</span><span class="sxs-lookup"><span data-stu-id="1bf67-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="1bf67-106">如果未指定任何來源，則會使用全域設定檔中定義的所有來源 `%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` ）。</span><span class="sxs-lookup"><span data-stu-id="1bf67-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="1bf67-107">如果 `NuGet.Config` 未指定來源，則會 `list` 使用預設摘要 (nuget.org) 。</span><span class="sxs-lookup"><span data-stu-id="1bf67-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="1bf67-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="1bf67-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="1bf67-109">選擇性搜尋詞彙將篩選所顯示的清單。</span><span class="sxs-lookup"><span data-stu-id="1bf67-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="1bf67-110">[搜尋詞彙](../../consume-packages/finding-and-choosing-packages.md#search-syntax) 會套用至套件、標籤和套件描述的名稱，就像在 nuget.org 上使用它們時一樣。</span><span class="sxs-lookup"><span data-stu-id="1bf67-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="1bf67-111">選項。</span><span class="sxs-lookup"><span data-stu-id="1bf67-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="1bf67-112">列出套件的所有版本。</span><span class="sxs-lookup"><span data-stu-id="1bf67-112">List all versions of a package.</span></span> <span data-ttu-id="1bf67-113">依預設，只會顯示最新的套件版本。</span><span class="sxs-lookup"><span data-stu-id="1bf67-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="1bf67-114">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="1bf67-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1bf67-115">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="1bf67-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="1bf67-116">*(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="1bf67-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="1bf67-117">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="1bf67-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="1bf67-118">*(3.2 +)* 顯示未列出的套件。</span><span class="sxs-lookup"><span data-stu-id="1bf67-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="1bf67-119">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="1bf67-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="1bf67-120">在清單中包含發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="1bf67-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="1bf67-121">要搜尋的套件來源。</span><span class="sxs-lookup"><span data-stu-id="1bf67-121">The package source to search.</span></span> <span data-ttu-id="1bf67-122">您可以多次使用此選項來指定多個來源 `-Source` 。</span><span class="sxs-lookup"><span data-stu-id="1bf67-122">You can specify multiple sources by using the `-Source` option multiple times.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="1bf67-123">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="1bf67-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="1bf67-124">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1bf67-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1bf67-125">範例</span><span class="sxs-lookup"><span data-stu-id="1bf67-125">Examples</span></span>

<span data-ttu-id="1bf67-126">從設定的摘要列出所有套件：</span><span class="sxs-lookup"><span data-stu-id="1bf67-126">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="1bf67-127">列出具有詳細詳細資訊的 Azure 相關套件：</span><span class="sxs-lookup"><span data-stu-id="1bf67-127">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="1bf67-128">從設定的摘要列出 Azure 相關套件的所有版本：</span><span class="sxs-lookup"><span data-stu-id="1bf67-128">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="1bf67-129">從指定的來源/摘要列出 JSON 相關封裝的所有版本：</span><span class="sxs-lookup"><span data-stu-id="1bf67-129">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="1bf67-130">列出來自多個來源/摘要的 JSON 相關套件：</span><span class="sxs-lookup"><span data-stu-id="1bf67-130">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
