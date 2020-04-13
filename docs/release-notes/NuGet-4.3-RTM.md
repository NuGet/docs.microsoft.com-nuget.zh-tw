---
title: NuGet 4.3 RTM 版本資訊
description: NuGet 4.3 RTM 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496597"
---
# <a name="nuget-43-release-notes"></a><span data-ttu-id="3c817-103">NuGet 4.3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="3c817-103">NuGet 4.3 Release Notes</span></span>

<span data-ttu-id="3c817-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附有 NuGet 4.3 RTM，它新增新案例的支援，例如 .NET Standard 2.0/.NET Core 2.0、包含許多品質修正，並且改善效能。</span><span class="sxs-lookup"><span data-stu-id="3c817-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="3c817-105">此版本也帶來數項改善，像是支援語意化版本控制系統 2.0.0、NuGet 警告和錯誤的 MSBuild 整合等等。</span><span class="sxs-lookup"><span data-stu-id="3c817-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="summary-whats-new-in-430"></a><span data-ttu-id="3c817-106">摘要:4.3.0 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="3c817-106">Summary: What's New in 4.3.0</span></span>

## <a name="summary-whats-new-in-431"></a><span data-ttu-id="3c817-107">摘要:4.3.1 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="3c817-107">Summary: What's New in 4.3.1</span></span>

* <span data-ttu-id="3c817-108">安全修復:在 #/.nuget 中創建的檔案的許可權在[CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673)太開放</span><span class="sxs-lookup"><span data-stu-id="3c817-108">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>
* <span data-ttu-id="3c817-109">安全修復:NUPKG 內部的檔可以在 NUPKG 目錄上方具有相對路徑[#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="3c817-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="3c817-110">已知問題</span><span class="sxs-lookup"><span data-stu-id="3c817-110">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="3c817-111">在某些情況下，NuGet restore 會將已停用的套件來源視為已啟用</span><span class="sxs-lookup"><span data-stu-id="3c817-111">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="3c817-112">問題</span><span class="sxs-lookup"><span data-stu-id="3c817-112">Issue</span></span>

<span data-ttu-id="3c817-113">下列 restore 命令列技術會將已停用的套件視為已啟用。</span><span class="sxs-lookup"><span data-stu-id="3c817-113">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="3c817-114">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="3c817-114">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="3c817-115">`dotnet restore` (可能出現在 VS 或 NetCore SDK 2.0.0 所隨附的 dotnet.exe)</span><span class="sxs-lookup"><span data-stu-id="3c817-115">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="3c817-116">因應措施</span><span class="sxs-lookup"><span data-stu-id="3c817-116">Workaround</span></span>

1. <span data-ttu-id="3c817-117">使用 Visual Studio (2017 15.3 或更新版本) 或 NuGet.exe (v4.3.0 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="3c817-117">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="3c817-118">刪除已停用的來源，然後繼續使用 msbuild 或 dotnet.exe。</span><span class="sxs-lookup"><span data-stu-id="3c817-118">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="3c817-119">對於您的解決方案，您可以在 NuGet.config 中使用 "Clear"，然後定義該解決方案的必要來源。</span><span class="sxs-lookup"><span data-stu-id="3c817-119">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="3c817-120">使用套件管理員主控台時，'Enter' 鍵可能無法運作</span><span class="sxs-lookup"><span data-stu-id="3c817-120">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="3c817-121">問題</span><span class="sxs-lookup"><span data-stu-id="3c817-121">Issue</span></span>

<span data-ttu-id="3c817-122">有時候，Enter 鍵無法在套件管理員主控台中運作。</span><span class="sxs-lookup"><span data-stu-id="3c817-122">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="3c817-123">如果您遇到此問題，請查看本修正的進度，並針對您的重新產生步驟提供任何有用的資訊。</span><span class="sxs-lookup"><span data-stu-id="3c817-123">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="3c817-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="3c817-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="3c817-125">因應措施</span><span class="sxs-lookup"><span data-stu-id="3c817-125">Workaround</span></span>

<span data-ttu-id="3c817-126">重新啟動 Visual Studio 並在開啟解決方案之前開啟 PMC。</span><span class="sxs-lookup"><span data-stu-id="3c817-126">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="3c817-127">或者，嘗試刪除 `project.lock.json` 並再次還原。</span><span class="sxs-lookup"><span data-stu-id="3c817-127">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="3c817-128">您無法使用 NuGet 套件管理員檢視、新增或更新 DotNetCLITools</span><span class="sxs-lookup"><span data-stu-id="3c817-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="3c817-129">問題</span><span class="sxs-lookup"><span data-stu-id="3c817-129">Issue</span></span>

<span data-ttu-id="3c817-130">NuGet 套件管理員沒有顯示，而且不允許加入/更新 DotNetCLITools。</span><span class="sxs-lookup"><span data-stu-id="3c817-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="3c817-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="3c817-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="3c817-132">因應措施</span><span class="sxs-lookup"><span data-stu-id="3c817-132">Workaround</span></span>

<span data-ttu-id="3c817-133">您必須在專案檔中手動編輯 DotNetCLIToolReferences。</span><span class="sxs-lookup"><span data-stu-id="3c817-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="3c817-134">重定目標 Framework 版本可能會導致不完整的 Intellisense</span><span class="sxs-lookup"><span data-stu-id="3c817-134">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="3c817-135">問題</span><span class="sxs-lookup"><span data-stu-id="3c817-135">Issue</span></span>

<span data-ttu-id="3c817-136">在 Visual Studio 中重定目標 Framework 版本可能會導致不完整的 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="3c817-136">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="3c817-137">當您使用 PackageReferences 作為套件管理員格式時，就會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="3c817-137">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="3c817-138">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="3c817-138">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="3c817-139">因應措施</span><span class="sxs-lookup"><span data-stu-id="3c817-139">Workaround</span></span>

<span data-ttu-id="3c817-140">請執行手動還原。</span><span class="sxs-lookup"><span data-stu-id="3c817-140">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="3c817-141">NuGet 4.3 RTM 時間範圍中已修正的問題</span><span class="sxs-lookup"><span data-stu-id="3c817-141">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="3c817-142">[NuGet 4.0 RTM 版本資訊](../release-notes/nuget-4.0-RTM.md) - 列出所有 NuGet 4.0 RTM 修正的問題</span><span class="sxs-lookup"><span data-stu-id="3c817-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="3c817-143">特性</span><span class="sxs-lookup"><span data-stu-id="3c817-143">Features</span></span>

- <span data-ttu-id="3c817-144">改善 NuGet 還原效能 - 針對命令列還原作業和 VS 實作更聰明的 NoOp - [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="3c817-144">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="3c817-145">NET Core 2.0：VS/Dotnet CLI 應該開始使用現有的 NuGet 功能：回溯資料夾 - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="3c817-145">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="3c817-146">NET Core 2.0：讓使用者能略過特定的還原警告 (或提高至錯誤) - [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="3c817-146">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="3c817-147">NET Core 2.0：CLI 當地語系化組件 - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="3c817-147">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="3c817-148">NET Core 2.0：向資產檔案註冊所有警告/錯誤 (包括 PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="3c817-148">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="3c817-149">啟用 TFM 支援：NetStandard2.0、Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="3c817-149">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="3c817-150">減少 NuGet.Core 和 NuGet.Client 專案數 (以及 DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="3c817-150">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="3c817-151">新增將 Nuget 警告標記為錯誤的功能 - [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="3c817-151">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="3c817-152">Bug</span><span class="sxs-lookup"><span data-stu-id="3c817-152">Bugs</span></span>

- <span data-ttu-id="3c817-153">msbuild /t:pack 失敗，因為 "PackTask" 工作不支援 "DevelopmentDependency" 參數 - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="3c817-153">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="3c817-154">如果不在 PackagePath 結尾處新增 Windows 目錄分隔符號，則為壓平合併的內容檔案目錄結構 - [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="3c817-154">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="3c817-155">netcore 專案不支援設定為 developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="3c817-155">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="3c817-156">同步載入 RestoreManagerPackage，這會封鎖 UI 執行緒並使 VS 鎖死 - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="3c817-156">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="3c817-157">dotnet</span><span class="sxs-lookup"><span data-stu-id="3c817-157">dotnet</span></span>
  - <span data-ttu-id="3c817-158">dotnetcore Restore (以及 msbuild /t:restore) 會略過具有明確方案專案相依性的專案 [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="3c817-158">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="3c817-159">如果解決方案中有參考到相同專案的 projectreferences、有不同的大小寫，還原可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="3c817-159">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="3c817-160">這也會影響大小寫沒有差異的不同相對路徑 - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="3c817-160">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="3c817-161">從 NuGet 套件還原的可執行檔，無法再與 .NET Core 2.0 搭配執行 - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="3c817-161">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="3c817-162">NuGet.exe 在剖析解決方案檔時會抑制例外狀況的詳細資料 - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="3c817-162">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="3c817-163">在 Windows 上，如果 ContentTargetFolders 包含結尾使用 '/' 的路徑，組件會將內容檔案放在錯誤的位置 - [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="3c817-163">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="3c817-164">無法為以 netcoreapp1.1 為目標的工具套件還原 DotNetCliToolReference - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="3c817-164">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="3c817-165">Nuget 更新 CLI 在專案檔中留下舊的套件版本條件 (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="3c817-165">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="3c817-166">DCR</span><span class="sxs-lookup"><span data-stu-id="3c817-166">DCRs</span></span>

- <span data-ttu-id="3c817-167">從 CPS nomation 讀取 DotnetCliToolTargetFramework - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="3c817-167">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="3c817-168">專案樣式 UWP 的 TPMinV 檢查應該能運作 - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="3c817-168">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="3c817-169">改善自動參考套件的 UI 描述 - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="3c817-169">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="3c817-170">NuGet 還原從執行階段欄位區段選取編譯資產。</span><span class="sxs-lookup"><span data-stu-id="3c817-170">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="3c817-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="3c817-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="3c817-172">相依性診斷放在鎖定檔中 - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="3c817-172">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="3c817-173">4.3 RTM 中已修正之 GitHub 問題的連結</span><span class="sxs-lookup"><span data-stu-id="3c817-173">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="3c817-174">問題清單</span><span class="sxs-lookup"><span data-stu-id="3c817-174">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
