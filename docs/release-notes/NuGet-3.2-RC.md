---
title: NuGet 3.2 RC 版本資訊
description: NuGet 3.2 RC 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8132affb8273604ae79d4e1f85e6072d8eaf5ad6
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780285"
---
# <a name="nuget-32-rc-release-notes"></a><span data-ttu-id="04a1b-103">NuGet 3.2 RC 版本資訊</span><span class="sxs-lookup"><span data-stu-id="04a1b-103">NuGet 3.2 RC Release Notes</span></span>

<span data-ttu-id="04a1b-104">[NuGet 3.1.1 版本](../release-notes/nuget-3.1.1.md)  |  資訊[NuGet 3.2 版本](../release-notes/nuget-3.2.md)資訊</span><span class="sxs-lookup"><span data-stu-id="04a1b-104">[NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md) | [NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md)</span></span>

<span data-ttu-id="04a1b-105">NuGet 3.2 候選版已于2015年9月2日發行，作為3.1.1 版本的增強功能和修正程式的集合。</span><span class="sxs-lookup"><span data-stu-id="04a1b-105">NuGet 3.2 release candidate was released September 2, 2015 as a collection of improvements and fixes for the 3.1.1 release.</span></span>  <span data-ttu-id="04a1b-106">此外，這些是先發行至新 dist.nuget.org 存放庫的第一個版本。</span><span class="sxs-lookup"><span data-stu-id="04a1b-106">Also, these are the first releases that are published first to the new dist.nuget.org repository.</span></span>

## <a name="new-features"></a><span data-ttu-id="04a1b-107">新功能</span><span class="sxs-lookup"><span data-stu-id="04a1b-107">New Features</span></span>

* <span data-ttu-id="04a1b-108">存在於相同資料夾中的專案現在可以 `project.json` 在每個專案特有的該資料夾中有不同的檔案。</span><span class="sxs-lookup"><span data-stu-id="04a1b-108">Projects that live in the same folder can now have different `project.json` files in that folder specific to each project.</span></span>  <span data-ttu-id="04a1b-109">針對每個專案，為檔案命名， `project.json` `{ProjectName}.project.json` 且 NuGet 會適當地參考並針對每個專案使用該內容。</span><span class="sxs-lookup"><span data-stu-id="04a1b-109">For each project, name the `project.json` file `{ProjectName}.project.json` and NuGet will properly reference and use that content for each project appropriately.</span></span>  <span data-ttu-id="04a1b-110">這支援新功能  [1102](https://github.com/NuGet/Home/issues/1102)</span><span class="sxs-lookup"><span data-stu-id="04a1b-110">This supports a new feature  [1102](https://github.com/NuGet/Home/issues/1102)</span></span>
* <span data-ttu-id="04a1b-111">`NuGet.Config` 現在支援 globalPackagesFolder 作為相對路徑- [1062](https://github.com/NuGet/Home/issues/1062)</span><span class="sxs-lookup"><span data-stu-id="04a1b-111">`NuGet.Config` now supports a globalPackagesFolder as a relative path - [1062](https://github.com/NuGet/Home/issues/1062)</span></span>

## <a name="command-line-updates"></a><span data-ttu-id="04a1b-112">命令列更新</span><span class="sxs-lookup"><span data-stu-id="04a1b-112">Command-line updates</span></span>

<span data-ttu-id="04a1b-113">這是第一個支援 NuGet v3 伺服器的 nuget.exe 用戶端版本，以及針對以檔案管理的專案還原套件的第一版 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="04a1b-113">This is the first version of the nuget.exe client that supports the NuGet v3 servers and restoring packages for projects managed with a `project.json` file.</span></span>

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a><span data-ttu-id="04a1b-114">此版本中已解決一些已驗證的摘要問題，以改善與用戶端的互動。</span><span class="sxs-lookup"><span data-stu-id="04a1b-114">There were a number of authenticated feed issues that were addressed in this release to improve interactions with the client.</span></span>

* <span data-ttu-id="04a1b-115">安裝/還原互動只會將初始要求的認證提交給已驗證的摘要- [1300](https://github.com/NuGet/Home/issues/1300)、 [456](https://github.com/NuGet/Home/issues/456)</span><span class="sxs-lookup"><span data-stu-id="04a1b-115">Install / restore interactions only submit credentials for the initial request to the authenticated feed - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)</span></span>
* <span data-ttu-id="04a1b-116">Push 命令無法解析來自設定的認證- [1248](https://github.com/NuGet/Home/issues/1248)</span><span class="sxs-lookup"><span data-stu-id="04a1b-116">Push command does not resolve credentials from configuration - [1248](https://github.com/NuGet/Home/issues/1248)</span></span>
* <span data-ttu-id="04a1b-117">使用者代理程式和標頭現在已提交至 NuGet 存放庫，以協助進行統計資料追蹤- [929](https://github.com/NuGet/Home/issues/929)</span><span class="sxs-lookup"><span data-stu-id="04a1b-117">User agent and headers are now submitted to NuGet repositories to help with statistics tracking - [929](https://github.com/NuGet/Home/issues/929)</span></span>

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a><span data-ttu-id="04a1b-118">我們進行了一些改善，以在嘗試使用遠端 NuGet 存放庫時更妥善處理網路失敗：</span><span class="sxs-lookup"><span data-stu-id="04a1b-118">We made a number of improvements to better handle network failures while attempting to work with a remote NuGet repository:</span></span>

* <span data-ttu-id="04a1b-119">改進無法連接到遠端摘要時的錯誤訊息- [1238](https://github.com/NuGet/Home/issues/1238)</span><span class="sxs-lookup"><span data-stu-id="04a1b-119">Improved error messages when unable to connect to remote feeds - [1238](https://github.com/NuGet/Home/issues/1238)</span></span>
* <span data-ttu-id="04a1b-120">修正了 NuGet 還原命令，以在發生錯誤狀況時正確傳回 1- [1186](https://github.com/NuGet/Home/issues/1186)</span><span class="sxs-lookup"><span data-stu-id="04a1b-120">Corrected NuGet restore command to properly return a 1 when an error condition occurs - [1186](https://github.com/NuGet/Home/issues/1186)</span></span>
* <span data-ttu-id="04a1b-121">現在，在 HTTP 5xx [1120](https://github.com/NuGet/Home/issues/1120)失敗的情況下，每個200毫秒重試網路連接最多5次</span><span class="sxs-lookup"><span data-stu-id="04a1b-121">Now retrying network connections every 200ms for a maximum of 5 attempts in the case of HTTP 5xx failures - [1120](https://github.com/NuGet/Home/issues/1120)</span></span>
* <span data-ttu-id="04a1b-122">改進在推送命令期間處理伺服器重新導向回應的功能- [1051](https://github.com/NuGet/Home/issues/1051)</span><span class="sxs-lookup"><span data-stu-id="04a1b-122">Improved handling of server redirect responses during a push command - [1051](https://github.com/NuGet/Home/issues/1051)</span></span>
* <span data-ttu-id="04a1b-123">`nuget install -source` 現在支援 Nuget.Config 的 URL 或存放庫名稱做為引數- [1046](https://github.com/NuGet/Home/issues/1046)</span><span class="sxs-lookup"><span data-stu-id="04a1b-123">`nuget install -source` now supports either URL or repository name from Nuget.Config as an argument - [1046](https://github.com/NuGet/Home/issues/1046)</span></span>
* <span data-ttu-id="04a1b-124">在還原期間缺少存放庫的套件，現在會回報為錯誤，而不是警告 [1038](https://github.com/NuGet/Home/issues/1038)</span><span class="sxs-lookup"><span data-stu-id="04a1b-124">Missing packages that were not located on a repository during a restore are now reported as errors instead of warnings [1038](https://github.com/NuGet/Home/issues/1038)</span></span>
* <span data-ttu-id="04a1b-125">修正了 \r\n for Unix/Linux 案例的 multipartwebrequest 處理- [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="04a1b-125">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a><span data-ttu-id="04a1b-126">各種命令的問題有一些修正：</span><span class="sxs-lookup"><span data-stu-id="04a1b-126">There are a number of fixes to issues with various commands:</span></span>

* <span data-ttu-id="04a1b-127">推播命令不再針對套件來源進行 PUT 之前的 GET- [1237](https://github.com/NuGet/Home/issues/1237)</span><span class="sxs-lookup"><span data-stu-id="04a1b-127">Push command no longer does a GET before a PUT against a package source - [1237](https://github.com/NuGet/Home/issues/1237)</span></span>
* <span data-ttu-id="04a1b-128">List 命令不再重複版本號碼- [1185](https://github.com/NuGet/Home/issues/1185)</span><span class="sxs-lookup"><span data-stu-id="04a1b-128">List command no longer repeats version numbers - [1185](https://github.com/NuGet/Home/issues/1185)</span></span>
* <span data-ttu-id="04a1b-129">具有-build 引數的套件現已正確支援 c # 6.0- [1107](https://github.com/NuGet/Home/issues/1107)</span><span class="sxs-lookup"><span data-stu-id="04a1b-129">Pack with the -build argument now properly supports C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)</span></span>
* <span data-ttu-id="04a1b-130">修正了嘗試封裝以 Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048)所建立的 F # 專案時所發生的問題</span><span class="sxs-lookup"><span data-stu-id="04a1b-130">Corrected issues attempting to pack an F# project built with Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)</span></span>
* <span data-ttu-id="04a1b-131">當套件已存在時立即還原- [1040](https://github.com/NuGet/Home/issues/1040)</span><span class="sxs-lookup"><span data-stu-id="04a1b-131">Restore now no-ops when packages already exist - [1040](https://github.com/NuGet/Home/issues/1040)</span></span>
* <span data-ttu-id="04a1b-132">改進檔案 `packages.config` 格式不正確的錯誤訊息 [-1034](https://github.com/NuGet/Home/issues/1034)</span><span class="sxs-lookup"><span data-stu-id="04a1b-132">Improved error messages when `packages.config` file is malformed - [1034](https://github.com/NuGet/Home/issues/1034)</span></span>
* <span data-ttu-id="04a1b-133">使用參數更正了 restore 命令 `-SolutionDirectory` 以使用相對路徑- [992](https://github.com/NuGet/Home/issues/992)</span><span class="sxs-lookup"><span data-stu-id="04a1b-133">Corrected restore command with `-SolutionDirectory` switch to work with relative paths - [992](https://github.com/NuGet/Home/issues/992)</span></span>
* <span data-ttu-id="04a1b-134">改進的更新命令以支援解決方案範圍的更新- [924](https://github.com/NuGet/Home/issues/924)</span><span class="sxs-lookup"><span data-stu-id="04a1b-134">Improved Updated command to support solution-wide update - [924](https://github.com/NuGet/Home/issues/924)</span></span>

<span data-ttu-id="04a1b-135">您可以在 NuGet GitHub [命令列里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)中找到此版本所解決之問題的完整清單。</span><span class="sxs-lookup"><span data-stu-id="04a1b-135">A complete list of issues addressed in this release can be found in the NuGet GitHub [Command-Line milestone](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).</span></span>

## <a name="visual-studio-extension-updates"></a><span data-ttu-id="04a1b-136">Visual Studio 擴充功能更新</span><span class="sxs-lookup"><span data-stu-id="04a1b-136">Visual Studio extension updates</span></span>

### <a name="new-features-in-visual-studio"></a><span data-ttu-id="04a1b-137">Visual Studio 的新功能</span><span class="sxs-lookup"><span data-stu-id="04a1b-137">New Features in Visual Studio</span></span>

* <span data-ttu-id="04a1b-138">方案節點上的方案總管中加入了新的內容功能表項目，可讓封裝還原，而不需要 ([1274](https://github.com/NuGet/Home/issues/1274)) 建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="04a1b-138">A new context menu item was added to the Solution Explorer on the solution node that allows packages to be restored without building the solution ([1274](https://github.com/NuGet/Home/issues/1274)).</span></span>

![新增 [還原套件] 內容功能表項目](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a><span data-ttu-id="04a1b-140">Visual Studio 中的更新和修正</span><span class="sxs-lookup"><span data-stu-id="04a1b-140">Updates and Fixes in Visual Studio</span></span>

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a><span data-ttu-id="04a1b-141">驗證摘要的修正程式也會在擴充功能中匯總和定址。</span><span class="sxs-lookup"><span data-stu-id="04a1b-141">The fixes for authenticated feeds were rolled up and addressed in the extension as well.</span></span>  <span data-ttu-id="04a1b-142">下列驗證專案也會在擴充功能中解決：</span><span class="sxs-lookup"><span data-stu-id="04a1b-142">The following authentication items were also addressed in the extension:</span></span>

* <span data-ttu-id="04a1b-143">現在正確地正確地將 NuGet v3 驗證的摘要正確地妥善處理，而不是 v2 驗證的摘要- [1216](https://github.com/NuGet/Home/issues/1216)</span><span class="sxs-lookup"><span data-stu-id="04a1b-143">Now correctly treating NuGet v3 authenticated feeds properly, instead of as v2 authenticated feeds - [1216](https://github.com/NuGet/Home/issues/1216)</span></span>
* <span data-ttu-id="04a1b-144">使用和與 v2 摘要進行通訊，以更正專案中驗證認證的要求 `project.json` - [1082](https://github.com/NuGet/Home/issues/1082)</span><span class="sxs-lookup"><span data-stu-id="04a1b-144">Corrected request for authentication credentials in projects using `project.json` and communicating with v2 feeds - [1082](https://github.com/NuGet/Home/issues/1082)</span></span>

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a><span data-ttu-id="04a1b-145">網路連線已影響 Visual Studio 中的使用者介面，我們使用下列修正程式解決此問題：</span><span class="sxs-lookup"><span data-stu-id="04a1b-145">Network connectivity had affected the user interface in Visual Studio, and we addressed this with the following fixes:</span></span>

* <span data-ttu-id="04a1b-146">改進套件版本的本機快取維護- [1096](https://github.com/NuGet/Home/issues/1096)</span><span class="sxs-lookup"><span data-stu-id="04a1b-146">Improved the maintenance of the local cache of package versions - [1096](https://github.com/NuGet/Home/issues/1096)</span></span>
* <span data-ttu-id="04a1b-147">變更連接到 v3 摘要時失敗的行為，不會再嘗試將它視為 v2 摘要- [1253](https://github.com/NuGet/Home/issues/1253)</span><span class="sxs-lookup"><span data-stu-id="04a1b-147">Changed the failure behavior when connecting to a v3 feed to no longer attempt to treat it as a v2 feed - [1253](https://github.com/NuGet/Home/issues/1253)</span></span>
* <span data-ttu-id="04a1b-148">現在防止安裝具有多個套件來源的套件時安裝失敗- [1183](https://github.com/NuGet/Home/issues/1183)</span><span class="sxs-lookup"><span data-stu-id="04a1b-148">Now preventing install failures when installing a package with multiple package sources - [1183](https://github.com/NuGet/Home/issues/1183)</span></span>

<span data-ttu-id="04a1b-149">我們已改善與組建作業的互動處理：</span><span class="sxs-lookup"><span data-stu-id="04a1b-149">We improved handling of interactions with build operations:</span></span>

* <span data-ttu-id="04a1b-150">如果還原單一專案的封裝失敗，現在繼續建立專案- [1169](https://github.com/NuGet/Home/issues/1169)</span><span class="sxs-lookup"><span data-stu-id="04a1b-150">Now continuing to build projects if restoring packages for a single project fails - [1169](https://github.com/NuGet/Home/issues/1169)</span></span>
* <span data-ttu-id="04a1b-151">將套件安裝至相依于方案中另一個專案的專案時，會強制方案重建- [981](https://github.com/NuGet/Home/issues/981)</span><span class="sxs-lookup"><span data-stu-id="04a1b-151">Installing a package into a project that is depended on by another project in the solution forces a solution rebuild - [981](https://github.com/NuGet/Home/issues/981)</span></span>
* <span data-ttu-id="04a1b-152">已更正失敗的套件安裝以正確地復原專案的變更- [1265](https://github.com/NuGet/Home/issues/1265)</span><span class="sxs-lookup"><span data-stu-id="04a1b-152">Corrected failed package installs to properly rollback changes to a project - [1265](https://github.com/NuGet/Home/issues/1265)</span></span>
* <span data-ttu-id="04a1b-153">修正 `developmentDependency` 在 `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)中意外移除封裝的屬性</span><span class="sxs-lookup"><span data-stu-id="04a1b-153">Corrected inadvertent removal of the `developmentDependency` attribute on a package in `packages.config` - [1263](https://github.com/NuGet/Home/issues/1263)</span></span>
* <span data-ttu-id="04a1b-154">呼叫 `install.ps1` 現在已傳遞適當的 `$package.AssemblyReferences` 物件- [1245](https://github.com/NuGet/Home/issues/1245)</span><span class="sxs-lookup"><span data-stu-id="04a1b-154">Calls to `install.ps1` now have a proper `$package.AssemblyReferences` object passed - [1245](https://github.com/NuGet/Home/issues/1245)</span></span>
* <span data-ttu-id="04a1b-155">當專案處於不正常的狀態時，不會再防止卸載 UWP 專案中的套件- [1128](https://github.com/NuGet/Home/issues/1128)</span><span class="sxs-lookup"><span data-stu-id="04a1b-155">No longer preventing uninstalls of packages in UWP projects while the project is in a bad state - [1128](https://github.com/NuGet/Home/issues/1128)</span></span>
* <span data-ttu-id="04a1b-156">`packages.config`現在已正確建立包含混合和專案的方案， `project.json` 而不需要第二個組建作業- [1122](https://github.com/NuGet/Home/issues/1122)</span><span class="sxs-lookup"><span data-stu-id="04a1b-156">Solutions containing a mix of `packages.config` and `project.json` projects are now properly built without requiring a second build operation - [1122](https://github.com/NuGet/Home/issues/1122)</span></span>
* <span data-ttu-id="04a1b-157">如果連結或位於不同的資料夾（ [1111](https://github.com/NuGet/Home/issues/1111)、 [894](https://github.com/NuGet/Home/issues/894) ），適當地找出 app.config 檔案</span><span class="sxs-lookup"><span data-stu-id="04a1b-157">Properly locating app.config files if they are linked or located in a different folder - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)</span></span>
* <span data-ttu-id="04a1b-158">UWP 專案現在可以安裝未列出的套件- [1109](https://github.com/NuGet/Home/issues/1109)</span><span class="sxs-lookup"><span data-stu-id="04a1b-158">UWP projects can now install unlisted packages - [1109](https://github.com/NuGet/Home/issues/1109)</span></span>
* <span data-ttu-id="04a1b-159">當解決方案未處於儲存狀態時，現在允許套件還原- [1081](https://github.com/NuGet/Home/issues/1081)</span><span class="sxs-lookup"><span data-stu-id="04a1b-159">Package restore is now allowed while a solution is not in a saved state - [1081](https://github.com/NuGet/Home/issues/1081)</span></span>


<span data-ttu-id="04a1b-160">處理設定檔的更新已修正：</span><span class="sxs-lookup"><span data-stu-id="04a1b-160">Handling updates to configuration files were corrected:</span></span>

* <span data-ttu-id="04a1b-161">不再從 managed 專案的後續組建中移除套件所傳遞的目標檔案 `project.json` - [1288](https://github.com/NuGet/Home/issues/1288)</span><span class="sxs-lookup"><span data-stu-id="04a1b-161">No longer removing a targets file delivered from a package on subsequent builds of a `project.json` managed project - [1288](https://github.com/NuGet/Home/issues/1288)</span></span>
* <span data-ttu-id="04a1b-162">在 ASP.NET 5 解決方案組建期間，不再修改 Nuget.Config 檔案- [1201](https://github.com/NuGet/Home/issues/1201)</span><span class="sxs-lookup"><span data-stu-id="04a1b-162">No longer modifying Nuget.Config files during ASP.NET 5 solution build - [1201](https://github.com/NuGet/Home/issues/1201)</span></span>
* <span data-ttu-id="04a1b-163">封裝更新期間不再變更允許的版本條件約束- [1130](https://github.com/NuGet/Home/issues/1130)</span><span class="sxs-lookup"><span data-stu-id="04a1b-163">No longer changing allowed versions constraint during package update - [1130](https://github.com/NuGet/Home/issues/1130)</span></span>
* <span data-ttu-id="04a1b-164">鎖定檔案現在在組建期間維持鎖定狀態- [1127](https://github.com/NuGet/Home/issues/1127)</span><span class="sxs-lookup"><span data-stu-id="04a1b-164">Lock files now remain locked during build - [1127](https://github.com/NuGet/Home/issues/1127)</span></span>
* <span data-ttu-id="04a1b-165">現在修改 `packages.config` 並不會在更新期間重寫- [585](https://github.com/NuGet/Home/issues/585)</span><span class="sxs-lookup"><span data-stu-id="04a1b-165">Now modifying `packages.config` and not rewriting it during updates - [585](https://github.com/NuGet/Home/issues/585)</span></span>


<span data-ttu-id="04a1b-166">與 TFS 原始檔控制的互動已獲得改良：</span><span class="sxs-lookup"><span data-stu-id="04a1b-166">Interactions with TFS source control are improved:</span></span>

* <span data-ttu-id="04a1b-167">針對系結至 TFS- [1164](https://github.com/NuGet/Home/issues/1164)， [980](https://github.com/NuGet/Home/issues/980)的封裝，不會再安裝失敗</span><span class="sxs-lookup"><span data-stu-id="04a1b-167">No longer failing installs for packages that are bound to TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)</span></span>
* <span data-ttu-id="04a1b-168">已更正 NuGet 使用者介面以允許 TFS 2013 整合- [1071](https://github.com/NuGet/Home/issues/1071)</span><span class="sxs-lookup"><span data-stu-id="04a1b-168">Corrected NuGet user interface to allow TFS 2013 integration - [1071](https://github.com/NuGet/Home/issues/1071)</span></span>
* <span data-ttu-id="04a1b-169">已更正還原的套件參考，可正確地來自套件資料夾- [1004](https://github.com/NuGet/Home/issues/1004)</span><span class="sxs-lookup"><span data-stu-id="04a1b-169">Corrected references to packages restored to properly come from a packages folder - [1004](https://github.com/NuGet/Home/issues/1004)</span></span>

<span data-ttu-id="04a1b-170">最後，我們也改善了這些專案：</span><span class="sxs-lookup"><span data-stu-id="04a1b-170">Finally, we also improved these items:</span></span>

* <span data-ttu-id="04a1b-171">針對 managed 專案減少記錄檔訊息的詳細資訊 `project.json` - [1163](https://github.com/NuGet/Home/issues/1163)</span><span class="sxs-lookup"><span data-stu-id="04a1b-171">Verbosity of log messages reduced for `project.json` managed projects - [1163](https://github.com/NuGet/Home/issues/1163)</span></span>
* <span data-ttu-id="04a1b-172">現在會正確地在使用者介面中顯示已安裝的套件版本- [1061](https://github.com/NuGet/Home/issues/1061)</span><span class="sxs-lookup"><span data-stu-id="04a1b-172">Now properly displaying the installed version of a package in the user interface - [1061](https://github.com/NuGet/Home/issues/1061)</span></span>


<span data-ttu-id="04a1b-173">您可以在 NuGet GitHub [3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)中找到針對 Visual Studio 擴充功能所解決之問題的完整清單</span><span class="sxs-lookup"><span data-stu-id="04a1b-173">A complete list of issues addressed for the Visual Studio extension can be found in the NuGet GitHub [3.2 milestone](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span></span>

## <a name="known-issues"></a><span data-ttu-id="04a1b-174">已知問題</span><span class="sxs-lookup"><span data-stu-id="04a1b-174">Known Issues</span></span>

<span data-ttu-id="04a1b-175">我們會持續追蹤 GitHub 問題清單的問題，您可以在下列網址找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="04a1b-175">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>