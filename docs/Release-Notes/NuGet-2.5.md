---
title: "NuGet 2.5 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c193f1e3-d114-427f-9425-9930cc8e4db3
description: "NuGet 2.5 的已知的問題、 錯誤修正、 新增的功能，以及 Dcr 包括版本資訊。"
keywords: "NuGet 2.5 版本資訊、 錯誤修正的已知問題，已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8d3bebbbe550645fcffad078538134427103cf98
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="29a15-104">NuGet 2.5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="29a15-104">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="29a15-105">[NuGet 2.2.1 版本資訊](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 版本資訊](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="29a15-105">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="29a15-106">NuGet 2.5 已於 2013 年 4 月 25 日發行。</span><span class="sxs-lookup"><span data-stu-id="29a15-106">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="29a15-107">此版本太大，我們被迫略過 2.3 和 2.4 版本 ！</span><span class="sxs-lookup"><span data-stu-id="29a15-107">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="29a15-108">若要到目前為止，這是我們之前 nuget，與最大版本透過[160 工作項目](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)版本中。</span><span class="sxs-lookup"><span data-stu-id="29a15-108">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="29a15-109">謝誌</span><span class="sxs-lookup"><span data-stu-id="29a15-109">Acknowledgements</span></span>

<span data-ttu-id="29a15-110">我們想要感謝下列外部參與者的重要為 NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="29a15-110">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="29a15-111">[奧 Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="29a15-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="29a15-112">[# 2847年](https://nuget.codeplex.com/workitem/2847)-新增 MonoAndroid、 MonoTouch 和 MonoMac 已知的目標 framework 識別碼的清單。</span><span class="sxs-lookup"><span data-stu-id="29a15-112">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
1. <span data-ttu-id="29a15-113">[安德列斯 G.Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="29a15-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="29a15-114">[# 2865年](https://nuget.codeplex.com/workitem/2865)-修正拼字`NuGet.targets`for 區分大小寫的 OS</span><span class="sxs-lookup"><span data-stu-id="29a15-114">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
1. <span data-ttu-id="29a15-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="29a15-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="29a15-116">請 Mono 上建置方案。</span><span class="sxs-lookup"><span data-stu-id="29a15-116">Make the solution build on Mono.</span></span>
1. <span data-ttu-id="29a15-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="29a15-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="29a15-118">修正 Mono 上失敗的單元測試。</span><span class="sxs-lookup"><span data-stu-id="29a15-118">Fix unit tests failing on Mono.</span></span>
1. <span data-ttu-id="29a15-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="29a15-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="29a15-120">[# 2920年](https://nuget.codeplex.com/workitem/2920)-nuget.exe 套件命令不會傳播至 MSBuild 屬性</span><span class="sxs-lookup"><span data-stu-id="29a15-120">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
1. <span data-ttu-id="29a15-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="29a15-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="29a15-122">[# 1511年](https://nuget.codeplex.com/workitem/1511)-修改的 XML 處理程式碼與保留的格式。</span><span class="sxs-lookup"><span data-stu-id="29a15-122">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
1. <span data-ttu-id="29a15-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="29a15-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="29a15-124">加入自訂字典，以允許 build.cmd 才能成功辨識的字。</span><span class="sxs-lookup"><span data-stu-id="29a15-124">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
1. [<span data-ttu-id="29a15-125">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="29a15-125">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="29a15-126">在當地語系化的 VS 中執行時，請修正單元測試。</span><span class="sxs-lookup"><span data-stu-id="29a15-126">Fix unit tests when running in localized VS.</span></span>
1. [<span data-ttu-id="29a15-127">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="29a15-127">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="29a15-128">從 PackageService 擷取的介面</span><span class="sxs-lookup"><span data-stu-id="29a15-128">Extracted interface from PackageService</span></span>
1. <span data-ttu-id="29a15-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="29a15-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
    - <span data-ttu-id="29a15-130">[#936](https://nuget.codeplex.com/workitem/936) -處理封裝作業時的專案相依性</span><span class="sxs-lookup"><span data-stu-id="29a15-130">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
1. <span data-ttu-id="29a15-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="29a15-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
    - <span data-ttu-id="29a15-132">[# 2991年](https://nuget.codeplex.com/workitem/2991)， [#3164](https://nuget.codeplex.com/workitem/3164) -支援純文字密碼時在 nuget.cofig 檔案中儲存封裝來源的認證</span><span class="sxs-lookup"><span data-stu-id="29a15-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
1. <span data-ttu-id="29a15-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="29a15-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
    - <span data-ttu-id="29a15-134">[#3190](http://nuget.codeplex.com/workitem/3190)， [#3191](http://nuget.codeplex.com/workitem/3191) -修正取得封裝的說明描述</span><span class="sxs-lookup"><span data-stu-id="29a15-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="29a15-135">我們也歡迎下列人員找出錯誤與 NuGet 2.5 Beta/RC 已核准與之前的最後發行版本修正：</span><span class="sxs-lookup"><span data-stu-id="29a15-135">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="29a15-136">[Tong 牆](https://www.codeplex.com/site/users/view/CodeChief)([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="29a15-136">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="29a15-137">[#3200](https://nuget.codeplex.com/workitem/3200) -MSTest 中斷且最新 NuGet 2.4 和 2.5 的組建</span><span class="sxs-lookup"><span data-stu-id="29a15-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

# <a name="notable-features-in-the-release"></a><span data-ttu-id="29a15-138">在版本中值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="29a15-138">Notable features in the release</span></span>

## <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="29a15-139">允許使用者覆寫已存在的內容檔案</span><span class="sxs-lookup"><span data-stu-id="29a15-139">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="29a15-140">其中一個最常要求的功能的所有時間已經過覆寫已存在時包含在 NuGet 套件中的磁碟的內容檔案的能力。</span><span class="sxs-lookup"><span data-stu-id="29a15-140">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="29a15-141">NuGet 2.5 從開始，這些衝突會識別，系統會提示您覆寫檔案，而先前這些檔案永遠略過。</span><span class="sxs-lookup"><span data-stu-id="29a15-141">Starting with NuGet 2.5, these conflicts are identified and you will be prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![覆寫內容檔案](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="29a15-143">'nuget.exe 更新' 和 'Install-package' 現在都有新的選項 '-FileConflictAction' 來設定一些預設命令列的案例。</span><span class="sxs-lookup"><span data-stu-id="29a15-143">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="29a15-144">從封裝檔案已存在目標專案中時，請設定預設動作。</span><span class="sxs-lookup"><span data-stu-id="29a15-144">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="29a15-145">設定為 [覆寫]，永遠覆寫檔案。</span><span class="sxs-lookup"><span data-stu-id="29a15-145">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="29a15-146">設為 [忽略] 略過檔案。</span><span class="sxs-lookup"><span data-stu-id="29a15-146">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="29a15-147">如果未指定，它會提示輸入每個衝突的檔案。</span><span class="sxs-lookup"><span data-stu-id="29a15-147">If not specified, it will prompt for each conflicting file.</span></span>

## <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="29a15-148">自動匯入的 MSBuild 目標與 props 檔案</span><span class="sxs-lookup"><span data-stu-id="29a15-148">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="29a15-149">在最上層的 NuGet 封裝已建立新的傳統資料夾。</span><span class="sxs-lookup"><span data-stu-id="29a15-149">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="29a15-150">等`\lib`， `\content`，和`\tools`，您現在可以包含`\build`在封裝中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="29a15-150">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="29a15-151">在這個資料夾中，您可以將兩個檔案，具有固定的名稱放`{packageid}.targets`或`{packageid}.props`。</span><span class="sxs-lookup"><span data-stu-id="29a15-151">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="29a15-152">這兩個檔案可以是直接在`build`或架構特定的資料夾，就像其他資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="29a15-152">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="29a15-153">挑選最相符的 framework 資料夾的規則是完全相同的。</span><span class="sxs-lookup"><span data-stu-id="29a15-153">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="29a15-154">當 NuGet 封裝安裝 \build 檔案時，它會將加入 MSBuild`<Import>`指向專案檔中的項目`.targets`和`.props`檔案。</span><span class="sxs-lookup"><span data-stu-id="29a15-154">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="29a15-155">`.props`檔案加入在頂端，而`.targets`檔案新增到下方。</span><span class="sxs-lookup"><span data-stu-id="29a15-155">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

## <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="29a15-156">指定每個平台使用不同參考`<References/>`項目</span><span class="sxs-lookup"><span data-stu-id="29a15-156">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="29a15-157">2.5 之前, 在`.nuspec`檔案，使用者只可以指定要加入所有 framework 相同的檔案參考。</span><span class="sxs-lookup"><span data-stu-id="29a15-157">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="29a15-158">現在使用者可以利用此在 2.5 的新功能，撰寫`<reference/>`每個支援的平台，例如項目：</span><span class="sxs-lookup"><span data-stu-id="29a15-158">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="29a15-159">以下是如何 NuGet 加入基礎專案的參考流程`.nuspec`檔案：</span><span class="sxs-lookup"><span data-stu-id="29a15-159">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="29a15-160">尋找`lib`資料夾，適用於目標架構，並從該資料夾中取得的組件清單</span><span class="sxs-lookup"><span data-stu-id="29a15-160">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="29a15-161">個別找到適合的目標 framework 的參考群組，並從該群組取得組件清單。</span><span class="sxs-lookup"><span data-stu-id="29a15-161">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="29a15-162">沒有指定目標 framework 的參考群組為後援的群組。</span><span class="sxs-lookup"><span data-stu-id="29a15-162">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="29a15-163">尋找交集處的兩個清單中，並以在其中做為參考加入</span><span class="sxs-lookup"><span data-stu-id="29a15-163">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="29a15-164">這項新功能可讓封裝作者使用 [參考] 功能，否則它們需要在多個執行重複的組件時，將組件子集套用到不同的架構`lib`資料夾。</span><span class="sxs-lookup"><span data-stu-id="29a15-164">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="29a15-165">注意： 您必須現在使用 nuget.exe 套件使用這項功能。NuGet 封裝總管 還不支援它。</span><span class="sxs-lookup"><span data-stu-id="29a15-165">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

## <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="29a15-166">更新所有的按鈕，以允許立即更新所有的封裝</span><span class="sxs-lookup"><span data-stu-id="29a15-166">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="29a15-167">知道有關 「 更新套件 」 的 PowerShell 指令程式來更新所有封裝。現在是可以輕鬆地透過 UI 以及執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="29a15-167">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="29a15-168">若要試用此功能：</span><span class="sxs-lookup"><span data-stu-id="29a15-168">To try this feature out:</span></span>

1. <span data-ttu-id="29a15-169">建立新的 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="29a15-169">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="29a15-170">啟動 [管理 NuGet 套件] 對話方塊</span><span class="sxs-lookup"><span data-stu-id="29a15-170">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="29a15-171">選取 '更新'</span><span class="sxs-lookup"><span data-stu-id="29a15-171">Select 'Updates'</span></span>
1. <span data-ttu-id="29a15-172">按一下 [全部更新] 按鈕</span><span class="sxs-lookup"><span data-stu-id="29a15-172">Click the 'Update All' button</span></span>

![更新對話方塊中的所有按鈕](./media/NuGet-2.5/update-all.png)

## <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="29a15-174">Nuget.exe 套件的改良的專案參考支援</span><span class="sxs-lookup"><span data-stu-id="29a15-174">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="29a15-175">現在 nuget.exe 套件命令處理程序會參考專案的下列規則：</span><span class="sxs-lookup"><span data-stu-id="29a15-175">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="29a15-176">如果參考的專案具有對應`.nuspec`檔案中，例如沒有名為的檔案`proj1.nuspec`相同資料夾中`proj1.csproj`、 然後此專案會加入做為相依性套件，並使用識別碼和版本讀取`.nuspec`檔案。</span><span class="sxs-lookup"><span data-stu-id="29a15-176">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="29a15-177">否則，參考專案的檔案會集結到套件中。</span><span class="sxs-lookup"><span data-stu-id="29a15-177">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="29a15-178">然後您會使用 sames 規則以遞迴方式來處理這個專案所參考的專案。</span><span class="sxs-lookup"><span data-stu-id="29a15-178">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="29a15-179">所有 DLL， `.pdb`，和`.exe`檔案加入。</span><span class="sxs-lookup"><span data-stu-id="29a15-179">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="29a15-180">所有其他內容的檔案會加入。</span><span class="sxs-lookup"><span data-stu-id="29a15-180">All other content files are added.</span></span>
1. <span data-ttu-id="29a15-181">會合併所有的相依性。</span><span class="sxs-lookup"><span data-stu-id="29a15-181">All dependencies are merged.</span></span>

<span data-ttu-id="29a15-182">這可讓參考的專案，如果沒有，被視為相依`.nuspec`檔案中，否則它會變成套件的一部分。</span><span class="sxs-lookup"><span data-stu-id="29a15-182">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="29a15-183">這裡有更多詳細資料： [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="29a15-183">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

## <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="29a15-184">將 ' 至少 NuGet Version' 屬性加入封裝</span><span class="sxs-lookup"><span data-stu-id="29a15-184">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="29a15-185">新的中繼資料屬性，稱為 'minClientVersion' 現在可以指出使用封裝所需的最小 NuGet 用戶端版本。</span><span class="sxs-lookup"><span data-stu-id="29a15-185">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="29a15-186">這項功能可協助封裝作者以指定只有在特定版本的 NuGet 之後，封裝將正常運作。</span><span class="sxs-lookup"><span data-stu-id="29a15-186">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="29a15-187">當新`.nuspec`功能後加入 NuGet 2.5，封裝將無法宣告的最小的 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="29a15-187">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="29a15-188">如果使用者已安裝的 NuGet 2.5，封裝會被識別為需要 2.6 視覺提示將會提供給使用者指出無法安裝套件中。</span><span class="sxs-lookup"><span data-stu-id="29a15-188">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="29a15-189">然後將更新自己版本的 NuGet 會引導使用者。</span><span class="sxs-lookup"><span data-stu-id="29a15-189">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="29a15-190">這可以改善時若要安裝，但失敗，表示無法辨識的結構描述版本已識別封裝的開始位置的現有體驗。</span><span class="sxs-lookup"><span data-stu-id="29a15-190">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

## <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="29a15-191">相依性不會再不必要地更新套件安裝</span><span class="sxs-lookup"><span data-stu-id="29a15-191">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="29a15-192">NuGet 2.5 之前時已安裝的套件相依於已安裝在專案中，封裝的相依性會更新新的安裝，即使現有版本符合相依性。</span><span class="sxs-lookup"><span data-stu-id="29a15-192">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="29a15-193">如果已符合相依性版本起 NuGet 2.5，相依性將不會更新其他封裝的安裝期間。</span><span class="sxs-lookup"><span data-stu-id="29a15-193">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="29a15-194">**案例：**</span><span class="sxs-lookup"><span data-stu-id="29a15-194">**The scenario:**</span></span>

1. <span data-ttu-id="29a15-195">來源儲存機制包含封裝 B 1.0.0 和 1.0.2 版。</span><span class="sxs-lookup"><span data-stu-id="29a15-195">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="29a15-196">它也包含封裝 A 會相依於 B (> = 1.0.0)。</span><span class="sxs-lookup"><span data-stu-id="29a15-196">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="29a15-197">假設目前的專案已有封裝 B 版本 1.0.0 已安裝。</span><span class="sxs-lookup"><span data-stu-id="29a15-197">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="29a15-198">現在您想要安裝封裝 a。</span><span class="sxs-lookup"><span data-stu-id="29a15-198">Now you want to install package A.</span></span>

<span data-ttu-id="29a15-199">**2.2 和較舊的 NuGet： 中**</span><span class="sxs-lookup"><span data-stu-id="29a15-199">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="29a15-200">當安裝的封裝，NuGet 會自動更新 B 為 1.0.2，即使現有的版本 1.0.0 已滿足相依性版本條件約束，也就是 > = 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="29a15-200">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="29a15-201">**在 NuGet 2.5 和更新版本：**</span><span class="sxs-lookup"><span data-stu-id="29a15-201">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="29a15-202">因為它偵測到現有的版本 1.0.0 符合相依性版本條件約束，NuGet 就不再更新 B。</span><span class="sxs-lookup"><span data-stu-id="29a15-202">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="29a15-203">如需這項變更的詳細背景，讀取詳細[工作項目](http://nuget.codeplex.com/workitem/1681)以及相關[討論](http://nuget.codeplex.com/discussions/436712)。</span><span class="sxs-lookup"><span data-stu-id="29a15-203">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

## <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="29a15-204">nuget.exe 輸出 http 要求，以及詳細的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="29a15-204">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="29a15-205">如果您正在疑難排解 nuget.exe 或只知道哪些發出 HTTP 要求會在作業期間，'-詳細等級的詳細 ' 參數現在會輸出所做的所有 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="29a15-205">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Nuget.exe 的 HTTP 輸出](./media/NuGet-2.5/verbosity.png)

## <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="29a15-207">nuget.exe 推送現可支援 UNC 和資料夾的來源</span><span class="sxs-lookup"><span data-stu-id="29a15-207">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="29a15-208">之前 NuGet 2.5，如果您嘗試執行 'nuget.exe 推送' 上的 UNC 路徑或本機資料夾，為基礎的封裝來源推播會失敗。</span><span class="sxs-lookup"><span data-stu-id="29a15-208">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="29a15-209">使用最近加入的階層式組態功能，它變得很常見的 nuget.exe 需要為目標的資料夾 UNC/來源或以 HTTP 為基礎的 NuGet Gallery。</span><span class="sxs-lookup"><span data-stu-id="29a15-209">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="29a15-210">如果 nuget.exe 識別 UNC/資料夾來源起 NuGet 2.5，就會執行檔案複製到來源。</span><span class="sxs-lookup"><span data-stu-id="29a15-210">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="29a15-211">下列命令能否正常運作：</span><span class="sxs-lookup"><span data-stu-id="29a15-211">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

## <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="29a15-212">nuget.exe 支援明確指定的組態檔</span><span class="sxs-lookup"><span data-stu-id="29a15-212">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="29a15-213">nuget.exe 命令的存取設定 （除了 '規格' 和 '組件' 全部） 現在支援新的 '-ConfigFile' 選項，強制執行特定的組態檔可用於取代 %appdata%\nuget\nuget.config 預設組態檔。</span><span class="sxs-lookup"><span data-stu-id="29a15-213">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="29a15-214">範例：</span><span class="sxs-lookup"><span data-stu-id="29a15-214">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

## <a name="support-for-native-projects"></a><span data-ttu-id="29a15-215">原生專案的支援</span><span class="sxs-lookup"><span data-stu-id="29a15-215">Support for Native projects</span></span>

<span data-ttu-id="29a15-216">以 NuGet 2.5 NuGet 工具現在是適用於 Visual Studio 中的原生專案。</span><span class="sxs-lookup"><span data-stu-id="29a15-216">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="29a15-217">我們預期最原生封裝會利用上述的 MSBuild 匯入功能使用工具所建立[CoApp 專案](http://coapp.org)。</span><span class="sxs-lookup"><span data-stu-id="29a15-217">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="29a15-218">如需詳細資訊，請參閱[工具的相關詳細資料](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html)coapp.org 網站上。</span><span class="sxs-lookup"><span data-stu-id="29a15-218">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="29a15-219">「 原生 」 的目標 framework 名稱被引進的封裝時所要包括檔案 \build、 \content，和 \tools 封裝安裝到原生專案。</span><span class="sxs-lookup"><span data-stu-id="29a15-219">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="29a15-220">\\`Lib' 資料夾不能用於原生專案。</span><span class="sxs-lookup"><span data-stu-id="29a15-220">The \`lib` folder is not used for native projects.</span></span>
