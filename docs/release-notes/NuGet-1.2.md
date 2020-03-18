---
title: NuGet 1.2 版本資訊
description: NuGet 1.2 的版本資訊，包括已知問題、bug 修正、新增功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429084"
---
# <a name="nuget-12-release-notes"></a><span data-ttu-id="27235-103">NuGet 1.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="27235-103">NuGet 1.2 Release Notes</span></span>

<span data-ttu-id="27235-104">[Nuget 1.0 和1.1 版本](../release-notes/nuget-1.1.md)資訊 | [nuget 1.3 版本](../release-notes/nuget-1.3.md)資訊</span><span class="sxs-lookup"><span data-stu-id="27235-104">[NuGet 1.0 and 1.1 Release Notes](../release-notes/nuget-1.1.md) | [NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md)</span></span>

<span data-ttu-id="27235-105">NuGet 1.2 已于2011年3月30日發行。</span><span class="sxs-lookup"><span data-stu-id="27235-105">NuGet 1.2 was released on March 30, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="27235-106">新功能</span><span class="sxs-lookup"><span data-stu-id="27235-106">New Features</span></span>

### <a name="framework-profile-support"></a><span data-ttu-id="27235-107">架構設定檔支援</span><span class="sxs-lookup"><span data-stu-id="27235-107">Framework Profile Support</span></span>

<span data-ttu-id="27235-108">從一開始，NuGet 支援的程式庫以不同的架構為目標。</span><span class="sxs-lookup"><span data-stu-id="27235-108">From the start, NuGet supported having libraries target different frameworks.</span></span> <span data-ttu-id="27235-109">但現在封裝可能包含以特定設定檔（例如 Windows Phone 設定檔）為目標的元件。</span><span class="sxs-lookup"><span data-stu-id="27235-109">But now packages may contain assemblies that target specific profiles such as the Windows Phone profile.</span></span> <span data-ttu-id="27235-110">若要以架構的特定設定檔為目標，請在設定檔縮寫後面附加一個破折號。</span><span class="sxs-lookup"><span data-stu-id="27235-110">To target a specific profile of a framework, append a dash followed by the profile abbreviation.</span></span> <span data-ttu-id="27235-111">例如，若要以 Windows Phone 上執行的 SilverLight （也稱為 Windows Phone 7）為目標，您可以將元件放在 sl3-wp 資料夾中，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="27235-111">For example, to target SilverLight running on a Windows Phone (aka Windows Phone 7), you can put an assembly in the sl3-wp folder as demonstrated in the following screenshot.</span></span>

![架構設定檔資料夾版面配置](./media/framework-profile-support.png)

<span data-ttu-id="27235-113">您可能會問，為什麼我們並未直接選擇使用 "wp7" 做為名字。</span><span class="sxs-lookup"><span data-stu-id="27235-113">You might ask why we didn’t just choose to use “wp7” as the moniker.</span></span> <span data-ttu-id="27235-114">在某些情況下，我們預期 Windows Phone 7 可能會在未來執行較新版本的 Silverlight，在此情況下，您可能需要更明確地瞭解您所瞄準的架構設定檔。</span><span class="sxs-lookup"><span data-stu-id="27235-114">In part, we’re anticipating that Windows Phone 7 might run a newer version of Silverlight in the future, in which case you may need to be more specific about which framework profile you’re targetting.</span></span>

### <a name="automatically-add-binding-redirects"></a><span data-ttu-id="27235-115">自動加入系結重新導向</span><span class="sxs-lookup"><span data-stu-id="27235-115">Automatically Add Binding Redirects</span></span>

<span data-ttu-id="27235-116">安裝具有強式命名元件的套件時，NuGet 現在可以偵測到專案需要將系結重新導向新增至設定檔的情況，讓專案能夠自動進行編譯及新增。</span><span class="sxs-lookup"><span data-stu-id="27235-116">When installing a package with strong named assemblies, NuGet can now detect cases where the project requires binding redirects to be added to the configuration file in order for the project to compile and add them automatically.</span></span> <span data-ttu-id="27235-117">David Ebbo 的第3部分：關於 NuGet 版本設定的「透過系結重新[導向進行統一](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)」，涵蓋此功能的目的。</span><span class="sxs-lookup"><span data-stu-id="27235-117">Part 3 of David Ebbo’s blog post series on NuGet Versioning entitled “[Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)” covers the purpose of this feature in more details.</span></span>

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a><span data-ttu-id="27235-118">指定架構元件參考（GAC）</span><span class="sxs-lookup"><span data-stu-id="27235-118">Specifying Framework Assembly References (GAC)</span></span>

<span data-ttu-id="27235-119">在某些情況下，封裝可能相依于 .NET Framework 中的元件。</span><span class="sxs-lookup"><span data-stu-id="27235-119">In some cases, a package may depend on an assembly that’s in the .NET Framework.</span></span> <span data-ttu-id="27235-120">嚴格來說，您的套件取用者不一定需要參考架構元件。</span><span class="sxs-lookup"><span data-stu-id="27235-120">Strictly speaking, it’s not always necessary that the consumer of your package reference the framework assembly.</span></span> <span data-ttu-id="27235-121">但在某些情況下，這一點很重要，例如，開發人員必須針對該元件中的型別撰寫程式碼，才能使用您的封裝。</span><span class="sxs-lookup"><span data-stu-id="27235-121">But in some cases, it's important, such as when the developer needs to code against types in that assembly in order to use your package.</span></span> <span data-ttu-id="27235-122">新的 `frameworkAssemblies` 專案（metadata 元素的子專案）可讓您指定一組指向 GAC 中之架構元件的 `frameworkAssembly` 元素。</span><span class="sxs-lookup"><span data-stu-id="27235-122">The new `frameworkAssemblies` element, a child element of the metadata element, allows you to specify a set of `frameworkAssembly` elements pointing to a Framework assembly in the GAC.</span></span> <span data-ttu-id="27235-123">請注意架構元件的重點。</span><span class="sxs-lookup"><span data-stu-id="27235-123">Note the emphasis on Framework assembly.</span></span>
<span data-ttu-id="27235-124">這些元件不會包含在您的套件中，因為它們會被視為 .NET Framework 中的每一部電腦上。</span><span class="sxs-lookup"><span data-stu-id="27235-124">These assemblies are not included in your package as they are assumed to be on every machine  as part of the .NET Framework.</span></span> <span data-ttu-id="27235-125">下表列出 `frameworkAssembly` 元素的屬性。</span><span class="sxs-lookup"><span data-stu-id="27235-125">The following table lists attributes of the `frameworkAssembly` element.</span></span>


|<span data-ttu-id="27235-126">屬性</span><span class="sxs-lookup"><span data-stu-id="27235-126">Attribute</span></span> |<span data-ttu-id="27235-127">描述</span><span class="sxs-lookup"><span data-stu-id="27235-127">Description</span></span>|
|----------------|-----------|
|<span data-ttu-id="27235-128">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="27235-128">**assemblyName**</span></span>|<span data-ttu-id="27235-129">*必要*。</span><span class="sxs-lookup"><span data-stu-id="27235-129">*Required*.</span></span> <span data-ttu-id="27235-130">元件的名稱，例如 `System.Net`。</span><span class="sxs-lookup"><span data-stu-id="27235-130">Name of the assembly such as `System.Net`.</span></span>|
|<span data-ttu-id="27235-131">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="27235-131">**targetFramework**</span></span>|<span data-ttu-id="27235-132">*選擇性*。</span><span class="sxs-lookup"><span data-stu-id="27235-132">*Optional*.</span></span> <span data-ttu-id="27235-133">允許指定此架構元件所適用的架構和設定檔名稱（或別名），例如 "net40" 或 "sl4"。</span><span class="sxs-lookup"><span data-stu-id="27235-133">Allows specifying a framework and profile name (or alias) that this framework assembly applies to such as "net40" or "sl4".</span></span> <span data-ttu-id="27235-134">使用[支援多個目標 framework](../create-packages/supporting-multiple-target-frameworks.md)中所述的相同格式。</span><span class="sxs-lookup"><span data-stu-id="27235-134">Uses the same format described in [Supporting Multiple Target Frameworks](../create-packages/supporting-multiple-target-frameworks.md).</span></span>|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a><span data-ttu-id="27235-135">nuget.exe 現在能夠儲存 API 金鑰認證</span><span class="sxs-lookup"><span data-stu-id="27235-135">nuget.exe now is able to store API Key credentials</span></span>

<span data-ttu-id="27235-136">使用 nuget.exe 命令列工具時，您現在可以使用 SetApiKey 命令來儲存您的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="27235-136">When using the nuget.exe command line tool, you can now use the SetApiKey command to store your API key.</span></span> <span data-ttu-id="27235-137">如此一來，您就不需要在每次推送封裝時指定它。</span><span class="sxs-lookup"><span data-stu-id="27235-137">That way, you won’t need to specify it every time you push a package.</span></span> <span data-ttu-id="27235-138">如需有關使用 nuget.exe 來儲存 API 金鑰的詳細資訊，請[參閱發行封裝的相關檔](../nuget-org/publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="27235-138">For more details on saving your API key with nuget.exe, [read the documentation on publishing a package](../nuget-org/publish-a-package.md).</span></span>

### <a name="package-explorer"></a><span data-ttu-id="27235-139">封裝瀏覽器</span><span class="sxs-lookup"><span data-stu-id="27235-139">Package Explorer</span></span>
<span data-ttu-id="27235-140">Package Explorer 已更新為支援 NuGet 1.2。</span><span class="sxs-lookup"><span data-stu-id="27235-140">Package Explorer has been updated to support NuGet 1.2.</span></span> <span data-ttu-id="27235-141">如需詳細資訊，請參閱[Package Explorer 版本](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)資訊。</span><span class="sxs-lookup"><span data-stu-id="27235-141">For more information, check out the [Package Explorer release notes](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).</span></span>

## <a name="other-featuresfixes"></a><span data-ttu-id="27235-142">其他功能/修正程式</span><span class="sxs-lookup"><span data-stu-id="27235-142">Other features/fixes</span></span>

<span data-ttu-id="27235-143">前一份清單是我們所實行的許多功能和我們修正的 bug 中最明顯的一項。</span><span class="sxs-lookup"><span data-stu-id="27235-143">The previous list were the most noticeable of the many features we implemented and bugs we fixed.</span></span> <span data-ttu-id="27235-144">畢竟，我們已在此版本中執行/修正[59 工作專案](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="27235-144">All in all, we implemented/fixed [59 work items](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in this release.</span></span>

## <a name="known-issues"></a><span data-ttu-id="27235-145">已知問題</span><span class="sxs-lookup"><span data-stu-id="27235-145">Known Issues</span></span>

* <span data-ttu-id="27235-146">**1.2 套件不相容**：使用最新版本的命令列工具所建立的套件，nuget.exe （> 1.2）將無法使用舊版 Nuget VS 增益集（例如1.1）。</span><span class="sxs-lookup"><span data-stu-id="27235-146">**1.2 Package incompatibility**: Packages built with the latest version of the command line tool, nuget.exe (> 1.2) will not work with older versions of the NuGet VS Add-in (such as 1.1).</span></span> <span data-ttu-id="27235-147">如果您遇到錯誤訊息，指出有關不相容架構的問題，則表示您遇到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="27235-147">If you run into an error message stating something about incompatible schema, you are running into this error.</span></span> <span data-ttu-id="27235-148">請將 NuGet 更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="27235-148">Please update NuGet to the latest version.</span></span>
* <span data-ttu-id="27235-149">**Nuget. 伺服器不相容**：如果您要使用 nuget.exe 專案裝載內部 NuGet 摘要，則必須使用最新版的 Nuget. 伺服器來更新該專案。</span><span class="sxs-lookup"><span data-stu-id="27235-149">**NuGet.Server incompatibility**: If you’re hosting an internal NuGet feed using the NuGet.Server project, you’ll need to update that project with the latest version of NuGet.Server.</span></span>
* <span data-ttu-id="27235-150">簽章**不相符錯誤**：如果您在升級期間遇到錯誤，但有簽章不相符的訊息，您必須先卸載 NuGet，然後再進行安裝。</span><span class="sxs-lookup"><span data-stu-id="27235-150">**Signature Mismatch Error**: If you run into an error during an upgrade with a message about a Signature Mismatch, you need to uninstall NuGet first and then install it.</span></span> <span data-ttu-id="27235-151">這會列在我們的「[已知問題」頁面](../release-notes/known-issues.md)中，其中提供更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="27235-151">This is listed in our [Known Issues page](../release-notes/known-issues.md) which provides more details.</span></span> <span data-ttu-id="27235-152">此問題只會影響執行 Visual Studio 2010 SP1 且安裝了不正確簽署之 NuGet 1.0 版本的作業。</span><span class="sxs-lookup"><span data-stu-id="27235-152">The issue only affects those running Visual Studio 2010 SP1 and have a version of NuGet 1.0 installed that was incorrectly signed.</span></span> <span data-ttu-id="27235-153">這個版本只會在 CodePlex 網站上提供一小段時間，因此此問題不會影響太多人。</span><span class="sxs-lookup"><span data-stu-id="27235-153">This version was only made available from the CodePlex website for a brief period so this issue shouldn't affect too many people.</span></span>