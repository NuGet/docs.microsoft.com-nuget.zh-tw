---
title: NuGet 5.0 RTM 版本資訊
description: NuGet 5.0 的版本資訊，包含已知問題、bug 修正、新功能及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901742"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="91b08-103">NuGet 5.0 版本資訊</span><span class="sxs-lookup"><span data-stu-id="91b08-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="91b08-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="91b08-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="91b08-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="91b08-105">NuGet version</span></span> | <span data-ttu-id="91b08-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="91b08-106">Available in Visual Studio version</span></span>| <span data-ttu-id="91b08-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="91b08-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="91b08-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="91b08-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="91b08-109">Visual Studio 2019 16.0 版</span><span class="sxs-lookup"><span data-stu-id="91b08-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="91b08-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="91b08-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="91b08-111">**5.0.2 版**</span><span class="sxs-lookup"><span data-stu-id="91b08-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="91b08-112">Visual Studio 2019 版本16.0.4 版</span><span class="sxs-lookup"><span data-stu-id="91b08-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="91b08-113">[2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="91b08-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="91b08-114"><sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="91b08-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="91b08-115"><sup>2</sup>可透過 .NET Core 工作負載，以選用的方式安裝 Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="91b08-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="91b08-116">摘要：5.0 中的新功能</span><span class="sxs-lookup"><span data-stu-id="91b08-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="91b08-117">支援在 Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)中還原已[篩選的解決方案](/visualstudio/ide/filtered-solutions)</span><span class="sxs-lookup"><span data-stu-id="91b08-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="91b08-118">`BuildTransitive` 資料夾可讓套件以可傳遞的目標/.props 給主項目目- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="91b08-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="91b08-119">針對 NuGet Iv Api 中的 PackageReference 案例提供更佳的支援- [#7005](https://github.com/NuGet/Home/issues/7005)、 [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="91b08-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="91b08-120">`nuget.exe pack project.json` 已淘汰- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="91b08-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="91b08-121">Gen 1 認證提供者外掛程式已由 [gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) 取代，即將淘汰- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="91b08-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="91b08-122">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="91b08-122">Issues fixed in this release</span></span>

<span data-ttu-id="91b08-123">**Bug**</span><span class="sxs-lookup"><span data-stu-id="91b08-123">**Bugs**</span></span>

* <span data-ttu-id="91b08-124">進行 NoOp 還原時，請避免在 obj 目錄中寫入 \* .dgspec.js[#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="91b08-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="91b08-125">在 ~/.nuget 內建立之檔案的許可權太開啟- [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="91b08-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="91b08-126">`dotnet list package --outdated`不適用於需要驗證[#7605](https://github.com/NuGet/Home/issues/7605)的來源</span><span class="sxs-lookup"><span data-stu-id="91b08-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="91b08-127">VisualStudio：在沒有套件參考的專案上呼叫一律會使用 packages.config，即使預設值設定為 PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="91b08-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="91b08-128">PMC： Update-Package 重新安裝失敗 ( delisted 套件上的「找不到套件」 ) 。</span><span class="sxs-lookup"><span data-stu-id="91b08-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="91b08-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="91b08-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="91b08-130">在我們的存放庫和 VSIX 中新增協力廠商通知- [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="91b08-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="91b08-131">如果未指定任何版本，則 VisualStudio 應該安裝最新版本- [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="91b08-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="91b08-132">--dotnet nuget push [#7519](https://github.com/NuGet/Home/issues/7519)的互動式支援</span><span class="sxs-lookup"><span data-stu-id="91b08-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="91b08-133">使用鎖定檔案還原時，不應該引發 NU1603 警告。</span><span class="sxs-lookup"><span data-stu-id="91b08-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="91b08-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="91b08-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="91b08-135">在還原期間，NuGet 不應使用基本記錄來列印專案路徑- [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="91b08-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="91b08-136">--dotnet 的互動式支援移除套件- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="91b08-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="91b08-137">使用 TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)來新增後置 NuGet</span><span class="sxs-lookup"><span data-stu-id="91b08-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="91b08-138">plugins_cache 需要較短的路徑，才能順利運作- [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="91b08-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="91b08-139">如果使用者未要求特定的 msbuild 版本，則偏好使用 msbuild 探索路徑- [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="91b08-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="91b08-140">`nuget.exe /?` 應列出正確的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="91b08-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="91b08-141">Nuget.exe (就是498，5) ：錯誤：找不到路徑 '/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793)的部分</span><span class="sxs-lookup"><span data-stu-id="91b08-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="91b08-142">還原不必要地列舉電腦快取中參考封裝的所有版本內容- [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="91b08-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="91b08-143">在安裝 VS 2019 Preview 之後，MSBuild 自動偵測一律會選取 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="91b08-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="91b08-144">解決方案的 dotnet 清單套件會輸出架構[#7607](https://github.com/NuGet/Home/issues/7607)的重複專案</span><span class="sxs-lookup"><span data-stu-id="91b08-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="91b08-145">在舊專案上呼叫 IVsPackageInstaller 時，例外狀況「空的路徑名稱不合法」，且套件資料夾不存在。</span><span class="sxs-lookup"><span data-stu-id="91b08-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="91b08-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="91b08-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="91b08-147">msbuild/t：還原的詳細程度應更低 [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="91b08-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="91b08-148">VS 16.0 的 NuGet UI 由於色彩問題而無法讀取索引標籤- [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="91b08-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="91b08-149">Nuget.exe & NuGet. 用戶端 License.txt 澄清- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="91b08-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="91b08-150">還原非必要的列舉全域封裝資料夾，以嘗試判斷類型 [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="91b08-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="91b08-151">[錯誤清單] 視窗中會顯示鎖定檔案強制執行的錯誤- [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="91b08-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="91b08-152">修正 NuGet.Configuration 問題- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="91b08-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="91b08-153">適應 MSBuild 更新其安裝位置- [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="91b08-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="91b08-154">Nuget.exe 應為開發相依性- [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="91b08-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="91b08-155">新增套件擴充點以包含 debug 符號- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="91b08-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="91b08-156">`dotnet pack` 應該保留所建立之 nupkg (中的相依性版本範圍，即使是使用浮動版本) [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="91b08-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="91b08-157">`dotnet restore`當使用者層級設定也有來源[#7209](https://github.com/NuGet/Home/issues/7209)時，已驗證的來源上會失敗</span><span class="sxs-lookup"><span data-stu-id="91b08-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="91b08-158">套件不應限制內容檔案的 BuildActions 集- [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="91b08-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="91b08-159">使用需要 AssetTargetFallback 成功的 ProjectReference 時，應該發出警告。</span><span class="sxs-lookup"><span data-stu-id="91b08-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="91b08-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="91b08-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="91b08-161">呼叫 CPS (CommonProjectSystem) [#7103](https://github.com/NuGet/Home/issues/7103)時，因執行緒問題而造成鎖死</span><span class="sxs-lookup"><span data-stu-id="91b08-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="91b08-162">`dotnet add package` 針對本機設定中指定的來源，不使用全域設定的認證- [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="91b08-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="91b08-163">在非同步程式碼路徑上呼叫 MEF 的執行緒問題- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="91b08-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="91b08-164">簽署：錯誤報表兩次且沒有呼叫堆疊- [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="91b08-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="91b08-165">安裝具有未受信任簽署憑證的已簽署套件應該會顯示錯誤- [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="91b08-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="91b08-166">當2個專案共用[#6114](https://github.com/NuGet/Home/issues/6114)的 obj 目錄時，NuGet 還原不當 NoOps</span><span class="sxs-lookup"><span data-stu-id="91b08-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="91b08-167">無法在 Linux 上搭配使用 PAT 與 `dotnet restore` 已驗證摘要的套件- [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="91b08-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="91b08-168">dotnet restore 因為已停用電腦寬摘要而失敗- [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="91b08-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="91b08-169">**DCR**</span><span class="sxs-lookup"><span data-stu-id="91b08-169">**DCRs**</span></span>

* <span data-ttu-id="91b08-170">未來移除「dotnet pack project.js」的警告- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="91b08-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="91b08-171">新增 Gen1 認證外掛程式的取代警告- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="91b08-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="91b08-172">簽署：已啟用存放庫，以要求每個套件的用戶端驗證（以存放庫簽署）--via RepositorySignatures/5.0.0 資源- [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="91b08-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="91b08-173">透過 NuGet.Config [#4538](https://github.com/NuGet/Home/issues/4538)限制每個來源的 HTTP 要求號碼</span><span class="sxs-lookup"><span data-stu-id="91b08-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="91b08-174">NuGet 應以 Net472 (為目標，以協助清理 VSIX) 的16.0 組建 [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="91b08-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="91b08-175">PMC： Remove OpenPackagePage 命令- [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="91b08-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="91b08-176">將 NetCoreApp 3.0 對應到 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="91b08-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="91b08-177">將 netstandard 2.0 支援新增至 NuGet. \* 套件- [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="91b08-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="91b08-178">允許封裝作者定義組建資產的可轉移行為- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="91b08-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="91b08-179">支援 VS 2019 解決方案篩選功能。</span><span class="sxs-lookup"><span data-stu-id="91b08-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="91b08-180">也支援不在方案中的專案，或已卸載的專案。</span><span class="sxs-lookup"><span data-stu-id="91b08-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="91b08-181">需要透過 CLI 或 VS) first [#5820](https://github.com/NuGet/Home/issues/5820)還原完整的解決方案 (</span><span class="sxs-lookup"><span data-stu-id="91b08-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="91b08-182">需要 .NET 4.7.2 的 NuGet 5.0 元件 (via TFM 變更) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="91b08-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="91b08-183">從 NuGet NuGetLicenseData。封裝應該是公用類型。</span><span class="sxs-lookup"><span data-stu-id="91b08-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="91b08-184">更新來自 spdx 的授權中繼資料內嵌。</span><span class="sxs-lookup"><span data-stu-id="91b08-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="91b08-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="91b08-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="91b08-186">移除淘汰的設定 Api- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="91b08-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="91b08-187">因應措施：在具有1個 cpu [#6742](https://github.com/NuGet/Home/issues/6742)的系統上還原超時</span><span class="sxs-lookup"><span data-stu-id="91b08-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="91b08-188">即使有 NuGet.config-新增設定選項中的認證可篩選認證的驗證類型，NuGet 仍優先于 NTLM 驗證- [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="91b08-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="91b08-189">啟用 EmbedInteropTypes for PackageReference (符合 Packages.Config 功能) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="91b08-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="91b08-190">**[此版本中所有已修正問題的清單-5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="91b08-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="91b08-191">摘要：5.0.2 版的新功能</span><span class="sxs-lookup"><span data-stu-id="91b08-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="91b08-192">透過 dotnet.exe 或 mono.exe) 執行時的安全性 (-應使用正確的許可權建立 obj 資料夾 [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="91b08-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="91b08-193">nuget.exe mono/MacOS 上的還原失敗，自訂 nuget.config 和 `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="91b08-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="91b08-194">已知問題</span><span class="sxs-lookup"><span data-stu-id="91b08-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="91b08-195">FallbackFolders 中由 .NET Core SDK 所安裝的套件是使用自訂方式安裝，而且未通過簽章驗證。</span><span class="sxs-lookup"><span data-stu-id="91b08-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="91b08-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="91b08-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="91b08-197">問題</span><span class="sxs-lookup"><span data-stu-id="91b08-197">Issue</span></span>
<span data-ttu-id="91b08-198">使用 dotnet.exe 2.x 來還原以 netcoreapp 1.x 與 netcoreapp 2.x 為多目標的專案時，後援資料夾被視為檔案摘要。</span><span class="sxs-lookup"><span data-stu-id="91b08-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="91b08-199">這表示，當還原時，NuGet 將會從後援資料夾挑選套件並嘗試將它安裝到全域套件資料夾，而且會執行平常的簽署驗證並失敗。</span><span class="sxs-lookup"><span data-stu-id="91b08-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="91b08-200">因應措施</span><span class="sxs-lookup"><span data-stu-id="91b08-200">Workaround</span></span>
<span data-ttu-id="91b08-201">將設定為 [無]，以停用 [回溯] 資料夾的使用方式 `RestoreAdditionalProjectSources` ：</span><span class="sxs-lookup"><span data-stu-id="91b08-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="91b08-202">請小心使用此方法，因為將會從 NuGet.org 下載將從回溯資料夾還原的封裝。</span><span class="sxs-lookup"><span data-stu-id="91b08-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>