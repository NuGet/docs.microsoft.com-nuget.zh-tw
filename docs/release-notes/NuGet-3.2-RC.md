---
title: NuGet 3.2 RC 版本資訊
description: 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 3.2 RC 版本資訊。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0310bac6fdb3ef92176f9224ace1620a230664af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822041"
---
# <a name="nuget-32-rc-release-notes"></a><span data-ttu-id="2feb7-103">NuGet 3.2 RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="2feb7-103">NuGet 3.2 RC Release Notes</span></span>

<span data-ttu-id="2feb7-104">[NuGet 3.1.1 版本資訊](../release-notes/nuget-3.1.1.md) | [NuGet 3.2 版本資訊](../release-notes/nuget-3.2.md)</span><span class="sxs-lookup"><span data-stu-id="2feb7-104">[NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md) | [NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md)</span></span>

<span data-ttu-id="2feb7-105">發行 NuGet 3.2 發行候選版本 2015 年 9 月 2 日的改良功能和修正程式 3.1.1 集合。</span><span class="sxs-lookup"><span data-stu-id="2feb7-105">NuGet 3.2 release candidate was released September 2, 2015 as a collection of improvements and fixes for the 3.1.1 release.</span></span>  <span data-ttu-id="2feb7-106">此外，這些是第一次發行至新的 dist.nuget.org 儲存機制的第一個發行版本。</span><span class="sxs-lookup"><span data-stu-id="2feb7-106">Also, these are the first releases that are published first to the new dist.nuget.org repository.</span></span>

## <a name="new-features"></a><span data-ttu-id="2feb7-107">新功能</span><span class="sxs-lookup"><span data-stu-id="2feb7-107">New Features</span></span>

* <span data-ttu-id="2feb7-108">在相同的資料夾中的專案現在可以有不同`project.json`特有的每個專案的資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="2feb7-108">Projects that live in the same folder can now have different `project.json` files in that folder specific to each project.</span></span>  <span data-ttu-id="2feb7-109">針對每個專案，名稱`project.json`檔案`{ProjectName}.project.json`NuGet 會正確參考，並且針對每個專案可以適當地利用該內容。</span><span class="sxs-lookup"><span data-stu-id="2feb7-109">For each project, name the `project.json` file `{ProjectName}.project.json` and NuGet will properly reference and use that content for each project appropriately.</span></span>  <span data-ttu-id="2feb7-110">這種情況支援新功能[1102年](https://github.com/NuGet/Home/issues/1102)</span><span class="sxs-lookup"><span data-stu-id="2feb7-110">This supports a new feature  [1102](https://github.com/NuGet/Home/issues/1102)</span></span>
* <span data-ttu-id="2feb7-111">`NuGet.Config` 現在支援為相對路徑-globalPackagesFolder [1062年](https://github.com/NuGet/Home/issues/1062)</span><span class="sxs-lookup"><span data-stu-id="2feb7-111">`NuGet.Config` now supports a globalPackagesFolder as a relative path - [1062](https://github.com/NuGet/Home/issues/1062)</span></span>

## <a name="command-line-updates"></a><span data-ttu-id="2feb7-112">命令列的更新</span><span class="sxs-lookup"><span data-stu-id="2feb7-112">Command-line updates</span></span>

<span data-ttu-id="2feb7-113">這是支援 NuGet v3 伺服器 nuget.exe 用戶端的第一個版本，而且還原專案封裝管理與`project.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="2feb7-113">This is the first version of the nuget.exe client that supports the NuGet v3 servers and restoring packages for projects managed with a `project.json` file.</span></span>

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a><span data-ttu-id="2feb7-114">沒有已驗證摘要的問題已解決在此版本中以改善用戶端之間的互動數目。</span><span class="sxs-lookup"><span data-stu-id="2feb7-114">There were a number of authenticated feed issues that were addressed in this release to improve interactions with the client.</span></span>

* <span data-ttu-id="2feb7-115">安裝 / 還原互動只能提交認證已驗證的摘要-初始要求[1300年](https://github.com/NuGet/Home/issues/1300)， [456](https://github.com/NuGet/Home/issues/456)</span><span class="sxs-lookup"><span data-stu-id="2feb7-115">Install / restore interactions only submit credentials for the initial request to the authenticated feed - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)</span></span>
* <span data-ttu-id="2feb7-116">推播命令無法解決從設定-認證[1248年](https://github.com/NuGet/Home/issues/1248)</span><span class="sxs-lookup"><span data-stu-id="2feb7-116">Push command does not resolve credentials from configuration - [1248](https://github.com/NuGet/Home/issues/1248)</span></span>
* <span data-ttu-id="2feb7-117">使用者代理程式和標頭會立即提交到 NuGet 儲存機制，以協助統計資料追蹤- [929](https://github.com/NuGet/Home/issues/929)</span><span class="sxs-lookup"><span data-stu-id="2feb7-117">User agent and headers are now submitted to NuGet repositories to help with statistics tracking - [929](https://github.com/NuGet/Home/issues/929)</span></span>

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a><span data-ttu-id="2feb7-118">我們進行改善可更妥善處理網路失敗嘗試與遠端的 NuGet 儲存機制搭配時數：</span><span class="sxs-lookup"><span data-stu-id="2feb7-118">We made a number of improvements to better handle network failures while attempting to work with a remote NuGet repository:</span></span>

* <span data-ttu-id="2feb7-119">改善錯誤訊息時無法連線到遠端摘要- [1238年](https://github.com/NuGet/Home/issues/1238)</span><span class="sxs-lookup"><span data-stu-id="2feb7-119">Improved error messages when unable to connect to remote feeds - [1238](https://github.com/NuGet/Home/issues/1238)</span></span>
* <span data-ttu-id="2feb7-120">已更正 NuGet 還原命令時，會發生錯誤狀況的正確傳回 1 [1186年](https://github.com/NuGet/Home/issues/1186)</span><span class="sxs-lookup"><span data-stu-id="2feb7-120">Corrected NuGet restore command to properly return a 1 when an error condition occurs - [1186](https://github.com/NuGet/Home/issues/1186)</span></span>
* <span data-ttu-id="2feb7-121">現在網路連線重試一次最多 5 次故障 HTTP 5xx-每個 200 毫秒[1120年](https://github.com/NuGet/Home/issues/1120)</span><span class="sxs-lookup"><span data-stu-id="2feb7-121">Now retrying network connections every 200ms for a maximum of 5 attempts in the case of HTTP 5xx failures - [1120](https://github.com/NuGet/Home/issues/1120)</span></span>
* <span data-ttu-id="2feb7-122">改善伺服器重新導向回應的處理期間的推播命令- [1051年](https://github.com/NuGet/Home/issues/1051)</span><span class="sxs-lookup"><span data-stu-id="2feb7-122">Improved handling of server redirect responses during a push command - [1051](https://github.com/NuGet/Home/issues/1051)</span></span>
* <span data-ttu-id="2feb7-123">`nuget install -source` 現在支援 URL 或儲存機制名稱做為引數-Nuget.Config [1046年](https://github.com/NuGet/Home/issues/1046)</span><span class="sxs-lookup"><span data-stu-id="2feb7-123">`nuget install -source` now supports either URL or repository name from Nuget.Config as an argument - [1046](https://github.com/NuGet/Home/issues/1046)</span></span>
* <span data-ttu-id="2feb7-124">遺漏已在還原期間不位於儲存機制的套件現在會報告為錯誤，而非警告[1038年](https://github.com/NuGet/Home/issues/1038)</span><span class="sxs-lookup"><span data-stu-id="2feb7-124">Missing packages that were not located on a repository during a restore are now reported as errors instead of warnings [1038](https://github.com/NuGet/Home/issues/1038)</span></span>
* <span data-ttu-id="2feb7-125">已更正的 Unix/Linux 案例-\r\n multipartwebrequest 處理[776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="2feb7-125">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a><span data-ttu-id="2feb7-126">有許多使用各種命令的問題的修正：</span><span class="sxs-lookup"><span data-stu-id="2feb7-126">There are a number of fixes to issues with various commands:</span></span>

* <span data-ttu-id="2feb7-127">推播命令不會再對套件來源-PUT 之前 GET [1237年](https://github.com/NuGet/Home/issues/1237)</span><span class="sxs-lookup"><span data-stu-id="2feb7-127">Push command no longer does a GET before a PUT against a package source - [1237](https://github.com/NuGet/Home/issues/1237)</span></span>
* <span data-ttu-id="2feb7-128">List 命令不會再重複一次的版本號碼為[1185年](https://github.com/NuGet/Home/issues/1185)</span><span class="sxs-lookup"><span data-stu-id="2feb7-128">List command no longer repeats version numbers - [1185](https://github.com/NuGet/Home/issues/1185)</span></span>
* <span data-ttu-id="2feb7-129">組件使用-建置引數現在正確支援 C# 6.0- [1107年](https://github.com/NuGet/Home/issues/1107)</span><span class="sxs-lookup"><span data-stu-id="2feb7-129">Pack with the -build argument now properly supports C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)</span></span>
* <span data-ttu-id="2feb7-130">已修正的問題嘗試將組件 F # 專案建置 Visual Studio 2015- [1048年](https://github.com/NuGet/Home/issues/1048)</span><span class="sxs-lookup"><span data-stu-id="2feb7-130">Corrected issues attempting to pack an F# project built with Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)</span></span>
* <span data-ttu-id="2feb7-131">封裝已存在時，還原現在沒有 ops [1040年](https://github.com/NuGet/Home/issues/1040)</span><span class="sxs-lookup"><span data-stu-id="2feb7-131">Restore now no-ops when packages already exist - [1040](https://github.com/NuGet/Home/issues/1040)</span></span>
* <span data-ttu-id="2feb7-132">改良的錯誤訊息`packages.config`檔案格式不正確- [1034年](https://github.com/NuGet/Home/issues/1034)</span><span class="sxs-lookup"><span data-stu-id="2feb7-132">Improved error messages when `packages.config` file is malformed - [1034](https://github.com/NuGet/Home/issues/1034)</span></span>
* <span data-ttu-id="2feb7-133">修正與 restore 命令`-SolutionDirectory`切換到使用相對路徑- [992](https://github.com/NuGet/Home/issues/992)</span><span class="sxs-lookup"><span data-stu-id="2feb7-133">Corrected restore command with `-SolutionDirectory` switch to work with relative paths - [992](https://github.com/NuGet/Home/issues/992)</span></span>
* <span data-ttu-id="2feb7-134">改善更新命令，以支援整個方案的更新- [924](https://github.com/NuGet/Home/issues/924)</span><span class="sxs-lookup"><span data-stu-id="2feb7-134">Improved Updated command to support solution-wide update - [924](https://github.com/NuGet/Home/issues/924)</span></span>

<span data-ttu-id="2feb7-135">在此版本中解決問題的完整清單位於 NuGet GitHub[命令列里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)。</span><span class="sxs-lookup"><span data-stu-id="2feb7-135">A complete list of issues addressed in this release can be found in the NuGet GitHub [Command-Line milestone](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).</span></span>

## <a name="visual-studio-extension-updates"></a><span data-ttu-id="2feb7-136">Visual Studio 擴充功能更新</span><span class="sxs-lookup"><span data-stu-id="2feb7-136">Visual Studio extension updates</span></span>

### <a name="new-features-in-visual-studio"></a><span data-ttu-id="2feb7-137">Visual Studio 中的新功能</span><span class="sxs-lookup"><span data-stu-id="2feb7-137">New Features in Visual Studio</span></span>

* <span data-ttu-id="2feb7-138">新的操作功能表項目已加入可讓封裝以建置方案，才能還原 [解決方案] 節點上的 [方案總管] ([1274年](https://github.com/NuGet/Home/issues/1274))。</span><span class="sxs-lookup"><span data-stu-id="2feb7-138">A new context menu item was added to the Solution Explorer on the solution node that allows packages to be restored without building the solution ([1274](https://github.com/NuGet/Home/issues/1274)).</span></span>

![新 '還原封裝' 操作功能表項目](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a><span data-ttu-id="2feb7-140">更新和修正程式，Visual Studio 中</span><span class="sxs-lookup"><span data-stu-id="2feb7-140">Updates and Fixes in Visual Studio</span></span>

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a><span data-ttu-id="2feb7-141">修正已驗證的摘要已彙總，並且處理中的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="2feb7-141">The fixes for authenticated feeds were rolled up and addressed in the extension as well.</span></span>  <span data-ttu-id="2feb7-142">下列的驗證項目也是延伸模組中定址：</span><span class="sxs-lookup"><span data-stu-id="2feb7-142">The following authentication items were also addressed in the extension:</span></span>

* <span data-ttu-id="2feb7-143">現在正確視為 NuGet v3 驗證摘要正常運作，而不是 v2 通過驗證後摘要- [1216年](https://github.com/NuGet/Home/issues/1216)</span><span class="sxs-lookup"><span data-stu-id="2feb7-143">Now correctly treating NuGet v3 authenticated feeds properly, instead of as v2 authenticated feeds - [1216](https://github.com/NuGet/Home/issues/1216)</span></span>
* <span data-ttu-id="2feb7-144">修正過的要求，在專案中使用的驗證認證`project.json`和溝通 v2 摘要- [1082年](https://github.com/NuGet/Home/issues/1082)</span><span class="sxs-lookup"><span data-stu-id="2feb7-144">Corrected request for authentication credentials in projects using `project.json` and communicating with v2 feeds - [1082](https://github.com/NuGet/Home/issues/1082)</span></span>

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a><span data-ttu-id="2feb7-145">網路連線有影響的使用者介面，在 Visual Studio 中，我們解決這有下列的修正程式：</span><span class="sxs-lookup"><span data-stu-id="2feb7-145">Network connectivity had affected the user interface in Visual Studio, and we addressed this with the following fixes:</span></span>

* <span data-ttu-id="2feb7-146">改善的封裝版本的本機快取維護[1096年](https://github.com/NuGet/Home/issues/1096)</span><span class="sxs-lookup"><span data-stu-id="2feb7-146">Improved the maintenance of the local cache of package versions - [1096](https://github.com/NuGet/Home/issues/1096)</span></span>
* <span data-ttu-id="2feb7-147">當連接至 v3，摘要不會再將它視為 v2 摘要-嘗試變更失敗行為[1253年](https://github.com/NuGet/Home/issues/1253)</span><span class="sxs-lookup"><span data-stu-id="2feb7-147">Changed the failure behavior when connecting to a v3 feed to no longer attempt to treat it as a v2 feed - [1253](https://github.com/NuGet/Home/issues/1253)</span></span>
* <span data-ttu-id="2feb7-148">使用多個封裝來源的安裝封裝時，現在防止安裝失敗[1183年](https://github.com/NuGet/Home/issues/1183)</span><span class="sxs-lookup"><span data-stu-id="2feb7-148">Now preventing install failures when installing a package with multiple package sources - [1183](https://github.com/NuGet/Home/issues/1183)</span></span>

<span data-ttu-id="2feb7-149">我們改進處理的建置作業之間的互動：</span><span class="sxs-lookup"><span data-stu-id="2feb7-149">We improved handling of interactions with build operations:</span></span>

* <span data-ttu-id="2feb7-150">現在繼續建立專案，如果還原封裝的單一專案失敗- [1169年](https://github.com/NuGet/Home/issues/1169)</span><span class="sxs-lookup"><span data-stu-id="2feb7-150">Now continuing to build projects if restoring packages for a single project fails - [1169](https://github.com/NuGet/Home/issues/1169)</span></span>
* <span data-ttu-id="2feb7-151">安裝到方案中的另一個專案相依於專案的封裝會強制方案重建- [981](https://github.com/NuGet/Home/issues/981)</span><span class="sxs-lookup"><span data-stu-id="2feb7-151">Installing a package into a project that is depended on by another project in the solution forces a solution rebuild - [981](https://github.com/NuGet/Home/issues/981)</span></span>
* <span data-ttu-id="2feb7-152">修正失敗的封裝會安裝至專案的正確復原變更[1265年](https://github.com/NuGet/Home/issues/1265)</span><span class="sxs-lookup"><span data-stu-id="2feb7-152">Corrected failed package installs to properly rollback changes to a project - [1265](https://github.com/NuGet/Home/issues/1265)</span></span>
* <span data-ttu-id="2feb7-153">已更正不小心移除`developmentDependency`屬性中的封裝`packages.config`  -  [1263年](https://github.com/NuGet/Home/issues/1263)</span><span class="sxs-lookup"><span data-stu-id="2feb7-153">Corrected inadvertent removal of the `developmentDependency` attribute on a package in `packages.config` - [1263](https://github.com/NuGet/Home/issues/1263)</span></span>
* <span data-ttu-id="2feb7-154">呼叫`install.ps1`現在有適當的`$package.AssemblyReferences`物件傳遞為[1245年](https://github.com/NuGet/Home/issues/1245)</span><span class="sxs-lookup"><span data-stu-id="2feb7-154">Calls to `install.ps1` now have a proper `$package.AssemblyReferences` object passed - [1245](https://github.com/NuGet/Home/issues/1245)</span></span>
* <span data-ttu-id="2feb7-155">不會再妨礙解除安裝 UWP 專案中的封裝專案處於不正常的狀態時[1128年](https://github.com/NuGet/Home/issues/1128)</span><span class="sxs-lookup"><span data-stu-id="2feb7-155">No longer preventing uninstalls of packages in UWP projects while the project is in a bad state - [1128](https://github.com/NuGet/Home/issues/1128)</span></span>
* <span data-ttu-id="2feb7-156">包含混合方案`packages.config`和`project.json`專案現在正確建置而不需要第二個建置作業- [1122年](https://github.com/NuGet/Home/issues/1122)</span><span class="sxs-lookup"><span data-stu-id="2feb7-156">Solutions containing a mix of `packages.config` and `project.json` projects are now properly built without requiring a second build operation - [1122](https://github.com/NuGet/Home/issues/1122)</span></span>
* <span data-ttu-id="2feb7-157">適當地尋找 app.config 檔案，如果連結或位於不同的資料夾- [1111年](https://github.com/NuGet/Home/issues/1111)， [894](https://github.com/NuGet/Home/issues/894)</span><span class="sxs-lookup"><span data-stu-id="2feb7-157">Properly locating app.config files if they are linked or located in a different folder - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)</span></span>
* <span data-ttu-id="2feb7-158">UWP 專案現在可以安裝未列出的套件- [1109年](https://github.com/NuGet/Home/issues/1109)</span><span class="sxs-lookup"><span data-stu-id="2feb7-158">UWP projects can now install unlisted packages - [1109](https://github.com/NuGet/Home/issues/1109)</span></span>
* <span data-ttu-id="2feb7-159">封裝還原現在允許時方案不是處於已儲存的狀態- [1081年](https://github.com/NuGet/Home/issues/1081)</span><span class="sxs-lookup"><span data-stu-id="2feb7-159">Package restore is now allowed while a solution is not in a saved state - [1081](https://github.com/NuGet/Home/issues/1081)</span></span>


<span data-ttu-id="2feb7-160">處理的組態檔已更正的更新：</span><span class="sxs-lookup"><span data-stu-id="2feb7-160">Handling updates to configuration files were corrected:</span></span>

* <span data-ttu-id="2feb7-161">從封裝的後續組建不會再移除目標檔案傳遞`project.json`受管理的專案- [1288年](https://github.com/NuGet/Home/issues/1288)</span><span class="sxs-lookup"><span data-stu-id="2feb7-161">No longer removing a targets file delivered from a package on subsequent builds of a `project.json` managed project - [1288](https://github.com/NuGet/Home/issues/1288)</span></span>
* <span data-ttu-id="2feb7-162">無法再修改 Nuget.Config 檔案在 ASP.NET 5 方案建置- [1201年](https://github.com/NuGet/Home/issues/1201)</span><span class="sxs-lookup"><span data-stu-id="2feb7-162">No longer modifying Nuget.Config files during ASP.NET 5 solution build - [1201](https://github.com/NuGet/Home/issues/1201)</span></span>
* <span data-ttu-id="2feb7-163">不會再變更期間套件更新為允許版本條件約束[1130年](https://github.com/NuGet/Home/issues/1130)</span><span class="sxs-lookup"><span data-stu-id="2feb7-163">No longer changing allowed versions constraint during package update - [1130](https://github.com/NuGet/Home/issues/1130)</span></span>
* <span data-ttu-id="2feb7-164">鎖定檔案現在保持鎖定期間組建- [1127年](https://github.com/NuGet/Home/issues/1127)</span><span class="sxs-lookup"><span data-stu-id="2feb7-164">Lock files now remain locked during build - [1127](https://github.com/NuGet/Home/issues/1127)</span></span>
* <span data-ttu-id="2feb7-165">現在修改`packages.config`和不重寫期間更新- [585](https://github.com/NuGet/Home/issues/585)</span><span class="sxs-lookup"><span data-stu-id="2feb7-165">Now modifying `packages.config` and not rewriting it during updates - [585](https://github.com/NuGet/Home/issues/585)</span></span>


<span data-ttu-id="2feb7-166">已改進 TFS 原始檔控制的互動：</span><span class="sxs-lookup"><span data-stu-id="2feb7-166">Interactions with TFS source control are improved:</span></span>

* <span data-ttu-id="2feb7-167">不會再失敗的封裝繫結至 TFS 的安裝[1164年](https://github.com/NuGet/Home/issues/1164)， [980](https://github.com/NuGet/Home/issues/980)</span><span class="sxs-lookup"><span data-stu-id="2feb7-167">No longer failing installs for packages that are bound to TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)</span></span>
* <span data-ttu-id="2feb7-168">修正過的 NuGet 使用者介面，讓 TFS 2013 整合- [1071年](https://github.com/NuGet/Home/issues/1071)</span><span class="sxs-lookup"><span data-stu-id="2feb7-168">Corrected NuGet user interface to allow TFS 2013 integration - [1071](https://github.com/NuGet/Home/issues/1071)</span></span>
* <span data-ttu-id="2feb7-169">已更正封裝還原正確來自封裝資料夾的參考[1004年](https://github.com/NuGet/Home/issues/1004)</span><span class="sxs-lookup"><span data-stu-id="2feb7-169">Corrected references to packages restored to properly come from a packages folder - [1004](https://github.com/NuGet/Home/issues/1004)</span></span>

<span data-ttu-id="2feb7-170">最後，我們也有所改善，這些項目：</span><span class="sxs-lookup"><span data-stu-id="2feb7-170">Finally, we also improved these items:</span></span>

* <span data-ttu-id="2feb7-171">針對記錄檔訊息的詳細等級縮小`project.json`managed 專案的[1163年](https://github.com/NuGet/Home/issues/1163)</span><span class="sxs-lookup"><span data-stu-id="2feb7-171">Verbosity of log messages reduced for `project.json` managed projects - [1163](https://github.com/NuGet/Home/issues/1163)</span></span>
* <span data-ttu-id="2feb7-172">現在正確安裝的封裝版本使用者介面中顯示為[1061年](https://github.com/NuGet/Home/issues/1061)</span><span class="sxs-lookup"><span data-stu-id="2feb7-172">Now properly displaying the installed version of a package in the user interface - [1061](https://github.com/NuGet/Home/issues/1061)</span></span>


<span data-ttu-id="2feb7-173">Visual Studio 擴充功能可以找到 NuGet GitHub 中解決問題的完整清單[3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span><span class="sxs-lookup"><span data-stu-id="2feb7-173">A complete list of issues addressed for the Visual Studio extension can be found in the NuGet GitHub [3.2 milestone](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span></span>

## <a name="known-issues"></a><span data-ttu-id="2feb7-174">已知問題</span><span class="sxs-lookup"><span data-stu-id="2feb7-174">Known Issues</span></span>

<span data-ttu-id="2feb7-175">我們將繼續在我們的 GitHub 問題清單，可以在找到追蹤問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="2feb7-175">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>