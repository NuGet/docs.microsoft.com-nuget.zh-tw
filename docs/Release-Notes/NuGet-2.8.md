---
title: "NuGet 2.8 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 77ba98d8-3d66-4126-b2b6-813ddd8ef192
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 2.8 的版本資訊。"
keywords: "NuGet 2.8 版本資訊、 錯誤修正的已知問題，已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0bb35e9d6ef6f3dde7919cd502b32ba5a550c689
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="c6712-104">NuGet 2.8 版本資訊</span><span class="sxs-lookup"><span data-stu-id="c6712-104">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="c6712-105">[NuGet 2.7.2 版本資訊](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 版本資訊](../release-notes/nuget-2.8.1.md)</span><span class="sxs-lookup"><span data-stu-id="c6712-105">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="c6712-106">NuGet 2.8 已於 2014 年 1 月 29 日發行。</span><span class="sxs-lookup"><span data-stu-id="c6712-106">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="c6712-107">謝誌</span><span class="sxs-lookup"><span data-stu-id="c6712-107">Acknowledgements</span></span>

1. <span data-ttu-id="c6712-108">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span><span class="sxs-lookup"><span data-stu-id="c6712-108">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="c6712-109">[#3466](https://nuget.codeplex.com/workitem/3466) -當壓縮封裝，驗證相依性套件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="c6712-109">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
1. <span data-ttu-id="c6712-110">[馬頓 Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span><span class="sxs-lookup"><span data-stu-id="c6712-110">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="c6712-111">[# 2379年](https://nuget.codeplex.com/workitem/2379)-persistening 摘要認證時，移除 $metadata 後置詞。</span><span class="sxs-lookup"><span data-stu-id="c6712-111">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
1. <span data-ttu-id="c6712-112">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span><span class="sxs-lookup"><span data-stu-id="c6712-112">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="c6712-113">[#3538](http://nuget.codeplex.com/workitem/3538) -指定 nuget.exe 更新命令的專案檔的支援。</span><span class="sxs-lookup"><span data-stu-id="c6712-113">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
1. [<span data-ttu-id="c6712-114">Juan Gonzalez</span><span class="sxs-lookup"><span data-stu-id="c6712-114">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="c6712-115">[#3536](http://nuget.codeplex.com/workitem/3536) -不會隨-IncludeReferencedProjects 取代語彙基元。</span><span class="sxs-lookup"><span data-stu-id="c6712-115">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
1. <span data-ttu-id="c6712-116">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span><span class="sxs-lookup"><span data-stu-id="c6712-116">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="c6712-117">[#3677](http://nuget.codeplex.com/workitem/3677) -修正 nuget.push 推入大型封裝時，擲回 OutOfMemoryException。</span><span class="sxs-lookup"><span data-stu-id="c6712-117">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
1. [<span data-ttu-id="c6712-118">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="c6712-118">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="c6712-119">[#3666](http://nuget.codeplex.com/workitem/3666) -修正不正確的目標路徑的專案參考另一個 CLI/c + + 專案時。</span><span class="sxs-lookup"><span data-stu-id="c6712-119">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
1. <span data-ttu-id="c6712-120">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="c6712-120">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="c6712-121">[#3639](https://nuget.codeplex.com/workitem/3639) -允許依預設，做為開發相依性安裝的封裝</span><span class="sxs-lookup"><span data-stu-id="c6712-121">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
1. <span data-ttu-id="c6712-122">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="c6712-122">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="c6712-123">[#3717](https://nuget.codeplex.com/workitem/3717) -移除隱含升級至最新修補程式版本</span><span class="sxs-lookup"><span data-stu-id="c6712-123">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
1. [<span data-ttu-id="c6712-124">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="c6712-124">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="c6712-125">數個 bug 修正和增強功能 NuGet.Server、 nuget.exe 鏡像命令，以及其他等等。</span><span class="sxs-lookup"><span data-stu-id="c6712-125">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="c6712-126">這項工作已完成 Gregory 我們努力右計時整合 2.8 主機幾個月。</span><span class="sxs-lookup"><span data-stu-id="c6712-126">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="c6712-127">修補程式解析的相依性</span><span class="sxs-lookup"><span data-stu-id="c6712-127">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="c6712-128">當解析封裝相依性，NuGet 在過去已實作選取最低的主要和次要的封裝版本能符合封裝上的相依性的策略。</span><span class="sxs-lookup"><span data-stu-id="c6712-128">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="c6712-129">不同於主要和次要版本中，不過，修補程式的版本是一定要解析為最高的版本。</span><span class="sxs-lookup"><span data-stu-id="c6712-129">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="c6712-130">雖然行為是本意良好，但，它會建立缺乏決定性具有相依性安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="c6712-130">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="c6712-131">參考下列範例：</span><span class="sxs-lookup"><span data-stu-id="c6712-131">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="c6712-132">在此範例中，即使 Developer1 Developer2 安裝和PackageA@1.0.0、 每個結束向上 PackageB 的不同版本。</span><span class="sxs-lookup"><span data-stu-id="c6712-132">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="c6712-133">NuGet 2.8 變更此預設行為的修補程式版本的相依性解析行為是使用主要和次要版本的行為一致。</span><span class="sxs-lookup"><span data-stu-id="c6712-133">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="c6712-134">在上述範例中，然後PackageB@1.0.0會安裝安裝PackageA@1.0.0，不論修補程式的較新版本。</span><span class="sxs-lookup"><span data-stu-id="c6712-134">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="c6712-135">-DependencyVersion 交換器</span><span class="sxs-lookup"><span data-stu-id="c6712-135">-DependencyVersion Switch</span></span>

<span data-ttu-id="c6712-136">雖然 NuGet 2.8 變更_預設_行為對於解析相依項，它也會加入相依性解析程序，透過-DependencyVersion 交換器的更精確地控制封裝管理員主控台中。</span><span class="sxs-lookup"><span data-stu-id="c6712-136">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="c6712-137">參數可讓解析的相依性，以最低的可能版本 （預設行為），可能最高的版本，或最高次要或修補程式的版本。</span><span class="sxs-lookup"><span data-stu-id="c6712-137">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="c6712-138">這個參數僅適用於安裝套件中的 powershell 命令。</span><span class="sxs-lookup"><span data-stu-id="c6712-138">This switch only works for install-package in the powershell command.</span></span>

![DependencyVersion 交換器](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="c6712-140">DependencyVersion 屬性</span><span class="sxs-lookup"><span data-stu-id="c6712-140">DependencyVersion Attribute</span></span>

<span data-ttu-id="c6712-141">除了以上詳述，能夠有也允許 NuGet 在 Nuget.Config 檔案中設定新的屬性-DependencyVersion 參數定義的預設值為何，如果未指定-DependencyVersion 交換器中的引動過程安裝套件。</span><span class="sxs-lookup"><span data-stu-id="c6712-141">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="c6712-142">這個值也會遵守任何安裝封裝作業的 [NuGet 套件管理員] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c6712-142">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="c6712-143">若要設定此值，請先 Nuget.Config 檔案中加入以下屬性：</span><span class="sxs-lookup"><span data-stu-id="c6712-143">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="c6712-144">預覽 NuGet 作業與-whatif</span><span class="sxs-lookup"><span data-stu-id="c6712-144">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="c6712-145">部分 NuGet 封裝可以有深入的相依性圖形，而在這種情況，它可以在安裝期間會有幫助、 解除安裝或更新作業來第一次看到 會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="c6712-145">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="c6712-146">NuGet 2.8 將標準的 PowerShell-whatif 參數新增至安裝套件、 解除安裝套件和更新套件的命令，以啟用視覺化的封裝命令將套用的整個終止。</span><span class="sxs-lookup"><span data-stu-id="c6712-146">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="c6712-147">例如，執行`install-package Microsoft.AspNet.WebApi -whatif`空的 ASP.NET Web 應用程式會產生下列。</span><span class="sxs-lookup"><span data-stu-id="c6712-147">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

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

## <a name="downgrade-package"></a><span data-ttu-id="c6712-148">降級封裝</span><span class="sxs-lookup"><span data-stu-id="c6712-148">Downgrade Package</span></span>

<span data-ttu-id="c6712-149">不常見的安裝套件的發行前版本，以便調查新的功能，然後決定要回復到最後一個穩定版本。</span><span class="sxs-lookup"><span data-stu-id="c6712-149">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="c6712-150">NuGet 2.8 之前，這是多重步驟的程序解除安裝發行前版本的封裝和其相依性，然後安裝較舊版本。</span><span class="sxs-lookup"><span data-stu-id="c6712-150">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="c6712-151">使用 NuGet 2.8，不過，更新套件現在會回復整個封裝封閉區段 （例如封裝的相依性樹狀目錄） 到之前的版本。</span><span class="sxs-lookup"><span data-stu-id="c6712-151">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="c6712-152">開發相依性</span><span class="sxs-lookup"><span data-stu-id="c6712-152">Development Dependencies</span></span>

<span data-ttu-id="c6712-153">許多不同類型的功能可以傳遞做為 NuGet 套件-包括用來最佳化開發程序的工具。</span><span class="sxs-lookup"><span data-stu-id="c6712-153">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="c6712-154">雖然可以很有幫助開發新的封裝，而這些元件不應視為發行新的封裝更新時的相依性。</span><span class="sxs-lookup"><span data-stu-id="c6712-154">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it is later published.</span></span> <span data-ttu-id="c6712-155">NuGet 2.8 可讓封裝本身中識別`.nuspec`developmentDependency 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6712-155">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="c6712-156">安裝時，此中繼資料也會以新增`packages.config`到其中安裝封裝的專案檔。</span><span class="sxs-lookup"><span data-stu-id="c6712-156">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="c6712-157">時， `packages.config` NuGet 相依性，在稍後分析檔案`nuget.exe pack`，其中會排除標記為開發相依性的相依性。</span><span class="sxs-lookup"><span data-stu-id="c6712-157">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="c6712-158">不同的平台的個別 packages.config 檔案</span><span class="sxs-lookup"><span data-stu-id="c6712-158">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="c6712-159">開發應用程式為多個目標平台，時，通常會有不同的專案檔的每個個別的建置環境。</span><span class="sxs-lookup"><span data-stu-id="c6712-159">When developing applications for multiple target platforms, it is common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="c6712-160">它通常也可以使用不同的專案檔中的不同 NuGet 套件封裝有各種不同平台的支援層級。</span><span class="sxs-lookup"><span data-stu-id="c6712-160">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="c6712-161">NuGet 2.8 提供改善的支援此案例藉由建立不同`packages.config`不同的平台專屬專案檔的檔案。</span><span class="sxs-lookup"><span data-stu-id="c6712-161">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![多個 package.config 檔案](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="c6712-163">後援至本機快取</span><span class="sxs-lookup"><span data-stu-id="c6712-163">Fallback to Local Cache</span></span>

<span data-ttu-id="c6712-164">雖然 NuGet 封裝通常使用從遠端組件庫例如[在 NuGet gallery](http://www.nuget.org/)使用網路連線，有許多用戶端無法連線的案例。</span><span class="sxs-lookup"><span data-stu-id="c6712-164">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="c6712-165">如果沒有網路連接，NuGet 用戶端無法成功安裝封裝-即使這些封裝工作已在本機的 NuGet 快取的用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="c6712-165">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="c6712-166">NuGet 2.8 會將後援自動快取加入至封裝管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="c6712-166">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="c6712-167">例如，當中斷連線的網路介面卡，安裝 jQuery 主控台顯示下列資訊：</span><span class="sxs-lookup"><span data-stu-id="c6712-167">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="c6712-168">快取後援功能不需要任何特定的命令列引數。</span><span class="sxs-lookup"><span data-stu-id="c6712-168">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="c6712-169">此外，後援的快取目前只適用於封裝管理員主控台-行為目前不適用於 [封裝管理員] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c6712-169">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="c6712-170">WebMatrix NuGet 用戶端更新</span><span class="sxs-lookup"><span data-stu-id="c6712-170">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="c6712-171">NuGet 2.8 以及 for WebMatrix NuGet 延伸模組也已更新成包含許多傳遞時的主要功能[NuGet 2.5](../release-notes/nuget-2.5.md)。</span><span class="sxs-lookup"><span data-stu-id="c6712-171">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="c6712-172">新功能包括例如 '更新 All'、' 最低 NuGet 版本 ' 和允許的內容檔案的覆寫。</span><span class="sxs-lookup"><span data-stu-id="c6712-172">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="c6712-173">若要更新您在 WebMatrix 3 的 NuGet 套件管理員擴充功能：</span><span class="sxs-lookup"><span data-stu-id="c6712-173">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="c6712-174">開啟 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="c6712-174">Open WebMatrix 3</span></span>
1. <span data-ttu-id="c6712-175">按一下功能區中的擴充功能圖示</span><span class="sxs-lookup"><span data-stu-id="c6712-175">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="c6712-176">選取 [更新] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="c6712-176">Select the Updates tab</span></span>
1. <span data-ttu-id="c6712-177">按一下以更新 2.5.0 NuGet 封裝管理員</span><span class="sxs-lookup"><span data-stu-id="c6712-177">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="c6712-178">關閉並重新啟動 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="c6712-178">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="c6712-179">這是 NuGet 小組的第一版 NuGet 套件管理員擴充 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="c6712-179">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="c6712-180">Microsoft 最近已造成程式碼到 NuGet 開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="c6712-180">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="c6712-181">先前，NuGet integration 已內建 WebMatrix，並且無法更新頻外方式從 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="c6712-181">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="c6712-182">我們現在有以進一步 NuGet 的用戶端工具的其餘部分一起更新它的功能。</span><span class="sxs-lookup"><span data-stu-id="c6712-182">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="c6712-183">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="c6712-183">Bug Fixes</span></span>

<span data-ttu-id="c6712-184">有一個主要的 bug 修正進行已更新套件中的效能改進層重新安裝命令。</span><span class="sxs-lookup"><span data-stu-id="c6712-184">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="c6712-185">除了這些功能與前述效能修正程式，這個版本的 NuGet 也包含許多其他 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="c6712-185">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="c6712-186">有一些版本中解決的 181 總問題。</span><span class="sxs-lookup"><span data-stu-id="c6712-186">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="c6712-187">如需完整清單的工作項目中修正 NuGet 2.8，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)。</span><span class="sxs-lookup"><span data-stu-id="c6712-187">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>
