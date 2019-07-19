---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327605"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="837fa-103">setapikey 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="837fa-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="837fa-104">**適用物件:** 套件耗用量、 &bullet;發行**支援的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="837fa-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="837fa-105">將指定伺服器 URL 的 API 金鑰儲存至`NuGet.Config` , 使其不需要在後續命令中輸入。</span><span class="sxs-lookup"><span data-stu-id="837fa-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="837fa-106">使用量</span><span class="sxs-lookup"><span data-stu-id="837fa-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="837fa-107">其中`<source>`識別伺服器, 而`<key>`是要儲存的金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="837fa-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="837fa-108">如果`<source>`省略, 則會假設為 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="837fa-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="837fa-109">選項</span><span class="sxs-lookup"><span data-stu-id="837fa-109">Options</span></span>

| <span data-ttu-id="837fa-110">選項</span><span class="sxs-lookup"><span data-stu-id="837fa-110">Option</span></span> | <span data-ttu-id="837fa-111">說明</span><span class="sxs-lookup"><span data-stu-id="837fa-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="837fa-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="837fa-112">ConfigFile</span></span> | <span data-ttu-id="837fa-113">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="837fa-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="837fa-114">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="837fa-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="837fa-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="837fa-115">ForceEnglishOutput</span></span> | <span data-ttu-id="837fa-116">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="837fa-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="837fa-117">Help</span><span class="sxs-lookup"><span data-stu-id="837fa-117">Help</span></span> | <span data-ttu-id="837fa-118">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="837fa-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="837fa-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="837fa-119">NonInteractive</span></span> | <span data-ttu-id="837fa-120">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="837fa-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="837fa-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="837fa-121">Verbosity</span></span> | <span data-ttu-id="837fa-122">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="837fa-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="837fa-123">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="837fa-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="837fa-124">範例</span><span class="sxs-lookup"><span data-stu-id="837fa-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
