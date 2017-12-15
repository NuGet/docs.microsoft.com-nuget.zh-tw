---
title: "NuGet 2.7 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba2edaad-4795-47a0-a572-d0e1716bd540
description: "版本資訊包含已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 2.7。"
keywords: "NuGet 2.7 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 502cb5e68f905e9ad8f4003bb0690d3e676f6bb7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-27-release-notes"></a><span data-ttu-id="d042c-104">NuGet 2.7 版本資訊</span><span class="sxs-lookup"><span data-stu-id="d042c-104">NuGet 2.7 Release Notes</span></span>

<span data-ttu-id="d042c-105">[如需 WebMatrix 版本資訊的 NuGet 2.6.1](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 版本資訊](../release-notes/nuget-2.7.1.md)</span><span class="sxs-lookup"><span data-stu-id="d042c-105">[NuGet 2.6.1 for WebMatrix Release Notes](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md)</span></span>

<span data-ttu-id="d042c-106">NuGet 2.7 已於 2013 年 8 月 22 日發行。</span><span class="sxs-lookup"><span data-stu-id="d042c-106">NuGet 2.7 was released on August 22, 2013.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="d042c-107">謝誌</span><span class="sxs-lookup"><span data-stu-id="d042c-107">Acknowledgements</span></span>

<span data-ttu-id="d042c-108">我們想要感謝下列外部 NuGet 2.7 其顯著比重的參與者：</span><span class="sxs-lookup"><span data-stu-id="d042c-108">We would like to thank the following external contributors for their significant contributions to NuGet 2.7:</span></span>

1. <span data-ttu-id="d042c-109">[Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))</span><span class="sxs-lookup"><span data-stu-id="d042c-109">[Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))</span></span>
    - <span data-ttu-id="d042c-110">當詳細列出封裝和詳細資訊會顯示授權 url。</span><span class="sxs-lookup"><span data-stu-id="d042c-110">Show License url when listing packages and verbosity is detailed.</span></span>
1. <span data-ttu-id="d042c-111">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="d042c-111">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="d042c-112">[# 1956年](http://nuget.codeplex.com/workitem/1956)-新增要 developmentDependency 屬性`packages.config`並使其只包含執行階段封裝組件命令中使用它</span><span class="sxs-lookup"><span data-stu-id="d042c-112">[#1956](http://nuget.codeplex.com/workitem/1956) - Add developmentDependency attribute to `packages.config` and use it in pack command to only include runtime packages</span></span>
1. <span data-ttu-id="d042c-113">[Rafael-salas.com Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))</span><span class="sxs-lookup"><span data-stu-id="d042c-113">[Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))</span></span>
    - <span data-ttu-id="d042c-114">避免重複 nuget.exe 套件命令的屬性索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d042c-114">Avoid duplicate Properties key in nuget.exe pack command.</span></span>
1. <span data-ttu-id="d042c-115">[Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))</span><span class="sxs-lookup"><span data-stu-id="d042c-115">[Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))</span></span>
    - <span data-ttu-id="d042c-116">[# 2610年](http://nuget.codeplex.com/workitem/2610)-machine 快取大小增加到 200。</span><span class="sxs-lookup"><span data-stu-id="d042c-116">[#2610](http://nuget.codeplex.com/workitem/2610) - Increase machine cache size to 200.</span></span>
1. <span data-ttu-id="d042c-117">[Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))</span><span class="sxs-lookup"><span data-stu-id="d042c-117">[Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))</span></span>
    - <span data-ttu-id="d042c-118">[#3217](http://nuget.codeplex.com/workitem/3217) -修正 NuGet 對話方塊顯示在 [錯誤] 索引標籤中的更新</span><span class="sxs-lookup"><span data-stu-id="d042c-118">[#3217](http://nuget.codeplex.com/workitem/3217) - Fix NuGet dialog showing updates in the wrong tab</span></span>
    - <span data-ttu-id="d042c-119">修正 Project.TargetFramework 可以是 null ProjectManager 中</span><span class="sxs-lookup"><span data-stu-id="d042c-119">Fix Project.TargetFramework can be null in ProjectManager</span></span>
    - <span data-ttu-id="d042c-120">[#3248](http://nuget.codeplex.com/workitem/3248) -修正 SharedPackageRepository FindPackage/FindPackagesById 上不存在 packageId，將會失敗</span><span class="sxs-lookup"><span data-stu-id="d042c-120">[#3248](http://nuget.codeplex.com/workitem/3248) - Fix SharedPackageRepository FindPackage/FindPackagesById will fail on non-existent packageId</span></span>
1. <span data-ttu-id="d042c-121">[Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))</span><span class="sxs-lookup"><span data-stu-id="d042c-121">[Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))</span></span>
    - <span data-ttu-id="d042c-122">[#3234](http://nuget.codeplex.com/workitem/3234) -啟用遊牧專案支援</span><span class="sxs-lookup"><span data-stu-id="d042c-122">[#3234](http://nuget.codeplex.com/workitem/3234) - Enable support for Nomad project</span></span>
1. <span data-ttu-id="d042c-123">[Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))</span><span class="sxs-lookup"><span data-stu-id="d042c-123">[Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))</span></span>
    - <span data-ttu-id="d042c-124">[#3252](http://nuget.codeplex.com/workitem/3252) -檔案不存在時，修正發送命令失敗，並結束程式碼 0。</span><span class="sxs-lookup"><span data-stu-id="d042c-124">[#3252](http://nuget.codeplex.com/workitem/3252) - Fix push command fails with exit code 0 when file doesn't exist.</span></span>
1. [<span data-ttu-id="d042c-125">Martin Veselý</span><span class="sxs-lookup"><span data-stu-id="d042c-125">Martin Veselý</span></span>](http://www.codeplex.com/site/users/view/veselkamartin)
    - <span data-ttu-id="d042c-126">[#3226](http://nuget.codeplex.com/workitem/3226) -使用專案參考資料庫專案時加入 BindingRedirect 命令修正 bug。</span><span class="sxs-lookup"><span data-stu-id="d042c-126">[#3226](http://nuget.codeplex.com/workitem/3226) - Fix bug with Add-BindingRedirect command when a project references a database project.</span></span>
1. <span data-ttu-id="d042c-127">[Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="d042c-127">[Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="d042c-128">[# 2891年](http://nuget.codeplex.com/workitem/2891)-修正 bug 的 nuget.pack 不正確剖析 'exclude' 屬性中的萬用字元。</span><span class="sxs-lookup"><span data-stu-id="d042c-128">[#2891](http://nuget.codeplex.com/workitem/2891) - Fix bug of nuget.pack parsing wildcard in the 'exclude' attribute incorrectly.</span></span>
1. <span data-ttu-id="d042c-129">[Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))</span><span class="sxs-lookup"><span data-stu-id="d042c-129">[Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))</span></span>
    - <span data-ttu-id="d042c-130">[#3307](http://nuget.codeplex.com/workitem/3307) -修正 bug`NuGet.targets`不 $(Platform) 時傳遞至 nuget.exe 還原封裝。</span><span class="sxs-lookup"><span data-stu-id="d042c-130">[#3307](http://nuget.codeplex.com/workitem/3307) - Fix bug `NuGet.targets` does not pass $(Platform) to nuget.exe when restoring packages.</span></span>
1. [<span data-ttu-id="d042c-131">Brian Federici</span><span class="sxs-lookup"><span data-stu-id="d042c-131">Brian Federici</span></span>](http://www.codeplex.com/site/users/view/benerdin)
    - <span data-ttu-id="d042c-132">[#3294](http://nuget.codeplex.com/workitem/3294) -nuget.exe 套件 命令會讓加入具有相同名稱但不同大小寫，最後導致 「 項目已經存在 」 的例外狀況的檔案中的修正 bug。</span><span class="sxs-lookup"><span data-stu-id="d042c-132">[#3294](http://nuget.codeplex.com/workitem/3294) - Fix bug in nuget.exe package command which would allow adding files with the same name but different casing, eventually causing "Item already exists" exception.</span></span>
1. <span data-ttu-id="d042c-133">[奧 Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))</span><span class="sxs-lookup"><span data-stu-id="d042c-133">[Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))</span></span>
    - <span data-ttu-id="d042c-134">[# 2990年](http://nuget.codeplex.com/workitem/2990)-新增版本 屬性，NetPortableProfile 類別。</span><span class="sxs-lookup"><span data-stu-id="d042c-134">[#2990](http://nuget.codeplex.com/workitem/2990) - Add Version property to NetPortableProfile class.</span></span>
1. [<span data-ttu-id="d042c-135">David Simner</span><span class="sxs-lookup"><span data-stu-id="d042c-135">David Simner</span></span>](https://www.codeplex.com/site/users/view/DavidSimner)
    - <span data-ttu-id="d042c-136">[#3460](https://nuget.codeplex.com/workitem/3460) -如果修正 bug NullReferenceException requireApiKey = true，但標頭 X-NUGET-APIKEY 不存在</span><span class="sxs-lookup"><span data-stu-id="d042c-136">[#3460](https://nuget.codeplex.com/workitem/3460) - Fix bug NullReferenceException if requireApiKey = true, but the header X-NUGET-APIKEY isn't present</span></span>
1. <span data-ttu-id="d042c-137">[Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))</span><span class="sxs-lookup"><span data-stu-id="d042c-137">[Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))</span></span>
    - <span data-ttu-id="d042c-138">[#3278](https://nuget.codeplex.com/workitem/3278) -修正 NuGet.Build 目標檔案，讓它 MonoDevelop 上正常運作</span><span class="sxs-lookup"><span data-stu-id="d042c-138">[#3278](https://nuget.codeplex.com/workitem/3278) - Fixes NuGet.Build targets file to so that it works correctly on MonoDevelop</span></span>
1. <span data-ttu-id="d042c-139">[Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))</span><span class="sxs-lookup"><span data-stu-id="d042c-139">[Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))</span></span>
    - <span data-ttu-id="d042c-140">還原命令的效能改善藉由增加平行化作業</span><span class="sxs-lookup"><span data-stu-id="d042c-140">Improve Restore command performance by increasing parallelization</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="d042c-141">在版本中值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="d042c-141">Notable features in the release</span></span>

### <a name="package-restore-by-default-with-implicit-consent"></a><span data-ttu-id="d042c-142">封裝還原預設 （與隱含地同意）</span><span class="sxs-lookup"><span data-stu-id="d042c-142">Package Restore by Default (with implicit consent)</span></span>

<span data-ttu-id="d042c-143">NuGet 2.7 導入了新的封裝還原，方法，也能夠克服大障礙： 封裝還原同意現在預設為開啟 ！</span><span class="sxs-lookup"><span data-stu-id="d042c-143">NuGet 2.7 introduces a new approach to package restore, and also overcomes a major hurdle: Package restore consent is now on by default!</span></span> <span data-ttu-id="d042c-144">新的方法和隱含地同意的組合會大幅簡化封裝還原實例。</span><span class="sxs-lookup"><span data-stu-id="d042c-144">The combination of the new approach and the implicit consent will drastically simplify package restore scenarios.</span></span>

#### <a name="implicit-consent"></a><span data-ttu-id="d042c-145">隱含地同意</span><span class="sxs-lookup"><span data-stu-id="d042c-145">Implicit Consent</span></span>

<span data-ttu-id="d042c-146">與 NuGet 版本 2.0、 2.1、 2.2、 2.5 和 2.6，明確地允許 NuGet 下載遺漏的封裝時所需的使用者來建立。</span><span class="sxs-lookup"><span data-stu-id="d042c-146">With NuGet versions 2.0, 2.1, 2.2, 2.5, and 2.6, users needed to explicitly allow NuGet to download missing packages during build.</span></span> <span data-ttu-id="d042c-147">如果不在此同意已明確指定為，則必須啟用封裝還原的方案會無法建立，直到使用者已獲得同意。</span><span class="sxs-lookup"><span data-stu-id="d042c-147">If this consent had not been explicitly given, then solutions that had enabled package restore would fail to build until the user had granted consent.</span></span>

<span data-ttu-id="d042c-148">從開始 NuGet 2.7，封裝還原同意預設為 ON 同時允許使用者明確*退出*的封裝還原，如有需要，在 Visual Studio 中的 NuGet 的設定中使用核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d042c-148">Starting with NuGet 2.7, package restore consent is ON by default while allowing users to explicitly *opt out* of package restore if desired, using the checkbox in NuGet's settings in Visual Studio.</span></span> <span data-ttu-id="d042c-149">隱含地同意此變更會影響 NuGet 在下列環境：</span><span class="sxs-lookup"><span data-stu-id="d042c-149">This change for implicit consent affects NuGet in the following environments:</span></span>

* <span data-ttu-id="d042c-150">Visual Studio 2013 Preview</span><span class="sxs-lookup"><span data-stu-id="d042c-150">Visual Studio 2013 Preview</span></span>
* <span data-ttu-id="d042c-151">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d042c-151">Visual Studio 2012</span></span>
* <span data-ttu-id="d042c-152">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="d042c-152">Visual Studio 2010</span></span>
* <span data-ttu-id="d042c-153">nuget.exe 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="d042c-153">nuget.exe Command-Line Utility</span></span>

#### <a name="automatic-package-restore-in-visual-studio"></a><span data-ttu-id="d042c-154">在 Visual Studio 中的自動封裝還原</span><span class="sxs-lookup"><span data-stu-id="d042c-154">Automatic Package Restore in Visual Studio</span></span>

<span data-ttu-id="d042c-155">NuGet 2.7 從開始，NuGet 會自動下載缺少的套件 Visual Studio 中，在建置期間即使封裝還原尚未明確啟用方案。</span><span class="sxs-lookup"><span data-stu-id="d042c-155">Starting with NuGet 2.7, NuGet will automatically download missing packages during build in Visual Studio, even if package restore hasn't been explicitly enabled for the solution.</span></span> <span data-ttu-id="d042c-156">這個自動封裝還原，發生在 Visual Studio 中，當您建置專案或方案，但是叫用 MSBuild 之前。</span><span class="sxs-lookup"><span data-stu-id="d042c-156">This Automatic Package Restore happens in Visual Studio when you build a project or the solution, but before MSBuild is invoked.</span></span> <span data-ttu-id="d042c-157">這會產生幾個重要的優點：</span><span class="sxs-lookup"><span data-stu-id="d042c-157">This yields a few significant benefits:</span></span>

1. <span data-ttu-id="d042c-158">不再需要在您的方案使用的 「 啟用 NuGet 封裝還原 」 的筆勢</span><span class="sxs-lookup"><span data-stu-id="d042c-158">No further need to use the "Enable NuGet Package Restore" gesture on your solution</span></span>
1. <span data-ttu-id="d042c-159">專案不需要修改，並 NuGet 將不會變更您的專案，確定已啟用封裝還原</span><span class="sxs-lookup"><span data-stu-id="d042c-159">Projects don't need to be modified, and NuGet won't make changes to your project to ensure package restore is enabled</span></span>
1. <span data-ttu-id="d042c-160">所有的 NuGet 封裝，包括包含 props/目標檔案的 MSBuild 匯入將會還原*之前*MSBuild 會叫用，確保在建置期間，正確辨識這些 props/目標</span><span class="sxs-lookup"><span data-stu-id="d042c-160">All NuGet packages, including those that included MSBuild imports for props/targets files, will be restored *before* MSBuild is invoked, ensuring those props/targets are properly recognized during the build</span></span>

<span data-ttu-id="d042c-161">若要在 Visual Studio 中，使用自動封裝還原，您只需要採取動作 （中） 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="d042c-161">In order to use Automatic Package Restore in Visual Studio, you only need to take one (in)action:</span></span>

1. <span data-ttu-id="d042c-162">請勿核取 您`packages`資料夾</span><span class="sxs-lookup"><span data-stu-id="d042c-162">Don't check in your `packages` folder</span></span>

<span data-ttu-id="d042c-163">有幾種方式可以省略您`packages`從原始檔控制的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d042c-163">There are several ways to omit your `packages` folder from source control.</span></span> <span data-ttu-id="d042c-164">如需詳細資訊，請參閱[封裝和原始檔控制](../consume-packages/packages-and-source-control.md)主題。</span><span class="sxs-lookup"><span data-stu-id="d042c-164">For more information, see the [Packages and Source Control](../consume-packages/packages-and-source-control.md) topic.</span></span>

<span data-ttu-id="d042c-165">雖然所有使用者都是隱含選擇加入自動封裝還原同意，您也可以輕鬆地退出透過 Visual Studio 中 套件管理員設定。</span><span class="sxs-lookup"><span data-stu-id="d042c-165">While all users are implicitly opted into Automatic Package Restore consent, you can easily opt out through the Package Manager settings in Visual Studio.</span></span>

![封裝管理員設定](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a><span data-ttu-id="d042c-167">簡化的封裝還原，從命令列</span><span class="sxs-lookup"><span data-stu-id="d042c-167">Simplified Package Restore from the Command-Line</span></span>

<span data-ttu-id="d042c-168">NuGet 2.7 導入了 nuget.exe 的新功能：`nuget.exe restore`</span><span class="sxs-lookup"><span data-stu-id="d042c-168">NuGet 2.7 introduces a new feature for nuget.exe: `nuget.exe restore`</span></span>

<span data-ttu-id="d042c-169">這個新的還原命令可讓您輕鬆地還原所有的套件在方案中使用單一命令中，接受的解決方案檔案或資料夾做為引數。</span><span class="sxs-lookup"><span data-stu-id="d042c-169">This new Restore command allows you to easily restore all packages for a solution with a single command, by accepting a solution file or folder as an argument.</span></span> <span data-ttu-id="d042c-170">此外，目前的資料夾中僅有單一的解決方案時，就會隱含該引數。</span><span class="sxs-lookup"><span data-stu-id="d042c-170">Furthermore, that argument is implied when there's only a single solution in the current folder.</span></span> <span data-ttu-id="d042c-171">這表示從包含單一方案檔 (MySolution.sln) 的資料夾的所有下列都工作：</span><span class="sxs-lookup"><span data-stu-id="d042c-171">That means the following all work from a folder that contains a single solution file (MySolution.sln):</span></span>

1. <span data-ttu-id="d042c-172">nuget.exe 還原 MySolution.sln</span><span class="sxs-lookup"><span data-stu-id="d042c-172">nuget.exe restore MySolution.sln</span></span>
1. <span data-ttu-id="d042c-173">nuget.exe 還原。</span><span class="sxs-lookup"><span data-stu-id="d042c-173">nuget.exe restore .</span></span>
1. <span data-ttu-id="d042c-174">nuget.exe 還原</span><span class="sxs-lookup"><span data-stu-id="d042c-174">nuget.exe restore</span></span>

<span data-ttu-id="d042c-175">還原命令會開啟方案檔，並尋找方案中的所有專案。</span><span class="sxs-lookup"><span data-stu-id="d042c-175">The Restore command will open the solution file and find all projects within the solution.</span></span> <span data-ttu-id="d042c-176">它會從該處找到`packages.config`針對每個專案和封裝的所有找到的還原的檔案。</span><span class="sxs-lookup"><span data-stu-id="d042c-176">From there, it will find the `packages.config` files for each of the projects and restore all of the packages found.</span></span> <span data-ttu-id="d042c-177">它也會還原方案層級中找不到封裝`.nuget\packages.config`檔案。</span><span class="sxs-lookup"><span data-stu-id="d042c-177">It also restores solution-level packages found in the `.nuget\packages.config` file.</span></span> <span data-ttu-id="d042c-178">可以找到新的 Restore 命令的詳細資訊，在[命令列參照](../tools/cli-ref-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="d042c-178">More information about the new Restore command can be found in the [Command-Line Reference](../tools/cli-ref-restore.md).</span></span>

#### <a name="the-new-package-restore-workflow"></a><span data-ttu-id="d042c-179">新的封裝還原工作流程</span><span class="sxs-lookup"><span data-stu-id="d042c-179">The New Package Restore Workflow</span></span>

<span data-ttu-id="d042c-180">很高興有關這些變更封裝還原，因為它導入了新的工作流程。</span><span class="sxs-lookup"><span data-stu-id="d042c-180">We are excited about these changes to Package Restore, as it introduces a new workflow.</span></span> <span data-ttu-id="d042c-181">如果您想要省略您從原始檔控制的封裝。 您只需不認可`packages`資料夾。</span><span class="sxs-lookup"><span data-stu-id="d042c-181">If you want to omit your packages from source control you simply don't commit the `packages` folder.</span></span> <span data-ttu-id="d042c-182">Visual Studio 使用者開啟並建置此方案將會看見自動還原封裝。</span><span class="sxs-lookup"><span data-stu-id="d042c-182">Visual Studio users who open and build the solution will see the packages automatically restored.</span></span> <span data-ttu-id="d042c-183">命令列組建，直接叫用`nuget.exe restore`叫用之前`msbuild`。</span><span class="sxs-lookup"><span data-stu-id="d042c-183">For command-line builds, simply invoke `nuget.exe restore` before invoking `msbuild`.</span></span> <span data-ttu-id="d042c-184">您將不再需要使用 「 啟用 NuGet 封裝還原 」 的筆勢，在您的方案，請記得，我們不再需要修改您要更改組建的專案。</span><span class="sxs-lookup"><span data-stu-id="d042c-184">You'll no longer need to remember to use the "Enable NuGet Package Restore" gesture on your solution, and we'll no longer need to modify your projects to alter the build.</span></span> <span data-ttu-id="d042c-185">這也會產生包含 MSBuild 匯入，特別是針對匯入透過 NuGet 的新功能加入封裝以改良過的體驗和[自動匯入 props/目標檔案](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files)\build 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="d042c-185">And this also yields a much improved experience for packages that include MSBuild imports, especially for imports added through NuGet's recent feature for [automatically importing props/targets files](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) from the \build folder.</span></span>

<span data-ttu-id="d042c-186">除了我們已經完成自己的工作，我們也正在使用一些重要的夥伴，來補足這種新方法。我們沒有具體的時間軸的其中任何棒的是，但每個夥伴為高興，因為我們新的方法。</span><span class="sxs-lookup"><span data-stu-id="d042c-186">In addition to the work we've done ourselves, we're also working with some important partners to round this new approach out. We don't have concrete timelines for any of these yet, but each partner is as excited as we are about the new approach.</span></span>

* <span data-ttu-id="d042c-187">Team Foundation Service-他們正在處理整合到呼叫`nuget.exe restore`到預設建置案例。</span><span class="sxs-lookup"><span data-stu-id="d042c-187">Team Foundation Service - They are working to integrate the call to `nuget.exe restore` into the default build scenarios.</span></span>
* <span data-ttu-id="d042c-188">Windows Azure Web Sites-他們正在處理可讓您將您的專案推送至 Azure，並讓`nuget.exe restore`建置您的網站之前呼叫。</span><span class="sxs-lookup"><span data-stu-id="d042c-188">Windows Azure Web Sites - They are working to allow you to push your project to Azure and have `nuget.exe restore` called before your web site is built.</span></span>
* <span data-ttu-id="d042c-189">TeamCity-它們會更新其 NuGet 安裝程式的外掛程式 TeamCity 8.x</span><span class="sxs-lookup"><span data-stu-id="d042c-189">TeamCity - They are updating their NuGet Installer plugin for TeamCity 8.x</span></span>
* <span data-ttu-id="d042c-190">AppHarbor-他們正在處理可讓您以 AppHarbor 推送您的儲存機制，並讓`nuget.exe restore`建置方案之前呼叫。</span><span class="sxs-lookup"><span data-stu-id="d042c-190">AppHarbor - They are working to allow you to push your repo to AppHarbor and have `nuget.exe restore` called before your solution is build.</span></span>

<span data-ttu-id="d042c-191">與每一個上述協力電腦，就可以使用他們自己的 nuget.exe 的複本，您不需要執行 nuget.exe 方案中。</span><span class="sxs-lookup"><span data-stu-id="d042c-191">With each of the partners above, they would use their own copy of nuget.exe and you would not need to carry nuget.exe in your solution.</span></span>

#### <a name="known-issues"></a><span data-ttu-id="d042c-192">已知問題</span><span class="sxs-lookup"><span data-stu-id="d042c-192">Known Issues</span></span>

<span data-ttu-id="d042c-193">有一些 nuget.exe 還原初始 2.7 版中，兩個已知的問題，但它們在 9/6/2013 的更新與已修正[NuGet.CommandLine 封裝](http://www.nuget.org/packages/NuGet.CommandLine/)。</span><span class="sxs-lookup"><span data-stu-id="d042c-193">There were two known issues with nuget.exe restore with the initial 2.7 release, but they were fixed on 9/6/2013 with an update to the [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/).</span></span>  <span data-ttu-id="d042c-194">此更新也會提供在[NuGet 2.7 下載頁面](https://nuget.codeplex.com/releases/view/107605)CodePlex 上。</span><span class="sxs-lookup"><span data-stu-id="d042c-194">This update is also available on the [NuGet 2.7 download page](https://nuget.codeplex.com/releases/view/107605) on CodePlex.</span></span>  <span data-ttu-id="d042c-195">執行`nuget.exe update -self`會更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="d042c-195">Running `nuget.exe update -self` will update to the latest release.</span></span>

<span data-ttu-id="d042c-196">固定所示：</span><span class="sxs-lookup"><span data-stu-id="d042c-196">The fixed were:</span></span>

1. [<span data-ttu-id="d042c-197">新的封裝還原不適用於的 Mono 時使用 SLN 檔案</span><span class="sxs-lookup"><span data-stu-id="d042c-197">New package restore doesn't work on Mono when using SLN file</span></span>](https://nuget.codeplex.com/workitem/3596)
1. [<span data-ttu-id="d042c-198">新的封裝還原不適合用於 Wix 專案</span><span class="sxs-lookup"><span data-stu-id="d042c-198">New package restore doesn't work with Wix projects</span></span>](https://nuget.codeplex.com/workitem/3598)

<span data-ttu-id="d042c-199">另外還有新的封裝還原工作流程的已知的問題，[自動封裝還原不適用於專案的方案資料夾下](https://nuget.codeplex.com/workitem/3625)。</span><span class="sxs-lookup"><span data-stu-id="d042c-199">There is also a known issue with the new package restore workflow whereby [Automatic Package Restore does not work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625).</span></span> <span data-ttu-id="d042c-200">NuGet 2.7.1 中已修正此問題。</span><span class="sxs-lookup"><span data-stu-id="d042c-200">This issue was fixed in NuGet 2.7.1.</span></span>

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a><span data-ttu-id="d042c-201">專案重定目標 」 和 「 升級建置錯誤/警告</span><span class="sxs-lookup"><span data-stu-id="d042c-201">Project Retargeting and Upgrade Build Errors/Warnings</span></span>

<span data-ttu-id="d042c-202">多次之後重定目標或升級您的專案，您發現部分 NuGet 封裝不正常運作。</span><span class="sxs-lookup"><span data-stu-id="d042c-202">Many times after retargeting or upgrading your project, you find that some NuGet packages aren't functioning properly.</span></span> <span data-ttu-id="d042c-203">不幸的是，沒有這個指示，則沒有任何指引，如何處理它。</span><span class="sxs-lookup"><span data-stu-id="d042c-203">Unfortunately, there is no indication of this and then there's no guidance on how to address it.</span></span> <span data-ttu-id="d042c-204">NuGet 2.7，我們現在使用某些 Visual Studio 事件來辨識重定目標或升級的方式會影響安裝的 NuGet 套件中的專案時。</span><span class="sxs-lookup"><span data-stu-id="d042c-204">With NuGet 2.7, we now use some Visual Studio events to recognize when you've retargeted or upgraded your project in a way that affects your installed NuGet packages.</span></span>

<span data-ttu-id="d042c-205">如果我們偵測到任何封裝已受到重定目標或升級，我們將會產生立即建置錯誤，讓您知道。</span><span class="sxs-lookup"><span data-stu-id="d042c-205">If we detect that any of your packages were affected by the retargeting or upgrade, we'll produce immediate build errors to let you know.</span></span> <span data-ttu-id="d042c-206">除了立即的建置錯誤，我們也會保留存`requireReinstallation="true"`加上旗標您`packages.config`檔案 for Visual Studio 中的受影響的重定目標，且每個後續的所有封裝都組建將會引發這些封裝的都建置警告。</span><span class="sxs-lookup"><span data-stu-id="d042c-206">In addition to the immediate build error, we also persist a `requireReinstallation="true"` flag in your `packages.config` file for all packages that were affected by the retargeting, and each subsequent build in Visual Studio will raise build warnings for those packages.</span></span>

<span data-ttu-id="d042c-207">雖然 NuGet 無法採取自動動作，以重新安裝受影響的封裝，我們希望此指示和警告會引導協助您找出當您需要重新安裝套件。</span><span class="sxs-lookup"><span data-stu-id="d042c-207">Although NuGet cannot take automatic action to reinstall affected packages, we hope this indication and warning will guide help you discover when you need to reinstall packages.</span></span> <span data-ttu-id="d042c-208">我們也正在[封裝重新安裝指引文件](../consume-packages/reinstalling-and-updating-packages.md)這些錯誤訊息引導您。</span><span class="sxs-lookup"><span data-stu-id="d042c-208">We are also working on [package reinstallation guidance documentation](../consume-packages/reinstalling-and-updating-packages.md) that these error messages direct you to.</span></span>

### <a name="nuget-configuration-defaults"></a><span data-ttu-id="d042c-209">NuGet 組態預設值</span><span class="sxs-lookup"><span data-stu-id="d042c-209">NuGet Configuration Defaults</span></span>

<span data-ttu-id="d042c-210">許多公司在內部使用 NuGet，但有難引導他們的開發人員，可以使用內部的封裝來源而不是 nuget.org。NuGet 2.7 引進了組態預設值的功能，可讓指定的整部機器的預設值：</span><span class="sxs-lookup"><span data-stu-id="d042c-210">Many companies are using NuGet internally, but have had a hard time guiding their developers to use internal package sources instead of nuget.org. NuGet 2.7 introduces a Configuration Defaults feature that allows machine-wide defaults to be specified for:</span></span>

1. <span data-ttu-id="d042c-211">已啟用的封裝來源</span><span class="sxs-lookup"><span data-stu-id="d042c-211">Enabled package sources</span></span>
1. <span data-ttu-id="d042c-212">已註冊，但是已停用封裝來源</span><span class="sxs-lookup"><span data-stu-id="d042c-212">Registered, but disabled package sources</span></span>
1. <span data-ttu-id="d042c-213">預設 nuget.exe 推送來源</span><span class="sxs-lookup"><span data-stu-id="d042c-213">The default nuget.exe push source</span></span>

<span data-ttu-id="d042c-214">其中每一項現在位於檔案內設定`%ProgramData%\NuGet\NuGetDefaults.Config`。</span><span class="sxs-lookup"><span data-stu-id="d042c-214">Each of these can now be configured within a file located at `%ProgramData%\NuGet\NuGetDefaults.Config`.</span></span> <span data-ttu-id="d042c-215">如果此組態檔指定封裝來源，則不會自動登錄的預設 nuget.org 的封裝來源中的項目和`NuGetDefaults.Config`將改為註冊。</span><span class="sxs-lookup"><span data-stu-id="d042c-215">If this config file specifies package sources, then the default nuget.org package source will not be registered automatically, and the ones in `NuGetDefaults.Config` will be registered instead.</span></span>

<span data-ttu-id="d042c-216">雖然不需要使用這項功能，但我們預期公司部署`NuGetDefaults.Config`檔案所使用的群組原則。</span><span class="sxs-lookup"><span data-stu-id="d042c-216">While not required to use this feature, we expect companies to deploy `NuGetDefaults.Config` files using Group Policy.</span></span>

<span data-ttu-id="d042c-217">*請注意，這項功能將會永遠不會導致從開發人員的 NuGet 設定中移除的封裝來源。這表示如果開發人員已經使用 NuGet 和因此 nuget.org 的封裝來源註冊，將不會移除它建立之後`NuGetDefaults.Config`檔案。*</span><span class="sxs-lookup"><span data-stu-id="d042c-217">*Note that this feature will never cause a package source to be removed from a developer's NuGet settings. That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.*</span></span>

<span data-ttu-id="d042c-218">請參閱[NuGet 組態預設值](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file)如需有關這項功能。</span><span class="sxs-lookup"><span data-stu-id="d042c-218">See [NuGet Configuration Defaults](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) for more information about this feature.</span></span>

### <a name="renaming-the-default-package-source"></a><span data-ttu-id="d042c-219">重新命名的預設封裝來源</span><span class="sxs-lookup"><span data-stu-id="d042c-219">Renaming the Default Package Source</span></span>

<span data-ttu-id="d042c-220">NuGet 一律已註冊預設稱為 「 NuGet 官方封裝來源 」 指向 nuget.org 的封裝來源。該名稱的詳細資訊，它也未指定位置的實際指向。</span><span class="sxs-lookup"><span data-stu-id="d042c-220">NuGet has always registered a default package source called "NuGet official package source" that points to nuget.org. That name was verbose and it also didn't specify where it was actually pointing.</span></span> <span data-ttu-id="d042c-221">若要解決這些兩個問題，我們已重新命名只要"nuget.org 」 在 UI 中此封裝來源。</span><span class="sxs-lookup"><span data-stu-id="d042c-221">To address those two issues, we've renamed this package source to simply "nuget.org" in the UI.</span></span> <span data-ttu-id="d042c-222">封裝來源的 URL 也已變更為包含"www"。</span><span class="sxs-lookup"><span data-stu-id="d042c-222">The URL for the package source was also changed to include the "www."</span></span> <span data-ttu-id="d042c-223">前置詞。</span><span class="sxs-lookup"><span data-stu-id="d042c-223">prefix.</span></span> <span data-ttu-id="d042c-224">使用 NuGet 2.7 之後, 您現有 「 NuGet 官方封裝來源 」 將自動更新 」 nuget.org"做為其名稱和"https://www.nuget.org/api/v2/"做為其 URL。</span><span class="sxs-lookup"><span data-stu-id="d042c-224">After using NuGet 2.7, your existing "NuGet official package source" will automatically be updated to "nuget.org" as its name and "https://www.nuget.org/api/v2/" as its URL.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="d042c-225">效能改善</span><span class="sxs-lookup"><span data-stu-id="d042c-225">Performance Improvements</span></span>

<span data-ttu-id="d042c-226">我們在將會產生較小的記憶體使用量、 較少的磁碟使用量和更快的套件安裝 2.7 進行一些效能改進。</span><span class="sxs-lookup"><span data-stu-id="d042c-226">We made some performance improvement in 2.7 which will yield smaller memory footprint, less disk usage and faster package installation.</span></span> <span data-ttu-id="d042c-227">我們也對 OData 摘要會減少整體裝載更佳的查詢。</span><span class="sxs-lookup"><span data-stu-id="d042c-227">We also made smarter queries to OData-based feeds which will reduce the overall payload.</span></span>

### <a name="new-extensibility-apis"></a><span data-ttu-id="d042c-228">新的擴充性 Api</span><span class="sxs-lookup"><span data-stu-id="d042c-228">New Extensibility APIs</span></span>

<span data-ttu-id="d042c-229">我們加入一些新 Api 至我們的擴充性服務，以填滿遺漏功能的差距，在先前的版本。</span><span class="sxs-lookup"><span data-stu-id="d042c-229">We added some new APIs to our extensibility services to fill the gap of missing functionalities in previous releases.</span></span>

#### <a name="ivspackageinstallerservices"></a><span data-ttu-id="d042c-230">IVsPackageInstallerServices</span><span class="sxs-lookup"><span data-stu-id="d042c-230">IVsPackageInstallerServices</span></span>

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a><span data-ttu-id="d042c-231">IVsPackageInstaller</span><span class="sxs-lookup"><span data-stu-id="d042c-231">IVsPackageInstaller</span></span>

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a><span data-ttu-id="d042c-232">開發階段專用的相依性</span><span class="sxs-lookup"><span data-stu-id="d042c-232">Development-Only Dependencies</span></span>

<span data-ttu-id="d042c-233">這項功能已由造成[Adam Ralph](https://twitter.com/adamralph)並可讓封裝作者以宣告只能用在開發階段的相依性的時間，且不需要的套件相依性。</span><span class="sxs-lookup"><span data-stu-id="d042c-233">This feature was contributed by [Adam Ralph](https://twitter.com/adamralph) and it allows package authors to declare dependencies that were only used at development time and don't require package dependencies.</span></span> <span data-ttu-id="d042c-234">藉由新增`developmentDependency="true"`屬性中的封裝`packages.config`，`nuget.exe pack`將不再包含該封裝做為相依性。</span><span class="sxs-lookup"><span data-stu-id="d042c-234">By adding a `developmentDependency="true"` attribute to a package in `packages.config`, `nuget.exe pack` will no longer include that package as a dependency.</span></span>

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a><span data-ttu-id="d042c-235">移除 Visual Studio 2010 Express 適用於 Windows Phone 的支援</span><span class="sxs-lookup"><span data-stu-id="d042c-235">Removed Support for Visual Studio 2010 Express for Windows Phone</span></span>

<span data-ttu-id="d042c-236">2.7 中新的封裝還原模型是由新的 VSPackage 主要 NuGet VSPackage 的不同實作。</span><span class="sxs-lookup"><span data-stu-id="d042c-236">The new package restore model in 2.7 is implemented by a new VSPackage which is different from the main NuGet VSPackage.</span></span> <span data-ttu-id="d042c-237">因為技術問題，這個新的 VSPackage 正確地在無法運作*Visual Studio 2010 Express for Windows Phone* SKU 為我們與其他共用相同的程式碼基底支援 Visual Studio Sku。</span><span class="sxs-lookup"><span data-stu-id="d042c-237">Due to a technical issue, this new VSPackage doesn't work correctly in the *Visual Studio 2010 Express for Windows Phone* SKU as we share the same code base with other supported Visual Studio SKUs.</span></span> <span data-ttu-id="d042c-238">因此，從 NuGet 2.7 開始，我們會卸除支援*Visual Studio 2010 Express for Windows Phone*來自已發行的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="d042c-238">Therefore, starting with NuGet 2.7, we are dropping support for *Visual Studio 2010 Express for Windows Phone* from the published extension.</span></span> <span data-ttu-id="d042c-239">支援*Visual Studio 2010 Express for Web*仍然包含在發行至 Visual Studio 延伸模組組件庫的主要延伸模組。</span><span class="sxs-lookup"><span data-stu-id="d042c-239">Support for *Visual Studio 2010 Express for Web* is still included in the primary extension published to the Visual Studio Extension Gallery.</span></span>

<span data-ttu-id="d042c-240">因為我們不確定如何許多開發人員仍在使用 NuGet 在該版本/版本的 Visual Studio 中，我們所發佈個別的 Visual Studio 擴充功能，特別是為那些使用者和發佈 CodePlex （而非 Visual Studio 擴充程式庫）.</span><span class="sxs-lookup"><span data-stu-id="d042c-240">Since we are unsure how many developers are still using NuGet in that version/edition of Visual Studio, we are publishing a separate Visual Studio extension specifically for those users and publishing it on CodePlex (rather than the Visual Studio Extension Gallery).</span></span> <span data-ttu-id="d042c-241">我們不打算繼續維持該擴充功能，但如果這會影響您，請讓我們知道藉由在 CodePlex 上提出問題。</span><span class="sxs-lookup"><span data-stu-id="d042c-241">We don't plan to continue to maintain that extension, but if this affects you please let us know by filing an issue on CodePlex.</span></span>

<span data-ttu-id="d042c-242">若要下載 NuGet 封裝管理員 （適用於 Visual Studio 2010 Express for Windows Phone)，請瀏覽[NuGet 2.7 下載](https://nuget.codeplex.com/releases/view/107605)頁面。</span><span class="sxs-lookup"><span data-stu-id="d042c-242">To download the NuGet Package Manager (for Visual Studio 2010 Express for Windows Phone), visit the [NuGet 2.7 Downloads](https://nuget.codeplex.com/releases/view/107605) page.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="d042c-243">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="d042c-243">Bug Fixes</span></span>

<span data-ttu-id="d042c-244">除了這些功能，此版本的 NuGet 也包含許多其他 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="d042c-244">In addition to these features, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="d042c-245">有一些版本中解決的 97 總問題。</span><span class="sxs-lookup"><span data-stu-id="d042c-245">There were 97 total issues addressed in the release.</span></span> <span data-ttu-id="d042c-246">如需完整的工作清單項目固定在 NuGet 2.7，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)。</span><span class="sxs-lookup"><span data-stu-id="d042c-246">For a full list of work items fixed in NuGet 2.7, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).</span></span>
