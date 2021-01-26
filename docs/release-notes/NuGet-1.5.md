---
title: NuGet 1.5 版本資訊
description: NuGet 1.5 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777098"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="151f8-103">NuGet 1.5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="151f8-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="151f8-104">[NuGet 1.4 版本](../release-notes/nuget-1.4.md)  |  資訊[NuGet 1.6 版本](../release-notes/nuget-1.6.md)資訊</span><span class="sxs-lookup"><span data-stu-id="151f8-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="151f8-105">NuGet 1.5 已于2011年8月30日發行。</span><span class="sxs-lookup"><span data-stu-id="151f8-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="151f8-106">功能</span><span class="sxs-lookup"><span data-stu-id="151f8-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="151f8-107">具有預先安裝 NuGet 套件的專案範本</span><span class="sxs-lookup"><span data-stu-id="151f8-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="151f8-108">建立新的 ASP.NET MVC 3 專案範本時，專案中包含的 jQuery 腳本程式庫實際上是藉由安裝 NuGet 套件來放置。</span><span class="sxs-lookup"><span data-stu-id="151f8-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="151f8-109">ASP.NET MVC 3 專案範本包含一組 NuGet 套件，可在叫用專案範本時一併安裝。</span><span class="sxs-lookup"><span data-stu-id="151f8-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="151f8-110">包含 NuGet 套件與專案範本的這項功能現在是 NuGet 的功能， _任何_ 專案範本現在都可以利用。</span><span class="sxs-lookup"><span data-stu-id="151f8-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="151f8-111">如需這項功能的詳細資訊，請閱讀此 [功能開發人員的這篇 blog 文章](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)。</span><span class="sxs-lookup"><span data-stu-id="151f8-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="151f8-112">明確的元件參考</span><span class="sxs-lookup"><span data-stu-id="151f8-112">Explicit Assembly References</span></span>

<span data-ttu-id="151f8-113">加入新的專案 `<references />` ，用來明確指定應參考封裝內的哪些元件。</span><span class="sxs-lookup"><span data-stu-id="151f8-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="151f8-114">例如，如果您新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="151f8-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="151f8-115">然後，只 `xunit.dll` 會 `xunit.extensions.dll` 從資料夾的適當 [架構/設定檔子](../reference/nuspec.md#explicit-assembly-references) 資料夾中參考和， `lib` 即使資料夾中有其他元件也一樣。</span><span class="sxs-lookup"><span data-stu-id="151f8-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="151f8-116">如果省略此元素，則會套用一般行為，也就是參考資料夾中的每個元件 `lib` 。</span><span class="sxs-lookup"><span data-stu-id="151f8-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="151f8-117">__這項功能的用途為何？__</span><span class="sxs-lookup"><span data-stu-id="151f8-117">__What is this feature used for?__</span></span>

<span data-ttu-id="151f8-118">這項功能僅支援設計階段元件。</span><span class="sxs-lookup"><span data-stu-id="151f8-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="151f8-119">例如，使用程式碼合約時，合約元件必須位於它們所擴充之執行時間元件的旁邊，以便 Visual Studio 可以找到它們，但是合約元件不應實際由專案參考，也不應該複製到 `bin` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="151f8-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="151f8-120">同樣地，這項功能可用於單元測試架構（例如 XUnit），這類架構需要在執行時間元件旁邊找出其工具元件，但不能從專案參考中排除。</span><span class="sxs-lookup"><span data-stu-id="151f8-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="151f8-121">已新增在 nuspec 中排除檔案的能力。</span><span class="sxs-lookup"><span data-stu-id="151f8-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="151f8-122">檔案 `<file>` 內的專案 `.nuspec` 可以用來包含特定檔案或使用萬用字元的檔案集合。</span><span class="sxs-lookup"><span data-stu-id="151f8-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="151f8-123">使用萬用字元時，不會有任何方法可以排除包含之檔案的特定子集。</span><span class="sxs-lookup"><span data-stu-id="151f8-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="151f8-124">例如，假設您想要一個資料夾中的所有文字檔，但有特定的檔案。</span><span class="sxs-lookup"><span data-stu-id="151f8-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="151f8-125">使用分號來指定多個檔案。</span><span class="sxs-lookup"><span data-stu-id="151f8-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="151f8-126">或使用萬用字元來排除一組檔案，例如所有備份檔案</span><span class="sxs-lookup"><span data-stu-id="151f8-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="151f8-127">使用對話方塊來移除套件會提示移除相依性</span><span class="sxs-lookup"><span data-stu-id="151f8-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="151f8-128">卸載具有相依性的套件時，NuGet 會提示您允許移除套件的相依性和套件。</span><span class="sxs-lookup"><span data-stu-id="151f8-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![移除相依封裝](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="151f8-130">`Get-Package` 命令改進</span><span class="sxs-lookup"><span data-stu-id="151f8-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="151f8-131">`Get-Package`命令現在支援 `-ProjectName` 參數。</span><span class="sxs-lookup"><span data-stu-id="151f8-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="151f8-132">命令</span><span class="sxs-lookup"><span data-stu-id="151f8-132">So the command</span></span>

```
Get-Package –ProjectName A
```

<span data-ttu-id="151f8-133">會列出安裝在專案 A 中的所有套件。</span><span class="sxs-lookup"><span data-stu-id="151f8-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="151f8-134">支援需要驗證的 proxy</span><span class="sxs-lookup"><span data-stu-id="151f8-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="151f8-135">在需要驗證的 proxy 後方使用 NuGet 時，NuGet 現在會提示您輸入 proxy 認證。</span><span class="sxs-lookup"><span data-stu-id="151f8-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="151f8-136">輸入認證可讓 NuGet 連接至遠端存放庫。</span><span class="sxs-lookup"><span data-stu-id="151f8-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="151f8-137">支援需要驗證的儲存機制</span><span class="sxs-lookup"><span data-stu-id="151f8-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="151f8-138">NuGet 現在支援連接到需要基本或 NTLM 驗證的 [私人存放庫](../hosting-packages/local-feeds.md) 。</span><span class="sxs-lookup"><span data-stu-id="151f8-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="151f8-139">未來的版本將會新增摘要式驗證的支援。</span><span class="sxs-lookup"><span data-stu-id="151f8-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="151f8-140">Nuget.org 存放庫的效能改進</span><span class="sxs-lookup"><span data-stu-id="151f8-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="151f8-141">我們已對 nuget.org 資源庫進行數個效能改進，讓套件清單和搜尋更快。</span><span class="sxs-lookup"><span data-stu-id="151f8-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="151f8-142">解決方案對話方塊專案篩選</span><span class="sxs-lookup"><span data-stu-id="151f8-142">Solution dialog project filtering</span></span>
<span data-ttu-id="151f8-143">在 [方案層級] 對話方塊中，當提示您要安裝哪些專案時，我們只會顯示與所選套件相容的專案。</span><span class="sxs-lookup"><span data-stu-id="151f8-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="151f8-144">封裝版本資訊</span><span class="sxs-lookup"><span data-stu-id="151f8-144">Package Release Notes</span></span>
<span data-ttu-id="151f8-145">NuGet 套件現在包含版本資訊的支援。</span><span class="sxs-lookup"><span data-stu-id="151f8-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="151f8-146">版本資訊只會在查看套件的 _更新_ 時顯示，因此將它們新增至您的第一個版本並不合理。</span><span class="sxs-lookup"><span data-stu-id="151f8-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![[更新] 索引標籤中的版本資訊](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="151f8-148">若要將版本資訊加入封裝，請在 NuSpec 檔中使用新的 `<releaseNotes />` 中繼資料元素。</span><span class="sxs-lookup"><span data-stu-id="151f8-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="151f8-149">nuspec &ltfiles/ &gt; 改進</span><span class="sxs-lookup"><span data-stu-id="151f8-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="151f8-150">檔案 `.nuspec` 現在允許空的 `<files />` 元素，這會告知 nuget.exe 不包含封裝中的任何檔案。</span><span class="sxs-lookup"><span data-stu-id="151f8-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="151f8-151">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="151f8-151">Bug Fixes</span></span>
<span data-ttu-id="151f8-152">NuGet 1.5 總共修正了107個工作專案。</span><span class="sxs-lookup"><span data-stu-id="151f8-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="151f8-153">這些標記為 bug 的103。</span><span class="sxs-lookup"><span data-stu-id="151f8-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="151f8-154">如需 NuGet 1.5 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="151f8-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="151f8-155">Bug 修正值得注意：</span><span class="sxs-lookup"><span data-stu-id="151f8-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="151f8-156">[問題 1273](http://nuget.codeplex.com/workitem/1273)： `packages.config` 依字母順序排序封裝和移除額外的空白字元，讓版本控制更容易使用。</span><span class="sxs-lookup"><span data-stu-id="151f8-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="151f8-157">[問題 844](http://nuget.codeplex.com/workitem/844)：現在已將版本號碼正規化，以便 `Install-Package 1.0` 在具有版本的套件上運作 `1.0.0` 。</span><span class="sxs-lookup"><span data-stu-id="151f8-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="151f8-158">[問題 1060](http://nuget.codeplex.com/workitem/1060)：使用 nuget.exe 建立封裝時，旗標會 `-Version` 覆寫 `<version />` 元素。</span><span class="sxs-lookup"><span data-stu-id="151f8-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
