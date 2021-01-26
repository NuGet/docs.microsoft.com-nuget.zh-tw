---
title: NuGet 3.2 版本資訊
description: NuGet 3.2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 38a56b1572770b02ff09135a3b0290742ca80f41
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780306"
---
# <a name="nuget-32-release-notes"></a><span data-ttu-id="150ad-103">NuGet 3.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="150ad-103">NuGet 3.2 Release Notes</span></span>

<span data-ttu-id="150ad-104">[NuGet 3.2-RC 版本](../release-notes/nuget-3.2-RC.md)  |  資訊[NuGet 3.2.1 版本](../release-notes/nuget-3.2.1.md)資訊</span><span class="sxs-lookup"><span data-stu-id="150ad-104">[NuGet 3.2-RC Release Notes](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md)</span></span>

<span data-ttu-id="150ad-105">NuGet 3.2 于2015年9月16日發行為3.1.1 版本的改進和修正集合，可從 [dist.nuget.org](http://dist.nuget.org/index.html) 和 [Visual Studio 資源庫](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)取得。</span><span class="sxs-lookup"><span data-stu-id="150ad-105">NuGet 3.2 was released September 16, 2015 as a collection of improvements and fixes for the 3.1.1 release and is available from both [dist.nuget.org](http://dist.nuget.org/index.html) and the [Visual Studio Gallery](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).</span></span>

## <a name="new-features"></a><span data-ttu-id="150ad-106">新功能</span><span class="sxs-lookup"><span data-stu-id="150ad-106">New Features</span></span>

* <span data-ttu-id="150ad-107">存在於相同資料夾中的專案現在可以 `project.json` 在每個專案特有的該資料夾中有不同的檔案。</span><span class="sxs-lookup"><span data-stu-id="150ad-107">Projects that live in the same folder can now have different `project.json` files in that folder specific to each project.</span></span>  <span data-ttu-id="150ad-108">針對每個專案，為檔案命名， `project.json` `{ProjectName}.project.json` 且 NuGet 會適當地為每個專案提供該設定的喜好設定。</span><span class="sxs-lookup"><span data-stu-id="150ad-108">For each project, name the `project.json` file `{ProjectName}.project.json` and NuGet will give preference to that configuration for each project appropriately.</span></span>  <span data-ttu-id="150ad-109">只有安裝 Windows 10 Tools v1.1 才支援此功能-  [1102](https://github.com/NuGet/Home/issues/1102)</span><span class="sxs-lookup"><span data-stu-id="150ad-109">This is only supported with Windows 10 Tools v1.1 installed -  [1102](https://github.com/NuGet/Home/issues/1102)</span></span>
* <span data-ttu-id="150ad-110">NuGet 用戶端支援指定全域 NUGET_PACKAGES 環境變數，以指定 `project.json` managed 專案中使用 Windows 10 tools v1.1 的共用全域套件資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="150ad-110">NuGet clients support specifying a global NUGET_PACKAGES environment variable to specify the location of the shared global packages folder used in `project.json` managed projects with Windows 10 tools v1.1.</span></span>

## <a name="command-line-updates"></a><span data-ttu-id="150ad-111">命令列更新</span><span class="sxs-lookup"><span data-stu-id="150ad-111">Command-line updates</span></span>

<span data-ttu-id="150ad-112">這是第一個支援 NuGet v3 伺服器的 nuget.exe 用戶端版本，以及針對以檔案管理的專案還原套件的第一版 `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="150ad-112">This is the first version of the nuget.exe client that supports the NuGet v3 servers and restoring packages for projects managed with a `project.json` file.</span></span>

<span data-ttu-id="150ad-113">此版本中已解決一些已驗證的摘要問題，以改善與用戶端的互動。</span><span class="sxs-lookup"><span data-stu-id="150ad-113">There were a number of authenticated feed issues that were addressed in this release to improve interactions with the client.</span></span>

* <span data-ttu-id="150ad-114">安裝/還原互動只會將初始要求的認證提交給已驗證的摘要- [1300](https://github.com/NuGet/Home/issues/1300)、 [456](https://github.com/NuGet/Home/issues/456)</span><span class="sxs-lookup"><span data-stu-id="150ad-114">Install / restore interactions only submit credentials for the initial request to the authenticated feed - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)</span></span>
* <span data-ttu-id="150ad-115">Push 命令無法解析來自設定的認證- [1248](https://github.com/NuGet/Home/issues/1248)</span><span class="sxs-lookup"><span data-stu-id="150ad-115">Push command does not resolve credentials from configuration - [1248](https://github.com/NuGet/Home/issues/1248)</span></span>
* <span data-ttu-id="150ad-116">使用者代理程式和標頭現在已提交至 NuGet 存放庫，以協助進行統計資料追蹤- [929](https://github.com/NuGet/Home/issues/929)</span><span class="sxs-lookup"><span data-stu-id="150ad-116">User agent and headers are now submitted to NuGet repositories to help with statistics tracking - [929](https://github.com/NuGet/Home/issues/929)</span></span>

<span data-ttu-id="150ad-117">我們進行了一些改善，以在嘗試使用遠端 NuGet 存放庫時更妥善處理網路失敗：</span><span class="sxs-lookup"><span data-stu-id="150ad-117">We made a number of improvements to better handle network failures while attempting to work with a remote NuGet repository:</span></span>

* <span data-ttu-id="150ad-118">改進無法連接到遠端摘要時的錯誤訊息- [1238](https://github.com/NuGet/Home/issues/1238)</span><span class="sxs-lookup"><span data-stu-id="150ad-118">Improved error messages when unable to connect to remote feeds - [1238](https://github.com/NuGet/Home/issues/1238)</span></span>
* <span data-ttu-id="150ad-119">修正了 NuGet 還原命令，以在發生錯誤狀況時正確傳回 1- [1186](https://github.com/NuGet/Home/issues/1186)</span><span class="sxs-lookup"><span data-stu-id="150ad-119">Corrected NuGet restore command to properly return a 1 when an error condition occurs - [1186](https://github.com/NuGet/Home/issues/1186)</span></span>
* <span data-ttu-id="150ad-120">現在，在 HTTP 5xx [1120](https://github.com/NuGet/Home/issues/1120)失敗的情況下，每個200毫秒重試網路連接最多5次</span><span class="sxs-lookup"><span data-stu-id="150ad-120">Now retrying network connections every 200ms for a maximum of 5 attempts in the case of HTTP 5xx failures - [1120](https://github.com/NuGet/Home/issues/1120)</span></span>
* <span data-ttu-id="150ad-121">改進在推送命令期間處理伺服器重新導向回應的功能- [1051](https://github.com/NuGet/Home/issues/1051)</span><span class="sxs-lookup"><span data-stu-id="150ad-121">Improved handling of server redirect responses during a push command - [1051](https://github.com/NuGet/Home/issues/1051)</span></span>
* <span data-ttu-id="150ad-122">`nuget install -source` 現在支援 Nuget.Config 的 URL 或存放庫名稱做為引數- [1046](https://github.com/NuGet/Home/issues/1046)</span><span class="sxs-lookup"><span data-stu-id="150ad-122">`nuget install -source` now supports either URL or repository name from Nuget.Config as an argument - [1046](https://github.com/NuGet/Home/issues/1046)</span></span>
* <span data-ttu-id="150ad-123">在還原期間缺少存放庫的套件，現在會回報為錯誤，而不是警告 [1038](https://github.com/NuGet/Home/issues/1038)</span><span class="sxs-lookup"><span data-stu-id="150ad-123">Missing packages that were not located on a repository during a restore are now reported as errors instead of warnings [1038](https://github.com/NuGet/Home/issues/1038)</span></span>
* <span data-ttu-id="150ad-124">修正了 \r\n for Unix/Linux 案例的 multipartwebrequest 處理- [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="150ad-124">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>

<span data-ttu-id="150ad-125">各種命令的問題有一些修正：</span><span class="sxs-lookup"><span data-stu-id="150ad-125">There are a number of fixes to issues with various commands:</span></span>

* <span data-ttu-id="150ad-126">推播命令不再針對套件來源進行 PUT 之前的 GET- [1237](https://github.com/NuGet/Home/issues/1237)</span><span class="sxs-lookup"><span data-stu-id="150ad-126">Push command no longer does a GET before a PUT against a package source - [1237](https://github.com/NuGet/Home/issues/1237)</span></span>
* <span data-ttu-id="150ad-127">List 命令不再重複版本號碼- [1185](https://github.com/NuGet/Home/issues/1185)</span><span class="sxs-lookup"><span data-stu-id="150ad-127">List command no longer repeats version numbers - [1185](https://github.com/NuGet/Home/issues/1185)</span></span>
* <span data-ttu-id="150ad-128">具有-build 引數的套件現已正確支援 c # 6.0- [1107](https://github.com/NuGet/Home/issues/1107)</span><span class="sxs-lookup"><span data-stu-id="150ad-128">Pack with the -build argument now properly supports C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)</span></span>
* <span data-ttu-id="150ad-129">修正了嘗試封裝以 Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048)所建立的 F # 專案時所發生的問題</span><span class="sxs-lookup"><span data-stu-id="150ad-129">Corrected issues attempting to pack an F# project built with Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)</span></span>
* <span data-ttu-id="150ad-130">當套件已存在時立即還原- [1040](https://github.com/NuGet/Home/issues/1040)</span><span class="sxs-lookup"><span data-stu-id="150ad-130">Restore now no-ops when packages already exist - [1040](https://github.com/NuGet/Home/issues/1040)</span></span>
* <span data-ttu-id="150ad-131">改進檔案 `packages.config` 格式不正確的錯誤訊息 [-1034](https://github.com/NuGet/Home/issues/1034)</span><span class="sxs-lookup"><span data-stu-id="150ad-131">Improved error messages when `packages.config` file is malformed - [1034](https://github.com/NuGet/Home/issues/1034)</span></span>
* <span data-ttu-id="150ad-132">使用-SolutionDirectory 參數更正了還原命令以使用相對路徑- [992](https://github.com/NuGet/Home/issues/992)</span><span class="sxs-lookup"><span data-stu-id="150ad-132">Corrected restore command with -SolutionDirectory switch to work with relative paths - [992](https://github.com/NuGet/Home/issues/992)</span></span>
* <span data-ttu-id="150ad-133">改進的更新命令以支援解決方案範圍的更新- [924](https://github.com/NuGet/Home/issues/924)</span><span class="sxs-lookup"><span data-stu-id="150ad-133">Improved Updated command to support solution-wide update - [924](https://github.com/NuGet/Home/issues/924)</span></span>

<span data-ttu-id="150ad-134">您可以在 NuGet GitHub [命令列里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)中找到此版本所解決之問題的完整清單。</span><span class="sxs-lookup"><span data-stu-id="150ad-134">A complete list of issues addressed in this release can be found in the NuGet GitHub [Command-Line milestone](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).</span></span>

## <a name="visual-studio-extension-updates"></a><span data-ttu-id="150ad-135">Visual Studio 擴充功能更新</span><span class="sxs-lookup"><span data-stu-id="150ad-135">Visual Studio extension updates</span></span>

### <a name="new-features-in-visual-studio"></a><span data-ttu-id="150ad-136">Visual Studio 的新功能</span><span class="sxs-lookup"><span data-stu-id="150ad-136">New Features in Visual Studio</span></span>

* <span data-ttu-id="150ad-137">方案節點上的方案總管中加入了新的內容功能表項目，可讓封裝還原，而不需要 ([1274](https://github.com/NuGet/Home/issues/1274)) 建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="150ad-137">A new context menu item was added to the Solution Explorer on the solution node that allows packages to be restored without building the solution ([1274](https://github.com/NuGet/Home/issues/1274)).</span></span>

![新增 [還原套件] 內容功能表項目](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a><span data-ttu-id="150ad-139">Visual Studio 中的更新和修正</span><span class="sxs-lookup"><span data-stu-id="150ad-139">Updates and Fixes in Visual Studio</span></span>

<span data-ttu-id="150ad-140">驗證摘要的修正程式也會在擴充功能中匯總和定址。</span><span class="sxs-lookup"><span data-stu-id="150ad-140">The fixes for authenticated feeds were rolled up and addressed in the extension as well.</span></span>  <span data-ttu-id="150ad-141">下列驗證專案也會在擴充功能中解決：</span><span class="sxs-lookup"><span data-stu-id="150ad-141">The following authentication items were also addressed in the extension:</span></span>

* <span data-ttu-id="150ad-142">現在正確地正確地將 NuGet v3 驗證的摘要正確地妥善處理，而不是 v2 驗證的摘要- [1216](https://github.com/NuGet/Home/issues/1216)</span><span class="sxs-lookup"><span data-stu-id="150ad-142">Now correctly treating NuGet v3 authenticated feeds properly, instead of as v2 authenticated feeds - [1216](https://github.com/NuGet/Home/issues/1216)</span></span>
* <span data-ttu-id="150ad-143">使用和與 v2 摘要進行通訊，以更正專案中驗證認證的要求 `project.json` - [1082](https://github.com/NuGet/Home/issues/1082)</span><span class="sxs-lookup"><span data-stu-id="150ad-143">Corrected request for authentication credentials in projects using `project.json` and communicating with v2 feeds - [1082](https://github.com/NuGet/Home/issues/1082)</span></span>

<span data-ttu-id="150ad-144">網路連線已影響 Visual Studio 中的使用者介面，我們使用下列修正程式解決此問題：</span><span class="sxs-lookup"><span data-stu-id="150ad-144">Network connectivity had affected the user interface in Visual Studio, and we addressed this with the following fixes:</span></span>

* <span data-ttu-id="150ad-145">改進套件版本的本機快取維護- [1096](https://github.com/NuGet/Home/issues/1096)</span><span class="sxs-lookup"><span data-stu-id="150ad-145">Improved the maintenance of the local cache of package versions - [1096](https://github.com/NuGet/Home/issues/1096)</span></span>
* <span data-ttu-id="150ad-146">變更連接到 v3 摘要時失敗的行為，不會再嘗試將它視為 v2 摘要- [1253](https://github.com/NuGet/Home/issues/1253)</span><span class="sxs-lookup"><span data-stu-id="150ad-146">Changed the failure behavior when connecting to a v3 feed to no longer attempt to treat it as a v2 feed - [1253](https://github.com/NuGet/Home/issues/1253)</span></span>
* <span data-ttu-id="150ad-147">現在防止安裝具有多個套件來源的套件時安裝失敗- [1183](https://github.com/NuGet/Home/issues/1183)</span><span class="sxs-lookup"><span data-stu-id="150ad-147">Now preventing install failures when installing a package with multiple package sources - [1183](https://github.com/NuGet/Home/issues/1183)</span></span>

<span data-ttu-id="150ad-148">我們已改善與組建作業的互動處理：</span><span class="sxs-lookup"><span data-stu-id="150ad-148">We improved handling of interactions with build operations:</span></span>

* <span data-ttu-id="150ad-149">如果還原單一專案的封裝失敗，現在繼續建立專案- [1169](https://github.com/NuGet/Home/issues/1169)</span><span class="sxs-lookup"><span data-stu-id="150ad-149">Now continuing to build projects if restoring packages for a single project fails - [1169](https://github.com/NuGet/Home/issues/1169)</span></span>
* <span data-ttu-id="150ad-150">將套件安裝至相依于方案中另一個專案的專案時，會強制方案重建- [981](https://github.com/NuGet/Home/issues/981)</span><span class="sxs-lookup"><span data-stu-id="150ad-150">Installing a package into a project that is depended on by another project in the solution forces a solution rebuild - [981](https://github.com/NuGet/Home/issues/981)</span></span>
* <span data-ttu-id="150ad-151">已更正失敗的套件安裝以正確地復原專案的變更- [1265](https://github.com/NuGet/Home/issues/1265)</span><span class="sxs-lookup"><span data-stu-id="150ad-151">Corrected failed package installs to properly rollback changes to a project - [1265](https://github.com/NuGet/Home/issues/1265)</span></span>
* <span data-ttu-id="150ad-152">修正 `developmentDependency` 在 `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)中意外移除封裝的屬性</span><span class="sxs-lookup"><span data-stu-id="150ad-152">Corrected inadvertent removal of the `developmentDependency` attribute on a package in `packages.config` - [1263](https://github.com/NuGet/Home/issues/1263)</span></span>
* <span data-ttu-id="150ad-153">呼叫 `install.ps1` 現在已傳遞適當的 `$package.AssemblyReferences` 物件- [1245](https://github.com/NuGet/Home/issues/1245)</span><span class="sxs-lookup"><span data-stu-id="150ad-153">Calls to `install.ps1` now have a proper `$package.AssemblyReferences` object passed - [1245](https://github.com/NuGet/Home/issues/1245)</span></span>
* <span data-ttu-id="150ad-154">當專案處於不正常的狀態時，不會再防止卸載 UWP 專案中的套件- [1128](https://github.com/NuGet/Home/issues/1128)</span><span class="sxs-lookup"><span data-stu-id="150ad-154">No longer preventing uninstalls of packages in UWP projects while the project is in a bad state - [1128](https://github.com/NuGet/Home/issues/1128)</span></span>
* <span data-ttu-id="150ad-155">`packages.config`現在已正確建立包含混合和專案的方案， `project.json` 而不需要第二個組建作業- [1122](https://github.com/NuGet/Home/issues/1122)</span><span class="sxs-lookup"><span data-stu-id="150ad-155">Solutions containing a mix of `packages.config` and `project.json` projects are now properly built without requiring a second build operation - [1122](https://github.com/NuGet/Home/issues/1122)</span></span>
* <span data-ttu-id="150ad-156">如果連結或位於不同的資料夾（ [1111](https://github.com/NuGet/Home/issues/1111)、 [894](https://github.com/NuGet/Home/issues/894) ），適當地找出 app.config 檔案</span><span class="sxs-lookup"><span data-stu-id="150ad-156">Properly locating app.config files if they are linked or located in a different folder - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)</span></span>
* <span data-ttu-id="150ad-157">UWP 專案現在可以安裝未列出的套件- [1109](https://github.com/NuGet/Home/issues/1109)</span><span class="sxs-lookup"><span data-stu-id="150ad-157">UWP projects can now install unlisted packages - [1109](https://github.com/NuGet/Home/issues/1109)</span></span>
* <span data-ttu-id="150ad-158">當解決方案未處於儲存狀態時，現在允許套件還原- [1081](https://github.com/NuGet/Home/issues/1081)</span><span class="sxs-lookup"><span data-stu-id="150ad-158">Package restore is now allowed while a solution is not in a saved state - [1081](https://github.com/NuGet/Home/issues/1081)</span></span>

<span data-ttu-id="150ad-159">處理設定檔的更新已修正：</span><span class="sxs-lookup"><span data-stu-id="150ad-159">Handling updates to configuration files were corrected:</span></span>

* <span data-ttu-id="150ad-160">不再從 managed 專案的後續組建中移除套件所傳遞的目標檔案 `project.json` - [1288](https://github.com/NuGet/Home/issues/1288)</span><span class="sxs-lookup"><span data-stu-id="150ad-160">No longer removing a targets file delivered from a package on subsequent builds of a `project.json` managed project - [1288](https://github.com/NuGet/Home/issues/1288)</span></span>
* <span data-ttu-id="150ad-161">在 ASP.NET 5 解決方案組建期間，不再修改 Nuget.Config 檔案- [1201](https://github.com/NuGet/Home/issues/1201)</span><span class="sxs-lookup"><span data-stu-id="150ad-161">No longer modifying Nuget.Config files during ASP.NET 5 solution build - [1201](https://github.com/NuGet/Home/issues/1201)</span></span>
* <span data-ttu-id="150ad-162">封裝更新期間不再變更允許的版本條件約束- [1130](https://github.com/NuGet/Home/issues/1130)</span><span class="sxs-lookup"><span data-stu-id="150ad-162">No longer changing allowed versions constraint during package update - [1130](https://github.com/NuGet/Home/issues/1130)</span></span>
* <span data-ttu-id="150ad-163">鎖定檔案現在在組建期間維持鎖定狀態- [1127](https://github.com/NuGet/Home/issues/1127)</span><span class="sxs-lookup"><span data-stu-id="150ad-163">Lock files now remain locked during build - [1127](https://github.com/NuGet/Home/issues/1127)</span></span>
* <span data-ttu-id="150ad-164">現在修改 `packages.config` 並不會在更新期間重寫- [585](https://github.com/NuGet/Home/issues/585)</span><span class="sxs-lookup"><span data-stu-id="150ad-164">Now modifying `packages.config` and not rewriting it during updates - [585](https://github.com/NuGet/Home/issues/585)</span></span>

<span data-ttu-id="150ad-165">與 TFS 原始檔控制的互動已獲得改良：</span><span class="sxs-lookup"><span data-stu-id="150ad-165">Interactions with TFS source control are improved:</span></span>

* <span data-ttu-id="150ad-166">針對系結至 TFS- [1164](https://github.com/NuGet/Home/issues/1164)， [980](https://github.com/NuGet/Home/issues/980)的封裝，不會再安裝失敗</span><span class="sxs-lookup"><span data-stu-id="150ad-166">No longer failing installs for packages that are bound to TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)</span></span>
* <span data-ttu-id="150ad-167">已更正 NuGet 使用者介面以允許 TFS 2013 整合- [1071](https://github.com/NuGet/Home/issues/1071)</span><span class="sxs-lookup"><span data-stu-id="150ad-167">Corrected NuGet user interface to allow TFS 2013 integration - [1071](https://github.com/NuGet/Home/issues/1071)</span></span>
* <span data-ttu-id="150ad-168">已更正還原的套件參考，可正確地來自套件資料夾- [1004](https://github.com/NuGet/Home/issues/1004)</span><span class="sxs-lookup"><span data-stu-id="150ad-168">Corrected references to packages restored to properly come from a packages folder - [1004](https://github.com/NuGet/Home/issues/1004)</span></span>

<span data-ttu-id="150ad-169">最後，我們也改善了這些專案：</span><span class="sxs-lookup"><span data-stu-id="150ad-169">Finally, we also improved these items:</span></span>

* <span data-ttu-id="150ad-170">針對 managed 專案減少記錄檔訊息的詳細資訊 `project.json` - [1163](https://github.com/NuGet/Home/issues/1163)</span><span class="sxs-lookup"><span data-stu-id="150ad-170">Verbosity of log messages reduced for `project.json` managed projects - [1163](https://github.com/NuGet/Home/issues/1163)</span></span>
* <span data-ttu-id="150ad-171">現在會正確地在使用者介面中顯示已安裝的套件版本- [1061](https://github.com/NuGet/Home/issues/1061)</span><span class="sxs-lookup"><span data-stu-id="150ad-171">Now properly displaying the installed version of a package in the user interface - [1061](https://github.com/NuGet/Home/issues/1061)</span></span>
* <span data-ttu-id="150ad-172">具有 nuspec 中所指定相依性範圍的套件，現在已針對穩定套件版本安裝這些相依性的發行前版本- [1304](https://github.com/NuGet/Home/issues/1304)</span><span class="sxs-lookup"><span data-stu-id="150ad-172">Packages with dependency ranges specified in their nuspec now have pre-release versions of those dependencies installed for a stable package version - [1304](https://github.com/NuGet/Home/issues/1304)</span></span>

<span data-ttu-id="150ad-173">您可以在 NuGet GitHub [3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)中找到針對 Visual Studio 擴充功能所解決之問題的完整清單</span><span class="sxs-lookup"><span data-stu-id="150ad-173">A complete list of issues addressed for the Visual Studio extension can be found in the NuGet GitHub [3.2 milestone](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span></span>

## <a name="known-issues"></a><span data-ttu-id="150ad-174">已知問題</span><span class="sxs-lookup"><span data-stu-id="150ad-174">Known Issues</span></span>

<span data-ttu-id="150ad-175">我們會持續追蹤 GitHub 問題清單的問題，您可以在下列網址找到： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="150ad-175">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>