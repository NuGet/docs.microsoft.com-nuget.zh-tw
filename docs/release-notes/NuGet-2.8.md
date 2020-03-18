---
title: NuGet 2.8 版本資訊
description: NuGet 2.8 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429049"
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="d24cd-103">NuGet 2.8 版本資訊</span><span class="sxs-lookup"><span data-stu-id="d24cd-103">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="d24cd-104">[Nuget 2.7.2 版本](../release-notes/nuget-2.7.2.md)資訊 | [nuget 2.8.1 版本](../release-notes/nuget-2.8.1.md)資訊</span><span class="sxs-lookup"><span data-stu-id="d24cd-104">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="d24cd-105">NuGet 2.8 已于2014年1月29日發行。</span><span class="sxs-lookup"><span data-stu-id="d24cd-105">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="d24cd-106">致謝</span><span class="sxs-lookup"><span data-stu-id="d24cd-106">Acknowledgements</span></span>

1. <span data-ttu-id="d24cd-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) （[@leppie](https://twitter.com/leppie)）</span><span class="sxs-lookup"><span data-stu-id="d24cd-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="d24cd-108">[#3466](https://nuget.codeplex.com/workitem/3466) -封裝套件時，驗證相依性套件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="d24cd-108">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
2. <span data-ttu-id="d24cd-109">[聖馬丁 Balliauw](https://www.codeplex.com/site/users/view/maartenba) （[@maartenballiauw](https://twitter.com/maartenballiauw)）</span><span class="sxs-lookup"><span data-stu-id="d24cd-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="d24cd-110">[#2379](https://nuget.codeplex.com/workitem/2379) -在 persistening 摘要認證時移除 $metadata 尾碼。</span><span class="sxs-lookup"><span data-stu-id="d24cd-110">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
3. <span data-ttu-id="d24cd-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) （[@foxtricks](https://twitter.com/foxtricks)）</span><span class="sxs-lookup"><span data-stu-id="d24cd-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="d24cd-112">[#3538](http://nuget.codeplex.com/workitem/3538) -支援指定 nuget.exe update 命令的專案檔。</span><span class="sxs-lookup"><span data-stu-id="d24cd-112">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
4. [<span data-ttu-id="d24cd-113">Juan Gonzalez</span><span class="sxs-lookup"><span data-stu-id="d24cd-113">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="d24cd-114">未隨-IncludeReferencedProjects 傳遞的[#3536](http://nuget.codeplex.com/workitem/3536)取代權杖。</span><span class="sxs-lookup"><span data-stu-id="d24cd-114">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
5. <span data-ttu-id="d24cd-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) （[@Sarkie_Dave](https://twitter.com/Sarkie_Dave)）</span><span class="sxs-lookup"><span data-stu-id="d24cd-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="d24cd-116">[#3677](http://nuget.codeplex.com/workitem/3677) -修正 nuget。推送大型套件時，發送擲回 OutOfMemoryException。</span><span class="sxs-lookup"><span data-stu-id="d24cd-116">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
6. [<span data-ttu-id="d24cd-117">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="d24cd-117">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="d24cd-118">[#3666](http://nuget.codeplex.com/workitem/3666) -當專案參考另一個 CLI/C++專案時，修正不正確的目標路徑。</span><span class="sxs-lookup"><span data-stu-id="d24cd-118">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
7. <span data-ttu-id="d24cd-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) （[@adamralph](https://twitter.com/adamralph)）</span><span class="sxs-lookup"><span data-stu-id="d24cd-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="d24cd-120">[#3639](https://nuget.codeplex.com/workitem/3639) -允許依預設將套件安裝為開發相依性</span><span class="sxs-lookup"><span data-stu-id="d24cd-120">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
8. <span data-ttu-id="d24cd-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) （[@davidfowl](https://twitter.com/davidfowl)）</span><span class="sxs-lookup"><span data-stu-id="d24cd-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="d24cd-122">[#3717](https://nuget.codeplex.com/workitem/3717) -移除對最新修補程式版本的隱含升級</span><span class="sxs-lookup"><span data-stu-id="d24cd-122">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
9. [<span data-ttu-id="d24cd-123">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="d24cd-123">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="d24cd-124">NuGet. 伺服器、nuget.exe 鏡像命令及其他專案的數個 bug 修正和改善。</span><span class="sxs-lookup"><span data-stu-id="d24cd-124">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="d24cd-125">這項工作已在數個月內完成，Gregory 與我們合作，以在適當的時機與我們整合到2.8 的主機。</span><span class="sxs-lookup"><span data-stu-id="d24cd-125">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="d24cd-126">相依性的修補程式解析</span><span class="sxs-lookup"><span data-stu-id="d24cd-126">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="d24cd-127">在解析套件相依性時，NuGet 過去已實行一種策略來選取符合封裝相依性的最低主要和次要套件版本。</span><span class="sxs-lookup"><span data-stu-id="d24cd-127">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="d24cd-128">但與主要和次要版本不同的是，修補程式版本一律會解析為最高版本。</span><span class="sxs-lookup"><span data-stu-id="d24cd-128">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="d24cd-129">雖然此行為是因為善意的，但它卻建立了安裝具有相依性之套件的不確定性。</span><span class="sxs-lookup"><span data-stu-id="d24cd-129">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="d24cd-130">請考慮下列範例：</span><span class="sxs-lookup"><span data-stu-id="d24cd-130">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="d24cd-131">在此範例中，即使已 PackageA@1.0.0安裝 Developer1 和 Developer2，每個都是以不同版本的 PackageB 來結束。</span><span class="sxs-lookup"><span data-stu-id="d24cd-131">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="d24cd-132">NuGet 2.8 會變更此預設行為，讓修補程式版本的相依性解析行為與主要和次要版本的行為一致。</span><span class="sxs-lookup"><span data-stu-id="d24cd-132">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="d24cd-133">在上述範例中，PackageB@1.0.0 會因為安裝 PackageA@1.0.0而安裝，而不論較新的修補程式版本為何。</span><span class="sxs-lookup"><span data-stu-id="d24cd-133">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="d24cd-134">-DependencyVersion 參數</span><span class="sxs-lookup"><span data-stu-id="d24cd-134">-DependencyVersion Switch</span></span>

<span data-ttu-id="d24cd-135">雖然 NuGet 2.8 會變更解析相依性的_預設_行為，但它也會透過套件管理員主控台中的-DependencyVersion 參數，更精確地控制相依性解析程式。</span><span class="sxs-lookup"><span data-stu-id="d24cd-135">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="d24cd-136">參數可讓您將相依性解析成最低可能版本（預設行為）、可能的最高版本，或最高的次要或修補程式版本。</span><span class="sxs-lookup"><span data-stu-id="d24cd-136">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="d24cd-137">此交換器僅適用于 powershell 命令中的安裝套件。</span><span class="sxs-lookup"><span data-stu-id="d24cd-137">This switch only works for install-package in the powershell command.</span></span>

![DependencyVersion 參數](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="d24cd-139">DependencyVersion 屬性</span><span class="sxs-lookup"><span data-stu-id="d24cd-139">DependencyVersion Attribute</span></span>

<span data-ttu-id="d24cd-140">除了上面詳述的-DependencyVersion 參數外，NuGet 也可以在定義預設值的 Nuget.exe 檔案中設定新屬性（如果未在的調用中指定-DependencyVersion 參數）。install-package。</span><span class="sxs-lookup"><span data-stu-id="d24cd-140">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="d24cd-141">[NuGet 套件管理員] 對話方塊也會遵循此值，進行任何安裝封裝作業。</span><span class="sxs-lookup"><span data-stu-id="d24cd-141">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="d24cd-142">若要設定此值，請將下列屬性新增至您的 Nuget .Config 檔案：</span><span class="sxs-lookup"><span data-stu-id="d24cd-142">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="d24cd-143">使用-whatif 預覽 NuGet 作業</span><span class="sxs-lookup"><span data-stu-id="d24cd-143">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="d24cd-144">某些 NuGet 套件可以有深度相依性圖形，因此在安裝、卸載或更新作業時，可能會先瞭解會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="d24cd-144">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="d24cd-145">NuGet 2.8 將標準 PowerShell-whatif 參數新增至安裝套件、卸載套件和更新套件命令，以視覺化方式將套用命令的整個套件關閉。</span><span class="sxs-lookup"><span data-stu-id="d24cd-145">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="d24cd-146">例如，在空白 ASP.NET Web 應用程式中執行 `install-package Microsoft.AspNet.WebApi -whatif` 會產生下列結果。</span><span class="sxs-lookup"><span data-stu-id="d24cd-146">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

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

## <a name="downgrade-package"></a><span data-ttu-id="d24cd-147">降級封裝</span><span class="sxs-lookup"><span data-stu-id="d24cd-147">Downgrade Package</span></span>

<span data-ttu-id="d24cd-148">安裝套件的搶鮮版，以調查新功能，然後決定復原到最後一個穩定版本，並不是很常見的情況。</span><span class="sxs-lookup"><span data-stu-id="d24cd-148">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="d24cd-149">在 NuGet 2.8 之前，這是卸載發行前版本套件及其相依性，然後再安裝舊版的多步驟程式。</span><span class="sxs-lookup"><span data-stu-id="d24cd-149">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="d24cd-150">不過，使用 NuGet 2.8，更新套件現在會將整個套件關閉（例如套件的相依性樹狀結構）復原到先前的版本。</span><span class="sxs-lookup"><span data-stu-id="d24cd-150">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="d24cd-151">開發相依性</span><span class="sxs-lookup"><span data-stu-id="d24cd-151">Development Dependencies</span></span>

<span data-ttu-id="d24cd-152">許多不同類型的功能可以做為 NuGet 套件提供，包括用來優化開發程式的工具。</span><span class="sxs-lookup"><span data-stu-id="d24cd-152">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="d24cd-153">這些元件雖然可能有助於開發新的套件，但在稍後發行時，不應將其視為新封裝的相依性。</span><span class="sxs-lookup"><span data-stu-id="d24cd-153">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it's later published.</span></span> <span data-ttu-id="d24cd-154">NuGet 2.8 可讓套件在 `.nuspec` 檔案中將其本身識別為 developmentDependency。</span><span class="sxs-lookup"><span data-stu-id="d24cd-154">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="d24cd-155">安裝時，此中繼資料也會加入至已安裝封裝之專案的 `packages.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="d24cd-155">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="d24cd-156">稍後在 `nuget.exe pack`中分析 NuGet 相依性的 `packages.config` 檔案時，將會排除標示為開發相依性的相依性。</span><span class="sxs-lookup"><span data-stu-id="d24cd-156">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="d24cd-157">不同平臺的個別封裝 .config 檔案</span><span class="sxs-lookup"><span data-stu-id="d24cd-157">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="d24cd-158">開發多個目標平臺的應用程式時，每個個別的組建環境都有不同的專案檔案。</span><span class="sxs-lookup"><span data-stu-id="d24cd-158">When developing applications for multiple target platforms, it's common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="d24cd-159">在不同的專案檔中使用不同的 NuGet 套件也很常見，因為套件具有不同平臺的各種支援層級。</span><span class="sxs-lookup"><span data-stu-id="d24cd-159">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="d24cd-160">NuGet 2.8 為不同平臺特定的專案檔建立不同的 `packages.config` 檔案，為此案例提供了更好的支援。</span><span class="sxs-lookup"><span data-stu-id="d24cd-160">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![多個 package .config 檔案](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="d24cd-162">回到本機快取</span><span class="sxs-lookup"><span data-stu-id="d24cd-162">Fallback to Local Cache</span></span>

<span data-ttu-id="d24cd-163">雖然 NuGet 套件通常是從使用網路連線的遠端資源庫（例如[nuget 資源庫](http://www.nuget.org/)）取用，但在許多情況下，用戶端並未連接。</span><span class="sxs-lookup"><span data-stu-id="d24cd-163">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="d24cd-164">如果沒有網路連線，NuGet 用戶端就無法成功安裝套件，即使這些套件已經在本機 NuGet 快取的用戶端電腦上也一樣。</span><span class="sxs-lookup"><span data-stu-id="d24cd-164">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="d24cd-165">NuGet 2.8 會將自動快取回溯新增至套件管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="d24cd-165">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="d24cd-166">例如，當中斷網路介面卡的連線並安裝 jQuery 時，主控台會顯示下列內容：</span><span class="sxs-lookup"><span data-stu-id="d24cd-166">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="d24cd-167">快取回退功能不需要任何特定的命令引數。</span><span class="sxs-lookup"><span data-stu-id="d24cd-167">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="d24cd-168">此外，快取回退目前僅適用于套件管理員主控台-此行為目前無法在 [套件管理員] 對話方塊中運作。</span><span class="sxs-lookup"><span data-stu-id="d24cd-168">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="d24cd-169">WebMatrix NuGet 用戶端更新</span><span class="sxs-lookup"><span data-stu-id="d24cd-169">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="d24cd-170">除了 NuGet 2.8，適用于 WebMatrix 的 NuGet 延伸模組也已更新，以包含[nuget 2.5](../release-notes/nuget-2.5.md)提供的許多主要功能。</span><span class="sxs-lookup"><span data-stu-id="d24cd-170">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="d24cd-171">新功能包括「全部更新」、「最低 NuGet 版本」，並允許覆寫內容檔案。</span><span class="sxs-lookup"><span data-stu-id="d24cd-171">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="d24cd-172">若要更新 WebMatrix 3 中的 NuGet 套件管理員延伸模組：</span><span class="sxs-lookup"><span data-stu-id="d24cd-172">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="d24cd-173">開啟 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="d24cd-173">Open WebMatrix 3</span></span>
1. <span data-ttu-id="d24cd-174">按一下功能區中的 [延伸模組] 圖示</span><span class="sxs-lookup"><span data-stu-id="d24cd-174">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="d24cd-175">選取 [更新] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="d24cd-175">Select the Updates tab</span></span>
1. <span data-ttu-id="d24cd-176">按一下以將 NuGet 套件管理員更新為2.5。0</span><span class="sxs-lookup"><span data-stu-id="d24cd-176">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="d24cd-177">關閉並重新啟動 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="d24cd-177">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="d24cd-178">這是 NuGet 小組第一版的 NuGet 套件管理員延伸模組（適用于 WebMatrix）。</span><span class="sxs-lookup"><span data-stu-id="d24cd-178">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="d24cd-179">Microsoft 最近將此程式碼提供給開放原始碼 NuGet 專案。</span><span class="sxs-lookup"><span data-stu-id="d24cd-179">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="d24cd-180">先前，NuGet 整合已內建到 WebMatrix 中，無法從 WebMatrix 升級。</span><span class="sxs-lookup"><span data-stu-id="d24cd-180">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="d24cd-181">我們現在可以進一步將它與 NuGet 用戶端工具的其餘部分一起更新。</span><span class="sxs-lookup"><span data-stu-id="d24cd-181">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="d24cd-182">錯誤修正</span><span class="sxs-lookup"><span data-stu-id="d24cd-182">Bug Fixes</span></span>

<span data-ttu-id="d24cd-183">其中一個主要錯誤修正是在更新-封裝-重新安裝命令中改善效能。</span><span class="sxs-lookup"><span data-stu-id="d24cd-183">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="d24cd-184">除了這些功能和前述的效能修正之外，這一版的 NuGet 也包含其他許多 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="d24cd-184">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="d24cd-185">發行中解決了181的總問題。</span><span class="sxs-lookup"><span data-stu-id="d24cd-185">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="d24cd-186">如需 NuGet 2.8 中已修正之工作專案的完整清單，請參閱[此版本的 NuGet 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。</span><span class="sxs-lookup"><span data-stu-id="d24cd-186">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>
