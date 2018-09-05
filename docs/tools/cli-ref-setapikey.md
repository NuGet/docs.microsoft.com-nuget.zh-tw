---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549216"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="5f3a9-103">setapikey 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5f3a9-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="5f3a9-104">**適用於：** 套件耗用量、 發行&bullet;**支援的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="5f3a9-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5f3a9-105">將 API 金鑰儲存到指定的伺服器 url `NuGet.Config` ，讓它不需要輸入後續命令。</span><span class="sxs-lookup"><span data-stu-id="5f3a9-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="5f3a9-106">使用量</span><span class="sxs-lookup"><span data-stu-id="5f3a9-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="5f3a9-107">何處`<source>`識別的伺服器和`<key>`是索引鍵或儲存的密碼。</span><span class="sxs-lookup"><span data-stu-id="5f3a9-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="5f3a9-108">如果`<source>`已省略，nuget.org 會假設。</span><span class="sxs-lookup"><span data-stu-id="5f3a9-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="5f3a9-109">選項</span><span class="sxs-lookup"><span data-stu-id="5f3a9-109">Options</span></span>

| <span data-ttu-id="5f3a9-110">選項</span><span class="sxs-lookup"><span data-stu-id="5f3a9-110">Option</span></span> | <span data-ttu-id="5f3a9-111">描述</span><span class="sxs-lookup"><span data-stu-id="5f3a9-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5f3a9-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5f3a9-112">ConfigFile</span></span> | <span data-ttu-id="5f3a9-113">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="5f3a9-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5f3a9-114">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="5f3a9-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5f3a9-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5f3a9-115">ForceEnglishOutput</span></span> | <span data-ttu-id="5f3a9-116">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="5f3a9-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5f3a9-117">說明</span><span class="sxs-lookup"><span data-stu-id="5f3a9-117">Help</span></span> | <span data-ttu-id="5f3a9-118">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="5f3a9-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="5f3a9-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5f3a9-119">NonInteractive</span></span> | <span data-ttu-id="5f3a9-120">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="5f3a9-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5f3a9-121">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="5f3a9-121">Verbosity</span></span> | <span data-ttu-id="5f3a9-122">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="5f3a9-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5f3a9-123">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5f3a9-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5f3a9-124">範例</span><span class="sxs-lookup"><span data-stu-id="5f3a9-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
