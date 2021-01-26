---
title: NuGet 2.8.6 版本資訊
description: NuGet 2.8.6 的版本資訊，包含已知問題、bug 修正、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776698"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="63f15-103">NuGet 2.8.6 版本資訊</span><span class="sxs-lookup"><span data-stu-id="63f15-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="63f15-104">[NuGet 2.8.5 版本](../release-notes/nuget-2.8.5.md)  |  資訊[NuGet 2.8.7 版本](../release-notes/nuget-2.8.7.md)資訊</span><span class="sxs-lookup"><span data-stu-id="63f15-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="63f15-105">NuGet 2.8.6 已于2015年7月20日發行為 2.8.5 VSIX 的次要更新，並提供一些目標修正和增強功能，以支援可透過 Windows 10 UWP 開發模型提供支援的封裝。</span><span class="sxs-lookup"><span data-stu-id="63f15-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="63f15-106">此版本的 NuGet 套件管理員延伸模組僅提供 Visual Studio 2013 的支援。</span><span class="sxs-lookup"><span data-stu-id="63f15-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="63f15-107">在此版本中，NuGet 封裝管理員對話方塊已新增下列功能的支援：</span><span class="sxs-lookup"><span data-stu-id="63f15-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="63f15-108">引進了 UAP 目標 Framework 的標記，以支援 Windows 10 應用程式開發。</span><span class="sxs-lookup"><span data-stu-id="63f15-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="63f15-109">NuGet 通訊協定第3版端點</span><span class="sxs-lookup"><span data-stu-id="63f15-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="63f15-110">支援在存放庫來源上 [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 屬性。</span><span class="sxs-lookup"><span data-stu-id="63f15-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="63f15-111">預設值為 "2"</span><span class="sxs-lookup"><span data-stu-id="63f15-111">Default value is "2"</span></span>
* <span data-ttu-id="63f15-112">在本機快取中無法使用必要的套件版本時，回復至遠端存放庫</span><span class="sxs-lookup"><span data-stu-id="63f15-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>