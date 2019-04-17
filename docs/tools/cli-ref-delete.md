---
title: NuGet CLI 刪除命令
description: Nuget.exe delete 命令參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548506"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="5a413-103">delete 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5a413-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="5a413-104">**適用於：** 封裝發行&bullet;**支援的版本：** 所有</span><span class="sxs-lookup"><span data-stu-id="5a413-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5a413-105">刪除或取消列出套件從套件來源。</span><span class="sxs-lookup"><span data-stu-id="5a413-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="5a413-106">對於 nuget.org，delete 命令[取消列出套件](../policies/deleting-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="5a413-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="5a413-107">使用量</span><span class="sxs-lookup"><span data-stu-id="5a413-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="5a413-108">何處`<packageID>`和`<packageVersion>`找出要刪除或取消列出確切的套件。</span><span class="sxs-lookup"><span data-stu-id="5a413-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="5a413-109">確切行為取決於來源。</span><span class="sxs-lookup"><span data-stu-id="5a413-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="5a413-110">對於本機資料夾，比方說，已經刪除套件;對於 nuget.org 的套件不會列出。</span><span class="sxs-lookup"><span data-stu-id="5a413-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="5a413-111">選項</span><span class="sxs-lookup"><span data-stu-id="5a413-111">Options</span></span>

| <span data-ttu-id="5a413-112">選項</span><span class="sxs-lookup"><span data-stu-id="5a413-112">Option</span></span> | <span data-ttu-id="5a413-113">描述</span><span class="sxs-lookup"><span data-stu-id="5a413-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5a413-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="5a413-114">ApiKey</span></span> | <span data-ttu-id="5a413-115">目標存放庫的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5a413-115">The API key for the target repository.</span></span> <span data-ttu-id="5a413-116">如果不存在，則會使用組態檔中所指定。</span><span class="sxs-lookup"><span data-stu-id="5a413-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="5a413-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5a413-117">ConfigFile</span></span> | <span data-ttu-id="5a413-118">若要套用 NuGet 組態檔。</span><span class="sxs-lookup"><span data-stu-id="5a413-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5a413-119">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`用 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="5a413-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5a413-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5a413-120">ForceEnglishOutput</span></span> | <span data-ttu-id="5a413-121">*（3.5 +)* 會強制執行使用的非變異的英文文化特性的 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="5a413-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5a413-122">Help</span><span class="sxs-lookup"><span data-stu-id="5a413-122">Help</span></span> | <span data-ttu-id="5a413-123">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="5a413-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="5a413-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5a413-124">NonInteractive</span></span> | <span data-ttu-id="5a413-125">隱藏提示使用者輸入或確認。</span><span class="sxs-lookup"><span data-stu-id="5a413-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5a413-126">Source</span><span class="sxs-lookup"><span data-stu-id="5a413-126">Source</span></span> | <span data-ttu-id="5a413-127">指定伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="5a413-127">Specifies the server URL.</span></span> <span data-ttu-id="5a413-128">Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="5a413-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="5a413-129">對於私用摘要，取代主機名稱，例如 *%hostname%/api/v3*。</span><span class="sxs-lookup"><span data-stu-id="5a413-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="5a413-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="5a413-130">Verbosity</span></span> | <span data-ttu-id="5a413-131">指定輸出中顯示的詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="5a413-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5a413-132">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5a413-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5a413-133">範例</span><span class="sxs-lookup"><span data-stu-id="5a413-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
