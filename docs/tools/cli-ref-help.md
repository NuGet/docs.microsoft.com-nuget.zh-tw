---
title: NuGet CLI [說明] 命令
description: Nuget.exe 的 [說明] 命令的參考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="e3bb4-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="e3bb4-103">help or ?</span></span> <span data-ttu-id="e3bb4-104">命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e3bb4-104">command (NuGet CLI)</span></span>

<span data-ttu-id="e3bb4-105">**適用於：** 所有&bullet;**支援的版本，**： 所有</span><span class="sxs-lookup"><span data-stu-id="e3bb4-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="e3bb4-106">顯示一般說明資訊，以及說明特定命令的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="e3bb4-107">使用量</span><span class="sxs-lookup"><span data-stu-id="e3bb4-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="e3bb4-108">其中 [的命令] 識別要顯示說明的特定命令。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="e3bb4-109">有些命令，以留意指定*協助*第一個，做為與`nuget help install`，因為封裝 nuget.org 上名為 「 說明 」。如果您提供命令`nuget install help`，您將不會取得 [說明] 的安裝命令，但會改為安裝說明的套件。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="e3bb4-110">選項</span><span class="sxs-lookup"><span data-stu-id="e3bb4-110">Options</span></span>

| <span data-ttu-id="e3bb4-111">選項</span><span class="sxs-lookup"><span data-stu-id="e3bb4-111">Option</span></span> | <span data-ttu-id="e3bb4-112">描述</span><span class="sxs-lookup"><span data-stu-id="e3bb4-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3bb4-113">全部</span><span class="sxs-lookup"><span data-stu-id="e3bb4-113">All</span></span> | <span data-ttu-id="e3bb4-114">列印所有可用的命令; 的詳細的說明如果特定命令提供，則會忽略。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="e3bb4-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e3bb4-115">ConfigFile</span></span> | <span data-ttu-id="e3bb4-116">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e3bb4-117">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e3bb4-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e3bb4-118">ForceEnglishOutput</span></span> | <span data-ttu-id="e3bb4-119">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e3bb4-120">說明</span><span class="sxs-lookup"><span data-stu-id="e3bb4-120">Help</span></span> | <span data-ttu-id="e3bb4-121">顯示的說明說明命令本身的資訊。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="e3bb4-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="e3bb4-122">Markdown</span></span> | <span data-ttu-id="e3bb4-123">列印詳細的說明，以搭配使用時的 markdown 格式`-All`。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="e3bb4-124">否則會忽略。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="e3bb4-125">非互動式</span><span class="sxs-lookup"><span data-stu-id="e3bb4-125">NonInteractive</span></span> | <span data-ttu-id="e3bb4-126">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e3bb4-127">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="e3bb4-127">Verbosity</span></span> | <span data-ttu-id="e3bb4-128">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="e3bb4-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e3bb4-129">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e3bb4-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e3bb4-130">範例</span><span class="sxs-lookup"><span data-stu-id="e3bb4-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
