---
title: NuGet CLI setapikey 命令
description: Nuget.exe setapikey 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383965"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="3f11c-103">setapikey 命令（NuGet CLI）</span><span class="sxs-lookup"><span data-stu-id="3f11c-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="3f11c-104">**適用物件：** 套件耗用量、發行 &bullet;**支援的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="3f11c-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3f11c-105">將指定伺服器 URL 的 API 金鑰儲存至 `NuGet.Config`，讓它不需要針對後續命令輸入。</span><span class="sxs-lookup"><span data-stu-id="3f11c-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="3f11c-106">使用</span><span class="sxs-lookup"><span data-stu-id="3f11c-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="3f11c-107">其中 `<source>` 會識別伺服器，而 `<key>` 則是要儲存的金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="3f11c-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="3f11c-108">如果省略 `<source>`，則會假設為 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="3f11c-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

> [!NOTE]
> <span data-ttu-id="3f11c-109">API 金鑰不會用來向私人摘要進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3f11c-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="3f11c-110">請參閱[`nuget sources` 命令](../cli-reference/cli-ref-sources.md)，以管理用來驗證來源的認證。</span><span class="sxs-lookup"><span data-stu-id="3f11c-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>

## <a name="options"></a><span data-ttu-id="3f11c-111">選項</span><span class="sxs-lookup"><span data-stu-id="3f11c-111">Options</span></span>

| <span data-ttu-id="3f11c-112">選項</span><span class="sxs-lookup"><span data-stu-id="3f11c-112">Option</span></span> | <span data-ttu-id="3f11c-113">描述</span><span class="sxs-lookup"><span data-stu-id="3f11c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3f11c-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3f11c-114">ConfigFile</span></span> | <span data-ttu-id="3f11c-115">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="3f11c-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3f11c-116">如果未指定，則會使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。</span><span class="sxs-lookup"><span data-stu-id="3f11c-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3f11c-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3f11c-117">ForceEnglishOutput</span></span> | <span data-ttu-id="3f11c-118">*（3.5 +）* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="3f11c-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3f11c-119">說明</span><span class="sxs-lookup"><span data-stu-id="3f11c-119">Help</span></span> | <span data-ttu-id="3f11c-120">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="3f11c-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="3f11c-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3f11c-121">NonInteractive</span></span> | <span data-ttu-id="3f11c-122">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="3f11c-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3f11c-123">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="3f11c-123">Verbosity</span></span> | <span data-ttu-id="3f11c-124">指定輸出中顯示的詳細資料量： [*一般*] *、[* 無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="3f11c-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3f11c-125">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3f11c-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3f11c-126">範例</span><span class="sxs-lookup"><span data-stu-id="3f11c-126">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
