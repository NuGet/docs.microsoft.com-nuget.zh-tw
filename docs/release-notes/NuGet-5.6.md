---
title: NuGet 5.6 版本資訊
description: NuGet 5.6 的版本資訊，包括新功能、bug 修正和 Dcr。
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727818"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="e2525-103">NuGet 5.6 版本資訊</span><span class="sxs-lookup"><span data-stu-id="e2525-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="e2525-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="e2525-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="e2525-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="e2525-105">NuGet version</span></span> | <span data-ttu-id="e2525-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="e2525-106">Available in Visual Studio version</span></span>| <span data-ttu-id="e2525-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e2525-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="e2525-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="e2525-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e2525-109">Visual Studio 2019 16.6 版</span><span class="sxs-lookup"><span data-stu-id="e2525-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e2525-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="e2525-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="e2525-111"><sup>1</sup>以含 .NET Core 工作負載的 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="e2525-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="e2525-112">摘要：5.6 中的新功能</span><span class="sxs-lookup"><span data-stu-id="e2525-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="e2525-113">支援具有浮動版本的發行前版本套件。</span><span class="sxs-lookup"><span data-stu-id="e2525-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="e2525-114">`Version="*-*"`、 `Version="1.*-*"` 和類似的浮動到最新版本，包括發行前版本（在指定的範圍內） [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="e2525-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="e2525-115">此版本所修正的問題</span><span class="sxs-lookup"><span data-stu-id="e2525-115">Issues fixed in this release</span></span>

<span data-ttu-id="e2525-116">**存在**</span><span class="sxs-lookup"><span data-stu-id="e2525-116">**Bugs:**</span></span>

* <span data-ttu-id="e2525-117">`nuget push *.nupkg`當 .snupkg 不存在時失敗- [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="e2525-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="e2525-118">Pack 和其他幾個程式碼路徑會因地區設定而失敗。</span><span class="sxs-lookup"><span data-stu-id="e2525-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="e2525-119">使用 System.text.regularexpressions.RegExoptions. Regexoptions.cultureinvariant- [#8246](https://github.com/NuGet/Home/issues/8246)</span><span class="sxs-lookup"><span data-stu-id="e2525-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="e2525-120">效能：卸載專案案例的 DG 規格不應以預覽還原撰寫- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="e2525-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="e2525-121">還原：藉由快取解決方案相依性圖形規格來改善效能[#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="e2525-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="e2525-122">PM UI 在使用 PM 主控台安裝套件之後，不適用於 SDK 樣式專案- [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="e2525-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="e2525-123">在 PM UI 中，無法以本機套件摘要顯示內嵌圖示-取決於/vs-- [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="e2525-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="e2525-124">NuGetVersion. TryParseStrict （）如果無法剖析，則應該傳回 false [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="e2525-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="e2525-125">`nuget.exe push`的說明 `-source` 應建議使用來源名稱，而不是來源 URL- [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="e2525-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="e2525-126">`dotnet nuget add package SourceUri`建立錯誤的預設封裝來源名稱- [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="e2525-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="e2525-127">螢幕閱讀程式未公告「搜尋 ...」切換索引標籤時的訊息- [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="e2525-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="e2525-128">協助工具：焦點矩形色彩無法以深色主題的 UI 索引標籤存取- [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="e2525-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="e2525-129">nuget.exe 5.5 無法使用 MSBuild 14 或以下的還原- [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="e2525-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="e2525-130">不要在還原訊息中記錄毫秒時間- [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="e2525-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="e2525-131">使 IOutputConsole 非同步[#9268](https://github.com/NuGet/Home/issues/9268)</span><span class="sxs-lookup"><span data-stu-id="e2525-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="e2525-132">MSBuild 版本挑選在某些非英文文化特性上運作不佳- [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="e2525-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="e2525-133">#9337 上的預設遺漏格式 `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="e2525-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="e2525-134">效能： RestoreOperationLogger 具有不必要的執行緒親和性- [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="e2525-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="e2525-135">自動建立命令的檔 `dotnet nuget` - [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="e2525-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="e2525-136">預設詳細資訊不應報告每個專案的 noop 還原- [#8792](https://github.com/NuGet/Home/issues/8792)</span><span class="sxs-lookup"><span data-stu-id="e2525-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="e2525-137">`-DependencyVersion`的支援參數 `NuGet.exe update` ，類似于 install command- [#7694](https://github.com/NuGet/Home/issues/7694)</span><span class="sxs-lookup"><span data-stu-id="e2525-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="e2525-138">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="e2525-138">**DCRs:**</span></span>

* <span data-ttu-id="e2525-139">新增 net 5.0 目標架構的初始支援- [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="e2525-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="e2525-140">在 PM UI 的 [更新] 索引標籤中依識別碼排序套件- [#9278](https://github.com/NuGet/Home/issues/9278)</span><span class="sxs-lookup"><span data-stu-id="e2525-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="e2525-141">**[此版本中已修正的所有問題清單-5。6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="e2525-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
