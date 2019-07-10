---
title: NuGet.org 常見問題集
description: 使用 NuGet 資源庫的常見問與答。
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: c2fc11c0f5dd5d98c40c8b97f9d5a72c4a334b79
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427283"
---
# <a name="nugetorg-frequently-asked-questions"></a>NuGet.org 常見問題集

## <a name="license-terms"></a>授權條款

**如果套件未提供特定授權資訊，則預設授權條款是什麼？**

每個套件都是受套件隨附的條款所控管。 您應該先檢閱適用的條款，再存取、下載或取得任何套件。 在 nuget.org 上，使用套件頁面上的 [授權資訊]  連結。

如果套件未指定授權條款，請使用 nuget.org 套件頁面上的 [連絡擁有者]  連結直接連絡套件擁有者。 Microsoft 不會將任何智慧財產權從協力廠商套件提供者授權給您，而且不負責協力廠商所提供的資訊。

## <a name="managing-packages-on-nugetorg"></a>在 Nuget.org 上管理套件

**我可以在上傳套件之後編輯套件中繼資料嗎？**

NuGet 建議簽署所有套件。 套件簽署的設計原則是已簽署的套件內容必須是不可變的，其中包含 nuspec。 編輯套件中繼資料會導致 nuspec 變更，並讓現有簽章失效。 建議修改現有工作流程，使其不需要在建立套件之後編輯套件中繼資料。

請注意，會自動從您套件本身產生針對套件所列出的相依性，而且無法進行編輯。

此外，將套件上傳至 [int.nugettest.org](https://int.nugettest.org) 是測試及驗證您套件的好方法，完全無須將套件設為可在公開資源庫中使用。 API 端點： https://apiint.nugettest.org/v3/index.json

**我可以刪除已經發行至 NuGet.org 的套件嗎？**

一般來說，我們不支援刪除已經發行到 NuGet.org 的套件。閱讀更多關於我們[刪除套件原則](policies/deleting-packages.md)的資訊。

**可以保留將在未來發行之套件的名稱嗎？**

可以。 要求帳戶的套件識別碼前置詞，即可在 [nuget.org](https://www.nuget.org/) 上保留套件的識別碼。 若要要求套件識別碼首碼，請遵循[文件](id-prefix-reservation.md)中的指示。

**如何宣告套件擁有權？**

請參閱[在 nuget.org 上管理套件擁有者](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)。

**如何處理違反我軟體授權的套件擁有者？**

鼓勵 NuGet 社群合作，以解決套件擁有者與其他軟體擁有者之間可能發生的任何爭議。 我們已製作可在要求 nuget.org 管理員仲裁之前遵循的[爭議解決程序](policies/dispute-resolution.md)。

**建議將測試套件上傳至 nuget.org 嗎？**

基於測試目的，您可以使用 [int.nugettest.org](https://int.nugettest.org) 或替代的公開 NuGet 伺服器，例如 [myget.org](https://myget.org) 或 [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/)。

請注意，上傳到 int.nugettest.org 的套件不會保留。

**我可以上傳至 nuget.org 的套件大小上限為何？**

nuget.org 允許最多 250MB 的套件，但建議盡可能保持 1MB 的套件，並使用相依性將套件連結在一起。 根據經驗法則，套件只包含一個組件來避免發生衝突。

NuGet 使用 HTTP 來下載套件，因此較大的套件與較小的套件相較之下更有可能會讓安裝失敗。

可能會在多個套件之間共用相依性，讓 NuGet 套件取用者的總下載大小變小。

相依性大部分是靜態的，而且永遠不會變更。 使用程式碼修正 Bug 時，可能不需要更新相依性。 如果您組合相依性，則每次最後都會得到較大的套件。 將 NuGet 套件分割為相關相依性，以更精細地調整您套件取用者的升級。

## <a name="nugetorg-not-accessible"></a>無法存取 nuget.org

**為何無法從 nuget.org 下載套件或將套件上傳至其中？**

首先，請確定您使用最新版的 NuGet。 如果該版本持續失敗，請[連絡支援人員](https://www.nuget.org/policies/Contact)，並提供其他連線疑難排解資訊，包含：

- 您所使用的 NuGet 版本
- 您所使用的套件來源
- 含詳細之詳細資訊的還原記錄
- MTR 或 Fiddler 追蹤 (請參閱下面)
- 您的地理區域
- 您的機器是否有 Proxy 或防火牆保護？
- 您的機器是否位於雲端提供者的資料中心 (Azure、AWS 等)？ 如果是的話，請提供提供者的名稱及區域。

*擷取 MTR：*

- 從 [http://winmtr.net/download/](http://winmtr.net/) 下載 WinMTR
- 輸入 `api.nuget.org` 作為主機名稱，然後按一下 [啟動]  。
- 等到 [已傳送]  資料行 >= 100。

    ![擷取 MTR](media/mtr.png)

- 將文字複製至剪貼簿。

*擷取 Fiddler：*

- 安裝最新版的 [Fiddler](http://www.telerik.com/download/fiddler)。
- 啟動 Fiddler，並使用 [檔案] > [擷取流量]  功能表來停用擷取流量。
- 移除所有工作階段 (選取清單中的所有項目，並按 **Delete** 鍵)。
- 設定 Fiddler 擷取 HTTPS 流量，方法是核取 [工具] > [Fiddler 選項]  功能表的 [HTTPS]  索引標籤中的 [Decrypt HTTPS traffic] (將 HTTPS 流量解密)  。
- 關閉 Visual Studio。
- 啟用 [檔案] > [擷取流量]  功能表。
- 啟動 Visual Studio 或 nuget.exe，然後執行無法運作的動作。 這些動作所產生的流量應該會顯示在 Fiddler 中。
- 執行動作之後，請使用 [檔案] > [儲存] > [所有工作階段]  來儲存所擷取的工作階段。

注意：可能必須將 `HTTP_PROXY` 環境變數設定為 `http://127.0.0.1:8888`，以透過 Fiddler 路由傳送 NuGet 流量。

如果該作業失敗，請嘗試[這篇 StackOverflow 文章所提及的祕訣](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)。

## <a name="nugetorg-account-management"></a>nuget.org 帳戶管理

### <a name="how-to-recover-nugetorg-password-login"></a>如何復原 nuget.org 密碼登入？

請注意，[nuget.org 密碼登入已中止](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html)，您只能使用個人 Microsoft 帳戶 (MSA) 或 Azure Active Directory (AAD) 帳戶登入 nuget.org。 不過，如果您無法存取建立關聯的 MSA/AAD 帳戶，就必須使用密碼登入來復原 nuget.org 帳戶。 在此情況下，請遵循下列步驟。
- **需求：** 對於您要復原密碼的帳戶，您必須能夠存取與該帳戶建立關聯的電子郵件。
- 前往[忘記密碼頁面](https://www.nuget.org/account/ForgotPassword)
- 輸入與您欲還原之 nuget.org 帳戶建立關聯的**電子郵件**地址。
- 按一下 [傳送]  按鈕。
- 您會收到寄給指定電子郵件地址帳戶，且附有重設密碼連結的電子郵件。 按一下此連結，然後設定新密碼。 若您找不到電子郵件，請檢查「垃圾郵件」資料夾。
- 完成後，您便可在 NuGet 上以使用者名稱/密碼登入。
- 若要以使用者名稱/密碼登入，請使用 [nuget.org 登入頁面](https://www.nuget.org/users/account/LogOn)上的**使用 Nuget.org 帳戶登入**連結。

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>哪一個 Microsoft 帳戶連結到我的 nuget.org 帳戶？

若您忘了哪一個 Microsoft 帳戶與您的 nuget.org 帳戶建立關聯，請遵循下列步驟以取得協助。
1. 前往 [nuget.org 登入頁面](https://www.nuget.org/users/account/LogOn)，然後按一下 **Need assistance signing in?** (需要登入上的協助嗎？) 連結。
1. 這將會顯示提供協助的快顯對話方塊。 遵循此對話方塊中的步驟，以了解與您 nuget.org 帳戶建立關聯的 Microsoft 帳戶。

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>如何變更我用來登入 nuget.org 的 Microsoft 帳戶？
若您想要為 nuget.org 使用者變更 Microsoft 帳戶，請遵循下列步驟。 假設您電子郵件為 `account1@outlook.com` 的 Microsoft 帳戶與使用者名稱為 `MyNuGetAccount` 的 nuget.org 帳戶建立關聯。 且您希望將登入帳戶變更成電子郵件為 `account2@outlook.com` 的另一個 Microsoft 帳戶
1. 請使用 **目前關聯的 Microsoft 帳戶**登入，也就是按一下 [使用 Microsoft 帳戶登入]  後，[登入頁面](https://www.nuget.org/users/account/LogOn)上的 `account1@outlook.com`。
1. 登入後，前往[帳戶設定](https://www.nuget.org/account)頁面。
1. 展開**登入帳戶**區段。 按一下 [變更帳戶]  按鈕。
1. 系統會將您重新導向至 Microsoft 登入頁面。 請使用您想要變更關聯的帳戶登入，亦即 `account2@outlook.com`。**注意**：您可能需要在登入流程期間按一下 [Sign out and sign in with different account]  \(登出並以其它帳戶登入\)，才能使用其他 Microsoft 帳戶登入。
1. 若您看到以下錯誤訊息，請參閱 [Microsoft 帳戶已與另一個 nuget.org 帳戶連結](#microsoft-account-is-linked-with-another-nugetorg-account)，以取得詳細資訊。
    >_Failed to update the Microsoft account with 'account2 <account2@outlook.com>'.This could happen if it is already linked to another NuGet account.Contact support for more information. (無法更新擁有 'account2 account2@outlook.com' 的 Microsoft 帳戶。若此帳戶已連結到另一個 NuGet 帳戶，就可能發生此情形。請連絡支援人員以取得詳細資訊。)_

1. 使用第二個帳戶成功登入後，系統會將您重新導向回 nuget.org 帳戶設定頁面，您現在應該會看到新的 Microsoft 帳戶已作為登入帳戶建立關聯。 接下來您應在登入 nuget.org 時，使用此帳戶。

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Microsoft 帳戶已與另一個 nuget.org 帳戶連結。

若您嘗試變更 Microsoft 登入，並看到以下錯誤訊息：
> _Failed to update the Microsoft account with 'account2 <account2@outlook.com>'.This could happen if it is already linked to another NuGet account.Contact support for more information. (無法更新擁有 'account2 account2@outlook.com' 的 Microsoft 帳戶。若此帳戶已連結到另一個 NuGet 帳戶，就可能發生此情形。請連絡支援人員以取得詳細資訊。)_

假設您嘗試將 Microsoft 帳戶登入從使用者名稱為 `MyNuGetAccount1` 之 nuget.org 使用者的 `account1@outlook.com` 變更為電子郵件為 `account2@outlook.com` 的另一個 Microsoft 帳戶。 然後看到以上錯誤訊息。

**以上錯誤訊息代表什麼意思？**

這代表有與 Microsoft 帳戶建立關聯的另一個 nuget.org 帳戶，且您嘗試將其變更為以上範例中，電子郵件為 `<account2@outlook.com>` 且與另一個 nuget.org 帳戶 (使用者名稱為 `MyNuGetAccount2`) 建立關聯的 Microsoft 帳戶。

您無法使用連結到其他 nuget.org 帳戶的 Microsoft 帳戶，變更關聯的登入。

**我忘了我有另一個的 nuget.org 帳戶，我要如何找出哪一個是我的 nuget.org 帳戶？**

在[登入頁面](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "登入頁面")上以第二個 Microsoft 帳戶登入。 這會將您登入至目前與第二個 Microsoft 帳戶建立關聯的 nuget.org 帳戶。 您接著可以檢視此帳戶上的已更新套件，及進行帳戶管理。

**我不在乎第二個 nuget.org 帳戶，且想要使用第二個 Microsoft 帳戶變更第一個 nuget.org 帳戶的登入。該怎麼做？**

如果您不在乎第二個 nuget.org 帳戶，但仍想使用電子郵件為 `account2@outlook.com` 的關聯 Microsoft 帳戶。 

您可以透過刪除 nuget.org 帳戶，解除 Microsoft 帳戶與 nuget.org 帳戶間的關聯。
1. 請遵循這些步驟，以[刪除第二個 nuget.org 帳戶 `MyNuGetAccount2` 的使用者](#how-to-delete-my-nugetorg-account)。 
1. 刪除此帳戶後，即可重試這些步驟來[變更 Microsoft 帳戶登入](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login)。

**等一下，我也需要這第二個帳戶。我不想要失去此帳戶，但要變更第一個帳戶的關聯帳戶登入。**

您必須建立/使用第三個 Microsoft 帳戶，也就是電子郵件為 `account3@outlook.com` 的帳戶。 
1. 首先，您應使用第二個 Microsoft 帳戶 (nuget.org 上的 `account2@outlook.com`) 登入。遵循上述步驟來變更關聯的登入，並將第三個 Microsoft 帳戶與此 nuget.org 帳戶建立關聯。
1. 完成後，電子郵件為 `account2@outlook.com` 的第二個 Microsoft 帳戶就可以與第一個 nuget.org 帳戶 `MyNuGetAccount1` 建立關聯。 遵循上述相同步驟，以將 Microsoft 登入變更為第二個 Microsoft 帳戶。

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>使用 Microsoft 帳戶登入，但顯示我的電子郵件已連結到另一個 Microsoft 帳戶

若您嘗試使用 Microsoft 帳戶，也就是電子郵件 `account1@outlook.com` 登入，且看到以下錯誤訊息：
> _The account with email 'account1@outlook.com' is linked with another microsoft account._
>
> _If you would like to update the linked Microsoft account you can do so from the account settings page. (電子郵件為 'account1@outlook.com' 的帳戶已與另一個 Microsoft 帳戶連結。若您想要更新已連結的 Microsoft 帳戶，可以從帳戶設定頁面執行此動作。)_

**以上錯誤訊息代表什麼意思？**

在 nuget.org 建立帳戶時，通訊電子郵件地址會與該帳戶建立關聯。 這通常與關聯 Microsoft 帳戶使用的電子郵件地址相同。 不過，您可以選擇指定其他電子郵件地址進行通訊。 所以，技術上來說，您可以擁有其他 Microsoft 帳戶 (亦即 `account2@outlook.com`)，且連結到通訊電子郵件地址為 `account1@outlook.com` 的 nuget.org 帳戶。

因此，上方的錯誤訊息代表已經有通訊電子郵件地址為 `account1@outlook.com` 的現有 nuget.org 帳戶，但卻與電子郵件**不是** `account1@outlook.com` 的另一個 Microsoft 帳戶建立關聯。

**如何找出哪一個 Microsoft 帳戶連結到此 nuget.org 帳戶？**

您應使用[登入協助](#which-microsoft-account-is-linked-to-my-nugetorg-account)流程，找出哪一個 Microsoft 帳戶連結到電子郵件地址為 `account1@outlook.com` 的 nuget.org 帳戶。

**我想要使用我的 Microsoft 帳戶覆寫該帳戶**

請遵循[無法使用 Microsoft 登入，如何復原我的 nuget.org 帳戶](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)一節所述的步驟，將 Microsoft 帳戶與現有的 nuget.org 帳戶建立關聯。

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>無法使用 Microsoft 登入，如何復原我的 nuget.org 帳戶？

若您已嘗試使用[登入協助](#which-microsoft-account-is-linked-to-my-nugetorg-account)，且沒有與 nuget.org 帳戶建立關聯之 Microsoft 帳戶的存取權，請遵循下列步驟，以將新的 Microsoft 帳戶連結到 nuget.org 帳戶。
1. **需求**:您需要未與任何現有 nuget.org 帳戶建立關聯之 Microsoft 帳戶的存取權。 如果沒有的話，您可以[建立](https://signup.live.com)帳戶。
2. 如果您忘記 nuget.org 帳戶的使用者名稱及密碼，請遵循[復原密碼登入的步驟](#how-to-recover-nugetorg-password-login)。
3. 以使用者名稱/密碼登入，[登入 nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount)。
4. 登入後，就會顯示出快顯對話方塊，如下所示。 此為密碼中止對話方塊。
5. **注意**：請忽略使用特定 Microsoft 帳戶登入的指示。 您現可將 nuget.org 帳戶連結到任何其他 Microsoft 登入。
6. 按一下 [使用 Microsoft 帳戶登入]  按鈕，然後使用您擁有其存取權的 Microsoft 帳戶登入，如步驟 1 所述。
7. 您的帳戶現在會連結到新的 Microsoft 帳戶，且往後可以將其用來登入 nuget.org。

    ![連結 MSA 對話方塊](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>如何將我的 nuget.org 帳戶轉換為組織？

若您想要將帳戶轉換為組織，且此帳戶已經與 Microsoft 帳戶登入建立關聯，那麼請遵循 [organizations on nuget org](organizations-on-nuget-org.md) (nuget org 上的組織) 一文中所提供的步驟。

不過，若您的 nuget.org 帳戶未與 Microsoft 帳戶建立關聯/連結，則可以遵循以下步驟將此帳戶轉換為組織。
1. **需求**:您必須先在 nuget.org 上建立個別帳戶，以作為組織帳戶上的系統管理員使用。 如果沒有的話，請[建立新的 nuget.org 帳戶](individual-accounts.md)
2. 若您沒有可供使用的密碼登入，請遵循為 nuget.org 帳戶[復原密碼登入的步驟](#how-to-recover-nugetorg-password-login)，如果有的話，略過此步驟。
3. 以使用者名稱/密碼登入，[登入 nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount)。
4. 登入後，就會顯示出快顯對話方塊，如下所示。 此為密碼中止對話方塊。 
    > [!Important]
    > 忽略此對話方塊，**請勿**按一下 [使用Microsoft 帳戶登入]  按鈕。

5. 移至 [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform)。 這會使您無須連結到 Microsoft 帳戶，就能夠將 nuget.org 帳戶轉換為組織。
6. 為您的個人 nuget.org 帳戶/在步驟 1 建立的帳戶，指定系統管理員使用者名稱。
7. 請遵循指示以完成將此帳戶轉換為組織。

    ![連結 MSA 對話方塊](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>具有非受控租用戶之 AAD 帳戶的 nuget.org 登入問題？

若您使用電子郵件帳戶網域 (@yourdomain.com) 在登入流程中看到以下錯誤訊息，請參閱下列步驟來復原 nuget.org 帳戶。

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**這項登入期間的非受控狀態是什麼？為什麼現在會發生這個問題？** 

看來您的帳戶之前註冊為個人 Microsoft 帳戶，且沒發生什麼問題，不過現在您的帳戶似乎已註冊為 Azure Active Directory (用來驗證 Microsoft 帳戶的識別服務) 中的「非受控」租用戶。 

若您或組織中的某人 (電子郵件地址為 @yourdomain.com) 使用其中一項 AAD 整合服務註冊，或進行會為所使用 Microsoft 帳戶網域 (也就是 @yourdomain.com) 建立這類「非受控」租用戶的 [Azure Active Directory 自助式註冊](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup)，就可能發生此情形。 

**該如何復原我的帳戶？**

因為此帳戶在 Azure Active directory 中具有這類「非受控」租用戶帳戶，所以目前我們 (nuget.org) 無法予以驗證。 我們正在尋找更好的方法來驗證這類帳戶。

若您想要使用 Microsoft 帳戶 (@yourdomain.com) 登入 nuget.org，您 (或公司的系統管理員) 就必須使用電子郵件地址 "@yourdomain.com" 進行 DNS 驗證來驗證使用者，以宣告 AAD 的擁有權。 請遵循由 Azure Active Directory 所記載[網域系統管理員接管](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover)的步驟。 完成後，您的一般登入應開始正常運作。

**我不想要執行這些動作，可以復原我帳戶的其他方式為何？**

您可以[建立](https://www.microsoft.com/en-us/account)新的 Microsoft 帳戶 (搭配**未**與 @yourdomain.com 建立關聯的電子郵件) 遵循[復原您的 nuget.org 帳戶](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)一節中提供的步驟。

### <a name="how-do-i-change-my-nugetorg-account-username"></a>如何變更我的 nuget.org 帳戶使用者名稱？

您不能進行變更。 因為原則的關係，我們目前不允許變更使用者名稱。 唯一變更使用者名稱的方式為，以想要的使用者名稱建立新帳戶。 建議您在建立新帳戶之前，先將現有的帳戶刪除，否則您將無法重複使用註冊的 Microsoft 帳戶。
> [!Important]
> 刪除使用者仍會**保留** `username`。 您將無法再重複使用相同的使用者名稱，**這也包含大小寫的變更**。 例如，若您建立了使用者名稱為 `mycoolname` 的使用者，且想要將其變更為 `MyCoolName` (大小寫變更)，則在刪除使用者後，就不可能達成目的。

請遵循[刪除 nuget.org 帳戶](#how-to-delete-my-nugetorg-account)一節中提供的步驟，並以正確的使用者名稱[註冊新帳戶](individual-accounts.md)。

### <a name="how-to-delete-my-nugetorg-account"></a>如何刪除我的 nuget.org 帳戶？

請注意，若要刪除您的帳戶，建議轉換您為唯一擁有者的所有套件擁有權。 您可以深入了解如何[管理套件擁有者](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg)。 這也有助於我們加速處理您的要求。

> [!Important]
> 刪除使用者會導致以下情形：
>  1. 撤銷關聯的 API 金鑰。 
>  2. 移除帳戶在所有子套件上的擁有者身分。
>  3. 解除所有先前既存識別碼前置詞保留與此帳戶的關聯。
>  4. 移除帳戶在所有組織的成員身分。
>  5. 您的使用者名稱將會保留，且只有擁有我們的權限才能予以重複使用。

請遵循下列步驟以繼續刪除帳戶。
1. 使用您想要刪除的帳戶[登入 nuget.org](https://www.nuget.org/users/account/LogOn)。
2. 按一下此 URL：[https://www.nuget.org/account/delete](https://www.nuget.org/account/delete)，然後遵循這些步驟，以提交刪除帳戶的要求。

我們的客戶支援會處理此要求，並將帳戶刪除。
