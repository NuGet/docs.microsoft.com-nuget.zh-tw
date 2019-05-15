---
title: NuGet 5.0 RTM 版本資訊
description: 包括已知的問題、 bug 修正、 新功能和 Dcr NuGet 5.0 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610667"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="c7b80-103">NuGet 5.0 版本資訊</span><span class="sxs-lookup"><span data-stu-id="c7b80-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="c7b80-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="c7b80-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="c7b80-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="c7b80-105">NuGet version</span></span> | <span data-ttu-id="c7b80-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="c7b80-106">Available in Visual Studio version</span></span>| <span data-ttu-id="c7b80-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c7b80-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="c7b80-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="c7b80-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="c7b80-109">Visual Studio 2019 版本 16.0</span><span class="sxs-lookup"><span data-stu-id="c7b80-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="c7b80-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="c7b80-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="c7b80-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="c7b80-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="c7b80-112">Visual Studio 2019 版本 16.0.4</span><span class="sxs-lookup"><span data-stu-id="c7b80-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="c7b80-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="c7b80-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="c7b80-114"><sup>1</sup>安裝的 Visual Studio 2019 是使用.NET Core 工作負載</span><span class="sxs-lookup"><span data-stu-id="c7b80-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="c7b80-115"><sup>2</sup>與.NET Core 工作負載的 Visual Studio 2019 提供選擇性的安裝</span><span class="sxs-lookup"><span data-stu-id="c7b80-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="c7b80-116">摘要: 什麼是 5.0 的新功能</span><span class="sxs-lookup"><span data-stu-id="c7b80-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="c7b80-117">支援還原[篩選解決方案](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019)在 Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="c7b80-117">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="c7b80-118">`BuildTransitive` 資料夾可讓封裝以可轉移方式參與目標 /props 至主應用程式專案- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="c7b80-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="c7b80-119">更妥善支援適合在 NuGet Iv Api-PackageReference [#7005](https://github.com/NuGet/Home/issues/7005)， [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="c7b80-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="c7b80-120">`nuget.exe pack project.json` 已被取代- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="c7b80-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="c7b80-121">層代 1 的認證提供者外掛程式已被取代[Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin)且即將被取代- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="c7b80-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="c7b80-122">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="c7b80-122">Issues fixed in this release</span></span>

<span data-ttu-id="c7b80-123">**Bug**</span><span class="sxs-lookup"><span data-stu-id="c7b80-123">**Bugs**</span></span>

* <span data-ttu-id="c7b80-124">NoOp 還原時，避免 \*。 在 obj 目錄-dgspec.json 寫入[#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="c7b80-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="c7b80-125">~/.Nuget 內建立檔案的權限會太開啟- [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="c7b80-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="c7b80-126">`dotnet list package --outdated` 不適用於需要驗證-來源[#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="c7b80-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="c7b80-127">NuGet.VisualStudio.IVsPackageInstaller-求助於未封裝的專案參考一律會使用 packages.config，即使預設設定為 PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="c7b80-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="c7b80-128">PMC:更新套件重新取消列入套件安裝失敗 （「 無法找到的套件 」）。</span><span class="sxs-lookup"><span data-stu-id="c7b80-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="c7b80-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="c7b80-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="c7b80-130">在我們的存放庫和 VSIX 內-新增第三方注意事項[#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="c7b80-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="c7b80-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage 應該安裝最新版本時指定-任何版本[#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="c7b80-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="c7b80-132">-dotnet nuget push 互動式支援- [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="c7b80-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="c7b80-133">還原時鎖定檔案，就不應該引發 NU1603 警告。</span><span class="sxs-lookup"><span data-stu-id="c7b80-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="c7b80-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="c7b80-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="c7b80-135">NuGet 不應該使用最低限度記錄-還原期間會列印專案路徑[#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="c7b80-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="c7b80-136">-dotnet 提供互動式支援移除封裝- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="c7b80-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="c7b80-137">新增與 TypeForwardedTo attrs-回 NuGet.Packaging.Core [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="c7b80-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="c7b80-138">plugins_cache 需要短的路徑無法正常運作- [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="c7b80-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="c7b80-139">偏好使用 msbuild 探索的路徑，如果使用者未要求特定的 msbuild 版本- [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="c7b80-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="c7b80-140">`nuget.exe /?` 應該會列出正確的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="c7b80-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="c7b80-141">NuGet.targets(498,5)： 錯誤：找不到的部分路徑 ' / tmp/NuGetScratch--在 mono 上[#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="c7b80-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="c7b80-142">還原不必要地列舉的所有版本的電腦快取中參照的套件內容[#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="c7b80-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="c7b80-143">MSBuild 的自動偵測一律選取 16.0 之後安裝 VS 2019 預覽- [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="c7b80-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="c7b80-144">在方案上的 dotnet 列出封裝輸出的架構-重複的項目[#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="c7b80-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="c7b80-145">例外狀況 「 空的路徑名稱不合法 」 呼叫 IVsPackageInstaller.InstallPackage 舊專案，並封裝資料夾不存在。</span><span class="sxs-lookup"><span data-stu-id="c7b80-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="c7b80-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="c7b80-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="c7b80-147">msbuild /t: restore 最少的詳細資訊應該很多小- [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="c7b80-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="c7b80-148">VS 16.0 的 NuGet UI 有無法讀取的索引標籤色彩的問題-由於[#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="c7b80-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="c7b80-149">NuGet.Core & NuGet.Clients License.txt 釐清- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="c7b80-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="c7b80-150">還原不必要地列舉全域套件資料夾，在嘗試判定類型- [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="c7b80-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="c7b80-151">鎖定檔案強制執行中的錯誤應該會顯示在錯誤清單 視窗- [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="c7b80-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="c7b80-152">修正 NuGet.Configuration 問題- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="c7b80-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="c7b80-153">適應 MSBuild 更新其安裝位置- [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="c7b80-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="c7b80-154">NuGet.Build.Tasks.Pack 應為開發相依性- [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="c7b80-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="c7b80-155">新增組件擴充點，包括偵錯符號- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="c7b80-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="c7b80-156">`dotnet pack` 應該保留在建立 nupkg 中的相依性版本範圍 （即使使用浮動版本）- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="c7b80-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="c7b80-157">`dotnet restore` 失敗時使用者層級組態也會有原始檔-已驗證的來源[#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="c7b80-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="c7b80-158">組件應該不會限制內容的檔案-BuildActions 集[#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="c7b80-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="c7b80-159">使用 ProjectReference 需要 AssetTargetFallback 才會成功，應該發出警告。</span><span class="sxs-lookup"><span data-stu-id="c7b80-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="c7b80-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="c7b80-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="c7b80-161">由於執行緒的問題，當呼叫 CPS (CommonProjectSystem)-死結[#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="c7b80-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="c7b80-162">`dotnet add package` 不使用認證，從全域設定本機設定-中指定的來源[#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="c7b80-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="c7b80-163">MEF 上非同步呼叫的執行緒問題的程式碼路徑- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="c7b80-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="c7b80-164">簽章： 錯誤報告兩次，而不呼叫堆疊- [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="c7b80-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="c7b80-165">安裝已簽署的封裝使用未受信任的簽章憑證應該會顯示錯誤- [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="c7b80-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="c7b80-166">NuGet 還原不正確 Noop 時 2 個專案共用 obj 目錄- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="c7b80-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="c7b80-167">無法使用與 PAT`dotnet restore`在 Linux 上使用來自已驗證的摘要-套件[#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="c7b80-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="c7b80-168">dotnet 還原失敗，因為已停用全機器摘要- [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="c7b80-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="c7b80-169">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="c7b80-169">**DCRs**</span></span>

* <span data-ttu-id="c7b80-170">未來移除"dotnet pack project.json-"，即發出警告[#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="c7b80-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="c7b80-171">新增取代警告 Gen1 認證外掛程式- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="c7b80-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="c7b80-172">簽署：已啟用的存放庫，以要求為存放庫的用戶端驗證的每個套件簽署-透過 RepositorySignatures/5.0.0 資源- [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="c7b80-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="c7b80-173">每個來源 NuGet.Config-透過 http 要求數目限制[#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="c7b80-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="c7b80-174">NuGet 應為目標 （以協助清除 VSIX 16.0 組建） Net472- [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="c7b80-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="c7b80-175">PMC:移除 OpenPackagePage 命令- [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="c7b80-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="c7b80-176">請 NetCoreApp 3.0 對應為 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="c7b80-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="c7b80-177">將 netstandard2.0 支援新增至 NuGet.\* 封裝- [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="c7b80-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="c7b80-178">讓套件作者可以定義建置的資產轉移行為- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="c7b80-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="c7b80-179">支援 VS 2019 方案篩選功能。</span><span class="sxs-lookup"><span data-stu-id="c7b80-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="c7b80-180">也支援不在方案中，專案或卸載的專案。</span><span class="sxs-lookup"><span data-stu-id="c7b80-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="c7b80-181">需要先還原完整的解決方案 （透過 CLI 或 VS） [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="c7b80-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="c7b80-182">NuGet 5.0 組件 （透過 TFM 變化）-需要.NET 4.7.2 [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="c7b80-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="c7b80-183">從 NuGet.Packaging NuGetLicenseData 應該是公用型別。</span><span class="sxs-lookup"><span data-stu-id="c7b80-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="c7b80-184">更新 spdx 從內嵌的授權中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c7b80-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="c7b80-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="c7b80-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="c7b80-186">移除過時的設定 Api- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="c7b80-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="c7b80-187">因應措施 1 的系統上的還原逾時 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="c7b80-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="c7b80-188">NuGet 偏好 NTLM 驗證，即使在 NuGet.config 中認證-config 選項加入篩選驗證類型，認證- [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="c7b80-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="c7b80-189">啟用 EmbedInteropTypes packagereference （比對 Packages.Config 功能）- [# 2365年](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="c7b80-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="c7b80-190">**[此版本為 5.0 RTM 修正的所有問題的清單](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="c7b80-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="c7b80-191">摘要: 5.0.2 中最新消息</span><span class="sxs-lookup"><span data-stu-id="c7b80-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="c7b80-192">（當透過 dotnet.exe 或 mono.exe 執行） 的安全性-obj 資料夾應該建立具有正確權限[#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="c7b80-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="c7b80-193">在 mono/MacOS 上的 nuget.exe 還原失敗自訂 nuget.config 並`PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="c7b80-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="c7b80-194">已知問題</span><span class="sxs-lookup"><span data-stu-id="c7b80-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="c7b80-195">FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="c7b80-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="c7b80-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="c7b80-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="c7b80-197">問題</span><span class="sxs-lookup"><span data-stu-id="c7b80-197">Issue</span></span>
<span data-ttu-id="c7b80-198">使用 dotnet.exe 2.x 來還原以 netcoreapp 1.x 與 netcoreapp 2.x 為多目標的專案時，後援資料夾被視為檔案摘要。</span><span class="sxs-lookup"><span data-stu-id="c7b80-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="c7b80-199">這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。</span><span class="sxs-lookup"><span data-stu-id="c7b80-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="c7b80-200">因應措施</span><span class="sxs-lookup"><span data-stu-id="c7b80-200">Workaround</span></span>
<span data-ttu-id="c7b80-201">停用的後援的資料夾使用方式設定`RestoreAdditionalProjectSources`沒有任何字元：</span><span class="sxs-lookup"><span data-stu-id="c7b80-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="c7b80-202">這個謹慎使用，現在會從 NuGet.org 下載會從後援資料夾還原的套件。</span><span class="sxs-lookup"><span data-stu-id="c7b80-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
