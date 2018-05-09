---
title: NuGet CLI list 命令
description: Nuget.exe list 命令的參考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="8fc0c-103">列出命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8fc0c-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="8fc0c-104">**適用於：**封裝耗用量、 發行&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="8fc0c-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8fc0c-105">顯示從指定的來源封裝的清單。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="8fc0c-106">如果未不指定任何來源，所有來源檔案中定義全域設定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`，所使用。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="8fc0c-107">如果`NuGet.Config`不指定任何來源，然後`list`會使用預設的摘要 (nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="8fc0c-108">使用量</span><span class="sxs-lookup"><span data-stu-id="8fc0c-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="8fc0c-109">其中選擇性的搜尋詞彙會篩選顯示的清單。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="8fc0c-110">就如同它們在 nuget.org 上使用它們時，搜尋詞彙會套用至封裝、 標記，以及封裝描述的名稱。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="8fc0c-111">選項</span><span class="sxs-lookup"><span data-stu-id="8fc0c-111">Options</span></span>

| <span data-ttu-id="8fc0c-112">選項</span><span class="sxs-lookup"><span data-stu-id="8fc0c-112">Option</span></span> | <span data-ttu-id="8fc0c-113">描述</span><span class="sxs-lookup"><span data-stu-id="8fc0c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8fc0c-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="8fc0c-114">AllVersions</span></span> | <span data-ttu-id="8fc0c-115">列出所有封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-115">List all versions of a package.</span></span> <span data-ttu-id="8fc0c-116">根據預設，會顯示只有最新的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="8fc0c-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8fc0c-117">ConfigFile</span></span> | <span data-ttu-id="8fc0c-118">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8fc0c-119">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8fc0c-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8fc0c-120">ForceEnglishOutput</span></span> | <span data-ttu-id="8fc0c-121">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8fc0c-122">說明</span><span class="sxs-lookup"><span data-stu-id="8fc0c-122">Help</span></span> | <span data-ttu-id="8fc0c-123">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="8fc0c-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="8fc0c-124">IncludeDelisted</span></span> | <span data-ttu-id="8fc0c-125">*（3.2 +)* 顯示未列出的封裝。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="8fc0c-126">非互動式</span><span class="sxs-lookup"><span data-stu-id="8fc0c-126">NonInteractive</span></span> | <span data-ttu-id="8fc0c-127">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8fc0c-128">發行前版本</span><span class="sxs-lookup"><span data-stu-id="8fc0c-128">PreRelease</span></span> | <span data-ttu-id="8fc0c-129">在清單中包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="8fc0c-130">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="8fc0c-130">Source</span></span> | <span data-ttu-id="8fc0c-131">指定要搜尋的套件來源清單。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="8fc0c-132">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="8fc0c-132">Verbosity</span></span> | <span data-ttu-id="8fc0c-133">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="8fc0c-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8fc0c-134">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8fc0c-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8fc0c-135">範例</span><span class="sxs-lookup"><span data-stu-id="8fc0c-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
