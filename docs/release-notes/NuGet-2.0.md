---
title: NuGet 2.0 版本資訊
description: NuGet 2.0 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776991"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="2f38c-103">NuGet 2.0 版本資訊</span><span class="sxs-lookup"><span data-stu-id="2f38c-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="2f38c-104">[NuGet 1.8 版本](../release-notes/nuget-1.8.md)  |  資訊[NuGet 2.1 版本](../release-notes/nuget-2.1.md)資訊</span><span class="sxs-lookup"><span data-stu-id="2f38c-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="2f38c-105">NuGet 2.0 已于2012年6月19日發行。</span><span class="sxs-lookup"><span data-stu-id="2f38c-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="2f38c-106">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="2f38c-106">Known Installation Issue</span></span>
<span data-ttu-id="2f38c-107">如果您執行的是 VS 2010 SP1，如果您已安裝較舊的版本，可能會在嘗試升級 NuGet 時發生安裝錯誤。</span><span class="sxs-lookup"><span data-stu-id="2f38c-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="2f38c-108">解決方法是直接卸載 NuGet，然後從 VS 延伸模組資源庫安裝它。</span><span class="sxs-lookup"><span data-stu-id="2f38c-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="2f38c-109"><https://support.microsoft.com/kb/2581019>如需詳細資訊，請參閱，或[直接移至 VS 修正程式](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="2f38c-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="2f38c-110">注意：如果 Visual Studio 不允許您卸載擴充功能 () 停用 [卸載] 按鈕，那麼您可能需要使用 [以系統管理員身分執行] 來重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="2f38c-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="2f38c-111">封裝還原同意現在已在使用中</span><span class="sxs-lookup"><span data-stu-id="2f38c-111">Package restore consent is now active</span></span>

<span data-ttu-id="2f38c-112">如同在 [套件還原同意的這篇文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)中所述，NuGet 2.0 現在將要求授與同意，才能讓套件還原上線並下載套件。</span><span class="sxs-lookup"><span data-stu-id="2f38c-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="2f38c-113">請確定您已透過 [套件管理員設定] 對話方塊或 EnableNuGetPackageRestore 環境變數來提供同意。</span><span class="sxs-lookup"><span data-stu-id="2f38c-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="2f38c-114">依目標 framework 分組相依性</span><span class="sxs-lookup"><span data-stu-id="2f38c-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="2f38c-115">從2.0 版開始，套件相依性會根據目標專案的 framework 設定檔而有所不同。</span><span class="sxs-lookup"><span data-stu-id="2f38c-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="2f38c-116">這是使用更新的架構來完成的 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="2f38c-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="2f38c-117">`<dependencies>`元素現在可以包含一組專案 `<group>` 。</span><span class="sxs-lookup"><span data-stu-id="2f38c-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="2f38c-118">每個群組都包含零或多個 `<dependency>` 元素和 `targetFramework` 屬性。</span><span class="sxs-lookup"><span data-stu-id="2f38c-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="2f38c-119">如果目標 framework 與目標專案架構設定檔相容，則會同時安裝群組內的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="2f38c-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="2f38c-120">例如：</span><span class="sxs-lookup"><span data-stu-id="2f38c-120">For example:</span></span>

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

<span data-ttu-id="2f38c-121">請注意，一個群組可以包含 **零個** 相依性。</span><span class="sxs-lookup"><span data-stu-id="2f38c-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="2f38c-122">在上述範例中，如果封裝安裝在以 Silverlight 3.0 或更新版本為目標的專案中，則不會安裝任何相依性。</span><span class="sxs-lookup"><span data-stu-id="2f38c-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="2f38c-123">如果封裝安裝在以 .NET 4.0 或更新版本為目標的專案中，則會安裝兩個相依性（jQuery 和 WebActivator）。</span><span class="sxs-lookup"><span data-stu-id="2f38c-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="2f38c-124">如果將套件安裝到以這兩個架構的早期版本為目標的專案，或任何其他架構，將會安裝 RouteMagic 1.1.0。</span><span class="sxs-lookup"><span data-stu-id="2f38c-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="2f38c-125">群組之間沒有任何繼承。</span><span class="sxs-lookup"><span data-stu-id="2f38c-125">There is no inheritance between groups.</span></span> <span data-ttu-id="2f38c-126">如果專案的目標 framework 符合群組的 `targetFramework` 屬性，則只會安裝該群組內的相依性。</span><span class="sxs-lookup"><span data-stu-id="2f38c-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="2f38c-127">封裝可以用兩種格式的其中一種來指定套件相依性：專案或群組的一般清單的舊格式 `<dependency>` 。</span><span class="sxs-lookup"><span data-stu-id="2f38c-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="2f38c-128">如果 `<group>` 使用格式，則無法將套件安裝到早于2.0 的 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="2f38c-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="2f38c-129">請注意，不允許混用這兩種格式。</span><span class="sxs-lookup"><span data-stu-id="2f38c-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="2f38c-130">例如，下列程式碼片段 **無效** ，將會被 NuGet 拒絕。</span><span class="sxs-lookup"><span data-stu-id="2f38c-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="2f38c-131">依目標 framework 將內容檔案和 PowerShell 腳本分組</span><span class="sxs-lookup"><span data-stu-id="2f38c-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="2f38c-132">除了元件參考以外，內容檔案和 PowerShell 腳本也可以依目標 framework 分組。</span><span class="sxs-lookup"><span data-stu-id="2f38c-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="2f38c-133">在用來指定目標 framework 的資料夾中找到的相同資料夾結構， `lib` 現在可以用相同的方式套用到 `content` 和 `tools` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2f38c-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="2f38c-134">例如：</span><span class="sxs-lookup"><span data-stu-id="2f38c-134">For example:</span></span>

```
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
```

<span data-ttu-id="2f38c-135">**注意**：因為 `init.ps1` 是在方案層級執行，而且不相依于任何個別專案，所以它必須直接放在 `tools` 資料夾下。</span><span class="sxs-lookup"><span data-stu-id="2f38c-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="2f38c-136">如果放置在特定架構的資料夾中，則會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="2f38c-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="2f38c-137">此外，NuGet 2.0 中的新功能是架構資料夾可以是 *空* 的，在這種情況下，NuGet 不會新增元件參考、新增內容檔案，或針對特定 framework 版本執行 PowerShell 腳本。</span><span class="sxs-lookup"><span data-stu-id="2f38c-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="2f38c-138">在上述範例中，資料夾 `content\net40` 是空的。</span><span class="sxs-lookup"><span data-stu-id="2f38c-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="2f38c-139">改善的 tab 鍵自動完成效能</span><span class="sxs-lookup"><span data-stu-id="2f38c-139">Improved tab completion performance</span></span>
<span data-ttu-id="2f38c-140">NuGet 封裝管理員主控台中的 tab 鍵自動完成功能已更新，可大幅提升效能。</span><span class="sxs-lookup"><span data-stu-id="2f38c-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="2f38c-141">按下 tab 鍵直到出現建議下拉式清單時，將會有很少的延遲。</span><span class="sxs-lookup"><span data-stu-id="2f38c-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="2f38c-142">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="2f38c-142">Bug Fixes</span></span>
<span data-ttu-id="2f38c-143">NuGet 2.0 包含許多 bug 修正，並著重于封裝還原的同意和效能。</span><span class="sxs-lookup"><span data-stu-id="2f38c-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="2f38c-144">如需 NuGet 2.0 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="2f38c-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
