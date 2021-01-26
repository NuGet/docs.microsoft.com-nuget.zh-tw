---
title: NuGet 2.8.2 版本資訊
description: NuGet 2.8.2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780375"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="81ad8-103">NuGet 2.8.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="81ad8-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="81ad8-104">[NuGet 2.8.1 版本](../release-notes/nuget-2.8.1.md)  |  資訊[NuGet 2.8.3 版本](../release-notes/nuget-2.8.3.md)資訊</span><span class="sxs-lookup"><span data-stu-id="81ad8-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="81ad8-105">已于2014年5月22日發行 NuGet 2.8.2。</span><span class="sxs-lookup"><span data-stu-id="81ad8-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="81ad8-106">此版本只包含 nuget.exe 命令列、NuGet. 伺服器套件和其他 NuGet 套件的變更。</span><span class="sxs-lookup"><span data-stu-id="81ad8-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="81ad8-107">版本不包含更新的 Visual Studio 延伸模組或 WebMatrix 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="81ad8-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="81ad8-108">值得注意的更新</span><span class="sxs-lookup"><span data-stu-id="81ad8-108">Notable Updates</span></span>

<span data-ttu-id="81ad8-109">最值得注意的更新是在 nuget.exe 命令列中，而 (適用于自我裝載 NuGet 摘要) 的 NuGet. 伺服器套件。</span><span class="sxs-lookup"><span data-stu-id="81ad8-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="81ad8-110">重要 nuget.exe 錯誤修正</span><span class="sxs-lookup"><span data-stu-id="81ad8-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="81ad8-111">nuget.exe 推送失敗並繼續重試</span><span class="sxs-lookup"><span data-stu-id="81ad8-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="81ad8-112">nuget.exe 推送不會正確傳送基本驗證認證</span><span class="sxs-lookup"><span data-stu-id="81ad8-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="81ad8-113">nuget.exe 推送不會遵循暫時重新導向</span><span class="sxs-lookup"><span data-stu-id="81ad8-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="81ad8-114">重要的 NuGet。伺服器錯誤修正</span><span class="sxs-lookup"><span data-stu-id="81ad8-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="81ad8-115">Nuget.exe 傳回的 IsAbsoluteLatestVersion 值錯誤。伺服器</span><span class="sxs-lookup"><span data-stu-id="81ad8-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="81ad8-116">更新的套件</span><span class="sxs-lookup"><span data-stu-id="81ad8-116">Packages Updated</span></span>

<span data-ttu-id="81ad8-117">nuget.exe 命令列和 NuGet. 伺服器修正會隨附于 NuGet 套件更新。</span><span class="sxs-lookup"><span data-stu-id="81ad8-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="81ad8-118">另外還有其他套件也會以2.8.2 更新。</span><span class="sxs-lookup"><span data-stu-id="81ad8-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="81ad8-119">以下是已更新的套件清單：</span><span class="sxs-lookup"><span data-stu-id="81ad8-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="81ad8-120">Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="81ad8-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="81ad8-121">Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="81ad8-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="81ad8-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="81ad8-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="81ad8-123">Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="81ad8-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="81ad8-124">[VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (套件，而不是延伸模組) </span><span class="sxs-lookup"><span data-stu-id="81ad8-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="81ad8-125">所有變更</span><span class="sxs-lookup"><span data-stu-id="81ad8-125">All Changes</span></span>
<span data-ttu-id="81ad8-126">發行中已解決10個問題。</span><span class="sxs-lookup"><span data-stu-id="81ad8-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="81ad8-127">如需 NuGet 2.8.2 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。</span><span class="sxs-lookup"><span data-stu-id="81ad8-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
