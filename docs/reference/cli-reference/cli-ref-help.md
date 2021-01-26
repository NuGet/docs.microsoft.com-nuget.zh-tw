---
title: NuGet CLI help 命令
description: nuget.exe help 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779360"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="930a6-103">help 或 ?</span><span class="sxs-lookup"><span data-stu-id="930a6-103">help or ?</span></span> <span data-ttu-id="930a6-104"> (NuGet CLI 的命令) </span><span class="sxs-lookup"><span data-stu-id="930a6-104">command (NuGet CLI)</span></span>

<span data-ttu-id="930a6-105">**適用于：** 所有 &bullet; **支援的版本**：全部</span><span class="sxs-lookup"><span data-stu-id="930a6-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="930a6-106">顯示有關特定命令的一般說明資訊和說明資訊。</span><span class="sxs-lookup"><span data-stu-id="930a6-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="930a6-107">使用方式</span><span class="sxs-lookup"><span data-stu-id="930a6-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="930a6-108">where [command] 識別要顯示說明的特定命令。</span><span class="sxs-lookup"><span data-stu-id="930a6-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="930a6-109">使用一些命令時，請注意先 *指定說明* ， `nuget help install` 因為 nuget.org 上有一個名為 "help" 的封裝。如果您指定命令 `nuget install help` ，就不會取得安裝命令的說明，而是會安裝名為 help 的封裝。</span><span class="sxs-lookup"><span data-stu-id="930a6-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="930a6-110">選項。</span><span class="sxs-lookup"><span data-stu-id="930a6-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="930a6-111">列印所有可用命令的詳細說明;如果指定了特定命令，則會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="930a6-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="930a6-112">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="930a6-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="930a6-113">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="930a6-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="930a6-114">*(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="930a6-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="930a6-115">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="930a6-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="930a6-116">搭配使用時，請列印 markdown 格式的詳細說明 `-All` 。</span><span class="sxs-lookup"><span data-stu-id="930a6-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="930a6-117">否則會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="930a6-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="930a6-118">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="930a6-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="930a6-119">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="930a6-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="930a6-120">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="930a6-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="930a6-121">範例</span><span class="sxs-lookup"><span data-stu-id="930a6-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
