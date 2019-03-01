---
title: NuGet 5.0 preview 版本資訊
description: 包括已知的問題、 bug 修正、 新功能和 Dcr NuGet 5.0 preview 版本資訊。
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 57b66b347ac47a3d05907a4bb237002de8981ecc
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196196"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="0a72d-103">NuGet 5.0 Preview 版本資訊</span><span class="sxs-lookup"><span data-stu-id="0a72d-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="0a72d-104">NuGet 5.0 Preview 版本</span><span class="sxs-lookup"><span data-stu-id="0a72d-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="0a72d-105">2010 年 2 月 27 日- [NuGet 5.0 Preview 4](#summary-whats-new-in-50-preview-4)</span><span class="sxs-lookup"><span data-stu-id="0a72d-105">February 27, 2010 - [NuGet 5.0 Preview 4](#summary-whats-new-in-50-preview-4)</span></span>
* <span data-ttu-id="0a72d-106">2019 年 2 月 13 日- [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="0a72d-106">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="0a72d-107">2019 年 1 月 23 日- [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="0a72d-107">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-4"></a><span data-ttu-id="0a72d-108">摘要: 什麼是 NuGet 5.0 Preview 4 的新功能</span><span class="sxs-lookup"><span data-stu-id="0a72d-108">Summary: What's New in NuGet 5.0 Preview 4</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="0a72d-109">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="0a72d-109">Issues fixed in this release</span></span>

<span data-ttu-id="0a72d-110">**錯誤：**</span><span class="sxs-lookup"><span data-stu-id="0a72d-110">**Bugs:**</span></span>

* <span data-ttu-id="0a72d-111">NuGet.VisualStudio.IVsPackageInstaller-求助於未封裝的專案參考一律會使用 packages.config，即使預設設定為 PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="0a72d-111">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="0a72d-112">PMC:更新套件重新取消列入套件安裝失敗 （「 無法找到的套件 」）。</span><span class="sxs-lookup"><span data-stu-id="0a72d-112">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="0a72d-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="0a72d-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="0a72d-114">在我們的存放庫和 VSIX 內-新增第三方注意事項[#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="0a72d-114">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="0a72d-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage 應該安裝最新版本時指定-任何版本[#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="0a72d-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="0a72d-116">-dotnet nuget push 互動式支援- [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="0a72d-116">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="0a72d-117">還原時鎖定檔案，就不應該引發 NU1603 警告。</span><span class="sxs-lookup"><span data-stu-id="0a72d-117">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="0a72d-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="0a72d-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="0a72d-119">NuGet 不應該使用最低限度記錄-還原期間會列印專案路徑[#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="0a72d-119">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="0a72d-120">-dotnet 提供互動式支援移除封裝- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="0a72d-120">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="0a72d-121">新增與 TypeForwardedTo attrs-回 NuGet.Packaging.Core [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="0a72d-121">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="0a72d-122">plugins_cache 需要短的路徑無法正常運作- [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="0a72d-122">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="0a72d-123">偏好使用 msbuild 探索的路徑，如果使用者未要求特定的 msbuild 版本- [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="0a72d-123">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

<span data-ttu-id="0a72d-124">**Dcr:**</span><span class="sxs-lookup"><span data-stu-id="0a72d-124">**DCRs:**</span></span>

* <span data-ttu-id="0a72d-125">每個來源 NuGet.Config-透過 http 要求數目限制[#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="0a72d-125">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="0a72d-126">NuGet 應為目標 （以協助清除 VSIX 16.0 組建） Net472- [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="0a72d-126">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="0a72d-127">PMC:移除 OpenPackagePage 命令- [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="0a72d-127">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="0a72d-128">請 NetCoreApp 3.0 對應為 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="0a72d-128">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="0a72d-129">將 netstandard2.0 支援新增至 NuGet.\* 封裝- [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="0a72d-129">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>


## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="0a72d-130">摘要: 什麼是 NuGet 5.0 Preview 3 的新功能</span><span class="sxs-lookup"><span data-stu-id="0a72d-130">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="0a72d-131">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="0a72d-131">Issues fixed in this release</span></span> 

<span data-ttu-id="0a72d-132">**錯誤：**</span><span class="sxs-lookup"><span data-stu-id="0a72d-132">**Bugs:**</span></span>

* <span data-ttu-id="0a72d-133">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="0a72d-133">nuget.exe /?</span></span> <span data-ttu-id="0a72d-134">應該會列出正確的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="0a72d-134">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="0a72d-135">NuGet.targets(498,5)： 錯誤：找不到的部分路徑 ' / tmp/NuGetScratch--在 mono 上[#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="0a72d-135">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="0a72d-136">還原不必要地列舉的所有版本的電腦快取中參照的套件內容[#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="0a72d-136">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="0a72d-137">MSBuild 的自動偵測一律選取 16.0 之後安裝 VS 2019 預覽- [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="0a72d-137">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="0a72d-138">在方案上的 dotnet 列出封裝輸出的架構-重複的項目[#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="0a72d-138">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="0a72d-139">例外狀況 「 空的路徑名稱不合法 」 呼叫 IVsPackageInstaller.InstallPackage 舊專案，並封裝資料夾不存在。</span><span class="sxs-lookup"><span data-stu-id="0a72d-139">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="0a72d-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="0a72d-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="0a72d-141">msbuild /t: restore 最少的詳細資訊應該很多小- [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="0a72d-141">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="0a72d-142">**Dcr:**</span><span class="sxs-lookup"><span data-stu-id="0a72d-142">**DCRs:**</span></span>

* <span data-ttu-id="0a72d-143">讓套件作者可以定義建置的資產轉移行為- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="0a72d-143">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="0a72d-144">在成功的專案不是方案的一部分或未載入，但先前已還原-VS 中啟用還原[#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="0a72d-144">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="0a72d-145">摘要: 什麼是 5.0 Preview 2 的新功能</span><span class="sxs-lookup"><span data-stu-id="0a72d-145">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="0a72d-146">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="0a72d-146">Issues fixed in this release</span></span>

<span data-ttu-id="0a72d-147">**錯誤：**</span><span class="sxs-lookup"><span data-stu-id="0a72d-147">**Bugs:**</span></span>

* <span data-ttu-id="0a72d-148">VS 16.0 的 NuGet UI 有無法讀取的索引標籤色彩的問題-由於[#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="0a72d-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="0a72d-149">NuGet.Core & NuGet.Clients License.txt 釐清- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="0a72d-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="0a72d-150">還原不必要地列舉全域套件資料夾，在嘗試判定類型- [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="0a72d-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="0a72d-151">鎖定檔案強制執行中的錯誤應該會顯示在錯誤清單 視窗- [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="0a72d-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="0a72d-152">修正 NuGet.Configuration 問題- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="0a72d-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="0a72d-153">適應 MSBuild 更新它的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="0a72d-153">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="0a72d-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="0a72d-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="0a72d-155">NuGet.Build.Tasks.Pack 應為開發相依性- [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="0a72d-155">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="0a72d-156">新增組件擴充點，包括偵錯符號- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="0a72d-156">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="0a72d-157">dotnet 套件應該保留在建立 nupkg 中的相依性版本範圍。</span><span class="sxs-lookup"><span data-stu-id="0a72d-157">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="0a72d-158">（即使使用浮動版本）- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="0a72d-158">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="0a72d-159">dotnet 還原會失敗已驗證的來源上，當使用者層級組態也會有原始檔- [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="0a72d-159">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="0a72d-160">組件應該不會限制內容的檔案-BuildActions 集[#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="0a72d-160">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="0a72d-161">使用 projectreference 需要 AssetTargetFallback 才會成功，應該發出警告。</span><span class="sxs-lookup"><span data-stu-id="0a72d-161">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="0a72d-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="0a72d-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="0a72d-163">由於執行緒的問題，當呼叫 CPS (CommonProjectSystem)-死結[#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="0a72d-163">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="0a72d-164">dotnet 新增套件不會使用本機組態檔-中指定的來源的認證，從全域設定[#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="0a72d-164">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="0a72d-165">執行緒處理問題與 MEF 所呼叫的非同步程式碼路徑- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="0a72d-165">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="0a72d-166">簽章： 錯誤報告兩次，而不呼叫堆疊- [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="0a72d-166">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="0a72d-167">安裝已簽署的封裝使用未受信任的簽章憑證應該會顯示錯誤- [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="0a72d-167">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="0a72d-168">NuGet 還原不正確 Noop 時 2 個專案共用 obj 目錄- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="0a72d-168">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="0a72d-169">無法使用 Linux 上的 dotnet restore，有來自已驗證的摘要-套件 PAT [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="0a72d-169">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="0a72d-170">dotnet 還原失敗，因為已停用全機器摘要- [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="0a72d-170">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="0a72d-171">**Dcr:**</span><span class="sxs-lookup"><span data-stu-id="0a72d-171">**DCRs:**</span></span>

* <span data-ttu-id="0a72d-172">NuGet 5.0 組件 （透過 TFM 變化）-需要.NET 4.7.2 [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="0a72d-172">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="0a72d-173">從 NuGet.Packaging NuGetLicenseData 應該是公用型別。</span><span class="sxs-lookup"><span data-stu-id="0a72d-173">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="0a72d-174">更新 spdx 從內嵌的授權中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0a72d-174">Update license metadata ingested from spdx.</span></span><span data-ttu-id="0a72d-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="0a72d-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="0a72d-176">移除過時的設定 Api- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="0a72d-176">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="0a72d-177">因應措施 1 的系統上的還原逾時 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="0a72d-177">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="0a72d-178">NuGet 偏好 NTLM 驗證，即使在 NuGet.config 中認證-config 選項加入篩選驗證類型，認證- [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="0a72d-178">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="0a72d-179">啟用 EmbedInteropTypes packagereference （比對 Packages.Config 功能）- [# 2365年](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="0a72d-179">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="0a72d-180">在此版本 5.0.0-preview2 中修正的所有問題的清單</span><span class="sxs-lookup"><span data-stu-id="0a72d-180">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="0a72d-181">已知問題</span><span class="sxs-lookup"><span data-stu-id="0a72d-181">Known issues</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="0a72d-182">FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="0a72d-182">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="0a72d-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="0a72d-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="0a72d-184">**問題**使用 dotnet.exe 時還原專案的多重目標 netcoreapp 2.x 1.x 和 netcoreapp 2.x，後援的資料夾會被視為檔案摘要。</span><span class="sxs-lookup"><span data-stu-id="0a72d-184">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="0a72d-185">這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。</span><span class="sxs-lookup"><span data-stu-id="0a72d-185">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="0a72d-186">**因應措施**停用的後援的資料夾使用方式設定`RestoreAdditionalProjectSources`為 nothing。</span><span class="sxs-lookup"><span data-stu-id="0a72d-186">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="0a72d-187">`<RestoreAdditionalProjectSources/>` 請小心使用，因為它將會導致從 NuGet.org 下載許多套件，而不是從後援資料夾還原這些套件。</span><span class="sxs-lookup"><span data-stu-id="0a72d-187">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
