---
title: NuGet 2.7.2 版本資訊
description: 版本資訊 NuGet 2.7.2 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550066"
---
# <a name="nuget-272-release-notes"></a><span data-ttu-id="435cc-103">NuGet 2.7.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="435cc-103">NuGet 2.7.2 Release Notes</span></span>

<span data-ttu-id="435cc-104">[NuGet 2.7.1 版本資訊](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md)</span><span class="sxs-lookup"><span data-stu-id="435cc-104">[NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md)</span></span>

<span data-ttu-id="435cc-105">NuGet 2.7.2 已於 2013 年 11 月 11 日發行。</span><span class="sxs-lookup"><span data-stu-id="435cc-105">NuGet 2.7.2 was released on November 11, 2013.</span></span>

## <a name="noteworthy-bug-fixes-and-features"></a><span data-ttu-id="435cc-106">值得注意的錯誤修正和功能</span><span class="sxs-lookup"><span data-stu-id="435cc-106">Noteworthy Bug Fixes and Features</span></span>

### <a name="license-text"></a><span data-ttu-id="435cc-107">授權文字</span><span class="sxs-lookup"><span data-stu-id="435cc-107">License Text</span></span>
<span data-ttu-id="435cc-108">好一段時間，Microsoft 已在 Visual Studio 中包含數個熱門的開放原始碼程式庫的 Web 應用程式專案的預設範本一部分的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="435cc-108">For quite some time, Microsoft has included the NuGet packages for several popular open-source libraries as a part of the default templates for Web application projects in Visual Studio.</span></span> <span data-ttu-id="435cc-109">jQuery 可能是眾所皆知的這種類型的程式庫範例。</span><span class="sxs-lookup"><span data-stu-id="435cc-109">jQuery is probably the most well-known example of this type of library.</span></span> <span data-ttu-id="435cc-110">因為傳遞以及產品的元件相關聯的支援協議的情況下，封裝的指令碼檔案會包含比公用 nuget.org 資源庫上找到的相同封裝中的指令碼檔案的不同授權文字。</span><span class="sxs-lookup"><span data-stu-id="435cc-110">Because of the support agreement associated with components that are delivered along with a product, the package's script file contains different license text than the script file found in the same package on the public nuget.org gallery.</span></span> <span data-ttu-id="435cc-111">在文字中的這項差異可以避免繼續進行，因為造成有不同的內容雜湊值的指令碼檔案的不同授權文字區塊的套件更新 （也因此被視為在專案中修改）。</span><span class="sxs-lookup"><span data-stu-id="435cc-111">This difference in text can prevent package updates from proceeding as a result of the different license text blocks causing the script files to have different content hash values (and therefore to be treated as modified within the project).</span></span>

<span data-ttu-id="435cc-112">若要解決這個問題，NuGet 2.7.2 可讓指令碼作者包括授權文字區塊，這看起來像這樣的特殊標記區段內。</span><span class="sxs-lookup"><span data-stu-id="435cc-112">To mitigate this issue, NuGet 2.7.2 allows the script author to include the license text block within a specially marked section which looks as follows.</span></span>

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

<span data-ttu-id="435cc-113">更新內容套件時檔案包含這個區塊中，NuGet 不會不納入與 NuGet 資源庫上的版本比較區塊的內容和可以因此刪除和更新內容檔案，就好像它會比對的原始複本。</span><span class="sxs-lookup"><span data-stu-id="435cc-113">When updating packages with content files containing this block, NuGet does not factor the contents of the block into the comparison with the version on the NuGet gallery, and can therefore delete and update the content file as though it matches the original copy.</span></span>

<span data-ttu-id="435cc-114">識別此區塊文字 「 NUGET:: BEGIN 授權文字 」 和 「 NUGET:: END 授權文字 」 發生任何一處開始和結束行。</span><span class="sxs-lookup"><span data-stu-id="435cc-114">This block is identified by the text "NUGET: BEGIN LICENSE TEXT" and "NUGET: END LICENSE TEXT" occurring anywhere on the beginning and ending lines.</span></span>  <span data-ttu-id="435cc-115">沒有其他格式的需求存在時，它會允許在任何類型的文字檔案，不論語言為何要使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="435cc-115">No other formatting requirements exist, allowing this feature to be used in any type of text file regardless of language.</span></span>

### <a name="add-binding-redirects-for-non-framework-assemblies"></a><span data-ttu-id="435cc-116">新增繫結重新導向的非 Framework 組件</span><span class="sxs-lookup"><span data-stu-id="435cc-116">Add Binding Redirects for non-Framework Assemblies</span></span>
<span data-ttu-id="435cc-117">對於屬於.NET Framework 的組件，NuGet 會略過新增繫結重新導向至應用程式的組態檔更新套件時。</span><span class="sxs-lookup"><span data-stu-id="435cc-117">For assemblies that are part of the .NET Framework, NuGet skips adding binding redirects into the application's configuration file when updating the package.</span></span> <span data-ttu-id="435cc-118">此修正位址的迴歸，藉此繫結重新導向不新增針對某些組件，即使這些組件不是 NuGet 2.7 中視為.NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="435cc-118">This fix addresses a regression in NuGet 2.7 whereby binding redirects were not being added for some assemblies, even though those assemblies are not considered a part of the .NET Framework.</span></span> <span data-ttu-id="435cc-119">NuGet 2.7.2 還原先前的 NuGet 2.5 和 2.6 的行為，並新增繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="435cc-119">NuGet 2.7.2 restores the previous NuGet 2.5 and 2.6 behavior and adds the binding redirects.</span></span>

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a><span data-ttu-id="435cc-120">使用已安裝 Xamarin 工具來安裝可攜式程式庫</span><span class="sxs-lookup"><span data-stu-id="435cc-120">Installing portable libraries with Xamarin Tools installed</span></span>
<span data-ttu-id="435cc-121">當在機器上安裝 Xamarin 的開發工具時，它們會修改支援的架構的組態資料，以指定現有的目標架構組合和 Xamarin 架構之間的相容性。</span><span class="sxs-lookup"><span data-stu-id="435cc-121">When Xamarin's development tools are installed on a machine, they modify the supported frameworks configuration data to specify compatibility between existing target framework combinations and Xamarin frameworks.</span></span> <span data-ttu-id="435cc-122">2.7.2 的版本，NuGet 會知道這些隱含的相容性規則，並因此可方便 Xamarin 平台為目標的開發人員套件中，因此安裝與 Xamarin 相容，但未明確標示的可攜式程式庫中繼資料本身。</span><span class="sxs-lookup"><span data-stu-id="435cc-122">With version 2.7.2, NuGet is now aware of these implicit compatibility rules, and therefore makes it easy for developers targeting Xamarin platforms to install portable libraries that are Xamarin-compatible but not explicitly marked as such in the package metadata itself.</span></span>

### <a name="machine-wide-configuration-settings-honored"></a><span data-ttu-id="435cc-123">接受的整部電腦的組態設定</span><span class="sxs-lookup"><span data-stu-id="435cc-123">Machine-wide configuration settings honored</span></span>
<span data-ttu-id="435cc-124">使用階層式 Nuget.Config 檔案時，repositoryPath 金鑰未被接受的最接近方案根目錄的 Nuget.Config 檔案。</span><span class="sxs-lookup"><span data-stu-id="435cc-124">When using hierarchical Nuget.Config files, the repositoryPath key was not being honored for Nuget.Config files closest to the solution root.</span></span> <span data-ttu-id="435cc-125">在 Visual Studio 2013 中，NuGet 會安裝自訂 Nuget.Config 檔於 %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config，才能夠加入 「 Microsoft 和.NET 」 套件來源。</span><span class="sxs-lookup"><span data-stu-id="435cc-125">In Visual Studio 2013, NuGet installs a custom Nuget.Config file at %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config in order to add the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="435cc-126">如此一來，因應措施在解決方案中使用自訂的 repositoryPath 已刪除的電腦層級 Nuget.Config-這也意味著移除 「 Microsoft 和.NET 」 套件來源。</span><span class="sxs-lookup"><span data-stu-id="435cc-126">As a result, the work-around for using a custom repositoryPath in a solution was to delete the machine-level Nuget.Config - which also meant removing the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="435cc-127">使用階層式 Nuget.Config 檔案時，NuGet 2.7.2 現在會接受 repositoryPath 的優先順序規則。</span><span class="sxs-lookup"><span data-stu-id="435cc-127">NuGet 2.7.2 now honors the precedence rules for repositoryPath when using hierarchical Nuget.Config files.</span></span>

## <a name="all-changes"></a><span data-ttu-id="435cc-128">所有的變更</span><span class="sxs-lookup"><span data-stu-id="435cc-128">All Changes</span></span>
<span data-ttu-id="435cc-129">如需完整的工作清單項目中已修正 NuGet 2.7.2，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。</span><span class="sxs-lookup"><span data-stu-id="435cc-129">For a full list of work items fixed in NuGet 2.7.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).</span></span>
