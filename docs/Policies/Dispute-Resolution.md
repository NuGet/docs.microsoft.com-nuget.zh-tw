---
title: "NuGet 套件名稱爭議解決方案 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "解決 NuGet 套件發行者之間有關品牌、商標和其他衝突情況爭議的程序。"
keywords: "NuGet 套件爭議, NuGet 爭議解決方法, 爭議解決程序"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 589fe4e7d2b05f3d589dcc70e78e7199d7e717c8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="bf932-104">解決 NuGet 套件名稱的爭議</span><span class="sxs-lookup"><span data-stu-id="bf932-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="bf932-105">本文提供解決社群成員與其他 NuGet 發行者發生爭議的建議解決方法流程。</span><span class="sxs-lookup"><span data-stu-id="bf932-105">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="bf932-106">例如，假設 Northwind Traders 建立了 CRM 系統，並從其網站提供用戶端驅動程式作為可下載的 MSI。</span><span class="sxs-lookup"><span data-stu-id="bf932-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="bf932-107">而獨立開發人員 Nancy，想要更輕鬆地使用 Northwind 的用戶端程式庫，並將它轉換成 NuGet 套件，稱之為 `NorthwindTraders.Client`。</span><span class="sxs-lookup"><span data-stu-id="bf932-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="bf932-108">在此之後，Northwind 想要產生自己的用戶端程式庫官方 NuGet 套件，因此就 Nancy 對套件名稱的擁有權發生爭議。</span><span class="sxs-lookup"><span data-stu-id="bf932-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="bf932-109">在此案例中，Nancy 似乎並無惡意，甚至貢獻了自己的時間和程式碼為 Northwind 的工具和客戶提供支援。</span><span class="sxs-lookup"><span data-stu-id="bf932-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="bf932-110">與此同時，Northwind 是 Northwind 名稱的合法擁有者。</span><span class="sxs-lookup"><span data-stu-id="bf932-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="bf932-111">藉由遵循下列程序，Northwind 和 Nancy 可以協調出適當的解決方式，因為雙方都有意服務開發人員社群。</span><span class="sxs-lookup"><span data-stu-id="bf932-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="bf932-112">NuGet 小組一般沒有必要介入，因為共同作業通常會運作出最佳方案。</span><span class="sxs-lookup"><span data-stu-id="bf932-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="bf932-113">事實上，至今為止，每件引起 NuGet 小組注意的爭議皆不必小組介入公評即已圓滿解決。</span><span class="sxs-lookup"><span data-stu-id="bf932-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>

## <a name="process"></a><span data-ttu-id="bf932-114">處理序</span><span class="sxs-lookup"><span data-stu-id="bf932-114">Process</span></span>

1. <span data-ttu-id="bf932-115">使用套件詳細資料頁面的**連絡擁有者**連結，連絡與您發生爭議的套件擁有者。</span><span class="sxs-lookup"><span data-stu-id="bf932-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="bf932-116">客氣地直接說明您的問題。</span><span class="sxs-lookup"><span data-stu-id="bf932-116">Explain your issue in a kind and direct manner.</span></span>
1. <span data-ttu-id="bf932-117">將您的郵件副本傳送至 [support@nuget.org](mailto:support@nuget.org)，以便 NuGet 和 .NET Foundation 了解您的爭議。</span><span class="sxs-lookup"><span data-stu-id="bf932-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
1. <span data-ttu-id="bf932-118">解決方法的等候期最多 30 天，屆時請再次通知 [support@nuget.org](mailto:support@nuget.org)。</span><span class="sxs-lookup"><span data-stu-id="bf932-118">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="bf932-119">nuget.org 支援小組會介入，嘗試解決雙方爭議。</span><span class="sxs-lookup"><span data-stu-id="bf932-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
