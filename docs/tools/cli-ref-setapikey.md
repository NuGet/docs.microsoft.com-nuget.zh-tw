---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817680"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="c7611-103">setapikey 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c7611-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="c7611-104">**適用於：** 封裝耗用量、 發行&bullet;**支援的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="c7611-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c7611-105">將 API 金鑰儲存到給定的伺服器 url`NuGet.Config`使它不需要輸入後續命令。</span><span class="sxs-lookup"><span data-stu-id="c7611-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="c7611-106">使用量</span><span class="sxs-lookup"><span data-stu-id="c7611-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="c7611-107">其中`<source>`識別伺服器並`<key>`是索引鍵或儲存的密碼。</span><span class="sxs-lookup"><span data-stu-id="c7611-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="c7611-108">如果`<source>`已省略，則會假設 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="c7611-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="c7611-109">選項</span><span class="sxs-lookup"><span data-stu-id="c7611-109">Options</span></span>

| <span data-ttu-id="c7611-110">選項</span><span class="sxs-lookup"><span data-stu-id="c7611-110">Option</span></span> | <span data-ttu-id="c7611-111">描述</span><span class="sxs-lookup"><span data-stu-id="c7611-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7611-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c7611-112">ConfigFile</span></span> | <span data-ttu-id="c7611-113">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="c7611-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c7611-114">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="c7611-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c7611-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c7611-115">ForceEnglishOutput</span></span> | <span data-ttu-id="c7611-116">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="c7611-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c7611-117">說明</span><span class="sxs-lookup"><span data-stu-id="c7611-117">Help</span></span> | <span data-ttu-id="c7611-118">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="c7611-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="c7611-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c7611-119">NonInteractive</span></span> | <span data-ttu-id="c7611-120">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="c7611-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c7611-121">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="c7611-121">Verbosity</span></span> | <span data-ttu-id="c7611-122">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="c7611-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c7611-123">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c7611-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c7611-124">範例</span><span class="sxs-lookup"><span data-stu-id="c7611-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
