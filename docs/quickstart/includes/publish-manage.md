---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496002"
---
從nuget.org上的個人資料中,選擇 **「管理包」** 以查看剛剛發佈的包。 您也會收到確認電子郵件。 請注意，可能需要一些時間才會編製套件的索引，並顯示在其他人可以找到它的搜尋結果中。 在這段期間，套件頁面會顯示下列訊息：

![此套件尚未編製索引。 編製索引完成後，它會出現在搜尋結果中，並且可供安裝/還原。](../media/QS_Create-03-NotIndexed.png)

就這麼簡單！ 您剛剛已將第一個 NuGet 套件發行至 nuget.org，其他開發人員可以在他們自己的專案中使用它。

如果您在本逐步解說中建立的套件不是真的很實用 (例如，使用空類別庫建立的套件)，則您應該「取消列出」** 該套件，以便在搜尋結果中加以隱藏：

1. 在 nuget.org，選取您的使用者名稱 (頁面右上方)，然後選取 [管理套件]****。

1. 在 [已發行]**** 下方找出您想要取消列出的套件，然後選取右邊的資源回收筒圖示：

    ![針對 nuget.org 上列出之套件顯示的資源回收筒圖示](../media/qs_create-vs-03-trash-can.png)

1. 在後續頁面上，清除標籤為 [在搜尋結果中列出 (package-name)]**** 的方塊，然後選取 [儲存]****：

    ![針對 nuget.org 上的套件清除 [列出] 核取方塊](../media/qs_create-vs-04-unlist.png)