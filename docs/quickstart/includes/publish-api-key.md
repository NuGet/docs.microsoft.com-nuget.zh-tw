---
ms.openlocfilehash: 5acdc54726e4cb07794f8ee07d5e0d357ff622a3
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842039"
---
1. [登入 nuget.org 帳戶](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) \(英文\)，或者，如果您還沒有帳戶，則建立一個帳戶。

1. 選取您的使用者名稱 (在右上方)，然後選取 [API 金鑰]  。

1. 選取 [建立]  ，提供金鑰的名稱，選取 [選取範圍] > [推送]  。 針對 [Glob 模式]  輸入 *，然後選取 [建立]  。 (如需範圍的詳細資訊，請參閱下方)。

1. 建立金鑰之後，選取 [複製]  以擷取 CLI 中您需要的存取金鑰：

    ![將 API 金鑰複製到剪貼簿](../media/QS_Create-02-APIKey.png)

1. **重要**：將您的金鑰儲存在安全的位置，因為您稍後就無法再次複製此金鑰。 如果您返回 API 金鑰頁面，則需要重新產生金鑰才能加以複製。 如果您不再想要透過 CLI 推送套件，也可以移除 API 金鑰。

設定範圍可讓您針對不同用途建立個別的 API 金鑰。 每個金鑰都有其到期的時間範圍，且可將範圍設定為特定套件 (或 Glob 模式)。 每個金鑰也可將範圍設定為特定作業：新套件和更新的推送、僅更新的推送，或取消列入。 透過設定範圍，您就可針對組織中管理套件的不同人員建立 API 金鑰，讓他們只具有所需的權限。 如需詳細資訊，請參閱[具範圍的 API 金鑰簡介](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) \(英文\) (blogs.nuget.org)。