---
title: NuGet 3.0 RC2 版本資訊
description: NuGet 3.0 RC2 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780277"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="95790-103">NuGet 3.0 RC2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="95790-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="95790-104">[NuGet 3.0 RC 版本](../release-notes/nuget-3.0-RC.md)  |  資訊[NuGet 3.0 版本](../release-notes/nuget-3.0.0.md)資訊</span><span class="sxs-lookup"><span data-stu-id="95790-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="95790-105">NuGet 3.0 RC2 發行于2015年6月3日，作為 Visual Studio 2015 擴充功能庫和 [Codeplex](https://nuget.codeplex.com/releases/view/615507)提供的過渡版。</span><span class="sxs-lookup"><span data-stu-id="95790-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="95790-106">此版本有許多重要的 bug 修正和效能改進，我們認為在完成的 Visual Studio 2015 版之前必須先釋出。</span><span class="sxs-lookup"><span data-stu-id="95790-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="95790-107">此 NuGet 擴充功能版本僅適用于 Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="95790-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="95790-108">我們在此版本中已關閉158問題，您可以在 [GitHub 上查看問題的完整清單](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)。</span><span class="sxs-lookup"><span data-stu-id="95790-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="95790-109">已解決常見問題的摘要</span><span class="sxs-lookup"><span data-stu-id="95790-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="95790-110">當套件管理員視窗重新整理時頻繁的網路更新呼叫</span><span class="sxs-lookup"><span data-stu-id="95790-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="95790-111">在封裝管理員中變更為已安裝的視圖時，延遲捲軸</span><span class="sxs-lookup"><span data-stu-id="95790-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="95790-112">應在背景執行緒上執行網路呼叫</span><span class="sxs-lookup"><span data-stu-id="95790-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* <span data-ttu-id="95790-113">[已新增 [不要顯示預覽視窗] 核取方塊](https://github.com/NuGet/Home/issues/566)</span><span class="sxs-lookup"><span data-stu-id="95790-113">[Added 'Do not show preview window' checkbox](https://github.com/NuGet/Home/issues/566)</span></span>
* [<span data-ttu-id="95790-114">已新增進程節流來降低處理器使用量</span><span class="sxs-lookup"><span data-stu-id="95790-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="95790-115">改良的便攜類別程式庫參考處理</span><span class="sxs-lookup"><span data-stu-id="95790-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="95790-116">自動完成服務區分大小寫</span><span class="sxs-lookup"><span data-stu-id="95790-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="95790-117">更新以重新引入基本驗證認證</span><span class="sxs-lookup"><span data-stu-id="95790-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="95790-118">已改善錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="95790-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="95790-119">已改善呼叫更新套件時的 powershell 錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="95790-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="95790-120">從 Codeplex 將此 [更新下載到 nuget 擴充](https://nuget.codeplex.com/releases/view/615507) 功能，請留意我們的 [blog](http://blog.nuget.org) ，以取得更多 nuget 3.0 的進度和公告！</span><span class="sxs-lookup"><span data-stu-id="95790-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>