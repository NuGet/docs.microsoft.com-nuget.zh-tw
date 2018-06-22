---
title: NuGet 1.5 版本資訊
description: 版本資訊包含已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.5。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f2f7ebe718ce943faa31b7e19395eead8726648
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821339"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="e5762-103">NuGet 1.5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="e5762-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="e5762-104">[NuGet 1.4 版本資訊](../release-notes/nuget-1.4.md) | [NuGet 1.6 版本資訊](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="e5762-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="e5762-105">NuGet 1.5 已於 2011 年 8 月 30 日發行。</span><span class="sxs-lookup"><span data-stu-id="e5762-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="e5762-106">功能</span><span class="sxs-lookup"><span data-stu-id="e5762-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="e5762-107">專案範本以預先安裝的 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="e5762-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="e5762-108">建立新的 ASP.NET MVC 3 專案範本時，包含在專案中的 jQuery 指令碼程式庫會實際放在該處安裝 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="e5762-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="e5762-109">ASP.NET MVC 3 專案範本包含一組叫用的專案範本時，取得安裝的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="e5762-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="e5762-110">這項功能包含 NuGet 封裝的專案範本現在是 NuGet 的功能，_任何_專案範本現在可以充分利用。</span><span class="sxs-lookup"><span data-stu-id="e5762-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="e5762-111">如需有關這項功能的詳細資訊，請閱讀本[功能的開發人員部落格文章](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e5762-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="e5762-112">明確的組件參考</span><span class="sxs-lookup"><span data-stu-id="e5762-112">Explicit Assembly References</span></span>

<span data-ttu-id="e5762-113">加入新`<references />`用來明確指定組件內的項目應該要參考的封裝。</span><span class="sxs-lookup"><span data-stu-id="e5762-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="e5762-114">例如，如果您將加入下列：</span><span class="sxs-lookup"><span data-stu-id="e5762-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="e5762-115">然後只`xunit.dll`和`xunit.extensions.dll`會參考適當[framework/設定檔的子資料夾](../reference/nuspec.md#explicit-assembly-references)的`lib`即使資料夾中沒有其他組件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5762-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="e5762-116">如果省略此元素，則很平常的行為，也就是參考中的每個組件適用於`lib`資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5762-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="e5762-117">__這項功能的使用是？__</span><span class="sxs-lookup"><span data-stu-id="e5762-117">__What is this feature used for?__</span></span>

<span data-ttu-id="e5762-118">此功能支援設計階段只有組件。</span><span class="sxs-lookup"><span data-stu-id="e5762-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="e5762-119">比方說，當使用程式碼合約，合約組件必須為它們擴大，讓 Visual Studio 可以找到它們，但應該不實際專案所參考的合約組件，並不會複製到執行階段組件旁邊`bin`資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5762-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="e5762-120">同樣地，此功能可用來針對單元測試架構，例如 XUnit 需要旁的執行階段組件，但排除專案參考其工具組件。</span><span class="sxs-lookup"><span data-stu-id="e5762-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="e5762-121">若要排除在.nuspec 檔案新增的功能</span><span class="sxs-lookup"><span data-stu-id="e5762-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="e5762-122">`<file>`內的項目`.nuspec`檔案可以用來包含特定的檔案或一組使用萬用字元的檔案。</span><span class="sxs-lookup"><span data-stu-id="e5762-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="e5762-123">使用萬用字元時, 沒有任何方法可以排除的特定子集包含的檔案。</span><span class="sxs-lookup"><span data-stu-id="e5762-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="e5762-124">例如，假設您想要特定以外之資料夾中的所有文字檔案。</span><span class="sxs-lookup"><span data-stu-id="e5762-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="e5762-125">使用分號來指定多個檔案。</span><span class="sxs-lookup"><span data-stu-id="e5762-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="e5762-126">或使用萬用字元來排除一組檔案，例如所有備份檔案</span><span class="sxs-lookup"><span data-stu-id="e5762-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="e5762-127">移除封裝使用的對話方塊會提示您移除相依性</span><span class="sxs-lookup"><span data-stu-id="e5762-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="e5762-128">當正在解除安裝的封裝相依性，NuGet 會提示，可讓封裝的相依性，以及套件移除。</span><span class="sxs-lookup"><span data-stu-id="e5762-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![移除相依的套件](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="e5762-130">`Get-Package` 命令的改進</span><span class="sxs-lookup"><span data-stu-id="e5762-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="e5762-131">`Get-Package`命令現在支援`-ProjectName`參數。</span><span class="sxs-lookup"><span data-stu-id="e5762-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="e5762-132">因此命令</span><span class="sxs-lookup"><span data-stu-id="e5762-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="e5762-133">會列出所有專案 A.中安裝的封裝</span><span class="sxs-lookup"><span data-stu-id="e5762-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="e5762-134">Proxy 需要驗證的支援</span><span class="sxs-lookup"><span data-stu-id="e5762-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="e5762-135">當使用 NuGet 需要驗證的 proxy 後面時，NuGet 會現在會提示輸入 proxy 認證。</span><span class="sxs-lookup"><span data-stu-id="e5762-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="e5762-136">輸入認證，可讓連接至遠端儲存機制的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="e5762-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="e5762-137">需要驗證的儲存機制的支援</span><span class="sxs-lookup"><span data-stu-id="e5762-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="e5762-138">NuGet 現在支援連接至[私用儲存機制](../hosting-packages/local-feeds.md)需要基本或 NTLM 驗證。</span><span class="sxs-lookup"><span data-stu-id="e5762-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="e5762-139">在未來版本將會加入摘要式驗證的支援。</span><span class="sxs-lookup"><span data-stu-id="e5762-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="e5762-140">Nuget.org 儲存機制的效能增強功能</span><span class="sxs-lookup"><span data-stu-id="e5762-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="e5762-141">我們已經 nuget.org 圖庫 列出及更快速搜尋套件的數個效能改良。</span><span class="sxs-lookup"><span data-stu-id="e5762-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="e5762-142">方案對話方塊專案篩選</span><span class="sxs-lookup"><span data-stu-id="e5762-142">Solution dialog project filtering</span></span>
<span data-ttu-id="e5762-143">在方案層級對話方塊中，若要安裝哪些專案的提示時，我們只會顯示所選取封裝相容的專案。</span><span class="sxs-lookup"><span data-stu-id="e5762-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="e5762-144">封裝的版本資訊</span><span class="sxs-lookup"><span data-stu-id="e5762-144">Package Release Notes</span></span>
<span data-ttu-id="e5762-145">NuGet 封裝現在包含版本資訊的支援。</span><span class="sxs-lookup"><span data-stu-id="e5762-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="e5762-146">版本會資訊向上只顯示檢視時_更新_是封裝，因此不會更有意義，將它們加入您的第一次釋放。</span><span class="sxs-lookup"><span data-stu-id="e5762-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![在 [更新] 索引標籤中的版本資訊](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="e5762-148">若要加入封裝的版本資訊，請使用 新`<releaseNotes />`NuSpec 檔中的中繼資料元素。</span><span class="sxs-lookup"><span data-stu-id="e5762-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="e5762-149">.nuspec & ltfiles /&gt;改進</span><span class="sxs-lookup"><span data-stu-id="e5762-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="e5762-150">`.nuspec`檔現在可讓空白`<files />`元素，其會告知 nuget.exe 加入封裝中的任何檔案。</span><span class="sxs-lookup"><span data-stu-id="e5762-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e5762-151">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="e5762-151">Bug Fixes</span></span>
<span data-ttu-id="e5762-152">NuGet 1.5 有工作項目固定 107 總數。</span><span class="sxs-lookup"><span data-stu-id="e5762-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="e5762-153">這些 103 被標示為錯誤。</span><span class="sxs-lookup"><span data-stu-id="e5762-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="e5762-154">如需完整的工作清單項目固定在 NuGet 1.5，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="e5762-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="e5762-155">值得注意的 bug 修正：</span><span class="sxs-lookup"><span data-stu-id="e5762-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="e5762-156">[問題 1273年](http://nuget.codeplex.com/workitem/1273)： 進行`packages.config`易記藉由依字母順序排序封裝，並移除多餘的空白字元的多個版本控制。</span><span class="sxs-lookup"><span data-stu-id="e5762-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="e5762-157">[問題 844](http://nuget.codeplex.com/workitem/844)： 現在會正規化版本號碼以便`Install-Package 1.0`版封裝適用於`1.0.0`。</span><span class="sxs-lookup"><span data-stu-id="e5762-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="e5762-158">[問題 1060年](http://nuget.codeplex.com/workitem/1060)： 使用 nuget.exe，建立封裝時`-Version`覆寫的旗標`<version />`項目。</span><span class="sxs-lookup"><span data-stu-id="e5762-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
