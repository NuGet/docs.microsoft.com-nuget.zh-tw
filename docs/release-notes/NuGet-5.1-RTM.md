---
title: NuGet 5.1 RTM 版本資訊
description: NuGet 5.1 的版本資訊，包括新功能、bug 修正及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: d6f6bffc6b5fda9ee1b9d9830f6d7d3c0f5be654
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780131"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="a94ad-103">NuGet 5.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="a94ad-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="a94ad-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="a94ad-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="a94ad-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="a94ad-105">NuGet version</span></span> | <span data-ttu-id="a94ad-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="a94ad-106">Available in Visual Studio version</span></span>| <span data-ttu-id="a94ad-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a94ad-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="a94ad-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="a94ad-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a94ad-109">Visual Studio 2019 16.1 版</span><span class="sxs-lookup"><span data-stu-id="a94ad-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a94ad-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="a94ad-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="a94ad-111"><sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="a94ad-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="a94ad-112"><sup>2</sup>可透過 .NET Core 工作負載，以選用的方式安裝 Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="a94ad-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="a94ad-113">摘要：5.1 中的新功能</span><span class="sxs-lookup"><span data-stu-id="a94ad-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="a94ad-114">支援略過封裝推送（如果已存在），以提供更好的 CI/CD 工作流程整合- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="a94ad-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="a94ad-115">Visual Studio 現在提供了一個方便的連結，可連至套件的 [nuget.org 資源庫] 頁面- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="a94ad-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="a94ad-116">支援新的 .NET Core 3.0 資產，例如 [目標套件](https://github.com/dotnet/cli/issues/10006) 和 [執行時間套件](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="a94ad-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="a94ad-117">FrameworkReferences 的 NuGet 套件和還原支援，以啟用目標和執行時間封裝參考- [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="a94ad-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="a94ad-118">支援「僅下載」套件案例與 PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="a94ad-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="a94ad-119">使用 PackageType 從搜尋結果中排除執行時間和目標套件 & restore graph- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="a94ad-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="a94ad-120">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="a94ad-120">Issues fixed in this release</span></span>

<span data-ttu-id="a94ad-121">**Bug**</span><span class="sxs-lookup"><span data-stu-id="a94ad-121">**Bugs**</span></span>

* <span data-ttu-id="a94ad-122">外掛程式：在外掛程式建立期間遺失例外狀況詳細資料- [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="a94ad-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="a94ad-123">如果其中一個來源上有下限，則具有獨佔下限的 PackageReference 範圍將無法運作。</span><span class="sxs-lookup"><span data-stu-id="a94ad-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="a94ad-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="a94ad-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="a94ad-125">改善 IsPackableFalseError 訊息- [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="a94ad-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="a94ad-126">封裝鎖定檔案-在專案圖形變更時重新產生鎖定檔案- [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="a94ad-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="a94ad-127">ProjectSystem bug：取得自動移除的 Nuget 套件- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="a94ad-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="a94ad-128">新增傳回 FrameworkReference 的目標，類似于 CollectPackageDownloads 和 CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="a94ad-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="a94ad-129">HTTP 快取： RepositoryResources 資源不會以已設定版本的方式快取- [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="a94ad-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="a94ad-130">記錄：未以詳細的詳細資訊[#7955](https://github.com/NuGet/Home/issues/7955)報告例外狀況呼叫堆疊</span><span class="sxs-lookup"><span data-stu-id="a94ad-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="a94ad-131">將所有 NuGet 檔 Url 變更為使用 HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="a94ad-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="a94ad-132">改善 NU3024 警告訊息- [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="a94ad-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="a94ad-133">packagereference 移除時鎖定檔案未更新- [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="a94ad-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="a94ad-134">改善在 nuspec 中驗證 licenseurl 和授權元素時的錯誤案例處理- [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="a94ad-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="a94ad-135">PM UI-以滑鼠右鍵按一下 tab 標頭，然後按一下 [開啟檔案位置] 會導致錯誤 [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="a94ad-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="a94ad-136">外掛程式：當外掛程式進程結束時記錄- [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="a94ad-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="a94ad-137">外掛程式：記錄日期時間值中的高衝突率- [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="a94ad-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="a94ad-138">資訊清單。具有 LicenseExpression [#7894](https://github.com/NuGet/Home/issues/7894)的任何 nuspec 上的 system.xml.linq.xnode.readfrom 失敗</span><span class="sxs-lookup"><span data-stu-id="a94ad-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="a94ad-139">RestoreLockedMode：當 ProjectReference 參考具有自訂 AssemblyName [#7889](https://github.com/NuGet/Home/issues/7889)的專案時，未預期的 NU1004</span><span class="sxs-lookup"><span data-stu-id="a94ad-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="a94ad-140">當外掛程式啟動失敗且發生例外狀況[#7857](https://github.com/NuGet/Home/issues/7857)時，會有更好的錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="a94ad-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="a94ad-141">進行 NoOp 還原時，請避免在 obj 目錄中寫入 \* .dgspec.js[#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="a94ad-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="a94ad-142">GeneratePathProperty = true 無法在案例不符時產生屬性- [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="a94ad-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="a94ad-143">設定：套件來源路徑中不合法的字元可能會損毀 VS- [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="a94ad-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="a94ad-144">如果刪除鎖定檔案，restore 不會在 NoOp 上產生鎖定檔案- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="a94ad-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="a94ad-145">授權 URL 和授權會導致中繼資料的讀取錯誤- [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="a94ad-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="a94ad-146">V2FeedParser 中未處理的例外狀況- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="a94ad-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="a94ad-147">nuget.exe 傳回無效引數的結束代碼零- [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="a94ad-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="a94ad-148">更新錯誤和警告檔以反映簽署相關案例- [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="a94ad-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="a94ad-149">資產檔案應該使用相對路徑來更輕鬆地啟用移動專案- [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="a94ad-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="a94ad-150">**DCR**</span><span class="sxs-lookup"><span data-stu-id="a94ad-150">**DCRs**</span></span>

* <span data-ttu-id="a94ad-151">外掛程式：啟用診斷記錄- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="a94ad-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="a94ad-152">將 Tizen 6 對應到 NetStandard 2.1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="a94ad-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="a94ad-153">**[此版本中所有已修正問題的清單-5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="a94ad-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
