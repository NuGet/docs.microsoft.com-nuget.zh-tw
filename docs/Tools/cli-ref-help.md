---
title: "NuGet CLI 說明命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Nuget.exe 的 [說明] 命令的參考"
keywords: "nuget 說明參考，幫助命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="d70c7-104">協助或嗎？</span><span class="sxs-lookup"><span data-stu-id="d70c7-104">help or ?</span></span> <span data-ttu-id="d70c7-105">命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d70c7-105">command (NuGet CLI)</span></span>

<span data-ttu-id="d70c7-106">**適用於：**所有&bullet;**支援的版本，**： 所有</span><span class="sxs-lookup"><span data-stu-id="d70c7-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="d70c7-107">顯示一般說明資訊，以及說明特定命令的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d70c7-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="d70c7-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="d70c7-108">Usage</span></span>

```
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="d70c7-109">其中 [的命令] 識別要顯示說明的特定命令。</span><span class="sxs-lookup"><span data-stu-id="d70c7-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="d70c7-110">有些命令，以留意指定*協助*第一個，做為與`nuget help install`，因為封裝 nuget.org 上名為 「 說明 」。如果您提供命令`nuget install help`，您不會取得 [說明] 的安裝指令，但會改為安裝說明的套件。</span><span class="sxs-lookup"><span data-stu-id="d70c7-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you'll not get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="d70c7-111">選項</span><span class="sxs-lookup"><span data-stu-id="d70c7-111">Options</span></span>

| <span data-ttu-id="d70c7-112">選項</span><span class="sxs-lookup"><span data-stu-id="d70c7-112">Option</span></span> | <span data-ttu-id="d70c7-113">說明</span><span class="sxs-lookup"><span data-stu-id="d70c7-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d70c7-114">全部</span><span class="sxs-lookup"><span data-stu-id="d70c7-114">All</span></span> | <span data-ttu-id="d70c7-115">列印所有可用的命令; 的詳細的說明如果特定命令提供，則會忽略。</span><span class="sxs-lookup"><span data-stu-id="d70c7-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="d70c7-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d70c7-116">ConfigFile</span></span> | <span data-ttu-id="d70c7-117">*（2.5 +)* NuGet 組態檔來套用。</span><span class="sxs-lookup"><span data-stu-id="d70c7-117">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="d70c7-118">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="d70c7-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="d70c7-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d70c7-119">ForceEnglishOutput</span></span> | <span data-ttu-id="d70c7-120">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="d70c7-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d70c7-121">說明</span><span class="sxs-lookup"><span data-stu-id="d70c7-121">Help</span></span> | <span data-ttu-id="d70c7-122">顯示的說明說明命令本身的資訊。</span><span class="sxs-lookup"><span data-stu-id="d70c7-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="d70c7-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="d70c7-123">Markdown</span></span> | <span data-ttu-id="d70c7-124">列印詳細的說明，以搭配使用時的 markdown 格式`-All`。</span><span class="sxs-lookup"><span data-stu-id="d70c7-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="d70c7-125">否則會忽略。</span><span class="sxs-lookup"><span data-stu-id="d70c7-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="d70c7-126">非互動式</span><span class="sxs-lookup"><span data-stu-id="d70c7-126">NonInteractive</span></span> | <span data-ttu-id="d70c7-127">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="d70c7-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d70c7-128">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="d70c7-128">Verbosity</span></span> | <span data-ttu-id="d70c7-129">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="d70c7-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="d70c7-130">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d70c7-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d70c7-131">範例</span><span class="sxs-lookup"><span data-stu-id="d70c7-131">Examples</span></span>

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
