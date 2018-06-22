---
title: NuGet 3.0 RC2 版本資訊
description: 版本資訊 NuGet 3.0 RC2 包括已知的問題、 錯誤修正、 新增的功能，以及 Dcr。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eb8b514fa967cc6ef850483b6b2a5df3ab27a550
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819880"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="67c8b-103">NuGet 3.0 RC2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="67c8b-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="67c8b-104">[NuGet 3.0 RC 版本資訊](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 版本資訊](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="67c8b-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="67c8b-105">從 Visual Studio 2015 擴充功能庫可用的過渡期版本與 NuGet 3.0 RC2 發行於 2015 年 6 月 3 日和[Codeplex](https://nuget.codeplex.com/releases/view/615507)。</span><span class="sxs-lookup"><span data-stu-id="67c8b-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="67c8b-106">此版本有一些重要的 bug 修正和效能增強功能，我們認為重要已完成 Visual Studio 2015 發行前版本。</span><span class="sxs-lookup"><span data-stu-id="67c8b-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="67c8b-107">此 NuGet 延伸模組版本只適用於 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="67c8b-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="67c8b-108">總共我們關閉 158 在本版中的問題，而且您可以檢閱[GitHub 上的問題的完整清單](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)。</span><span class="sxs-lookup"><span data-stu-id="67c8b-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="67c8b-109">最常發生的問題已解決的摘要</span><span class="sxs-lookup"><span data-stu-id="67c8b-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="67c8b-110">封裝管理員 視窗中重新整理時，呼叫經常網路更新</span><span class="sxs-lookup"><span data-stu-id="67c8b-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="67c8b-111">變更為安裝在封裝管理員的檢視時，延遲捲軸</span><span class="sxs-lookup"><span data-stu-id="67c8b-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="67c8b-112">應在背景執行緒上執行的網路呼叫</span><span class="sxs-lookup"><span data-stu-id="67c8b-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* <span data-ttu-id="67c8b-113">[加入 [不顯示預覽視窗] 核取方塊](https://github.com/NuGet/Home/issues/566)</span><span class="sxs-lookup"><span data-stu-id="67c8b-113">[Added 'Do not show preview window' checkbox](https://github.com/NuGet/Home/issues/566)</span></span>
* [<span data-ttu-id="67c8b-114">加入的處理序節流來減少處理器使用量</span><span class="sxs-lookup"><span data-stu-id="67c8b-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="67c8b-115">改良的可攜式類別庫參考處理</span><span class="sxs-lookup"><span data-stu-id="67c8b-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="67c8b-116">「 自動完成 」 服務是區分大小寫</span><span class="sxs-lookup"><span data-stu-id="67c8b-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="67c8b-117">若要重新引入基本驗證認證的更新</span><span class="sxs-lookup"><span data-stu-id="67c8b-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="67c8b-118">改良的錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="67c8b-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="67c8b-119">呼叫更新封裝時改善的 powershell 錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="67c8b-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="67c8b-120">下載此[NuGet 延伸模組更新](https://nuget.codeplex.com/releases/view/615507)從 Codeplex 和請持續監控[我們的部落格](http://blog.nuget.org)詳細進度及針對 NuGet 3.0 公告 ！</span><span class="sxs-lookup"><span data-stu-id="67c8b-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>