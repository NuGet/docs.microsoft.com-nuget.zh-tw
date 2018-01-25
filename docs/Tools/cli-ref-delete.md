---
title: "NuGet CLI delete 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe delete 命令的參考"
keywords: "nuget 刪除參考，則刪除套件 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3890e33ab0fc425e1c2ee39631ade57ea9b92bc9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="8f77f-104">delete 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8f77f-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="8f77f-105">**適用於：**封裝發行&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="8f77f-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8f77f-106">刪除或 unlists 從套件來源的封裝。</span><span class="sxs-lookup"><span data-stu-id="8f77f-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="8f77f-107">為 delete 命令，nuget.org [unlists 封裝](../policies/Deleting-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="8f77f-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8f77f-108">使用量</span><span class="sxs-lookup"><span data-stu-id="8f77f-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="8f77f-109">其中`<packageID>`和`<packageVersion>`識別要刪除或 unlist 確切的封裝。</span><span class="sxs-lookup"><span data-stu-id="8f77f-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="8f77f-110">確切行為取決於來源。</span><span class="sxs-lookup"><span data-stu-id="8f77f-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="8f77f-111">針對本機資料夾，例如，已經刪除套件;nuget.org 的封裝未列出。</span><span class="sxs-lookup"><span data-stu-id="8f77f-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="8f77f-112">選項</span><span class="sxs-lookup"><span data-stu-id="8f77f-112">Options</span></span>

| <span data-ttu-id="8f77f-113">選項</span><span class="sxs-lookup"><span data-stu-id="8f77f-113">Option</span></span> | <span data-ttu-id="8f77f-114">描述</span><span class="sxs-lookup"><span data-stu-id="8f77f-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f77f-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="8f77f-115">ApiKey</span></span> | <span data-ttu-id="8f77f-116">目標存放庫 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="8f77f-116">The API key for the target repository.</span></span> <span data-ttu-id="8f77f-117">如果不存在，在中指定一個*%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="8f77f-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="8f77f-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8f77f-118">ConfigFile</span></span> | <span data-ttu-id="8f77f-119">要套用的 NuGet 設定檔案。</span><span class="sxs-lookup"><span data-stu-id="8f77f-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8f77f-120">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="8f77f-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="8f77f-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8f77f-121">ForceEnglishOutput</span></span> | <span data-ttu-id="8f77f-122">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="8f77f-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8f77f-123">說明</span><span class="sxs-lookup"><span data-stu-id="8f77f-123">Help</span></span> | <span data-ttu-id="8f77f-124">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="8f77f-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="8f77f-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8f77f-125">NonInteractive</span></span> | <span data-ttu-id="8f77f-126">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="8f77f-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8f77f-127">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="8f77f-127">Source</span></span> | <span data-ttu-id="8f77f-128">指定伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="8f77f-128">Specifies the server URL.</span></span> <span data-ttu-id="8f77f-129">Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="8f77f-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="8f77f-130">私用的摘要，替代的主機名稱，例如*%hostname%/api/v3*。</span><span class="sxs-lookup"><span data-stu-id="8f77f-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="8f77f-131">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="8f77f-131">Verbosity</span></span> | <span data-ttu-id="8f77f-132">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細*。</span><span class="sxs-lookup"><span data-stu-id="8f77f-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8f77f-133">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8f77f-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8f77f-134">範例</span><span class="sxs-lookup"><span data-stu-id="8f77f-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
