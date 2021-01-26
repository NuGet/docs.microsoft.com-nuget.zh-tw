---
title: 適用于 WebMatrix 的 NuGet 2.6.1 版本資訊
description: 適用于 WebMatrix 的 NuGet 2.6.1 版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780417"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="96f23-103">適用于 WebMatrix 的 NuGet 2.6.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="96f23-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="96f23-104">[NuGet 2.6 版本](../release-notes/nuget-2.6.md)  |  資訊[NuGet 2.7 版本](../release-notes/nuget-2.7.md)資訊</span><span class="sxs-lookup"><span data-stu-id="96f23-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="96f23-105">NuGet 小組在2014年3月26日發行了 WebMatrix 的更新 NuGet 封裝管理員延伸模組。</span><span class="sxs-lookup"><span data-stu-id="96f23-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="96f23-106">您可以使用下列步驟，從 [WebMatrix 擴充功能庫](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) 安裝此更新：</span><span class="sxs-lookup"><span data-stu-id="96f23-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="96f23-107">開啟 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="96f23-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="96f23-108">按一下 [首頁] 功能區中的延伸模組圖示</span><span class="sxs-lookup"><span data-stu-id="96f23-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="96f23-109">選取 [更新] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="96f23-109">Select the Updates tab</span></span>
1. <span data-ttu-id="96f23-110">按一下以將 NuGet 封裝管理員更新為2.6。1</span><span class="sxs-lookup"><span data-stu-id="96f23-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="96f23-111">關閉並重新啟動 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="96f23-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="96f23-112">值得注意的變更</span><span class="sxs-lookup"><span data-stu-id="96f23-112">Notable Changes</span></span>

<span data-ttu-id="96f23-113">此延伸模組更新解決了使用者在 WebMatrix 中使用 NuGet 套件的兩個最大問題。</span><span class="sxs-lookup"><span data-stu-id="96f23-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="96f23-114">第一個是 NuGet 架構版本錯誤，第二個是在資料夾中導致零位元組 Dll 的錯誤（bug） `bin` 。</span><span class="sxs-lookup"><span data-stu-id="96f23-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="96f23-115">NuGet 架構版本錯誤</span><span class="sxs-lookup"><span data-stu-id="96f23-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="96f23-116">由於 WebMatrix 3 已發行，因此已將新功能引進 NuGet 套件，需要新的架構版本。</span><span class="sxs-lookup"><span data-stu-id="96f23-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="96f23-117">當您嘗試在網站中管理 NuGet 套件時，這些新的封裝可能會導致您在 WebMatrix 中看到的錯誤。</span><span class="sxs-lookup"><span data-stu-id="96f23-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![發生錯誤。](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="96f23-121">此最新版本提供與最新 NuGet 套件的相容性，以防止發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="96f23-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="96f23-122">新版本的套件（包括 Microsoft）現在可以安裝在 WebMatrix 中。</span><span class="sxs-lookup"><span data-stu-id="96f23-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="96f23-123">其中有些套件使用 NuGet 功能，例如 XDT 設定 [轉換](../release-notes/nuget-2.6.md#xdt)，在 WebMatrix 中不受支援。</span><span class="sxs-lookup"><span data-stu-id="96f23-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="96f23-124">在 bin 資料夾中 Zero-Byte Dll</span><span class="sxs-lookup"><span data-stu-id="96f23-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="96f23-125">有些使用者在安裝包含複製到 bin 之 Dll 的 WebMatrix 中安裝 NuGet 套件之後，會發現 Dll 會以0位元組檔案的 `bin` 形式顯示在資料夾中。</span><span class="sxs-lookup"><span data-stu-id="96f23-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="96f23-126">這會在執行時間中斷應用程式。</span><span class="sxs-lookup"><span data-stu-id="96f23-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="96f23-127">現在已修正[此問題](https://nuget.codeplex.com/workitem/4060)。</span><span class="sxs-lookup"><span data-stu-id="96f23-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="96f23-128">其他最近的改進</span><span class="sxs-lookup"><span data-stu-id="96f23-128">Other Recent Improvements</span></span>

<span data-ttu-id="96f23-129">針對 Visual Studio 發行 NuGet 封裝管理員2.8 時，我們也發行了適用于 WebMatrix 的 NuGet 封裝管理員2.5.0。</span><span class="sxs-lookup"><span data-stu-id="96f23-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="96f23-130">雖然 [NuGet 2.8 版本](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)資訊中提及這一點，但我們並未提及更新所引進的特定新功能。</span><span class="sxs-lookup"><span data-stu-id="96f23-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="96f23-131">全部更新</span><span class="sxs-lookup"><span data-stu-id="96f23-131">Update All</span></span>

<span data-ttu-id="96f23-132">您現在可以在一個步驟中更新所有網站套件！</span><span class="sxs-lookup"><span data-stu-id="96f23-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="96f23-133">當您在 WebMatrix 中開啟 NuGet 擴充功能時，您會看到資源庫上的所有套件清單、已安裝的套件，以及有可用更新的套件。</span><span class="sxs-lookup"><span data-stu-id="96f23-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="96f23-134">先前，每個套件都必須個別更新，但現在會在 [更新] 索引標籤上顯示有用的 [全部更新] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="96f23-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![按一下 [全部更新] 以更新具有可用更新的所有套件](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="96f23-136">覆寫現有的檔案</span><span class="sxs-lookup"><span data-stu-id="96f23-136">Overwrite Existing Files</span></span>

<span data-ttu-id="96f23-137">當您安裝的套件中包含已存在於您的網站中的檔案時，NuGet 一律只會以無訊息方式略過這些檔案， (保留現有的檔案) 。</span><span class="sxs-lookup"><span data-stu-id="96f23-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="96f23-138">這可能會導致您認為封裝已正確安裝或更新，但事實上並不是。</span><span class="sxs-lookup"><span data-stu-id="96f23-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="96f23-139">NuGet 現在會提示您輸入要覆寫的檔案。</span><span class="sxs-lookup"><span data-stu-id="96f23-139">NuGet will now prompt for files to be overwritten.</span></span>

![檔案衝突解決](./media/NuGet-2.8/webmatrix-overwrite-file.png)
