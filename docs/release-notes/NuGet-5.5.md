---
title: NuGet 5.5 版本資訊
description: NuGet 5.5 的版本資訊，包括新功能、bug 修正及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780108"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="fae54-103">NuGet 5.5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="fae54-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="fae54-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="fae54-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="fae54-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="fae54-105">NuGet version</span></span> | <span data-ttu-id="fae54-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="fae54-106">Available in Visual Studio version</span></span>| <span data-ttu-id="fae54-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="fae54-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="fae54-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="fae54-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="fae54-109">Visual Studio 2019 16.5 版</span><span class="sxs-lookup"><span data-stu-id="fae54-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="fae54-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="fae54-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="fae54-111"><sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="fae54-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="fae54-112">摘要：5.5 中的新功能</span><span class="sxs-lookup"><span data-stu-id="fae54-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="fae54-113">改善 Visual Studio 中 NuGet 套件管理員 UI 的協助工具和螢幕讀取程式體驗</span><span class="sxs-lookup"><span data-stu-id="fae54-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="fae54-114">螢幕閱讀程式體驗中的協助工具問題，已安裝的文字方塊缺少 altText 和可存取的名稱，以及- [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="fae54-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="fae54-115">套件清單中螢幕閱讀程式體驗的協助工具問題- [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="fae54-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="fae54-116">與 [流覽]、[安裝]、[更新] 索引標籤相關的螢幕閱讀程式體驗中的協助工具問題- [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="fae54-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="fae54-117">朗讀程式未宣告「空白」、「沒有 Dependencies"、key org」、「MIT」連結標籤 [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="fae54-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="fae54-118">支援在 Visual Studio 套件管理員 UI 中，為裝載于本機摘要上的套件呈現獨立的圖示- [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="fae54-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="fae54-119">藉 `RestoreUseStaticGraphEvaluation` 由呼叫 MSBuild 靜態圖形 api 來加速評估，以大幅改善無作業還原效能- [8791](https://github.com/NuGet/Home/issues/8791)</span><span class="sxs-lookup"><span data-stu-id="fae54-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="fae54-120">使用跨平臺驗證外掛程式改善 dotnet.exe 可靠性</span><span class="sxs-lookup"><span data-stu-id="fae54-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="fae54-121">dotnet restore 失敗並出現 TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="fae54-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="fae54-122">外掛程式：「工作已取消」-ADO 驗證的問題，原因如下。</span><span class="sxs-lookup"><span data-stu-id="fae54-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="fae54-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="fae54-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="fae54-124">新增 `dotnet nuget <add|remove|update|disable|enable|list> source` 命令- [#4126](https://github.com/NuGet/Home/issues/4126)</span><span class="sxs-lookup"><span data-stu-id="fae54-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="fae54-125">`--skip-duplicate`使用 dotnet nuget push [#8778](https://github.com/NuGet/Home/issues/8778)的支援</span><span class="sxs-lookup"><span data-stu-id="fae54-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="fae54-126">支援 `packages.config` msbuild/restore- [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="fae54-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="fae54-127">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="fae54-127">Issues fixed in this release</span></span>

<span data-ttu-id="fae54-128">**Bug**</span><span class="sxs-lookup"><span data-stu-id="fae54-128">**Bugs**</span></span>

* <span data-ttu-id="fae54-129">使用 V3 Api 修改 Self-Updater- [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="fae54-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="fae54-130">套件相依性版本設定為 ' \* ' 時，錯誤的套件相依性版本- [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="fae54-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="fae54-131">ErrorUnsafePackageEntry 錯誤訊息未指向問題來源- [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="fae54-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="fae54-132">「\*」案例中不接受鎖定檔案- [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="fae54-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="fae54-133">在 PackageReference 中使用 \* 時，NuGet.exe 無法解析為最新版本的套件 (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="fae54-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="fae54-134">具有多目標 WPF 專案的 dotnet 清單套件- [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="fae54-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="fae54-135">改善 ConcurrencyUtilities (降低 CPU 使用量) - [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="fae54-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="fae54-136">已卸載專案案例的 DG 規格不應以預覽還原來撰寫- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="fae54-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="fae54-137">Visual Studio NuGet 套件 (RestoreManagerPackage) 必須在解決方案組建事件上自動載入- [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="fae54-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="fae54-138">.Vssettings init 中的鎖死- [#8842](https://github.com/NuGet/Home/issues/8842)</span><span class="sxs-lookup"><span data-stu-id="fae54-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="fae54-139">如果專案放置於方案資料夾中，則不會從 NuGet 套件填入 VisualStudio 工具箱- [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="fae54-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="fae54-140">VS：解決方案還原永久因競爭條件而失敗- [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="fae54-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="fae54-141">[已安裝] 索引標籤上的 [正在載入 ...] 常數，以及搜尋</span><span class="sxs-lookup"><span data-stu-id="fae54-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="fae54-142">[更新] 索引標籤上的 [更新] 索引標籤 [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="fae54-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="fae54-143">快取到期之後，VS PM UI 中缺少內嵌的圖示- [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="fae54-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="fae54-144">FireAndForget PM UI 啟動- [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="fae54-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="fae54-145">Restore： IncludeExcludeFiles. Equals ( ... ) 執行不正確- [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="fae54-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="fae54-146">Restore： PackageSpec. Clone ( # A1 建立不相等的複製- [#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="fae54-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="fae54-147">未核取 [如果組建完成但發生錯誤時一律顯示錯誤清單]，所顯示的錯誤清單- [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="fae54-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="fae54-148">靜態圖形還原不應傳遞空的 SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061)</span><span class="sxs-lookup"><span data-stu-id="fae54-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="fae54-149">還原：每個專案4次計算的關閉次數- [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="fae54-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="fae54-150">Restore： DependencyGraphSpec Load ( ... ) 不需要 JObject- [#9040](https://github.com/NuGet/Home/issues/9040)</span><span class="sxs-lookup"><span data-stu-id="fae54-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="fae54-151">還原：在大型物件堆積上建立的大型字串 (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="fae54-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="fae54-152">新 mono 的自訂 nuget.exe 可能會因 MSBuild SDK 解析程式而中斷- [8848](https://github.com/NuGet/Home/issues/8848)</span><span class="sxs-lookup"><span data-stu-id="fae54-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="fae54-153">當 nuget.dgspec.js為「由另一個進程使用中」時，restore 會失敗- [8692](https://github.com/NuGet/Home/issues/8692)</span><span class="sxs-lookup"><span data-stu-id="fae54-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="fae54-154">**DCR**</span><span class="sxs-lookup"><span data-stu-id="fae54-154">**DCRs**</span></span>

* <span data-ttu-id="fae54-155">_GetRestoreProjectStyle 中的邏輯應該在工作中 [#8804](https://github.com/NuGet/Home/issues/8804)</span><span class="sxs-lookup"><span data-stu-id="fae54-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="fae54-156">預設會在 [已安裝] 索引標籤上新增取代資訊- [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="fae54-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="fae54-157">**[此版本修正的所有問題清單-5。5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="fae54-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
