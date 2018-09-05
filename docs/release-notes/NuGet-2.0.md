---
title: NuGet 2.0 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 2.0 版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547571"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="15d1f-103">NuGet 2.0 版本資訊</span><span class="sxs-lookup"><span data-stu-id="15d1f-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="15d1f-104">[NuGet 1.8 版本資訊](../release-notes/nuget-1.8.md) | [NuGet 2.1 版本資訊](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="15d1f-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="15d1f-105">NuGet 2.0 已於 2012 年 6 月 19 日發行。</span><span class="sxs-lookup"><span data-stu-id="15d1f-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="15d1f-106">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="15d1f-106">Known Installation Issue</span></span>
<span data-ttu-id="15d1f-107">如果您執行的 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您已安裝較舊版本。</span><span class="sxs-lookup"><span data-stu-id="15d1f-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="15d1f-108">因應措施是只解除安裝 NuGet，然後再從 VS 延伸模組資源庫進行安裝。</span><span class="sxs-lookup"><span data-stu-id="15d1f-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="15d1f-109">請參閱[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)如需詳細資訊，或[直接前往 VS hotfix](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="15d1f-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="15d1f-110">注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕已停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。</span><span class="sxs-lookup"><span data-stu-id="15d1f-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="15d1f-111">套件還原同意目前為作用中</span><span class="sxs-lookup"><span data-stu-id="15d1f-111">Package restore consent is now active</span></span>

<span data-ttu-id="15d1f-112">在此所述[將張貼在套件還原同意](http://blog.nuget.org/20120518/package-restore-and-consent.html)，NuGet 2.0 現在會要求同意要提供給啟用套件還原回到線上，並下載套件。</span><span class="sxs-lookup"><span data-stu-id="15d1f-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="15d1f-113">請確定您已提供同意透過套件管理員的組態對話方塊中或 EnableNuGetPackageRestore 環境變數。</span><span class="sxs-lookup"><span data-stu-id="15d1f-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="15d1f-114">依目標架構的群組相依性</span><span class="sxs-lookup"><span data-stu-id="15d1f-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="15d1f-115">從 2.0 版開始，相依性可能會不同的封裝會根據目標專案的 framework 設定檔。</span><span class="sxs-lookup"><span data-stu-id="15d1f-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="15d1f-116">這利用更新完成`.nuspec`結構描述。</span><span class="sxs-lookup"><span data-stu-id="15d1f-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="15d1f-117">`<dependencies>`項目現在可包含一組`<group>`項目。</span><span class="sxs-lookup"><span data-stu-id="15d1f-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="15d1f-118">每個群組包含零或多個`<dependency>`項目和`targetFramework`屬性。</span><span class="sxs-lookup"><span data-stu-id="15d1f-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="15d1f-119">如果目標架構與目標專案的 framework 設定檔相容時，會同時安裝在群組內的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="15d1f-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="15d1f-120">例如: </span><span class="sxs-lookup"><span data-stu-id="15d1f-120">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="15d1f-121">請注意，群組可以包含**零**相依性。</span><span class="sxs-lookup"><span data-stu-id="15d1f-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="15d1f-122">在上述範例中，如果封裝會安裝至專案目標 Silverlight 3.0 或更新版本，會不安裝任何相依性。</span><span class="sxs-lookup"><span data-stu-id="15d1f-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="15d1f-123">如果封裝被安裝至專案目標.NET 4.0 或更新版本，將會安裝兩個相依性，jQuery 和 WebActivator。</span><span class="sxs-lookup"><span data-stu-id="15d1f-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="15d1f-124">如果封裝已安裝至這些 2 的架構或任何其他架構的最早的版本為目標的專案中，將會安裝 RouteMagic 1.1.0。</span><span class="sxs-lookup"><span data-stu-id="15d1f-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="15d1f-125">群組之間沒有任何繼承。</span><span class="sxs-lookup"><span data-stu-id="15d1f-125">There is no inheritance between groups.</span></span> <span data-ttu-id="15d1f-126">如果專案的目標架構符合`targetFramework`群組，只有該群組內的相依性屬性將會安裝。</span><span class="sxs-lookup"><span data-stu-id="15d1f-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="15d1f-127">封裝可以指定兩種格式之一的封裝相依性： 舊格式的一般清單的`<dependency>`項目或群組。</span><span class="sxs-lookup"><span data-stu-id="15d1f-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="15d1f-128">如果`<group>`格式時，無法安裝此套件，NuGet 的版本早於 2.0。</span><span class="sxs-lookup"><span data-stu-id="15d1f-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="15d1f-129">請注意，不允許混用兩種格式。</span><span class="sxs-lookup"><span data-stu-id="15d1f-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="15d1f-130">例如，下列程式碼片段是**無效**和 nuget 將會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="15d1f-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="15d1f-131">群組的內容檔案和 PowerShell 指令碼，以依目標架構</span><span class="sxs-lookup"><span data-stu-id="15d1f-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="15d1f-132">除了組件參考，內容檔案和 PowerShell 指令碼可以也會依目標 framework。</span><span class="sxs-lookup"><span data-stu-id="15d1f-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="15d1f-133">相同的資料夾結構中找到`lib`資料夾，用於指定目標 framework 現在可套用至相同的方式`content`和`tools`資料夾。</span><span class="sxs-lookup"><span data-stu-id="15d1f-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="15d1f-134">例如: </span><span class="sxs-lookup"><span data-stu-id="15d1f-134">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="15d1f-135">**附註**： 因為`init.ps1`方案層級執行，且不相依於任何個別的專案，它必須放在正下方`tools`資料夾。</span><span class="sxs-lookup"><span data-stu-id="15d1f-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="15d1f-136">如果用來放置架構特有資料夾內，將會忽略它。</span><span class="sxs-lookup"><span data-stu-id="15d1f-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="15d1f-137">此外，NuGet 2.0 中的新功能是可以在架構資料夾*空*，在此情況下，NuGet 不會新增組件參考、 加入內容的檔案或執行特定的 framework 版本的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="15d1f-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="15d1f-138">在範例中，資料夾`content\net40`是空的。</span><span class="sxs-lookup"><span data-stu-id="15d1f-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="15d1f-139">改善的索引標籤完成效能</span><span class="sxs-lookup"><span data-stu-id="15d1f-139">Improved tab completion performance</span></span>
<span data-ttu-id="15d1f-140">已更新 NuGet 套件管理員主控台中的索引標籤完成功能以大幅改善效能。</span><span class="sxs-lookup"><span data-stu-id="15d1f-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="15d1f-141">會從建議下拉式清單中出現之前按下 tab 鍵的時間少很多延遲。</span><span class="sxs-lookup"><span data-stu-id="15d1f-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="15d1f-142">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="15d1f-142">Bug Fixes</span></span>
<span data-ttu-id="15d1f-143">NuGet 2.0 包含套件還原同意和效能，特別強調的許多錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="15d1f-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="15d1f-144">如需完整的工作清單項目中已修正 NuGet 2.0，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="15d1f-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
