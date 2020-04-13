---
title: 刪除 nuget.org 中的 NuGet 套件
description: 取消列出 nuget.org 中套件的原則。除非套件違反其他原則，否則不支援永久刪除。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3abe809d76e75801c2f936aba129d27ba7b64913
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "80581271"
---
# <a name="deleting-packages"></a>刪除套件

nuget.org 不支援永久刪除套件。 這樣會中斷依賴套件可用性的每個專案，尤其是使用包含套件還原的建置工作流程。

nuget.org支援[取消列出包](#unlisting-a-package),可以在網站上的包管理頁中完成。 未列出的套件不會出現在 nuget.org 或 Visual Studio UI 中，也不會出現在搜尋結果中。 不過，使用支援套件還原的確切版本號碼仍可以下載及安裝未列出的套件。 此外，下列特定案例仍會探索到未列出的套件：

- 使用浮點版本的套件還原 (例如，`1.0.0-*`)，如果最新的可用套件符合版本或相依性條件約束是未列出的套件。
- 透過目錄複寫套件 (因為目錄也包含未列出的套件)。

## <a name="exceptions"></a>例外狀況

在發生著作權侵權和有潛在危險內容等例外情況下，NuGet 小組可以手動刪除套件。 您可使用 NuGet.org 套件詳細資料頁面上的 [檢舉不當使用] 按鈕來回報套件。 若您為套件擁有者，請登入 NuGet.org 帳戶，使用 NuGet.org 套件詳細資料頁面上的 [連絡支援人員] 按鈕來尋求 NuGet 的支援。

## <a name="prohibited-use"></a>禁止使用

所有符合下列準則的套件概不允許出現在公用 NuGet 資源庫中，且沒有商量餘地立即移除。 但會通知套件擁有者移除相關事項。

- 包含惡意程式碼、廣告軟體或任何種類的間諜軟體。
- 旨在傷害開發人員工作站或其組織。
- 侵害著作權或違反授權。
- 包含不法內容。
- 旨在佔用套件識別碼，包括具有零生產力內容的套件。 套件必須包含程式碼，否則擁有者必須將識別碼讓實際上有產品要出貨的人。
- 嘗試讓資源庫進行未明確設計其執行的作業。

如果您發現有套件違反其中任一項目，請按一下套件詳細資料頁面上的 [檢舉不當使用]**** 連結並提交報告。

請注意，NuGet 小組和 .NET Foundation 保留隨時變更這些準則的權利。

## <a name="unlisting-a-package"></a>取消列出套件
取消列出包版本會將其隱藏在搜索和nuget.org包詳細資訊頁中。 這允許包的現有使用者繼續使用它,但減少了新的採用,因為包在搜索中不可見。

取消列出套件清單的步驟:

1. 選擇`Your account name`(右上角)>`Manage packages` > `Published packages`
1. 選擇「管理包」圖示
1. 展開「清單」部分並選擇套件版本
1. 取消選取中的"搜尋結果中的清單"並選擇"保存"

特定包版本現已未列出。 為了驗證這一點,登出您的帳號並瀏覽到套件頁(沒有版本元件),例如: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/。 您將看到該包的所有版本**尚未**列出。 但是,包擁有者在登錄時可以看到所有版本及其列表狀態。

也可以棄用套件版本(如果無法刪除包版本)。 有關棄用套件版本的詳細資訊,請參閱[棄用包](../deprecate-packages.md)。
