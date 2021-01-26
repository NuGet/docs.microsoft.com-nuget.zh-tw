---
title: NuGet 5.4 版本資訊
description: NuGet 5.4 的版本資訊，包括新功能、bug 修正及 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: dd4c10672db3a65b68f18636105ee55ab09da7ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776179"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="a57ca-103">NuGet 5.4 版本資訊</span><span class="sxs-lookup"><span data-stu-id="a57ca-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="a57ca-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="a57ca-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="a57ca-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="a57ca-105">NuGet version</span></span> | <span data-ttu-id="a57ca-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="a57ca-106">Available in Visual Studio version</span></span>| <span data-ttu-id="a57ca-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a57ca-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="a57ca-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="a57ca-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a57ca-109">Visual Studio 2019 16.4 版</span><span class="sxs-lookup"><span data-stu-id="a57ca-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a57ca-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="a57ca-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="a57ca-111"><sup>1</sup>使用 .NET Core 工作負載搭配 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="a57ca-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="a57ca-112">摘要：5.4 中的新功能</span><span class="sxs-lookup"><span data-stu-id="a57ca-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="a57ca-113">更快速的解決方案載入時間-第一個解決方案載入期間執行 NuGet 程式碼的額外負荷已透過部分 ngen 減少，以降低 JIT 成本 [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="a57ca-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="a57ca-114">新的 helper 函式-提供套件識別碼和版本的清單，取得可能的最上層套件。</span><span class="sxs-lookup"><span data-stu-id="a57ca-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="a57ca-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="a57ca-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

* <span data-ttu-id="a57ca-116">[`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions)在[GitHub Actions](https://github.com/features/actions)上安裝和設定 NuGet.exe 的新動作。</span><span class="sxs-lookup"><span data-stu-id="a57ca-116">New [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) action for installing and configuring NuGet.exe on [GitHub Actions](https://github.com/features/actions).</span></span><span data-ttu-id="a57ca-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span><span class="sxs-lookup"><span data-stu-id="a57ca-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="a57ca-118">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="a57ca-118">Issues fixed in this release</span></span>

<span data-ttu-id="a57ca-119">**Bug**</span><span class="sxs-lookup"><span data-stu-id="a57ca-119">**Bugs**</span></span>

* <span data-ttu-id="a57ca-120">外掛程式： linux/Mac 上的記錄時間精確度已關閉- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="a57ca-120">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="a57ca-121">處置外掛程式有時可能會擲回並讓整個作業失敗。</span><span class="sxs-lookup"><span data-stu-id="a57ca-121">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="a57ca-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="a57ca-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="a57ca-123">停止在 PMUI 中于允許和封鎖的版本清單中顯示版本重複專案- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="a57ca-123">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="a57ca-124">鎖定檔案未正確產生-架構排序不應該影響 restore with lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="a57ca-124">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="a57ca-125">針對 SDK 3.0.100 中設定的專案，LockFile 驗證失敗 <RuntimeIdentifiers> - [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="a57ca-125">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="a57ca-126">簽署驗證現在會正確地拒絕具有時間戳記的簽章，這在相同的 OID 下有2個值 [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="a57ca-126">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="a57ca-127">更新授權清單- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="a57ca-127">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="a57ca-128">**DCR**</span><span class="sxs-lookup"><span data-stu-id="a57ca-128">**DCRs**</span></span>

* <span data-ttu-id="a57ca-129">將診斷檔案上架到 IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="a57ca-129">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="a57ca-130">**[此版本修正的所有問題清單-5。4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="a57ca-130">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
