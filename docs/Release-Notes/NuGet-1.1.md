---
title: "NuGet 1.0 和 1.1 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.1 版本資訊。"
keywords: "NuGet 1.1 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a596e61f144e7269f703f2dba3dddb4fd338e6a
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-10-and-11-release-notes"></a><span data-ttu-id="075f1-104">NuGet 1.0 和 1.1 版版本資訊</span><span class="sxs-lookup"><span data-stu-id="075f1-104">NuGet 1.0 and 1.1 Release Notes</span></span>

[<span data-ttu-id="075f1-105">NuGet 1.2 的版本資訊</span><span class="sxs-lookup"><span data-stu-id="075f1-105">NuGet 1.2 Release Notes</span></span>](../release-notes/nuget-1.2.md)

<span data-ttu-id="075f1-106">NuGet 1.0 已於 2011 年 1 月 13 日發行。</span><span class="sxs-lookup"><span data-stu-id="075f1-106">NuGet 1.0 was released on January 13, 2011.</span></span>  <span data-ttu-id="075f1-107">NuGet 1.1 已於 2011 年 2 月 12 日發行。</span><span class="sxs-lookup"><span data-stu-id="075f1-107">NuGet 1.1 was released on February 12, 2011.</span></span>

## <a name="overview"></a><span data-ttu-id="075f1-108">總覽</span><span class="sxs-lookup"><span data-stu-id="075f1-108">Overview</span></span>

<span data-ttu-id="075f1-109">本文件包含 NuGet 1.0 主要的預覽版本進行分組的各種版本的版本資訊。</span><span class="sxs-lookup"><span data-stu-id="075f1-109">This document contains the release notes for the various releases of NuGet 1.0 grouped according to major preview release.</span></span>

<span data-ttu-id="075f1-110">NuGet 會包含下列元件：</span><span class="sxs-lookup"><span data-stu-id="075f1-110">NuGet includes the following components:</span></span>

* <span data-ttu-id="075f1-111">*NuGet.Tools.vsix* \* 所組成：</span><span class="sxs-lookup"><span data-stu-id="075f1-111">*NuGet.Tools.vsix* \* which consists of:</span></span>
  * <span data-ttu-id="075f1-112">**新增程式庫封裝對話方塊**\* Visual Studio 用來瀏覽及安裝套件 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="075f1-112">**Add Library Package Dialog** \* Dialog within Visual Studio used to browse and install packages.</span></span>
  * <span data-ttu-id="075f1-113">**Package Manager Console** \* Powershell 型的 Visual Studio 中的主控台。</span><span class="sxs-lookup"><span data-stu-id="075f1-113">**Package Manager Console** \* Powershell based console within Visual Studio.</span></span>
* <span data-ttu-id="075f1-114">*NuGet 命令列工具*\* 工具用來建立 （及最終發佈） 封裝。</span><span class="sxs-lookup"><span data-stu-id="075f1-114">*NuGet Command Line Tool* \* Tool used to create (and eventually publish) packages.</span></span>

<span data-ttu-id="075f1-115">NuGet 工具 Visual Studio 擴充功能 (*NuGet.Tools.vsix*) 需要：</span><span class="sxs-lookup"><span data-stu-id="075f1-115">The NuGet Tools Visual Studio Extension (*NuGet.Tools.vsix*) requires:</span></span>

* <span data-ttu-id="075f1-116">Visual Studio 2010 或 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="075f1-116">Visual Studio 2010 or Visual Web Developer 2010 Express.</span></span>

<span data-ttu-id="075f1-117">需要 NuGet 命令列工具：</span><span class="sxs-lookup"><span data-stu-id="075f1-117">The NuGet Command Line Tool requires:</span></span>

* <span data-ttu-id="075f1-118">.NET framework 4 版</span><span class="sxs-lookup"><span data-stu-id="075f1-118">.NET Framework Version 4</span></span>

## <a name="installation"></a><span data-ttu-id="075f1-119">安裝</span><span class="sxs-lookup"><span data-stu-id="075f1-119">Installation</span></span>

<span data-ttu-id="075f1-120">若要使用這個[最新版本](http://nuget.codeplex.com/releases/view/52018):</span><span class="sxs-lookup"><span data-stu-id="075f1-120">To use this [latest release](http://nuget.codeplex.com/releases/view/52018):</span></span>

* <span data-ttu-id="075f1-121">先解除安裝較舊組建。</span><span class="sxs-lookup"><span data-stu-id="075f1-121">First uninstall your older build.</span></span> <span data-ttu-id="075f1-122">您要與執行以系統管理員身分執行此動作。</span><span class="sxs-lookup"><span data-stu-id="075f1-122">You need to run VS as administrator to do this.</span></span>
* <span data-ttu-id="075f1-123">移除您所擁有的所有現有摘要。</span><span class="sxs-lookup"><span data-stu-id="075f1-123">Remove all the existing feeds that you have.</span></span>
* <span data-ttu-id="075f1-124">加入新的摘要指向[http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669)。</span><span class="sxs-lookup"><span data-stu-id="075f1-124">Add a new feed pointing to [http://go.microsoft.com/fwlink/?LinkId=206669](http://go.microsoft.com/fwlink/?LinkId=206669).</span></span>

## <a name="nuget-11"></a><span data-ttu-id="075f1-125">NuGet 1.1</span><span class="sxs-lookup"><span data-stu-id="075f1-125">NuGet 1.1</span></span>

<span data-ttu-id="075f1-126">在此版本中修正的問題清單[可以在這裡找到](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)</span><span class="sxs-lookup"><span data-stu-id="075f1-126">The list of issues fixed in this release [can be found here](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)</span></span>

## <a name="nuget-10-rtm"></a><span data-ttu-id="075f1-127">NuGet 1.0 RTM</span><span class="sxs-lookup"><span data-stu-id="075f1-127">NuGet 1.0 RTM</span></span>

<span data-ttu-id="075f1-128">一個問題已修正自 RC RTM。</span><span class="sxs-lookup"><span data-stu-id="075f1-128">One issue was fixed for RTM since the RC.</span></span>

* [<span data-ttu-id="075f1-129">問題 474： 移除封裝會影響方案中的所有專案</span><span class="sxs-lookup"><span data-stu-id="075f1-129">Issue 474: Removing Packages Affects All Project In Solution</span></span>](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a><span data-ttu-id="075f1-130">發行候選版本</span><span class="sxs-lookup"><span data-stu-id="075f1-130">Release Candidate</span></span>

<span data-ttu-id="075f1-131">以下是自 CTP 2 本發行候選版本中所做的變更。</span><span class="sxs-lookup"><span data-stu-id="075f1-131">The following are the changes made in this Release Candidate since CTP 2.</span></span> <span data-ttu-id="075f1-132">請瀏覽問題追蹤程式，以查看完整的 bug 清單。</span><span class="sxs-lookup"><span data-stu-id="075f1-132">Visit the Issue Tracker to see the full list of bugs.</span></span>

* [<span data-ttu-id="075f1-133">更新套件的主控台不會更新相依性。</span><span class="sxs-lookup"><span data-stu-id="075f1-133">Updating Package from Console does not update dependencies.</span></span>](http://nuget.codeplex.com/workitem/443)
* [<span data-ttu-id="075f1-134">Bin 加入封裝拾取不套件參考 (CTP1)</span><span class="sxs-lookup"><span data-stu-id="075f1-134">Adding package picks up bin not package reference (CTP1)</span></span>](http://nuget.codeplex.com/workitem/442)
* [<span data-ttu-id="075f1-135">更新封裝離開中斷的參考</span><span class="sxs-lookup"><span data-stu-id="075f1-135">Updating a package leaves broken references</span></span>](http://nuget.codeplex.com/workitem/440)
* [<span data-ttu-id="075f1-136">取得封裝的更新失敗，在對話方塊中，或在主控台中選取 所有' 彙總來源</span><span class="sxs-lookup"><span data-stu-id="075f1-136">Get-Package -Updates fails in the dialog, or when the 'All' aggregate source is selected in the console</span></span>](http://nuget.codeplex.com/workitem/439)
* [<span data-ttu-id="075f1-137">取得封裝驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="075f1-137">Getting package verification errors</span></span>](http://nuget.codeplex.com/workitem/426)
* <span data-ttu-id="075f1-138">[無法安裝封裝，從 [新增套件] 對話方塊時警告使用者](http://nuget.codeplex.com/workitem/425)</span><span class="sxs-lookup"><span data-stu-id="075f1-138">[Warn users when a package cannot be installed from the Add Package Dialog](http://nuget.codeplex.com/workitem/425)</span></span>
* [<span data-ttu-id="075f1-139">取得封裝的更新封裝的大數目時，更新會擲回</span><span class="sxs-lookup"><span data-stu-id="075f1-139">Get-Package -Updates throws when updating large number of packages</span></span>](http://nuget.codeplex.com/workitem/424)
* [<span data-ttu-id="075f1-140">改善錯誤處理時 nuspec 檔案撰寫不正確</span><span class="sxs-lookup"><span data-stu-id="075f1-140">Improve error handling when nuspec files are authored incorrectly</span></span>](http://nuget.codeplex.com/workitem/423)
* [<span data-ttu-id="075f1-141">Nuget 套件會忽略指定的檔案</span><span class="sxs-lookup"><span data-stu-id="075f1-141">Nuget pack ignores specified files</span></span>](http://nuget.codeplex.com/workitem/422)
* <span data-ttu-id="075f1-142">[移除第二個到最後一個封裝來源，然後按一下 [下移] 損毀 VS](http://nuget.codeplex.com/workitem/418)</span><span class="sxs-lookup"><span data-stu-id="075f1-142">[Removing the second-to-last package source and then clicking "Move Down" crashes VS](http://nuget.codeplex.com/workitem/418)</span></span>
* [<span data-ttu-id="075f1-143">安裝封裝時移除組件參考</span><span class="sxs-lookup"><span data-stu-id="075f1-143">Remove assembly reference while installing packages</span></span>](http://nuget.codeplex.com/workitem/413)
* <span data-ttu-id="075f1-144">[開啟 [設定] 對話方塊時 InvalidOperationException](http://nuget.codeplex.com/workitem/411)</span><span class="sxs-lookup"><span data-stu-id="075f1-144">[InvalidOperationException when opening Settings dialog](http://nuget.codeplex.com/workitem/411)</span></span>
* [<span data-ttu-id="075f1-145">Package Manager Console 中的封裝來源的存取金鑰無法運作</span><span class="sxs-lookup"><span data-stu-id="075f1-145">Access Key for Package Source in Package Manager Console doesn't work</span></span>](http://nuget.codeplex.com/workitem/410)
* [<span data-ttu-id="075f1-146">NuGet VS 設定對話方塊存取的索引鍵將焦點提供給錯誤的欄位</span><span class="sxs-lookup"><span data-stu-id="075f1-146">NuGet VS Settings Dialog Access Keys Give Focus to Wrong Fields</span></span>](http://nuget.codeplex.com/workitem/409)
* [<span data-ttu-id="075f1-147">封裝識別碼 intellisense 不應該查詢項目太多</span><span class="sxs-lookup"><span data-stu-id="075f1-147">Package ID intellisense should not query too many items</span></span>](http://nuget.codeplex.com/workitem/404)
* [<span data-ttu-id="075f1-148">將封裝加入至專案，以點字元專案名稱中的失敗</span><span class="sxs-lookup"><span data-stu-id="075f1-148">Failure adding package to project with a dot character in the Project name</span></span>](http://nuget.codeplex.com/workitem/403)
* [<span data-ttu-id="075f1-149">Nuspec 中指定的檔案的問題</span><span class="sxs-lookup"><span data-stu-id="075f1-149">Issue with specified files in nuspec</span></span>](http://nuget.codeplex.com/workitem/400)
* [<span data-ttu-id="075f1-150">使用較新組建時，應該取得註冊正確官方摘要</span><span class="sxs-lookup"><span data-stu-id="075f1-150">Correct official feed should get registered when using newer build</span></span>](http://nuget.codeplex.com/workitem/399)
* [<span data-ttu-id="075f1-151">標記應該使用空格而不是 #</span><span class="sxs-lookup"><span data-stu-id="075f1-151">Tags should use spaces instead of #</span></span>](http://nuget.codeplex.com/workitem/397)
* [<span data-ttu-id="075f1-152">IPackageMetadata 缺少某些有用的資訊</span><span class="sxs-lookup"><span data-stu-id="075f1-152">IPackageMetadata lacks some useful information</span></span>](http://nuget.codeplex.com/workitem/388)
* [<span data-ttu-id="075f1-153">將報表濫用連結加入至對話方塊</span><span class="sxs-lookup"><span data-stu-id="075f1-153">Add Report Abuse Link to the Dialog</span></span>](http://nuget.codeplex.com/workitem/386)
* [<span data-ttu-id="075f1-154">若要解壓縮封裝符號，Visual Studio 中的使用 App_Data</span><span class="sxs-lookup"><span data-stu-id="075f1-154">Using App_Data to unzip packages breaks in Visual Studio</span></span>](http://nuget.codeplex.com/workitem/380)
* [<span data-ttu-id="075f1-155">實作標記</span><span class="sxs-lookup"><span data-stu-id="075f1-155">Implement Tags</span></span>](http://nuget.codeplex.com/workitem/376)
* [<span data-ttu-id="075f1-156">PackageBuilder 可讓不含相依性建立的空白封裝</span><span class="sxs-lookup"><span data-stu-id="075f1-156">PackageBuilder allows empty package with no dependencies to be created</span></span>](http://nuget.codeplex.com/workitem/373)
* [<span data-ttu-id="075f1-157">加入封裝的擁有者欄位</span><span class="sxs-lookup"><span data-stu-id="075f1-157">Add Owners Field for the Package</span></span>](http://nuget.codeplex.com/workitem/365)
* [<span data-ttu-id="075f1-158">更新說出 NuGet 封裝管理員，而不是 VSIX 工具的 VSIX 資訊清單</span><span class="sxs-lookup"><span data-stu-id="075f1-158">Update the VSIX manifest to say NuGet Package Manager rather than VSIX Tools</span></span>](http://nuget.codeplex.com/workitem/364)
* [<span data-ttu-id="075f1-159">取得封裝的命令在選取所有的來源時，會擲回錯誤</span><span class="sxs-lookup"><span data-stu-id="075f1-159">Get-Package command throws error when All source is selected</span></span>](http://nuget.codeplex.com/workitem/359)
* [<span data-ttu-id="075f1-160">允許的選項 對話方塊中的封裝來源順序</span><span class="sxs-lookup"><span data-stu-id="075f1-160">Allow ordering of package sources in Options dialog</span></span>](http://nuget.codeplex.com/workitem/356)
* [<span data-ttu-id="075f1-161">更新套件不會移除舊的版本</span><span class="sxs-lookup"><span data-stu-id="075f1-161">Update-Package does not remove older version</span></span>](http://nuget.codeplex.com/workitem/352)
* [<span data-ttu-id="075f1-162">相依性的實作版本範圍規格</span><span class="sxs-lookup"><span data-stu-id="075f1-162">Implement Version Range Specification for Dependencies</span></span>](http://nuget.codeplex.com/workitem/347)
* <span data-ttu-id="075f1-163">[按一下 [加入新的封裝] 時，visual Studio 損毀](http://nuget.codeplex.com/workitem/346)</span><span class="sxs-lookup"><span data-stu-id="075f1-163">[Visual Studio crashes when clicking "Add new package"](http://nuget.codeplex.com/workitem/346)</span></span>
* <span data-ttu-id="075f1-164">[在 [新增套件] 對話方塊中顯示的下載與分級](http://nuget.codeplex.com/workitem/345)</span><span class="sxs-lookup"><span data-stu-id="075f1-164">[Display Downloads and Ratings in the Add Package Dialog](http://nuget.codeplex.com/workitem/345)</span></span>
* [<span data-ttu-id="075f1-165">在對話方塊中的封裝來源之間的變更不會更新使用中的來源</span><span class="sxs-lookup"><span data-stu-id="075f1-165">Changing between package sources in the Dialog doesn't update active source</span></span>](http://nuget.codeplex.com/workitem/344)
* [<span data-ttu-id="075f1-166">移除封裝管理員主控台 視窗的索引鍵繫結</span><span class="sxs-lookup"><span data-stu-id="075f1-166">Remove Key Binding for Package Manager Console Window</span></span>](http://nuget.codeplex.com/workitem/339)
* [<span data-ttu-id="075f1-167">安裝套件無法辨識為指令程式名稱...</span><span class="sxs-lookup"><span data-stu-id="075f1-167">Install-Package is not recognized as the name of a cmdlet...</span></span>](http://nuget.codeplex.com/workitem/338)
* [<span data-ttu-id="075f1-168">無法解析安裝封裝，從本機摘要的相依性規則的摘要</span><span class="sxs-lookup"><span data-stu-id="075f1-168">Installing a package from a local feed the dependencies on regular feeds are not resolved</span></span>](http://nuget.codeplex.com/workitem/332)
* [<span data-ttu-id="075f1-169">RemoveDependencies 應該略過仍在使用的相依性</span><span class="sxs-lookup"><span data-stu-id="075f1-169">RemoveDependencies should skip dependencies that are still in use</span></span>](http://nuget.codeplex.com/workitem/331)
* [<span data-ttu-id="075f1-170">如果取消頁面巡覽，使用者無法瀏覽至其他頁面而原始頁面要求會傳回</span><span class="sxs-lookup"><span data-stu-id="075f1-170">If cancelling page navigation, user cannot navigate to a different page while the original page request returns</span></span>](http://nuget.codeplex.com/workitem/325)
* [<span data-ttu-id="075f1-171">請調查 NuPack.Server 的效能摘要提供使用大量的封裝。</span><span class="sxs-lookup"><span data-stu-id="075f1-171">Investigate performance of NuPack.Server for serving feeds with large number of packages.</span></span>](http://nuget.codeplex.com/workitem/324)
* [<span data-ttu-id="075f1-172">封裝的第二次我篩選它會使用 「 新增 」 封裝來源，而不是先前選取的來源。</span><span class="sxs-lookup"><span data-stu-id="075f1-172">The second time I filter for a package it uses the "New" package source, instead of the previously selected source.</span></span>](http://nuget.codeplex.com/workitem/321)
* [<span data-ttu-id="075f1-173">選取對話方塊上的 「 上線 」 索引標籤時，就應該選取預設的封裝來源。</span><span class="sxs-lookup"><span data-stu-id="075f1-173">Default package source should be selected when selecting the "Online" tab on the dialog.</span></span>](http://nuget.codeplex.com/workitem/320)
* [<span data-ttu-id="075f1-174">列出封裝應顯示預設的已安裝的封裝</span><span class="sxs-lookup"><span data-stu-id="075f1-174">List-Package should show installed packages by default</span></span>](http://nuget.codeplex.com/workitem/309)
* [<span data-ttu-id="075f1-175">組件參考 HintPaths</span><span class="sxs-lookup"><span data-stu-id="075f1-175">Assembly Reference HintPaths</span></span>](http://nuget.codeplex.com/workitem/294)
* [<span data-ttu-id="075f1-176">開啟 Package Manager Console 時發生例外狀況</span><span class="sxs-lookup"><span data-stu-id="075f1-176">Exception while opening Package Manager Console</span></span>](http://nuget.codeplex.com/workitem/268)
* [<span data-ttu-id="075f1-177">主控台 intellisense 下載整個摘要</span><span class="sxs-lookup"><span data-stu-id="075f1-177">Console intellisense downloads entire feed</span></span>](http://nuget.codeplex.com/workitem/259)
* [<span data-ttu-id="075f1-178">'Default' 封裝來源應該重新命名為 'Active'</span><span class="sxs-lookup"><span data-stu-id="075f1-178">'Default' package source should be renamed to 'Active'</span></span>](http://nuget.codeplex.com/workitem/258)
* <span data-ttu-id="075f1-179">[封裝來源 UI： 按下 [確定] 應該加入新的來源，如果名稱/來源欄位不可空白](http://nuget.codeplex.com/workitem/257)</span><span class="sxs-lookup"><span data-stu-id="075f1-179">[Package sources UI: pressing OK should add the new source if Name/Source fields are non-empty](http://nuget.codeplex.com/workitem/257)</span></span>
* [<span data-ttu-id="075f1-180">已安裝的封裝數目很大時，對話方塊變成 super 緩慢</span><span class="sxs-lookup"><span data-stu-id="075f1-180">Dialog becomes super slow when the number of installed packages is large</span></span>](http://nuget.codeplex.com/workitem/243)
* [<span data-ttu-id="075f1-181">支援強式名稱組件繫結重新導向</span><span class="sxs-lookup"><span data-stu-id="075f1-181">Support Binding Redirects for Strong Named Assemblies</span></span>](http://nuget.codeplex.com/workitem/238)
* [<span data-ttu-id="075f1-182">新增封裝參考...UI 以向下包含封裝來源拖放</span><span class="sxs-lookup"><span data-stu-id="075f1-182">Add Package Reference... UI to include drop down for Package source</span></span>](http://nuget.codeplex.com/workitem/226)
* [<span data-ttu-id="075f1-183">NuPack 需要支援的組態檔名稱 agnostically config 轉換</span><span class="sxs-lookup"><span data-stu-id="075f1-183">NuPack needs to support config transform agnostically of the config file name</span></span>](http://nuget.codeplex.com/workitem/224)
* [<span data-ttu-id="075f1-184">允許將它覆寫 NuPack.exe 中的基本路徑</span><span class="sxs-lookup"><span data-stu-id="075f1-184">Allows BasePath to be Overriden in NuPack.exe</span></span>](http://nuget.codeplex.com/workitem/222)
* [<span data-ttu-id="075f1-185">封裝來源後援行為</span><span class="sxs-lookup"><span data-stu-id="075f1-185">Package Source Fallback Behavior</span></span>](http://nuget.codeplex.com/workitem/204)
* [<span data-ttu-id="075f1-186">GUI 損毀</span><span class="sxs-lookup"><span data-stu-id="075f1-186">Crash on GUI</span></span>](http://nuget.codeplex.com/workitem/201)
* [<span data-ttu-id="075f1-187">加入排序新增套件 對話方塊的選項</span><span class="sxs-lookup"><span data-stu-id="075f1-187">Add sorting options to Add Package Dialog</span></span>](http://nuget.codeplex.com/workitem/179)
* [<span data-ttu-id="075f1-188">若要清除在 Package Manager Console 攠摝坫</span><span class="sxs-lookup"><span data-stu-id="075f1-188">shortcut key to clear the Package Manager Console</span></span>](http://nuget.codeplex.com/workitem/174)
* [<span data-ttu-id="075f1-189">PowerConsole 會導致失敗的 NuPack 主控台</span><span class="sxs-lookup"><span data-stu-id="075f1-189">PowerConsole causes NuPack Console to fail</span></span>](http://nuget.codeplex.com/workitem/166)
* [<span data-ttu-id="075f1-190">主控台和新增套件 對話方塊應該在要求中設定使用者代理程式</span><span class="sxs-lookup"><span data-stu-id="075f1-190">Console and Add Package Dialog should set user agent in requests</span></span>](http://nuget.codeplex.com/workitem/141)
* [<span data-ttu-id="075f1-191">在組建中，設定 VSIX 和 NuPack.exe 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="075f1-191">Set version number of the VSIX and NuPack.exe in the build.</span></span>](http://nuget.codeplex.com/workitem/134)
* [<span data-ttu-id="075f1-192">隱藏一般 PowerShell 參數？</span><span class="sxs-lookup"><span data-stu-id="075f1-192">Hide common PowerShell parameters from -?</span></span>](http://nuget.codeplex.com/workitem/118)
* [<span data-ttu-id="075f1-193">新增主控台命令詳細的的說明</span><span class="sxs-lookup"><span data-stu-id="075f1-193">Add -detailed help for console commands</span></span>](http://nuget.codeplex.com/workitem/110)
* [<span data-ttu-id="075f1-194">新增套件 對話方塊應該允許選擇目前的封裝來源</span><span class="sxs-lookup"><span data-stu-id="075f1-194">Add Package Dialog Should Allow Choosing the Current Package Source</span></span>](http://nuget.codeplex.com/workitem/88)
* [<span data-ttu-id="075f1-195">將 NuPack.Core 類別移至不同的命名空間</span><span class="sxs-lookup"><span data-stu-id="075f1-195">Move NuPack.Core classes into different namespaces</span></span>](http://nuget.codeplex.com/workitem/50)
* [<span data-ttu-id="075f1-196">新增至 cmdlet 的說明</span><span class="sxs-lookup"><span data-stu-id="075f1-196">Add help to cmdlets</span></span>](http://nuget.codeplex.com/workitem/23)
* [<span data-ttu-id="075f1-197">在套件下載後確認從摘要的雜湊</span><span class="sxs-lookup"><span data-stu-id="075f1-197">Verify hash from feed after package download</span></span>](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a><span data-ttu-id="075f1-198">CTP 2</span><span class="sxs-lookup"><span data-stu-id="075f1-198">CTP 2</span></span>

<span data-ttu-id="075f1-199">以下是最重要 CTP 2 中所做的變更：</span><span class="sxs-lookup"><span data-stu-id="075f1-199">The following are the most significant changes made in CTP 2:</span></span>

* <span data-ttu-id="075f1-200">切換至 OData 服務端點從 ATOM 摘要的封裝： 如果您升級到 CTP2 版本的 NuGet，請務必新增為套件來源的下列 URL: https://feed.nuget.org/ctp2/odata/v1/。</span><span class="sxs-lookup"><span data-stu-id="075f1-200">Switched the package feed from ATOM to an OData service endpoint: If you upgrade to the CTP2 version of NuGet, be sure to add the following URL as a package source: https://feed.nuget.org/ctp2/odata/v1/.</span></span>
* <span data-ttu-id="075f1-201">重新命名以 [新增套件] 命令*Install-package*。</span><span class="sxs-lookup"><span data-stu-id="075f1-201">Renamed the Add-Package command to *Install-Package*.</span></span>
* <span data-ttu-id="075f1-202">更新`.nuspec`格式。</span><span class="sxs-lookup"><span data-stu-id="075f1-202">Updated the `.nuspec` Format.</span></span> <span data-ttu-id="075f1-203">`.nuspec`格式現在包含*iconUrl*欄位來指定將會顯示在 [新增套件] 對話方塊 32 x 32 png 圖示。</span><span class="sxs-lookup"><span data-stu-id="075f1-203">The `.nuspec` format now includes the *iconUrl* field for specifying a 32x32 png icon which will show up in the Add Package Dialog.</span></span> <span data-ttu-id="075f1-204">因此請務必設定，以區別您的封裝。</span><span class="sxs-lookup"><span data-stu-id="075f1-204">So be sure to set that to distinguish your package.</span></span> <span data-ttu-id="075f1-205">`.nuspec`格式亦包含新*projectUrl*欄位可用來指向提供封裝的詳細資訊的網頁。</span><span class="sxs-lookup"><span data-stu-id="075f1-205">The `.nuspec` format also includes the new *projectUrl* field which you can use to point to a web page that provides more information about your package.</span></span>

<span data-ttu-id="075f1-206">此組建將無法運作，與舊`.nupkg`檔案。</span><span class="sxs-lookup"><span data-stu-id="075f1-206">This build will not work with old `.nupkg` files.</span></span> <span data-ttu-id="075f1-207">如果您收到 null 參考例外狀況，您要使用舊`.nupkg`檔案，並需要重建與更新[NuGet 命令列工具](http://nuget.codeplex.com/releases/52017/download/165468)。</span><span class="sxs-lookup"><span data-stu-id="075f1-207">If you get null reference exceptions, you're using an old `.nupkg` file and need to rebuild it with the updated [NuGet command line tool](http://nuget.codeplex.com/releases/52017/download/165468).</span></span>

<span data-ttu-id="075f1-208">以下是功能清單 （不包括錯誤的次要的程式碼清除等）。 NuGet CTP 2 已獲得修正的 bug。</span><span class="sxs-lookup"><span data-stu-id="075f1-208">The following is a list of features and bugs that were fixed for NuGet CTP 2 (does not include bugs for minor code cleanups etc.).</span></span>

* [<span data-ttu-id="075f1-209">解壓縮封裝組件的錯誤時與指定之組件 TargetFramework。</span><span class="sxs-lookup"><span data-stu-id="075f1-209">Error unpacking package assemblies when specifiying the TargetFramework for an assembly.</span></span>](http://nuget.codeplex.com/workitem/10)
* [<span data-ttu-id="075f1-210">請更容易找到 NuPack 主控台視窗</span><span class="sxs-lookup"><span data-stu-id="075f1-210">Make NuPack Console window more discoverable</span></span>](http://nuget.codeplex.com/workitem/14)
* [<span data-ttu-id="075f1-211">ILMerge nupack.exe 版本</span><span class="sxs-lookup"><span data-stu-id="075f1-211">ILMerge the nupack.exe release</span></span>](http://nuget.codeplex.com/workitem/19)
* [<span data-ttu-id="075f1-212">更好的錯誤/例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="075f1-212">Better error/exception handling</span></span>](http://nuget.codeplex.com/workitem/24)
* <span data-ttu-id="075f1-213">[[Nupack.Core]: PackageManager 應妥善處理摘要相關的錯誤](http://nuget.codeplex.com/workitem/28)</span><span class="sxs-lookup"><span data-stu-id="075f1-213">[[Nupack.Core]: PackageManager should gracefully handle feed-related errors](http://nuget.codeplex.com/workitem/28)</span></span>
* [<span data-ttu-id="075f1-214">主控台需要新的圖示</span><span class="sxs-lookup"><span data-stu-id="075f1-214">Need a new icon for the console</span></span>](http://nuget.codeplex.com/workitem/29)
* [<span data-ttu-id="075f1-215">在對話方塊中的字串當地語系化</span><span class="sxs-lookup"><span data-stu-id="075f1-215">Localize strings in the Dialog</span></span>](http://nuget.codeplex.com/workitem/38)
* [<span data-ttu-id="075f1-216">NuPack 快取下載的.nupack 檔案中的記憶體</span><span class="sxs-lookup"><span data-stu-id="075f1-216">NuPack caches downloaded .nupack files in memory</span></span>](http://nuget.codeplex.com/workitem/40)
* [<span data-ttu-id="075f1-217">NuPack 主控台： 變更預設快速鍵顯示主控台</span><span class="sxs-lookup"><span data-stu-id="075f1-217">NuPack Console: Change the default shortcut for displaying console</span></span>](http://nuget.codeplex.com/workitem/48)
* [<span data-ttu-id="075f1-218">ProjectSystem 應該支援的通用屬性的預設值</span><span class="sxs-lookup"><span data-stu-id="075f1-218">ProjectSystem should support default values for common properties</span></span>](http://nuget.codeplex.com/workitem/49)
* [<span data-ttu-id="075f1-219">執行 nupack.exe 資料夾中只有一個 nuspec 檔案，則應該使用該 nuspec</span><span class="sxs-lookup"><span data-stu-id="075f1-219">Running nupack.exe in a folder with just one nuspec file should use that nuspec</span></span>](http://nuget.codeplex.com/workitem/52)
* [<span data-ttu-id="075f1-220">即使載入任何專案/方案時顯示的專案 功能表</span><span class="sxs-lookup"><span data-stu-id="075f1-220">Project Menu Shows Up Even When No Project/Solution Is Loaded</span></span>](http://nuget.codeplex.com/workitem/54)
* [<span data-ttu-id="075f1-221">在程式碼基底的全新複本上的 build.cmd 失敗</span><span class="sxs-lookup"><span data-stu-id="075f1-221">build.cmd fails on a clean clone of the codebase</span></span>](http://nuget.codeplex.com/workitem/56)
* [<span data-ttu-id="075f1-222">更新可用的功能</span><span class="sxs-lookup"><span data-stu-id="075f1-222">Updates available feature</span></span>](http://nuget.codeplex.com/workitem/57)
* [<span data-ttu-id="075f1-223">對話方塊： 加入封裝，以透過對話方塊在主控台中移除提示</span><span class="sxs-lookup"><span data-stu-id="075f1-223">Dialog: Adding a package through the dialog removes the prompt in the console</span></span>](http://nuget.codeplex.com/workitem/73)
* <span data-ttu-id="075f1-224">[新增套件，依序按一下 [安裝] 通常是沒有視覺回應緩慢](http://nuget.codeplex.com/workitem/80)</span><span class="sxs-lookup"><span data-stu-id="075f1-224">[Adding a package by clicking 'Install' is often slow, with no visual feedback](http://nuget.codeplex.com/workitem/80)</span></span>
* [<span data-ttu-id="075f1-225">沒有任何方法來探索我已安裝的套件必須有更新。</span><span class="sxs-lookup"><span data-stu-id="075f1-225">There is no way to discover which of my installed packages have updates.</span></span>](http://nuget.codeplex.com/workitem/82)
* [<span data-ttu-id="075f1-226">沒有任何方法以更新對話方塊中已安裝的封裝。</span><span class="sxs-lookup"><span data-stu-id="075f1-226">There is no way to update an installed package in the dialog.</span></span>](http://nuget.codeplex.com/workitem/83)
* [<span data-ttu-id="075f1-227">沒有任何方法來解除安裝 對話方塊中已安裝的封裝</span><span class="sxs-lookup"><span data-stu-id="075f1-227">There is no way to uninstall an installed package in the dialog</span></span>](http://nuget.codeplex.com/workitem/84)
* [<span data-ttu-id="075f1-228">&ldquo;新增封裝參考&hellip;&rdquo;會出現在已安裝參照的內容功能表</span><span class="sxs-lookup"><span data-stu-id="075f1-228">&ldquo;Add Package Reference&hellip;&rdquo; appears on the context menu of installed references</span></span>](http://nuget.codeplex.com/workitem/85)
* [<span data-ttu-id="075f1-229">在更新之後從主控台的封裝，它會顯示舊的版本與新的版本已安裝</span><span class="sxs-lookup"><span data-stu-id="075f1-229">After updating a package from the console, it shows both the old version and the new version as installed</span></span>](http://nuget.codeplex.com/workitem/86)
* [<span data-ttu-id="075f1-230">使用之後，在主控台中，當使用對話方塊中，活動會消失</span><span class="sxs-lookup"><span data-stu-id="075f1-230">The activity in the console, when using the dialog, disappears after use</span></span>](http://nuget.codeplex.com/workitem/87)
* [<span data-ttu-id="075f1-231">清除命令列剖析 nupack.exe 中</span><span class="sxs-lookup"><span data-stu-id="075f1-231">Cleanup command line parsing in nupack.exe</span></span>](http://nuget.codeplex.com/workitem/89)
* [<span data-ttu-id="075f1-232">加入封裝來源中的易記名稱</span><span class="sxs-lookup"><span data-stu-id="075f1-232">Add a friendly name to package sources</span></span>](http://nuget.codeplex.com/workitem/98)
* [<span data-ttu-id="075f1-233">更新.nuspec 支援包括套件圖示</span><span class="sxs-lookup"><span data-stu-id="075f1-233">Update .nuspec to support including package icons</span></span>](http://nuget.codeplex.com/workitem/103)
* [<span data-ttu-id="075f1-234">摘要的 UI 不允許複製 URL</span><span class="sxs-lookup"><span data-stu-id="075f1-234">Feed UI doesn't allow copying the URL</span></span>](http://nuget.codeplex.com/workitem/105)
* [<span data-ttu-id="075f1-235">更好的移除封裝的錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="075f1-235">Better remove-package error handling.</span></span>](http://nuget.codeplex.com/workitem/107)
* [<span data-ttu-id="075f1-236">在主控台視窗中輸入取決於將游標焦點</span><span class="sxs-lookup"><span data-stu-id="075f1-236">Typing in Console Window depends on cursor focus</span></span>](http://nuget.codeplex.com/workitem/112)
* [<span data-ttu-id="075f1-237">錯誤訊息看起來的樣子</span><span class="sxs-lookup"><span data-stu-id="075f1-237">Error messages look awful</span></span>](http://nuget.codeplex.com/workitem/116)
* [<span data-ttu-id="075f1-238">移除封裝的效能，也未安裝的套件已損毀</span><span class="sxs-lookup"><span data-stu-id="075f1-238">The performance of Remove-Package for a package that isn't installed is bad</span></span>](http://nuget.codeplex.com/workitem/117)
* [<span data-ttu-id="075f1-239">移除封裝失敗時沒有套件來源</span><span class="sxs-lookup"><span data-stu-id="075f1-239">Removing a package fails when there are no package sources</span></span>](http://nuget.codeplex.com/workitem/119)
* [<span data-ttu-id="075f1-240">封裝來源無法使用時，移除封裝會失敗</span><span class="sxs-lookup"><span data-stu-id="075f1-240">Remove-Package fails when the package source is unavailable</span></span>](http://nuget.codeplex.com/workitem/120)
* [<span data-ttu-id="075f1-241">加入封裝中繼資料和摘要的標題。</span><span class="sxs-lookup"><span data-stu-id="075f1-241">Add Title to the package metadata and the feed.</span></span>](http://nuget.codeplex.com/workitem/125)
* [<span data-ttu-id="075f1-242">新增-來源參數傳回給加入封裝</span><span class="sxs-lookup"><span data-stu-id="075f1-242">Add the -Source parameter back to Add-Package</span></span>](http://nuget.codeplex.com/workitem/127)
* [<span data-ttu-id="075f1-243">清單套件都應該有-來源參數</span><span class="sxs-lookup"><span data-stu-id="075f1-243">List-Package should have a -Source parameter</span></span>](http://nuget.codeplex.com/workitem/128)
* [<span data-ttu-id="075f1-244">若要要求 NuPack 使用者代理程式來下載套件的更新 NuPack.Server</span><span class="sxs-lookup"><span data-stu-id="075f1-244">Update NuPack.Server to require NuPack User Agent To Download Package</span></span>](http://nuget.codeplex.com/workitem/142)
* [<span data-ttu-id="075f1-245">授權接受對話方塊必須列出授權要求接受的所有相依性</span><span class="sxs-lookup"><span data-stu-id="075f1-245">License Acceptance Dialog Must List Licenses For All Dependencies That Require Acceptance</span></span>](http://nuget.codeplex.com/workitem/145)
* [<span data-ttu-id="075f1-246">記錄錯誤時封裝就會擲回之摘要中</span><span class="sxs-lookup"><span data-stu-id="075f1-246">Log an error when a package throws in the feed</span></span>](http://nuget.codeplex.com/workitem/150)
* [<span data-ttu-id="075f1-247">NuPack.exe 應該不允許空&lt;licenseurl&gt;項目</span><span class="sxs-lookup"><span data-stu-id="075f1-247">NuPack.exe should not allow an empty &lt;licenseurl&gt; element</span></span>](http://nuget.codeplex.com/workitem/152)
* [<span data-ttu-id="075f1-248">將列出封裝重新命名為 Get 封裝，加入-封裝安裝套件，並移除套件解除安裝套件</span><span class="sxs-lookup"><span data-stu-id="075f1-248">Rename List-Package to Get-Package, Add-Package to Install-Package, and Remove-Package to Uninstall-Package</span></span>](http://nuget.codeplex.com/workitem/155)
* [<span data-ttu-id="075f1-249">使用新增封裝參考功能表項目，從方案導覽損毀 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="075f1-249">Using the Add Package Reference menu item from the Solution Navigator crashes Visual Studio</span></span>](http://nuget.codeplex.com/workitem/158)
* <span data-ttu-id="075f1-250">[遺漏冒號 [可用的封裝來源] 標籤。](http://nuget.codeplex.com/workitem/160)</span><span class="sxs-lookup"><span data-stu-id="075f1-250">["Available package sources" label is missing a colon](http://nuget.codeplex.com/workitem/160)</span></span>
* [<span data-ttu-id="075f1-251">請.nuspec xml 項目大小寫一致地 camel 命名法的大小寫</span><span class="sxs-lookup"><span data-stu-id="075f1-251">Make .nuspec xml element casing consistently camel cased</span></span>](http://nuget.codeplex.com/workitem/161)
* [<span data-ttu-id="075f1-252">若要開啟 「 管理員 」 位元必須 NuPack VSIX 資訊清單</span><span class="sxs-lookup"><span data-stu-id="075f1-252">The NuPack VSIX's manifest needs to turn on the 'admin' bit</span></span>](http://nuget.codeplex.com/workitem/162)
* [<span data-ttu-id="075f1-253">如果您列出封裝執行了任何摘要時，會產生 null 參考錯誤</span><span class="sxs-lookup"><span data-stu-id="075f1-253">If you run List-Package with no feeds, you get null ref error</span></span>](http://nuget.codeplex.com/workitem/164)
* [<span data-ttu-id="075f1-254">nuget.exe： 指定目的地路徑</span><span class="sxs-lookup"><span data-stu-id="075f1-254">nuget.exe: specify destination path</span></span>](http://nuget.codeplex.com/workitem/171)
* [<span data-ttu-id="075f1-255">開啟 套件管理主控台上 WinXP Powershell 錯誤</span><span class="sxs-lookup"><span data-stu-id="075f1-255">Powershell Errors Opening Package Management Console on WinXP</span></span>](http://nuget.codeplex.com/workitem/175)
* [<span data-ttu-id="075f1-256">VS 損毀時嘗試載入的封裝清單</span><span class="sxs-lookup"><span data-stu-id="075f1-256">VS Crashes while trying to load package list</span></span>](http://nuget.codeplex.com/workitem/176)
* [<span data-ttu-id="075f1-257">允許中繼封裝 （沒有檔案、 相依性）</span><span class="sxs-lookup"><span data-stu-id="075f1-257">allow meta packages (no files, only dependencies)</span></span>](http://nuget.codeplex.com/workitem/180)
* [<span data-ttu-id="075f1-258">將 Powershell 指令碼轉換成 Powershell 2.0 模組</span><span class="sxs-lookup"><span data-stu-id="075f1-258">Convert Powershell Script to Powershell 2.0 Module</span></span>](http://nuget.codeplex.com/workitem/181)
* [<span data-ttu-id="075f1-259">指定目標時，PathResolver 應該捨棄路徑部分都與先前萬用字元</span><span class="sxs-lookup"><span data-stu-id="075f1-259">PathResolver should discard path portion preceeding wildcard characters when target is specified</span></span>](http://nuget.codeplex.com/workitem/183)
* [<span data-ttu-id="075f1-260">沒有任何相依性</span><span class="sxs-lookup"><span data-stu-id="075f1-260">No dependencies</span></span>](http://nuget.codeplex.com/workitem/186)
* [<span data-ttu-id="075f1-261">安裝 Elmah 時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="075f1-261">Error installing Elmah</span></span>](http://nuget.codeplex.com/workitem/192)
* [<span data-ttu-id="075f1-262">設定轉換不正確地使用&lt;c&gt;</span><span class="sxs-lookup"><span data-stu-id="075f1-262">Config transforms don't work correctly with &lt;configsections&gt;</span></span>](http://nuget.codeplex.com/workitem/194)
* [<span data-ttu-id="075f1-263">變數 ' $全域： projectCache' 無法擷取，因為尚未設定</span><span class="sxs-lookup"><span data-stu-id="075f1-263">The variable '$global:projectCache' cannot be retrieved because it has not been set</span></span>](http://nuget.codeplex.com/workitem/203)
* [<span data-ttu-id="075f1-264">將加入 MSBuild 工作，以建立 NuPack 封裝</span><span class="sxs-lookup"><span data-stu-id="075f1-264">Add MSBuild task for creating NuPack packages</span></span>](http://nuget.codeplex.com/workitem/205)
* [<span data-ttu-id="075f1-265">列出封裝需要支援搜尋/篩選</span><span class="sxs-lookup"><span data-stu-id="075f1-265">list-package needs to support searching/filtering</span></span>](http://nuget.codeplex.com/workitem/206)
* [<span data-ttu-id="075f1-266">一律授權如果封裝作者提供授權 URL</span><span class="sxs-lookup"><span data-stu-id="075f1-266">Always display a link to license if the package author provides a license URL</span></span>](http://nuget.codeplex.com/workitem/208)
* [<span data-ttu-id="075f1-267">偶發的 「 拒絕存取 」 例外狀況，並移除封裝</span><span class="sxs-lookup"><span data-stu-id="075f1-267">Occasional "Access Denied" exception with Remove-Package</span></span>](http://nuget.codeplex.com/workitem/213)
* [<span data-ttu-id="075f1-268">單元測試失敗： InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries</span><span class="sxs-lookup"><span data-stu-id="075f1-268">Unit Tests Failing: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries</span></span>](http://nuget.codeplex.com/workitem/214)
* [<span data-ttu-id="075f1-269">允許後援/預設的檔案集，如果找不到以特定的 framework 版本</span><span class="sxs-lookup"><span data-stu-id="075f1-269">Allow for a fallback/default set of files if a specfic framework version cannot be found</span></span>](http://nuget.codeplex.com/workitem/223)
* [<span data-ttu-id="075f1-270">新增封裝參考...UI 無法移除封裝</span><span class="sxs-lookup"><span data-stu-id="075f1-270">Add Package Reference... UI cannot remove a package</span></span>](http://nuget.codeplex.com/workitem/225)
* [<span data-ttu-id="075f1-271">新增封裝參考發生當機 studio 當一個或多個專案是卸載</span><span class="sxs-lookup"><span data-stu-id="075f1-271">Add Package Reference crashes studio when one or more project is unloaded</span></span>](http://nuget.codeplex.com/workitem/228)
* [<span data-ttu-id="075f1-272">Config 轉換，似乎不處理 web.debug.config 檔案</span><span class="sxs-lookup"><span data-stu-id="075f1-272">Config transform does not appear to work on web.debug.config file</span></span>](http://nuget.codeplex.com/workitem/229)
* [<span data-ttu-id="075f1-273">init.ps1 不引發自訂封裝</span><span class="sxs-lookup"><span data-stu-id="075f1-273">init.ps1 not firing on custom package</span></span>](http://nuget.codeplex.com/workitem/237)
* <span data-ttu-id="075f1-274">[將路徑加入至 feedlist 的預設按鈕設為 [確定]，因此如果按 ENTER 它會自動關閉](http://nuget.codeplex.com/workitem/240)</span><span class="sxs-lookup"><span data-stu-id="075f1-274">[When adding paths to the feedlist, the default button is set to OK, so if I press ENTER it automatically closes](http://nuget.codeplex.com/workitem/240)</span></span>
* [<span data-ttu-id="075f1-275">嘗試解除安裝相依性將會損毀 VS，如果嘗試在資料列中的 2 倍</span><span class="sxs-lookup"><span data-stu-id="075f1-275">Attempt to uninstall a dependency will crash VS if attempted 2 times in a row</span></span>](http://nuget.codeplex.com/workitem/241)
* <span data-ttu-id="075f1-276">[在 [新增套件] 對話方塊中顯示專案 URL](http://nuget.codeplex.com/workitem/253)</span><span class="sxs-lookup"><span data-stu-id="075f1-276">[Display the Project URL in the Add Package dialog](http://nuget.codeplex.com/workitem/253)</span></span>
* <span data-ttu-id="075f1-277">[預設已安裝的套件 [新增套件] 對話方塊](http://nuget.codeplex.com/workitem/254)</span><span class="sxs-lookup"><span data-stu-id="075f1-277">[Default the Add-Package dialog to Installed Packages](http://nuget.codeplex.com/workitem/254)</span></span>
* [<span data-ttu-id="075f1-278">將變更新增套件 對話方塊的功能表項目。</span><span class="sxs-lookup"><span data-stu-id="075f1-278">Change Add Package Dialog menu item.</span></span>](http://nuget.codeplex.com/workitem/261)
* [<span data-ttu-id="075f1-279">重新命名的命名空間和組件</span><span class="sxs-lookup"><span data-stu-id="075f1-279">Rename namespaces and assemblies</span></span>](http://nuget.codeplex.com/workitem/274)
* [<span data-ttu-id="075f1-280">重新命名 NuPack 專案至 NuGet</span><span class="sxs-lookup"><span data-stu-id="075f1-280">Rename the NuPack Project to NuGet</span></span>](http://nuget.codeplex.com/workitem/282)
* [<span data-ttu-id="075f1-281">加入下列文字底下的相依性清單</span><span class="sxs-lookup"><span data-stu-id="075f1-281">Add the following text under the list of dependencies</span></span>](http://nuget.codeplex.com/workitem/288)
* [<span data-ttu-id="075f1-282">變更授權接受對話方塊中的授權接受文字</span><span class="sxs-lookup"><span data-stu-id="075f1-282">Change the license acceptance text in the License Acceptance Dialog</span></span>](http://nuget.codeplex.com/workitem/291)
* [<span data-ttu-id="075f1-283">變更在 授權接受對話方塊中的封裝清單上方的文字</span><span class="sxs-lookup"><span data-stu-id="075f1-283">Change the text in the License Acceptance Dialog above the list of packages</span></span>](http://nuget.codeplex.com/workitem/292)
* [<span data-ttu-id="075f1-284">OData 無法搭配 fwlink URL</span><span class="sxs-lookup"><span data-stu-id="075f1-284">OData doesn't work with an fwlink URL</span></span>](http://nuget.codeplex.com/workitem/304)
* [<span data-ttu-id="075f1-285">封裝管理員 UI： 透過主動快取封裝用於分頁的計數</span><span class="sxs-lookup"><span data-stu-id="075f1-285">Package Manager UI: Over aggressive caching of package count used for paging</span></span>](http://nuget.codeplex.com/workitem/317)
* [<span data-ttu-id="075f1-286">NuPack / NuGet-&gt; Package Manager Console 錯誤</span><span class="sxs-lookup"><span data-stu-id="075f1-286">NuPack / NuGet -&gt; Package Manager Console error</span></span>](http://nuget.codeplex.com/workitem/335)
* [<span data-ttu-id="075f1-287">新增套件 對話方塊會顯示授權接受的已安裝封裝</span><span class="sxs-lookup"><span data-stu-id="075f1-287">Add Package Dialog shows License Acceptance For Already Installed Packaged</span></span>](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a><span data-ttu-id="075f1-288">CTP 1</span><span class="sxs-lookup"><span data-stu-id="075f1-288">CTP 1</span></span>

<span data-ttu-id="075f1-289">以下是功能 NuGet CTP 1 已獲得修正的 bug 清單。</span><span class="sxs-lookup"><span data-stu-id="075f1-289">The following is a list of features and bugs that were fixed for NuGet CTP 1.</span></span>

* [<span data-ttu-id="075f1-290">組件延伸應該會重新命名為.nupack</span><span class="sxs-lookup"><span data-stu-id="075f1-290">Package extension should be renamed to .nupack</span></span>](http://nuget.codeplex.com/workitem/1)
* [<span data-ttu-id="075f1-291">將封裝檔案移到資料夾</span><span class="sxs-lookup"><span data-stu-id="075f1-291">Move package file into folder</span></span>](http://nuget.codeplex.com/workitem/2)
* [<span data-ttu-id="075f1-292">合併安裝&amp;新增 PS 命令</span><span class="sxs-lookup"><span data-stu-id="075f1-292">Merge install &amp; Add PS commands</span></span>](http://nuget.codeplex.com/workitem/3)
* [<span data-ttu-id="075f1-293">為動詞-名詞 」 cmdlet 建立別名</span><span class="sxs-lookup"><span data-stu-id="075f1-293">Create aliases for Verb-Noun cmdlets</span></span>](http://nuget.codeplex.com/workitem/4)
* [<span data-ttu-id="075f1-294">在 VS 中切換方案時，取得混淆 NuPack</span><span class="sxs-lookup"><span data-stu-id="075f1-294">NuPack gets confused when switching solution in VS</span></span>](http://nuget.codeplex.com/workitem/6)
* [<span data-ttu-id="075f1-295">依預設，我們應該隱藏 'packages' 方案資料夾</span><span class="sxs-lookup"><span data-stu-id="075f1-295">We should hide the 'packages' solution folder by default</span></span>](http://nuget.codeplex.com/workitem/11)
* [<span data-ttu-id="075f1-296">內容項目中新增語彙基元替換的支援。</span><span class="sxs-lookup"><span data-stu-id="075f1-296">Add support for token replacement in content items.</span></span>](http://nuget.codeplex.com/workitem/12)
* [<span data-ttu-id="075f1-297">NuPack.UI 應該使用 PackageSource API</span><span class="sxs-lookup"><span data-stu-id="075f1-297">NuPack.UI should use the PackageSource API</span></span>](http://nuget.codeplex.com/workitem/26)
* <span data-ttu-id="075f1-298">[[Nupack.Core]: PackageManager 將標示封裝為安裝它們之前，安裝](http://nuget.codeplex.com/workitem/27)</span><span class="sxs-lookup"><span data-stu-id="075f1-298">[[Nupack.Core]: PackageManager marks packages as installed prior to installing them](http://nuget.codeplex.com/workitem/27)</span></span>
* [<span data-ttu-id="075f1-299">刪除預設專案從方案仍會顯示已刪除的專案做為預設值</span><span class="sxs-lookup"><span data-stu-id="075f1-299">Deleting default project from solution still shows the deleted project as default</span></span>](http://nuget.codeplex.com/workitem/30)
* [<span data-ttu-id="075f1-300">新封裝會失敗，並 無法新增部分為指定的 URI 因為它已經在封裝中。</span><span class="sxs-lookup"><span data-stu-id="075f1-300">New-Package fails with "Cannot add part for the specified URI because it's already in the package."</span></span>](http://nuget.codeplex.com/workitem/32)
* [<span data-ttu-id="075f1-301">從 Visual Studio GUI 移除"NuPack 」 字串</span><span class="sxs-lookup"><span data-stu-id="075f1-301">Remove "NuPack" strings from Visual Studio GUI</span></span>](http://nuget.codeplex.com/workitem/35)
* [<span data-ttu-id="075f1-302">加入 COPYRIGHT.txt 至 Apache 標頭檔</span><span class="sxs-lookup"><span data-stu-id="075f1-302">Add Apache Header To a COPYRIGHT.txt file</span></span>](http://nuget.codeplex.com/workitem/36)
* [<span data-ttu-id="075f1-303">移除更新 PackageSource 命令</span><span class="sxs-lookup"><span data-stu-id="075f1-303">Remove Update-PackageSource Command</span></span>](http://nuget.codeplex.com/workitem/37)
* [<span data-ttu-id="075f1-304">封裝管理員無法使用載入設定檔時擲回例外狀況</span><span class="sxs-lookup"><span data-stu-id="075f1-304">Package Manager unusable when loading profile throws an exception</span></span>](http://nuget.codeplex.com/workitem/39)
* [<span data-ttu-id="075f1-305">init.ps1 install.ps1，uninstall.ps1 需要接收其他狀態</span><span class="sxs-lookup"><span data-stu-id="075f1-305">init.ps1, install.ps1 and uninstall.ps1 need to receive additional state</span></span>](http://nuget.codeplex.com/workitem/41)
* [<span data-ttu-id="075f1-306">將主控台和 GUI 封裝結合成單一套件</span><span class="sxs-lookup"><span data-stu-id="075f1-306">Combine Console and GUI Packages Into One Package</span></span>](http://nuget.codeplex.com/workitem/42)
* [<span data-ttu-id="075f1-307">如果套用至不在根目錄的 XML，Xml 轉換邏輯無法運作</span><span class="sxs-lookup"><span data-stu-id="075f1-307">Xml transform logic doesn't work if applied to XML that isn't at the root</span></span>](http://nuget.codeplex.com/workitem/43)
* [<span data-ttu-id="075f1-308">管理未更新 NuPack 主控台的封裝來源設定對話方塊</span><span class="sxs-lookup"><span data-stu-id="075f1-308">Manage package sources settings dialog not updating the NuPack console</span></span>](http://nuget.codeplex.com/workitem/44)
* [<span data-ttu-id="075f1-309">NuPack 主控台 UI： 重新命名 '封裝來源' 摘要的 「 封裝 」 下拉式清單</span><span class="sxs-lookup"><span data-stu-id="075f1-309">NuPack Console UI: Rename 'Package feed' drop-down list to 'Package source'</span></span>](http://nuget.codeplex.com/workitem/45)
* [<span data-ttu-id="075f1-310">NuPack 主控台選項： 重新命名 ' 儲存機制 UI' NuPack 主控台與一致</span><span class="sxs-lookup"><span data-stu-id="075f1-310">NuPack Console Options: Rename 'Repository UI' to be consistent with NuPack Console</span></span>](http://nuget.codeplex.com/workitem/46)
* [<span data-ttu-id="075f1-311">加入封裝失敗時針對開啟從 IIS 或 URL 的網站</span><span class="sxs-lookup"><span data-stu-id="075f1-311">Add-Package fails against a website that was opened from IIS or a URL</span></span>](http://nuget.codeplex.com/workitem/53)
* [<span data-ttu-id="075f1-312">封裝管理員的來源不能使用 FwLink</span><span class="sxs-lookup"><span data-stu-id="075f1-312">Package Manager Source Doesn't Work With FwLink</span></span>](http://nuget.codeplex.com/workitem/55)
* [<span data-ttu-id="075f1-313">設定預設的封裝來源</span><span class="sxs-lookup"><span data-stu-id="075f1-313">Set the default package source</span></span>](http://nuget.codeplex.com/workitem/59)
* [<span data-ttu-id="075f1-314">當加入封裝來源 選項，提供唯一的來源時，會假設它是預設值。</span><span class="sxs-lookup"><span data-stu-id="075f1-314">When adding package sources in option, when only one source is supplied, assume it's the default.</span></span>](http://nuget.codeplex.com/workitem/60)
* [<span data-ttu-id="075f1-315">對話方塊 UI 顯示假的 「 最新 」 封裝</span><span class="sxs-lookup"><span data-stu-id="075f1-315">The Dialog UI shows fake "recent" packages</span></span>](http://nuget.codeplex.com/workitem/62)
* <span data-ttu-id="075f1-316">[選項： 按一下 [取消] 5d; 並不會取消變更](http://nuget.codeplex.com/workitem/63)</span><span class="sxs-lookup"><span data-stu-id="075f1-316">[Options: Clicking cancel does not cancel changes](http://nuget.codeplex.com/workitem/63)</span></span>
* [<span data-ttu-id="075f1-317">新增套件參考對話方塊搜尋應該不區分大小寫</span><span class="sxs-lookup"><span data-stu-id="075f1-317">Add Package Reference Dialog Search should be case insensitive</span></span>](http://nuget.codeplex.com/workitem/65)
* [<span data-ttu-id="075f1-318">在 AssemblyInfo.cs 檔案中修正公司中繼資料</span><span class="sxs-lookup"><span data-stu-id="075f1-318">Fix company metadata in AssemblyInfo.cs files</span></span>](http://nuget.codeplex.com/workitem/67)
* [<span data-ttu-id="075f1-319">Vsix 的版本號碼</span><span class="sxs-lookup"><span data-stu-id="075f1-319">Version number for the VSIX</span></span>](http://nuget.codeplex.com/workitem/71)
* [<span data-ttu-id="075f1-320">移除封裝： 使用-？顯示說明兩次</span><span class="sxs-lookup"><span data-stu-id="075f1-320">Remove-Package: Using -? displays help twice</span></span>](http://nuget.codeplex.com/workitem/72)
* [<span data-ttu-id="075f1-321">執行安裝/解除安裝封裝的專案層級的封裝</span><span class="sxs-lookup"><span data-stu-id="075f1-321">Execute install/uninstall packages for project level packages</span></span>](http://nuget.codeplex.com/workitem/74)
* [<span data-ttu-id="075f1-322">伺服器無法建立一個 nupack 驗證失敗時的摘要</span><span class="sxs-lookup"><span data-stu-id="075f1-322">Server unable to create feed when one nupack fails validation</span></span>](http://nuget.codeplex.com/workitem/90)
* [<span data-ttu-id="075f1-323">需要取代 NuPack 圖示</span><span class="sxs-lookup"><span data-stu-id="075f1-323">Need to Replace NuPack Icons</span></span>](http://nuget.codeplex.com/workitem/94)
* [<span data-ttu-id="075f1-324">NTLM http proxy 不會驗證摘要的封裝。</span><span class="sxs-lookup"><span data-stu-id="075f1-324">NTLM http proxy does not authenticate to the package feed.</span></span>](http://nuget.codeplex.com/workitem/96)
* [<span data-ttu-id="075f1-325">對話方塊不一定置中與在視窗中啟動</span><span class="sxs-lookup"><span data-stu-id="075f1-325">The dialog doesn't always start centered in the VS window</span></span>](http://nuget.codeplex.com/workitem/100)
* [<span data-ttu-id="075f1-326">許多封裝詳細資料中的欄位未被填入對話方塊</span><span class="sxs-lookup"><span data-stu-id="075f1-326">Many of the fields in a packages details are not being populated in the dialog</span></span>](http://nuget.codeplex.com/workitem/102)
* [<span data-ttu-id="075f1-327">UI 對話方塊不會顯示作者姓名</span><span class="sxs-lookup"><span data-stu-id="075f1-327">Dialog UI doesn't show Authors' names</span></span>](http://nuget.codeplex.com/workitem/108)
* [<span data-ttu-id="075f1-328">為什麼-移除封裝版本</span><span class="sxs-lookup"><span data-stu-id="075f1-328">Why -Version for Remove-Package</span></span>](http://nuget.codeplex.com/workitem/113)
* <span data-ttu-id="075f1-329">[移除對話方塊 UI 上的 [最近] 索引標籤](http://nuget.codeplex.com/workitem/115)</span><span class="sxs-lookup"><span data-stu-id="075f1-329">[Remove the Recent tab on the Dialog UI](http://nuget.codeplex.com/workitem/115)</span></span>
* [<span data-ttu-id="075f1-330">VS 損毀時右邊按一下方案資料夾開啟對話方塊 UI 至少一個之後。</span><span class="sxs-lookup"><span data-stu-id="075f1-330">VS crash when right click on solution folder after opening Dialog UI at least one.</span></span>](http://nuget.codeplex.com/workitem/126)
* [<span data-ttu-id="075f1-331">變更清單封裝-本機參數-安裝</span><span class="sxs-lookup"><span data-stu-id="075f1-331">Change the -Local parameter of List-Package to -Installed</span></span>](http://nuget.codeplex.com/workitem/129)
* [<span data-ttu-id="075f1-332">重新命名 NuPack.config packages.xml</span><span class="sxs-lookup"><span data-stu-id="075f1-332">Rename packages.xml to NuPack.config</span></span>](http://nuget.codeplex.com/workitem/132)
* [<span data-ttu-id="075f1-333">主控台會在行尾中強制資料指標</span><span class="sxs-lookup"><span data-stu-id="075f1-333">Console forces cursor to the end of line</span></span>](http://nuget.codeplex.com/workitem/135)
* [<span data-ttu-id="075f1-334">移除封裝 intellisense 已中斷</span><span class="sxs-lookup"><span data-stu-id="075f1-334">Remove-Package intellisense is broken</span></span>](http://nuget.codeplex.com/workitem/136)
* [<span data-ttu-id="075f1-335">將 RequireLicenseAcceptance 旗標加入.nuspec 和摘要</span><span class="sxs-lookup"><span data-stu-id="075f1-335">Add RequireLicenseAcceptance Flag to .nuspec and Feed</span></span>](http://nuget.codeplex.com/workitem/137)
* [<span data-ttu-id="075f1-336">新增.nuspec 格式和套件的 LicenseUrl 摘要</span><span class="sxs-lookup"><span data-stu-id="075f1-336">Add LicenseUrl to .nuspec Format and Package Feed</span></span>](http://nuget.codeplex.com/workitem/138)
* [<span data-ttu-id="075f1-337">按一下 安裝套件需要接受，應該會顯示接受對話方塊</span><span class="sxs-lookup"><span data-stu-id="075f1-337">Clicking Install For Package That Requires Acceptance Should Show Acceptance Dialog</span></span>](http://nuget.codeplex.com/workitem/139)
* <span data-ttu-id="075f1-338">[免責聲明文字加入 [新增套件] 對話方塊](http://nuget.codeplex.com/workitem/140)</span><span class="sxs-lookup"><span data-stu-id="075f1-338">[Add Disclaimer Text to the Add Package Dialog](http://nuget.codeplex.com/workitem/140)</span></span>
* [<span data-ttu-id="075f1-339">新增免責聲明當封裝執行主控台的第一次</span><span class="sxs-lookup"><span data-stu-id="075f1-339">Add Disclaimer When the Package Console is run the first time</span></span>](http://nuget.codeplex.com/workitem/143)
* [<span data-ttu-id="075f1-340">在主控台安裝封裝之後顯示免責聲明</span><span class="sxs-lookup"><span data-stu-id="075f1-340">Display Disclaimer After Installing Package In The Console</span></span>](http://nuget.codeplex.com/workitem/144)
* [<span data-ttu-id="075f1-341">重新命名.nupkg.nupack 延伸模組</span><span class="sxs-lookup"><span data-stu-id="075f1-341">Rename the .nupack extension to .nupkg</span></span>](http://nuget.codeplex.com/workitem/146)