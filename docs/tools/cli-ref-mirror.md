---
title: NuGet CLI 鏡像命令
description: Nuget.exe 鏡像命令參考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4cec854f05fcd207bb15a50ea4ebdc201fdb3ac6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818148"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="7fe3e-103">mirror 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7fe3e-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="7fe3e-104">**適用於：** 封裝發行&bullet;**支援的版本：** 3.2 + 中已被取代</span><span class="sxs-lookup"><span data-stu-id="7fe3e-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="7fe3e-105">反映封裝及其相依性從指定的來源儲存機制的目標儲存機制。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="7fe3e-106">若要啟用此命令的 NuGet 版本 3.2 之前，請移至[ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)、 選取最新穩定版本，請下載`NuGet.ServerExtensions.dll`和`Nuget-Signed.exe`您的本機磁碟和重新命名`Nuget-Signed.exe`至`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="7fe3e-107">使用量</span><span class="sxs-lookup"><span data-stu-id="7fe3e-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="7fe3e-108">其中`<packageID>`是要建立鏡像的封裝或`<configFilePath>`識別`packages.config`檔案，其中列出要鏡像的封裝。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="7fe3e-109">`<listUrlTarget>`指定來源儲存機制和`<publishUrlTarget>`指定目標存放庫。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="7fe3e-110">如果您的目標儲存機制位於`https://machine/repo`執行[NuGet.Server](../hosting-packages/nuget-server.md)，清單並推送 url 就是`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`分別。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="7fe3e-111">選項</span><span class="sxs-lookup"><span data-stu-id="7fe3e-111">Options</span></span>

| <span data-ttu-id="7fe3e-112">選項</span><span class="sxs-lookup"><span data-stu-id="7fe3e-112">Option</span></span> | <span data-ttu-id="7fe3e-113">描述</span><span class="sxs-lookup"><span data-stu-id="7fe3e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7fe3e-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="7fe3e-114">ApiKey</span></span> | <span data-ttu-id="7fe3e-115">目標存放庫 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-115">The API key for the target repository.</span></span> <span data-ttu-id="7fe3e-116">如果不存在，指定在組態檔中會使用 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux))。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="7fe3e-117">說明</span><span class="sxs-lookup"><span data-stu-id="7fe3e-117">Help</span></span> | <span data-ttu-id="7fe3e-118">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="7fe3e-119">無快取記憶體</span><span class="sxs-lookup"><span data-stu-id="7fe3e-119">NoCache</span></span> | <span data-ttu-id="7fe3e-120">NuGet 可防止使用快取的封裝。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="7fe3e-121">請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="7fe3e-122">Noop</span><span class="sxs-lookup"><span data-stu-id="7fe3e-122">Noop</span></span> | <span data-ttu-id="7fe3e-123">記錄項目會完成，但不會執行動作。假設推送作業成功。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="7fe3e-124">發行前版本</span><span class="sxs-lookup"><span data-stu-id="7fe3e-124">PreRelease</span></span> | <span data-ttu-id="7fe3e-125">鏡像作業中包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="7fe3e-126">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="7fe3e-126">Source</span></span> | <span data-ttu-id="7fe3e-127">要鏡像的封裝來源清單。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-127">A list of package sources to mirror.</span></span> <span data-ttu-id="7fe3e-128">如果未不指定任何來源中, 定義的組態檔 （請參閱上述 ApiKey） 使用，如果未指定任何 nuget.org 預設值。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="7fe3e-129">等候逾時</span><span class="sxs-lookup"><span data-stu-id="7fe3e-129">Timeout</span></span> | <span data-ttu-id="7fe3e-130">指定在逾時，以秒為單位，可用於推入到伺服器。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="7fe3e-131">預設值是 300 秒 （5 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="7fe3e-132">版本</span><span class="sxs-lookup"><span data-stu-id="7fe3e-132">Version</span></span> | <span data-ttu-id="7fe3e-133">要安裝之封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-133">The version of the package to install.</span></span> <span data-ttu-id="7fe3e-134">如果未指定，則會鏡像的最新版本。</span><span class="sxs-lookup"><span data-stu-id="7fe3e-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="7fe3e-135">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7fe3e-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7fe3e-136">範例</span><span class="sxs-lookup"><span data-stu-id="7fe3e-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
