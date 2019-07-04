---
title: 使用者資料要求
description: 要求使用者資料匯出和刪除的原則
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426983"
---
# <a name="user-data-requests"></a>使用者資料要求

nuget.org 使用者可以透過 [nuget.org](https://www.nuget.org) 送出資訊刪除要求和資訊匯出要求。這兩種類型都會以支援要求形式送出，並由 nuget.org 系統管理員在 30 天內執行。

下列使用者資料可直接透過 nuget.org 存取：

* 帳戶相關資料，例如電子郵件地址、登入帳戶、個人資料圖片和電子郵件通知設定
* 擁有的 API 金鑰
* 擁有的套件清單

透過支援要求匯出的資料中不包含這項資料。

## <a name="identifying-customer-data"></a>識別客戶資料

客戶資料可識別為 nuget.org 使用者帳戶名稱。

## <a name="deleting-customer-data"></a>刪除客戶資料

若要要求從 nuget.org 刪除使用者資料：

1. 使用者必須登入 [nuget.org](https://www.nuget.org)
1. 使用者必須送出要刪除其帳戶的要求 [nuget.org/account/delete](https://www.nuget.org/account/delete)

建議唯一擁有套件的使用者先尋找新的擁有者，再要求刪除其帳戶。 如果未轉移套件擁有權，NuGet 套件不會列出，如此一來，就無法再用於 Visual Studio 中或 nuget.org 網站上的搜尋查詢。 刪除帳戶之前，nuget.org 系統管理員會與使用者合作，尋找使用者所擁有之套件的新擁有者。

nuget.org 系統管理員會在要求日期起的 30 天內完成帳戶刪除動作。

刪除帳戶時，會從 nuget.org 系統移除使用者的所有資料，並執行下列動作：

* 與 nuget.org 取消註冊已刪除的帳戶
* 刪除所有擁有的 API 金鑰
* 釋放所有保留的命名空間
* 移除任何套件擁有權

「不會」  刪除擁有的套件。 雖然這些套件未列於搜尋結果中，但透過套件還原，還是可供相依於這些套件的專案使用。

## <a name="exporting-customer-data"></a>匯出客戶資料

登入 nuget.org 之後，使用者可以透過 [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact) 送出匯出要求

使用者可以在 48 小時內透過 Azure Blob 下載匯出的資料。 48 小時後，存取會過期，而使用者必須視需求送出新的匯出要求。

匯出的資料包括：

* 使用者的支援要求
* 保存在稽核記錄中的使用者動作 (發佈套件、建立帳戶)
* 保存在 IIS 記錄中的任何使用者資訊
