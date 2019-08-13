---
title: NuGet CLI 鏡像命令
description: Nuget.exe 鏡像命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959716"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="c750d-103">mirror 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c750d-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="c750d-104">**適用于:** 套件發行&bullet; **支援的版本:** 3.2 + 中已淘汰</span><span class="sxs-lookup"><span data-stu-id="c750d-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="c750d-105">將封裝及其相依性從指定的來源存放庫鏡像到目標儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c750d-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="c750d-106">先前在 NuGet 2.x 中支援此命令的 ServerExtensions .dll 和 NuGet-Signed (藉由將 NuGet-Signed 重新命名為 nuget.exe) 已不再提供下載。</span><span class="sxs-lookup"><span data-stu-id="c750d-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="c750d-107">若要使用類似的命令, 請嘗試[NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)。</span><span class="sxs-lookup"><span data-stu-id="c750d-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="c750d-108">使用量</span><span class="sxs-lookup"><span data-stu-id="c750d-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="c750d-109">其中`<packageID>`是要鏡像的封裝, 或`<configFilePath>`識別`packages.config`列出要鏡像之封裝的檔案。</span><span class="sxs-lookup"><span data-stu-id="c750d-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="c750d-110">會指定來源存放庫, 並`<publishUrlTarget>`指定目標存放庫。 `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="c750d-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="c750d-111">如果您的目標存放庫`https://machine/repo`是在執行[nuget.exe](../../hosting-packages/nuget-server.md)的上, 則清單和推播 url 會`https://machine/repo/nuget`分別`https://machine/repo/api/v2/package`是和。</span><span class="sxs-lookup"><span data-stu-id="c750d-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c750d-112">選項</span><span class="sxs-lookup"><span data-stu-id="c750d-112">Options</span></span>

| <span data-ttu-id="c750d-113">選項</span><span class="sxs-lookup"><span data-stu-id="c750d-113">Option</span></span> | <span data-ttu-id="c750d-114">說明</span><span class="sxs-lookup"><span data-stu-id="c750d-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c750d-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="c750d-115">ApiKey</span></span> | <span data-ttu-id="c750d-116">目標存放庫的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c750d-116">The API key for the target repository.</span></span> <span data-ttu-id="c750d-117">如果不存在, 則會使用設定檔中指定的檔案 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux))。</span><span class="sxs-lookup"><span data-stu-id="c750d-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="c750d-118">Help</span><span class="sxs-lookup"><span data-stu-id="c750d-118">Help</span></span> | <span data-ttu-id="c750d-119">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="c750d-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="c750d-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="c750d-120">NoCache</span></span> | <span data-ttu-id="c750d-121">防止 NuGet 使用快取的套件。</span><span class="sxs-lookup"><span data-stu-id="c750d-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="c750d-122">請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="c750d-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="c750d-123">Noop</span><span class="sxs-lookup"><span data-stu-id="c750d-123">Noop</span></span> | <span data-ttu-id="c750d-124">記錄哪些作業會完成, 但不會執行動作;假設推送作業成功。</span><span class="sxs-lookup"><span data-stu-id="c750d-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="c750d-125">版</span><span class="sxs-lookup"><span data-stu-id="c750d-125">PreRelease</span></span> | <span data-ttu-id="c750d-126">包括鏡像作業中的發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="c750d-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="c750d-127">Source</span><span class="sxs-lookup"><span data-stu-id="c750d-127">Source</span></span> | <span data-ttu-id="c750d-128">要鏡像的封裝來源清單。</span><span class="sxs-lookup"><span data-stu-id="c750d-128">A list of package sources to mirror.</span></span> <span data-ttu-id="c750d-129">如果未指定任何來源, 則會使用設定檔中所定義的來源 (如上面的 ApiKey), 預設為 nuget.org (如果未指定)。</span><span class="sxs-lookup"><span data-stu-id="c750d-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="c750d-130">逾時</span><span class="sxs-lookup"><span data-stu-id="c750d-130">Timeout</span></span> | <span data-ttu-id="c750d-131">指定推送至伺服器的超時時間 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="c750d-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="c750d-132">預設值為300秒 (5 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="c750d-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="c750d-133">版本</span><span class="sxs-lookup"><span data-stu-id="c750d-133">Version</span></span> | <span data-ttu-id="c750d-134">要安裝的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="c750d-134">The version of the package to install.</span></span> <span data-ttu-id="c750d-135">如果未指定, 則會鏡像最新版本。</span><span class="sxs-lookup"><span data-stu-id="c750d-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="c750d-136">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c750d-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c750d-137">範例</span><span class="sxs-lookup"><span data-stu-id="c750d-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
