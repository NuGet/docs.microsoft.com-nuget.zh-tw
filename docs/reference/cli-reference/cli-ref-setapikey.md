---
title: NuGet CLI setapikey 命令
description: nuget.exe setapikey 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622807"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="16a21-103"> (NuGet CLI 的 setapikey 命令) </span><span class="sxs-lookup"><span data-stu-id="16a21-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="16a21-104">**適用于：** 套件耗用量、發佈 &bullet; **支援的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="16a21-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="16a21-105">將指定的伺服器 URL 的 API 金鑰儲存在中 `NuGet.Config` ，如此一來，就不需要針對後續命令輸入它。</span><span class="sxs-lookup"><span data-stu-id="16a21-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="16a21-106">使用方式</span><span class="sxs-lookup"><span data-stu-id="16a21-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="16a21-107">`<source>`識別伺服器的位置，以及 `<key>` 要儲存的金鑰。</span><span class="sxs-lookup"><span data-stu-id="16a21-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="16a21-108">如果 `<source>` 省略，則會假設為 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="16a21-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="16a21-109">API 金鑰不會用來向私人摘要進行驗證。</span><span class="sxs-lookup"><span data-stu-id="16a21-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="16a21-110">請參閱[ `nuget sources` 命令](../cli-reference/cli-ref-sources.md)來管理用來驗證來源的認證。</span><span class="sxs-lookup"><span data-stu-id="16a21-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="16a21-111">您可以從個別的 NuGet 伺服器取得 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="16a21-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="16a21-112">若要建立和管理 nuget.org 的 >apikeys.cs，請參閱 [取得---api 金鑰](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span><span class="sxs-lookup"><span data-stu-id="16a21-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="16a21-113">選項。</span><span class="sxs-lookup"><span data-stu-id="16a21-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="16a21-114">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="16a21-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="16a21-115">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="16a21-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="16a21-116">\* (3.5 +) \* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="16a21-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="16a21-117">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="16a21-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="16a21-118">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="16a21-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="16a21-119">API 金鑰有效的伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="16a21-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="16a21-120">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="16a21-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="16a21-121">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="16a21-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="16a21-122">範例</span><span class="sxs-lookup"><span data-stu-id="16a21-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
