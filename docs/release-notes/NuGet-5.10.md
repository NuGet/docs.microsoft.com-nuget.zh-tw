---
title: NuGet 5.10 版本資訊
description: NuGet 5.10 的版本資訊，包括新功能、bug 修正及 Dcr。
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356534"
---
# <a name="nuget-510-release-notes"></a><span data-ttu-id="39c75-103">NuGet 5.10 版本資訊</span><span class="sxs-lookup"><span data-stu-id="39c75-103">NuGet 5.10 Release Notes</span></span>

<span data-ttu-id="39c75-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="39c75-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="39c75-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="39c75-105">NuGet version</span></span> | <span data-ttu-id="39c75-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="39c75-106">Available in Visual Studio version</span></span> | <span data-ttu-id="39c75-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="39c75-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="39c75-108">**5.10.0**</span><span class="sxs-lookup"><span data-stu-id="39c75-108">**5.10.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="39c75-109">Visual Studio 2019 16.10 版</span><span class="sxs-lookup"><span data-stu-id="39c75-109">Visual Studio 2019 version 16.10</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="39c75-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="39c75-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="39c75-111"><sup>1</sup> 與 .net Core 工作負載搭配 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="39c75-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="39c75-112">Visual Studio 16.10、MSBuild 16.10 和 .NET 5.0.300 + 需要 NuGet.exe 5.10 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="39c75-112">Visual Studio 16.10, MSBuild 16.10, and .NET 5.0.300+ requires NuGet.exe 5.10 or later.</span></span>

## <a name="summary-whats-new-in-510"></a><span data-ttu-id="39c75-113">摘要：5.10 中的新功能</span><span class="sxs-lookup"><span data-stu-id="39c75-113">Summary: What's New in 5.10</span></span>

* <span data-ttu-id="39c75-114">簽署：實行 dotnet 受信任-簽署者命令- [#8053](https://github.com/NuGet/Home/issues/8053)</span><span class="sxs-lookup"><span data-stu-id="39c75-114">Signing: implement dotnet trusted-signers command - [#8053](https://github.com/NuGet/Home/issues/8053)</span></span>

* <span data-ttu-id="39c75-115">在 Linux 上將預設驗證設為停用，但在 Windows 上預設為啟用- [#10713](https://github.com/NuGet/Home/issues/10713)</span><span class="sxs-lookup"><span data-stu-id="39c75-115">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

* <span data-ttu-id="39c75-116">在 .NET 5 + Linux/MAC 上新增適用于套件簽署驗證的 ENV 變數- [#10742](https://github.com/NuGet/Home/issues/10742)</span><span class="sxs-lookup"><span data-stu-id="39c75-116">Add an ENV Variable for Package Signing Verification on .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)</span></span>

* <span data-ttu-id="39c75-117">改善大型解決方案的安裝新套件效能- [#10166](https://github.com/NuGet/Home/issues/10166)</span><span class="sxs-lookup"><span data-stu-id="39c75-117">Improve install new package performance for large solutions - [#10166](https://github.com/NuGet/Home/issues/10166)</span></span>

* <span data-ttu-id="39c75-118">將專案類型新增 `nfproj` 至 NUGET CLI 的 supportedProjectExtensions 清單。</span><span class="sxs-lookup"><span data-stu-id="39c75-118">Add the project type `nfproj` to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="39c75-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="39c75-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="39c75-120">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="39c75-120">Issues fixed in this release</span></span>

* <span data-ttu-id="39c75-121"><requireLicenseAcceptance>封裝專案時隱藏元素- [#5133](https://github.com/NuGet/Home/issues/5133)</span><span class="sxs-lookup"><span data-stu-id="39c75-121">Suppress the <requireLicenseAcceptance> element when packing a project - [#5133](https://github.com/NuGet/Home/issues/5133)</span></span>

* <span data-ttu-id="39c75-122">[CPVM] 預覽警告應顯示在 dotnet cli 上- [#10226](https://github.com/NuGet/Home/issues/10226)</span><span class="sxs-lookup"><span data-stu-id="39c75-122">[CPVM] preview warning should be shown on dotnet cli - [#10226](https://github.com/NuGet/Home/issues/10226)</span></span>

* <span data-ttu-id="39c75-123">將 PMUI 的背景和前景色彩標記更新為 CommonDocumentColors- [#10608](https://github.com/NuGet/Home/issues/10608)</span><span class="sxs-lookup"><span data-stu-id="39c75-123">Update the background and foreground color tokens of the PMUI to CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span></span>

* <span data-ttu-id="39c75-124">[Bug Bash]在 PM UI 中快速切換索引標籤時，[使用者已取消的作業] 錯誤顯示在 [錯誤清單] 視窗中： [#10671](https://github.com/NuGet/Home/issues/10671)</span><span class="sxs-lookup"><span data-stu-id="39c75-124">[Bug Bash] Error “operation canceled by user” show in Error List window when switching between tabs quickly in PM UI - [#10671](https://github.com/NuGet/Home/issues/10671)</span></span>

* <span data-ttu-id="39c75-125">PM UI：改善解決方案層級的套件安裝效能- [#10210](https://github.com/NuGet/Home/issues/10210)</span><span class="sxs-lookup"><span data-stu-id="39c75-125">PM UI:  Improve package installation performance on the solution level - [#10210](https://github.com/NuGet/Home/issues/10210)</span></span>

* <span data-ttu-id="39c75-126">將 GetService 取代為 NuGet 中的所有位置 GetServiceAsync。用戶端- [#3784](https://github.com/NuGet/Home/issues/3784)</span><span class="sxs-lookup"><span data-stu-id="39c75-126">Replace GetService with GetServiceAsync everywhere in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)</span></span>

* <span data-ttu-id="39c75-127">`..`相對路徑[#5016](https://github.com/NuGet/Home/issues/5016) NuGet.exe 套件效能問題</span><span class="sxs-lookup"><span data-stu-id="39c75-127">NuGet.exe pack performance problem with `..` relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>

* <span data-ttu-id="39c75-128">「Nuget 套件」的效能隨著來源路徑中增加的層級而減少- [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="39c75-128">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>

* <span data-ttu-id="39c75-129">使用重複的檔案封裝 nuspec 時，NuGet 不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="39c75-129">NuGet doesn't error when packaging nuspec with duplicate files.</span></span><span data-ttu-id="39c75-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span><span class="sxs-lookup"><span data-stu-id="39c75-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span></span>

* <span data-ttu-id="39c75-131">NuGet 套件「指定的 DateTimeOffset 無法轉換成 Zip 檔案時間戳記」- [#7001](https://github.com/NuGet/Home/issues/7001)</span><span class="sxs-lookup"><span data-stu-id="39c75-131">NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" - [#7001](https://github.com/NuGet/Home/issues/7001)</span></span>

* <span data-ttu-id="39c75-132">封裝封裝的檔案時間戳記會依時區 [#7395](https://github.com/NuGet/Home/issues/7395)</span><span class="sxs-lookup"><span data-stu-id="39c75-132">Timestamps of file of packed package is shifted by the timezone - [#7395](https://github.com/NuGet/Home/issues/7395)</span></span>

* <span data-ttu-id="39c75-133">NU1004 應包含更具可採取動作的資訊- [#7696](https://github.com/NuGet/Home/issues/7696)</span><span class="sxs-lookup"><span data-stu-id="39c75-133">NU1004 should contain more actionable information  - [#7696](https://github.com/NuGet/Home/issues/7696)</span></span>

* <span data-ttu-id="39c75-134">[Bug Bash][測試失敗]當執行 ' dotnet restore-------------------lock-mode ' 時，不應更新空白/格式錯誤的鎖定檔案- [#8640](https://github.com/NuGet/Home/issues/8640)</span><span class="sxs-lookup"><span data-stu-id="39c75-134">[Bug Bash][Test Failure] The empty/malformed lock file should not be updated when running ‘dotnet restore --use-lock-file --locked-mode’ - [#8640](https://github.com/NuGet/Home/issues/8640)</span></span>

* <span data-ttu-id="39c75-135">NuGetVersionRange 可剖析邏輯上不正確的範圍- [#9145](https://github.com/NuGet/Home/issues/9145)</span><span class="sxs-lookup"><span data-stu-id="39c75-135">NuGetVersionRange allows logically incorrect ranges to be parsed - [#9145](https://github.com/NuGet/Home/issues/9145)</span></span>

* <span data-ttu-id="39c75-136">PM UI 無法在選取和暫留套件來源之間顯示有辨別的背景色彩- [#9538](https://github.com/NuGet/Home/issues/9538)</span><span class="sxs-lookup"><span data-stu-id="39c75-136">PM UI can’t show distinguishable background color between selected and hovered package sources - [#9538](https://github.com/NuGet/Home/issues/9538)</span></span>

* <span data-ttu-id="39c75-137">螢幕讀取器無法讀取選取要安裝之專案的核取方塊- [#9578](https://github.com/NuGet/Home/issues/9578)</span><span class="sxs-lookup"><span data-stu-id="39c75-137">Checkbox for selecting projects to install to isn't being read by screen reader - [#9578](https://github.com/NuGet/Home/issues/9578)</span></span>

* <span data-ttu-id="39c75-138">詳細資料窗格版本下拉式清單預設選項應安裝/LatestStable 在 [已安裝/更新] 索引標籤上- [#9887](https://github.com/NuGet/Home/issues/9887)</span><span class="sxs-lookup"><span data-stu-id="39c75-138">Details Pane Versions Dropdown default selection should be Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span></span>

* <span data-ttu-id="39c75-139">移除 #9913 的一些 .net 5 sdk 報表 TargetPlatformMoniker 的因應措施帳戶 ` ,Version= `  -  [](https://github.com/NuGet/Home/issues/9913)</span><span class="sxs-lookup"><span data-stu-id="39c75-139">Remove workaround account for some .NET 5 SDKs report TargetPlatformMoniker of ` ,Version= ` - [#9913](https://github.com/NuGet/Home/issues/9913)</span></span>

* <span data-ttu-id="39c75-140">dotnet nuget 驗證太安靜- [#10316](https://github.com/NuGet/Home/issues/10316)</span><span class="sxs-lookup"><span data-stu-id="39c75-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span></span>

* <span data-ttu-id="39c75-141">VersionRange 無法剖析單一位數的範圍- [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="39c75-141">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>

* <span data-ttu-id="39c75-142">VS Solution manager 在調試期間擲回 null 例外狀況- [#10352](https://github.com/NuGet/Home/issues/10352)</span><span class="sxs-lookup"><span data-stu-id="39c75-142">VS Solution manager throws null exception for during debugging - [#10352](https://github.com/NuGet/Home/issues/10352)</span></span>

* <span data-ttu-id="39c75-143">將 CLI 例外狀況訊息移至字串資源檔- [#10392](https://github.com/NuGet/Home/issues/10392)</span><span class="sxs-lookup"><span data-stu-id="39c75-143">Move CLI exception messages to String Resource files - [#10392](https://github.com/NuGet/Home/issues/10392)</span></span>

* <span data-ttu-id="39c75-144">移除不正確程式碼 (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span><span class="sxs-lookup"><span data-stu-id="39c75-144">Remove dead code (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span></span>

* <span data-ttu-id="39c75-145">更新內容功能表應該會滾動至第一個選取的專案- [#10498](https://github.com/NuGet/Home/issues/10498)</span><span class="sxs-lookup"><span data-stu-id="39c75-145">Update context menu should scroll to first selected item - [#10498](https://github.com/NuGet/Home/issues/10498)</span></span>

* <span data-ttu-id="39c75-146">方案 PMUI 詳細資料具有重迭的水準橫條 [#10533](https://github.com/NuGet/Home/issues/10533)</span><span class="sxs-lookup"><span data-stu-id="39c75-146">Solution PMUI Details has overlapping horizontal bar - [#10533](https://github.com/NuGet/Home/issues/10533)</span></span>

* <span data-ttu-id="39c75-147">簽署：當憑證過期且時間戳記不受信任時，不會顯示主要簽章詳細資料- [#10535](https://github.com/NuGet/Home/issues/10535)</span><span class="sxs-lookup"><span data-stu-id="39c75-147">Signing:  primary signature details not displayed when certificate expired and timestamp untrusted - [#10535](https://github.com/NuGet/Home/issues/10535)</span></span>

* <span data-ttu-id="39c75-148">沒有已啟用的來源會防止 PM UI 顯示 [#10541](https://github.com/NuGet/Home/issues/10541)</span><span class="sxs-lookup"><span data-stu-id="39c75-148">Having no enabled sources prevents the PM UI from showing - [#10541](https://github.com/NuGet/Home/issues/10541)</span></span>

* <span data-ttu-id="39c75-149">封裝中繼資料 (詳細資料、取代) 有時不會從 CodeSpaces 中的 nuget.org 提取- [#10549](https://github.com/NuGet/Home/issues/10549)</span><span class="sxs-lookup"><span data-stu-id="39c75-149">Package Metadata (details, deprecation) are sometimes not pulled from nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span></span>

* <span data-ttu-id="39c75-150">PMUI 初始化失敗，但在 debug 會話期間發生例外狀況- [#10559](https://github.com/NuGet/Home/issues/10559)</span><span class="sxs-lookup"><span data-stu-id="39c75-150">PMUI initialization fails with exception during debug session - [#10559](https://github.com/NuGet/Home/issues/10559)</span></span>

* <span data-ttu-id="39c75-151">nuget 還原會導致大型 endian 系統的套件完整性檢查失敗- [#10567](https://github.com/NuGet/Home/issues/10567)</span><span class="sxs-lookup"><span data-stu-id="39c75-151">nuget restore results in a package integrity check failure on big endian system - [#10567](https://github.com/NuGet/Home/issues/10567)</span></span>

* <span data-ttu-id="39c75-152">擲回 >formatexception，而不是 PackagingException- [#10595](https://github.com/NuGet/Home/issues/10595)</span><span class="sxs-lookup"><span data-stu-id="39c75-152">FormatException is thrown instead of PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span></span>

* <span data-ttu-id="39c75-153">CPVM-圖形中的並行問題逐步解說演算法- [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="39c75-153">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>

* <span data-ttu-id="39c75-154">新增 PMC powershell 版本遙測- [#10609](https://github.com/NuGet/Home/issues/10609)</span><span class="sxs-lookup"><span data-stu-id="39c75-154">Add PMC powershell version telemetry - [#10609](https://github.com/NuGet/Home/issues/10609)</span></span>

* <span data-ttu-id="39c75-155">改善 NuGetVersion 排序效能- [#10611](https://github.com/NuGet/Home/issues/10611)</span><span class="sxs-lookup"><span data-stu-id="39c75-155">Improve NuGetVersion sort performance - [#10611](https://github.com/NuGet/Home/issues/10611)</span></span>

* <span data-ttu-id="39c75-156">受信任-簽署者新增具有不一致的引數- [#10647](https://github.com/NuGet/Home/issues/10647)</span><span class="sxs-lookup"><span data-stu-id="39c75-156">Trusted-signers Add has inconsistent arguments - [#10647](https://github.com/NuGet/Home/issues/10647)</span></span>

* <span data-ttu-id="39c75-157">Vs2019 v 16.9.0：將 NuGet 封裝管理員中的索引標籤從 [更新] 切換至 [已安裝] 時，不會更新框架。</span><span class="sxs-lookup"><span data-stu-id="39c75-157">Vs2019 v16.9.0: Switching tabs in NuGet Package Manager from "Updates" to "Installed" doesn't update the frame.</span></span><span data-ttu-id="39c75-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span><span class="sxs-lookup"><span data-stu-id="39c75-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span></span>

* <span data-ttu-id="39c75-159">從 PMUI 中的版本號碼移除 "v"- [#10677](https://github.com/NuGet/Home/issues/10677)</span><span class="sxs-lookup"><span data-stu-id="39c75-159">Remove the "v" from the version number in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span></span>

* <span data-ttu-id="39c75-160">INuGetProjectService 會在接收 CPS 專案系統提名之前擲回 GetInstalledPackagesAsync- [#10681](https://github.com/NuGet/Home/issues/10681)</span><span class="sxs-lookup"><span data-stu-id="39c75-160">INuGetProjectService.GetInstalledPackagesAsync throws before receiving CPS project system nomination - [#10681](https://github.com/NuGet/Home/issues/10681)</span></span>

* <span data-ttu-id="39c75-161">內嵌圖示會導致在流覽索引標籤上從來源「Microsoft Visual Studio 離線套件」拒絕存取- [#10687](https://github.com/NuGet/Home/issues/10687)</span><span class="sxs-lookup"><span data-stu-id="39c75-161">Embedded Icons cause Access Denied from source "Microsoft Visual Studio Offline Packages" on Browse tab - [#10687](https://github.com/NuGet/Home/issues/10687)</span></span>

* <span data-ttu-id="39c75-162">如果未設定 MSBuildProjectExtensionsPath，則會擲回 INuGetProjectService GetInstalledPackagesAsync- [#10739](https://github.com/NuGet/Home/issues/10739)</span><span class="sxs-lookup"><span data-stu-id="39c75-162">INuGetProjectService.GetInstalledPackagesAsync throws when MSBuildProjectExtensionsPath is not set - [#10739](https://github.com/NuGet/Home/issues/10739)</span></span>

* <span data-ttu-id="39c75-163">「dotnet nuget 移除來源 nuget.org」無法在第一次使用 [#10745](https://github.com/NuGet/Home/issues/10745)</span><span class="sxs-lookup"><span data-stu-id="39c75-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>

* <span data-ttu-id="39c75-164">Nuget 會封鎖非同步方法中的 threadpool 執行緒，以對 UI 執行緒進行同步呼叫 [#10775](https://github.com/NuGet/Home/issues/10775)</span><span class="sxs-lookup"><span data-stu-id="39c75-164">Nuget blocks a threadpool thread in an async method making a synchronous call to the UI thread - [#10775](https://github.com/NuGet/Home/issues/10775)</span></span>

* <span data-ttu-id="39c75-165">工具-> 選項-> NuGet 封裝管理員字串會被截斷- [#10779](https://github.com/NuGet/Home/issues/10779)</span><span class="sxs-lookup"><span data-stu-id="39c75-165">Tools -> Options -> NuGet Package Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span></span>

* <span data-ttu-id="39c75-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` 是不正確程式碼，並會影響效能- [#10790](https://github.com/NuGet/Home/issues/10790)</span><span class="sxs-lookup"><span data-stu-id="39c75-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` is dead code and hurting performance - [#10790](https://github.com/NuGet/Home/issues/10790)</span></span>

* <span data-ttu-id="39c75-167">使用 NuGet SDK 套件中的內嵌圖示- [#10795](https://github.com/NuGet/Home/issues/10795)</span><span class="sxs-lookup"><span data-stu-id="39c75-167">Use embedded icon in NuGet SDK packages - [#10795](https://github.com/NuGet/Home/issues/10795)</span></span>

* <span data-ttu-id="39c75-168">更新 SPDX 授權清單- [#10806](https://github.com/NuGet/Home/issues/10806)</span><span class="sxs-lookup"><span data-stu-id="39c75-168">Update the SPDX license list - [#10806](https://github.com/NuGet/Home/issues/10806)</span></span>

<span data-ttu-id="39c75-169">**[此版本修正的所有問題清單-5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span><span class="sxs-lookup"><span data-stu-id="39c75-169">**[List of all issues fixed in this release - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span></span>
  
<span data-ttu-id="39c75-170">**[此版本中的認可清單-5.10。0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span><span class="sxs-lookup"><span data-stu-id="39c75-170">**[List of commits in this release - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span></span>
  
### <a name="community-contributions"></a><span data-ttu-id="39c75-171">社群投稿</span><span class="sxs-lookup"><span data-stu-id="39c75-171">Community contributions</span></span>

<span data-ttu-id="39c75-172">感謝所有協助讓此 NuGet 版本絕佳的參與者！</span><span class="sxs-lookup"><span data-stu-id="39c75-172">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="39c75-173">人員</span><span class="sxs-lookup"><span data-stu-id="39c75-173">Who</span></span>|<span data-ttu-id="39c75-174">Pr</span><span class="sxs-lookup"><span data-stu-id="39c75-174">PRs</span></span>|<span data-ttu-id="39c75-175">問題</span><span class="sxs-lookup"><span data-stu-id="39c75-175">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="39c75-176">港-z</span><span class="sxs-lookup"><span data-stu-id="39c75-176">louis-z</span></span>](https://github.com/louis-z) | [<span data-ttu-id="39c75-177">3991</span><span class="sxs-lookup"><span data-stu-id="39c75-177">3991</span></span>](https://github.com/NuGet/NuGet.Client/pull/3991) | <span data-ttu-id="39c75-178">VersionRange 無法剖析單一位數的範圍- [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="39c75-178">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>
[<span data-ttu-id="39c75-179">omajid</span><span class="sxs-lookup"><span data-stu-id="39c75-179">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="39c75-180">3860</span><span class="sxs-lookup"><span data-stu-id="39c75-180">3860</span></span>](https://github.com/NuGet/NuGet.Client/pull/3860) | <span data-ttu-id="39c75-181">NuGet. 用戶端 build.sh 中斷- [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="39c75-181">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="39c75-182">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="39c75-182">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="39c75-183">3623</span><span class="sxs-lookup"><span data-stu-id="39c75-183">3623</span></span>](https://github.com/NuGet/NuGet.Client/pull/3623) | <span data-ttu-id="39c75-184">NuGet. 用戶端 build.sh 中斷- [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="39c75-184">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="39c75-185">BlackGad</span><span class="sxs-lookup"><span data-stu-id="39c75-185">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="39c75-186">3953</span><span class="sxs-lookup"><span data-stu-id="39c75-186">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="39c75-187">「Nuget 套件」的效能隨著來源路徑中增加的層級而減少- [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="39c75-187">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>
[<span data-ttu-id="39c75-188">BlackGad</span><span class="sxs-lookup"><span data-stu-id="39c75-188">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="39c75-189">3953</span><span class="sxs-lookup"><span data-stu-id="39c75-189">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="39c75-190">NuGet.exe pack 效能問題。</span><span class="sxs-lookup"><span data-stu-id="39c75-190">NuGet.exe pack performance problem with ..</span></span> <span data-ttu-id="39c75-191">相對路徑- [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="39c75-191">relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>
[<span data-ttu-id="39c75-192">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="39c75-192">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="39c75-193">3940</span><span class="sxs-lookup"><span data-stu-id="39c75-193">3940</span></span>](https://github.com/NuGet/NuGet.Client/pull/3940) | <span data-ttu-id="39c75-194">CPVM-圖形中的並行問題逐步解說演算法- [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="39c75-194">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>
[<span data-ttu-id="39c75-195">josesimoes</span><span class="sxs-lookup"><span data-stu-id="39c75-195">josesimoes</span></span>](https://github.com/josesimoes) | [<span data-ttu-id="39c75-196">3943</span><span class="sxs-lookup"><span data-stu-id="39c75-196">3943</span></span>](https://github.com/NuGet/NuGet.Client/pull/3943) | <span data-ttu-id="39c75-197">將專案類型 nfproj 新增至 Nuget CLI 的 supportedProjectExtensions 清單。</span><span class="sxs-lookup"><span data-stu-id="39c75-197">Add the project type nfproj to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="39c75-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="39c75-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="39c75-199">歡迎意見反應</span><span class="sxs-lookup"><span data-stu-id="39c75-199">Feedback welcome</span></span>

<span data-ttu-id="39c75-200">您的意見反應對我們非常寶貴。</span><span class="sxs-lookup"><span data-stu-id="39c75-200">Your feedback is important to us.</span></span>  <span data-ttu-id="39c75-201">如果此版本有任何問題，請查看我們的 [GitHub 問題](https://github.com/NuGet/Home/issues) ，並 [Visual Studio 開發人員社群](https://developercommunity.visualstudio.com/) 現有的問題。</span><span class="sxs-lookup"><span data-stu-id="39c75-201">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="39c75-202">針對 NuGet 內的新問題，請報告 [GitHub 問題](https://github.com/NuGet/Home/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="39c75-202">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="39c75-203">如需一般的 NuGet 體驗問題，請透過 [說明] 下您最愛的 IDE 中的 [回報 [問題](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) ] 選項，讓我們知道 **> 報告問題**。</span><span class="sxs-lookup"><span data-stu-id="39c75-203">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
