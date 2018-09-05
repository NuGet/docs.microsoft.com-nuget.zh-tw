---
title: NuGet CLI list 命令
description: Nuget.exe list 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549797"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="289a6-103">列出命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="289a6-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="289a6-104">**適用於：** 套件耗用量、 發行&bullet;**支援的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="289a6-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="289a6-105">顯示從指定來源的封裝清單。</span><span class="sxs-lookup"><span data-stu-id="289a6-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="289a6-106">如果未不指定任何來源，所有來源檔案中定義全域設定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`，會使用。</span><span class="sxs-lookup"><span data-stu-id="289a6-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="289a6-107">如果`NuGet.Config`不指定任何來源，然後`list`會使用預設的摘要 (nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="289a6-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="289a6-108">使用量</span><span class="sxs-lookup"><span data-stu-id="289a6-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="289a6-109">其中選擇性的搜尋條件會篩選顯示的清單。</span><span class="sxs-lookup"><span data-stu-id="289a6-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="289a6-110">就如同它們在 nuget.org 上使用它們時，搜尋字詞會套用至封裝、 標籤及封裝描述的名稱。</span><span class="sxs-lookup"><span data-stu-id="289a6-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="289a6-111">選項</span><span class="sxs-lookup"><span data-stu-id="289a6-111">Options</span></span>

| <span data-ttu-id="289a6-112">選項</span><span class="sxs-lookup"><span data-stu-id="289a6-112">Option</span></span> | <span data-ttu-id="289a6-113">描述</span><span class="sxs-lookup"><span data-stu-id="289a6-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="289a6-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="289a6-114">AllVersions</span></span> | <span data-ttu-id="289a6-115">列出所有版本的封裝。</span><span class="sxs-lookup"><span data-stu-id="289a6-115">List all versions of a package.</span></span> <span data-ttu-id="289a6-116">根據預設，會顯示最新套件版本。</span><span class="sxs-lookup"><span data-stu-id="289a6-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="289a6-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="289a6-117">ConfigFile</span></span> | <span data-ttu-id="289a6-118">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="289a6-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="289a6-119">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="289a6-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="289a6-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="289a6-120">ForceEnglishOutput</span></span> | <span data-ttu-id="289a6-121">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="289a6-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="289a6-122">說明</span><span class="sxs-lookup"><span data-stu-id="289a6-122">Help</span></span> | <span data-ttu-id="289a6-123">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="289a6-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="289a6-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="289a6-124">IncludeDelisted</span></span> | <span data-ttu-id="289a6-125">*（3.2 +)* 顯示未列出的套件。</span><span class="sxs-lookup"><span data-stu-id="289a6-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="289a6-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="289a6-126">NonInteractive</span></span> | <span data-ttu-id="289a6-127">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="289a6-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="289a6-128">發行前版本</span><span class="sxs-lookup"><span data-stu-id="289a6-128">PreRelease</span></span> | <span data-ttu-id="289a6-129">包含發行前版本套件清單中。</span><span class="sxs-lookup"><span data-stu-id="289a6-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="289a6-130">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="289a6-130">Source</span></span> | <span data-ttu-id="289a6-131">指定要搜尋的封裝來源清單。</span><span class="sxs-lookup"><span data-stu-id="289a6-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="289a6-132">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="289a6-132">Verbosity</span></span> | <span data-ttu-id="289a6-133">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="289a6-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="289a6-134">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="289a6-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="289a6-135">範例</span><span class="sxs-lookup"><span data-stu-id="289a6-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
