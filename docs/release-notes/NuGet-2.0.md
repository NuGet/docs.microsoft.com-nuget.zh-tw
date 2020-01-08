---
title: NuGet 2.0 版本資訊
description: NuGet 2.0 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383063"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="7238d-103">NuGet 2.0 版本資訊</span><span class="sxs-lookup"><span data-stu-id="7238d-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="7238d-104">[Nuget 1.8 版本](../release-notes/nuget-1.8.md)資訊 | [nuget 2.1 版本](../release-notes/nuget-2.1.md)資訊</span><span class="sxs-lookup"><span data-stu-id="7238d-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="7238d-105">NuGet 2.0 已于2012年6月19日發行。</span><span class="sxs-lookup"><span data-stu-id="7238d-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="7238d-106">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="7238d-106">Known Installation Issue</span></span>
<span data-ttu-id="7238d-107">如果您執行 VS 2010 SP1，如果您已安裝舊版，則嘗試升級 NuGet 時可能會發生安裝錯誤。</span><span class="sxs-lookup"><span data-stu-id="7238d-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="7238d-108">因應措施是直接卸載 NuGet，然後從 VS 延伸模組資源庫進行安裝。</span><span class="sxs-lookup"><span data-stu-id="7238d-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="7238d-109">如需詳細資訊，請參閱 <https://support.microsoft.com/kb/2581019>，或[直接移至 VS 提供程式](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="7238d-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="7238d-110">注意：如果 Visual Studio 不允許您卸載擴充功能（[卸載] 按鈕已停用），您可能需要使用 [以系統管理員身分執行] 重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="7238d-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="7238d-111">套件還原同意現已啟用</span><span class="sxs-lookup"><span data-stu-id="7238d-111">Package restore consent is now active</span></span>

<span data-ttu-id="7238d-112">如這[篇關於封裝還原同意文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)中所述，NuGet 2.0 現在需要授與同意，才能讓套件還原上線並下載套件。</span><span class="sxs-lookup"><span data-stu-id="7238d-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="7238d-113">請確定您已透過 [套件管理員設定] 對話方塊或 EnableNuGetPackageRestore 環境變數提供同意。</span><span class="sxs-lookup"><span data-stu-id="7238d-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="7238d-114">依目標 framework 群組相依性</span><span class="sxs-lookup"><span data-stu-id="7238d-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="7238d-115">從2.0 版開始，封裝相依性可能會根據目標專案的 framework 設定檔而有所不同。</span><span class="sxs-lookup"><span data-stu-id="7238d-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="7238d-116">這項作業是使用已更新的 `.nuspec` 架構來完成。</span><span class="sxs-lookup"><span data-stu-id="7238d-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="7238d-117">`<dependencies>` 元素現在可以包含一組 `<group>` 元素。</span><span class="sxs-lookup"><span data-stu-id="7238d-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="7238d-118">每個群組都包含零個或多個 `<dependency>` 元素和一個 `targetFramework` 屬性。</span><span class="sxs-lookup"><span data-stu-id="7238d-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="7238d-119">如果目標 framework 與目標專案架構設定檔相容，則會同時安裝群組內的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="7238d-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="7238d-120">例如：</span><span class="sxs-lookup"><span data-stu-id="7238d-120">For example:</span></span>

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

<span data-ttu-id="7238d-121">請注意，群組可以包含**零個**相依性。</span><span class="sxs-lookup"><span data-stu-id="7238d-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="7238d-122">在上述範例中，如果將套件安裝到以 Silverlight 3.0 或更新版本為目標的專案中，則不會安裝任何相依性。</span><span class="sxs-lookup"><span data-stu-id="7238d-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="7238d-123">如果將封裝安裝到以 .NET 4.0 或更新版本為目標的專案中，將會安裝兩個相依性（jQuery 和 WebActivator）。</span><span class="sxs-lookup"><span data-stu-id="7238d-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="7238d-124">如果將封裝安裝到以這兩個架構的早期版本為目標的專案中，或任何其他架構，則會安裝 RouteMagic 1.1.0。</span><span class="sxs-lookup"><span data-stu-id="7238d-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="7238d-125">群組之間沒有任何繼承。</span><span class="sxs-lookup"><span data-stu-id="7238d-125">There is no inheritance between groups.</span></span> <span data-ttu-id="7238d-126">如果專案的目標 framework 符合群組的 `targetFramework` 屬性，則只會安裝該群組中的相依性。</span><span class="sxs-lookup"><span data-stu-id="7238d-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="7238d-127">封裝可以使用兩種格式的其中一種來指定封裝相依性： `<dependency>` 專案或群組之一般清單的舊格式。</span><span class="sxs-lookup"><span data-stu-id="7238d-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="7238d-128">如果使用 `<group>` 格式，套件就無法安裝在2.0 之前的 NuGet 版本中。</span><span class="sxs-lookup"><span data-stu-id="7238d-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="7238d-129">請注意，不允許混用這兩種格式。</span><span class="sxs-lookup"><span data-stu-id="7238d-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="7238d-130">例如，下列程式碼片段**無效**，NuGet 將會拒絕。</span><span class="sxs-lookup"><span data-stu-id="7238d-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="7238d-131">依目標架構將內容檔案和 PowerShell 腳本分組</span><span class="sxs-lookup"><span data-stu-id="7238d-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="7238d-132">除了元件參考之外，也可以依目標 framework 將內容檔案和 PowerShell 腳本分組。</span><span class="sxs-lookup"><span data-stu-id="7238d-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="7238d-133">在用來指定目標 framework 的 `lib` 資料夾中找到的相同資料夾結構，現在可以用相同方式套用至 `content` 和 `tools` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="7238d-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="7238d-134">例如：</span><span class="sxs-lookup"><span data-stu-id="7238d-134">For example:</span></span>

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

<span data-ttu-id="7238d-135">**注意**：因為 `init.ps1` 是在方案層級執行，而且不相依于任何個別專案，所以必須直接放在 `tools` 資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="7238d-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="7238d-136">如果放在架構特定的資料夾內，則會忽略它。</span><span class="sxs-lookup"><span data-stu-id="7238d-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="7238d-137">此外，NuGet 2.0 中的一項新功能是，架構資料夾可以是*空*的，在這種情況下，nuget 將不會新增元件參考、新增內容檔案或針對特定架構版本執行 PowerShell 腳本。</span><span class="sxs-lookup"><span data-stu-id="7238d-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="7238d-138">在上述範例中，`content\net40` 的資料夾是空的。</span><span class="sxs-lookup"><span data-stu-id="7238d-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="7238d-139">改良的 tab 鍵自動完成效能</span><span class="sxs-lookup"><span data-stu-id="7238d-139">Improved tab completion performance</span></span>
<span data-ttu-id="7238d-140">NuGet 套件管理員主控台中的 tab 鍵自動完成功能已更新，可大幅改善效能。</span><span class="sxs-lookup"><span data-stu-id="7238d-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="7238d-141">按下 tab 鍵，直到出現 [建議] 下拉式清單時，才會有更少的延遲。</span><span class="sxs-lookup"><span data-stu-id="7238d-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="7238d-142">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="7238d-142">Bug Fixes</span></span>
<span data-ttu-id="7238d-143">NuGet 2.0 包含許多 bug 修正，並著重于封裝還原同意和效能。</span><span class="sxs-lookup"><span data-stu-id="7238d-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="7238d-144">如需 NuGet 2.0 中已修正之工作專案的完整清單，請參閱[此版本的 NuGet 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="7238d-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
