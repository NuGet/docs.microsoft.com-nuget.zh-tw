---
title: "NuGet 2.8.6 版本資訊 |Microsoft 文件"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "版本資訊包含 NuGet 2.8.6 已知問題、 錯誤修正、 新增的功能，以及 Dcr。"
keywords: "NuGet 2.8.6 版本資訊，將 bug 修正、 已知問題、 已新增的功能，Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f33c1edd3ef703a8cd97b7bdd97c37e12426aafa
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="f08c1-104">NuGet 2.8.6 版本資訊</span><span class="sxs-lookup"><span data-stu-id="f08c1-104">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="f08c1-105">[NuGet 2.8.5 版本資訊](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 版本資訊](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="f08c1-105">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="f08c1-106">發行 NuGet 2.8.6 2015 年 7 月 20 日為我們 2.8.5 的次要更新，但有一些 VSIX 目標修正和增強功能支援 Windows 10 UWP 開發模型的支援可能會傳遞的套件。</span><span class="sxs-lookup"><span data-stu-id="f08c1-106">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="f08c1-107">這個版本的 NuGet 封裝管理員延伸模組會提供僅適用於 Visual Studio 2013 支援。</span><span class="sxs-lookup"><span data-stu-id="f08c1-107">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="f08c1-108">在此版本中，[NuGet 封裝管理員] 對話方塊會有新增的支援：</span><span class="sxs-lookup"><span data-stu-id="f08c1-108">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="f08c1-109">導入了 UAP 目標 Framework Moniker，以支援 Windows 10 應用程式開發。</span><span class="sxs-lookup"><span data-stu-id="f08c1-109">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="f08c1-110">NuGet 的通訊協定第 3 版端點</span><span class="sxs-lookup"><span data-stu-id="f08c1-110">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="f08c1-111">支援[Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 屬性儲存機制來源。</span><span class="sxs-lookup"><span data-stu-id="f08c1-111">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="f08c1-112">預設值為"2"</span><span class="sxs-lookup"><span data-stu-id="f08c1-112">Default value is "2"</span></span>
* <span data-ttu-id="f08c1-113">回到遠端儲存機制如果在本機快取無法使用必要的套件版本</span><span class="sxs-lookup"><span data-stu-id="f08c1-113">Falling back to remote repository if a required package version is not available in the local cache</span></span>