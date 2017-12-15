---
title: "NuGet 2.8.5 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60b96b2e-2a61-4f10-b5ad-3299f5a6d453
description: "版本資訊包含 NuGet 2.8.5 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 2.8.5 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3b297704968b8423f60e9de08e27860dc375c019
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="ae636-104">NuGet 2.8.5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="ae636-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="ae636-105">[NuGet 2.8.3 版本資訊](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 版本資訊](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="ae636-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="ae636-106">NuGet 2.8.5 2015 年 3 月 30 日發行。</span><span class="sxs-lookup"><span data-stu-id="ae636-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="ae636-107">它是次要更新某些 VSIX 設為我們 2.8.3 目標修正程式。</span><span class="sxs-lookup"><span data-stu-id="ae636-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="ae636-108">在本版中的 NuGet 封裝管理員 新增的支援[DNX 目標 Framework Moniker](https://github.com/aspnet/dnx)。</span><span class="sxs-lookup"><span data-stu-id="ae636-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="ae636-109">這些新的 framework moniker 的支援包括：</span><span class="sxs-lookup"><span data-stu-id="ae636-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="ae636-110">**core50** -'base' 的目標 framework moniker (TFM) 和核心 CLR 相容。</span><span class="sxs-lookup"><span data-stu-id="ae636-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="ae636-111">**dnx452** -使用完整 4.5.2 TFM DNX 為基礎的特定應用程式的 framework 版本</span><span class="sxs-lookup"><span data-stu-id="ae636-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="ae636-112">**dnx46** -使用 framework 完整 4.6 版 TFM DNX 為基礎的特定應用程式</span><span class="sxs-lookup"><span data-stu-id="ae636-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="ae636-113">**dnxcore50** -A TFM DNX 為基礎的特定應用程式使用 framework Core 5.0 版</span><span class="sxs-lookup"><span data-stu-id="ae636-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="ae636-114">一個 bug 已修正無法正確安裝到 FSharp 專案無法在封裝：</span><span class="sxs-lookup"><span data-stu-id="ae636-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="ae636-115">https://nuget.codeplex.com/workitem/4400</span><span class="sxs-lookup"><span data-stu-id="ae636-115">https://nuget.codeplex.com/workitem/4400</span></span>