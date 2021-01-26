---
title: 刪除 nuget.org 中的 NuGet 套件
description: 取消列出 nuget.org 中套件的原則。除非套件違反其他原則，否則不支援永久刪除。
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: e5c62177b40162cb8b6b37b0d272fb7a945156c1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775710"
---
# <a name="deleting-packages"></a>刪除套件

nuget.org 不支援永久刪除套件。 這樣會中斷依賴套件可用性的每個專案，尤其是使用包含套件還原的建置工作流程。

nuget.org 支援 [取消列出封裝](#unlisting-a-package)，您可以在網站上的 [封裝管理] 頁面中進行。 未列出的套件不會出現在 nuget.org 或 Visual Studio UI 中，也不會出現在搜尋結果中。 不過，使用支援套件還原的確切版本號碼仍可以下載及安裝未列出的套件。 此外，下列特定案例仍會探索到未列出的套件：

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

如果您發現有套件違反其中任一項目，請按一下套件詳細資料頁面上的 [檢舉不當使用]  連結並提交報告。

請注意，NuGet 小組和 .NET Foundation 保留隨時變更這些準則的權利。

## <a name="unlisting-a-package"></a>取消列出套件
取消列出套件版本會將它從 [搜尋] 和 [nuget.org 封裝詳細資料] 頁面中隱藏。 這可讓套件的現有使用者繼續使用，但會減少新的採用，因為搜尋中看不到套件。

取消列出套件的步驟：

1. 選取 `Your account name` 右上角的 () >`Manage packages` > `Published packages`
1. 選取 [管理封裝] 圖示
1. 展開 [清單] 區段，然後選取套件版本
1. 取消核取 [在搜尋結果中列出]，然後選取 [儲存]

特定套件版本現在已未列出。 若要確認這一點，請登出您的帳戶，並流覽至 [套件] 頁面 (沒有版本的元件) 例如： https://www.nuget.org/packages/YOUR-PACKAGE-NAME/ 。 您將會看到該套件的所有 **版本尚未列出** 。 不過，當套件擁有者登入時，可以看到所有版本及其清單狀態。

您也可以取代套件版本 (，以防無法刪除) 的套件版本。 如需淘汰套件版本的詳細資訊，請參閱 [淘汰套件](../deprecate-packages.md)。
