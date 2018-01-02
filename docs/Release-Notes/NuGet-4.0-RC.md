---
title: "NuGet 4.0 RC 版本資訊 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/17/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: fa64825d-5908-4abe-9792-d70766d6e2ff
description: "NuGet 4.0 RC 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。"
keywords: "NuGet 4.0 RC 版本資訊, Bug 修正, 已知問題, 新增功能, DCR"
ms.reviewer: kraigb
ms.openlocfilehash: aa1c43be7ac0640bb5e118a162616acb36d44a83
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="40-rc-release-notes"></a><span data-ttu-id="046f4-104">4.0 RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="046f4-104">4.0 RC Release Notes</span></span>

[<span data-ttu-id="046f4-105">NuGet 3.5 RTM 版本資訊</span><span class="sxs-lookup"><span data-stu-id="046f4-105">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="046f4-106">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) 著重於新增 .NET Core 案例支援、處理重要客戶意見，以及改善各種案例中的效能。</span><span class="sxs-lookup"><span data-stu-id="046f4-106">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="046f4-107">此版本帶來幾項改善，像是支援 PackageReference，以及 MSBuild 目標、背景套件還原等多項 NuGet 命令。</span><span class="sxs-lookup"><span data-stu-id="046f4-107">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="046f4-108">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="046f4-108">Bug Fixes</span></span>

* <span data-ttu-id="046f4-109">`dotnet pack --version-suffix foo` 中的行為變更  - [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="046f4-109">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

* <span data-ttu-id="046f4-110">僅有 vs "15" 電腦上的 nuget.exe restore 失敗 - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="046f4-110">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

* <span data-ttu-id="046f4-111">.NETCore 檔案新專案應該在還原期間封鎖組建 - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="046f4-111">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

* <span data-ttu-id="046f4-112">無法還原從 VS2015 移轉至 VS "15" 的 ASP.NET Core Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="046f4-112">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="046f4-113"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="046f4-113"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

* <span data-ttu-id="046f4-114">[測試失敗] PM UI 無法解除安裝套件「jQuery 驗證」- [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="046f4-114">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

* <span data-ttu-id="046f4-115">將套件安裝至 UWP `project.json` 時，也應該還原父專案 - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="046f4-115">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

* <span data-ttu-id="046f4-116">修改 NuGet 目標以將套件來源記錄為高詳細資訊，而非標準 - [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="046f4-116">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

* <span data-ttu-id="046f4-117">dotnet pack3 預設應該會包含 XML 文件 - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="046f4-117">dotnet pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

* <span data-ttu-id="046f4-118">從沒有套件的來源並選取所有來源時，從 UI 的批次更新會失敗 - [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="046f4-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

* <span data-ttu-id="046f4-119">Nuget pack 命令不會包含所有檔案 - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="046f4-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

* <span data-ttu-id="046f4-120">OOM 問題 - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="046f4-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

* <span data-ttu-id="046f4-121">資產檔案的 ProjectFileDependencyGroups 區段應該使用專案的程式庫名稱 - [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="046f4-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

* <span data-ttu-id="046f4-122">"dotnet restore" 和遞迴目錄 - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="046f4-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

* <span data-ttu-id="046f4-123">Restore3 失敗會記錄為警告，而非錯誤 - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="046f4-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

* <span data-ttu-id="046f4-124">TFS 問題：「在您的工作區中找不到 [file]，或您沒有其存取權限」- [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="046f4-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

* <span data-ttu-id="046f4-125">在 vs 快速啟動搜尋方塊中鍵入 "nuget <packagename>" 會保留 "nuget " 前置詞 - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="046f4-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

* <span data-ttu-id="046f4-126">System.Xml.XmlException: 在 Core Properties 部分發現無法識別的根項目。</span><span class="sxs-lookup"><span data-stu-id="046f4-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="046f4-127">行 2，位置 2。</span><span class="sxs-lookup"><span data-stu-id="046f4-127">Line 2, position 2.</span></span><span data-ttu-id="046f4-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="046f4-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

* <span data-ttu-id="046f4-129">不再建置文字欄位中含逸出 &lt; 或 &gt; 的`.nuspec` - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="046f4-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

* <span data-ttu-id="046f4-130">nuget.exe delete 不會提示您輸入認證 (它是非互動模式) - [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="046f4-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

* <span data-ttu-id="046f4-131">nuget.exe delete 會警告本機來源的 API 金鑰，即使沒有任何意義也是一樣 - [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="046f4-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

* <span data-ttu-id="046f4-132">安裝 EF 時錯誤體驗不佳 -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="046f4-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

* <span data-ttu-id="046f4-133">在套件管理員中變更選取範圍之後，Visual Studio 讓嘗試損毀 - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="046f4-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

* <span data-ttu-id="046f4-134">使用浮動版本時，dotnet restore 會對一般清單本機存放庫執行區分大小寫識別碼查閱 - [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="046f4-134">Dotnet restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

* <span data-ttu-id="046f4-135">中斷 V2 摘要的 nuget.exe delete - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="046f4-135">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

* <span data-ttu-id="046f4-136">nuget.exe push timeout 需要較佳的錯誤訊息 - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="046f4-136">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

* <span data-ttu-id="046f4-137">沒有適當匯入的工具還原會以無訊息模式失敗。</span><span class="sxs-lookup"><span data-stu-id="046f4-137">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="046f4-138"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="046f4-138"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

* <span data-ttu-id="046f4-139">有私人摘要時，NuGet 會提示輸入認證，即使從 nuget.org 安裝時也是一樣 - [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="046f4-139">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

* <span data-ttu-id="046f4-140">ApplicationInsights 2.0 套件已列出，但尚未存在 - [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="046f4-140">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

* <span data-ttu-id="046f4-141">VS "15" Preview 5 分支中的 UIDelay - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="046f4-141">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

* <span data-ttu-id="046f4-142">在 UWP 建置期間遺漏還原的第一個 OnBuild 事件 - [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="046f4-142">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

* <span data-ttu-id="046f4-143">PowerShell5 中斷 EntityFramework 安裝？</span><span class="sxs-lookup"><span data-stu-id="046f4-143">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="046f4-144"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="046f4-144"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

* <span data-ttu-id="046f4-145">將來源新增至詳細記錄 (請考慮用於 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="046f4-145">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

* <span data-ttu-id="046f4-146">nuget 用戶端版本 3.4+ 不支援 NoCache 參數 - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="046f4-146">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

* <span data-ttu-id="046f4-147">VS 中無法載入認證提供者時，不會中斷 NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="046f4-147">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>


## <a name="features"></a><span data-ttu-id="046f4-148">功能</span><span class="sxs-lookup"><span data-stu-id="046f4-148">Features</span></span>

* <span data-ttu-id="046f4-149">設定 CI 執行 x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="046f4-149">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

* <span data-ttu-id="046f4-150">自動還原 3/3：非封鎖 UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="046f4-150">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

* <span data-ttu-id="046f4-151">自動還原 2/3：提名時的背景還原 - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="046f4-151">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

* <span data-ttu-id="046f4-152">還原專案參考以符合建置行為 (遞迴) - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="046f4-152">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

* <span data-ttu-id="046f4-153">VS "15" 中的 DPL 支援 - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="046f4-153">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

* <span data-ttu-id="046f4-154">將設定檔移至 Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="046f4-154">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

* <span data-ttu-id="046f4-155">產生的還原屬性和目標需要跨目標參與支援 - [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="046f4-155">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

* <span data-ttu-id="046f4-156">PackageTargetFallback 的 NuGet Restore 支援 (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="046f4-156">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

* <span data-ttu-id="046f4-157">ToolsRef 實作 - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="046f4-157">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

* <span data-ttu-id="046f4-158">RID 的 Restore3 - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="046f4-158">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

* <span data-ttu-id="046f4-159">支援新增/移除/更新 PackageRefs 的 NuGet UI - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="046f4-159">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

* <span data-ttu-id="046f4-160">自動還原 1/3：透過快取專案還原資訊的提名 API 實作 - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="046f4-160">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

* <span data-ttu-id="046f4-161">[0] NuGet Restore 工作和目標 - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="046f4-161">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

* <span data-ttu-id="046f4-162">[1] 在 MSBuild 中啟用方案層級還原 - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="046f4-162">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

* <span data-ttu-id="046f4-163">Visual Studio 中支援認證提供者公用擴充性 - [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="046f4-163">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

* <span data-ttu-id="046f4-164">遞迴 nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="046f4-164">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

* <span data-ttu-id="046f4-165">無法在 dev15 上載入 Microsoft.TeamFoundation.Client，需要將 VS "15" Preview 的 Microsoft.TeamFoundation.Client 版本更新為 15.0 - [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="046f4-165">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

* <span data-ttu-id="046f4-166">在 VS "15" Preview 中，無法將 C++ 套件安裝至 C++ UWP 專案 - [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="046f4-166">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

* <span data-ttu-id="046f4-167">Nupkg 需要支援 \buildCrossTargeting\ 資料夾 - 以及匯入 `.targets` / `.props` 來「跨目標設為」MSBuild 範圍。</span><span class="sxs-lookup"><span data-stu-id="046f4-167">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="046f4-168"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="046f4-168"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

* <span data-ttu-id="046f4-169">ToolsReference 設計 - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="046f4-169">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

* <span data-ttu-id="046f4-170">修正 NuGet UI 以支援 `.csproj` 中含 PackageReferences 的 restore - [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="046f4-170">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

* <span data-ttu-id="046f4-171">將清除快取按鈕新增至 VS 套件管理員設定 - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="046f4-171">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="046f4-172">DCR</span><span class="sxs-lookup"><span data-stu-id="046f4-172">DCRs</span></span>

* <span data-ttu-id="046f4-173">進行自動還原時，應該會封鎖方案還原。</span><span class="sxs-lookup"><span data-stu-id="046f4-173">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="046f4-174"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="046f4-174"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

* <span data-ttu-id="046f4-175">NuGet 套件管理員 UI 中的 NetCore install 會安裝到每個 TFM，而不是套件所支援的 TFM - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="046f4-175">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

* <span data-ttu-id="046f4-176">還原提名者 API 也需要支援 DotNetCliToolsReferences。</span><span class="sxs-lookup"><span data-stu-id="046f4-176">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="046f4-177"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="046f4-177"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

* <span data-ttu-id="046f4-178">將 VS "15" vsix 標示為 systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="046f4-178">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

* <span data-ttu-id="046f4-179">從參考 MS.VS.Services.Client 移轉至 MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="046f4-179">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

* <span data-ttu-id="046f4-180">restore 應該在專案層級使用 $(RestoreLegacyPackagesDirectory) - [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="046f4-180">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

* <span data-ttu-id="046f4-181">還原至含單一 TargetFramework 的專案不得設定屬性條件 - [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="046f4-181">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

* <span data-ttu-id="046f4-182">dotnet restore3 foo.csproj 應該遵循 projectref 相依性，同時還原這些相依性。</span><span class="sxs-lookup"><span data-stu-id="046f4-182">dotnet restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="046f4-183">例如組建。</span><span class="sxs-lookup"><span data-stu-id="046f4-183">Like build.</span></span><span data-ttu-id="046f4-184"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="046f4-184"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

* <span data-ttu-id="046f4-185">在鎖定檔案中，"type": "platform" 相依性呈現為 "type":"package" - [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="046f4-185">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

* <span data-ttu-id="046f4-186">nuget.exe 詳細資訊模式應該顯示下載 URL - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="046f4-186">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

* <span data-ttu-id="046f4-187">將 NuGet xplat 移至 Microsoft.NetCore.App 和 netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="046f4-187">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

* <span data-ttu-id="046f4-188">推送 - 從命令列推送時，應該可以覆寫符號伺服器 - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="046f4-188">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

* <span data-ttu-id="046f4-189">合併用於尋找全域套件路徑的程式碼 - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="046f4-189">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

* <span data-ttu-id="046f4-190">需要比 suppressParent 更適合的名稱 - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="046f4-190">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

* <span data-ttu-id="046f4-191">判斷要用於 MSBuild 專案的 `project.json` 相依性名稱 - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="046f4-191">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

* <span data-ttu-id="046f4-192">將 SemVer 2.0.0 支援新增至 NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="046f4-192">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

* <span data-ttu-id="046f4-193">允許可在 MSBuild 中使用 `.targets` 的可轉移相依性 NuPkg - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="046f4-193">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

* <span data-ttu-id="046f4-194">命令列中的 NuGet restore 明顯比 VS 還要慢 - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="046f4-194">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

* <span data-ttu-id="046f4-195">將套件識別碼和版本比較設為不區分大小寫 - [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="046f4-195">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

* <span data-ttu-id="046f4-196">NoCache 選項不適用於 `packages.config` 型 restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="046f4-196">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

* <span data-ttu-id="046f4-197">FindPackageByIdResource 資源需要預設快取內容和記錄器 - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="046f4-197">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
