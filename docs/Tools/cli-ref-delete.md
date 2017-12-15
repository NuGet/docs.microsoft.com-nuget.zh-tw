---
title: "NuGet CLI delete 命令 |Microsoft 文件"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Nuget.exe delete 命令的參考"
keywords: "nuget 刪除參考，則刪除套件 命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="e8b11-104">delete 命令 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e8b11-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="e8b11-105">**適用於：**封裝發行&bullet;**支援的版本：**所有</span><span class="sxs-lookup"><span data-stu-id="e8b11-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e8b11-106">刪除或 unlists 從套件來源的封裝。</span><span class="sxs-lookup"><span data-stu-id="e8b11-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="e8b11-107">為 delete 命令，nuget.org [unlists 封裝](../policies/Deleting-Packages.md)。</span><span class="sxs-lookup"><span data-stu-id="e8b11-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="e8b11-108">使用方式</span><span class="sxs-lookup"><span data-stu-id="e8b11-108">Usage</span></span>

```
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="e8b11-109">其中`<packageID>`和`<packageVersion>`識別要刪除或 unlist 確切的封裝。</span><span class="sxs-lookup"><span data-stu-id="e8b11-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="e8b11-110">確切行為取決於來源。</span><span class="sxs-lookup"><span data-stu-id="e8b11-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="e8b11-111">針對本機資料夾，例如，已經刪除套件;nuget.org 的封裝未列出。</span><span class="sxs-lookup"><span data-stu-id="e8b11-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="e8b11-112">選項</span><span class="sxs-lookup"><span data-stu-id="e8b11-112">Options</span></span>

| <span data-ttu-id="e8b11-113">選項</span><span class="sxs-lookup"><span data-stu-id="e8b11-113">Option</span></span> | <span data-ttu-id="e8b11-114">說明</span><span class="sxs-lookup"><span data-stu-id="e8b11-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e8b11-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="e8b11-115">ApiKey</span></span> | <span data-ttu-id="e8b11-116">目標存放庫 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e8b11-116">The API key for the target repository.</span></span> <span data-ttu-id="e8b11-117">如果不存在，在中指定一個*%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="e8b11-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="e8b11-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e8b11-118">ConfigFile</span></span> | <span data-ttu-id="e8b11-119">*（2.5 +)* NuGet 組態檔來套用。</span><span class="sxs-lookup"><span data-stu-id="e8b11-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="e8b11-120">如果未指定， *%AppData%\NuGet\NuGet.Config*用。</span><span class="sxs-lookup"><span data-stu-id="e8b11-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="e8b11-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e8b11-121">ForceEnglishOutput</span></span> | <span data-ttu-id="e8b11-122">*（3.5 +)*強制 nuget.exe 使用不變，英文的文化特性來執行。</span><span class="sxs-lookup"><span data-stu-id="e8b11-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e8b11-123">說明</span><span class="sxs-lookup"><span data-stu-id="e8b11-123">Help</span></span> | <span data-ttu-id="e8b11-124">顯示說明命令的資訊。</span><span class="sxs-lookup"><span data-stu-id="e8b11-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="e8b11-125">非互動式</span><span class="sxs-lookup"><span data-stu-id="e8b11-125">NonInteractive</span></span> | <span data-ttu-id="e8b11-126">抑制使用者輸入或確認提示。</span><span class="sxs-lookup"><span data-stu-id="e8b11-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e8b11-127">來源</span><span class="sxs-lookup"><span data-stu-id="e8b11-127">Source</span></span> | <span data-ttu-id="e8b11-128">指定伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="e8b11-128">Specifies the server URL.</span></span> <span data-ttu-id="e8b11-129">Nuget.org 的 URL 是`https://api.nuget.org/v3/index.json`。</span><span class="sxs-lookup"><span data-stu-id="e8b11-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="e8b11-130">私用的摘要，替代的主機名稱，例如*%hostname%/api/v3*。</span><span class="sxs-lookup"><span data-stu-id="e8b11-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="e8b11-131">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="e8b11-131">Verbosity</span></span> | <span data-ttu-id="e8b11-132">指定在輸出中顯示詳細資料的數量：*正常*，*安靜*，*詳細 （2.5 +）*。</span><span class="sxs-lookup"><span data-stu-id="e8b11-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="e8b11-133">另請參閱[環境變數](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e8b11-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e8b11-134">範例</span><span class="sxs-lookup"><span data-stu-id="e8b11-134">Examples</span></span>

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
