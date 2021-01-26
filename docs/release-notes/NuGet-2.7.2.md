---
title: NuGet 2.7.2 版本資訊
description: NuGet 2.7.2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776779"
---
# <a name="nuget-272-release-notes"></a><span data-ttu-id="85535-103">NuGet 2.7.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="85535-103">NuGet 2.7.2 Release Notes</span></span>

<span data-ttu-id="85535-104">[NuGet 2.7.1 版本](../release-notes/nuget-2.7.1.md)  |  資訊[NuGet 2.8 版本](../release-notes/nuget-2.8.md)資訊</span><span class="sxs-lookup"><span data-stu-id="85535-104">[NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md)</span></span>

<span data-ttu-id="85535-105">NuGet 2.7.2 已于2013年11月11日發行。</span><span class="sxs-lookup"><span data-stu-id="85535-105">NuGet 2.7.2 was released on November 11, 2013.</span></span>

## <a name="noteworthy-bug-fixes-and-features"></a><span data-ttu-id="85535-106">值得注意的錯誤修正和功能</span><span class="sxs-lookup"><span data-stu-id="85535-106">Noteworthy Bug Fixes and Features</span></span>

### <a name="license-text"></a><span data-ttu-id="85535-107">授權文字</span><span class="sxs-lookup"><span data-stu-id="85535-107">License Text</span></span>
<span data-ttu-id="85535-108">Microsoft 針對 Visual Studio 中的 Web 應用程式專案的預設範本，包含了數個常用的開放原始碼程式庫的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="85535-108">For quite some time, Microsoft has included the NuGet packages for several popular open-source libraries as a part of the default templates for Web application projects in Visual Studio.</span></span> <span data-ttu-id="85535-109">jQuery 可能是這種程式庫類型最知名的範例。</span><span class="sxs-lookup"><span data-stu-id="85535-109">jQuery is probably the most well-known example of this type of library.</span></span> <span data-ttu-id="85535-110">由於與產品一起傳遞的元件相關聯的支援合約，封裝的腳本檔案所含的授權文字，與公用 nuget.org 資源庫上相同套件中找到的指令檔不同。</span><span class="sxs-lookup"><span data-stu-id="85535-110">Because of the support agreement associated with components that are delivered along with a product, the package's script file contains different license text than the script file found in the same package on the public nuget.org gallery.</span></span> <span data-ttu-id="85535-111">這項文字差異可以防止套件更新因為不同的授權文字區塊而無法繼續，而導致腳本檔案 (不同的內容雜湊值，因此在專案) 內視為已修改。</span><span class="sxs-lookup"><span data-stu-id="85535-111">This difference in text can prevent package updates from proceeding as a result of the different license text blocks causing the script files to have different content hash values (and therefore to be treated as modified within the project).</span></span>

<span data-ttu-id="85535-112">為了減輕這個問題，NuGet 2.7.2 允許腳本作者在特別標示的區段內包含授權文字區塊，如下所示。</span><span class="sxs-lookup"><span data-stu-id="85535-112">To mitigate this issue, NuGet 2.7.2 allows the script author to include the license text block within a specially marked section which looks as follows.</span></span>

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

<span data-ttu-id="85535-113">當使用包含此區塊的內容檔案來更新套件時，NuGet 不會將區塊的內容視為與 NuGet 資源庫上的版本進行比較，因此可以刪除和更新內容檔案，就好像它符合原始複本一樣。</span><span class="sxs-lookup"><span data-stu-id="85535-113">When updating packages with content files containing this block, NuGet does not factor the contents of the block into the comparison with the version on the NuGet gallery, and can therefore delete and update the content file as though it matches the original copy.</span></span>

<span data-ttu-id="85535-114">此區塊是由文字「NUGET：開始授權文字」和「NUGET：結束授權文字」所識別，並在開頭和結尾行的任何位置發生。</span><span class="sxs-lookup"><span data-stu-id="85535-114">This block is identified by the text "NUGET: BEGIN LICENSE TEXT" and "NUGET: END LICENSE TEXT" occurring anywhere on the beginning and ending lines.</span></span>  <span data-ttu-id="85535-115">不存在任何其他格式化需求，不論語言為何，都可以在任何類型的文字檔中使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="85535-115">No other formatting requirements exist, allowing this feature to be used in any type of text file regardless of language.</span></span>

### <a name="add-binding-redirects-for-non-framework-assemblies"></a><span data-ttu-id="85535-116">新增非架構元件的系結重新導向</span><span class="sxs-lookup"><span data-stu-id="85535-116">Add Binding Redirects for non-Framework Assemblies</span></span>
<span data-ttu-id="85535-117">針對屬於 .NET Framework 一部分的元件，NuGet 會在更新套件時，略過將系結重新導向新增至應用程式的設定檔。</span><span class="sxs-lookup"><span data-stu-id="85535-117">For assemblies that are part of the .NET Framework, NuGet skips adding binding redirects into the application's configuration file when updating the package.</span></span> <span data-ttu-id="85535-118">這項修正可解決 NuGet 2.7 中的回歸，因為某些元件不會加入系結重新導向，即使這些元件不會被視為 .NET Framework 的一部分也一樣。</span><span class="sxs-lookup"><span data-stu-id="85535-118">This fix addresses a regression in NuGet 2.7 whereby binding redirects were not being added for some assemblies, even though those assemblies are not considered a part of the .NET Framework.</span></span> <span data-ttu-id="85535-119">NuGet 2.7.2 會還原先前的 NuGet 2.5 和2.6 行為，並新增系結重新導向。</span><span class="sxs-lookup"><span data-stu-id="85535-119">NuGet 2.7.2 restores the previous NuGet 2.5 and 2.6 behavior and adds the binding redirects.</span></span>

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a><span data-ttu-id="85535-120">安裝已安裝 Xamarin 工具的便攜程式庫</span><span class="sxs-lookup"><span data-stu-id="85535-120">Installing portable libraries with Xamarin Tools installed</span></span>
<span data-ttu-id="85535-121">當 Xamarin 的開發工具安裝在電腦上時，它們會修改支援的架構設定資料，以指定現有目標 framework 組合和 Xamarin framework 之間的相容性。</span><span class="sxs-lookup"><span data-stu-id="85535-121">When Xamarin's development tools are installed on a machine, they modify the supported frameworks configuration data to specify compatibility between existing target framework combinations and Xamarin frameworks.</span></span> <span data-ttu-id="85535-122">使用版本2.7.2 時，NuGet 現在知道這些隱含相容性規則，因此可讓開發人員輕鬆地以 Xamarin 平臺為目標，以安裝 Xamarin 相容但未明確標示為套件中繼資料本身的便攜程式庫。</span><span class="sxs-lookup"><span data-stu-id="85535-122">With version 2.7.2, NuGet is now aware of these implicit compatibility rules, and therefore makes it easy for developers targeting Xamarin platforms to install portable libraries that are Xamarin-compatible but not explicitly marked as such in the package metadata itself.</span></span>

### <a name="machine-wide-configuration-settings-honored"></a><span data-ttu-id="85535-123">接受全電腦的設定</span><span class="sxs-lookup"><span data-stu-id="85535-123">Machine-wide configuration settings honored</span></span>
<span data-ttu-id="85535-124">使用階層式 Nuget.Config 檔案時，不會針對最接近解決方案根目錄的 Nuget.Config 檔案接受 repositoryPath 金鑰。</span><span class="sxs-lookup"><span data-stu-id="85535-124">When using hierarchical Nuget.Config files, the repositoryPath key was not being honored for Nuget.Config files closest to the solution root.</span></span> <span data-ttu-id="85535-125">在 Visual Studio 2013 中，NuGet 會在% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config 安裝自訂 Nuget.Config 檔案，以新增 "Microsoft 和 .NET" 套件來源。</span><span class="sxs-lookup"><span data-stu-id="85535-125">In Visual Studio 2013, NuGet installs a custom Nuget.Config file at %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config in order to add the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="85535-126">因此，在解決方案中使用自訂 repositoryPath 的解決方法是刪除電腦層級的 Nuget.Config，也就是移除「Microsoft 和 .NET」套件來源。</span><span class="sxs-lookup"><span data-stu-id="85535-126">As a result, the work-around for using a custom repositoryPath in a solution was to delete the machine-level Nuget.Config - which also meant removing the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="85535-127">在使用階層式 Nuget.Config 檔案時，NuGet 2.7.2 現在接受 repositoryPath 的優先順序規則。</span><span class="sxs-lookup"><span data-stu-id="85535-127">NuGet 2.7.2 now honors the precedence rules for repositoryPath when using hierarchical Nuget.Config files.</span></span>

## <a name="all-changes"></a><span data-ttu-id="85535-128">所有變更</span><span class="sxs-lookup"><span data-stu-id="85535-128">All Changes</span></span>
<span data-ttu-id="85535-129">如需 NuGet 2.7.2 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。</span><span class="sxs-lookup"><span data-stu-id="85535-129">For a full list of work items fixed in NuGet 2.7.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).</span></span>
