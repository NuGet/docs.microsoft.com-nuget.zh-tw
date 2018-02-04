---
title: "NuGet 2.7.2 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "版本資訊包含 NuGet 2.7.2 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 2.7.2 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8fe9acc3ad9c1c368fc750694ea523ac845995c5
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-272-release-notes"></a><span data-ttu-id="e58ce-104">NuGet 2.7.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="e58ce-104">NuGet 2.7.2 Release Notes</span></span>

<span data-ttu-id="e58ce-105">[NuGet 2.7.1 版本資訊](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md)</span><span class="sxs-lookup"><span data-stu-id="e58ce-105">[NuGet 2.7.1 Release Notes](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md)</span></span>

<span data-ttu-id="e58ce-106">NuGet 2.7.2 已於 2013 年 11 月 11 日發行。</span><span class="sxs-lookup"><span data-stu-id="e58ce-106">NuGet 2.7.2 was released on November 11, 2013.</span></span>

## <a name="noteworthy-bug-fixes-and-features"></a><span data-ttu-id="e58ce-107">值得注意的錯誤修正和功能</span><span class="sxs-lookup"><span data-stu-id="e58ce-107">Noteworthy Bug Fixes and Features</span></span>

### <a name="license-text"></a><span data-ttu-id="e58ce-108">授權文字</span><span class="sxs-lookup"><span data-stu-id="e58ce-108">License Text</span></span>
<span data-ttu-id="e58ce-109">一段時間，Microsoft Visual Studio 中已包含幾個常用的開放原始碼程式庫的 Web 應用程式專案的預設範本一部分的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="e58ce-109">For quite some time, Microsoft has included the NuGet packages for several popular open-source libraries as a part of the default templates for Web application projects in Visual Studio.</span></span> <span data-ttu-id="e58ce-110">jQuery 可能是這種類型的文件庫眾所皆知的範例。</span><span class="sxs-lookup"><span data-stu-id="e58ce-110">jQuery is probably the most well-known example of this type of library.</span></span> <span data-ttu-id="e58ce-111">支援協議與產品一起傳送的元件相關聯，因為封裝的指令碼檔案會包含比公用 nuget.org 的組件庫上找到的相同封裝中的指令碼檔案的不同授權文字。</span><span class="sxs-lookup"><span data-stu-id="e58ce-111">Because of the support agreement associated with components that are delivered along with a product, the package's script file contains different license text than the script file found in the same package on the public nuget.org gallery.</span></span> <span data-ttu-id="e58ce-112">文字的差異可避免造成有不同的內容雜湊值的指令碼檔案的不同授權文字區塊的結果繼續執行的封裝更新，並因此被視為在專案中修改。</span><span class="sxs-lookup"><span data-stu-id="e58ce-112">This difference in text can prevent package updates from proceeding as a result of the different license text blocks causing the script files to have different content hash values (and therefore to be treated as modified within the project).</span></span>

<span data-ttu-id="e58ce-113">若要減輕這個問題，NuGet 2.7.2 可讓指令碼作者，以包含授權文字區塊，看起來，如下所示的特殊標記區段內。</span><span class="sxs-lookup"><span data-stu-id="e58ce-113">To mitigate this issue, NuGet 2.7.2 allows the script author to include the license text block within a specially marked section which looks as follows.</span></span>

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

<span data-ttu-id="e58ce-114">更新封裝的內容時檔案，其中包含這個區塊中，NuGet 不因素區塊的內容與在 NuGet gallery 上的版本比較可以因此刪除和更新內容檔案，就好像它會比對的原始複本。</span><span class="sxs-lookup"><span data-stu-id="e58ce-114">When updating packages with content files containing this block, NuGet does not factor the contents of the block into the comparison with the version on the NuGet gallery, and can therefore delete and update the content file as though it matches the original copy.</span></span>

<span data-ttu-id="e58ce-115">此區塊是以文字"NUGET:: BEGIN 授權 」 和識別 「 NUGET:: END 授權文字 」 發生任何位置的開始和結束行。</span><span class="sxs-lookup"><span data-stu-id="e58ce-115">This block is identified by the text "NUGET: BEGIN LICENSE TEXT" and "NUGET: END LICENSE TEXT" occurring anywhere on the beginning and ending lines.</span></span>  <span data-ttu-id="e58ce-116">沒有其他格式的需求存在時，它會讓這項功能，以用於任何類型的文字檔案，不論語言為何。</span><span class="sxs-lookup"><span data-stu-id="e58ce-116">No other formatting requirements exist, allowing this feature to be used in any type of text file regardless of language.</span></span>

### <a name="add-binding-redirects-for-non-framework-assemblies"></a><span data-ttu-id="e58ce-117">將繫結重新導向的非 Framework 組件</span><span class="sxs-lookup"><span data-stu-id="e58ce-117">Add Binding Redirects for non-Framework Assemblies</span></span>
<span data-ttu-id="e58ce-118">對於屬於.NET Framework 的組件，NuGet 會略過加入繫結重新導向至應用程式的組態檔更新封裝時。</span><span class="sxs-lookup"><span data-stu-id="e58ce-118">For assemblies that are part of the .NET Framework, NuGet skips adding binding redirects into the application's configuration file when updating the package.</span></span> <span data-ttu-id="e58ce-119">此修正位址 NuGet 2.7 藉此繫結重新導向未被加入針對某些組件，即使這些組件不在迴歸視為.NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="e58ce-119">This fix addresses a regression in NuGet 2.7 whereby binding redirects were not being added for some assemblies, even though those assemblies are not considered a part of the .NET Framework.</span></span> <span data-ttu-id="e58ce-120">NuGet 2.7.2 還原先前的 NuGet 2.5 和 2.6 行為，並加入繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="e58ce-120">NuGet 2.7.2 restores the previous NuGet 2.5 and 2.6 behavior and adds the binding redirects.</span></span>

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a><span data-ttu-id="e58ce-121">利用 Xamarin 工具安裝中安裝可攜式程式庫</span><span class="sxs-lookup"><span data-stu-id="e58ce-121">Installing portable libraries with Xamarin Tools installed</span></span>
<span data-ttu-id="e58ce-122">Xamarin 的開發工具的機器上安裝之後，他們會修改指定現有的目標 framework 組合和 Xamarin 架構之間的相容性支援的架構組態資料。</span><span class="sxs-lookup"><span data-stu-id="e58ce-122">When Xamarin's development tools are installed on a machine, they modify the supported frameworks configuration data to specify compatibility between existing target framework combinations and Xamarin frameworks.</span></span> <span data-ttu-id="e58ce-123">2.7.2 的版本，NuGet 是留意這些隱含的相容性規則，因此輕鬆 Xamarin 平台目標的開發人員套件中的這類安裝之 Xamarin 相容，但未明確標記為可攜式類別庫中繼資料本身。</span><span class="sxs-lookup"><span data-stu-id="e58ce-123">With version 2.7.2, NuGet is now aware of these implicit compatibility rules, and therefore makes it easy for developers targeting Xamarin platforms to install portable libraries that are Xamarin-compatible but not explicitly marked as such in the package metadata itself.</span></span>

### <a name="machine-wide-configuration-settings-honored"></a><span data-ttu-id="e58ce-124">接受的整部機器的組態設定</span><span class="sxs-lookup"><span data-stu-id="e58ce-124">Machine-wide configuration settings honored</span></span>
<span data-ttu-id="e58ce-125">使用階層式 Nuget.Config 檔案時，repositoryPath 索引鍵不被接受 Nuget.Config 檔案的最接近方案根目錄。</span><span class="sxs-lookup"><span data-stu-id="e58ce-125">When using hierarchical Nuget.Config files, the repositoryPath key was not being honored for Nuget.Config files closest to the solution root.</span></span> <span data-ttu-id="e58ce-126">在 Visual Studio 2013 中，NuGet 會安裝在 %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config 自訂 Nuget.Config 檔案以加入 < Microsoft 和.NET 封裝來源。</span><span class="sxs-lookup"><span data-stu-id="e58ce-126">In Visual Studio 2013, NuGet installs a custom Nuget.Config file at %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config in order to add the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="e58ce-127">如此一來，解決在方案中使用自訂的 repositoryPath 已刪除電腦層級 Nuget.Config-這也意味著移除 < Microsoft 和.NET 封裝來源。</span><span class="sxs-lookup"><span data-stu-id="e58ce-127">As a result, the work-around for using a custom repositoryPath in a solution was to delete the machine-level Nuget.Config - which also meant removing the "Microsoft and .NET" package source.</span></span> <span data-ttu-id="e58ce-128">使用階層式 Nuget.Config 檔案時，NuGet 2.7.2 現在會接受 repositoryPath 優先順序規則。</span><span class="sxs-lookup"><span data-stu-id="e58ce-128">NuGet 2.7.2 now honors the precedence rules for repositoryPath when using hierarchical Nuget.Config files.</span></span>

## <a name="all-changes"></a><span data-ttu-id="e58ce-129">所有的變更</span><span class="sxs-lookup"><span data-stu-id="e58ce-129">All Changes</span></span>
<span data-ttu-id="e58ce-130">如需完整的工作清單項目固定在 NuGet 2.7.2，請檢視[此版本的 NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)。</span><span class="sxs-lookup"><span data-stu-id="e58ce-130">For a full list of work items fixed in NuGet 2.7.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).</span></span>
