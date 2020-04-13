---
title: NuGet 4.6 RTM 版本資訊
description: NuGet 4.6.0 版本資訊，包含已知問題、Bug 修正、新增功能和 DCR。
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: eacd29d4c9340a0f015fcdf6c5b9dd41bf781419
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498690"
---
# <a name="nuget-46-release-notes"></a><span data-ttu-id="6751e-103">NuGet 4.6 版本資訊</span><span class="sxs-lookup"><span data-stu-id="6751e-103">NuGet 4.6 Release Notes</span></span>

<span data-ttu-id="6751e-104">[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 隨附 [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe)。</span><span class="sxs-lookup"><span data-stu-id="6751e-104">[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-460"></a><span data-ttu-id="6751e-105">摘要:4.6.0 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="6751e-105">Summary: What's New in 4.6.0</span></span>

* <span data-ttu-id="6751e-106">新增了[簽署套件](../create-packages/sign-a-package.md)的支援。</span><span class="sxs-lookup"><span data-stu-id="6751e-106">We have added support for [signing packages](../create-packages/sign-a-package.md).</span></span>
* <span data-ttu-id="6751e-107">Visual Studio 2017 和 nuget.exe 現在會在安裝之前驗證套件的完整性，為[簽署的套件](../reference/signed-packages-reference.md)還原套件。</span><span class="sxs-lookup"><span data-stu-id="6751e-107">Visual Studio 2017 and nuget.exe now verifies package integrity before installing, restoring packages for [signed packages](../reference/signed-packages-reference.md).</span></span>
* <span data-ttu-id="6751e-108">改善了後續還原的效能。</span><span class="sxs-lookup"><span data-stu-id="6751e-108">We have improved performance of successive restores.</span></span>

## <a name="summary-whats-new-in-463"></a><span data-ttu-id="6751e-109">摘要:4.6.3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="6751e-109">Summary: What's New in 4.6.3</span></span>

* <span data-ttu-id="6751e-110">安全修復:在 #/.nuget 中創建的檔案的許可權在[CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673)太開放</span><span class="sxs-lookup"><span data-stu-id="6751e-110">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-464"></a><span data-ttu-id="6751e-111">摘要:4.6.4 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="6751e-111">Summary: What's New in 4.6.4</span></span>

* <span data-ttu-id="6751e-112">安全修復:NUPKG 內部的檔可以在 NUPKG 目錄上方具有相對路徑[#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="6751e-112">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="6751e-113">已知問題</span><span class="sxs-lookup"><span data-stu-id="6751e-113">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="6751e-114">含 .NET Framework 和 NuGet 的.NET Standard 2.0 問題</span><span class="sxs-lookup"><span data-stu-id="6751e-114">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="6751e-115">.NET Standard 和其工具的設計目的是讓目標設為 .NET Framework 4.6.1 的專案可以使用 NuGet 套件以及目標設為 .NET Standard 2.0 或更早版本的專案。</span><span class="sxs-lookup"><span data-stu-id="6751e-115">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="6751e-116">[這份文件](https://github.com/dotnet/standard/issues/481)摘要說明該情況的問題、解決它們的計劃，以及您可使用目前的工具狀態所部署的因應措施。</span><span class="sxs-lookup"><span data-stu-id="6751e-116">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

## <a name="top-issues-fixed-in-this-release"></a><span data-ttu-id="6751e-117">本版修正的主要問題</span><span class="sxs-lookup"><span data-stu-id="6751e-117">Top issues fixed in this release</span></span>

<span data-ttu-id="6751e-118">**效能修正**</span><span class="sxs-lookup"><span data-stu-id="6751e-118">**Performance fixes**</span></span>

* <span data-ttu-id="6751e-119">請勿在沒有任何變更時寫入資產檔案 - [#6491](https://github.com/NuGet/Home/issues/6491)</span><span class="sxs-lookup"><span data-stu-id="6751e-119">Don't write asset files when there is no change - [#6491](https://github.com/NuGet/Home/issues/6491)</span></span>
* <span data-ttu-id="6751e-120">當子專案的 TFM 與父專案的不符時，還原會造成額外的 MSBuild 評估 - [#6311](https://github.com/NuGet/Home/issues/6311)</span><span class="sxs-lookup"><span data-stu-id="6751e-120">Restore causes extra MSBuild evaluations when child projects' TFM do not match with the parent project's - [#6311](https://github.com/NuGet/Home/issues/6311)</span></span>
* <span data-ttu-id="6751e-121">將相依性關係圖的規格建立最佳化，以改善 NoOp 還原效能 - [#6252](https://github.com/NuGet/Home/issues/6252)</span><span class="sxs-lookup"><span data-stu-id="6751e-121">Improve NoOp restore perf by optimizing dependency graph spec creation - [#6252](https://github.com/NuGet/Home/issues/6252)</span></span>

<span data-ttu-id="6751e-122">**Bug**</span><span class="sxs-lookup"><span data-stu-id="6751e-122">**Bugs**</span></span>

* <span data-ttu-id="6751e-123">推送到本機資料夾會鎖定 nupkg - [#6325](https://github.com/NuGet/Home/issues/6325)</span><span class="sxs-lookup"><span data-stu-id="6751e-123">Push to local folder leaves nupkg locked - [#6325](https://github.com/NuGet/Home/issues/6325)</span></span>
* <span data-ttu-id="6751e-124">NuGet 外掛程式實作：多項問題 - [#6149](https://github.com/NuGet/Home/issues/6149)</span><span class="sxs-lookup"><span data-stu-id="6751e-124">NuGet Plugin implementation:  multiple issues - [#6149](https://github.com/NuGet/Home/issues/6149)</span></span>
* <span data-ttu-id="6751e-125">UIHang - 從 VSSolutionManager 的 MEF 初始化移除查詢服務呼叫 - [#6110](https://github.com/NuGet/Home/issues/6110)</span><span class="sxs-lookup"><span data-stu-id="6751e-125">UIHang - Remove query service call from MEF initialization in VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)</span></span>
* <span data-ttu-id="6751e-126">回報取消的套件下載工作有例外狀況時發生錯誤 - [#6096](https://github.com/NuGet/Home/issues/6096)</span><span class="sxs-lookup"><span data-stu-id="6751e-126">Error reporting exception for cancelled package download task - [#6096](https://github.com/NuGet/Home/issues/6096)</span></span>
* <span data-ttu-id="6751e-127">在組件名稱中，NuGet.exe 會將 '+' 取代為 '%2B' - [#5956](https://github.com/NuGet/Home/issues/5956)</span><span class="sxs-lookup"><span data-stu-id="6751e-127">NuGet.exe replaces '+' with '%2B' in assembly name - [#5956](https://github.com/NuGet/Home/issues/5956)</span></span>
* <span data-ttu-id="6751e-128">在 PM UI 和主控台，Fn + F1 不會導向正確的說明頁面 - [#5912](https://github.com/NuGet/Home/issues/5912)</span><span class="sxs-lookup"><span data-stu-id="6751e-128">Fn+F1 does not take to the right help page for PM UI and Console - [#5912](https://github.com/NuGet/Home/issues/5912)</span></span>
* <span data-ttu-id="6751e-129">VS NuGet 在特定情況下會將絕對路徑寫入專案檔 - [#5888](https://github.com/NuGet/Home/issues/5888)</span><span class="sxs-lookup"><span data-stu-id="6751e-129">VS NuGet writes absolute paths into project files under specific circumstances - [#5888](https://github.com/NuGet/Home/issues/5888)</span></span>
* <span data-ttu-id="6751e-130">修正 4.3 迴歸 - 預留位置 $product$ 和 $AssemblyGuid$ 未透過轉換在 contentfile 中取代 - [#5880](https://github.com/NuGet/Home/issues/5880)</span><span class="sxs-lookup"><span data-stu-id="6751e-130">Fix 4.3 regression - Placeholders $product$ and $AssemblyGuid$ not replaced in contentfile through transformation - [#5880](https://github.com/NuGet/Home/issues/5880)</span></span>
* <span data-ttu-id="6751e-131">dotnet restore 有多次原始檔損毀 - [#5817](https://github.com/NuGet/Home/issues/5817)</span><span class="sxs-lookup"><span data-stu-id="6751e-131">dotnet restore with multiple sources crashes - [#5817](https://github.com/NuGet/Home/issues/5817)</span></span>
* <span data-ttu-id="6751e-132">套件應重新評估專案版本，以允許 git 版本控制 - [#4790](https://github.com/NuGet/Home/issues/4790)</span><span class="sxs-lookup"><span data-stu-id="6751e-132">Pack should re-evaluate project versions to allow git versioning - [#4790](https://github.com/NuGet/Home/issues/4790)</span></span>
* <span data-ttu-id="6751e-133">改善了安裝不相容的套件時，難以理解的錯誤 - [#4555](https://github.com/NuGet/Home/issues/4555)</span><span class="sxs-lookup"><span data-stu-id="6751e-133">Improve hard to understand errors when you install an incompatible package - [#4555](https://github.com/NuGet/Home/issues/4555)</span></span>
* <span data-ttu-id="6751e-134">TemplateWizard 需要選項來將套件安裝為 PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)</span><span class="sxs-lookup"><span data-stu-id="6751e-134">TemplateWizard needs option to install packages as PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)</span></span>
* <span data-ttu-id="6751e-135">當 MSBuild.exe 從開發人員命令提示字元之外執行時，會略過套件傳遞的 props 檔案 - [#4530](https://github.com/NuGet/Home/issues/4530)</span><span class="sxs-lookup"><span data-stu-id="6751e-135">Package-delivered props files ignored when MSBuild.exe is run from outside a Developer Command Prompt - [#4530](https://github.com/NuGet/Home/issues/4530)</span></span>
* <span data-ttu-id="6751e-136">修正在參考不適用於專案的 .NET Standard 程式庫時，不良的錯誤訊息 - [#4423](https://github.com/NuGet/Home/issues/4423)</span><span class="sxs-lookup"><span data-stu-id="6751e-136">Fix poor error message when referencing .NET Standard Library that is not applicable to project - [#4423](https://github.com/NuGet/Home/issues/4423)</span></span>
* <span data-ttu-id="6751e-137">dotnet add package 在以可攜式設定檔為目標的套件會失敗，而且顯示很少指導 - [#4349](https://github.com/NuGet/Home/issues/4349)</span><span class="sxs-lookup"><span data-stu-id="6751e-137">dotnet add package fails for package targeting portable profile with little guidance - [#4349](https://github.com/NuGet/Home/issues/4349)</span></span>
* <span data-ttu-id="6751e-138">ProjectReference 中缺少 dotnet pack - 版本尾碼 - [#4337](https://github.com/NuGet/Home/issues/4337)</span><span class="sxs-lookup"><span data-stu-id="6751e-138">dotnet pack - version suffix missing from ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)</span></span>
* <span data-ttu-id="6751e-139">.NET Core 範本出現建置錯誤，而且 VS 會損毀 - [#3973](https://github.com/NuGet/Home/issues/3973)</span><span class="sxs-lookup"><span data-stu-id="6751e-139">Build errors and VS crash with .NET Core template - [#3973](https://github.com/NuGet/Home/issues/3973)</span></span>
* <span data-ttu-id="6751e-140">無法為來源 https:\* 載入服務索引 - [#3681](https://github.com/NuGet/Home/issues/3681)</span><span class="sxs-lookup"><span data-stu-id="6751e-140">Unable to load the service index for source https:\* - [#3681](https://github.com/NuGet/Home/issues/3681)</span></span>
* <span data-ttu-id="6751e-141">nuget.exe list -allversions 無法運作 - [#3441](https://github.com/NuGet/Home/issues/3441)</span><span class="sxs-lookup"><span data-stu-id="6751e-141">nuget.exe list -allversions doesn't work - [#3441](https://github.com/NuGet/Home/issues/3441)</span></span>
* <span data-ttu-id="6751e-142">誤導的相依性解析錯誤訊息 - [#2984](https://github.com/NuGet/Home/issues/2984)</span><span class="sxs-lookup"><span data-stu-id="6751e-142">Misleading dependency resolution error message - [#2984](https://github.com/NuGet/Home/issues/2984)</span></span>
* <span data-ttu-id="6751e-143">nuget.exe restore 不會為 .msbuildproj (v3.3.0-3.4.4 升級中的迴歸) 產生 .props 和 .targets 檔案 - [#2921](https://github.com/NuGet/Home/issues/2921)</span><span class="sxs-lookup"><span data-stu-id="6751e-143">nuget.exe restore doesn't produce .props and .targets files for .msbuildproj (regression in v3.3.0-3.4.4 upgrade) - [#2921](https://github.com/NuGet/Home/issues/2921)</span></span>
* <span data-ttu-id="6751e-144">在 XAML 檔案開啟的情況下，UI 會在更新 NuGet 套件時延遲 - [#2878](https://github.com/NuGet/Home/issues/2878)</span><span class="sxs-lookup"><span data-stu-id="6751e-144">UI delay when updating a NuGet package with XAML file open - [#2878](https://github.com/NuGet/Home/issues/2878)</span></span>
* <span data-ttu-id="6751e-145">來自 IIS 的 Web 專案因路徑中有不合法的字元而失敗 - [#2798](https://github.com/NuGet/Home/issues/2798)</span><span class="sxs-lookup"><span data-stu-id="6751e-145">WebSite project from IIS fails with illegal characters in path - [#2798](https://github.com/NuGet/Home/issues/2798)</span></span>
* <span data-ttu-id="6751e-146">Nuget add 在 CentOS 會停止回應 - [#2708](https://github.com/NuGet/Home/issues/2708)</span><span class="sxs-lookup"><span data-stu-id="6751e-146">Nuget add hangs on CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)</span></span>
* <span data-ttu-id="6751e-147">在 json.net 使用 packagesavemode -nupkg 進行還原會失敗 - [#2706](https://github.com/NuGet/Home/issues/2706)</span><span class="sxs-lookup"><span data-stu-id="6751e-147">Restore with packagesavemode -nupkg fails for json.net - [#2706](https://github.com/NuGet/Home/issues/2706)</span></span>
* <span data-ttu-id="6751e-148">在還原命令的 VS 輸出視窗中，套件管理員篩選無法使用 - [#2704](https://github.com/NuGet/Home/issues/2704)</span><span class="sxs-lookup"><span data-stu-id="6751e-148">Package Manager filter not available in vs output window for restore command - [#2704](https://github.com/NuGet/Home/issues/2704)</span></span>

[<span data-ttu-id="6751e-149">本版修正的所有問題清單</span><span class="sxs-lookup"><span data-stu-id="6751e-149">List of all issues fixed in this release</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
