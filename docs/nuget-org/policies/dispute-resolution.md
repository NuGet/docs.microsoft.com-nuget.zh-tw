---
title: NuGet 套件名稱爭議解決方案
description: 解決 NuGet 套件發行者之間有關品牌、商標和其他衝突情況爭議的程序。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: a2f1fed578f1635296892ab925219f0f27883c02
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "67426933"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>解決 NuGet 套件名稱的爭議

本文提供解決社群成員與其他 NuGet 發行者發生爭議的建議解決方法流程。

例如，假設 Northwind Traders 建立了 CRM 系統，並從其網站提供用戶端驅動程式作為可下載的 MSI。 而獨立開發人員 Nancy，想要更輕鬆地使用 Northwind 的用戶端程式庫，並將它轉換成 NuGet 套件，稱之為 `NorthwindTraders.Client`。 在此之後，Northwind 想要產生自己的用戶端程式庫官方 NuGet 套件，因此就 Nancy 對套件名稱的擁有權發生爭議。

在此案例中，Nancy 似乎並無惡意，甚至貢獻了自己的時間和程式碼為 Northwind 的工具和客戶提供支援。 與此同時，Northwind 是 Northwind 名稱的合法擁有者。

藉由遵循下列程序，Northwind 和 Nancy 可以協調出適當的解決方式，因為雙方都有意服務開發人員社群。 NuGet 小組一般沒有必要介入，因為共同作業通常會運作出最佳方案。 事實上，至今為止，每件引起 NuGet 小組注意的爭議皆不必小組介入公評即已圓滿解決。

## <a name="process"></a>Process

1. 使用套件詳細資料頁面上的 [連絡擁有者]**** 連結，連絡有爭端的套件擁有者。 以和善、適當的口吻說明您的問題。
2. 傳送您的郵件複本[support@nuget.org](mailto:support@nuget.org), 以便 NuGet 和 .NET 基金會瞭解您的爭議。
3. 最多等待 30 天以尋求解決方案,[support@nuget.org](mailto:support@nuget.org)然後再次通知。 nuget.org 支援小組會介入，嘗試解決雙方爭議。
