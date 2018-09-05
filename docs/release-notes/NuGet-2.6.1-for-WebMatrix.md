---
title: NuGet 2.6.1 for WebMatrix 版本資訊
description: Webmatrix 包括已知的問題、 bug 修正、 新增的功能和 Dcr NuGet 2.6.1 的版本資訊。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550313"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="da6ee-103">NuGet 2.6.1 for WebMatrix 版本資訊</span><span class="sxs-lookup"><span data-stu-id="da6ee-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="da6ee-104">[NuGet 2.6 版本資訊](../release-notes/nuget-2.6.md) | [NuGet 2.7 版本資訊](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="da6ee-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="da6ee-105">NuGet 小組發行於 2014 年 3 月 26 日 WebMatrix 更新的 NuGet 套件管理員延伸模組。</span><span class="sxs-lookup"><span data-stu-id="da6ee-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="da6ee-106">可以從安裝此更新[WebMatrix 延伸模組庫](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery)使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="da6ee-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="da6ee-107">開啟 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="da6ee-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="da6ee-108">按一下 [首頁] 功能區中的延伸模組圖示</span><span class="sxs-lookup"><span data-stu-id="da6ee-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="da6ee-109">選取 [更新] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="da6ee-109">Select the Updates tab</span></span>
1. <span data-ttu-id="da6ee-110">按一下以更新 2.6.1 NuGet 套件管理員</span><span class="sxs-lookup"><span data-stu-id="da6ee-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="da6ee-111">關閉並重新啟動 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="da6ee-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="da6ee-112">值得注意的變更</span><span class="sxs-lookup"><span data-stu-id="da6ee-112">Notable Changes</span></span>

<span data-ttu-id="da6ee-113">此延伸模組更新可解決兩個的最大的問題使用者面臨在 WebMatrix 內取用 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="da6ee-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="da6ee-114">第一個是 NuGet 結構描述版本錯誤，且第二個前置零位元組 dll 的 bug`bin`資料夾。</span><span class="sxs-lookup"><span data-stu-id="da6ee-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="da6ee-115">NuGet 的結構描述版本錯誤</span><span class="sxs-lookup"><span data-stu-id="da6ee-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="da6ee-116">WebMatrix 3 已發行，因為新的結構描述版本所需的 NuGet 套件的 nuget 已推出新功能。</span><span class="sxs-lookup"><span data-stu-id="da6ee-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="da6ee-117">管理網站中的 NuGet 封裝時，這些新的封裝可能會導致您在 WebMatrix 中看到的錯誤。</span><span class="sxs-lookup"><span data-stu-id="da6ee-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![發生錯誤。](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="da6ee-121">這個最新版本提供與最新的 NuGet 套件，防止發生此錯誤的相容性。</span><span class="sxs-lookup"><span data-stu-id="da6ee-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="da6ee-122">現在可以在 WebMatrix 中安裝套件包括 Microsoft.AspNet.WebPages 的新版本。</span><span class="sxs-lookup"><span data-stu-id="da6ee-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="da6ee-123">部分這些封裝所使用的 NuGet 功能，例如[XDT 組態轉換](../release-notes/nuget-2.6.md#xdt)，但不支援在 WebMatrix 中到目前為止。</span><span class="sxs-lookup"><span data-stu-id="da6ee-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="da6ee-124">在 bin 資料夾中的零位元組 Dll</span><span class="sxs-lookup"><span data-stu-id="da6ee-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="da6ee-125">安裝 NuGet 封裝在 WebMatrix 中包含 Dll 複製到分類收納，Dll 顯示中之後，某些使用者有報告的`bin`0 位元組檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="da6ee-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="da6ee-126">這會中斷應用程式在執行階段。</span><span class="sxs-lookup"><span data-stu-id="da6ee-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="da6ee-127">[此問題](https://nuget.codeplex.com/workitem/4060)現在已修正。</span><span class="sxs-lookup"><span data-stu-id="da6ee-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="da6ee-128">其他最近的改進功能</span><span class="sxs-lookup"><span data-stu-id="da6ee-128">Other Recent Improvements</span></span>

<span data-ttu-id="da6ee-129">當 NuGet 封裝管理員 2.8 已發行適用於 Visual Studio 中時，我們也會發行 NuGet 套件管理員 2.5.0 for WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="da6ee-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="da6ee-130">雖然這在提到[NuGet 2.8 版本資訊](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)，我們忘了提特定的新功能導入該更新。</span><span class="sxs-lookup"><span data-stu-id="da6ee-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="da6ee-131">全部更新</span><span class="sxs-lookup"><span data-stu-id="da6ee-131">Update All</span></span>

<span data-ttu-id="da6ee-132">您現在可以更新所有網站的套件，在一個步驟中 ！</span><span class="sxs-lookup"><span data-stu-id="da6ee-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="da6ee-133">當您在 WebMatrix 中開啟 NuGet 延伸模組時，您會看到資源庫、 安裝，以及可用的更新以外的所有封裝的清單。</span><span class="sxs-lookup"><span data-stu-id="da6ee-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="da6ee-134">之前，每個套件必須個別更新，但現在已經是有用的 [全部更新] 按鈕，就會出現在 [更新] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="da6ee-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![按一下 [全部更新]，以使用可用的更新來更新所有封裝](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="da6ee-136">覆寫現有檔案</span><span class="sxs-lookup"><span data-stu-id="da6ee-136">Overwrite Existing Files</span></span>

<span data-ttu-id="da6ee-137">安裝套件，其中包含存在於您的網站的檔案時，NuGet 就是一律只以無訊息方式略過這些檔案 （保留現有的檔案）。</span><span class="sxs-lookup"><span data-stu-id="da6ee-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="da6ee-138">這可能會導致封裝已安裝，或當事實上它未正確更新的印象。</span><span class="sxs-lookup"><span data-stu-id="da6ee-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="da6ee-139">NuGet 現在會提示輸入覆寫檔案中。</span><span class="sxs-lookup"><span data-stu-id="da6ee-139">NuGet will now prompt for files to be overwritten.</span></span>

![解決檔案衝突](./media/NuGet-2.8/webmatrix-overwrite-file.png)
