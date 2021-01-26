---
title: NuGet 5.3 版本資訊
description: NuGet 5.3 的版本資訊，包括新功能、bug 修正及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 009a219139a767ee6453305be68ccce478b0ec75
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780120"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="073ce-103">NuGet 5.3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="073ce-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="073ce-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="073ce-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="073ce-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="073ce-105">NuGet version</span></span> | <span data-ttu-id="073ce-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="073ce-106">Available in Visual Studio version</span></span>| <span data-ttu-id="073ce-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="073ce-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="073ce-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="073ce-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="073ce-109">Visual Studio 2019 16.3 版</span><span class="sxs-lookup"><span data-stu-id="073ce-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="073ce-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="073ce-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="073ce-111">**5.3.1**</span><span class="sxs-lookup"><span data-stu-id="073ce-111">**5.3.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="073ce-112">Visual Studio 2019 版本16.3.6 版</span><span class="sxs-lookup"><span data-stu-id="073ce-112">Visual Studio 2019 version 16.3.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="073ce-113">未來版本：3.0.101</span><span class="sxs-lookup"><span data-stu-id="073ce-113">Future version: 3.0.101</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<span data-ttu-id="073ce-114"><sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="073ce-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="073ce-115">摘要：5.3 中的新功能</span><span class="sxs-lookup"><span data-stu-id="073ce-115">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="073ce-116">[封裝圖示可以內嵌于封裝中](../reference/msbuild-targets.md#packing-an-icon-image-file)，而不需要外部 URL。</span><span class="sxs-lookup"><span data-stu-id="073ce-116">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="073ce-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="073ce-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="073ce-118">增強了 SHA 追蹤和強制執行 Packages.Config [#7281](https://github.com/NuGet/Home/issues/7281)的安全性</span><span class="sxs-lookup"><span data-stu-id="073ce-118">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="073ce-119">啟用淘汰/舊版 NuGet 套件的淘汰[#2867](https://github.com/NuGet/Home/issues/2867)  |  [Blog 文章](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/)  |  [](../nuget-org/deprecate-packages.md)檔</span><span class="sxs-lookup"><span data-stu-id="073ce-119">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](../nuget-org/deprecate-packages.md)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="073ce-120">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="073ce-120">Issues fixed in this release</span></span>

<span data-ttu-id="073ce-121">**Bug**</span><span class="sxs-lookup"><span data-stu-id="073ce-121">**Bugs**</span></span>

* <span data-ttu-id="073ce-122">2.2 SDK 使用者無法使用 3.0.100-preview9 SDK 所產生的 NuGet 套件 .。。視您的時區而定 [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="073ce-122">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="073ce-123">「路徑」中的字元會導致「路徑中有不合法的字元」失敗 `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="073ce-123">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="073ce-124">VS：元件完全是 ngen-ed，並非部分 ngen-ed- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="073ce-124">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="073ce-125">減少記憶體使用量 (取消訂閱事件) - [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="073ce-125">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="073ce-126">"Error_UnableToFindProjectInfo" 訊息的語法不正確- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="073ce-126">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="073ce-127">NU1403 改進-驗證所有封裝，包括預期/實際的 sha 值- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="073ce-127">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="073ce-128">#8401 中的多個列舉 `NuGetPackageManager.PreviewUpdatePackagesAsync`  -  [](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="073ce-128">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="073ce-129">還原 PluginProcess 中的「公用-> 內部」變更- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="073ce-129">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="073ce-130">IVsPackageSourceProvider. GetSources ( ... ) 定義錯誤的例外狀況行為- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="073ce-130">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="073ce-131">再次將 PluginManager 的函式設為公用- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="073ce-131">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="073ce-132">追蹤 PM UI 更新率的計量- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="073ce-132">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="073ce-133">當透過封裝管理員 UI 安裝時，減少 UI 重新整理的次數- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="073ce-133">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="073ce-134">遙測：日期時間值使用特定文化特性格式- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="073ce-134">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="073ce-135">在封裝管理員 UI 的 [流覽] 索引標籤中減少 UI 重新整理 #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="073ce-135">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="073ce-136">[測試失敗][無法剖析設定檔] 會出現兩次的提示 [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="073ce-136">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="073ce-137">使用良好的 doc 頁面引發 NU5037 錯誤，此頁面會解釋客戶修正 (套件缺少必要的 nuspec 檔) - [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="073ce-137">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="073ce-138">變更專案的 RuntimeIdentifier 時，鎖定模式還原失敗- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="073ce-138">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="073ce-139">將設定讀入 VS lazy [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="073ce-139">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="073ce-140">中的回歸 `Nuget sources add` 會導致 "'： ' 字元（十六進位值0x3A）不能包含在名稱" errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="073ce-140">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="073ce-141">NuGet 外掛程式認證提供者-隱藏進程視窗- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="073ce-141">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="073ce-142">強制 PackagePathResolver 是絕對路徑- [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="073ce-142">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="073ce-143">減少封裝管理員 UI 的 [安裝和更新] 索引標籤中的 UI 更新- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="073ce-143">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="073ce-144">**DCR：**</span><span class="sxs-lookup"><span data-stu-id="073ce-144">**DCR:**</span></span>

* <span data-ttu-id="073ce-145">將 Xamarin framework 更新為對應至 NetStandard 2.1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="073ce-145">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="073ce-146">針對安裝/更新- [#8324](https://github.com/NuGet/Home/issues/8324)啟用複製套件管理員 "preview window" 的內容</span><span class="sxs-lookup"><span data-stu-id="073ce-146">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="073ce-147">在 proj 檔案上啟用還原- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="073ce-147">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="073ce-148">引進 `NUGET_NETFX_PLUGIN_PATHS` 和 `NUGET_NETCORE_PLUGIN_PATHS` 支援同時設定兩者 [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="073ce-148">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="073ce-149">啟用 PackageDownload via Version 屬性的多個版本- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="073ce-149">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="073ce-150">將-SolutionDirectory 和-PackageDirectory 選項新增至 nuget.exe 套件- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="073ce-150">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="073ce-151">**[此版本修正的所有問題清單-5。3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="073ce-151">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>

## <a name="summary-whats-new-in-531"></a><span data-ttu-id="073ce-152">摘要：5.3.1 的新功能</span><span class="sxs-lookup"><span data-stu-id="073ce-152">Summary: What's New in 5.3.1</span></span>

* <span data-ttu-id="073ce-153">外掛程式：工作已取消-不要讓取消影響外掛程式具現化- [#8648](https://github.com/NuGet/Home/issues/8648)</span><span class="sxs-lookup"><span data-stu-id="073ce-153">Plugin: A task was canceled - don't let cancellations affect plugin instantiation - [#8648](https://github.com/NuGet/Home/issues/8648)</span></span>

* <span data-ttu-id="073ce-154">當使用認證提供者時，無法在一個進程 (中安全地執行還原工作) - [#8688](https://github.com/NuGet/Home/issues/8688)</span><span class="sxs-lookup"><span data-stu-id="073ce-154">Restore Task cannot be safely run twice in one process (when Credential providers are used) - [#8688](https://github.com/NuGet/Home/issues/8688)</span></span>
