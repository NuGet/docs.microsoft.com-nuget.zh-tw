---
title: NuGet 5.4 版本資訊
description: NuGet 5.4 的版本資訊，包括新功能、bug 修正和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384107"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="d8878-103">NuGet 5.4 版本資訊</span><span class="sxs-lookup"><span data-stu-id="d8878-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="d8878-104">NuGet 配送車：</span><span class="sxs-lookup"><span data-stu-id="d8878-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d8878-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="d8878-105">NuGet version</span></span> | <span data-ttu-id="d8878-106">隨附於 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="d8878-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d8878-107">隨附於 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d8878-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d8878-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="d8878-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d8878-109">Visual Studio 2019 16.4 版</span><span class="sxs-lookup"><span data-stu-id="d8878-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d8878-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d8878-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="d8878-111"><sup>1</sup>以含 .NET Core 工作負載的 Visual Studio 2019 安裝</span><span class="sxs-lookup"><span data-stu-id="d8878-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="d8878-112">摘要：5.4 中的新功能</span><span class="sxs-lookup"><span data-stu-id="d8878-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="d8878-113">更快速的解決方案載入時間-第一次載入解決方案時，執行 NuGet 程式碼的額外負荷已透過部分-ngen 降低，以減少 JIT 成本- [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="d8878-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="d8878-114">新 helper 函式-提供套件識別碼和版本清單，取得可能的最上層套件。</span><span class="sxs-lookup"><span data-stu-id="d8878-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="d8878-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="d8878-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

* <span data-ttu-id="d8878-116">在[GitHub 動作](https://github.com/features/actions)上安裝和設定 nuget.exe 的新[`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions)動作。</span><span class="sxs-lookup"><span data-stu-id="d8878-116">New [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) action for installing and configuring NuGet.exe on [GitHub Actions](https://github.com/features/actions).</span></span><span data-ttu-id="d8878-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span><span class="sxs-lookup"><span data-stu-id="d8878-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d8878-118">本版已修正的問題</span><span class="sxs-lookup"><span data-stu-id="d8878-118">Issues fixed in this release</span></span>

<span data-ttu-id="d8878-119">**Bug**</span><span class="sxs-lookup"><span data-stu-id="d8878-119">**Bugs**</span></span>

* <span data-ttu-id="d8878-120">外掛程式： linux/Mac 上的記錄時間準確度已關閉- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="d8878-120">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="d8878-121">處置外掛程式有時可能會擲回並使整個作業失敗。</span><span class="sxs-lookup"><span data-stu-id="d8878-121">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="d8878-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="d8878-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="d8878-123">在 PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)中停止顯示 [允許] 和 [封鎖的版本] 清單中的版本重複</span><span class="sxs-lookup"><span data-stu-id="d8878-123">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="d8878-124">鎖定檔案未正確產生-架構順序應該不會影響 restore with lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="d8878-124">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="d8878-125">在 SDK 3.0.100 中設定 <RuntimeIdentifiers> 的專案 LockFile 驗證失敗- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="d8878-125">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="d8878-126">簽署驗證現在會使用具有相同 OID 之2個值的時間戳記，正確地拒絕簽章[#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="d8878-126">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="d8878-127">更新授權清單- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="d8878-127">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="d8878-128">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="d8878-128">**DCRs**</span></span>

* <span data-ttu-id="d8878-129">將診斷檔案上架至 IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="d8878-129">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="d8878-130">**[此版本中已修正的所有問題清單-5。4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="d8878-130">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
