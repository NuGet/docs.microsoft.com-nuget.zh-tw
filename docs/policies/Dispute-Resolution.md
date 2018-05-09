---
title: NuGet 套件名稱爭議解決方案
description: 解決 NuGet 套件發行者之間有關品牌、商標和其他衝突情況爭議的程序。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 39fe993d73f11ca4b83ae07b1e8b93ae0682d519
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a>解決 NuGet 套件名稱的爭議

本文提供解決社群成員與其他 NuGet 發行者發生爭議的建議解決方法流程。

例如，假設 Northwind Traders 建立了 CRM 系統，並從其網站提供用戶端驅動程式作為可下載的 MSI。 而獨立開發人員 Nancy，想要更輕鬆地使用 Northwind 的用戶端程式庫，並將它轉換成 NuGet 套件，稱之為 `NorthwindTraders.Client`。 在此之後，Northwind 想要產生自己的用戶端程式庫官方 NuGet 套件，因此就 Nancy 對套件名稱的擁有權發生爭議。

在此案例中，Nancy 似乎並無惡意，甚至貢獻了自己的時間和程式碼為 Northwind 的工具和客戶提供支援。 與此同時，Northwind 是 Northwind 名稱的合法擁有者。

藉由遵循下列程序，Northwind 和 Nancy 可以協調出適當的解決方式，因為雙方都有意服務開發人員社群。 NuGet 小組一般沒有必要介入，因為共同作業通常會運作出最佳方案。 事實上，至今為止，每件引起 NuGet 小組注意的爭議皆不必小組介入公評即已圓滿解決。

## <a name="process"></a>處理序

1. 使用套件詳細資料頁面的**連絡擁有者**連結，連絡與您發生爭議的套件擁有者。 客氣地直接說明您的問題。
2. 將您的郵件副本傳送至 [support@nuget.org](mailto:support@nuget.org)，以便 NuGet 和 .NET Foundation 了解您的爭議。
3. 解決方法的等候期最多 30 天，屆時請再次通知 [support@nuget.org](mailto:support@nuget.org)。 nuget.org 支援小組會介入，嘗試解決雙方爭議。
