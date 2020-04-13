---
title: 個人帳戶 - NuGet.org
description: 必須要有 NuGet.org 上的個人帳戶才能發佈套件
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429014"
---
# <a name="individual-accounts-on-nugetorg"></a>NuGet.org 上的個人帳戶

您必須建立個人帳戶，才能在 NuGet.org 上發佈和管理套件。

## <a name="individual-accounts-vs-organization-accounts"></a>個人帳戶與組織帳戶

個人 (使用者) 帳戶是您在 NuGet.org 上的身分識別，且可以是任意數目組織的成員。 套件可以屬於組織帳戶，就像可以屬於個人帳戶一樣。 套件取用者看不到個別帳戶和組織帳戶之間的差異：兩者皆以套件 `owners` 形式出現。

組織帳戶有一或多個作為其成員的個人帳戶。 這些成員可以管理一組套件，同時維持擁有權的單一身分識別。

## <a name="add-a-new-individual-account"></a>新增新的個人帳戶

您必須擁有個人 Microsoft 帳戶或 Azure Active Directory (AAD) 帳戶才能建立 NuGet.org 帳戶。 如果沒有的話，您可以[建立](https://signup.live.com)帳戶。 如果您擁有 MSA 或 AAD 帳戶，請遵循下列步驟。

1. 跳到[NuGet.org 登入頁面](https://www.nuget.org/users/account/LogOn)。

1. 按一下 [使用 Microsoft 帳戶登入]**** 按鈕。

1. 輸入您的 Microsoft 帳戶或 Azure Active Directory 帳戶詳細資料。

1. 請按一下 [是]**** 接受要提供給 *NuGet.org* 申請的權限。

   ![將權限授與 NuGet.org](media/nuget-org-permissions.png)

1. 您將被重定向到*nuget.org*,並要求註冊使用者名。

1. 在輸入方塊中指定使用者名稱。 請注意，使用者名稱**會**區分大小寫，且往後無法再變更或重新命名。

   ![在 NuGet.org 上指定使用者名稱](media/nuget-org-register.png) 

1. 按下 **「註冊」** 按鈕。

您現在擁有 NuGet.org 帳戶。 您可以在[帳戶設定](https://www.nuget.org/account)頁面上進行帳戶管理。

## <a name="enable-two-factor-authentication-2fa"></a>使用雙重要素驗證 (2FA)

雙重身份驗證(2FA)是登錄網站或應用時使用的額外安全層。 使用 2FA,您必須使用 Microsoft 帳戶 (MSA) 登錄並提供只有您知道或有權訪問的另一種形式的身份驗證。 若要更有效地保護您的帳戶，請啟用雙重要素驗證 (建議)。

1. 登入您的帳戶後，開啟您的設定檔，然後選擇 [登入帳戶]**** 下的 [啟用]****。

   ![啟用 2FA](media/nuget-org-register-2fa.png)

   您會看到一則訊息，告訴您下一次登入 *nuget.org* 時，系統會要求您提供額外的認證。

2. 若要立即完成驗證，請先登出，然後再重新登入一次。

3. 當您登入時，請選擇簡訊或電子郵件做為第二種形式的驗證。

   確認已與 Microsoft 帳戶相關聯的電話號碼或電子郵件。 您可能需要為您的帳戶輸入新的電話號碼或電子郵件。 如果是這樣，請依照指示輸入必要資訊，然後按一下 [下一步]****。

   ![啟用 2FA](media/nuget-org-sign-in-2fa.png)

4. 檢查您的裝置或電子郵件帳戶，然後輸入我們剛傳送給您的代碼。

   ![啟用 2FA](media/nuget-org-enter-code-2fa.png)

5. 請遵循任何其他指示來完成雙重要素驗證。

> [!Tip]
> 為NuGet.org帳戶啟用 2FA 不會影響可能連結到您用於登入NuGet.org的Microsoft帳戶的其他帳戶或服務的身份驗證設置。

## <a name="delete-a-nugetorg-account"></a>刪除 NuGet.org 帳戶

如需其他帳戶相關工作 (例如刪除 NuGet.org 帳戶) 的說明，請參閱 [NuGet.org 帳戶管理](nuget-org-faq.md#nugetorg-account-management)。
