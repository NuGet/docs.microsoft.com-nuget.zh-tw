---
title: NuGet 2.8 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 2.8 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547455"
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="c1489-103">NuGet 2.8 版本資訊</span><span class="sxs-lookup"><span data-stu-id="c1489-103">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="c1489-104">[NuGet 2.7.2 版本資訊](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 版本資訊](../release-notes/nuget-2.8.1.md)</span><span class="sxs-lookup"><span data-stu-id="c1489-104">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="c1489-105">NuGet 2.8 已於 2014 年 1 月 29 日發行。</span><span class="sxs-lookup"><span data-stu-id="c1489-105">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="c1489-106">謝誌</span><span class="sxs-lookup"><span data-stu-id="c1489-106">Acknowledgements</span></span>

1. <span data-ttu-id="c1489-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span><span class="sxs-lookup"><span data-stu-id="c1489-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="c1489-108">[#3466](https://nuget.codeplex.com/workitem/3466) -當封裝套件，驗證相依性套件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="c1489-108">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
2. <span data-ttu-id="c1489-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span><span class="sxs-lookup"><span data-stu-id="c1489-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="c1489-110">[# 2379年](https://nuget.codeplex.com/workitem/2379)-persistening 摘要認證時，移除 $metadata 後置詞。</span><span class="sxs-lookup"><span data-stu-id="c1489-110">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
3. <span data-ttu-id="c1489-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span><span class="sxs-lookup"><span data-stu-id="c1489-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="c1489-112">[#3538](http://nuget.codeplex.com/workitem/3538) -指定專案檔的 nuget.exe 更新命令的支援。</span><span class="sxs-lookup"><span data-stu-id="c1489-112">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
4. [<span data-ttu-id="c1489-113">Juan Gonzalez</span><span class="sxs-lookup"><span data-stu-id="c1489-113">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="c1489-114">[#3536](http://nuget.codeplex.com/workitem/3536) --IncludeReferencedProjects 與失敗的取代權杖。</span><span class="sxs-lookup"><span data-stu-id="c1489-114">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
5. <span data-ttu-id="c1489-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span><span class="sxs-lookup"><span data-stu-id="c1489-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="c1489-116">[#3677](http://nuget.codeplex.com/workitem/3677) -修正 nuget.push 推送大型封裝時，擲回 OutOfMemoryException。</span><span class="sxs-lookup"><span data-stu-id="c1489-116">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
6. [<span data-ttu-id="c1489-117">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="c1489-117">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="c1489-118">[#3666](http://nuget.codeplex.com/workitem/3666) -專案參考另一個的 CLI/c + + 專案時，修正不正確的目標路徑。</span><span class="sxs-lookup"><span data-stu-id="c1489-118">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
7. <span data-ttu-id="c1489-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="c1489-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="c1489-120">[#3639](https://nuget.codeplex.com/workitem/3639) -允許依預設，做為開發相依性安裝封裝</span><span class="sxs-lookup"><span data-stu-id="c1489-120">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
8. <span data-ttu-id="c1489-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="c1489-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="c1489-122">[#3717](https://nuget.codeplex.com/workitem/3717) -移除隱含升級至最新的修補程式版本</span><span class="sxs-lookup"><span data-stu-id="c1489-122">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
9. [<span data-ttu-id="c1489-123">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="c1489-123">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="c1489-124">數個 bug 修正和改善的 NuGet.Server、 nuget.exe 鏡像命令和其他項目。</span><span class="sxs-lookup"><span data-stu-id="c1489-124">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="c1489-125">這項工作已完成幾個月，Gregory 正確的時機與我們合作，將整合到 2.8 的主要。</span><span class="sxs-lookup"><span data-stu-id="c1489-125">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="c1489-126">修補程式解決相依性</span><span class="sxs-lookup"><span data-stu-id="c1489-126">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="c1489-127">當解析套件相依性，NuGet 已在過去實作選取最低的主要和次要封裝版本符合封裝上的相依性的策略。</span><span class="sxs-lookup"><span data-stu-id="c1489-127">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="c1489-128">不同於主要和次要版本，不過，修補程式版本已一律解決的最高版本。</span><span class="sxs-lookup"><span data-stu-id="c1489-128">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="c1489-129">行為是用意良好，但它會建立決定性具有相依性安裝套件的缺乏。</span><span class="sxs-lookup"><span data-stu-id="c1489-129">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="c1489-130">參考下列範例：</span><span class="sxs-lookup"><span data-stu-id="c1489-130">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="c1489-131">在此範例中，即使 Developer1 和 Developer2 安裝PackageA@1.0.0、 每個結束向上 PackageB 的不同版本。</span><span class="sxs-lookup"><span data-stu-id="c1489-131">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="c1489-132">NuGet 2.8 會變更此預設行為，因此修補程式版本的相依性解析行為會與主要和次要版本的行為一致。</span><span class="sxs-lookup"><span data-stu-id="c1489-132">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="c1489-133">在上述範例中，然後PackageB@1.0.0由於安裝會安裝PackageA@1.0.0，而不論較新的修補程式版本。</span><span class="sxs-lookup"><span data-stu-id="c1489-133">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="c1489-134">-DependencyVersion 參數</span><span class="sxs-lookup"><span data-stu-id="c1489-134">-DependencyVersion Switch</span></span>

<span data-ttu-id="c1489-135">雖然變更 NuGet 2.8_預設_行為解析相依性，它也會加入更精確地控制相依性解析程序-DependencyVersion 參數透過套件管理員主控台中。</span><span class="sxs-lookup"><span data-stu-id="c1489-135">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="c1489-136">參數可讓您解析的相依性，以最低的可能版本 （預設行為）、 最高的可能版本，或最高次要或修補程式版本。</span><span class="sxs-lookup"><span data-stu-id="c1489-136">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="c1489-137">此參數僅適用於安裝套件中的 powershell 命令。</span><span class="sxs-lookup"><span data-stu-id="c1489-137">This switch only works for install-package in the powershell command.</span></span>

![DependencyVersion 參數](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="c1489-139">DependencyVersion 屬性</span><span class="sxs-lookup"><span data-stu-id="c1489-139">DependencyVersion Attribute</span></span>

<span data-ttu-id="c1489-140">除了以上詳述，NuGet 也可讓提供的能力的 Nuget.Config 檔案中設定新的屬性-DependencyVersion 參數定義的預設值為何，如果未指定-DependencyVersion 參數中的引動過程安裝套件。</span><span class="sxs-lookup"><span data-stu-id="c1489-140">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="c1489-141">此值也會遵守任何安裝封裝作業的 [NuGet 套件管理員] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c1489-141">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="c1489-142">若要設定此值，請先 Nuget.Config 檔案中加入以下屬性：</span><span class="sxs-lookup"><span data-stu-id="c1489-142">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="c1489-143">預覽 NuGet 作業，與-whatif</span><span class="sxs-lookup"><span data-stu-id="c1489-143">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="c1489-144">部分 NuGet 套件可以有深入的相依性圖形，而此情況下，它可以在安裝期間會有幫助、 解除安裝或更新作業，先查看 會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="c1489-144">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="c1489-145">NuGet 2.8 會將標準的 PowerShell-whatif 參數新增至安裝套件、 解除安裝套件和更新套件的命令，來啟用視覺化整個 closure 的封裝將會套用命令。</span><span class="sxs-lookup"><span data-stu-id="c1489-145">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="c1489-146">例如，執行`install-package Microsoft.AspNet.WebApi -whatif`在空的 ASP.NET Web 應用程式會產生下列結果。</span><span class="sxs-lookup"><span data-stu-id="c1489-146">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a><span data-ttu-id="c1489-147">降級封裝</span><span class="sxs-lookup"><span data-stu-id="c1489-147">Downgrade Package</span></span>

<span data-ttu-id="c1489-148">不常見安裝套件的發行前版本，以便調查的新功能，但後來回復到最新穩定版本。</span><span class="sxs-lookup"><span data-stu-id="c1489-148">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="c1489-149">NuGet 2.8 以前這會是多重步驟的程序解除安裝發行前版本套件和其相依性，然後安裝 先前的版本。</span><span class="sxs-lookup"><span data-stu-id="c1489-149">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="c1489-150">使用 NuGet 2.8，不過，更新套件現在會回復整個封裝結束 （例如套件的相依性樹狀結構） 到之前的版本。</span><span class="sxs-lookup"><span data-stu-id="c1489-150">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="c1489-151">開發相依性</span><span class="sxs-lookup"><span data-stu-id="c1489-151">Development Dependencies</span></span>

<span data-ttu-id="c1489-152">許多不同類型的功能可能會傳送為 NuGet 套件-包括用來最佳化開發過程的工具。</span><span class="sxs-lookup"><span data-stu-id="c1489-152">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="c1489-153">這些元件，雖然也很有幫助開發新封裝時，不應視為新的封裝相依性更新版本發行時。</span><span class="sxs-lookup"><span data-stu-id="c1489-153">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it's later published.</span></span> <span data-ttu-id="c1489-154">NuGet 2.8 可讓封裝本身中識別`.nuspec`為 developmentDependency 的檔案。</span><span class="sxs-lookup"><span data-stu-id="c1489-154">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="c1489-155">安裝時，此中繼資料也會加入至`packages.config`封裝已安裝所在的專案檔案。</span><span class="sxs-lookup"><span data-stu-id="c1489-155">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="c1489-156">時， `packages.config` NuGet 相依性期間稍後分析檔案`nuget.exe pack`，它會排除這些標示為開發相依性的相依性。</span><span class="sxs-lookup"><span data-stu-id="c1489-156">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="c1489-157">適用於不同平台的個別 packages.config 檔案</span><span class="sxs-lookup"><span data-stu-id="c1489-157">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="c1489-158">在開發用於多個目標平台的應用程式時，常會每個個別的建置環境有不同的專案檔。</span><span class="sxs-lookup"><span data-stu-id="c1489-158">When developing applications for multiple target platforms, it's common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="c1489-159">它也很常見使用不同的 NuGet 封裝，在不同的專案檔中，因為套件會有各種不同平台的支援層級。</span><span class="sxs-lookup"><span data-stu-id="c1489-159">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="c1489-160">NuGet 2.8 可改進支援此案例藉由建立不同`packages.config`不同的平台專屬專案檔的檔案。</span><span class="sxs-lookup"><span data-stu-id="c1489-160">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![多個 package.config 檔案](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="c1489-162">切換回本機快取</span><span class="sxs-lookup"><span data-stu-id="c1489-162">Fallback to Local Cache</span></span>

<span data-ttu-id="c1489-163">雖然 NuGet 套件通常都是從遠端資源庫這類[在 NuGet gallery](http://www.nuget.org/)使用網路連線，有許多用戶端未連接的案例。</span><span class="sxs-lookup"><span data-stu-id="c1489-163">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="c1489-164">沒有網路連線，NuGet 用戶端無法成功安裝封裝-，即使這些套件已在本機 NuGet 快取的用戶端的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c1489-164">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="c1489-165">NuGet 2.8 會將套件管理員主控台中的自動後援的快取。</span><span class="sxs-lookup"><span data-stu-id="c1489-165">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="c1489-166">比方說，當中斷連線的網路介面卡，並安裝 jQuery、 在主控台顯示下列資訊：</span><span class="sxs-lookup"><span data-stu-id="c1489-166">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="c1489-167">快取後援功能不需要任何特定的命令列引數。</span><span class="sxs-lookup"><span data-stu-id="c1489-167">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="c1489-168">此外，快取後援目前只適用於套件管理員主控台-行為目前不適用於 [套件管理員] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c1489-168">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="c1489-169">WebMatrix NuGet 用戶端更新</span><span class="sxs-lookup"><span data-stu-id="c1489-169">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="c1489-170">NuGet 2.8 以及 WebMatrix 的 NuGet 擴充功能也已更新為包含的許多主要的功能隨附於[NuGet 2.5](../release-notes/nuget-2.5.md)。</span><span class="sxs-lookup"><span data-stu-id="c1489-170">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="c1489-171">新功能包括例如 '更新 All'、' 最低 NuGet 版本 ' 和允許的內容檔案的覆寫。</span><span class="sxs-lookup"><span data-stu-id="c1489-171">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="c1489-172">若要更新您在 WebMatrix 3 中的 NuGet 套件管理員延伸模組：</span><span class="sxs-lookup"><span data-stu-id="c1489-172">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="c1489-173">開啟 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="c1489-173">Open WebMatrix 3</span></span>
1. <span data-ttu-id="c1489-174">按一下功能區中的延伸模組圖示</span><span class="sxs-lookup"><span data-stu-id="c1489-174">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="c1489-175">選取 [更新] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="c1489-175">Select the Updates tab</span></span>
1. <span data-ttu-id="c1489-176">按一下以更新 2.5.0 NuGet 套件管理員</span><span class="sxs-lookup"><span data-stu-id="c1489-176">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="c1489-177">關閉並重新啟動 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="c1489-177">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="c1489-178">這是 NuGet 小組的第一版的 NuGet 套件管理員延伸模組 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="c1489-178">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="c1489-179">Microsoft 最近被提供程式碼到開放原始碼 NuGet 專案。</span><span class="sxs-lookup"><span data-stu-id="c1489-179">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="c1489-180">先前，NuGet 整合內建在 WebMatrix 中，並無法更新超出訊號範圍從 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="c1489-180">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="c1489-181">我們現在有可進一步與 NuGet 的用戶端工具的其餘部分一起更新它的功能。</span><span class="sxs-lookup"><span data-stu-id="c1489-181">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="c1489-182">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="c1489-182">Bug Fixes</span></span>

<span data-ttu-id="c1489-183">其中一個所做的重大錯誤修正已更新套件中的效能改進-重新安裝命令。</span><span class="sxs-lookup"><span data-stu-id="c1489-183">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="c1489-184">除了這些功能和修正上述的效能，這一版的 NuGet 也會包含其他許多 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="c1489-184">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="c1489-185">發生在版本中解決的 181 總問題。</span><span class="sxs-lookup"><span data-stu-id="c1489-185">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="c1489-186">如需完整的工作清單項目中已修正 NuGet 2.8，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。</span><span class="sxs-lookup"><span data-stu-id="c1489-186">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>
