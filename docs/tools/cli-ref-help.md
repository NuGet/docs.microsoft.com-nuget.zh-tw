---
title: NuGet CLI 說明 命令
description: Nuget.exe 的 [說明] 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546559"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="5128e-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="5128e-103">help or ?</span></span> <span data-ttu-id="5128e-104">命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5128e-104">command (NuGet CLI)</span></span>

<span data-ttu-id="5128e-105">**適用於：** 所有&bullet;**支援的版本**： 所有</span><span class="sxs-lookup"><span data-stu-id="5128e-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="5128e-106">顯示一般說明資訊，以及說明特定命令的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5128e-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="5128e-107">使用量</span><span class="sxs-lookup"><span data-stu-id="5128e-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="5128e-108">其中 [command] 會識別特定的命令要顯示的說明。</span><span class="sxs-lookup"><span data-stu-id="5128e-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="5128e-109">一些命令，以留意指定*幫助*第一次，以使用`nuget help install`，因為有在 nuget.org 上名為 「 說明 」 的套件。如果您提供命令`nuget install help`，您將不會取得安裝命令的說明，但會改為安裝說明的套件。</span><span class="sxs-lookup"><span data-stu-id="5128e-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="5128e-110">選項</span><span class="sxs-lookup"><span data-stu-id="5128e-110">Options</span></span>

| <span data-ttu-id="5128e-111">選項</span><span class="sxs-lookup"><span data-stu-id="5128e-111">Option</span></span> | <span data-ttu-id="5128e-112">描述</span><span class="sxs-lookup"><span data-stu-id="5128e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5128e-113">全部</span><span class="sxs-lookup"><span data-stu-id="5128e-113">All</span></span> | <span data-ttu-id="5128e-114">列印所有可用的命令; 的詳細的說明如果有特定的命令，則會忽略。</span><span class="sxs-lookup"><span data-stu-id="5128e-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="5128e-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5128e-115">ConfigFile</span></span> | <span data-ttu-id="5128e-116">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="5128e-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5128e-117">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="5128e-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5128e-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5128e-118">ForceEnglishOutput</span></span> | <span data-ttu-id="5128e-119">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="5128e-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5128e-120">說明</span><span class="sxs-lookup"><span data-stu-id="5128e-120">Help</span></span> | <span data-ttu-id="5128e-121">顯示說明資訊本身的 [說明] 命令。</span><span class="sxs-lookup"><span data-stu-id="5128e-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="5128e-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="5128e-122">Markdown</span></span> | <span data-ttu-id="5128e-123">列印與搭配使用時的 markdown 格式的詳細的說明`-All`。</span><span class="sxs-lookup"><span data-stu-id="5128e-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="5128e-124">否則會忽略。</span><span class="sxs-lookup"><span data-stu-id="5128e-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="5128e-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5128e-125">NonInteractive</span></span> | <span data-ttu-id="5128e-126">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="5128e-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5128e-127">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="5128e-127">Verbosity</span></span> | <span data-ttu-id="5128e-128">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="5128e-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5128e-129">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5128e-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5128e-130">範例</span><span class="sxs-lookup"><span data-stu-id="5128e-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
