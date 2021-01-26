---
title: 3.5 RC 版本資訊
description: NuGet 3.5 RC 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780195"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="b9af8-103">NuGet 3.5 RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="b9af8-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="b9af8-104">[NuGet 3.5-Beta2 版本](../release-notes/nuget-3.5-Beta2.md)  |  資訊[NuGet 3.5-RTM 版本](../release-notes/nuget-3.5-RTM.md)資訊</span><span class="sxs-lookup"><span data-stu-id="b9af8-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="b9af8-105">3.5 版著重于改善 NuGet 用戶端的品質和效能。</span><span class="sxs-lookup"><span data-stu-id="b9af8-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="b9af8-106">此外，我們也提供了一些功能，例如支援回溯 [資料夾](https://github.com/NuGet/Home/issues/2899)、 [PackageType](https://github.com/NuGet/Home/issues/2476) 支援 `.nuspec` 等等。</span><span class="sxs-lookup"><span data-stu-id="b9af8-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="b9af8-107">問題清單</span><span class="sxs-lookup"><span data-stu-id="b9af8-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="b9af8-108">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="b9af8-108">Bug Fixes</span></span>

* <span data-ttu-id="b9af8-109">套件的安裝/還原失敗，並出現「封裝包含多個檔案」 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="b9af8-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="b9af8-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="b9af8-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="b9af8-111">無論什麼 #3203，nuget 套件都會強制將檔案新增 `.tt` 至[](https://github.com/NuGet/Home/issues/3203)內容資料夾</span><span class="sxs-lookup"><span data-stu-id="b9af8-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="b9af8-112">nuget 套件 .csproj (`project.json` 如果沒有 JSON 檔案中的 packOptions 和擁有者，) 會當機- [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="b9af8-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="b9af8-113">的 nuget 套件會 `project.json` 忽略 packOptions 標記，例如摘要、作者、擁有者等 [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="b9af8-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="b9af8-114">nuget 套件會忽略 #3145 輸出 `.nuspec` 的 `project.json`  -  [](https://github.com/NuGet/Home/issues/3145)相依性</span><span class="sxs-lookup"><span data-stu-id="b9af8-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="b9af8-115">使用 rollback 更新多個封裝會讓專案處於中斷狀態- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="b9af8-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="b9af8-116">未針對 netstandard 專案新增任何的 ContentFiles- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="b9af8-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="b9af8-117">無法正確封裝以 .Net Standard 為目標的程式庫- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="b9af8-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="b9af8-118">檔案-> 新專案 > 類別庫 (便攜) 專案在 VS2015 和 Dev15 中失敗- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="b9af8-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="b9af8-119">NuGet 錯誤-1.0.0-\* 不是有效的版本字串- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="b9af8-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="b9af8-120">Find-Package 無法顯示，但 Install-Package 運作- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="b9af8-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="b9af8-121">在 dev15 上「安裝套件 jquery. 驗證」時發生錯誤- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="b9af8-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="b9af8-122">在使用 NuGet 版本3.5.0 的 VS 上安裝 VS 2015 update 3 時發生錯誤- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="b9af8-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="b9af8-123">套件管理員 UI：更新封裝之後不會顯示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="b9af8-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="b9af8-124">-在3.5.0 中不會讀取/傳送 ApiKey on delete 命令列-Beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="b9af8-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="b9af8-125">不正確的字串：套件的穩定版本不應具有發行前版本的相依性。</span><span class="sxs-lookup"><span data-stu-id="b9af8-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="b9af8-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="b9af8-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="b9af8-127">建立 PCL (net46 和 windows 10) project get NullRef 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b9af8-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="b9af8-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="b9af8-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="b9af8-129">當較高的版本受限於 allowedVersions 條件約束時，Nuget 更新應提供資訊性訊息 [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="b9af8-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="b9af8-130">認證外掛程式結束，發生錯誤-1/在使用具有多個來源的認證提供者時下載封裝時發生錯誤- [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="b9af8-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="b9af8-131">nuget 套件-套件相依性缺少 Newtonsoft.Js- [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="b9af8-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="b9af8-132">Linux/MacOS + Mono [#2860](https://github.com/NuGet/Home/issues/2860)上的 ExecuteSynchronizedCore 錯誤</span><span class="sxs-lookup"><span data-stu-id="b9af8-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="b9af8-133">VS 不支援 repositoryPath ( # A0) [#2763](https://github.com/NuGet/Home/issues/2763)的環境變數</span><span class="sxs-lookup"><span data-stu-id="b9af8-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="b9af8-134">修正協助工具問題- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="b9af8-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="b9af8-135">具有斷字元設定檔的可移植架構會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="b9af8-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="b9af8-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="b9af8-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="b9af8-137">NuGet 套件管理員應該確定套件詳細資料的選項清單不適用 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="b9af8-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="b9af8-138">NuGet 3.3.0 更新失敗，並出現「額外的條件約束 .。。在 packages.config 中定義會防止這項作業。</span><span class="sxs-lookup"><span data-stu-id="b9af8-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="b9af8-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="b9af8-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="b9af8-140">從不存在的本機來源安裝套件會擲回假訊息 [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="b9af8-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="b9af8-141">"Upgrade v) " 篩選器會顯示違反版本條件約束的升級- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="b9af8-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="b9af8-142">效能改進</span><span class="sxs-lookup"><span data-stu-id="b9af8-142">Performance Improvements</span></span>

* <span data-ttu-id="b9af8-143">效能：改善 ContentModel 目標 framework 剖析- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="b9af8-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="b9af8-144">效能：避免讀取沒有 `runtime.json` rid [#3150](https://github.com/NuGet/Home/issues/3150)的還原檔案。</span><span class="sxs-lookup"><span data-stu-id="b9af8-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="b9af8-145">在 CI 機器上，將範例 ASP.NET Web 應用程式的還原從超過15秒減少為3秒。</span><span class="sxs-lookup"><span data-stu-id="b9af8-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="b9af8-146">效能：封裝管理員主控台 init.ps1 載入時間 [#2956](https://github.com/NuGet/Home/issues/2956)。</span><span class="sxs-lookup"><span data-stu-id="b9af8-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="b9af8-147">從132s 到10s 的某些案例中，開啟 PackageManagerConsole 的時間已獲得改善。</span><span class="sxs-lookup"><span data-stu-id="b9af8-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="b9af8-148">解決 NuGet 更新中的 ReSharper 效能問題- [#3044](https://github.com/NuGet/Home/issues/3044)：在範例專案中，安裝套件所需的時間從140s 減少到68s。</span><span class="sxs-lookup"><span data-stu-id="b9af8-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="b9af8-149">DCR</span><span class="sxs-lookup"><span data-stu-id="b9af8-149">DCRs</span></span>

* <span data-ttu-id="b9af8-150">NuGet 必須讓使用者知道以 dotnet tfm 為基礎的 PCL 進行升級/安裝可能會造成問題- [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="b9af8-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="b9af8-151">針對專案的不正確安裝/升級發出警告/tfm = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="b9af8-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="b9af8-152">新增 netcoreapp11 和 netstandard17 支援- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="b9af8-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="b9af8-153">在 nuget.exe [#2934](https://github.com/NuGet/Home/issues/2934)中將 NuGet-Warning 標頭內容列印到主控台</span><span class="sxs-lookup"><span data-stu-id="b9af8-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="b9af8-154">利用 AssemblyMetadata 屬性進行 `.nuspec` 權杖取代- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="b9af8-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="b9af8-155">從鎖定檔案中移除鎖定的屬性- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="b9af8-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="b9af8-156">在安裝或更新時，不應該使用符號套件 #2807</span><span class="sxs-lookup"><span data-stu-id="b9af8-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="b9af8-157">功能</span><span class="sxs-lookup"><span data-stu-id="b9af8-157">Features</span></span>

* <span data-ttu-id="b9af8-158">支援 fallback 封裝資料夾- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="b9af8-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="b9af8-159">設計和執行封裝類型的概念以支援工具套件- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="b9af8-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="b9af8-160">取得全域套件資料夾路徑的 API- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="b9af8-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="b9af8-161">原生套件更新支援- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="b9af8-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
