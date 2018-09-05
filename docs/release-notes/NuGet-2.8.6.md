---
title: NuGet 2.8.6 版本資訊
description: 版本資訊 NuGet 2.8.6 包括已知問題、 bug 修正、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546487"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="1beb3-103">NuGet 2.8.6 版本資訊</span><span class="sxs-lookup"><span data-stu-id="1beb3-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="1beb3-104">[NuGet 2.8.5 版本資訊](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 版本資訊](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="1beb3-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="1beb3-105">發行 NuGet 2.8.6 2015 年 7 月 20 日做為我們 2.8.5 次要更新 VSIX 某些目標修正和改善，以支援 Windows 10 UWP 開發模型的支援可能會傳遞的封裝。</span><span class="sxs-lookup"><span data-stu-id="1beb3-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="1beb3-106">這個版本的 NuGet 套件管理員延伸模組提供只適用於 Visual Studio 2013 支援。</span><span class="sxs-lookup"><span data-stu-id="1beb3-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="1beb3-107">在此版本中，[NuGet 套件管理員] 對話方塊會有新增的支援：</span><span class="sxs-lookup"><span data-stu-id="1beb3-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="1beb3-108">導入了 UAP 目標 Framework Moniker，以支援 Windows 10 應用程式開發。</span><span class="sxs-lookup"><span data-stu-id="1beb3-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="1beb3-109">NuGet 通訊協定第 3 版端點</span><span class="sxs-lookup"><span data-stu-id="1beb3-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="1beb3-110">支援[Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 屬性儲存機制來源。</span><span class="sxs-lookup"><span data-stu-id="1beb3-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="1beb3-111">預設值為"2"</span><span class="sxs-lookup"><span data-stu-id="1beb3-111">Default value is "2"</span></span>
* <span data-ttu-id="1beb3-112">正在回復到遠端存放庫如果在本機快取無法使用必要的套件版本</span><span class="sxs-lookup"><span data-stu-id="1beb3-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>