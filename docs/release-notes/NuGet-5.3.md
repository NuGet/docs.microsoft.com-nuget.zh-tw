---
title: NuGet 5.3 版本資訊
description: NuGet 5.3 的版本資訊，包括新功能、bug 修正和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 994a0da3728e05a09b5537d150f2203477922efc
ms.sourcegitcommit: 904cbee57770af04efcae0b3709301685475bf64
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2019
ms.locfileid: "72962297"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="0cce9-103">NuGet 5.3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="0cce9-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="0cce9-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="0cce9-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="0cce9-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="0cce9-105">NuGet version</span></span> | <span data-ttu-id="0cce9-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="0cce9-106">Available in Visual Studio version</span></span>| <span data-ttu-id="0cce9-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0cce9-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="0cce9-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="0cce9-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="0cce9-109">Visual Studio 2019 16.3 版</span><span class="sxs-lookup"><span data-stu-id="0cce9-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="0cce9-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="0cce9-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="0cce9-111">**5.3.1**</span><span class="sxs-lookup"><span data-stu-id="0cce9-111">**5.3.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="0cce9-112">Visual Studio 2019 版本16.3。6</span><span class="sxs-lookup"><span data-stu-id="0cce9-112">Visual Studio 2019 version 16.3.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="0cce9-113">未來版本：3.0.101</span><span class="sxs-lookup"><span data-stu-id="0cce9-113">Future version: 3.0.101</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<span data-ttu-id="0cce9-114"><sup>1</sup>以含 .NET Core 工作負載的 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="0cce9-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="0cce9-115">摘要：5.3 中的新功能</span><span class="sxs-lookup"><span data-stu-id="0cce9-115">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="0cce9-116">[封裝圖示可以內嵌在封裝中](../reference/msbuild-targets.md#packing-an-icon-image-file)，而不需要外部 URL。</span><span class="sxs-lookup"><span data-stu-id="0cce9-116">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="0cce9-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="0cce9-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="0cce9-118">針對封裝進行 SHA 追蹤和強制執行的增強安全性- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="0cce9-118">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="0cce9-119">啟用淘汰/舊版 NuGet 套件的取代[#2867](https://github.com/NuGet/Home/issues/2867) | [Blog 文章](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [檔](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)</span><span class="sxs-lookup"><span data-stu-id="0cce9-119">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="0cce9-120">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="0cce9-120">Issues fixed in this release</span></span>

<span data-ttu-id="0cce9-121">**Bug**</span><span class="sxs-lookup"><span data-stu-id="0cce9-121">**Bugs**</span></span>

* <span data-ttu-id="0cce9-122">2\.2 SDK 使用者無法使用 3.0.100-preview9 SDK 所產生的 NuGet 套件 .。。視您的時區而定[#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="0cce9-122">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="0cce9-123">`nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)中的「路徑中的字元，路徑中有不合法的字元」錯誤</span><span class="sxs-lookup"><span data-stu-id="0cce9-123">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="0cce9-124">VS：元件完全是 ngen-ed，不是部分 ngen [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="0cce9-124">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="0cce9-125">減少記憶體使用量（取消訂閱事件）- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="0cce9-125">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="0cce9-126">"Error_UnableToFindProjectInfo" 訊息的語法不正確- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="0cce9-126">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="0cce9-127">NU1403 改進-驗證所有套件，包括預期/實際的 sha 值- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="0cce9-127">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="0cce9-128">`NuGetPackageManager.PreviewUpdatePackagesAsync` - 中的多個列舉[#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="0cce9-128">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="0cce9-129">還原 PluginProcess 中的「公用 > 內部」變更- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="0cce9-129">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="0cce9-130">IVsPackageSourceProvider. GetSources （...）定義錯誤的例外狀況行為- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="0cce9-130">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="0cce9-131">再次將 PluginManager 的函式設為公用- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="0cce9-131">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="0cce9-132">追蹤 PM UI 的重新整理頻率的計量- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="0cce9-132">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="0cce9-133">透過套件管理員 UI 安裝時，減少 UI 重新整理的次數- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="0cce9-133">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="0cce9-134">遙測： datetime 值使用特定文化特性格式- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="0cce9-134">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="0cce9-135">在套件管理員 UI 的 [流覽] 索引標籤中減少 UI 重新整理 #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="0cce9-135">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="0cce9-136">[測試失敗]「無法剖析設定檔」會提示兩次[#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="0cce9-136">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="0cce9-137">以良好的檔頁面引發 NU5037 錯誤，其中會說明客戶修正（套件缺少必要的 nuspec 檔案）- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="0cce9-137">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="0cce9-138">當專案的 RuntimeIdentifier 變更時，鎖定模式的還原會失敗- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="0cce9-138">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="0cce9-139">在 VS lazy [#8156](https://github.com/NuGet/Home/issues/8156)中進行讀取設定</span><span class="sxs-lookup"><span data-stu-id="0cce9-139">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="0cce9-140">`Nuget sources add` 中的回歸會導致 "'： ' 字元、十六進位值0x3A 不能包含在名稱" errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="0cce9-140">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="0cce9-141">NuGet 外掛程式認證提供者-隱藏進程視窗- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="0cce9-141">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="0cce9-142">強制 PackagePathResolver 是絕對路徑- [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="0cce9-142">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="0cce9-143">在套件管理員 UI 的 [安裝及更新] 索引標籤中減少 UI 重新整理- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="0cce9-143">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="0cce9-144">**DCR：**</span><span class="sxs-lookup"><span data-stu-id="0cce9-144">**DCR:**</span></span>

* <span data-ttu-id="0cce9-145">更新 Xamarin 架構以對應至 NetStandard 2.1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="0cce9-145">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="0cce9-146">針對安裝/更新[#8324](https://github.com/NuGet/Home/issues/8324) ，啟用複製套件管理員「預覽視窗」的內容</span><span class="sxs-lookup"><span data-stu-id="0cce9-146">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="0cce9-147">在 proj 檔案上啟用還原- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="0cce9-147">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="0cce9-148">引進 `NUGET_NETFX_PLUGIN_PATHS` 和 `NUGET_NETCORE_PLUGIN_PATHS` 以同時支援兩者的設定- [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="0cce9-148">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="0cce9-149">透過版本屬性啟用 PackageDownload 的多個版本- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="0cce9-149">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="0cce9-150">將-SolutionDirectory 和-PackageDirectory 選項新增至 nuget.exe pack- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="0cce9-150">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="0cce9-151">**[此版本中已修正的所有問題清單-5。3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="0cce9-151">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>

## <a name="summary-whats-new-in-531"></a><span data-ttu-id="0cce9-152">摘要：5.3.1 的新功能</span><span class="sxs-lookup"><span data-stu-id="0cce9-152">Summary: What's New in 5.3.1</span></span>

* <span data-ttu-id="0cce9-153">外掛程式：工作已取消-不要讓取消作業影響外掛程式具現化- [#8648](https://github.com/NuGet/Home/issues/8648)</span><span class="sxs-lookup"><span data-stu-id="0cce9-153">Plugin: A task was canceled - don't let cancellations affect plugin instantiation - [#8648](https://github.com/NuGet/Home/issues/8648)</span></span>

* <span data-ttu-id="0cce9-154">還原工作無法安全地在一個進程中執行兩次（使用認證提供者時）- [#8688](https://github.com/NuGet/Home/issues/8688)</span><span class="sxs-lookup"><span data-stu-id="0cce9-154">Restore Task cannot be safely run twice in one process (when Credential providers are used) - [#8688](https://github.com/NuGet/Home/issues/8688)</span></span>
