---
title: NuGet CLI delete 命令
description: Nuget.exe delete 命令的參考
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="eda22-103">delete 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="eda22-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="eda22-104">**適用於：**封裝發行&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="eda22-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="eda22-105">刪除或 unlists 從套件來源的封裝。</span><span class="sxs-lookup"><span data-stu-id="eda22-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="eda22-106">為 delete 命令，nuget.org [unlists 封裝](../policies/deleting-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="eda22-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="eda22-107">使用量</span><span class="sxs-lookup"><span data-stu-id="eda22-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="eda22-108">其中`<packageID>`和`<packageVersion>`識別要刪除或 unlist 確切的封裝。</span><span class="sxs-lookup"><span data-stu-id="eda22-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="eda22-109">確切行為取決於來源。</span><span class="sxs-lookup"><span data-stu-id="eda22-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="eda22-110">針對本機資料夾，例如，已經刪除套件;nuget.org 的封裝未列出。</span><span class="sxs-lookup"><span data-stu-id="eda22-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="eda22-111">選項</span><span class="sxs-lookup"><span data-stu-id="eda22-111">Options</span></span>

| <span data-ttu-id="eda22-112">選項</span><span class="sxs-lookup"><span data-stu-id="eda22-112">Option</span></span> | <span data-ttu-id="eda22-113">描述</span><span class="sxs-lookup"><span data-stu-id="eda22-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eda22-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="eda22-114">ApiKey</span></span> | <span data-ttu-id="eda22-115">目標存放庫 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="eda22-115">The API key for the target repository.</span></span> <span data-ttu-id="eda22-116">如果不存在，則會使用組態檔中所指定。</span><span class="sxs-lookup"><span data-stu-id="eda22-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="eda22-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="eda22-117">ConfigFile</span></span> | <span data-ttu-id="eda22-118">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="eda22-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="eda22-119">如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 會使用。</span><span class="sxs-lookup"><span data-stu-id="eda22-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="eda22-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="eda22-120">ForceEnglishOutput</span></span> | <span data-ttu-id="eda22-121">*（3.5 +)* 強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="eda22-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="eda22-122">說明</span><span class="sxs-lookup"><span data-stu-id="eda22-122">Help</span></span> | <span data-ttu-id="eda22-123">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="eda22-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="eda22-124">非互動式</span><span class="sxs-lookup"><span data-stu-id="eda22-124">NonInteractive</span></span> | <span data-ttu-id="eda22-125">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="eda22-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="eda22-126">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="eda22-126">Source</span></span> | <span data-ttu-id="eda22-127">指定伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="eda22-127">Specifies the server URL.</span></span> <span data-ttu-id="eda22-128">Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="eda22-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="eda22-129">私用的摘要，替代的主機名稱，例如 *%hostname%/api/v3*。</span><span class="sxs-lookup"><span data-stu-id="eda22-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="eda22-130">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="eda22-130">Verbosity</span></span> | <span data-ttu-id="eda22-131">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="eda22-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="eda22-132">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="eda22-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="eda22-133">範例</span><span class="sxs-lookup"><span data-stu-id="eda22-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
