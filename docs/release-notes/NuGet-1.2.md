---
title: NuGet 1.2 版本資訊
description: 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 1.2 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426195"
---
# <a name="nuget-12-release-notes"></a><span data-ttu-id="2fde3-103">NuGet 1.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="2fde3-103">NuGet 1.2 Release Notes</span></span>

<span data-ttu-id="2fde3-104">[NuGet 1.0 和 1.1 版本資訊](../release-notes/nuget-1.1.md) | [NuGet 1.3 版本資訊](../release-notes/nuget-1.3.md)</span><span class="sxs-lookup"><span data-stu-id="2fde3-104">[NuGet 1.0 and 1.1 Release Notes](../release-notes/nuget-1.1.md) | [NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md)</span></span>

<span data-ttu-id="2fde3-105">NuGet 1.2 於 2011 年 3 月 30 日發行。</span><span class="sxs-lookup"><span data-stu-id="2fde3-105">NuGet 1.2 was released on March 30, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="2fde3-106">新功能</span><span class="sxs-lookup"><span data-stu-id="2fde3-106">New Features</span></span>

### <a name="framework-profile-support"></a><span data-ttu-id="2fde3-107">Framework 設定檔支援</span><span class="sxs-lookup"><span data-stu-id="2fde3-107">Framework Profile Support</span></span>

<span data-ttu-id="2fde3-108">從開始時，NuGet 會支援具有程式庫為目標不同的架構。</span><span class="sxs-lookup"><span data-stu-id="2fde3-108">From the start, NuGet supported having libraries target different frameworks.</span></span> <span data-ttu-id="2fde3-109">但是現在套件可能會包含以特定的設定檔，例如 Windows Phone 設定檔為目標的組件。</span><span class="sxs-lookup"><span data-stu-id="2fde3-109">But now packages may contain assemblies that target specific profiles such as the Windows Phone profile.</span></span> <span data-ttu-id="2fde3-110">若要以目標 framework 的特定設定檔，附加一個破折號後面的設定檔的縮寫。</span><span class="sxs-lookup"><span data-stu-id="2fde3-110">To target a specific profile of a framework, append a dash followed by the profile abbreviation.</span></span> <span data-ttu-id="2fde3-111">比方說，若要在 Windows Phone (也稱為 Windows Phone 7) 上執行的 SilverLight 為目標，您可以將組件放在 sl3 wp 資料夾中，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="2fde3-111">For example, to target SilverLight running on a Windows Phone (aka Windows Phone 7), you can put an assembly in the sl3-wp folder as demonstrated in the following screenshot.</span></span>

![Framework 設定檔資料夾版面配置](./media/framework-profile-support.png)

<span data-ttu-id="2fde3-113">您可能會問為什麼我們不只是選擇 「 wp7"做為 moniker。</span><span class="sxs-lookup"><span data-stu-id="2fde3-113">You might ask why we didn’t just choose to use “wp7” as the moniker.</span></span> <span data-ttu-id="2fde3-114">中的情況下，我們會預期 Windows Phone 7 可能在未來執行較新版本的 Silverlight，在此情況下，您可能需要更明確了解您的架構設定檔就為目標的。</span><span class="sxs-lookup"><span data-stu-id="2fde3-114">In part, we’re anticipating that Windows Phone 7 might run a newer version of Silverlight in the future, in which case you may need to be more specific about which framework profile you’re targetting.</span></span>

### <a name="automatically-add-binding-redirects"></a><span data-ttu-id="2fde3-115">自動新增繫結重新導向</span><span class="sxs-lookup"><span data-stu-id="2fde3-115">Automatically Add Binding Redirects</span></span>

<span data-ttu-id="2fde3-116">當使用強式名稱組件安裝套件，NuGet 現在可以偵測表示專案需要繫結重新導向加入至專案，以編譯並自動新增它們的順序中的組態檔的情況。</span><span class="sxs-lookup"><span data-stu-id="2fde3-116">When installing a package with strong named assemblies, NuGet can now detect cases where the project requires binding redirects to be added to the configuration file in order for the project to compile and add them automatically.</span></span> <span data-ttu-id="2fde3-117">第 3 部分 David Ebbo 的部落格文章系列的 NuGet 版本設定名為"[透過繫結重新導向的統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)"涵蓋更多詳細資料中的這項功能的目的。</span><span class="sxs-lookup"><span data-stu-id="2fde3-117">Part 3 of David Ebbo’s blog post series on NuGet Versioning entitled “[Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)” covers the purpose of this feature in more details.</span></span>

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a><span data-ttu-id="2fde3-118">指定 Framework 組件參考 (GAC)</span><span class="sxs-lookup"><span data-stu-id="2fde3-118">Specifying Framework Assembly References (GAC)</span></span>

<span data-ttu-id="2fde3-119">在某些情況下，封裝可能取決於.NET Framework 中的組件。</span><span class="sxs-lookup"><span data-stu-id="2fde3-119">In some cases, a package may depend on an assembly that’s in the .NET Framework.</span></span> <span data-ttu-id="2fde3-120">嚴格來說，它不一定需要取用者的您的套件參考的 framework 組件。</span><span class="sxs-lookup"><span data-stu-id="2fde3-120">Strictly speaking, it’s not always necessary that the consumer of your package reference the framework assembly.</span></span> <span data-ttu-id="2fde3-121">但在某些情況下，很重要的例如當開發人員必須針對該組件中的型別程式碼，才能使用您的套件。</span><span class="sxs-lookup"><span data-stu-id="2fde3-121">But in some cases, it's important, such as when the developer needs to code against types in that assembly in order to use your package.</span></span> <span data-ttu-id="2fde3-122">新`frameworkAssemblies`項目，項目的子項目中繼資料，可讓您指定一組`frameworkAssembly`在 GAC 中的 Framework 組件所指向的項目。</span><span class="sxs-lookup"><span data-stu-id="2fde3-122">The new `frameworkAssemblies` element, a child element of the metadata element, allows you to specify a set of `frameworkAssembly` elements pointing to a Framework assembly in the GAC.</span></span> <span data-ttu-id="2fde3-123">請注意其重視 Framework 組件。</span><span class="sxs-lookup"><span data-stu-id="2fde3-123">Note the emphasis on Framework assembly.</span></span>
<span data-ttu-id="2fde3-124">因為它們假設為每部電腦上，.NET Framework 的一部分，這些組件不會包含在套件中。</span><span class="sxs-lookup"><span data-stu-id="2fde3-124">These assemblies are not included in your package as they are assumed to be on every machine  as part of the .NET Framework.</span></span> <span data-ttu-id="2fde3-125">下表列出的屬性`frameworkAssembly`項目。</span><span class="sxs-lookup"><span data-stu-id="2fde3-125">The following table lists attributes of the `frameworkAssembly` element.</span></span>


|<span data-ttu-id="2fde3-126">屬性</span><span class="sxs-lookup"><span data-stu-id="2fde3-126">Attribute</span></span> |<span data-ttu-id="2fde3-127">描述</span><span class="sxs-lookup"><span data-stu-id="2fde3-127">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="2fde3-128">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="2fde3-128">**assemblyName**</span></span>|<span data-ttu-id="2fde3-129">*所需*。</span><span class="sxs-lookup"><span data-stu-id="2fde3-129">*Required*.</span></span> <span data-ttu-id="2fde3-130">這類的組件名稱`System.Net`。</span><span class="sxs-lookup"><span data-stu-id="2fde3-130">Name of the assembly such as `System.Net`.</span></span>|
|<span data-ttu-id="2fde3-131">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="2fde3-131">**targetFramework**</span></span>|<span data-ttu-id="2fde3-132">*選擇性*。</span><span class="sxs-lookup"><span data-stu-id="2fde3-132">*Optional*.</span></span> <span data-ttu-id="2fde3-133">可讓您指定架構和設定檔的名稱 （或別名），這個架構組件適用於 「 net40"或"sl4 」 等。</span><span class="sxs-lookup"><span data-stu-id="2fde3-133">Allows specifying a framework and profile name (or alias) that this framework assembly applies to such as "net40" or "sl4".</span></span> <span data-ttu-id="2fde3-134">使用相同的格式中所述[支援多個目標架構](../create-packages/supporting-multiple-target-frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="2fde3-134">Uses the same format described in [Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md).</span></span>|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a><span data-ttu-id="2fde3-135">nuget.exe 現在已能夠儲存 API 金鑰認證</span><span class="sxs-lookup"><span data-stu-id="2fde3-135">nuget.exe now is able to store API Key credentials</span></span>

<span data-ttu-id="2fde3-136">使用 nuget.exe 命令列工具時，您現在可以使用 SetApiKey 命令來儲存您的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2fde3-136">When using the nuget.exe command line tool, you can now use the SetApiKey command to store your API key.</span></span> <span data-ttu-id="2fde3-137">如此一來，您不需要指定它，每次您將封裝推送。</span><span class="sxs-lookup"><span data-stu-id="2fde3-137">That way, you won’t need to specify it every time you push a package.</span></span> <span data-ttu-id="2fde3-138">如需有關使用 nuget.exe，儲存您的 API 金鑰[閱讀相關文件發行套件](../nuget-org/publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="2fde3-138">For more details on saving your API key with nuget.exe, [read the documentation on publishing a package](../nuget-org/publish-a-package.md).</span></span>

### <a name="package-explorer"></a><span data-ttu-id="2fde3-139">封裝總管</span><span class="sxs-lookup"><span data-stu-id="2fde3-139">Package Explorer</span></span>
<span data-ttu-id="2fde3-140">封裝總管 已更新為支援 NuGet 1.2。</span><span class="sxs-lookup"><span data-stu-id="2fde3-140">Package Explorer has been updated to support NuGet 1.2.</span></span> <span data-ttu-id="2fde3-141">如需詳細資訊，請參閱[封裝總管版本資訊](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)。</span><span class="sxs-lookup"><span data-stu-id="2fde3-141">For more information, check out the [Package Explorer release notes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).</span></span>

## <a name="other-featuresfixes"></a><span data-ttu-id="2fde3-142">其他功能/修正程式</span><span class="sxs-lookup"><span data-stu-id="2fde3-142">Other features/fixes</span></span>

<span data-ttu-id="2fde3-143">先前的清單是最明顯的許多我們實作的功能和我們已修正的 bug。</span><span class="sxs-lookup"><span data-stu-id="2fde3-143">The previous list were the most noticeable of the many features we implemented and bugs we fixed.</span></span> <span data-ttu-id="2fde3-144">總而言之，我們實作/修正[59 工作項目](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)在此版本中。</span><span class="sxs-lookup"><span data-stu-id="2fde3-144">All in all, we implemented/fixed [59 work items](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in this release.</span></span>

## <a name="known-issues"></a><span data-ttu-id="2fde3-145">已知問題</span><span class="sxs-lookup"><span data-stu-id="2fde3-145">Known Issues</span></span>

* <span data-ttu-id="2fde3-146">**1.2 封裝不相容**:使用命令列工具的最新版本建置的套件，nuget.exe (> 1.2) 不適用於舊版的 NuGet VS 增益集 （例如 1.1)。</span><span class="sxs-lookup"><span data-stu-id="2fde3-146">**1.2 Package incompatibility**: Packages built with the latest version of the command line tool, nuget.exe (> 1.2) will not work with older versions of the NuGet VS Add-in (such as 1.1).</span></span> <span data-ttu-id="2fde3-147">如果您遇到錯誤訊息，說明不相容的結構描述相關的項目時，您遇到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="2fde3-147">If you run into an error message stating something about incompatible schema, you are running into this error.</span></span> <span data-ttu-id="2fde3-148">請更新至最新版的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="2fde3-148">Please update NuGet to the latest version.</span></span>
* <span data-ttu-id="2fde3-149">**NuGet.Server 不相容**:如果您正在裝載內部的 NuGet 摘要使用 NuGet.Server 的專案，您必須使用最新版的 NuGet.Server 更新該專案。</span><span class="sxs-lookup"><span data-stu-id="2fde3-149">**NuGet.Server incompatibility**: If you’re hosting an internal NuGet feed using the NuGet.Server project, you’ll need to update that project with the latest version of NuGet.Server.</span></span>
* <span data-ttu-id="2fde3-150">**簽章不相符錯誤**:如果您使用相關的簽章不相符的訊息升級期間遇到錯誤，必須先解除安裝 NuGet，然後再進行安裝。</span><span class="sxs-lookup"><span data-stu-id="2fde3-150">**Signature Mismatch Error**: If you run into an error during an upgrade with a message about a Signature Mismatch, you need to uninstall NuGet first and then install it.</span></span> <span data-ttu-id="2fde3-151">這會列在我們[已知問題頁面](../release-notes/known-issues.md)提供更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2fde3-151">This is listed in our [Known Issues page](../release-notes/known-issues.md) which provides more details.</span></span> <span data-ttu-id="2fde3-152">此問題只會影響執行 Visual Studio 2010 SP1，且資料不正確地簽署 NuGet 1.0 一起安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="2fde3-152">The issue only affects those running Visual Studio 2010 SP1 and have a version of NuGet 1.0 installed that was incorrectly signed.</span></span> <span data-ttu-id="2fde3-153">此版本已僅能從 CodePlex 網站在短時間內讓此問題，應該不會影響太多人。</span><span class="sxs-lookup"><span data-stu-id="2fde3-153">This version was only made available from the CodePlex website for a brief period so this issue shouldn't affect too many people.</span></span>