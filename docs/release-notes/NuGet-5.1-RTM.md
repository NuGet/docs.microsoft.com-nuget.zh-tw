---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975832"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="cebc2-101">NuGet 5.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="cebc2-101">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="cebc2-102">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="cebc2-102">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="cebc2-103">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="cebc2-103">NuGet version</span></span> | <span data-ttu-id="cebc2-104">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="cebc2-104">Available in Visual Studio version</span></span>| <span data-ttu-id="cebc2-105">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="cebc2-105">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="cebc2-106">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="cebc2-106">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="cebc2-107">Visual Studio 2019 版本 16.1</span><span class="sxs-lookup"><span data-stu-id="cebc2-107">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="cebc2-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="cebc2-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="cebc2-109"><sup>1</sup>安裝的 Visual Studio 2019 是使用.NET Core 工作負載</span><span class="sxs-lookup"><span data-stu-id="cebc2-109"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="cebc2-110"><sup>2</sup>與.NET Core 工作負載的 Visual Studio 2019 提供選擇性的安裝</span><span class="sxs-lookup"><span data-stu-id="cebc2-110"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="cebc2-111">摘要: 在 5.1 中最新消息</span><span class="sxs-lookup"><span data-stu-id="cebc2-111">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="cebc2-112">如果已經存在以允許與 CI/CD 工作流程-更緊密整合，請略過封裝推送支援[# 1630年](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="cebc2-112">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="cebc2-113">Visual Studio 現在提供方便的連結，以套件的 nuget.org 資源庫頁面- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="cebc2-113">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="cebc2-114">這類支援.NET Core 3.0 的新資產[為目標的組件](https://github.com/dotnet/cli/issues/10006)和[執行階段組件](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="cebc2-114">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="cebc2-115">若要啟用目標和執行階段封裝參考-FrameworkReferences 支援 NuGet 封裝和還原[#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="cebc2-115">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="cebc2-116">支援 「 只下載 」 套件案例 PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="cebc2-116">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="cebc2-117">排除的執行階段和目標從搜尋結果與還原的套件圖形使用 PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="cebc2-117">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="cebc2-118">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="cebc2-118">Issues fixed in this release</span></span>

<span data-ttu-id="cebc2-119">**Bug**</span><span class="sxs-lookup"><span data-stu-id="cebc2-119">**Bugs**</span></span>

* <span data-ttu-id="cebc2-120">外掛程式： 例外狀況詳細資料遺失期間外掛程式- [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="cebc2-120">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="cebc2-121">PackageReference 獨佔的下限範圍無法運作如果下限是存在的其中一個來源。</span><span class="sxs-lookup"><span data-stu-id="cebc2-121">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="cebc2-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="cebc2-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="cebc2-123">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="cebc2-123">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="cebc2-124">封裝鎖定檔案-重新產生的鎖定檔案的專案圖形變更時- [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="cebc2-124">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="cebc2-125">ProjectSystem bug:Nuget 套件取得自動移除- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="cebc2-125">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="cebc2-126">新增的目標傳回 FrameworkReference 類似 CollectPackageDownloads 和 CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="cebc2-126">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="cebc2-127">HTTP 快取：RepositoryResources 資源不會快取版本控制的方式- [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="cebc2-127">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="cebc2-128">記錄： 例外狀況呼叫堆疊不會報告與詳細等級- [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="cebc2-128">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="cebc2-129">變更所有 NuGet Docs Url 使用 HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="cebc2-129">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="cebc2-130">改善 NU3024 警告訊息- [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="cebc2-130">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="cebc2-131">無法更新時鎖定檔案移除-packagereference [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="cebc2-131">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="cebc2-132">驗證在 nuspec-licenseurl 和授權的項目時，改善錯誤案例處理[#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="cebc2-132">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="cebc2-133">PM UI-以滑鼠右鍵按一下索引標籤行標頭，然後按一下 [開啟檔案位置] 會導致錯誤- [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="cebc2-133">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="cebc2-134">外掛程式： 記錄外掛程式處理序結束-時[#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="cebc2-134">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="cebc2-135">外掛程式： 記錄的日期時間值中高衝突率[#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="cebc2-135">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="cebc2-136">任何 nuspec LicenseExpression-與失敗 Manifest.ReadFrom [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="cebc2-136">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="cebc2-137">RestoreLockedMode:未預期的 NU1004 當參考的專案的自訂組件名稱-ProjectReference [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="cebc2-137">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="cebc2-138">更好的錯誤訊息時外掛程式啟動失敗並發生例外狀況- [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="cebc2-138">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="cebc2-139">NoOp 還原時，避免 \*。 在 obj 目錄-dgspec.json 寫入[#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="cebc2-139">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="cebc2-140">GeneratePathProperty = true 無法產生屬性上大小寫不符- [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="cebc2-140">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="cebc2-141">設定： 在 套件來源路徑不合法的字元可能會損毀 VS- [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="cebc2-141">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="cebc2-142">如果刪除鎖定檔案時，還原不會產生鎖定檔案上 NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="cebc2-142">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="cebc2-143">授權 URL 和授權讀取中繼資料-錯誤的原因[#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="cebc2-143">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="cebc2-144">未處理例外狀況中 V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="cebc2-144">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="cebc2-145">nuget.exe 會傳回無效的引數-的結束代碼為零[#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="cebc2-145">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="cebc2-146">更新 錯誤和警告文件以反映簽章的相關的案例- [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="cebc2-146">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="cebc2-147">資產檔案應該使用相對路徑，來更輕鬆地-啟用移動專案[#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="cebc2-147">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="cebc2-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="cebc2-148">**DCRs**</span></span>

* <span data-ttu-id="cebc2-149">外掛程式： 啟用診斷記錄- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="cebc2-149">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="cebc2-150">請 Tizen 6 對應為 NetStandard 2.1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="cebc2-150">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="cebc2-151">**[此版本為 5.1 RTM 修正的所有問題的清單](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="cebc2-151">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
