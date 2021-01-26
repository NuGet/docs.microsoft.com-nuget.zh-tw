---
title: NuGet CLI 刪除命令
description: nuget.exe delete 命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775953"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="56c01-103"> (NuGet CLI 刪除命令) </span><span class="sxs-lookup"><span data-stu-id="56c01-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="56c01-104">**適用于：** 套件發行 &bullet; **支援的版本：** 全部</span><span class="sxs-lookup"><span data-stu-id="56c01-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="56c01-105">從套件來源刪除或取消列出套件。</span><span class="sxs-lookup"><span data-stu-id="56c01-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="56c01-106">若為 nuget.org，delete 命令會 [取消列出封裝](../../nuget-org/policies/deleting-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="56c01-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="56c01-107">使用方式</span><span class="sxs-lookup"><span data-stu-id="56c01-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="56c01-108">， `<packageID>` 並 `<packageVersion>` 識別要刪除或取消列出的確切套件。</span><span class="sxs-lookup"><span data-stu-id="56c01-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="56c01-109">確切的行為取決於來源。</span><span class="sxs-lookup"><span data-stu-id="56c01-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="56c01-110">舉例來說，如果是本機資料夾，則會刪除封裝;若為 nuget.org，則不會列出套件。</span><span class="sxs-lookup"><span data-stu-id="56c01-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="56c01-111">選項。</span><span class="sxs-lookup"><span data-stu-id="56c01-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="56c01-112">目標儲存機制的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="56c01-112">The API key for the target repository.</span></span> <span data-ttu-id="56c01-113">如果不存在，則會使用設定檔中指定的。</span><span class="sxs-lookup"><span data-stu-id="56c01-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="56c01-114">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="56c01-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="56c01-115">如果未指定， `%AppData%\NuGet\NuGet.Config` 則會使用 (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。</span><span class="sxs-lookup"><span data-stu-id="56c01-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="56c01-116">*(3.5 +)* 使用不因文化特性而異的文化特性，強制執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="56c01-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="56c01-117">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="56c01-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="56c01-118">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="56c01-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="56c01-119">刪除時不要提示。</span><span class="sxs-lookup"><span data-stu-id="56c01-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="56c01-120">**`-NoServiceEndpoint`** 不會將 "api/v2/套件" 附加至來源 URL。</span><span class="sxs-lookup"><span data-stu-id="56c01-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="56c01-121">指定伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="56c01-121">Specifies the server URL.</span></span> <span data-ttu-id="56c01-122">Nuget.org 的 URL 是 `https://api.nuget.org/v3/index.json` 。</span><span class="sxs-lookup"><span data-stu-id="56c01-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="56c01-123">若為私用摘要，請取代主機名稱，例如 *% hostname%/api/v3*。</span><span class="sxs-lookup"><span data-stu-id="56c01-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="56c01-124">指定輸出中顯示的詳細資料量： `normal` (預設) 、 `quiet` 或 `detailed` 。</span><span class="sxs-lookup"><span data-stu-id="56c01-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="56c01-125">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="56c01-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="56c01-126">範例</span><span class="sxs-lookup"><span data-stu-id="56c01-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
