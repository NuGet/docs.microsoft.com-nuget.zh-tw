---
title: NuGet 5.9 版本資訊
description: NuGet 5.9 的版本資訊，包括新功能、bug 修正及 Dcr。
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 50fd277a4f1f39b4a68a89cd07af4e21f0d3d831
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508809"
---
# <a name="nuget-59-release-notes"></a><span data-ttu-id="38e3c-103">NuGet 5.9 版本資訊</span><span class="sxs-lookup"><span data-stu-id="38e3c-103">NuGet 5.9 Release Notes</span></span>

<span data-ttu-id="38e3c-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="38e3c-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="38e3c-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="38e3c-105">NuGet version</span></span> | <span data-ttu-id="38e3c-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="38e3c-106">Available in Visual Studio version</span></span> | <span data-ttu-id="38e3c-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="38e3c-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="38e3c-108">**5.9.0**</span><span class="sxs-lookup"><span data-stu-id="38e3c-108">**5.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="38e3c-109">Visual Studio 2019 16.9 版</span><span class="sxs-lookup"><span data-stu-id="38e3c-109">Visual Studio 2019 version 16.9</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="38e3c-110">[5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="38e3c-110">[5.0.200](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="38e3c-111">**5.9.1**</span><span class="sxs-lookup"><span data-stu-id="38e3c-111">**5.9.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="38e3c-112">Visual Studio 2019 16.9 版</span><span class="sxs-lookup"><span data-stu-id="38e3c-112">Visual Studio 2019 version 16.9</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="38e3c-113">[5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="38e3c-113">[5.0.202](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="38e3c-114"><sup>1</sup> 與 .net Core 工作負載搭配 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="38e3c-114"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="38e3c-115">Visual Studio 16.9、MSBuild 16.9 和 .NET 5.0.200 + 需要 NuGet.exe 5.9 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="38e3c-115">Visual Studio 16.9, MSBuild 16.9, and .NET 5.0.200+ requires NuGet.exe 5.9 or later.</span></span>

## <a name="summary-whats-new-in-59"></a><span data-ttu-id="38e3c-116">摘要：5.9 中的新功能</span><span class="sxs-lookup"><span data-stu-id="38e3c-116">Summary: What's New in 5.9</span></span>

* <span data-ttu-id="38e3c-117">針對使用預先選取的套件啟動封裝管理員 UI 的套件相依性，新增 [更新] 內容功能表項目以更新- [#10378](https://github.com/NuGet/Home/issues/10378)</span><span class="sxs-lookup"><span data-stu-id="38e3c-117">Add "Update" context menu item for package dependencies that launches Package Manager UI with preselected packages to update - [#10378](https://github.com/NuGet/Home/issues/10378)</span></span>

    ![以滑鼠右鍵按一下 [封裝] 的 [更新] 體驗](media/releasenotes-59-update.png)

* <span data-ttu-id="38e3c-119">在方案層級中，于方案層級的 [版本] 資料行中顯示要求的版本 (包括浮動版本或版本範圍要求) 封裝管理員 UI- [#9827](https://github.com/NuGet/Home/issues/9827)</span><span class="sxs-lookup"><span data-stu-id="38e3c-119">Show the requested version (including floating version or version range request) in the "Version" column of the project list in the solution level Package Manager UI - [#9827](https://github.com/NuGet/Home/issues/9827)</span></span>

    ![解決方案層級封裝管理員 UI 中要求的版本](media/releasenotes-59-requested-version.png)

* <span data-ttu-id="38e3c-121">在封裝管理員 UI 流覽索引標籤中 IntelliCode 封裝的建議（以 A/B 測試 [#10053](https://github.com/NuGet/Home/issues/10053)</span><span class="sxs-lookup"><span data-stu-id="38e3c-121">IntelliCode package suggestions in the Package Manager UI Browse tab released as an A/B test - [#10053](https://github.com/NuGet/Home/issues/10053)</span></span>

* <span data-ttu-id="38e3c-122">擴充檔案 `.nupkg.metadata` 以包含安裝來源- [#10354](https://github.com/NuGet/Home/issues/10354)</span><span class="sxs-lookup"><span data-stu-id="38e3c-122">Extend the `.nupkg.metadata` file to include the installation source - [#10354](https://github.com/NuGet/Home/issues/10354)</span></span>

* <span data-ttu-id="38e3c-123">引進新的 msbuild 屬性，在 pack 工作期間排除特定 Tfm 的組建輸出- [#10396](https://github.com/NuGet/Home/issues/10396)</span><span class="sxs-lookup"><span data-stu-id="38e3c-123">Introduce a new msbuild property to exclude build output for specific TFMs during pack task - [#10396](https://github.com/NuGet/Home/issues/10396)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="38e3c-124">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="38e3c-124">Issues fixed in this release</span></span>

<span data-ttu-id="38e3c-125">**Dcr (設計變更要求) ：**</span><span class="sxs-lookup"><span data-stu-id="38e3c-125">**DCRs(Design Change Request):**</span></span>

* <span data-ttu-id="38e3c-126">安裝最新的套件版本時，關閉圖示圖示並不直覺。</span><span class="sxs-lookup"><span data-stu-id="38e3c-126">The down icon icon when the latest package version is installed is not intuitive.</span></span> <span data-ttu-id="38e3c-127">舊的綠色刻度是完美的 [#9789](https://github.com/NuGet/Home/issues/9789)</span><span class="sxs-lookup"><span data-stu-id="38e3c-127">The old green tick was perfect - [#9789](https://github.com/NuGet/Home/issues/9789)</span></span>

* <span data-ttu-id="38e3c-128">Nuget Debug 詳細資訊應該指出封裝的來源- [#3055](https://github.com/NuGet/Home/issues/3055)</span><span class="sxs-lookup"><span data-stu-id="38e3c-128">Nuget Debug verbosity should say where a package came from - [#3055](https://github.com/NuGet/Home/issues/3055)</span></span>

* <span data-ttu-id="38e3c-129">NuGet 套件應該在版本號碼中攔截不正確的點省略- [#9215](https://github.com/NuGet/Home/issues/9215)</span><span class="sxs-lookup"><span data-stu-id="38e3c-129">NuGet pack should catch incorrect omitting of the dot in version numbers - [#9215](https://github.com/NuGet/Home/issues/9215)</span></span>

* <span data-ttu-id="38e3c-130">[CPVM]停用集中式可轉移相依性的釘選- [#10132](https://github.com/NuGet/Home/issues/10132)</span><span class="sxs-lookup"><span data-stu-id="38e3c-130">[CPVM] Disable pinning of the central transitive dependencies  - [#10132](https://github.com/NuGet/Home/issues/10132)</span></span>

* <span data-ttu-id="38e3c-131">net5 TFM：缺少 TPV 時產生錯誤- [#9441](https://github.com/NuGet/Home/issues/9441)</span><span class="sxs-lookup"><span data-stu-id="38e3c-131">net5 TFM: produce error when missing TPV - [#9441](https://github.com/NuGet/Home/issues/9441)</span></span>

* <span data-ttu-id="38e3c-132">記錄檔封裝 contenthash 在) 解壓縮期間的還原記錄 (- [#10384](https://github.com/NuGet/Home/issues/10384)</span><span class="sxs-lookup"><span data-stu-id="38e3c-132">Log package contenthash during restore logging (during extraction) - [#10384](https://github.com/NuGet/Home/issues/10384)</span></span>

* <span data-ttu-id="38e3c-133">針對在開啟解決方案時呼叫還原的舊版 PR 專案，執行預先註冊機制 [#9986](https://github.com/NuGet/Home/issues/9986)</span><span class="sxs-lookup"><span data-stu-id="38e3c-133">Implement a pre-registration mechanism for legacy PR projects that call restore at solution open - [#9986](https://github.com/NuGet/Home/issues/9986)</span></span>

* <span data-ttu-id="38e3c-134">當套件管理員中選取了一個以上的來源時，NuGet 套件推薦應該會運作- [#10433](https://github.com/NuGet/Home/issues/10433)</span><span class="sxs-lookup"><span data-stu-id="38e3c-134">NuGet package recommender should work when more than one source is selected in package manager - [#10433](https://github.com/NuGet/Home/issues/10433)</span></span>

* <span data-ttu-id="38e3c-135">在正常的詳細資訊還原時，記錄要從中還原封裝的來源 [#10461](https://github.com/NuGet/Home/issues/10461)</span><span class="sxs-lookup"><span data-stu-id="38e3c-135">When restoring at normal verbosity, log which source a package is being restored from - [#10461](https://github.com/NuGet/Home/issues/10461)</span></span>

<span data-ttu-id="38e3c-136">**錯誤：**</span><span class="sxs-lookup"><span data-stu-id="38e3c-136">**Bugs:**</span></span>

* <span data-ttu-id="38e3c-137">INuGetPackageFileService-針對 Codespaces 連線和獨立[#10151](https://github.com/NuGet/Home/issues/10151)提取映射和內嵌授權</span><span class="sxs-lookup"><span data-stu-id="38e3c-137">INuGetPackageFileService - Fetch Images and embedded licenses for Codespaces-connected and standalone - [#10151](https://github.com/NuGet/Home/issues/10151)</span></span>

* <span data-ttu-id="38e3c-138">VS OE： IProjectMetadataCoNtextInfo 缺少格式器- [#10079](https://github.com/NuGet/Home/issues/10079)</span><span class="sxs-lookup"><span data-stu-id="38e3c-138">VS OE:  IProjectMetadataContextInfo missing formatter - [#10079](https://github.com/NuGet/Home/issues/10079)</span></span>

* <span data-ttu-id="38e3c-139">[CPVM-效能]減少寫入至 centralTransitiveDependencyGroups 的資訊- [#10002](https://github.com/NuGet/Home/issues/10002)</span><span class="sxs-lookup"><span data-stu-id="38e3c-139">[CPVM-Perf] Reduce the information written to centralTransitiveDependencyGroups - [#10002](https://github.com/NuGet/Home/issues/10002)</span></span>

* <span data-ttu-id="38e3c-140">因為未載入的專案所擲回的還原作業會回報為 `NoOp` 遙測 [#9985](https://github.com/NuGet/Home/issues/9985)</span><span class="sxs-lookup"><span data-stu-id="38e3c-140">Restore operations that throw due to a project not being loaded are reported as `NoOp` in telemetry - [#9985](https://github.com/NuGet/Home/issues/9985)</span></span>

* <span data-ttu-id="38e3c-141">具有特定顏色託盤的圖示會導致 PM UI 損毀與 [#10037](https://github.com/NuGet/Home/issues/10037)</span><span class="sxs-lookup"><span data-stu-id="38e3c-141">Icons with certain color pallets causes PM UI to crash VS - [#10037](https://github.com/NuGet/Home/issues/10037)</span></span>

* <span data-ttu-id="38e3c-142">[CPVM-效能]新增 CPVM 資訊時減少 PackageSpec 複製- [#10003](https://github.com/NuGet/Home/issues/10003)</span><span class="sxs-lookup"><span data-stu-id="38e3c-142">[CPVM-Perf] Reduce the PackageSpec clone when adding the CPVM information  - [#10003](https://github.com/NuGet/Home/issues/10003)</span></span>

* <span data-ttu-id="38e3c-143">PM UI-asyncify 圖示載入- [#10009](https://github.com/NuGet/Home/issues/10009)</span><span class="sxs-lookup"><span data-stu-id="38e3c-143">PM UI - asyncify icon loading - [#10009](https://github.com/NuGet/Home/issues/10009)</span></span>

* <span data-ttu-id="38e3c-144">在 PM UI 中載入圖示 Url 時的 UI 延遲- [#8505](https://github.com/NuGet/Home/issues/8505)</span><span class="sxs-lookup"><span data-stu-id="38e3c-144">UI delay when loading icon URLs in PM UI - [#8505](https://github.com/NuGet/Home/issues/8505)</span></span>

* <span data-ttu-id="38e3c-145">BitmapSource 和 WPF UI 執行緒中的執行緒親和性- [#9161](https://github.com/NuGet/Home/issues/9161)</span><span class="sxs-lookup"><span data-stu-id="38e3c-145">Thread affinity in BitmapSource and WPF UI threads - [#9161](https://github.com/NuGet/Home/issues/9161)</span></span>

* <span data-ttu-id="38e3c-146">使用 targetframework 別名來 packastool 時警告 NU5128 的警告- [#10097](https://github.com/NuGet/Home/issues/10097)</span><span class="sxs-lookup"><span data-stu-id="38e3c-146">Warning for warning NU5128 when packastool with targetframework alias - [#10097](https://github.com/NuGet/Home/issues/10097)</span></span>

* <span data-ttu-id="38e3c-147">自訂群組建中套件目標的 OutputPath 邏輯無法正常運作- [#9234](https://github.com/NuGet/Home/issues/9234)</span><span class="sxs-lookup"><span data-stu-id="38e3c-147">OutputPath logic in Pack targets in a customized build doesn't work properly - [#9234](https://github.com/NuGet/Home/issues/9234)</span></span>

* <span data-ttu-id="38e3c-148">VS OE：用戶端上的快取 IServiceBroker 實例- [#10141](https://github.com/NuGet/Home/issues/10141)</span><span class="sxs-lookup"><span data-stu-id="38e3c-148">VS OE:  cache IServiceBroker instance on client - [#10141](https://github.com/NuGet/Home/issues/10141)</span></span>

* <span data-ttu-id="38e3c-149">建立 NuGetProjectActions 以從 PM UI 卸載平行作業- [#9956](https://github.com/NuGet/Home/issues/9956)</span><span class="sxs-lookup"><span data-stu-id="38e3c-149">Make creating NuGetProjectActions for uninstall  from PM UI a parallel operation - [#9956](https://github.com/NuGet/Home/issues/9956)</span></span>

* <span data-ttu-id="38e3c-150">效能：減少舊版專案和非 PR 專案的 GetPackageSpecsAsync UIDelays- [#9953](https://github.com/NuGet/Home/issues/9953)</span><span class="sxs-lookup"><span data-stu-id="38e3c-150">Performance: Reduce UIDelays in GetPackageSpecsAsync for Legacy projects and non PR projects - [#9953](https://github.com/NuGet/Home/issues/9953)</span></span>

* <span data-ttu-id="38e3c-151">``dotnet nuget push *.nupkg`` 未推送一個以上的檔案- [#4393](https://github.com/NuGet/Home/issues/4393)</span><span class="sxs-lookup"><span data-stu-id="38e3c-151">``dotnet nuget push *.nupkg`` doesn't push more than one file - [#4393](https://github.com/NuGet/Home/issues/4393)</span></span>

* <span data-ttu-id="38e3c-152">當重新導向時，輸出會在 macOS 上以80個字元包裝： [#10198](https://github.com/NuGet/Home/issues/10198)</span><span class="sxs-lookup"><span data-stu-id="38e3c-152">Output is wrapped at 80 characters on macOS when redirected - [#10198](https://github.com/NuGet/Home/issues/10198)</span></span>

* <span data-ttu-id="38e3c-153">還原失敗，發生來源 <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)</span><span class="sxs-lookup"><span data-stu-id="38e3c-153">Restore fails with -Source <Relative Path> - [#9406](https://github.com/NuGet/Home/issues/9406)</span></span>

* <span data-ttu-id="38e3c-154">netcoreapp 5.0-windows 不會來回行程，也不會剖析平臺資訊- [#10177](https://github.com/NuGet/Home/issues/10177)</span><span class="sxs-lookup"><span data-stu-id="38e3c-154">netcoreapp5.0-windows does not round trip and does not parse platform information - [#10177](https://github.com/NuGet/Home/issues/10177)</span></span>

* <span data-ttu-id="38e3c-155">自訂的 CPS 專案需要 AssemblyReferences 專案功能才能進行還原。</span><span class="sxs-lookup"><span data-stu-id="38e3c-155">Custom CPS projects require AssemblyReferences project capability in order to restore.</span></span><span data-ttu-id="38e3c-156"> - [#8071](https://github.com/NuGet/Home/issues/8071)</span><span class="sxs-lookup"><span data-stu-id="38e3c-156"> - [#8071](https://github.com/NuGet/Home/issues/8071)</span></span>

* <span data-ttu-id="38e3c-157">授權和圖示檔案存在檢查應該一律使用區分大小寫的比較- [#9817](https://github.com/NuGet/Home/issues/9817)</span><span class="sxs-lookup"><span data-stu-id="38e3c-157">License and icon file existence check should always use a case-sensitive comparison - [#9817](https://github.com/NuGet/Home/issues/9817)</span></span>

* <span data-ttu-id="38e3c-158">DotnetCLiToolReference 還原會讓您難以找出無 op 專案計數/uptodateprojectscount 的原因 [#10038](https://github.com/NuGet/Home/issues/10038)</span><span class="sxs-lookup"><span data-stu-id="38e3c-158">DotnetCLiToolReference restores make it difficult to reason about no-op projects count/uptodateprojectscount - [#10038](https://github.com/NuGet/Home/issues/10038)</span></span>

* <span data-ttu-id="38e3c-159">當您在深色主題中透過 [選擇 NuGet 封裝管理員格式] 對話方塊流覽時，很難看到套件格式的虛線方塊- [#9729](https://github.com/NuGet/Home/issues/9729)</span><span class="sxs-lookup"><span data-stu-id="38e3c-159">Hard to see the dash-line box of package format when navigating by tab through the “Choose NuGet Package Manager Format” dialog in Dark theme - [#9729](https://github.com/NuGet/Home/issues/9729)</span></span>

* <span data-ttu-id="38e3c-160">從 #10314 排除可轉移的架構參考 `CollectFrameworkReferences`  -  [](https://github.com/NuGet/Home/issues/10314)</span><span class="sxs-lookup"><span data-stu-id="38e3c-160">Exclude transitive framework references from `CollectFrameworkReferences` - [#10314](https://github.com/NuGet/Home/issues/10314)</span></span>

* <span data-ttu-id="38e3c-161">比較子的靜態屬性應為等冪- [#10339](https://github.com/NuGet/Home/issues/10339)</span><span class="sxs-lookup"><span data-stu-id="38e3c-161">Comparer static properties should be idempotent  - [#10339](https://github.com/NuGet/Home/issues/10339)</span></span>

* <span data-ttu-id="38e3c-162">解決內部合約元件載入 (修正 RPS 或取得例外狀況) - [#9919](https://github.com/NuGet/Home/issues/9919)</span><span class="sxs-lookup"><span data-stu-id="38e3c-162">resolve internal contracts assembly loading (fix RPS or get exception) - [#9919](https://github.com/NuGet/Home/issues/9919)</span></span>

* <span data-ttu-id="38e3c-163">將 GetService 取代為 NuGet 中的 GetServiceAsync。用戶端，第1部分- [#10362](https://github.com/NuGet/Home/issues/10362)</span><span class="sxs-lookup"><span data-stu-id="38e3c-163">Replace GetService with GetServiceAsync in NuGet.Clients, Part 1 - [#10362](https://github.com/NuGet/Home/issues/10362)</span></span>

* <span data-ttu-id="38e3c-164">CLI 安裝不應安裝未列出的套件- [#7466](https://github.com/NuGet/Home/issues/7466)</span><span class="sxs-lookup"><span data-stu-id="38e3c-164">CLI installs should not install unlisted packages - [#7466](https://github.com/NuGet/Home/issues/7466)</span></span>

* <span data-ttu-id="38e3c-165">靜態 msbuild graph 還原-unnnecessary 有關 MSBuildStartupDirectory 的記錄- [#10335](https://github.com/NuGet/Home/issues/10335)</span><span class="sxs-lookup"><span data-stu-id="38e3c-165">Static msbuild graph restore - unnnecessary logging about MSBuildStartupDirectory - [#10335](https://github.com/NuGet/Home/issues/10335)</span></span>

* <span data-ttu-id="38e3c-166">標記為 PrivateAssets 之 ProjectReferences 的專案相依性不應該包含在鎖定檔案中的最新檢查 [#8565](https://github.com/NuGet/Home/issues/8565)</span><span class="sxs-lookup"><span data-stu-id="38e3c-166">Project Dependencies of ProjectReferences marked as PrivateAssets should not be included in the lock file up to date check - [#8565](https://github.com/NuGet/Home/issues/8565)</span></span>

* <span data-ttu-id="38e3c-167">具有錯誤資料的 SDK 專案未顯示 VS- [#10406](https://github.com/NuGet/Home/issues/10406)中的還原錯誤</span><span class="sxs-lookup"><span data-stu-id="38e3c-167">SDK projects with bad data not showing restore errors in VS - [#10406](https://github.com/NuGet/Home/issues/10406)</span></span>

* <span data-ttu-id="38e3c-168">從具有 LockedMode [#9623](https://github.com/NuGet/Home/issues/9623)的 cmd 行還原具有混合舊版和 netstandard2 專案的方案時，NU1004</span><span class="sxs-lookup"><span data-stu-id="38e3c-168">NU1004 when restoring a solution that has mixed Legacy and netstandard2 projects from cmd line with LockedMode - [#9623](https://github.com/NuGet/Home/issues/9623)</span></span>

* <span data-ttu-id="38e3c-169">套件包含透過相依性套件帶入目前專案套件中的內容， (SDK 型專案只) [#8867](https://github.com/NuGet/Home/issues/8867)</span><span class="sxs-lookup"><span data-stu-id="38e3c-169">Pack includes content brought in through dependency packages into the current project's package (SDK based projects only) - [#8867](https://github.com/NuGet/Home/issues/8867)</span></span>

* <span data-ttu-id="38e3c-170">新增 NuGet 與擴充性 API 錯誤的遙測- [#10062](https://github.com/NuGet/Home/issues/10062)</span><span class="sxs-lookup"><span data-stu-id="38e3c-170">Add telemetry for NuGet's VS extensibility API faults - [#10062](https://github.com/NuGet/Home/issues/10062)</span></span>

* <span data-ttu-id="38e3c-171">在靜態圖形還原中新增 GenerateRestoreGraphFile，以改善 debugability。</span><span class="sxs-lookup"><span data-stu-id="38e3c-171">Add GenerateRestoreGraphFile in static graph restore to improve debugability.</span></span><span data-ttu-id="38e3c-172">  - [#10365](https://github.com/NuGet/Home/issues/10365)</span><span class="sxs-lookup"><span data-stu-id="38e3c-172">  - [#10365](https://github.com/NuGet/Home/issues/10365)</span></span>

* <span data-ttu-id="38e3c-173">無法開啟 NuGet 套件管理員- [#10336](https://github.com/NuGet/Home/issues/10336)</span><span class="sxs-lookup"><span data-stu-id="38e3c-173">Cannot open the NuGet Package manager - [#10336](https://github.com/NuGet/Home/issues/10336)</span></span>

* <span data-ttu-id="38e3c-174">NVDA/朗讀程式未讀取 "Apache-2.0" 連結的「授權」標籤- [#10425](https://github.com/NuGet/Home/issues/10425)</span><span class="sxs-lookup"><span data-stu-id="38e3c-174">NVDA/Narrator is not reading "License" label for "Apache-2.0" link - [#10425](https://github.com/NuGet/Home/issues/10425)</span></span>

* <span data-ttu-id="38e3c-175">在 VS- [#9402](https://github.com/NuGet/Home/issues/9402)中，最新的狀態列訊息不太理想</span><span class="sxs-lookup"><span data-stu-id="38e3c-175">The up to date status bar message is not great in VS - [#9402](https://github.com/NuGet/Home/issues/9402)</span></span>

* <span data-ttu-id="38e3c-176">packages.config package.lock.js使用不正確的目標架構- [#10257](https://github.com/NuGet/Home/issues/10257)</span><span class="sxs-lookup"><span data-stu-id="38e3c-176">packages.config package.lock.json uses an incorrect target framework - [#10257](https://github.com/NuGet/Home/issues/10257)</span></span>

* <span data-ttu-id="38e3c-177">Codespaces：修正 https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)的遙測</span><span class="sxs-lookup"><span data-stu-id="38e3c-177">Codespaces:  fix telemetry from https://github.com/NuGet/NuGet.Client/pull/3786 - [#10439](https://github.com/NuGet/Home/issues/10439)</span></span>

* <span data-ttu-id="38e3c-178">在啟用「RestoreLockedMode」之後建立解決方案時，錯誤 NU1004 消失- [#8973](https://github.com/NuGet/Home/issues/8973)</span><span class="sxs-lookup"><span data-stu-id="38e3c-178">Error NU1004 disappears when building solution after enabling “RestoreLockedMode” - [#8973](https://github.com/NuGet/Home/issues/8973)</span></span>

* <span data-ttu-id="38e3c-179">反向的 PMUI 中的 tab 鍵應向前鏡像 [#10234](https://github.com/NuGet/Home/issues/10234)</span><span class="sxs-lookup"><span data-stu-id="38e3c-179">Tabbing through PMUI in the reverse should mirror forward direction - [#10234](https://github.com/NuGet/Home/issues/10234)</span></span>

* <span data-ttu-id="38e3c-180">在實驗性實例中的 PMUI 錯，有時會從 SolutionView 擲回 InvalidCastException 至 ProjectView- [#10416](https://github.com/NuGet/Home/issues/10416)</span><span class="sxs-lookup"><span data-stu-id="38e3c-180">Debugging PMUI in Experimental Instance sometimes throws InvalidCastException from SolutionView to ProjectView - [#10416](https://github.com/NuGet/Home/issues/10416)</span></span>

* <span data-ttu-id="38e3c-181">在 [流覽] 索引標籤中按一下已淘汰的封裝之後，預設版本是 null- [#10380](https://github.com/NuGet/Home/issues/10380)</span><span class="sxs-lookup"><span data-stu-id="38e3c-181">The default version is null after clicking a deprecated package in Browse tab - [#10380](https://github.com/NuGet/Home/issues/10380)</span></span>

* <span data-ttu-id="38e3c-182">Visual Studio 中的 NuGet 管理員在重新獲得焦點時重載- [#4176](https://github.com/NuGet/Home/issues/4176)</span><span class="sxs-lookup"><span data-stu-id="38e3c-182">The NuGet manager in Visual Studio reloads when focus is regained - [#4176](https://github.com/NuGet/Home/issues/4176)</span></span>

* <span data-ttu-id="38e3c-183">移除 IPackageSourceProvider2 和相關類型- [#10098](https://github.com/NuGet/Home/issues/10098)</span><span class="sxs-lookup"><span data-stu-id="38e3c-183">Remove IPackageSourceProvider2 and related types - [#10098](https://github.com/NuGet/Home/issues/10098)</span></span>

* <span data-ttu-id="38e3c-184">套件 ' NameOfPackage ' 與專案[#5127](https://github.com/NuGet/Home/issues/5127)中的「所有」架構不相容</span><span class="sxs-lookup"><span data-stu-id="38e3c-184">Package 'NameOfPackage' is incompatible with 'all' frameworks in project - [#5127](https://github.com/NuGet/Home/issues/5127)</span></span>

* <span data-ttu-id="38e3c-185">CreateVersionsAsync 不需要 NuGetVersion 比較- [#10436](https://github.com/NuGet/Home/issues/10436)</span><span class="sxs-lookup"><span data-stu-id="38e3c-185">CreateVersionsAsync does unnecessary NuGetVersion Compares - [#10436](https://github.com/NuGet/Home/issues/10436)</span></span>

* <span data-ttu-id="38e3c-186">NuGet。用戶端應該使用 ManagedImageMonikers 取代 KnownMonikers- [#9977](https://github.com/NuGet/Home/issues/9977)</span><span class="sxs-lookup"><span data-stu-id="38e3c-186">NuGet.Client should replace using of ManagedImageMonikers with KnownMonikers - [#9977](https://github.com/NuGet/Home/issues/9977)</span></span>

* <span data-ttu-id="38e3c-187">已淘汰的圖示與 [流覽] 索引標籤中已淘汰的套件版本重迭 [#10452](https://github.com/NuGet/Home/issues/10452)</span><span class="sxs-lookup"><span data-stu-id="38e3c-187">The deprecated icon overlaps with the version of the deprecated package in Browse tab - [#10452](https://github.com/NuGet/Home/issues/10452)</span></span>

* <span data-ttu-id="38e3c-188">PackageReference NU1604 錯誤處理在 VS 和命令列之間不同 (Restore & 封裝管理員 UI) - [#9289](https://github.com/NuGet/Home/issues/9289)</span><span class="sxs-lookup"><span data-stu-id="38e3c-188">PackageReference NU1604 error handling is different across VS and command line (Restore & Package Manager UI) - [#9289](https://github.com/NuGet/Home/issues/9289)</span></span>

* <span data-ttu-id="38e3c-189">Codespaces：未註冊必要的格式器- [#10467](https://github.com/NuGet/Home/issues/10467)</span><span class="sxs-lookup"><span data-stu-id="38e3c-189">Codespaces:  necessary formatters not registered - [#10467](https://github.com/NuGet/Home/issues/10467)</span></span>

* <span data-ttu-id="38e3c-190">從 NuGet 以目標 framework 形式移除 net45。架構- [#10470](https://github.com/NuGet/Home/issues/10470)</span><span class="sxs-lookup"><span data-stu-id="38e3c-190">Remove net45 as as a target framework from NuGet.Frameworks - [#10470](https://github.com/NuGet/Home/issues/10470)</span></span>

* <span data-ttu-id="38e3c-191">執行-新增遙測以追蹤與 PMC 和 Powershell 使用方式相關的事件。</span><span class="sxs-lookup"><span data-stu-id="38e3c-191">Implementation - Add new telemetries to track events related to PMC and Powershell usage.</span></span><span data-ttu-id="38e3c-192"> - [#10142](https://github.com/NuGet/Home/issues/10142)</span><span class="sxs-lookup"><span data-stu-id="38e3c-192"> - [#10142](https://github.com/NuGet/Home/issues/10142)</span></span>

* <span data-ttu-id="38e3c-193">當封裝管理員 UI 中有多個套件可供更新時，[預覽變更] 視窗中只會顯示一個套件： [#10483](https://github.com/NuGet/Home/issues/10483)</span><span class="sxs-lookup"><span data-stu-id="38e3c-193">Only one package shows in the Preview Changes window when there are multiple packages available to update in the Package Manager UI - [#10483](https://github.com/NuGet/Home/issues/10483)</span></span>

* <span data-ttu-id="38e3c-194">封裝 multitargeted 專案時，應該產生空白的 frameworkReferences 群組- [#10218](https://github.com/NuGet/Home/issues/10218)</span><span class="sxs-lookup"><span data-stu-id="38e3c-194">Empty frameworkReferences groups should be generated when packing multitargeted projects - [#10218](https://github.com/NuGet/Home/issues/10218)</span></span>

* <span data-ttu-id="38e3c-195">很難在 [更新] 索引標籤[#8963](https://github.com/NuGet/Home/issues/8963))  (中，流覽 [更新] 索引標籤中的 [套件] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="38e3c-195">Hard to see the check-box of package in ‘Updates’ Tab is focused with a dash-line box when navigating through Tab in Blue/Blue (Extra Contrast)/Light themes - [#8963](https://github.com/NuGet/Home/issues/8963)</span></span>

* <span data-ttu-id="38e3c-196">[更新] 索引標籤核取方塊無法與螢幕讀取器搭配使用- [#10449](https://github.com/NuGet/Home/issues/10449)</span><span class="sxs-lookup"><span data-stu-id="38e3c-196">Updates Tab checkboxes do not work well with screen-readers - [#10449](https://github.com/NuGet/Home/issues/10449)</span></span>

* <span data-ttu-id="38e3c-197">在 PMUI 中更新會導致物件參考未設定為物件的實例- [#9882](https://github.com/NuGet/Home/issues/9882)</span><span class="sxs-lookup"><span data-stu-id="38e3c-197">Updating in PMUI causes Object reference not set to an instance of an object - [#9882](https://github.com/NuGet/Home/issues/9882)</span></span>

* <span data-ttu-id="38e3c-198">執行-新增遙測以追蹤與 PMC 相關的事件，以及後續的 Powershell 使用方式。</span><span class="sxs-lookup"><span data-stu-id="38e3c-198">Implementation - Add new telemetries to track events related to PMC and Powershell usage follow up.</span></span><span data-ttu-id="38e3c-199"> - [#10478](https://github.com/NuGet/Home/issues/10478)</span><span class="sxs-lookup"><span data-stu-id="38e3c-199"> - [#10478](https://github.com/NuGet/Home/issues/10478)</span></span>

* <span data-ttu-id="38e3c-200">V2FeedPackageInfo 中的複製貼上錯誤- [#10480](https://github.com/NuGet/Home/issues/10480)</span><span class="sxs-lookup"><span data-stu-id="38e3c-200">Copy-paste error in V2FeedPackageInfo - [#10480](https://github.com/NuGet/Home/issues/10480)</span></span>

* <span data-ttu-id="38e3c-201">NuGetPackageFileService 修正-使用以取得可處置的 memorystream- [#10503](https://github.com/NuGet/Home/issues/10503)</span><span class="sxs-lookup"><span data-stu-id="38e3c-201">NuGetPackageFileService fix - use using for disposable memorystream - [#10503](https://github.com/NuGet/Home/issues/10503)</span></span>

<span data-ttu-id="38e3c-202">**[此版本修正的所有問題清單-5.9。0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**</span><span class="sxs-lookup"><span data-stu-id="38e3c-202">**[List of all issues fixed in this release - 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**</span></span>

<span data-ttu-id="38e3c-203">**[此版本中的認可清單-5.9。0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**</span><span class="sxs-lookup"><span data-stu-id="38e3c-203">**[List of commits in this release - 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="38e3c-204">社群投稿</span><span class="sxs-lookup"><span data-stu-id="38e3c-204">Community contributions</span></span>

<span data-ttu-id="38e3c-205">感謝所有協助讓此 NuGet 版本絕佳的參與者！</span><span class="sxs-lookup"><span data-stu-id="38e3c-205">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="38e3c-206">人員</span><span class="sxs-lookup"><span data-stu-id="38e3c-206">Who</span></span>|<span data-ttu-id="38e3c-207">Pr</span><span class="sxs-lookup"><span data-stu-id="38e3c-207">PRs</span></span>|<span data-ttu-id="38e3c-208">問題</span><span class="sxs-lookup"><span data-stu-id="38e3c-208">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="38e3c-209">omajid</span><span class="sxs-lookup"><span data-stu-id="38e3c-209">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="38e3c-210">3865</span><span class="sxs-lookup"><span data-stu-id="38e3c-210">3865</span></span>](https://github.com/NuGet/NuGet.Client/pull/3865) | <span data-ttu-id="38e3c-211">V2FeedPackageInfo 中的複製貼上錯誤- [#10480](https://github.com/NuGet/Home/issues/10480)</span><span class="sxs-lookup"><span data-stu-id="38e3c-211">Copy-paste error in V2FeedPackageInfo - [#10480](https://github.com/NuGet/Home/issues/10480)</span></span>
[<span data-ttu-id="38e3c-212">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="38e3c-212">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="38e3c-213">3812</span><span class="sxs-lookup"><span data-stu-id="38e3c-213">3812</span></span>](https://github.com/NuGet/NuGet.Client/pull/3812) | <span data-ttu-id="38e3c-214">遺漏以 PrivateAssets = "All" 屬性參考套件的案例的測試 [#10397](https://github.com/NuGet/Home/issues/10397)</span><span class="sxs-lookup"><span data-stu-id="38e3c-214">Missing tests for the case where packages are referenced with PrivateAssets="All" attribute - [#10397](https://github.com/NuGet/Home/issues/10397)</span></span>
[<span data-ttu-id="38e3c-215">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="38e3c-215">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="38e3c-216">3739</span><span class="sxs-lookup"><span data-stu-id="38e3c-216">3739</span></span>](https://github.com/NuGet/NuGet.Client/pull/3739) | <span data-ttu-id="38e3c-217">新增推送多個套件的支援- [#4393](https://github.com/NuGet/Home/issues/4393)</span><span class="sxs-lookup"><span data-stu-id="38e3c-217">Adding support for pushing multiple packages - [#4393](https://github.com/NuGet/Home/issues/4393)</span></span>
[<span data-ttu-id="38e3c-218">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="38e3c-218">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="38e3c-219">3723</span><span class="sxs-lookup"><span data-stu-id="38e3c-219">3723</span></span>](https://github.com/NuGet/NuGet.Client/pull/3723) | <span data-ttu-id="38e3c-220">停用元件簽署時，NuGet 程式庫的組建會中斷- [#10173](https://github.com/NuGet/Home/issues/10173)</span><span class="sxs-lookup"><span data-stu-id="38e3c-220">Build of NuGet libraries is broken when assembly signing is disabled - [#10173](https://github.com/NuGet/Home/issues/10173)</span></span>
[<span data-ttu-id="38e3c-221">kant2002</span><span class="sxs-lookup"><span data-stu-id="38e3c-221">kant2002</span></span>](https://github.com/kant2002) | [<span data-ttu-id="38e3c-222">3807</span><span class="sxs-lookup"><span data-stu-id="38e3c-222">3807</span></span>](https://github.com/NuGet/NuGet.Client/pull/3807) | <span data-ttu-id="38e3c-223">清除參與的檔- [#10399](https://github.com/NuGet/Home/issues/10399)</span><span class="sxs-lookup"><span data-stu-id="38e3c-223">Clean-up the contributing docs - [#10399](https://github.com/NuGet/Home/issues/10399)</span></span>
[<span data-ttu-id="38e3c-224">PathogenDavid</span><span class="sxs-lookup"><span data-stu-id="38e3c-224">PathogenDavid</span></span>](https://github.com/PathogenDavid) | [<span data-ttu-id="38e3c-225">3754</span><span class="sxs-lookup"><span data-stu-id="38e3c-225">3754</span></span>](https://github.com/NuGet/NuGet.Client/pull/3754) | <span data-ttu-id="38e3c-226">授權和圖示檔案存在檢查應該一律使用區分大小寫的比較- [#9817](https://github.com/NuGet/Home/issues/9817)</span><span class="sxs-lookup"><span data-stu-id="38e3c-226">License and icon file existence check should always use a case-sensitive comparison - [#9817](https://github.com/NuGet/Home/issues/9817)</span></span>
[<span data-ttu-id="38e3c-227">campersau</span><span class="sxs-lookup"><span data-stu-id="38e3c-227">campersau</span></span>](https://github.com/campersau) | [<span data-ttu-id="38e3c-228">3677</span><span class="sxs-lookup"><span data-stu-id="38e3c-228">3677</span></span>](https://github.com/NuGet/NuGet.Client/pull/3677) | <span data-ttu-id="38e3c-229">使用 DecodePixelWidth [#10037](https://github.com/NuGet/Home/issues/10037)時，請使用 BitmapCreateOptions IGNORECOLORPROFILE 解決 WPF 問題</span><span class="sxs-lookup"><span data-stu-id="38e3c-229">Use BitmapCreateOptions.IgnoreColorProfile to workaround WPF issue when using DecodePixelWidth - [#10037](https://github.com/NuGet/Home/issues/10037)</span></span>
[<span data-ttu-id="38e3c-230">bjorkstromm</span><span class="sxs-lookup"><span data-stu-id="38e3c-230">bjorkstromm</span></span>](https://github.com/bjorkstromm) | [<span data-ttu-id="38e3c-231">3697</span><span class="sxs-lookup"><span data-stu-id="38e3c-231">3697</span></span>](https://github.com/NuGet/NuGet.Client/pull/3697) | <span data-ttu-id="38e3c-232">NuGet 中的 Windows SDK 10 連結已中斷。用戶端投稿指南- [#10099](https://github.com/NuGet/Home/issues/10099)</span><span class="sxs-lookup"><span data-stu-id="38e3c-232">Windows SDK 10 link is broken in NuGet.Client Contribution guide - [#10099](https://github.com/NuGet/Home/issues/10099)</span></span>
[<span data-ttu-id="38e3c-233">bjorkstromm</span><span class="sxs-lookup"><span data-stu-id="38e3c-233">bjorkstromm</span></span>](https://github.com/bjorkstromm) | [<span data-ttu-id="38e3c-234">3696</span><span class="sxs-lookup"><span data-stu-id="38e3c-234">3696</span></span>](https://github.com/NuGet/NuGet.Client/pull/3696) | <span data-ttu-id="38e3c-235">NuGet 中的相對連結已中斷。用戶端偵測指南- [#10100](https://github.com/NuGet/Home/issues/10100)</span><span class="sxs-lookup"><span data-stu-id="38e3c-235">Relative links are broken in NuGet.Client debugging guide - [#10100](https://github.com/NuGet/Home/issues/10100)</span></span>
[<span data-ttu-id="38e3c-236">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="38e3c-236">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="38e3c-237">3637</span><span class="sxs-lookup"><span data-stu-id="38e3c-237">3637</span></span>](https://github.com/NuGet/NuGet.Client/pull/3637) | <span data-ttu-id="38e3c-238">改善測試元件和相關的程式碼- [#9996](https://github.com/NuGet/Home/issues/9996)</span><span class="sxs-lookup"><span data-stu-id="38e3c-238">Improve test fixtures and related code - [#9996](https://github.com/NuGet/Home/issues/9996)</span></span>
[<span data-ttu-id="38e3c-239">rolfbjarne</span><span class="sxs-lookup"><span data-stu-id="38e3c-239">rolfbjarne</span></span>](https://github.com/rolfbjarne) | [<span data-ttu-id="38e3c-240">3743</span><span class="sxs-lookup"><span data-stu-id="38e3c-240">3743</span></span>](https://github.com/NuGet/NuGet.Client/pull/3743) | <span data-ttu-id="38e3c-241">當重新導向時，輸出會在 macOS 上以80個字元包裝： [#10198](https://github.com/NuGet/Home/issues/10198)</span><span class="sxs-lookup"><span data-stu-id="38e3c-241">Output is wrapped at 80 characters on macOS when redirected - [#10198](https://github.com/NuGet/Home/issues/10198)</span></span>
[<span data-ttu-id="38e3c-242">xen2</span><span class="sxs-lookup"><span data-stu-id="38e3c-242">xen2</span></span>](https://github.com/xen2) | [<span data-ttu-id="38e3c-243">2861</span><span class="sxs-lookup"><span data-stu-id="38e3c-243">2861</span></span>](https://github.com/NuGet/NuGet.Client/pull/2861) | <span data-ttu-id="38e3c-244">讓 Nuget.exe 以 .NET Standard 套件的形式提供- [#6150](https://github.com/NuGet/Home/issues/6150)</span><span class="sxs-lookup"><span data-stu-id="38e3c-244">Make NuGet.PackageManagement available as a .NET Standard package - [#6150](https://github.com/NuGet/Home/issues/6150)</span></span>
[<span data-ttu-id="38e3c-245">Anipik</span><span class="sxs-lookup"><span data-stu-id="38e3c-245">Anipik</span></span>](https://github.com/Anipik) | [<span data-ttu-id="38e3c-246">3810</span><span class="sxs-lookup"><span data-stu-id="38e3c-246">3810</span></span>](https://github.com/NuGet/NuGet.Client/pull/3810) | <span data-ttu-id="38e3c-247">引進新的 msbuild 屬性，在 pack 工作期間排除特定 tfm 的組建輸出- [#10396](https://github.com/NuGet/Home/issues/10396)</span><span class="sxs-lookup"><span data-stu-id="38e3c-247">Introduce a new msbuild property to exclude build output for specific tfms during pack task - [#10396](https://github.com/NuGet/Home/issues/10396)</span></span>

## <a name="summary-whats-new-in-591"></a><span data-ttu-id="38e3c-248">摘要：5.9.1 的新功能</span><span class="sxs-lookup"><span data-stu-id="38e3c-248">Summary: What's New in 5.9.1</span></span>

* <span data-ttu-id="38e3c-249">「dotnet nuget 移除來源 nuget.org」無法在第一次使用 [#10745](https://github.com/NuGet/Home/issues/10745)</span><span class="sxs-lookup"><span data-stu-id="38e3c-249">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>
* <span data-ttu-id="38e3c-250">在 Linux 上將預設驗證設為停用，但在 Windows 上預設為啟用- [#10713](https://github.com/NuGet/Home/issues/10713)</span><span class="sxs-lookup"><span data-stu-id="38e3c-250">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

<span data-ttu-id="38e3c-251">**[此版本修正的所有問題清單-5.9。1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**</span><span class="sxs-lookup"><span data-stu-id="38e3c-251">**[List of all issues fixed in this release - 5.9.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f42efd068017639b4036)**</span></span>

<span data-ttu-id="38e3c-252">**[此版本中的認可清單-5.9。1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**</span><span class="sxs-lookup"><span data-stu-id="38e3c-252">**[List of commits in this release - 5.9.1](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.9.1.8)**</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="38e3c-253">歡迎意見反應</span><span class="sxs-lookup"><span data-stu-id="38e3c-253">Feedback welcome</span></span>

<span data-ttu-id="38e3c-254">您的意見反應對我們非常寶貴。</span><span class="sxs-lookup"><span data-stu-id="38e3c-254">Your feedback is important to us.</span></span>  <span data-ttu-id="38e3c-255">如果此版本有任何問題，請查看我們的 [GitHub 問題](https://github.com/NuGet/Home/issues) ，並 [Visual Studio 開發人員社群](https://developercommunity.visualstudio.com/) 現有的問題。</span><span class="sxs-lookup"><span data-stu-id="38e3c-255">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="38e3c-256">針對 NuGet 內的新問題，請報告 [GitHub 問題](https://github.com/NuGet/Home/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="38e3c-256">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="38e3c-257">如需一般的 NuGet 體驗問題，請透過 [說明] 下您最愛的 IDE 中的 [回報 [問題](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) ] 選項，讓我們知道 **> 報告問題**。</span><span class="sxs-lookup"><span data-stu-id="38e3c-257">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
