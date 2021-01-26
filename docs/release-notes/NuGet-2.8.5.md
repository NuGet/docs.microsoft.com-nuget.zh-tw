---
title: NuGet 2.8.5 版本資訊
description: NuGet 2.8.5 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780350"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="71160-103">NuGet 2.8.5 版本資訊</span><span class="sxs-lookup"><span data-stu-id="71160-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="71160-104">[NuGet 2.8.3 版本](../release-notes/nuget-2.8.3.md)  |  資訊[NuGet 2.8.6 版本](../release-notes/nuget-2.8.6.md)資訊</span><span class="sxs-lookup"><span data-stu-id="71160-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="71160-105">NuGet 2.8.5 已于2015年3月30日發行。</span><span class="sxs-lookup"><span data-stu-id="71160-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="71160-106">這是 2.8.3 VSIX 的次要更新，包含一些目標修正。</span><span class="sxs-lookup"><span data-stu-id="71160-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="71160-107">在此版本中，已針對 [DNX 目標 Framework 的名字](https://github.com/aspnet/dnx)已新增 NuGet 封裝管理員的支援對話方塊。</span><span class="sxs-lookup"><span data-stu-id="71160-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="71160-108">支援的新 framework 標記包括：</span><span class="sxs-lookup"><span data-stu-id="71160-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="71160-109">**core50** -A ' base ' 目標 framework 標記 (TFM 與核心 CLR 相容的) 。</span><span class="sxs-lookup"><span data-stu-id="71160-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="71160-110">**dnx452** -使用完整4.5.2 版架構的 DNX 型應用程式專用 TFM</span><span class="sxs-lookup"><span data-stu-id="71160-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="71160-111">**dnx46** -使用完整4.6 版架構的 DNX 型應用程式專用 TFM</span><span class="sxs-lookup"><span data-stu-id="71160-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="71160-112">**dnxcore50** -使用核心5.0 版架構的 DNX 型應用程式專用 TFM</span><span class="sxs-lookup"><span data-stu-id="71160-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="71160-113">修正了一個錯誤，導致套件無法正確安裝至 Fsharp.core 專案：</span><span class="sxs-lookup"><span data-stu-id="71160-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400