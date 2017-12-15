---
title: "NuGet 2.8.2 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "版本資訊包含 NuGet 2.8.2 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 2.8.2 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="aae36-104">NuGet 2.8.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="aae36-104">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="aae36-105">[NuGet 2.8.1 版本資訊](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 版本資訊](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="aae36-105">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="aae36-106">NuGet 2.8.2 已於 2014 年 22 日發行。</span><span class="sxs-lookup"><span data-stu-id="aae36-106">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="aae36-107">此版本僅包含變更 nuget.exe 命令列、 NuGet.Server 套件以及其他 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="aae36-107">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="aae36-108">更新 Visual Studio 擴充功能或 WebMatrix 的擴充功能未包含版本。</span><span class="sxs-lookup"><span data-stu-id="aae36-108">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="aae36-109">值得注意的更新</span><span class="sxs-lookup"><span data-stu-id="aae36-109">Notable Updates</span></span>

<span data-ttu-id="aae36-110">最值得注意的更新已在命令列 nuget.exe 和 NuGet.Server （適用於封裝自我裝載的 NuGet 摘要）。</span><span class="sxs-lookup"><span data-stu-id="aae36-110">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="aae36-111">重要 nuget.exe Bug 修正</span><span class="sxs-lookup"><span data-stu-id="aae36-111">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="aae36-112">nuget.exe 推送失敗，且會持續重試一次</span><span class="sxs-lookup"><span data-stu-id="aae36-112">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="aae36-113">nuget.exe 推送不會正確傳送基本驗證認證</span><span class="sxs-lookup"><span data-stu-id="aae36-113">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="aae36-114">nuget.exe 推送將不會遵循暫時重新導向</span><span class="sxs-lookup"><span data-stu-id="aae36-114">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="aae36-115">重要 NuGet.Server Bug 修正</span><span class="sxs-lookup"><span data-stu-id="aae36-115">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="aae36-116">IsAbsoluteLatestVersion NuGet.Server 所傳回的值錯誤</span><span class="sxs-lookup"><span data-stu-id="aae36-116">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="aae36-117">更新套件</span><span class="sxs-lookup"><span data-stu-id="aae36-117">Packages Updated</span></span>

<span data-ttu-id="aae36-118">Nuget.exe 命令列和 NuGet.Server 修正隨附做為 NuGet 套件的更新。</span><span class="sxs-lookup"><span data-stu-id="aae36-118">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="aae36-119">沒有更新 2.8.2 以及其他封裝。</span><span class="sxs-lookup"><span data-stu-id="aae36-119">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="aae36-120">以下是已更新封裝的清單：</span><span class="sxs-lookup"><span data-stu-id="aae36-120">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="aae36-121">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="aae36-121">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="aae36-122">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="aae36-122">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="aae36-123">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="aae36-123">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="aae36-124">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="aae36-124">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="aae36-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) （封裝、 非副檔名）</span><span class="sxs-lookup"><span data-stu-id="aae36-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="aae36-126">所有的變更</span><span class="sxs-lookup"><span data-stu-id="aae36-126">All Changes</span></span>
<span data-ttu-id="aae36-127">有一些 10 發行版本中解決的問題。</span><span class="sxs-lookup"><span data-stu-id="aae36-127">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="aae36-128">如需完整清單的工作項目固定在 NuGet 2.8.2，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="aae36-128">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
