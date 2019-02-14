---
title: NuGet 5.0 preview 版本資訊
description: 包括已知的問題、 bug 修正、 新功能和 Dcr NuGet 5.0 preview 版本資訊。
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247655"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="8fca5-103">NuGet 5.0 Preview 版本資訊</span><span class="sxs-lookup"><span data-stu-id="8fca5-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="8fca5-104">NuGet 5.0 Preview 版本</span><span class="sxs-lookup"><span data-stu-id="8fca5-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="8fca5-105">2019 年 2 月 13 日- [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="8fca5-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="8fca5-106">2019 年 1 月 23 日- [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="8fca5-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="8fca5-107">摘要: 什麼是 NuGet 5.0 Preview 3 的新功能</span><span class="sxs-lookup"><span data-stu-id="8fca5-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="8fca5-108">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="8fca5-108">Issues fixed in this release</span></span> 

<span data-ttu-id="8fca5-109">**錯誤：**</span><span class="sxs-lookup"><span data-stu-id="8fca5-109">**Bugs:**</span></span>

* <span data-ttu-id="8fca5-110">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="8fca5-110">nuget.exe /?</span></span> <span data-ttu-id="8fca5-111">應該會列出正確的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="8fca5-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="8fca5-112">NuGet.targets(498,5)： 錯誤：找不到的部分路徑 ' / tmp/NuGetScratch--在 mono 上[#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="8fca5-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="8fca5-113">還原不必要地列舉的所有版本的電腦快取中參照的套件內容[#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="8fca5-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="8fca5-114">MSBuild 的自動偵測一律選取 16.0 之後安裝 VS 2019 預覽- [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="8fca5-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="8fca5-115">在方案上的 dotnet 列出封裝輸出的架構-重複的項目[#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="8fca5-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="8fca5-116">例外狀況 「 空的路徑名稱不合法 」 呼叫 IVsPackageInstaller.InstallPackage 舊專案，並封裝資料夾不存在。</span><span class="sxs-lookup"><span data-stu-id="8fca5-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="8fca5-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="8fca5-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="8fca5-118">msbuild /t: restore 最少的詳細資訊應該很多小- [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="8fca5-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="8fca5-119">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="8fca5-119">**DCRs**</span></span>

* <span data-ttu-id="8fca5-120">讓套件作者可以定義建置的資產轉移行為- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="8fca5-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="8fca5-121">在成功的專案不是方案的一部分或未載入，但先前已還原-VS 中啟用還原[#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="8fca5-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="8fca5-122">摘要: 什麼是 5.0 Preview 2 的新功能</span><span class="sxs-lookup"><span data-stu-id="8fca5-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="8fca5-123">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="8fca5-123">Issues fixed in this release</span></span>

<span data-ttu-id="8fca5-124">**錯誤：**</span><span class="sxs-lookup"><span data-stu-id="8fca5-124">**Bugs:**</span></span>

* <span data-ttu-id="8fca5-125">VS 16.0 的 NuGet UI 有無法讀取的索引標籤色彩的問題-由於[#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="8fca5-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="8fca5-126">NuGet.Core & NuGet.Clients License.txt 釐清- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="8fca5-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="8fca5-127">還原不必要地列舉全域套件資料夾，在嘗試判定類型- [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="8fca5-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="8fca5-128">鎖定檔案強制執行中的錯誤應該會顯示在錯誤清單 視窗- [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="8fca5-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="8fca5-129">修正 NuGet.Configuration 問題- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="8fca5-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="8fca5-130">適應 MSBuild 更新它的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="8fca5-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="8fca5-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="8fca5-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="8fca5-132">NuGet.Build.Tasks.Pack 應為開發相依性- [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="8fca5-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="8fca5-133">新增組件擴充點，包括偵錯符號- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="8fca5-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="8fca5-134">dotnet 套件應該保留在建立 nupkg 中的相依性版本範圍。</span><span class="sxs-lookup"><span data-stu-id="8fca5-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="8fca5-135">（即使使用浮動版本）- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="8fca5-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="8fca5-136">dotnet 還原會失敗已驗證的來源上，當使用者層級組態也會有原始檔- [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="8fca5-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="8fca5-137">組件應該不會限制內容的檔案-BuildActions 集[#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="8fca5-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="8fca5-138">使用 projectreference 需要 AssetTargetFallback 才會成功，應該發出警告。</span><span class="sxs-lookup"><span data-stu-id="8fca5-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="8fca5-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="8fca5-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="8fca5-140">由於執行緒的問題，當呼叫 CPS (CommonProjectSystem)-死結[#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="8fca5-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="8fca5-141">dotnet 新增套件不會使用本機組態檔-中指定的來源的認證，從全域設定[#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="8fca5-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="8fca5-142">執行緒處理問題與 MEF 所呼叫的非同步程式碼路徑- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="8fca5-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="8fca5-143">簽章： 錯誤報告兩次，而不呼叫堆疊- [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="8fca5-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="8fca5-144">安裝已簽署的封裝使用未受信任的簽章憑證應該會顯示錯誤- [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="8fca5-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="8fca5-145">NuGet 還原不正確 Noop 時 2 個專案共用 obj 目錄- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="8fca5-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="8fca5-146">無法使用 Linux 上的 dotnet restore，有來自已驗證的摘要-套件 PAT [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="8fca5-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="8fca5-147">dotnet 還原失敗，因為已停用全機器摘要- [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="8fca5-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="8fca5-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="8fca5-148">**DCRs**</span></span>

* <span data-ttu-id="8fca5-149">NuGet 5.0 組件 （透過 TFM 變化）-需要.NET 4.7.2 [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="8fca5-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="8fca5-150">從 NuGet.Packaging NuGetLicenseData 應該是公用型別。</span><span class="sxs-lookup"><span data-stu-id="8fca5-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="8fca5-151">更新 spdx 從內嵌的授權中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8fca5-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="8fca5-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="8fca5-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="8fca5-153">移除過時的設定 Api- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="8fca5-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="8fca5-154">因應措施 1 的系統上的還原逾時 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="8fca5-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="8fca5-155">NuGet 偏好 NTLM 驗證，即使在 NuGet.config 中認證-config 選項加入篩選驗證類型，認證- [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="8fca5-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="8fca5-156">啟用 EmbedInteropTypes packagereference （比對 Packages.Config 功能）- [# 2365年](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="8fca5-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="8fca5-157">在此版本 5.0.0-preview2 中修正的所有問題的清單</span><span class="sxs-lookup"><span data-stu-id="8fca5-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="8fca5-158">已知問題</span><span class="sxs-lookup"><span data-stu-id="8fca5-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="8fca5-159">dotnet nuget push --interactive 在 Mac 上發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="8fca5-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="8fca5-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="8fca5-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="8fca5-161">**問題**`--interactive`引數不轉送 dotnet cli 和錯誤會導致`error: Missing value for option 'interactive'` 
**因應措施**以互動式的選項，例如執行任何其他的dotnet命令`dotnet restore --interactive`並進行驗證。</span><span class="sxs-lookup"><span data-stu-id="8fca5-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="8fca5-162">驗證接著可能會由認證提供者快取。</span><span class="sxs-lookup"><span data-stu-id="8fca5-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="8fca5-163">接著，執行 `dotnet nuget push`。</span><span class="sxs-lookup"><span data-stu-id="8fca5-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="8fca5-164">FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="8fca5-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="8fca5-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="8fca5-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="8fca5-166">**問題**使用 dotnet.exe 時還原專案的多重目標 netcoreapp 2.x 1.x 和 netcoreapp 2.x，後援的資料夾會被視為檔案摘要。</span><span class="sxs-lookup"><span data-stu-id="8fca5-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="8fca5-167">這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。</span><span class="sxs-lookup"><span data-stu-id="8fca5-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="8fca5-168">**因應措施**停用的後援的資料夾使用方式設定`RestoreAdditionalProjectSources`為 nothing。</span><span class="sxs-lookup"><span data-stu-id="8fca5-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="8fca5-169">`<RestoreAdditionalProjectSources/>` 請小心使用，因為它將會導致從 NuGet.org 下載許多套件，而不是從後援資料夾還原這些套件。</span><span class="sxs-lookup"><span data-stu-id="8fca5-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
