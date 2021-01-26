---
title: NuGet 2.2 版本資訊
description: NuGet 2.2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780428"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="3bce4-103">NuGet 2.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="3bce4-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="3bce4-104">[NuGet 2.1 版本](../release-notes/nuget-2.1.md)  |  資訊[NuGet 2.2.1 版本](../release-notes/nuget-2.2.1.md)資訊</span><span class="sxs-lookup"><span data-stu-id="3bce4-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="3bce4-105">NuGet 2.2 已于2012年12月12日發行。</span><span class="sxs-lookup"><span data-stu-id="3bce4-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="3bce4-106">Visual Studio 快速啟動</span><span class="sxs-lookup"><span data-stu-id="3bce4-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="3bce4-107">在 Visual Studio 2012 中新增的其中一個新功能是 [ [快速啟動] 對話方塊](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)。</span><span class="sxs-lookup"><span data-stu-id="3bce4-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="3bce4-108">NuGet 2.2 會擴充此對話方塊，讓它能夠使用快速啟動中輸入的搜尋字詞來初始化 [套件管理員] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3bce4-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="3bce4-109">例如，在 [快速啟動] 中輸入 ' jquery ' 現在會在結果中包含一個選項，以搜尋與 ' jquery ' 相符的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="3bce4-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Visual Studio 快速啟動中的 NuGet](./media/quick-launch.png)

<span data-ttu-id="3bce4-111">選取此選項將會啟動「jquery」一詞的標準 NuGet 套件管理員搜尋體驗。</span><span class="sxs-lookup"><span data-stu-id="3bce4-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![預先填入的 NuGet 封裝管理員對話方塊](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="3bce4-113">針對套件內容指定整個資料夾</span><span class="sxs-lookup"><span data-stu-id="3bce4-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="3bce4-114">NuGet 2.2 現在可讓您在檔案的元素中指定整個資料夾， `<file>` `.nuspec` 以包含該資料夾的所有內容。</span><span class="sxs-lookup"><span data-stu-id="3bce4-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="3bce4-115">例如，下列程式碼會在套件安裝至專案時，將封裝腳本資料夾中的所有腳本新增至 contents\scripts 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3bce4-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="3bce4-116">**更新6/24/16：安裝套件時，會忽略 [內容] 資料夾中的空資料夾。**</span><span class="sxs-lookup"><span data-stu-id="3bce4-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="3bce4-117">已知問題</span><span class="sxs-lookup"><span data-stu-id="3bce4-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="3bce4-118">使用套件管理員主控台時，F # 專案的套件安裝失敗</span><span class="sxs-lookup"><span data-stu-id="3bce4-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="3bce4-119">使用套件管理員主控台嘗試將 NuGet 套件安裝到 F # 專案時，會擲回 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="3bce4-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="3bce4-120">我們正積極使用 F # 小組來解決問題，但在此情況下，因應措施是透過 NuGet 的 [套件管理員] 對話方塊（而不是主控台）將 NuGet 套件安裝到 F # 專案中。</span><span class="sxs-lookup"><span data-stu-id="3bce4-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="3bce4-121">您[可以在 CodePlex 上取得詳細資訊](http://nuget.codeplex.com/workitem/2873)。</span><span class="sxs-lookup"><span data-stu-id="3bce4-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="3bce4-122">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="3bce4-122">Bug Fixes</span></span>
<span data-ttu-id="3bce4-123">NuGet 2.2 包含許多 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="3bce4-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="3bce4-124">如需 NuGet 2.2 中已修正之工作專案的完整清單，請參閱 [此版本的 Nuget 問題追蹤程式](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="3bce4-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
