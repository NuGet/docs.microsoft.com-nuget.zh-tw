---
title: 個人帳戶
description: 必須要有 NuGet.org 上的個人帳戶才能發佈套件
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427133"
---
# <a name="individual-accounts"></a>個人帳戶

您必須建立個人帳戶，才能在 NuGet.org 上發佈和管理套件。

## <a name="individual-accounts-vs-organization-accounts"></a>個人帳戶與組織帳戶

個人 (使用者) 帳戶是您在 NuGet.org 上的身分識別，且可以是任意數目組織的成員。 套件可以屬於組織帳戶，如同其可屬於個別帳戶。 套件取用者看不到個人帳戶和組織帳戶之間的差異：兩者皆以套件 `owners` 形式出現。

組織帳戶有一或多個作為其成員的個人帳戶。 這些成員可以管理一組套件，同時維持擁有權的單一身分識別。

## <a name="add-a-new-individual-account"></a>新增新的個人帳戶

您必須擁有個人 Microsoft 帳戶或 Azure Active Directory (AAD) 帳戶才能建立 NuGet.org 帳戶。 如果沒有的話，您可以[建立](https://signup.live.com)帳戶。 如果您擁有 MSA 或 AAD 帳戶，請遵循下列步驟。

1. 前往 [uGet.org 登入頁面](https://www.nuget.org/users/account/LogOn)。

1. 按一下 [使用 Microsoft 帳戶登入]  按鈕。

1. 輸入您的 Microsoft 帳戶或 Azure Active Directory 帳戶詳細資料。

1. 請按一下 [是]  接受要提供給 *NuGet.org* 申請的權限。

   ![將權限授與 NuGet.org](media/nuget-org-permissions.png)

1. 系統會將您重新導向至 *nuget.org*，並向您要求註冊使用者名稱。

1. 在輸入方塊中指定使用者名稱。 請注意，使用者名稱**會**區分大小寫，且往後無法再變更或重新命名。

   ![在 NuGet.org 上指定使用者名稱](media/nuget-org-register.png) 

1. 按一下 [註冊]  按鈕。

您現在擁有 NuGet.org 帳戶。 您可以在[帳戶設定](https://www.nuget.org/account)頁面上進行帳戶管理。
