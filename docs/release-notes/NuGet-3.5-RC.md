---
title: 3.5 RC 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.5 RC 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548534"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="480b1-103">NuGet 3.5 RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="480b1-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="480b1-104">[NuGet 3.5-Beta2 版本資訊](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 的 RTM 版本資訊](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="480b1-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="480b1-105">3.5 版本著重於提升品質與效能的 NuGet 用戶端。</span><span class="sxs-lookup"><span data-stu-id="480b1-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="480b1-106">此外，我們所提供的一些功能，像是支援[後援的資料夾](https://github.com/NuGet/Home/issues/2899)， [PackageType](https://github.com/NuGet/Home/issues/2476)支援`.nuspec`和更多功能。</span><span class="sxs-lookup"><span data-stu-id="480b1-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="480b1-107">問題清單</span><span class="sxs-lookup"><span data-stu-id="480b1-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="480b1-108">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="480b1-108">Bug Fixes</span></span>

* <span data-ttu-id="480b1-109">安裝/還原套件的失敗 」 封裝包含多個`.nuspec`檔案。 」</span><span class="sxs-lookup"><span data-stu-id="480b1-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="480b1-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="480b1-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="480b1-111">nuget 組件會強制加入`.tt`檔案複製到內容的資料夾，無論如何- [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="480b1-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="480b1-112">nuget 套件 csproj (與`project.json`) 如果沒有任何 packOptions 及 JSON 檔案中的擁有者會當機[#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="480b1-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="480b1-113">適用於 nuget 套件`project.json`會忽略 packOptions 標記，例如摘要、 作者、 擁有者等- [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="480b1-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="480b1-114">nuget 套件會忽略輸出中的相依性`.nuspec`for `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="480b1-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="480b1-115">使用回復更新多個封裝離開專案處於中斷狀態- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="480b1-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="480b1-116">任何的 ContentFiles 不會新增為 netstandard 專案- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="480b1-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="480b1-117">無法封裝以.Net 為目標的程式庫標準正確- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="480b1-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="480b1-118">檔案]-> [新增專案]-> [類別庫 （可攜式） 專案會失敗，VS2015 和 Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="480b1-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="480b1-119">NuGet 錯誤-1.0.0-\* 不是有效的版本字串- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="480b1-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="480b1-120">尋找套件無法顯示，但安裝套件的運作方式- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="480b1-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="480b1-121">錯誤時 「 Install-package jquery.validation 」 在 dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="480b1-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="480b1-122">當已安裝的 VS 2015 更新 3 上使用的 NuGet 3.5.0 的版本時發生錯誤，就會發生-VS [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="480b1-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="480b1-123">套件管理員 UI： 不會顯示在更新封裝之後，新的版本- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="480b1-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="480b1-124">刪除命令列上的-ApiKey 中不會讀取/傳送 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="480b1-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="480b1-125">不正確的字串： 上的發行前版本的相依性不應該有套件的穩定版本。</span><span class="sxs-lookup"><span data-stu-id="480b1-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="480b1-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="480b1-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="480b1-127">正在建立 PCL （net46 和 windows 10） 專案取得 NullRef 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="480b1-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="480b1-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="480b1-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="480b1-129">Nuget 更新應該提供的告知性訊息，當較高的版本會受到 allowedVersions 條件約束- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="480b1-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="480b1-130">認證外掛程式已結束，錯誤為-1 / 錯誤下載套件時使用多個來源的認證提供者[# 2885年](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="480b1-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="480b1-131">nuget 套件遺漏 Newtonsoft.Json 套件相依性- [# 2876年](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="480b1-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="480b1-132">在 Linux/MacOS + Mono-ExecuteSynchronizedCore bug [# 2860年](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="480b1-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="480b1-133">與不支援環境變數中 repositoryPath （nuget.exe 執行）- [# 2763年](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="480b1-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="480b1-134">修正問題的協助工具問題- [# 2745年](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="480b1-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="480b1-135">可移植的架構，與連字號連接的設定檔會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="480b1-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="480b1-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="480b1-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="480b1-137">NuGet 套件管理員可以讓您清楚該詳細資料不適用於封裝中的 [選項] 清單`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="480b1-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="480b1-138">NuGet 3.3.0 更新因 '...額外的條件約束中定義 packages.config 可避免這項作業。 '</span><span class="sxs-lookup"><span data-stu-id="480b1-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="480b1-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="480b1-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="480b1-140">假的訊息-從本機來源不存在則會擲回安裝封裝[# 1674年](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="480b1-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="480b1-141">「 可用的升級 」 篩選條件會顯示升級違反版本條件約束- [# 1094年](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="480b1-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="480b1-142">效能改善</span><span class="sxs-lookup"><span data-stu-id="480b1-142">Performance Improvements</span></span>

* <span data-ttu-id="480b1-143">效能： 改善 ContentModel 目標 framework 剖析- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="480b1-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="480b1-144">效能： 避免讀取`runtime.json`檔案的還原作業沒有 Rid [#3150](https://github.com/NuGet/Home/issues/3150)。</span><span class="sxs-lookup"><span data-stu-id="480b1-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="480b1-145">CI 電腦上的 ASP.NET Web 應用程式減少 15 秒到 3 的秒數可從範例中還原。</span><span class="sxs-lookup"><span data-stu-id="480b1-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="480b1-146">效能： Package Manager Console init.ps1 載入時間[# 2956年](https://github.com/NuGet/Home/issues/2956)。</span><span class="sxs-lookup"><span data-stu-id="480b1-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="480b1-147">在 10 秒從 132s年某些情況下，改善開啟 PackageManagerConsole 的時間。</span><span class="sxs-lookup"><span data-stu-id="480b1-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="480b1-148">解決 NuGet 更新-ReSharper 效能問題[#3044](https://github.com/NuGet/Home/issues/3044)： 範例專案，安裝套件所花費的時間用來減少從 140s年 68s。</span><span class="sxs-lookup"><span data-stu-id="480b1-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="480b1-149">DCR</span><span class="sxs-lookup"><span data-stu-id="480b1-149">DCRs</span></span>

* <span data-ttu-id="480b1-150">NuGet 需要讓使用者知道，升級/安裝中基礎 dotnet tfm PCL 可能會造成問題- [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="480b1-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="480b1-151">不正確安裝/升級具有 tfm 的專案，即發出警告 ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="480b1-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="480b1-152">新增 netcoreapp11 和 netstandard17 支援- [# 2998年](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="480b1-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="480b1-153">列印到主控台中 nuget.exe-NuGet 警告標頭內容[# 2934年](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="480b1-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="480b1-154">運用 AssemblyMetadata 屬性`.nuspec`語彙基元取代- [# 2851年](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="480b1-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="480b1-155">已鎖定的屬性移除鎖定檔中- [# 2379年](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="480b1-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="480b1-156">符號套件應該不曾經用於安裝或更新 #2807</span><span class="sxs-lookup"><span data-stu-id="480b1-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="480b1-157">功能</span><span class="sxs-lookup"><span data-stu-id="480b1-157">Features</span></span>

* <span data-ttu-id="480b1-158">支援後援的套件資料夾- [# 2899年](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="480b1-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="480b1-159">設計和實作封裝類型的概念，以支援工具套件- [# 2476年](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="480b1-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="480b1-160">API 來取得全域套件資料夾的路徑[# 2403年](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="480b1-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="480b1-161">原生套件更新的支援- [# 1291年](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="480b1-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
