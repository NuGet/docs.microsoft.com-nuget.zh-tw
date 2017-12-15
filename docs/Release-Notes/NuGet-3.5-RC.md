---
title: "3.5 RC 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 75a9b496-5762-48b6-922f-fdddf1369c45
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.5 RC 版本資訊。"
keywords: "NuGet 3.5 RC 版本資訊、 錯誤修正的已知問題，已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09d566de6f53bc0f0ddd8049143dc647f3075671
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
#<a name="35-rc-release-notes"></a><span data-ttu-id="87128-104">3.5 RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="87128-104">3.5 RC Release Notes</span></span>

<span data-ttu-id="87128-105">[NuGet 3.5 Beta2 前版本資訊](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM 版本資訊](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="87128-105">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="87128-106">3.5 版本著重於改善品質及效能的 NuGet 用戶端。</span><span class="sxs-lookup"><span data-stu-id="87128-106">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="87128-107">此外，我們已寄出一些功能，例如支援[後援資料夾](https://github.com/NuGet/Home/issues/2899)， [PackageType](https://github.com/NuGet/Home/issues/2476)支援`.nuspec`等等。</span><span class="sxs-lookup"><span data-stu-id="87128-107">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="87128-108">問題清單</span><span class="sxs-lookup"><span data-stu-id="87128-108">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a><span data-ttu-id="87128-109">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="87128-109">Bug Fixes</span></span>

* <span data-ttu-id="87128-110">封裝安裝/還原失敗的 「 封裝包含多個`.nuspec`檔案。 」</span><span class="sxs-lookup"><span data-stu-id="87128-110">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="87128-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="87128-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="87128-112">強制將 nuget 套件加入`.tt`檔案解壓縮至內容的資料夾，不論什麼- [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="87128-112">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="87128-113">nuget 套件 csproj (與`project.json`) 損毀，如果有任何 packOptions 和擁有者，在 JSON 檔案- [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="87128-113">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="87128-114">nuget 套件`project.json`會忽略摘要、 作者、 等位的擁有者等 packOptions 標記[#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="87128-114">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="87128-115">nuget 套件會忽略輸出中的相依性`.nuspec`如`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="87128-115">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="87128-116">使用回復更新多個封裝保持專案處於中斷狀態- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="87128-116">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="87128-117">Netstandard 專案-不會新增任何 ContentFiles [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="87128-117">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="87128-118">無法封裝以.Net 為目標的程式庫標準正確[#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="87128-118">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="87128-119">檔案]-> [新增專案]-> [類別庫 （可攜式） 專案失敗 VS2015 和 Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="87128-119">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="87128-120">NuGet 錯誤-1.0.0-* 不是有效的版本字串- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="87128-120">NuGet error - 1.0.0-* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="87128-121">尋找套件無法顯示，但是 Install-package works- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="87128-121">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="87128-122">錯誤時 dev15 層上的 「 安裝套件 jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="87128-122">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="87128-123">當已安裝的 VS 2015 更新 3 上使用的 NuGet 版本 3.5.0 錯誤，就會發生-VS [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="87128-123">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="87128-124">封裝管理員 UI： 更新封裝之後，不會顯示新的版本- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="87128-124">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="87128-125">-ApiKey delete 命令列上不會讀取/傳送中 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="87128-125">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="87128-126">不正確的字串： 一個穩定的套件版本不應該在發行前版本相依性。</span><span class="sxs-lookup"><span data-stu-id="87128-126">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="87128-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="87128-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="87128-128">建立 （net46 和 windows 10） 的 PCL 專案 get NullRef 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="87128-128">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="87128-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="87128-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="87128-130">Nuget 更新應該提供具有資訊價值訊息時更高的版本受到 allowedVersions 條件約束- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="87128-130">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="87128-131">認證外掛程式已結束，錯誤碼為-1 / 錯誤下載封裝使用多個來源的認證提供者時[# 2885年](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="87128-131">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="87128-132">nuget 套件遺漏 Newtonsoft.Json 封裝相依性- [# 2876年](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="87128-132">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="87128-133">Linux/MacOS + Mono-ExecuteSynchronizedCore 中的 bug [# 2860年](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="87128-133">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="87128-134">VS 不支援環境變數中 repositoryPath （nuget.exe 運作）- [# 2763年](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="87128-134">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="87128-135">修正存取問題- [# 2745年](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="87128-135">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="87128-136">可攜式架構來使用連字號連接的設定檔會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="87128-136">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="87128-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="87128-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="87128-138">NuGet 封裝管理員可以讓您清楚該詳細不適用於封裝中的選項清單`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="87128-138">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="87128-139">NuGet 3.3.0 更新無法使用 '...額外的條件約束中定義 packages.config 阻止了此作業。 '</span><span class="sxs-lookup"><span data-stu-id="87128-139">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="87128-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="87128-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="87128-141">假的訊息-不存在則會擲回的本機來源從安裝封裝[# 1674年](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="87128-141">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="87128-142">「 可用的升級 」 篩選條件會顯示升級違反版本條件約束- [# 1094年](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="87128-142">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="87128-143">效能改善</span><span class="sxs-lookup"><span data-stu-id="87128-143">Performance Improvements</span></span>

* <span data-ttu-id="87128-144">效能： 改善 ContentModel 目標 framework 剖析- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="87128-144">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="87128-145">效能： 避免讀取`runtime.json`檔案的還原作業沒有 Rid [#3150](https://github.com/NuGet/Home/issues/3150)。</span><span class="sxs-lookup"><span data-stu-id="87128-145">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="87128-146">CI 在電腦上，還原的範例，透過 15 秒至 3 秒降低的 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="87128-146">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="87128-147">效能： Package Manager Console init.ps1 載入時間[# 2956年](https://github.com/NuGet/Home/issues/2956)。</span><span class="sxs-lookup"><span data-stu-id="87128-147">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="87128-148">若要開啟 PackageManagerConsole 時間改善 10s 132s年從某些情況。</span><span class="sxs-lookup"><span data-stu-id="87128-148">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="87128-149">解決 NuGet 更新-ReSharper 效能問題[#3044](https://github.com/NuGet/Home/issues/3044)： 範例專案，安裝套件時所花費的時間用來減少從 140s年 68s。</span><span class="sxs-lookup"><span data-stu-id="87128-149">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="87128-150">Dcr</span><span class="sxs-lookup"><span data-stu-id="87128-150">DCRs</span></span>

* <span data-ttu-id="87128-151">若要讓使用者知道，在基礎 dotnet tfm 升級/安裝 PCL 可能會導致問題-需要 NuGet [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="87128-151">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="87128-152">警告錯誤安裝/升級專案以 tfm ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="87128-152">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="87128-153">新增 netcoreapp11 和 netstandard17 支援- [# 2998年](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="87128-153">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="87128-154">列印到主控台中 nuget.exe-NuGet 警告標頭內容[# 2934年](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="87128-154">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="87128-155">運用 AssemblyMetadata 屬性`.nuspec`語彙基元取代- [# 2851年](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="87128-155">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="87128-156">鎖定的屬性移除鎖定檔案- [# 2379年](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="87128-156">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="87128-157">符號套件不應曾經用於安裝或更新 #2807</span><span class="sxs-lookup"><span data-stu-id="87128-157">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="87128-158">功能</span><span class="sxs-lookup"><span data-stu-id="87128-158">Features</span></span>

* <span data-ttu-id="87128-159">支援後援封裝資料夾- [# 2899年](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="87128-159">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="87128-160">設計和實作封裝類型的概念，以支援工具套件- [# 2476年](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="87128-160">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="87128-161">API 來取得全域套件資料夾的路徑[# 2403年](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="87128-161">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="87128-162">原生封裝更新支援- [# 1291年](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="87128-162">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
