---
title: NuGet 3.2 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 3.2 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5bdd2aa5621eead9ce79794052663cc2f8a63d45
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549518"
---
# <a name="nuget-32-release-notes"></a><span data-ttu-id="f4256-103">NuGet 3.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="f4256-103">NuGet 3.2 Release Notes</span></span>

<span data-ttu-id="f4256-104">[NuGet 3.2 RC 版本資訊](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 版本資訊](../release-notes/nuget-3.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="f4256-104">[NuGet 3.2-RC Release Notes](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md)</span></span>

<span data-ttu-id="f4256-105">發行 NuGet 3.2 2015 年 9 月 16 日的改進和修正 3.1.1 集合版本，並且可從[dist.nuget.org](http://dist.nuget.org/index.html)並[Visual Studio 元件庫](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015)。</span><span class="sxs-lookup"><span data-stu-id="f4256-105">NuGet 3.2 was released September 16, 2015 as a collection of improvements and fixes for the 3.1.1 release and is available from both [dist.nuget.org](http://dist.nuget.org/index.html) and the [Visual Studio Gallery](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2015).</span></span>

## <a name="new-features"></a><span data-ttu-id="f4256-106">新功能</span><span class="sxs-lookup"><span data-stu-id="f4256-106">New Features</span></span>

* <span data-ttu-id="f4256-107">存在於相同的資料夾中的專案現在可以有不同`project.json`特有的每個專案的資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="f4256-107">Projects that live in the same folder can now have different `project.json` files in that folder specific to each project.</span></span>  <span data-ttu-id="f4256-108">針對每個專案，命名`project.json`檔案`{ProjectName}.project.json`，NuGet 就會適當地給喜好設定給每個專案的組態。</span><span class="sxs-lookup"><span data-stu-id="f4256-108">For each project, name the `project.json` file `{ProjectName}.project.json` and NuGet will give preference to that configuration for each project appropriately.</span></span>  <span data-ttu-id="f4256-109">這僅支援安裝的 Windows 10 工具 v1.1 [1102年](https://github.com/NuGet/Home/issues/1102)</span><span class="sxs-lookup"><span data-stu-id="f4256-109">This is only supported with Windows 10 Tools v1.1 installed -  [1102](https://github.com/NuGet/Home/issues/1102)</span></span>
* <span data-ttu-id="f4256-110">NuGet 用戶端支援指定全域的 NUGET_PACKAGES 環境變數來指定用於共用的全域套件資料夾的位置`project.json`管理具有 Windows 10 工具 1.1 版的專案。</span><span class="sxs-lookup"><span data-stu-id="f4256-110">NuGet clients support specifying a global NUGET_PACKAGES environment variable to specify the location of the shared global packages folder used in `project.json` managed projects with Windows 10 tools v1.1.</span></span>

## <a name="command-line-updates"></a><span data-ttu-id="f4256-111">命令列的更新</span><span class="sxs-lookup"><span data-stu-id="f4256-111">Command-line updates</span></span>

<span data-ttu-id="f4256-112">這是支援 NuGet v3 伺服器的 nuget.exe 用戶端的第一個版本，並使用正在還原專案的封裝管理`project.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="f4256-112">This is the first version of the nuget.exe client that supports the NuGet v3 servers and restoring packages for projects managed with a `project.json` file.</span></span>

<span data-ttu-id="f4256-113">沒有已驗證摘要處理問題，都在此版本中提升用戶端之間的互動數。</span><span class="sxs-lookup"><span data-stu-id="f4256-113">There were a number of authenticated feed issues that were addressed in this release to improve interactions with the client.</span></span>

* <span data-ttu-id="f4256-114">安裝 / 還原互動只會提交已驗證的摘要-的初始要求的認證[1300年](https://github.com/NuGet/Home/issues/1300)， [456](https://github.com/NuGet/Home/issues/456)</span><span class="sxs-lookup"><span data-stu-id="f4256-114">Install / restore interactions only submit credentials for the initial request to the authenticated feed - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)</span></span>
* <span data-ttu-id="f4256-115">推送命令無法解決從組態集的認證[1248年](https://github.com/NuGet/Home/issues/1248)</span><span class="sxs-lookup"><span data-stu-id="f4256-115">Push command does not resolve credentials from configuration - [1248](https://github.com/NuGet/Home/issues/1248)</span></span>
* <span data-ttu-id="f4256-116">使用者代理程式 」 和 「 標頭現在會提交至 NuGet 存放庫，來協助進行統計資料追蹤- [929](https://github.com/NuGet/Home/issues/929)</span><span class="sxs-lookup"><span data-stu-id="f4256-116">User agent and headers are now submitted to NuGet repositories to help with statistics tracking - [929](https://github.com/NuGet/Home/issues/929)</span></span>

<span data-ttu-id="f4256-117">我們進行了多項改良，可更妥善處理網路失敗，嘗試使用遠端的 NuGet 存放庫：</span><span class="sxs-lookup"><span data-stu-id="f4256-117">We made a number of improvements to better handle network failures while attempting to work with a remote NuGet repository:</span></span>

* <span data-ttu-id="f4256-118">改進錯誤訊息時無法連線到遠端的摘要- [1238年](https://github.com/NuGet/Home/issues/1238)</span><span class="sxs-lookup"><span data-stu-id="f4256-118">Improved error messages when unable to connect to remote feeds - [1238](https://github.com/NuGet/Home/issues/1238)</span></span>
* <span data-ttu-id="f4256-119">已更正 NuGet 還原命令，以正確地傳回 1，當錯誤狀況，就會發生- [1186年](https://github.com/NuGet/Home/issues/1186)</span><span class="sxs-lookup"><span data-stu-id="f4256-119">Corrected NuGet restore command to properly return a 1 when an error condition occurs - [1186](https://github.com/NuGet/Home/issues/1186)</span></span>
* <span data-ttu-id="f4256-120">現在重試網路連線的 HTTP 5xx 故障-5 的嘗試次數最多每隔 200 毫秒[1120年](https://github.com/NuGet/Home/issues/1120)</span><span class="sxs-lookup"><span data-stu-id="f4256-120">Now retrying network connections every 200ms for a maximum of 5 attempts in the case of HTTP 5xx failures - [1120](https://github.com/NuGet/Home/issues/1120)</span></span>
* <span data-ttu-id="f4256-121">改進的伺服器重新導向回應的處理期間的 push 命令- [1051年](https://github.com/NuGet/Home/issues/1051)</span><span class="sxs-lookup"><span data-stu-id="f4256-121">Improved handling of server redirect responses during a push command - [1051](https://github.com/NuGet/Home/issues/1051)</span></span>
* <span data-ttu-id="f4256-122">`nuget install -source` 現在支援 URL 或儲存機制名稱做為引數-Nuget.Config [1046年](https://github.com/NuGet/Home/issues/1046)</span><span class="sxs-lookup"><span data-stu-id="f4256-122">`nuget install -source` now supports either URL or repository name from Nuget.Config as an argument - [1046](https://github.com/NuGet/Home/issues/1046)</span></span>
* <span data-ttu-id="f4256-123">遺漏的套件在還原期間不位於存放庫現在會回報為錯誤而非警告[1038年](https://github.com/NuGet/Home/issues/1038)</span><span class="sxs-lookup"><span data-stu-id="f4256-123">Missing packages that were not located on a repository during a restore are now reported as errors instead of warnings [1038](https://github.com/NuGet/Home/issues/1038)</span></span>
* <span data-ttu-id="f4256-124">已更正的 Unix/Linux 案例-\r\n multipartwebrequest 處理[776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="f4256-124">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>

<span data-ttu-id="f4256-125">有數個與各種命令的問題的修正：</span><span class="sxs-lookup"><span data-stu-id="f4256-125">There are a number of fixes to issues with various commands:</span></span>

* <span data-ttu-id="f4256-126">推送命令不會再發生之前對套件來源-PUT GET [1237年](https://github.com/NuGet/Home/issues/1237)</span><span class="sxs-lookup"><span data-stu-id="f4256-126">Push command no longer does a GET before a PUT against a package source - [1237](https://github.com/NuGet/Home/issues/1237)</span></span>
* <span data-ttu-id="f4256-127">列出命令不會再重複的版本號碼- [1185年](https://github.com/NuGet/Home/issues/1185)</span><span class="sxs-lookup"><span data-stu-id="f4256-127">List command no longer repeats version numbers - [1185](https://github.com/NuGet/Home/issues/1185)</span></span>
* <span data-ttu-id="f4256-128">組件使用-建置引數現在正確支援 C# 6.0- [1107年](https://github.com/NuGet/Home/issues/1107)</span><span class="sxs-lookup"><span data-stu-id="f4256-128">Pack with the -build argument now properly supports C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)</span></span>
* <span data-ttu-id="f4256-129">已修正的問題，嘗試將組件的 F # 專案建置與 Visual Studio 2015- [1048年](https://github.com/NuGet/Home/issues/1048)</span><span class="sxs-lookup"><span data-stu-id="f4256-129">Corrected issues attempting to pack an F# project built with Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)</span></span>
* <span data-ttu-id="f4256-130">還原現在不會生效，當封裝已經存在- [1040年](https://github.com/NuGet/Home/issues/1040)</span><span class="sxs-lookup"><span data-stu-id="f4256-130">Restore now no-ops when packages already exist - [1040](https://github.com/NuGet/Home/issues/1040)</span></span>
* <span data-ttu-id="f4256-131">改良的錯誤訊息的時機`packages.config`檔案格式不正確- [1034年](https://github.com/NuGet/Home/issues/1034)</span><span class="sxs-lookup"><span data-stu-id="f4256-131">Improved error messages when `packages.config` file is malformed - [1034](https://github.com/NuGet/Home/issues/1034)</span></span>
* <span data-ttu-id="f4256-132">已更正還原命令搭配-SolutionDirectory 參數搭配使用相對路徑- [992](https://github.com/NuGet/Home/issues/992)</span><span class="sxs-lookup"><span data-stu-id="f4256-132">Corrected restore command with -SolutionDirectory switch to work with relative paths - [992](https://github.com/NuGet/Home/issues/992)</span></span>
* <span data-ttu-id="f4256-133">改善更新命令，以支援整個方案的更新- [924](https://github.com/NuGet/Home/issues/924)</span><span class="sxs-lookup"><span data-stu-id="f4256-133">Improved Updated command to support solution-wide update - [924](https://github.com/NuGet/Home/issues/924)</span></span>

<span data-ttu-id="f4256-134">在此版本中已解決問題的完整清單可在 NuGet GitHub[命令列里程碑](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)。</span><span class="sxs-lookup"><span data-stu-id="f4256-134">A complete list of issues addressed in this release can be found in the NuGet GitHub [Command-Line milestone](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).</span></span>

## <a name="visual-studio-extension-updates"></a><span data-ttu-id="f4256-135">Visual Studio 擴充功能更新</span><span class="sxs-lookup"><span data-stu-id="f4256-135">Visual Studio extension updates</span></span>

### <a name="new-features-in-visual-studio"></a><span data-ttu-id="f4256-136">Visual Studio 中的新功能</span><span class="sxs-lookup"><span data-stu-id="f4256-136">New Features in Visual Studio</span></span>

* <span data-ttu-id="f4256-137">新的操作功能表項目已加入至方案總管中，於 [方案] 節點，可讓封裝以建置方案，才能還原 ([1274年](https://github.com/NuGet/Home/issues/1274))。</span><span class="sxs-lookup"><span data-stu-id="f4256-137">A new context menu item was added to the Solution Explorer on the solution node that allows packages to be restored without building the solution ([1274](https://github.com/NuGet/Home/issues/1274)).</span></span>

![新 '還原套件' 操作功能表項目](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a><span data-ttu-id="f4256-139">更新和修正在 Visual Studio 中</span><span class="sxs-lookup"><span data-stu-id="f4256-139">Updates and Fixes in Visual Studio</span></span>

<span data-ttu-id="f4256-140">已驗證的摘要的修正彙總中的延伸模組已解決。</span><span class="sxs-lookup"><span data-stu-id="f4256-140">The fixes for authenticated feeds were rolled up and addressed in the extension as well.</span></span>  <span data-ttu-id="f4256-141">延伸模組已也將討論下列驗證項目：</span><span class="sxs-lookup"><span data-stu-id="f4256-141">The following authentication items were also addressed in the extension:</span></span>

* <span data-ttu-id="f4256-142">現在正確將 NuGet v3 已驗證的摘要正確，而不是如 v2 驗證摘要- [1216年](https://github.com/NuGet/Home/issues/1216)</span><span class="sxs-lookup"><span data-stu-id="f4256-142">Now correctly treating NuGet v3 authenticated feeds properly, instead of as v2 authenticated feeds - [1216](https://github.com/NuGet/Home/issues/1216)</span></span>
* <span data-ttu-id="f4256-143">已更正的要求，在專案中使用的驗證認證`project.json`，而且與 v2 摘要-通訊[1082年](https://github.com/NuGet/Home/issues/1082)</span><span class="sxs-lookup"><span data-stu-id="f4256-143">Corrected request for authentication credentials in projects using `project.json` and communicating with v2 feeds - [1082](https://github.com/NuGet/Home/issues/1082)</span></span>

<span data-ttu-id="f4256-144">網路連線有影響的使用者介面，在 Visual Studio 中，和我們解決這與下列修正：</span><span class="sxs-lookup"><span data-stu-id="f4256-144">Network connectivity had affected the user interface in Visual Studio, and we addressed this with the following fixes:</span></span>

* <span data-ttu-id="f4256-145">改善的套件版本的本機快取維護[1096年](https://github.com/NuGet/Home/issues/1096)</span><span class="sxs-lookup"><span data-stu-id="f4256-145">Improved the maintenance of the local cache of package versions - [1096](https://github.com/NuGet/Home/issues/1096)</span></span>
* <span data-ttu-id="f4256-146">連接至 v3，不會再嘗試將它視為 v2 摘要-摘要時，變更失敗行為[1253年](https://github.com/NuGet/Home/issues/1253)</span><span class="sxs-lookup"><span data-stu-id="f4256-146">Changed the failure behavior when connecting to a v3 feed to no longer attempt to treat it as a v2 feed - [1253](https://github.com/NuGet/Home/issues/1253)</span></span>
* <span data-ttu-id="f4256-147">現在會導致安裝失敗，使用多個套件來源-安裝套件時[1183年](https://github.com/NuGet/Home/issues/1183)</span><span class="sxs-lookup"><span data-stu-id="f4256-147">Now preventing install failures when installing a package with multiple package sources - [1183](https://github.com/NuGet/Home/issues/1183)</span></span>

<span data-ttu-id="f4256-148">我們已改善建置作業之間的互動的處理：</span><span class="sxs-lookup"><span data-stu-id="f4256-148">We improved handling of interactions with build operations:</span></span>

* <span data-ttu-id="f4256-149">現在繼續建立專案，如果還原套件，針對單一專案失敗- [1169年](https://github.com/NuGet/Home/issues/1169)</span><span class="sxs-lookup"><span data-stu-id="f4256-149">Now continuing to build projects if restoring packages for a single project fails - [1169](https://github.com/NuGet/Home/issues/1169)</span></span>
* <span data-ttu-id="f4256-150">套件安裝至專案的方案中的另一個專案相依於強制方案重建- [981](https://github.com/NuGet/Home/issues/981)</span><span class="sxs-lookup"><span data-stu-id="f4256-150">Installing a package into a project that is depended on by another project in the solution forces a solution rebuild - [981](https://github.com/NuGet/Home/issues/981)</span></span>
* <span data-ttu-id="f4256-151">已更正失敗的封裝會安裝正確的回復變更的專案- [1265年](https://github.com/NuGet/Home/issues/1265)</span><span class="sxs-lookup"><span data-stu-id="f4256-151">Corrected failed package installs to properly rollback changes to a project - [1265](https://github.com/NuGet/Home/issues/1265)</span></span>
* <span data-ttu-id="f4256-152">已更正不小心移除`developmentDependency`中的封裝屬性`packages.config`  -  [1263年](https://github.com/NuGet/Home/issues/1263)</span><span class="sxs-lookup"><span data-stu-id="f4256-152">Corrected inadvertent removal of the `developmentDependency` attribute on a package in `packages.config` - [1263](https://github.com/NuGet/Home/issues/1263)</span></span>
* <span data-ttu-id="f4256-153">呼叫`install.ps1`現在有適當`$package.AssemblyReferences`物件傳遞為[1245年](https://github.com/NuGet/Home/issues/1245)</span><span class="sxs-lookup"><span data-stu-id="f4256-153">Calls to `install.ps1` now have a proper `$package.AssemblyReferences` object passed - [1245](https://github.com/NuGet/Home/issues/1245)</span></span>
* <span data-ttu-id="f4256-154">不會再導致解除安裝的 UWP 專案中的封裝專案時處於不正常的狀態- [1128年](https://github.com/NuGet/Home/issues/1128)</span><span class="sxs-lookup"><span data-stu-id="f4256-154">No longer preventing uninstalls of packages in UWP projects while the project is in a bad state - [1128](https://github.com/NuGet/Home/issues/1128)</span></span>
* <span data-ttu-id="f4256-155">解決方案包含各種`packages.config`並`project.json`而不需要第二個現在正確建置的專案建立作業- [1122年](https://github.com/NuGet/Home/issues/1122)</span><span class="sxs-lookup"><span data-stu-id="f4256-155">Solutions containing a mix of `packages.config` and `project.json` projects are now properly built without requiring a second build operation - [1122](https://github.com/NuGet/Home/issues/1122)</span></span>
* <span data-ttu-id="f4256-156">適當地尋找 app.config 檔案，如果其為連結，或位於不同的資料夾- [1111年](https://github.com/NuGet/Home/issues/1111)， [894](https://github.com/NuGet/Home/issues/894)</span><span class="sxs-lookup"><span data-stu-id="f4256-156">Properly locating app.config files if they are linked or located in a different folder - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)</span></span>
* <span data-ttu-id="f4256-157">UWP 專案現在可以安裝未列出的套件- [1109年](https://github.com/NuGet/Home/issues/1109)</span><span class="sxs-lookup"><span data-stu-id="f4256-157">UWP projects can now install unlisted packages - [1109](https://github.com/NuGet/Home/issues/1109)</span></span>
* <span data-ttu-id="f4256-158">套件還原不允許使用時的方案不是處於儲存狀態- [1081年](https://github.com/NuGet/Home/issues/1081)</span><span class="sxs-lookup"><span data-stu-id="f4256-158">Package restore is now allowed while a solution is not in a saved state - [1081](https://github.com/NuGet/Home/issues/1081)</span></span>

<span data-ttu-id="f4256-159">處理已更正檔案的組態更新：</span><span class="sxs-lookup"><span data-stu-id="f4256-159">Handling updates to configuration files were corrected:</span></span>

* <span data-ttu-id="f4256-160">從後續建置的套件不會再移除目標檔案傳遞`project.json`受管理的專案- [1288年](https://github.com/NuGet/Home/issues/1288)</span><span class="sxs-lookup"><span data-stu-id="f4256-160">No longer removing a targets file delivered from a package on subsequent builds of a `project.json` managed project - [1288](https://github.com/NuGet/Home/issues/1288)</span></span>
* <span data-ttu-id="f4256-161">無法再修改 ASP.NET 5 方案建置-期間的 Nuget.Config 檔案[1201年](https://github.com/NuGet/Home/issues/1201)</span><span class="sxs-lookup"><span data-stu-id="f4256-161">No longer modifying Nuget.Config files during ASP.NET 5 solution build - [1201](https://github.com/NuGet/Home/issues/1201)</span></span>
* <span data-ttu-id="f4256-162">不會再變更套件的更新-期間允許版本條件約束[1130年](https://github.com/NuGet/Home/issues/1130)</span><span class="sxs-lookup"><span data-stu-id="f4256-162">No longer changing allowed versions constraint during package update - [1130](https://github.com/NuGet/Home/issues/1130)</span></span>
* <span data-ttu-id="f4256-163">鎖定檔案現在保持鎖定狀態期間組建- [1127年](https://github.com/NuGet/Home/issues/1127)</span><span class="sxs-lookup"><span data-stu-id="f4256-163">Lock files now remain locked during build - [1127](https://github.com/NuGet/Home/issues/1127)</span></span>
* <span data-ttu-id="f4256-164">現在修改`packages.config`並不重寫期間更新- [585](https://github.com/NuGet/Home/issues/585)</span><span class="sxs-lookup"><span data-stu-id="f4256-164">Now modifying `packages.config` and not rewriting it during updates - [585](https://github.com/NuGet/Home/issues/585)</span></span>

<span data-ttu-id="f4256-165">TFS 原始檔控制與互動都已獲得改善：</span><span class="sxs-lookup"><span data-stu-id="f4256-165">Interactions with TFS source control are improved:</span></span>

* <span data-ttu-id="f4256-166">不會再失敗的繫結至 TFS-的套件會安裝[1164年](https://github.com/NuGet/Home/issues/1164)， [980](https://github.com/NuGet/Home/issues/980)</span><span class="sxs-lookup"><span data-stu-id="f4256-166">No longer failing installs for packages that are bound to TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)</span></span>
* <span data-ttu-id="f4256-167">已更正的 NuGet 使用者介面，以允許 TFS 2013 整合- [1071年](https://github.com/NuGet/Home/issues/1071)</span><span class="sxs-lookup"><span data-stu-id="f4256-167">Corrected NuGet user interface to allow TFS 2013 integration - [1071](https://github.com/NuGet/Home/issues/1071)</span></span>
* <span data-ttu-id="f4256-168">已更正正確來自的 packages 資料夾-還原的套件參考[1004年](https://github.com/NuGet/Home/issues/1004)</span><span class="sxs-lookup"><span data-stu-id="f4256-168">Corrected references to packages restored to properly come from a packages folder - [1004](https://github.com/NuGet/Home/issues/1004)</span></span>

<span data-ttu-id="f4256-169">最後，我們也改進了這些項目：</span><span class="sxs-lookup"><span data-stu-id="f4256-169">Finally, we also improved these items:</span></span>

* <span data-ttu-id="f4256-170">記錄檔訊息詳細程度降低`project.json`managed 專案- [1163年](https://github.com/NuGet/Home/issues/1163)</span><span class="sxs-lookup"><span data-stu-id="f4256-170">Verbosity of log messages reduced for `project.json` managed projects - [1163](https://github.com/NuGet/Home/issues/1163)</span></span>
* <span data-ttu-id="f4256-171">現在正確顯示使用者介面-中的 安裝的封裝的版本[1061年](https://github.com/NuGet/Home/issues/1061)</span><span class="sxs-lookup"><span data-stu-id="f4256-171">Now properly displaying the installed version of a package in the user interface - [1061](https://github.com/NuGet/Home/issues/1061)</span></span>
* <span data-ttu-id="f4256-172">現在他們 nuspec 中指定的相依性範圍的套件有穩定套件版本-安裝這些相依性的發行前版本[1304年](https://github.com/NuGet/Home/issues/1304)</span><span class="sxs-lookup"><span data-stu-id="f4256-172">Packages with dependency ranges specified in their nuspec now have pre-release versions of those dependencies installed for a stable package version - [1304](https://github.com/NuGet/Home/issues/1304)</span></span>

<span data-ttu-id="f4256-173">Visual Studio 擴充功能可以找到 NuGet GitHub 中的已解決問題的完整清單[3.2 里程碑](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span><span class="sxs-lookup"><span data-stu-id="f4256-173">A complete list of issues addressed for the Visual Studio extension can be found in the NuGet GitHub [3.2 milestone](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span></span>

## <a name="known-issues"></a><span data-ttu-id="f4256-174">已知問題</span><span class="sxs-lookup"><span data-stu-id="f4256-174">Known Issues</span></span>

<span data-ttu-id="f4256-175">我們繼續追蹤，請參閱我們 GitHub 問題清單上的問題： [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="f4256-175">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>