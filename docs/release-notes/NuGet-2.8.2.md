---
title: NuGet 2.8.2 版本資訊
description: 版本資訊 NuGet 2.8.2 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551144"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="6acb7-103">NuGet 2.8.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="6acb7-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="6acb7-104">[NuGet 2.8.1 版本資訊](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 版本資訊](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="6acb7-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="6acb7-105">NuGet 2.8.2 已於 2014 5 月 22 日發行。</span><span class="sxs-lookup"><span data-stu-id="6acb7-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="6acb7-106">此版本只包含變更 nuget.exe 命令列、 NuGet.Server 套件以及其他 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="6acb7-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="6acb7-107">更新 Visual Studio 擴充功能或 WebMatrix 延伸模組未包含版本。</span><span class="sxs-lookup"><span data-stu-id="6acb7-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="6acb7-108">值得注意的更新</span><span class="sxs-lookup"><span data-stu-id="6acb7-108">Notable Updates</span></span>

<span data-ttu-id="6acb7-109">Nuget.exe 命令列和 NuGet.Server 套件 （適用於自我裝載的 NuGet 摘要） 中，是最值得注意的更新。</span><span class="sxs-lookup"><span data-stu-id="6acb7-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="6acb7-110">重要的 nuget.exe Bug 修正</span><span class="sxs-lookup"><span data-stu-id="6acb7-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="6acb7-111">nuget.exe 推送失敗，且會保留重試</span><span class="sxs-lookup"><span data-stu-id="6acb7-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="6acb7-112">nuget.exe 推送不會正確地傳送基本驗證認證</span><span class="sxs-lookup"><span data-stu-id="6acb7-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="6acb7-113">nuget.exe 推送不會遵循暫時重新導向</span><span class="sxs-lookup"><span data-stu-id="6acb7-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="6acb7-114">NuGet.Server 重要 Bug 修正</span><span class="sxs-lookup"><span data-stu-id="6acb7-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="6acb7-115">錯誤的 IsAbsoluteLatestVersion NuGet.Server 所傳回的值</span><span class="sxs-lookup"><span data-stu-id="6acb7-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="6acb7-116">已更新封裝</span><span class="sxs-lookup"><span data-stu-id="6acb7-116">Packages Updated</span></span>

<span data-ttu-id="6acb7-117">為 NuGet 套件更新運送的 nuget.exe 命令列和 NuGet.Server 修正。</span><span class="sxs-lookup"><span data-stu-id="6acb7-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="6acb7-118">沒有其他使用 2.8.2 也已更新的封裝。</span><span class="sxs-lookup"><span data-stu-id="6acb7-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="6acb7-119">以下是更新的套件清單：</span><span class="sxs-lookup"><span data-stu-id="6acb7-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="6acb7-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="6acb7-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="6acb7-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="6acb7-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="6acb7-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="6acb7-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="6acb7-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="6acb7-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="6acb7-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) （封裝，不是延伸模組）</span><span class="sxs-lookup"><span data-stu-id="6acb7-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="6acb7-125">所有的變更</span><span class="sxs-lookup"><span data-stu-id="6acb7-125">All Changes</span></span>
<span data-ttu-id="6acb7-126">沒有 10 發行版本中已解決的問題。</span><span class="sxs-lookup"><span data-stu-id="6acb7-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="6acb7-127">如需完整的工作清單項目中已修正 NuGet 2.8.2，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="6acb7-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
