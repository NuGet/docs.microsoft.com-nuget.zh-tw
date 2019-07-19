---
title: NuGet CLI help 命令
description: Nuget.exe help 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327795"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="bbd4b-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="bbd4b-103">help or ?</span></span> <span data-ttu-id="bbd4b-104">命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="bbd4b-104">command (NuGet CLI)</span></span>

<span data-ttu-id="bbd4b-105">**適用于:** 所有&bullet; **支援的版本**: 全部</span><span class="sxs-lookup"><span data-stu-id="bbd4b-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="bbd4b-106">顯示特定命令的一般說明資訊和說明資訊。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="bbd4b-107">使用量</span><span class="sxs-lookup"><span data-stu-id="bbd4b-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="bbd4b-108">其中 [command] 識別要顯示說明的特定命令。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="bbd4b-109">使用一些命令時, 請注意先  指定說明, 如同`nuget help install`, 因為 nuget.org 上有一個名為 "help" 的套件。如果您提供命令`nuget install help`, 就不會取得安裝命令的說明, 而是會安裝名為 [說明] 的套件。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="bbd4b-110">選項</span><span class="sxs-lookup"><span data-stu-id="bbd4b-110">Options</span></span>

| <span data-ttu-id="bbd4b-111">選項</span><span class="sxs-lookup"><span data-stu-id="bbd4b-111">Option</span></span> | <span data-ttu-id="bbd4b-112">描述</span><span class="sxs-lookup"><span data-stu-id="bbd4b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bbd4b-113">All</span><span class="sxs-lookup"><span data-stu-id="bbd4b-113">All</span></span> | <span data-ttu-id="bbd4b-114">列印所有可用命令的詳細說明;如果指定了特定的命令, 則會忽略。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="bbd4b-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="bbd4b-115">ConfigFile</span></span> | <span data-ttu-id="bbd4b-116">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bbd4b-117">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="bbd4b-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="bbd4b-118">ForceEnglishOutput</span></span> | <span data-ttu-id="bbd4b-119">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="bbd4b-120">Help</span><span class="sxs-lookup"><span data-stu-id="bbd4b-120">Help</span></span> | <span data-ttu-id="bbd4b-121">顯示 help 命令本身的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="bbd4b-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="bbd4b-122">Markdown</span></span> | <span data-ttu-id="bbd4b-123">當搭配使用時, `-All`列印 markdown 格式的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="bbd4b-124">否則會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="bbd4b-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="bbd4b-125">NonInteractive</span></span> | <span data-ttu-id="bbd4b-126">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="bbd4b-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="bbd4b-127">Verbosity</span></span> | <span data-ttu-id="bbd4b-128">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="bbd4b-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="bbd4b-129">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bbd4b-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="bbd4b-130">範例</span><span class="sxs-lookup"><span data-stu-id="bbd4b-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
