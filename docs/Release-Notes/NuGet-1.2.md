---
title: "NuGet 1.2 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr NuGet 1.2 的版本資訊。"
keywords: "NuGet 1.2 的版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cb9eb1cb8fc3a77fc297e04ce73aaf8e24fc557a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-12-release-notes"></a><span data-ttu-id="3dffa-104">NuGet 1.2 的版本資訊</span><span class="sxs-lookup"><span data-stu-id="3dffa-104">NuGet 1.2 Release Notes</span></span>

<span data-ttu-id="3dffa-105">[NuGet 1.0 和 1.1 版本資訊](../release-notes/nuget-1.1.md) | [NuGet 1.3 版本資訊](../release-notes/nuget-1.3.md)</span><span class="sxs-lookup"><span data-stu-id="3dffa-105">[NuGet 1.0 and 1.1 Release Notes](../release-notes/nuget-1.1.md) | [NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md)</span></span>

<span data-ttu-id="3dffa-106">NuGet 1.2 起已於 2011 年 3 月 30 日發行。</span><span class="sxs-lookup"><span data-stu-id="3dffa-106">NuGet 1.2 was released on March 30, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="3dffa-107">新功能</span><span class="sxs-lookup"><span data-stu-id="3dffa-107">New Features</span></span>

### <a name="framework-profile-support"></a><span data-ttu-id="3dffa-108">支援 framework 設定檔</span><span class="sxs-lookup"><span data-stu-id="3dffa-108">Framework Profile Support</span></span>

<span data-ttu-id="3dffa-109">從開始，NuGet 會支援具有程式庫以不同的架構為目標。</span><span class="sxs-lookup"><span data-stu-id="3dffa-109">From the start, NuGet supported having libraries target different frameworks.</span></span> <span data-ttu-id="3dffa-110">但現在封裝可能包含以特定的設定檔，例如 Windows Phone 設定檔為目標的組件。</span><span class="sxs-lookup"><span data-stu-id="3dffa-110">But now packages may contain assemblies that target specific profiles such as the Windows Phone profile.</span></span> <span data-ttu-id="3dffa-111">若要以特定架構的設定檔為目標，附加破折號，後面接著的設定檔的縮寫。</span><span class="sxs-lookup"><span data-stu-id="3dffa-111">To target a specific profile of a framework, append a dash followed by the profile abbreviation.</span></span> <span data-ttu-id="3dffa-112">例如，若要在 Windows Phone (也稱為 Windows Phone 7) 上執行的 SilverLight，您可以將組件 sl3 wp 資料夾如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="3dffa-112">For example, to target SilverLight running on a Windows Phone (aka Windows Phone 7), you can put an assembly in the sl3-wp folder as demonstrated in the following screenshot.</span></span>

![Framework 設定檔資料夾版面配置](./media/framework-profile-support.png)

<span data-ttu-id="3dffa-114">您可能會要求為什麼我們不只要選擇"wp7"做為 moniker。</span><span class="sxs-lookup"><span data-stu-id="3dffa-114">You might ask why we didn’t just choose to use “wp7” as the moniker.</span></span> <span data-ttu-id="3dffa-115">部分，我們所預期，Windows Phone 7 可能在未來執行較新版的 Silverlight，在此情況下，您可能需要更特定的對您的 framework 設定檔是以。</span><span class="sxs-lookup"><span data-stu-id="3dffa-115">In part, we’re anticipating that Windows Phone 7 might run a newer version of Silverlight in the future, in which case you may need to be more specific about which framework profile you’re targetting.</span></span>

### <a name="automatically-add-binding-redirects"></a><span data-ttu-id="3dffa-116">繫結重新導向自動加入</span><span class="sxs-lookup"><span data-stu-id="3dffa-116">Automatically Add Binding Redirects</span></span>

<span data-ttu-id="3dffa-117">當強式名稱組件的安裝套件，NuGet 現在可以偵測專案需要繫結重新導向加入至編譯，並將其自動加入專案中的組態檔的情況。</span><span class="sxs-lookup"><span data-stu-id="3dffa-117">When installing a package with strong named assemblies, NuGet can now detect cases where the project requires binding redirects to be added to the configuration file in order for the project to compile and add them automatically.</span></span> <span data-ttu-id="3dffa-118">第 3 部分 David Ebbo 部落格文章系列的 NuGet 版本控制標題為 「[透過繫結重新導向的統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"涵蓋更多詳細資料中的這項功能的目的。</span><span class="sxs-lookup"><span data-stu-id="3dffa-118">Part 3 of David Ebbo’s blog post series on NuGet Versioning entitled “[Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)” covers the purpose of this feature in more details.</span></span>

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a><span data-ttu-id="3dffa-119">指定 Framework 組件參考 (GAC)</span><span class="sxs-lookup"><span data-stu-id="3dffa-119">Specifying Framework Assembly References (GAC)</span></span>

<span data-ttu-id="3dffa-120">在某些情況下，封裝可能取決於為.NET Framework 中的組件。</span><span class="sxs-lookup"><span data-stu-id="3dffa-120">In some cases, a package may depend on an assembly that’s in the .NET Framework.</span></span> <span data-ttu-id="3dffa-121">嚴格來說，它不一定需要取用者，您的封裝參考 framework 組件。</span><span class="sxs-lookup"><span data-stu-id="3dffa-121">Strictly speaking, it’s not always necessary that the consumer of your package reference the framework assembly.</span></span> <span data-ttu-id="3dffa-122">但在某些情況下，是很重要的例如，開發人員必須撰寫程式碼對該組件中的型別才能使用您的封裝。</span><span class="sxs-lookup"><span data-stu-id="3dffa-122">But in some cases, it's important, such as when the developer needs to code against types in that assembly in order to use your package.</span></span> <span data-ttu-id="3dffa-123">新`frameworkAssemblies`項目，項目的子項目中繼資料，可讓您指定的一組`frameworkAssembly`Framework 組件在 GAC 中所指向的項目。</span><span class="sxs-lookup"><span data-stu-id="3dffa-123">The new `frameworkAssemblies` element, a child element of the metadata element, allows you to specify a set of `frameworkAssembly` elements pointing to a Framework assembly in the GAC.</span></span> <span data-ttu-id="3dffa-124">請注意在 Framework 組件上的強調。</span><span class="sxs-lookup"><span data-stu-id="3dffa-124">Note the emphasis on Framework assembly.</span></span>
<span data-ttu-id="3dffa-125">假設為每部電腦上，.NET Framework 的一部分時，這些組件不會包含在封裝中。</span><span class="sxs-lookup"><span data-stu-id="3dffa-125">These assemblies are not included in your package as they are assumed to be on every machine  as part of the .NET Framework.</span></span> <span data-ttu-id="3dffa-126">下表列出的屬性`frameworkAssembly`項目。</span><span class="sxs-lookup"><span data-stu-id="3dffa-126">The following table lists attributes of the `frameworkAssembly` element.</span></span>


|<span data-ttu-id="3dffa-127">屬性</span><span class="sxs-lookup"><span data-stu-id="3dffa-127">Attribute</span></span> |<span data-ttu-id="3dffa-128">描述</span><span class="sxs-lookup"><span data-stu-id="3dffa-128">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="3dffa-129">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="3dffa-129">**assemblyName**</span></span>|<span data-ttu-id="3dffa-130">*需要*。</span><span class="sxs-lookup"><span data-stu-id="3dffa-130">*Required*.</span></span> <span data-ttu-id="3dffa-131">例如，組件名稱`System.Net`。</span><span class="sxs-lookup"><span data-stu-id="3dffa-131">Name of the assembly such as `System.Net`.</span></span>|
|<span data-ttu-id="3dffa-132">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="3dffa-132">**targetFramework**</span></span>|<span data-ttu-id="3dffa-133">*選擇性*。</span><span class="sxs-lookup"><span data-stu-id="3dffa-133">*Optional*.</span></span> <span data-ttu-id="3dffa-134">可讓您指定架構和設定檔名稱 （或別名），例如"net40"或"sl4"適用於這個 framework 組件。</span><span class="sxs-lookup"><span data-stu-id="3dffa-134">Allows specifying a framework and profile name (or alias) that this framework assembly applies to such as "net40" or "sl4".</span></span> <span data-ttu-id="3dffa-135">使用相同的格式中所述[支援多個目標架構](../create-packages/supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="3dffa-135">Uses the same format described in [Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md).</span></span>|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a><span data-ttu-id="3dffa-136">nuget.exe 現在是能夠將儲存 API 金鑰認證</span><span class="sxs-lookup"><span data-stu-id="3dffa-136">nuget.exe now is able to store API Key credentials</span></span>

<span data-ttu-id="3dffa-137">使用 nuget.exe 命令列工具時，您現在可以使用 SetApiKey 命令來儲存您的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="3dffa-137">When using the nuget.exe command line tool, you can now use the SetApiKey command to store your API key.</span></span> <span data-ttu-id="3dffa-138">這樣一來，您不需要每次推送封裝，請指定它。</span><span class="sxs-lookup"><span data-stu-id="3dffa-138">That way, you won’t need to specify it every time you push a package.</span></span> <span data-ttu-id="3dffa-139">如需詳細資訊以 nuget.exe，儲存您的 API 金鑰[讀取發行套件的文件](../create-packages/publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="3dffa-139">For more details on saving your API key with nuget.exe, [read the documentation on publishing a package](../create-packages/publish-a-package.md).</span></span>

### <a name="package-explorer"></a><span data-ttu-id="3dffa-140">封裝總管</span><span class="sxs-lookup"><span data-stu-id="3dffa-140">Package Explorer</span></span>
<span data-ttu-id="3dffa-141">封裝總管 已更新為支援 NuGet 1.2。</span><span class="sxs-lookup"><span data-stu-id="3dffa-141">Package Explorer has been updated to support NuGet 1.2.</span></span> <span data-ttu-id="3dffa-142">如需詳細資訊，請參閱[封裝總管 的版本資訊](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)。</span><span class="sxs-lookup"><span data-stu-id="3dffa-142">For more information, check out the [Package Explorer release notes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).</span></span>

## <a name="other-featuresfixes"></a><span data-ttu-id="3dffa-143">其他功能/修正</span><span class="sxs-lookup"><span data-stu-id="3dffa-143">Other features/fixes</span></span>

<span data-ttu-id="3dffa-144">上述清單了許多我們實作的功能和我們已修正的 bug 最為明顯。</span><span class="sxs-lookup"><span data-stu-id="3dffa-144">The previous list were the most noticeable of the many features we implemented and bugs we fixed.</span></span> <span data-ttu-id="3dffa-145">總而言之，我們實作/修正[59 工作項目](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)在此版本中。</span><span class="sxs-lookup"><span data-stu-id="3dffa-145">All in all, we implemented/fixed [59 work items](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in this release.</span></span>

## <a name="known-issues"></a><span data-ttu-id="3dffa-146">已知問題</span><span class="sxs-lookup"><span data-stu-id="3dffa-146">Known Issues</span></span>

* <span data-ttu-id="3dffa-147">**1.2 封裝不相容**： 使用命令列工具的最新版本建立套件、 nuget.exe (> 1.2) 不適用於舊版的 NuGet VS 增益集 （例如 1.1)。</span><span class="sxs-lookup"><span data-stu-id="3dffa-147">**1.2 Package incompatibility**: Packages built with the latest version of the command line tool, nuget.exe (> 1.2) will not work with older versions of the NuGet VS Add-in (such as 1.1).</span></span> <span data-ttu-id="3dffa-148">如果遇到錯誤訊息，說明不相容的結構描述相關的項目時，會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="3dffa-148">If you run into an error message stating something about incompatible schema, you are running into this error.</span></span> <span data-ttu-id="3dffa-149">請更新至最新版的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="3dffa-149">Please update NuGet to the latest version.</span></span>
* <span data-ttu-id="3dffa-150">**NuGet.Server 不相容**： 如果您正在裝載內部的 NuGet 摘要使用 NuGet.Server 專案，您必須使用最新版的 NuGet.Server 更新該專案。</span><span class="sxs-lookup"><span data-stu-id="3dffa-150">**NuGet.Server incompatibility**: If you’re hosting an internal NuGet feed using the NuGet.Server project, you’ll need to update that project with the latest version of NuGet.Server.</span></span>
* <span data-ttu-id="3dffa-151">**簽章不相符錯誤**： 如果您使用簽章不相符，相關訊息升級期間執行時發生錯誤，您必須先解除安裝 NuGet，然後再進行安裝。</span><span class="sxs-lookup"><span data-stu-id="3dffa-151">**Signature Mismatch Error**: If you run into an error during an upgrade with a message about a Signature Mismatch, you'll need to uninstall NuGet first and then install it.</span></span> <span data-ttu-id="3dffa-152">這會列在我們[已知問題頁面](../release-notes/Known-Issues.md)提供更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3dffa-152">This is listed in our [Known Issues page](../release-notes/Known-Issues.md) which provides more details.</span></span> <span data-ttu-id="3dffa-153">問題只會影響這些執行 Visual Studio 2010 SP1，且有新版 NuGet 1.0 安裝未正確簽署。</span><span class="sxs-lookup"><span data-stu-id="3dffa-153">The issue only affects those running Visual Studio 2010 SP1 and have a version of NuGet 1.0 installed that was incorrectly signed.</span></span> <span data-ttu-id="3dffa-154">這個版本只對可從 CodePlex 網站一小段時間無法讓此問題應該不會太多人的影響。</span><span class="sxs-lookup"><span data-stu-id="3dffa-154">This version was only made available from the CodePlex website for a brief period so this issue shouldn't affect too many people.</span></span>