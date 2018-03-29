---
title: NuGet CLI 鏡像命令 |Microsoft 文件
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 鏡像命令參考
keywords: nuget 鏡像參考，鏡像命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 512bd72d568cda81eb7c6a1555c36ead66b5c438
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="c94a4-104">鏡像命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c94a4-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="c94a4-105">**適用於：**封裝發行&bullet;**支援的版本：** 3.2 + 中已被取代</span><span class="sxs-lookup"><span data-stu-id="c94a4-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="c94a4-106">反映封裝及其相依性從指定的來源儲存機制的目標儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c94a4-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="c94a4-107">若要啟用此命令的 NuGet 版本 3.2 之前，請移至[ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)、 選取最新穩定版本，請下載`NuGet.ServerExtensions.dll`和`Nuget-Signed.exe`您的本機磁碟和重新命名`Nuget-Signed.exe`至`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="c94a4-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="c94a4-108">使用量</span><span class="sxs-lookup"><span data-stu-id="c94a4-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="c94a4-109">其中`<packageID>`是要建立鏡像的封裝或`<configFilePath>`識別`packages.config`檔案，其中列出要鏡像的封裝。</span><span class="sxs-lookup"><span data-stu-id="c94a4-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="c94a4-110">`<listUrlTarget>`指定來源儲存機制和`<publishUrlTarget>`指定目標存放庫。</span><span class="sxs-lookup"><span data-stu-id="c94a4-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="c94a4-111">如果您的目標儲存機制位於`https://machine/repo`執行[NuGet.Server](../hosting-packages/nuget-server.md)，清單並推送 url 就是`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`分別。</span><span class="sxs-lookup"><span data-stu-id="c94a4-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c94a4-112">選項</span><span class="sxs-lookup"><span data-stu-id="c94a4-112">Options</span></span>

| <span data-ttu-id="c94a4-113">選項</span><span class="sxs-lookup"><span data-stu-id="c94a4-113">Option</span></span> | <span data-ttu-id="c94a4-114">描述</span><span class="sxs-lookup"><span data-stu-id="c94a4-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c94a4-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="c94a4-115">ApiKey</span></span> | <span data-ttu-id="c94a4-116">目標存放庫 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c94a4-116">The API key for the target repository.</span></span> <span data-ttu-id="c94a4-117">如果不存在，指定在組態檔中會使用 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux))。</span><span class="sxs-lookup"><span data-stu-id="c94a4-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="c94a4-118">說明</span><span class="sxs-lookup"><span data-stu-id="c94a4-118">Help</span></span> | <span data-ttu-id="c94a4-119">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="c94a4-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="c94a4-120">無快取記憶體</span><span class="sxs-lookup"><span data-stu-id="c94a4-120">NoCache</span></span> | <span data-ttu-id="c94a4-121">NuGet 可防止使用快取的封裝。</span><span class="sxs-lookup"><span data-stu-id="c94a4-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="c94a4-122">請參閱[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)。</span><span class="sxs-lookup"><span data-stu-id="c94a4-122">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="c94a4-123">Noop</span><span class="sxs-lookup"><span data-stu-id="c94a4-123">Noop</span></span> | <span data-ttu-id="c94a4-124">記錄項目會完成，但不會執行動作。假設推送作業成功。</span><span class="sxs-lookup"><span data-stu-id="c94a4-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="c94a4-125">發行前版本</span><span class="sxs-lookup"><span data-stu-id="c94a4-125">PreRelease</span></span> | <span data-ttu-id="c94a4-126">鏡像作業中包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="c94a4-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="c94a4-127">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="c94a4-127">Source</span></span> | <span data-ttu-id="c94a4-128">要鏡像的封裝來源清單。</span><span class="sxs-lookup"><span data-stu-id="c94a4-128">A list of package sources to mirror.</span></span> <span data-ttu-id="c94a4-129">如果未不指定任何來源中, 定義的組態檔 （請參閱上述 ApiKey） 使用，如果未指定任何 nuget.org 預設值。</span><span class="sxs-lookup"><span data-stu-id="c94a4-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="c94a4-130">等候逾時</span><span class="sxs-lookup"><span data-stu-id="c94a4-130">Timeout</span></span> | <span data-ttu-id="c94a4-131">指定在逾時，以秒為單位，可用於推入到伺服器。</span><span class="sxs-lookup"><span data-stu-id="c94a4-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="c94a4-132">預設值是 300 秒 （5 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="c94a4-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="c94a4-133">版本</span><span class="sxs-lookup"><span data-stu-id="c94a4-133">Version</span></span> | <span data-ttu-id="c94a4-134">要安裝之封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="c94a4-134">The version of the package to install.</span></span> <span data-ttu-id="c94a4-135">如果未指定，則會鏡像的最新版本。</span><span class="sxs-lookup"><span data-stu-id="c94a4-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="c94a4-136">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c94a4-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c94a4-137">範例</span><span class="sxs-lookup"><span data-stu-id="c94a4-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
