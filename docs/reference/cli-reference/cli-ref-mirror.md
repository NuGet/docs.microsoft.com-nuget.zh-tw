---
title: NuGet CLI 鏡像命令
description: Nuget.exe 鏡像命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327665"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="18801-103">mirror 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="18801-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="18801-104">**適用于:** 套件發行&bullet; **支援的版本:** 3.2 + 中已淘汰</span><span class="sxs-lookup"><span data-stu-id="18801-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="18801-105">將封裝及其相依性從指定的來源存放庫鏡像到目標儲存機制。</span><span class="sxs-lookup"><span data-stu-id="18801-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="18801-106">若要在3.2 之前的 NuGet 版本啟用此命令, [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)請移至, 選取最新的`NuGet.ServerExtensions.dll` 穩定`Nuget-Signed.exe` 版本, 將和下載到`Nuget-Signed.exe` 您`nuget.exe` 的本機磁片, 並將重新命名為。</span><span class="sxs-lookup"><span data-stu-id="18801-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="18801-107">使用量</span><span class="sxs-lookup"><span data-stu-id="18801-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="18801-108">其中`<packageID>`是要鏡像的封裝, 或`<configFilePath>`識別`packages.config`列出要鏡像之封裝的檔案。</span><span class="sxs-lookup"><span data-stu-id="18801-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="18801-109">會指定來源存放庫, 並`<publishUrlTarget>`指定目標存放庫。 `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="18801-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="18801-110">如果您的目標存放庫`https://machine/repo`是在執行[nuget.exe](../../hosting-packages/nuget-server.md)的上, 則清單和推播 url 會`https://machine/repo/nuget`分別`https://machine/repo/api/v2/package`是和。</span><span class="sxs-lookup"><span data-stu-id="18801-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="18801-111">選項</span><span class="sxs-lookup"><span data-stu-id="18801-111">Options</span></span>

| <span data-ttu-id="18801-112">選項</span><span class="sxs-lookup"><span data-stu-id="18801-112">Option</span></span> | <span data-ttu-id="18801-113">描述</span><span class="sxs-lookup"><span data-stu-id="18801-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="18801-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="18801-114">ApiKey</span></span> | <span data-ttu-id="18801-115">目標存放庫的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="18801-115">The API key for the target repository.</span></span> <span data-ttu-id="18801-116">如果不存在, 則會使用設定檔中指定的檔案 (`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config` (Mac/Linux))。</span><span class="sxs-lookup"><span data-stu-id="18801-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="18801-117">Help</span><span class="sxs-lookup"><span data-stu-id="18801-117">Help</span></span> | <span data-ttu-id="18801-118">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="18801-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="18801-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="18801-119">NoCache</span></span> | <span data-ttu-id="18801-120">防止 NuGet 使用快取的套件。</span><span class="sxs-lookup"><span data-stu-id="18801-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="18801-121">請參閱[管理全域套件和](../../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="18801-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="18801-122">Noop</span><span class="sxs-lookup"><span data-stu-id="18801-122">Noop</span></span> | <span data-ttu-id="18801-123">記錄哪些作業會完成, 但不會執行動作;假設推送作業成功。</span><span class="sxs-lookup"><span data-stu-id="18801-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="18801-124">版</span><span class="sxs-lookup"><span data-stu-id="18801-124">PreRelease</span></span> | <span data-ttu-id="18801-125">包括鏡像作業中的發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="18801-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="18801-126">Source</span><span class="sxs-lookup"><span data-stu-id="18801-126">Source</span></span> | <span data-ttu-id="18801-127">要鏡像的封裝來源清單。</span><span class="sxs-lookup"><span data-stu-id="18801-127">A list of package sources to mirror.</span></span> <span data-ttu-id="18801-128">如果未指定任何來源, 則會使用設定檔中所定義的來源 (如上面的 ApiKey), 預設為 nuget.org (如果未指定)。</span><span class="sxs-lookup"><span data-stu-id="18801-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="18801-129">逾時</span><span class="sxs-lookup"><span data-stu-id="18801-129">Timeout</span></span> | <span data-ttu-id="18801-130">指定推送至伺服器的超時時間 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="18801-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="18801-131">預設值為300秒 (5 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="18801-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="18801-132">版本</span><span class="sxs-lookup"><span data-stu-id="18801-132">Version</span></span> | <span data-ttu-id="18801-133">要安裝的封裝版本。</span><span class="sxs-lookup"><span data-stu-id="18801-133">The version of the package to install.</span></span> <span data-ttu-id="18801-134">如果未指定, 則會鏡像最新版本。</span><span class="sxs-lookup"><span data-stu-id="18801-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="18801-135">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="18801-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="18801-136">範例</span><span class="sxs-lookup"><span data-stu-id="18801-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
