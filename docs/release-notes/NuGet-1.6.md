---
title: NuGet 1.6 版的版本資訊
description: 版本資訊適用於 NuGet 1.6 包括已知的問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549008"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="adbee-103">NuGet 1.6 版的版本資訊</span><span class="sxs-lookup"><span data-stu-id="adbee-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="adbee-104">[NuGet 1.5 版本資訊](../release-notes/nuget-1.5.md) | [NuGet 1.7 版本資訊](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="adbee-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="adbee-105">於 2011 年 12 月 13 日發行 NuGet 1.6。</span><span class="sxs-lookup"><span data-stu-id="adbee-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="adbee-106">已知的安裝問題</span><span class="sxs-lookup"><span data-stu-id="adbee-106">Known Installation Issue</span></span>
<span data-ttu-id="adbee-107">如果您執行的 VS 2010 SP1，您可能會遇到安裝錯誤時嘗試升級 NuGet，如果您已安裝較舊版本。</span><span class="sxs-lookup"><span data-stu-id="adbee-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="adbee-108">因應措施是只解除安裝 NuGet，然後再從 VS 延伸模組資源庫進行安裝。</span><span class="sxs-lookup"><span data-stu-id="adbee-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="adbee-109">請參閱 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="adbee-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="adbee-110">注意： 如果 Visual Studio 不會允許您解除安裝 （解除安裝 按鈕已停用） 的延伸模組，則您可能需要重新啟動 Visual Studio 中使用 「 以系統管理員身分執行 」。</span><span class="sxs-lookup"><span data-stu-id="adbee-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="adbee-111">功能</span><span class="sxs-lookup"><span data-stu-id="adbee-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="adbee-112">支援語意版本設定和發行前版本套件</span><span class="sxs-lookup"><span data-stu-id="adbee-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="adbee-113">NuGet 1.6 版引進了支援語意版本控制 (SemVer)。</span><span class="sxs-lookup"><span data-stu-id="adbee-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="adbee-114">如需如何使用 SemVer 的詳細資訊，請參閱[版本控制說明文件](../create-packages/prerelease-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="adbee-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="adbee-115">使用 NuGet 不簽入套件 （套件還原）</span><span class="sxs-lookup"><span data-stu-id="adbee-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="adbee-116">NuGet 1.6 現在提供工作流程中的 NuGet 套件不會新增至原始檔控制，但改為會還原在建置階段如果遺失的第一級支援。</span><span class="sxs-lookup"><span data-stu-id="adbee-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="adbee-117">如需詳細資訊，請參閱[使用的 NuGet，而不需要認可至原始檔控制的套件](../consume-packages/packages-and-source-control.md)主題。</span><span class="sxs-lookup"><span data-stu-id="adbee-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="adbee-118">安裝 NuGet 套件的項目範本</span><span class="sxs-lookup"><span data-stu-id="adbee-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="adbee-119">為建置基礎的工作，以支援 Visual Studio 專案範本以預先安裝的 NuGet 套件，NuGet 1.6 也新增支援 Visual Studio 項目範本。</span><span class="sxs-lookup"><span data-stu-id="adbee-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="adbee-120">叫用中的範本時所安裝的 NuGet 套件時，項目範本可以有相關聯。</span><span class="sxs-lookup"><span data-stu-id="adbee-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="adbee-121">如需如何變更專案/項目範本，以安裝 NuGet 套件的詳細資訊，請參閱[Visual Studio 範本中的套件](../visual-studio-extensibility/visual-studio-templates.md)主題。</span><span class="sxs-lookup"><span data-stu-id="adbee-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="adbee-122">停用套件來源的支援</span><span class="sxs-lookup"><span data-stu-id="adbee-122">Support for disabling package sources</span></span>
<span data-ttu-id="adbee-123">多個套件來源設定時，NuGet 會安裝封裝及其相依性期間尋找套件的每個。</span><span class="sxs-lookup"><span data-stu-id="adbee-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="adbee-124">已關閉，因為某些原因可以嚴重會拖慢 NuGet 的套件來源。</span><span class="sxs-lookup"><span data-stu-id="adbee-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="adbee-125">NuGet 1.6 中，您無法移除封裝來源，但接著您必須記得的詳細資料，為您想要將其新增回去。</span><span class="sxs-lookup"><span data-stu-id="adbee-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="adbee-126">NuGet 1.6 版可讓您取消核取 停用它，但保留該套件來源。</span><span class="sxs-lookup"><span data-stu-id="adbee-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![停用封裝](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="adbee-128">Bug 修正</span><span class="sxs-lookup"><span data-stu-id="adbee-128">Bug Fixes</span></span>
<span data-ttu-id="adbee-129">NuGet 1.6 必須共 106 工作固定的項目。</span><span class="sxs-lookup"><span data-stu-id="adbee-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="adbee-130">95 這些已分類為 bug，10，這些是功能。</span><span class="sxs-lookup"><span data-stu-id="adbee-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="adbee-131">如需完整的工作清單項目固定在 NuGet 1.6 中，請檢視[此版本的 NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="adbee-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
