---
title: "NuGet 3.0 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "版本資訊包含 NuGet 3.0.0 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 3.0.0 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 65251b28093d2ac275053b8bfef6620e16e3fb4a
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="d6d71-104">NuGet 3.0 版本資訊</span><span class="sxs-lookup"><span data-stu-id="d6d71-104">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="d6d71-105">[NuGet 3.0 RC2 版本資訊](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 版本資訊](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="d6d71-105">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="d6d71-106">NuGet 3.0 為配套延伸至 Visual Studio 2015 發行於 2015 年 7 月 20 日。</span><span class="sxs-lookup"><span data-stu-id="d6d71-106">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="d6d71-107">我們推入傳遞此版本與 Visual Studio，讓完整的更新的 NuGet 3.0 經驗會是適用於新的 Visual Studio 使用者。</span><span class="sxs-lookup"><span data-stu-id="d6d71-107">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="d6d71-108">此 NuGet 延伸模組版本只適用於 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="d6d71-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="d6d71-109">我們建議您有存取權，可供使用，因為我們會包含支援 Windows 10 開發的 Visual Studio 2015 發行後，馬上發佈更新的最新版本更新 Visual Studio 組件庫的開發人員。</span><span class="sxs-lookup"><span data-stu-id="d6d71-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="d6d71-110">總共我們關閉 240 在 3.0 版中，問題，而且您可以檢閱[GitHub 上的問題的完整清單](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)。</span><span class="sxs-lookup"><span data-stu-id="d6d71-110">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="d6d71-111">已知問題</span><span class="sxs-lookup"><span data-stu-id="d6d71-111">Known Issues</span></span>

<span data-ttu-id="d6d71-112">沒有提供幾個使用此版本中，傳遞的已知問題，而且所有這些項目會在與 Windows 10 版本一致。 上年 7 月 29 我們排定 3.1 版本中修正。</span><span class="sxs-lookup"><span data-stu-id="d6d71-112">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="d6d71-113">也可以更新您的 Visual Studio 擴充功能，從組件庫上該日期或之後修正這些已知的問題。</span><span class="sxs-lookup"><span data-stu-id="d6d71-113">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="d6d71-114">未提供轉譯為 「 不要顯示此訊息 」 索引標籤上 [預覽] 視窗和 「 著作人 」 標籤封裝描述視窗中。</span><span class="sxs-lookup"><span data-stu-id="d6d71-114">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="d6d71-115">當您使用 TFS 處理專案原始檔控制時，NuGet 無法顯示封裝管理員的使用者介面 Nuget.Config 檔案標示為唯讀。</span><span class="sxs-lookup"><span data-stu-id="d6d71-115">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="d6d71-116">**因應措施**簽出檔案，從 TFS。</span><span class="sxs-lookup"><span data-stu-id="d6d71-116">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="d6d71-117">黃色 NuGet Powershell 視窗中的 「 重新啟動列 」 中的文字不是可見的當您使用 Visual Studio 暗色調佈景主題。</span><span class="sxs-lookup"><span data-stu-id="d6d71-117">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="d6d71-118">**因應措施**使用 Visual Studio 淺色佈景主題。</span><span class="sxs-lookup"><span data-stu-id="d6d71-118">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="d6d71-119">最常發生的問題已解決的摘要</span><span class="sxs-lookup"><span data-stu-id="d6d71-119">Summary of top issues resolved</span></span>

* [<span data-ttu-id="d6d71-120">封裝管理員 視窗中重新整理時，呼叫經常網路更新</span><span class="sxs-lookup"><span data-stu-id="d6d71-120">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="d6d71-121">變更為安裝在封裝管理員的檢視時，延遲捲軸</span><span class="sxs-lookup"><span data-stu-id="d6d71-121">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="d6d71-122">應在背景執行緒上執行的網路呼叫</span><span class="sxs-lookup"><span data-stu-id="d6d71-122">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* <span data-ttu-id="d6d71-123">[加入 [不顯示預覽視窗] 核取方塊](https://github.com/NuGet/Home/issues/566)</span><span class="sxs-lookup"><span data-stu-id="d6d71-123">[Added 'Do not show preview window' checkbox](https://github.com/NuGet/Home/issues/566)</span></span>
* [<span data-ttu-id="d6d71-124">加入的處理序節流來減少處理器使用量</span><span class="sxs-lookup"><span data-stu-id="d6d71-124">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="d6d71-125">改良的可攜式類別庫參考處理</span><span class="sxs-lookup"><span data-stu-id="d6d71-125">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="d6d71-126">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="d6d71-126">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="d6d71-127">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="d6d71-127">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="d6d71-128">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="d6d71-128">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="d6d71-129">「 自動完成 」 服務是區分大小寫</span><span class="sxs-lookup"><span data-stu-id="d6d71-129">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="d6d71-130">若要重新引入基本驗證認證的更新</span><span class="sxs-lookup"><span data-stu-id="d6d71-130">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="d6d71-131">改良的錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="d6d71-131">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="d6d71-132">呼叫更新封裝時改善的 powershell 錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="d6d71-132">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="d6d71-133">固定 '深入了解選項' 連結，以防止在 Windows 10 上損毀</span><span class="sxs-lookup"><span data-stu-id="d6d71-133">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="d6d71-134">請記住發行前版本核取方塊設定</span><span class="sxs-lookup"><span data-stu-id="d6d71-134">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="d6d71-135">藉由跨專案的方案中快取結果改善蒐集效能</span><span class="sxs-lookup"><span data-stu-id="d6d71-135">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="d6d71-136">您可以收集多個封裝，以平行方式</span><span class="sxs-lookup"><span data-stu-id="d6d71-136">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="d6d71-137">安裝套件中移除-強制執行命令</span><span class="sxs-lookup"><span data-stu-id="d6d71-137">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="d6d71-138">請持續監控[我們的部落格](http://blog.nuget.org)詳細進度及公告隨著準備好將提供對 Windows 10 開發的支援。</span><span class="sxs-lookup"><span data-stu-id="d6d71-138">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>