---
title: NuGet 套件名稱爭議解決方案
description: 解決 NuGet 套件發行者之間有關品牌、商標和其他衝突情況爭議的程序。
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: d9ed7de95a1f38ea2c288b28958519b1dff0e595
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775660"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>解決 NuGet 套件名稱的爭議

本文提供解決社群成員與其他 NuGet 發行者發生爭議的建議解決方法流程。

例如，假設 Northwind Traders 建立了 CRM 系統，並從其網站提供用戶端驅動程式作為可下載的 MSI。 而獨立開發人員 Nancy，想要更輕鬆地使用 Northwind 的用戶端程式庫，並將它轉換成 NuGet 套件，稱之為 `NorthwindTraders.Client`。 在此之後，Northwind 想要產生自己的用戶端程式庫官方 NuGet 套件，因此就 Nancy 對套件名稱的擁有權發生爭議。

在此案例中，Nancy 似乎並無惡意，甚至貢獻了自己的時間和程式碼為 Northwind 的工具和客戶提供支援。 與此同時，Northwind 是 Northwind 名稱的合法擁有者。

藉由遵循下列程序，Northwind 和 Nancy 可以協調出適當的解決方式，因為雙方都有意服務開發人員社群。 NuGet 小組一般沒有必要介入，因為共同作業通常會運作出最佳方案。

## <a name="process"></a>Process

1. 使用套件詳細資料頁面上的 [連絡擁有者]  連結，連絡有爭端的套件擁有者。 以和善、適當的口吻說明您的問題。
2. 將您的訊息副本傳送給， [support@nuget.org](mailto:support@nuget.org) 讓 NuGet 和 .Net Foundation 知道您的爭議。
3. 請等候最多30天的解析度，然後再次通知 [support@nuget.org](mailto:support@nuget.org) 。 nuget.org 支援小組會介入，嘗試解決雙方爭議。
