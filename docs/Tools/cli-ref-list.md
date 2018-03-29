---
title: NuGet CLI list 命令 |Microsoft 文件
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe list 命令的參考
keywords: nuget 清單參考，列出封裝命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61ad02eb99d6c56968c38841498df8aa9f74159d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="44a56-104">列出命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="44a56-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="44a56-105">**適用於：**封裝耗用量、 發行&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="44a56-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="44a56-106">顯示從指定的來源封裝的清單。</span><span class="sxs-lookup"><span data-stu-id="44a56-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="44a56-107">如果未不指定任何來源，所有來源檔案中定義全域設定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`，所使用。</span><span class="sxs-lookup"><span data-stu-id="44a56-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="44a56-108">如果`NuGet.Config`不指定任何來源，然後`list`會使用預設的摘要 (nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="44a56-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="44a56-109">使用量</span><span class="sxs-lookup"><span data-stu-id="44a56-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="44a56-110">其中選擇性的搜尋詞彙會篩選顯示的清單。</span><span class="sxs-lookup"><span data-stu-id="44a56-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="44a56-111">就如同它們在 nuget.org 上使用它們時，搜尋詞彙會套用至封裝、 標記，以及封裝描述的名稱。</span><span class="sxs-lookup"><span data-stu-id="44a56-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="44a56-112">選項</span><span class="sxs-lookup"><span data-stu-id="44a56-112">Options</span></span>

| <span data-ttu-id="44a56-113">選項</span><span class="sxs-lookup"><span data-stu-id="44a56-113">Option</span></span> | <span data-ttu-id="44a56-114">描述</span><span class="sxs-lookup"><span data-stu-id="44a56-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44a56-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="44a56-115">AllVersions</span></span> | <span data-ttu-id="44a56-116">列出所有封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="44a56-116">List all versions of a package.</span></span> <span data-ttu-id="44a56-117">根據預設，會顯示只有最新的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="44a56-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="44a56-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="44a56-118">ConfigFile</span></span> | <span data-ttu-id="44a56-119">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="44a56-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="44a56-120">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="44a56-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="44a56-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="44a56-121">ForceEnglishOutput</span></span> | <span data-ttu-id="44a56-122">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="44a56-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="44a56-123">說明</span><span class="sxs-lookup"><span data-stu-id="44a56-123">Help</span></span> | <span data-ttu-id="44a56-124">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="44a56-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="44a56-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="44a56-125">IncludeDelisted</span></span> | <span data-ttu-id="44a56-126">*（3.2 +)*顯示未列出的封裝。</span><span class="sxs-lookup"><span data-stu-id="44a56-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="44a56-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="44a56-127">NonInteractive</span></span> | <span data-ttu-id="44a56-128">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="44a56-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="44a56-129">發行前版本</span><span class="sxs-lookup"><span data-stu-id="44a56-129">PreRelease</span></span> | <span data-ttu-id="44a56-130">在清單中包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="44a56-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="44a56-131">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="44a56-131">Source</span></span> | <span data-ttu-id="44a56-132">指定要搜尋的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="44a56-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="44a56-133">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="44a56-133">Verbosity</span></span> | <span data-ttu-id="44a56-134">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="44a56-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="44a56-135">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="44a56-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="44a56-136">範例</span><span class="sxs-lookup"><span data-stu-id="44a56-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
