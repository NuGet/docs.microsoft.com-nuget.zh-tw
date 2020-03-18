---
title: NuGet 2.5 版本資訊
description: NuGet 2.5 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428713"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="c4033-103">NuGet 2.5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="c4033-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="c4033-104">[Nuget 2.2.1 版本](../release-notes/nuget-2.2.1.md)資訊 | [nuget 2.6 版本](../release-notes/nuget-2.6.md)資訊</span><span class="sxs-lookup"><span data-stu-id="c4033-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="c4033-105">NuGet 2.5 已于2013年4月25日發行。</span><span class="sxs-lookup"><span data-stu-id="c4033-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="c4033-106">此版本很大，我們認為不需要略過2.3 和2.4 版！</span><span class="sxs-lookup"><span data-stu-id="c4033-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="c4033-107">到目前為止，這是我們針對 NuGet 所擁有的最大版本，版本中有超過[160 個工作專案](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all)。</span><span class="sxs-lookup"><span data-stu-id="c4033-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="c4033-108">致謝</span><span class="sxs-lookup"><span data-stu-id="c4033-108">Acknowledgements</span></span>

<span data-ttu-id="c4033-109">我們想要感謝下列外部參與者對 NuGet 2.5 的重大貢獻：</span><span class="sxs-lookup"><span data-stu-id="c4033-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="c4033-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) （[@dsplaisted](https://twitter.com/dsplaisted)）</span><span class="sxs-lookup"><span data-stu-id="c4033-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="c4033-111">[#2847](https://nuget.codeplex.com/workitem/2847) -將 MonoAndroid、MonoTouch 和 MonoMac 新增至已知的目標 framework 識別碼清單。</span><span class="sxs-lookup"><span data-stu-id="c4033-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="c4033-112">[Andres g. Aragoneses](https://www.codeplex.com/site/users/view/knocte) （[@knocte](https://twitter.com/knocte)）</span><span class="sxs-lookup"><span data-stu-id="c4033-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="c4033-113">[#2865](https://nuget.codeplex.com/workitem/2865) -修正區分大小寫 OS 的 `NuGet.targets` 拼寫</span><span class="sxs-lookup"><span data-stu-id="c4033-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="c4033-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) （[@davidfowl](https://twitter.com/davidfowl)）</span><span class="sxs-lookup"><span data-stu-id="c4033-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="c4033-115">在 Mono 上建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="c4033-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="c4033-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) （[@atheken](https://twitter.com/atheken)）</span><span class="sxs-lookup"><span data-stu-id="c4033-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="c4033-117">修正 Mono 上的單元測試失敗。</span><span class="sxs-lookup"><span data-stu-id="c4033-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="c4033-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) （[@OliIsCool](https://twitter.com/oliiscool)）</span><span class="sxs-lookup"><span data-stu-id="c4033-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="c4033-119">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe pack 命令不會將屬性傳播到 MSBuild</span><span class="sxs-lookup"><span data-stu-id="c4033-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="c4033-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) （[@bajtos](https://twitter.com/bajtos)）</span><span class="sxs-lookup"><span data-stu-id="c4033-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="c4033-121">[#1511](https://nuget.codeplex.com/workitem/1511)修改過的 XML 處理常式代碼，以保留格式。</span><span class="sxs-lookup"><span data-stu-id="c4033-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="c4033-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) （[@adamralph](https://twitter.com/adamralph)）</span><span class="sxs-lookup"><span data-stu-id="c4033-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="c4033-123">已將可辨識的單字加入自訂字典，以允許成功建立 .cmd。</span><span class="sxs-lookup"><span data-stu-id="c4033-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="c4033-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="c4033-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="c4033-125">修正在當地語系化與中執行時的單元測試</span><span class="sxs-lookup"><span data-stu-id="c4033-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="c4033-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="c4033-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="c4033-127">已從 PackageService 解壓縮介面</span><span class="sxs-lookup"><span data-stu-id="c4033-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="c4033-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) （[@brugidou](https://twitter.com/brugidou)）</span><span class="sxs-lookup"><span data-stu-id="c4033-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="c4033-129">[#936](https://nuget.codeplex.com/workitem/936) -在封裝時處理專案相依性</span><span class="sxs-lookup"><span data-stu-id="c4033-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="c4033-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) （[@XavierDecoster](https://twitter.com/xavierdecoster)）</span><span class="sxs-lookup"><span data-stu-id="c4033-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="c4033-131">[#2991](https://nuget.codeplex.com/workitem/2991)， [#3164](https://nuget.codeplex.com/workitem/3164)支援在 cofig 檔案中儲存封裝來源認證時的純文字密碼</span><span class="sxs-lookup"><span data-stu-id="c4033-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="c4033-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) （[@manningj](https://twitter.com/manningj)）</span><span class="sxs-lookup"><span data-stu-id="c4033-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="c4033-133">[#3190](http://nuget.codeplex.com/workitem/3190)， [#3191](http://nuget.codeplex.com/workitem/3191) -修正取得封裝說明描述</span><span class="sxs-lookup"><span data-stu-id="c4033-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="c4033-134">我們也感謝下列個人在最終發行之前，使用已核准和修正的 NuGet 2.5 Beta/RC 來尋找 bug：</span><span class="sxs-lookup"><span data-stu-id="c4033-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="c4033-135">[Tony 牆](https://www.codeplex.com/site/users/view/CodeChief)（[@CodeChief](https://twitter.com/codechief)）</span><span class="sxs-lookup"><span data-stu-id="c4033-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="c4033-136">[#3200](https://nuget.codeplex.com/workitem/3200) -MSTest 與最新 NuGet 2.4 和2.5 組建中斷</span><span class="sxs-lookup"><span data-stu-id="c4033-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="c4033-137">版本中值得注意的功能</span><span class="sxs-lookup"><span data-stu-id="c4033-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="c4033-138">允許使用者覆寫已存在的內容檔案</span><span class="sxs-lookup"><span data-stu-id="c4033-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="c4033-139">所有時間最常要求的功能之一，就是當包含在 NuGet 套件中時，可以覆寫磁片上已存在的內容檔案。</span><span class="sxs-lookup"><span data-stu-id="c4033-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="c4033-140">從 NuGet 2.5 開始，會識別這些衝突，而且系統會提示您覆寫檔案，而先前這些檔案一律會略過。</span><span class="sxs-lookup"><span data-stu-id="c4033-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![覆寫內容檔案](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="c4033-142">[nuget.exe update] 和 [Install-Package] 現在都有一個新選項 [-FileConflictAction] 可設定命令列案例的一些預設值。</span><span class="sxs-lookup"><span data-stu-id="c4033-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="c4033-143">當目標專案中已經有套件的檔案存在時，設定預設動作。</span><span class="sxs-lookup"><span data-stu-id="c4033-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="c4033-144">設定為 [覆寫] 一律會覆寫檔案。</span><span class="sxs-lookup"><span data-stu-id="c4033-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="c4033-145">設定為 [忽略] 以略過檔案。</span><span class="sxs-lookup"><span data-stu-id="c4033-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="c4033-146">如果未指定，則會提示每個衝突的檔案。</span><span class="sxs-lookup"><span data-stu-id="c4033-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="c4033-147">自動匯入 MSBuild 目標和 .props 檔</span><span class="sxs-lookup"><span data-stu-id="c4033-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="c4033-148">已在 NuGet 封裝的最上層建立新的傳統資料夾。</span><span class="sxs-lookup"><span data-stu-id="c4033-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="c4033-149">若要對 `\lib`、`\content`和 `\tools`的對等，您現在可以在封裝中包含 `\build` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c4033-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="c4033-150">在此資料夾底下，您可以將兩個具有固定名稱的檔案 `{packageid}.targets` 或 `{packageid}.props`。</span><span class="sxs-lookup"><span data-stu-id="c4033-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="c4033-151">這兩個檔案可以直接在 `build` 之下，或在架構特定資料夾之下，就像其他資料夾一樣。</span><span class="sxs-lookup"><span data-stu-id="c4033-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="c4033-152">挑選 [最符合規範的架構] 資料夾的規則與在中的原則完全相同。</span><span class="sxs-lookup"><span data-stu-id="c4033-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="c4033-153">當 NuGet 安裝具有 \build 檔案的套件時，它會在指向 `.targets` 和 `.props` 檔案的專案檔中新增 MSBuild `<Import>` 元素。</span><span class="sxs-lookup"><span data-stu-id="c4033-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="c4033-154">`.props` 檔案會新增到頂端，而 `.targets` 檔案則會加入至底部。</span><span class="sxs-lookup"><span data-stu-id="c4033-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="c4033-155">使用 `<References/>` 元素，為每個平臺指定不同的參考</span><span class="sxs-lookup"><span data-stu-id="c4033-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="c4033-156">在2.5 之前，在 `.nuspec` 檔案中，使用者只能指定要為所有架構新增的參考檔案。</span><span class="sxs-lookup"><span data-stu-id="c4033-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="c4033-157">使用2.5 中的這項新功能，使用者可以為每個支援的平臺撰寫 `<reference/>` 元素，例如：</span><span class="sxs-lookup"><span data-stu-id="c4033-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="c4033-158">以下是 NuGet 如何根據 `.nuspec` 檔案新增專案參考的流程：</span><span class="sxs-lookup"><span data-stu-id="c4033-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="c4033-159">尋找適用于目標 framework 的 `lib` 資料夾，並從該資料夾取得元件清單</span><span class="sxs-lookup"><span data-stu-id="c4033-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="c4033-160">分別尋找適用于目標 framework 的 [參考] 群組，並從該群組取得元件清單。</span><span class="sxs-lookup"><span data-stu-id="c4033-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="c4033-161">未指定目標 framework 的參考群組是回溯群組。</span><span class="sxs-lookup"><span data-stu-id="c4033-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="c4033-162">尋找兩個清單的交集，並使用它做為要新增的參考</span><span class="sxs-lookup"><span data-stu-id="c4033-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="c4033-163">這項新功能可讓套件作者使用「參考」功能，將元件的子集套用至不同的架構，當它們需要在多個 `lib` 資料夾中執行重複的元件時。</span><span class="sxs-lookup"><span data-stu-id="c4033-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="c4033-164">注意：您目前必須使用 nuget.exe pack 才能使用此功能;NuGet Package Explorer 尚未支援。</span><span class="sxs-lookup"><span data-stu-id="c4033-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="c4033-165">[全部更新] 按鈕可讓您一次更新所有套件</span><span class="sxs-lookup"><span data-stu-id="c4033-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="c4033-166">您有許多人都知道「更新套件」 PowerShell Cmdlet 來更新所有套件;現在，您也可以透過 UI 輕鬆執行此動作。</span><span class="sxs-lookup"><span data-stu-id="c4033-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="c4033-167">若要嘗試這項功能：</span><span class="sxs-lookup"><span data-stu-id="c4033-167">To try this feature out:</span></span>

1. <span data-ttu-id="c4033-168">建立新的 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="c4033-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="c4033-169">啟動 [管理 NuGet 封裝] 對話方塊</span><span class="sxs-lookup"><span data-stu-id="c4033-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="c4033-170">選取 [更新]</span><span class="sxs-lookup"><span data-stu-id="c4033-170">Select 'Updates'</span></span>
1. <span data-ttu-id="c4033-171">按一下 [全部更新] 按鈕</span><span class="sxs-lookup"><span data-stu-id="c4033-171">Click the 'Update All' button</span></span>

![對話方塊中的 [全部更新] 按鈕](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="c4033-173">已改善 nuget .exe 套件的專案參考支援</span><span class="sxs-lookup"><span data-stu-id="c4033-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="c4033-174">現在，nuget.exe pack 命令會以下列規則處理參考的專案：</span><span class="sxs-lookup"><span data-stu-id="c4033-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="c4033-175">如果參考的專案具有對應的 `.nuspec` 檔案（例如，在與 `proj1.csproj`相同的資料夾中有稱為 `proj1.nuspec` 的檔案），則會使用從 `.nuspec` 檔案讀取的識別碼和版本，將此專案新增為封裝的相依性。</span><span class="sxs-lookup"><span data-stu-id="c4033-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="c4033-176">否則，會將參考專案的檔案配套到封裝中。</span><span class="sxs-lookup"><span data-stu-id="c4033-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="c4033-177">此專案所參考的專案，將會以遞迴方式使用相同規則來處理。</span><span class="sxs-lookup"><span data-stu-id="c4033-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="c4033-178">新增所有 DLL、`.pdb`和 `.exe` 檔案。</span><span class="sxs-lookup"><span data-stu-id="c4033-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="c4033-179">新增所有其他內容檔案。</span><span class="sxs-lookup"><span data-stu-id="c4033-179">All other content files are added.</span></span>
1. <span data-ttu-id="c4033-180">會合並所有相依性。</span><span class="sxs-lookup"><span data-stu-id="c4033-180">All dependencies are merged.</span></span>

<span data-ttu-id="c4033-181">這可讓參考的專案視為相依性（如果有 `.nuspec` 檔案），否則它會成為封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="c4033-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="c4033-182">詳細資料請參閱： [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="c4033-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="c4033-183">將「最低 NuGet 版本」屬性新增至套件</span><span class="sxs-lookup"><span data-stu-id="c4033-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="c4033-184">名為 ' minClientVersion ' 的新中繼資料屬性現在可以指出使用封裝所需的最低 NuGet 用戶端版本。</span><span class="sxs-lookup"><span data-stu-id="c4033-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="c4033-185">這項功能可協助封裝作者指定套件僅在特定版本的 NuGet 之後才可使用。</span><span class="sxs-lookup"><span data-stu-id="c4033-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="c4033-186">由於新的 `.nuspec` 功能會在 NuGet 2.5 之後加入，因此套件將能夠索取最低的 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="c4033-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="c4033-187">如果使用者已安裝 NuGet 2.5，並將套件識別為需要2.6，則會提供視覺提示給使用者，指出將無法安裝該套件。</span><span class="sxs-lookup"><span data-stu-id="c4033-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="c4033-188">接著，系統會引導使用者更新其 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="c4033-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="c4033-189">這將會改善套件開始安裝的現有體驗，但接著會失敗，指出已識別出無法辨識的架構版本。</span><span class="sxs-lookup"><span data-stu-id="c4033-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="c4033-190">在套件安裝期間，不再需要更新相依性</span><span class="sxs-lookup"><span data-stu-id="c4033-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="c4033-191">在 NuGet 2.5 之前，如果安裝的套件相依于已安裝在專案中的套件，則會在新的安裝過程中更新相依性，即使現有版本已滿足相依性也一樣。</span><span class="sxs-lookup"><span data-stu-id="c4033-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="c4033-192">從 NuGet 2.5 開始，如果已滿足相依性版本，則不會在其他套件安裝期間更新相依性。</span><span class="sxs-lookup"><span data-stu-id="c4033-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="c4033-193">**案例：**</span><span class="sxs-lookup"><span data-stu-id="c4033-193">**The scenario:**</span></span>

1. <span data-ttu-id="c4033-194">來源存放庫包含1.0.0 和1.0.2 版的套件 B。</span><span class="sxs-lookup"><span data-stu-id="c4033-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="c4033-195">它也包含相依于 B （> = 1.0.0）的套件 A。</span><span class="sxs-lookup"><span data-stu-id="c4033-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="c4033-196">假設目前的專案已安裝 package B 1.0.0 版。</span><span class="sxs-lookup"><span data-stu-id="c4033-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="c4033-197">現在您想要安裝套件 A。</span><span class="sxs-lookup"><span data-stu-id="c4033-197">Now you want to install package A.</span></span>

<span data-ttu-id="c4033-198">**在 NuGet 2.2 和更舊版本中：**</span><span class="sxs-lookup"><span data-stu-id="c4033-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="c4033-199">安裝套件 A 時，NuGet 會自動將 B 更新為1.0.2，即使現有的1.0.0 版已經滿足相依性版本條件約束，也就是 > = 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="c4033-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="c4033-200">**在 NuGet 2.5 和更新版本中：**</span><span class="sxs-lookup"><span data-stu-id="c4033-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="c4033-201">NuGet 將不再更新 B，因為它偵測到現有的1.0.0 版符合相依性版本條件約束。</span><span class="sxs-lookup"><span data-stu-id="c4033-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="c4033-202">如需這項變更的詳細背景，請閱讀詳細的[工作專案](http://nuget.codeplex.com/workitem/1681)，以及相關的[討論執行緒](http://nuget.codeplex.com/discussions/436712)。</span><span class="sxs-lookup"><span data-stu-id="c4033-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="c4033-203">nuget.exe 輸出 HTTP 要求的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="c4033-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="c4033-204">如果您要針對 nuget.exe 進行疑難排解，或只想知道作業期間所提出的 HTTP 要求，「詳細資訊明細」參數現在會輸出所有發出的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="c4033-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Nuget.exe 的 HTTP 輸出](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="c4033-206">nuget.exe push 現在支援 UNC 和資料夾來源</span><span class="sxs-lookup"><span data-stu-id="c4033-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="c4033-207">在 NuGet 2.5 之前，如果您嘗試對以 UNC 路徑或本機資料夾為基礎的套件來源執行「nuget.exe push」，推送將會失敗。</span><span class="sxs-lookup"><span data-stu-id="c4033-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="c4033-208">有了最近新增的階層式設定功能，nuget.exe 就必須以 UNC/資料夾來源或 HTTP 型 NuGet 資源庫為目標。</span><span class="sxs-lookup"><span data-stu-id="c4033-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="c4033-209">從 NuGet 2.5 開始，如果 nuget.exe 識別 UNC/資料夾來源，它就會對來源執行檔案複製。</span><span class="sxs-lookup"><span data-stu-id="c4033-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="c4033-210">現在可以使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="c4033-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="c4033-211">nuget.exe 支援明確指定的設定檔</span><span class="sxs-lookup"><span data-stu-id="c4033-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="c4033-212">存取設定的 nuget.exe 命令（「規格」和「套件」除外）現在支援新的 '-tlbimp.exe ' 選項，它會強制使用特定的設定檔來取代預設的設定檔，位於%AppData%\nuget\Nuget.Config。</span><span class="sxs-lookup"><span data-stu-id="c4033-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="c4033-213">範例：</span><span class="sxs-lookup"><span data-stu-id="c4033-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="c4033-214">原生專案的支援</span><span class="sxs-lookup"><span data-stu-id="c4033-214">Support for Native projects</span></span>

<span data-ttu-id="c4033-215">使用 NuGet 2.5，NuGet 工具現在可用於 Visual Studio 中的原生專案。</span><span class="sxs-lookup"><span data-stu-id="c4033-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="c4033-216">我們預期大部分的原生封裝都會利用上述的 MSBuild 匯入功能，並使用[CoApp 專案](http://coapp.org)所建立的工具。</span><span class="sxs-lookup"><span data-stu-id="c4033-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="c4033-217">如需詳細資訊，請參閱 coapp.org 網站上[有關此工具的詳細資料](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html)。</span><span class="sxs-lookup"><span data-stu-id="c4033-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="c4033-218">當封裝安裝到原生專案時，會為封裝引進「原生」的目標架構名稱，以在 \build、\content 和 \tools 中包含檔案。</span><span class="sxs-lookup"><span data-stu-id="c4033-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="c4033-219">[\`lib] 資料夾不適用於原生專案。</span><span class="sxs-lookup"><span data-stu-id="c4033-219">The \`lib\` folder is not used for native projects.</span></span>
