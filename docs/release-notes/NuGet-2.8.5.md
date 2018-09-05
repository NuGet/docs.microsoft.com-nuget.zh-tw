---
title: NuGet 2.8.5 版本資訊
description: 版本資訊 NuGet 2.8.5 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548621"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="70905-103">NuGet 2.8.5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="70905-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="70905-104">[NuGet 2.8.3 版本資訊](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 版本資訊](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="70905-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="70905-105">NuGet 2.8.5 釋放 2015 年 3 月 30 日。</span><span class="sxs-lookup"><span data-stu-id="70905-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="70905-106">它是次要更新到我們 2.8.3 VSIX 某些目標修正。</span><span class="sxs-lookup"><span data-stu-id="70905-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="70905-107">在此版本中，NuGet 套件管理員 對話方塊的支援已針對[DNX 目標 Framework Moniker](https://github.com/aspnet/dnx)。</span><span class="sxs-lookup"><span data-stu-id="70905-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="70905-108">這些新的 framework moniker 的支援包括：</span><span class="sxs-lookup"><span data-stu-id="70905-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="70905-109">**core50** -'base' 的目標 framework moniker (TFM) 與核心 CLR 相容。</span><span class="sxs-lookup"><span data-stu-id="70905-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="70905-110">**dnx452** -使用完整 4.5.2 TFM 特定 DNX 型應用程式的 framework 版本</span><span class="sxs-lookup"><span data-stu-id="70905-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="70905-111">**dnx46** -使用完整 4.6 版本的 framework TFM 特定 DNX 型應用程式</span><span class="sxs-lookup"><span data-stu-id="70905-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="70905-112">**dnxcore50** -使用 framework Core 5.0 版的 TFM 特定 DNX 型應用程式</span><span class="sxs-lookup"><span data-stu-id="70905-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="70905-113">一個 bug 已修正導致無法正確地安裝到 FSharp 專案封裝：</span><span class="sxs-lookup"><span data-stu-id="70905-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400