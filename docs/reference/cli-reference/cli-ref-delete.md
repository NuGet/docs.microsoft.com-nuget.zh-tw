---
title: NuGet CLI delete 命令
description: Nuget.exe delete 命令的參考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327835"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="9884d-103">delete 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9884d-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="9884d-104">**適用于:** 套件發行&bullet; **支援的版本:** 全部</span><span class="sxs-lookup"><span data-stu-id="9884d-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="9884d-105">從封裝來源刪除或取消列出封裝。</span><span class="sxs-lookup"><span data-stu-id="9884d-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="9884d-106">針對 nuget.org, delete 命令會[取消列出套件](../../nuget-org/policies/deleting-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="9884d-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="9884d-107">使用量</span><span class="sxs-lookup"><span data-stu-id="9884d-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="9884d-108">其中`<packageID>` , `<packageVersion>`和會識別要刪除或取消列出的確切封裝。</span><span class="sxs-lookup"><span data-stu-id="9884d-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="9884d-109">確切的行為視來源而定。</span><span class="sxs-lookup"><span data-stu-id="9884d-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="9884d-110">例如, 針對本機資料夾, 會刪除封裝;針對 nuget.org, 封裝為未列出。</span><span class="sxs-lookup"><span data-stu-id="9884d-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="9884d-111">選項</span><span class="sxs-lookup"><span data-stu-id="9884d-111">Options</span></span>

| <span data-ttu-id="9884d-112">選項</span><span class="sxs-lookup"><span data-stu-id="9884d-112">Option</span></span> | <span data-ttu-id="9884d-113">說明</span><span class="sxs-lookup"><span data-stu-id="9884d-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9884d-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="9884d-114">ApiKey</span></span> | <span data-ttu-id="9884d-115">目標存放庫的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="9884d-115">The API key for the target repository.</span></span> <span data-ttu-id="9884d-116">如果不存在, 則會使用設定檔中指定的檔案。</span><span class="sxs-lookup"><span data-stu-id="9884d-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="9884d-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9884d-117">ConfigFile</span></span> | <span data-ttu-id="9884d-118">要套用的 NuGet 設定檔。</span><span class="sxs-lookup"><span data-stu-id="9884d-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9884d-119">如果未指定, `%AppData%\NuGet\NuGet.Config`則會使用 ( `~/.nuget/NuGet/NuGet.Config` Windows) 或 (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="9884d-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9884d-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9884d-120">ForceEnglishOutput</span></span> | <span data-ttu-id="9884d-121">*(3.5 +)* 強制使用非變異的英文文化特性來執行 nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="9884d-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9884d-122">Help</span><span class="sxs-lookup"><span data-stu-id="9884d-122">Help</span></span> | <span data-ttu-id="9884d-123">顯示命令的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="9884d-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="9884d-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="9884d-124">NonInteractive</span></span> | <span data-ttu-id="9884d-125">抑制使用者輸入或確認的提示。</span><span class="sxs-lookup"><span data-stu-id="9884d-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9884d-126">Source</span><span class="sxs-lookup"><span data-stu-id="9884d-126">Source</span></span> | <span data-ttu-id="9884d-127">指定伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="9884d-127">Specifies the server URL.</span></span> <span data-ttu-id="9884d-128">Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="9884d-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="9884d-129">若是私人摘要, 請以主機名稱取代, 例如 *% hostname%/api/v3*。</span><span class="sxs-lookup"><span data-stu-id="9884d-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="9884d-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="9884d-130">Verbosity</span></span> | <span data-ttu-id="9884d-131">指定輸出中顯示的詳細資料量: [*一般*]  、[無訊息]、[*詳細*]。</span><span class="sxs-lookup"><span data-stu-id="9884d-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9884d-132">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9884d-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9884d-133">範例</span><span class="sxs-lookup"><span data-stu-id="9884d-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
