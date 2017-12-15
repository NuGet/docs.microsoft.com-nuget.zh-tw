---
title: "NuGet CLI 鏡像命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: "Nuget.exe 鏡像命令參考"
keywords: "nuget 鏡像參考，鏡像命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="d280a-104">鏡像命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d280a-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="d280a-105">**適用於：**封裝發行&bullet;**支援的版本：** 3.2 + 中已被取代</span><span class="sxs-lookup"><span data-stu-id="d280a-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="d280a-106">反映封裝及其相依性從指定的來源儲存機制的目標儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d280a-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="d280a-107">若要啟用此命令的 NuGet 版本 3.2 之前，請移至[https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)、 選取最新穩定版本，請下載`NuGet.ServerExtensions.dll`和`Nuget-Signed.exe`您的本機磁碟和重新命名`Nuget-Signed.exe`至`nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="d280a-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="d280a-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="d280a-108">Usage</span></span>

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="d280a-109">其中`<packageID>`是要建立鏡像的封裝或`<configFilePath>`識別`packages.config`檔案，其中列出要鏡像的封裝。</span><span class="sxs-lookup"><span data-stu-id="d280a-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="d280a-110">`<listUrlTarget>`指定來源儲存機制和`<publishUrlTarget>`指定目標存放庫。</span><span class="sxs-lookup"><span data-stu-id="d280a-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="d280a-111">如果您的目標儲存機制位於`https://machine/repo`執行[NuGet.Server](../hosting-packages/NuGet-Server.md)，清單並推送 url 就是`https://machine/repo/nuget`和`https://machine/repo/api/v2/package`分別。</span><span class="sxs-lookup"><span data-stu-id="d280a-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/NuGet-Server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="d280a-112">選項</span><span class="sxs-lookup"><span data-stu-id="d280a-112">Options</span></span>

| <span data-ttu-id="d280a-113">選項</span><span class="sxs-lookup"><span data-stu-id="d280a-113">Option</span></span> | <span data-ttu-id="d280a-114">說明</span><span class="sxs-lookup"><span data-stu-id="d280a-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d280a-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="d280a-115">ApiKey</span></span> | <span data-ttu-id="d280a-116">目標存放庫 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="d280a-116">The API key for the target repository.</span></span> <span data-ttu-id="d280a-117">如果不存在，在中指定一個*%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="d280a-117">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="d280a-118">說明</span><span class="sxs-lookup"><span data-stu-id="d280a-118">Help</span></span> | <span data-ttu-id="d280a-119">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="d280a-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="d280a-120">無快取記憶體</span><span class="sxs-lookup"><span data-stu-id="d280a-120">NoCache</span></span> | <span data-ttu-id="d280a-121">NuGet 可防止從本機電腦的快取使用的封裝。</span><span class="sxs-lookup"><span data-stu-id="d280a-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="d280a-122">Noop</span><span class="sxs-lookup"><span data-stu-id="d280a-122">Noop</span></span> | <span data-ttu-id="d280a-123">記錄項目會完成，但不會執行動作。假設推送作業成功。</span><span class="sxs-lookup"><span data-stu-id="d280a-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="d280a-124">發行前版本</span><span class="sxs-lookup"><span data-stu-id="d280a-124">PreRelease</span></span> | <span data-ttu-id="d280a-125">鏡像作業中包含套件發行前版本。</span><span class="sxs-lookup"><span data-stu-id="d280a-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="d280a-126">來源</span><span class="sxs-lookup"><span data-stu-id="d280a-126">Source</span></span> | <span data-ttu-id="d280a-127">要鏡像的封裝來源清單。</span><span class="sxs-lookup"><span data-stu-id="d280a-127">A list of package sources to mirror.</span></span> <span data-ttu-id="d280a-128">如果未不指定任何來源中, 定義的*%AppData%\NuGet\NuGet.Config*使用時，如果未指定任何 nuget.org 預設值。</span><span class="sxs-lookup"><span data-stu-id="d280a-128">If no sources are specified, the ones defined in *%AppData%\NuGet\NuGet.Config* are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="d280a-129">等候逾時</span><span class="sxs-lookup"><span data-stu-id="d280a-129">Timeout</span></span> | <span data-ttu-id="d280a-130">指定在逾時，以秒為單位，可用於推入到伺服器。</span><span class="sxs-lookup"><span data-stu-id="d280a-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="d280a-131">預設值是 300 秒 （5 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="d280a-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="d280a-132">版本</span><span class="sxs-lookup"><span data-stu-id="d280a-132">Version</span></span> | <span data-ttu-id="d280a-133">要安裝之封裝的版本。</span><span class="sxs-lookup"><span data-stu-id="d280a-133">The version of the package to install.</span></span> <span data-ttu-id="d280a-134">如果未指定，則會鏡像的最新版本。</span><span class="sxs-lookup"><span data-stu-id="d280a-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="d280a-135">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d280a-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d280a-136">範例</span><span class="sxs-lookup"><span data-stu-id="d280a-136">Examples</span></span>

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
