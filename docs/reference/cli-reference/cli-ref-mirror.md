---
title: NuGet CLI 鏡像命令
description: nuget.exe 鏡像命令的參考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779178"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="0d2de-103">NuGet CLI (的鏡像命令) </span><span class="sxs-lookup"><span data-stu-id="0d2de-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="0d2de-104">**適用于：** 套件發行 &bullet; **支援的版本：** 已在 3.2 + 中淘汰</span><span class="sxs-lookup"><span data-stu-id="0d2de-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="0d2de-105">將封裝及其相依性從指定的來源存放庫鏡像至目標存放庫。</span><span class="sxs-lookup"><span data-stu-id="0d2de-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="0d2de-106">先前在 NuGet 2.x (中支援這個命令 NuGet.ServerExtensions.dll 和 NuGet-Signed.exe 將無法再重新命名 NuGet-Signed.exe 至 nuget.exe) 。</span><span class="sxs-lookup"><span data-stu-id="0d2de-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="0d2de-107">若要使用類似的命令，請嘗試 [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)。</span><span class="sxs-lookup"><span data-stu-id="0d2de-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="0d2de-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="0d2de-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="0d2de-109">其中 `<packageID>` 是要鏡像的封裝，或 `<configFilePath>` 識別 `packages.config` 列出要鏡像之套件的檔案。</span><span class="sxs-lookup"><span data-stu-id="0d2de-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="0d2de-110">會 `<listUrlTarget>` 指定來源存放庫，並 `<publishUrlTarget>` 指定目標存放庫。</span><span class="sxs-lookup"><span data-stu-id="0d2de-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="0d2de-111">如果您的目標儲存機制是在執行 `https://machine/repo` [nuget.exe](../../hosting-packages/nuget-server.md)的電腦上，則清單和推送 url 會 `https://machine/repo/nuget` 分別為和 `https://machine/repo/api/v2/package` 。</span><span class="sxs-lookup"><span data-stu-id="0d2de-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="0d2de-112">選項。</span><span class="sxs-lookup"><span data-stu-id="0d2de-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="0d2de-113">目標儲存機制的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d2de-113">The API key for the target repository.</span></span> <span data-ttu-id="0d2de-114">如果不存在，則會使用設定檔中指定的 (`%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) # A5。</span><span class="sxs-lookup"><span data-stu-id="0d2de-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="0d2de-115">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="0d2de-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="0d2de-116">防止 NuGet 使用快取的封裝。</span><span class="sxs-lookup"><span data-stu-id="0d2de-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="0d2de-117">請參閱 [管理全域封裝和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="0d2de-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="0d2de-118">記錄會執行的動作，但不會執行動作。假設推送作業成功。</span><span class="sxs-lookup"><span data-stu-id="0d2de-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="0d2de-119">在鏡像作業中包含發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="0d2de-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="0d2de-120">要鏡像的封裝來源清單。</span><span class="sxs-lookup"><span data-stu-id="0d2de-120">A list of package sources to mirror.</span></span> <span data-ttu-id="0d2de-121">如果未指定任何來源，則會使用在設定檔中定義的 ApiKey， (查看上述) ，如果未指定，則預設為 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="0d2de-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="0d2de-122">指定推送至伺服器的超時時間（以秒為單位）。</span><span class="sxs-lookup"><span data-stu-id="0d2de-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="0d2de-123">預設值是 300 秒 (5 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="0d2de-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="0d2de-124">要安裝之套件的版本。</span><span class="sxs-lookup"><span data-stu-id="0d2de-124">The version of the package to install.</span></span> <span data-ttu-id="0d2de-125">如果未指定，則會鏡像最新版本。</span><span class="sxs-lookup"><span data-stu-id="0d2de-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="0d2de-126">另請參閱 [環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0d2de-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0d2de-127">範例</span><span class="sxs-lookup"><span data-stu-id="0d2de-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
