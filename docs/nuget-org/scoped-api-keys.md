---
title: 限定範圍的 API 金鑰
description: 控制您用來推送套件的 API 金鑰
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: a3d2504528249f3545e2eb5d9bce7713029638db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901586"
---
# <a name="scoped-api-keys"></a>限定範圍的 API 金鑰

若要讓 NuGet 成為更安全的套件發佈環境，您可以透過新增範圍來控制 API 金鑰。

提供 API 金鑰範圍的能力可讓您更好控制 API。 您可以：

- 建立多個限定範圍的 API 金鑰，以用於不同套件配合不同的到期時間範圍。
- 安全取得 API 金鑰。
- 編輯現有的 API 金鑰以變更套件適用性。
- 重新整理或刪除現有的 API 金鑰，但不使用其他金鑰來阻礙作業。

## <a name="why-do-we-support-scoped-api-keys"></a>為什麼支援限定範圍的 API 金鑰？

我們支援限定範圍的 API 金鑰，讓您擁有更細緻的權限。 過去，NuGet 一個帳戶提供一個 API 金鑰，而此方法有幾個缺點：

- **一個 API 金鑰控制所有套件**。 當多位開發人員涉及不同套件且共用一個發佈者帳戶時，使用用於管理所有套件的單一 API 金鑰會難以安全共用金鑰。
- **所有權限或無權限**。 具有 API 金鑰存取權的任何人即擁有套件全部權限 (發佈、推送和取消列出)。 這通常不適合具有多個小組的環境。
- **單一失敗點**。 單一 API 金鑰也表示單一失敗點。 如果金鑰遭到入侵，則所有與該帳戶建立關聯的套件都可能遭到入侵。 重新整理 API 金鑰是防堵洩漏並避免中斷 CI/CD 工作流程的唯一方式。 此外，您也可能想要撤銷個別人士的 API 金鑰存取權 (例如，員工離職時)。 目前沒有清楚的方法可處理此問題。

我們嘗試使用限定範圍的 API 金鑰來解決這些問題，且同時確保現有的工作流程都不中斷。

## <a name="acquire-an-api-key"></a>取得 API 金鑰

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>建立限定範圍的 API 金鑰

您可以根據需求建立多個 API 金鑰。 一個 API 金鑰可以套用至一或多個套件、具有授與特定權限的不同範圍，以及具有與其建立關聯的到期日。

在下列範例中，您擁有名為 `Contoso service CI` 的 API 金鑰，它可用來推送特定 `Contoso.Service` 套件的套件，有效期限為 365 天。 這是一般案例：同一組織中有不同小組處理不同的套件，而小組成員獲得的金鑰，僅提供他們處理目前工作中套件的權限。 到期日是避免過期或忘記金鑰的機制。

![建立 API 金鑰](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>使用 Glob 模式

如果您要使用多個套件，且有龐大的套件清單要管理，您可以選擇使用萬用字元模式，同時選取多個套件。 例如，如果您想要授與金鑰給所有套件識別碼開頭為 `Fabrikam.Service` 的特定範圍，您可以在 [Glob 模式] 文字方塊中指定 `fabrikam.service.*` 來執行此作業。

![建立 API 金鑰-2](media/scoped-api-keys-glob-pattern.png)

使用 Glob 模式判斷 API 金鑰權限是否也適用於符合 Glob 模式的套件。 例如，如果您嘗試推送名為 `Fabrikam.Service.Framework` 的新套件，您可使用先前建立的金鑰完成此作業，因為套件符合 Glob 模式 `fabrikam.service.*`。

## <a name="obtain-api-keys-securely"></a>安全取得 API 金鑰

基於安全性，新建立的金鑰絕不會顯示在螢幕中，且只能使用 [複製] 按鈕取得。 同樣地，頁面重新整理後即無法存取金鑰。

![建立 API 金鑰-3](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>編輯現有的 API 金鑰

您可能也想要更新金鑰權限和範圍，但不變更金鑰本身。 如果您的金鑰具有單一套件特定範圍，您可以選擇將相同的範圍套用至一或多個其他套件。

![建立 API 金鑰-4](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>重新整理或刪除現有的 API 金鑰

帳戶擁有者可以選擇重新整理金鑰，如此一來，(套件的) 權限、範圍與到期日將維持不變，但會發出新的金鑰，讓舊的金鑰無法使用。 這有利於管理過時金鑰或有可能外洩的 API 金鑰。

![建立 API 金鑰-5](media/scoped-api-keys-refresh.png)

如果不再需要這些金鑰，您也可以選擇刪除它們。 刪除金鑰會移除該金鑰，並讓它無法使用。

## <a name="faqs"></a>常見問題集

### <a name="what-happens-to-my-old-legacy-api-key"></a>舊的 (舊版) API 金鑰會怎麼樣？

您的舊 API 金鑰 (舊版) 會繼續運作，且您想要它運作多久都可以。 不過，如果超過 365 天未使用這些金鑰來推送套件，則會加以淘汰。 如需詳細資料，請參閱部落格文章 [Changes to expiring API keys](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html) (即將過期 API 金鑰的變更)。 您無法再重新整理此金鑰。 您需要刪除舊版金鑰，改建立新的限定範圍金鑰。

> [!NOTE]
> 此金鑰具有所有套件的全部權限，且永不過期。 您應該考慮刪除此金鑰，並使用限定範圍的權限和明確到期日來建立新的金鑰。

### <a name="how-many-api-keys-can-i-create"></a>可以建立幾個 API 金鑰？

您可以建立無數個 API 金鑰。 不過，建議您保持在可管理的計數，以免最後因為過時的金鑰太多，而不知道誰在何處使用它們。

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>我可以刪除舊版 API 金鑰或立即停止嗎？

是。 您可以 (而且可能應該) 刪除舊版的 API 金鑰。

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>我可以找回不小心刪除的 API 金鑰嗎？

不會。 刪除後，您只能建立新的金鑰。 無法復原意外刪除的金鑰。

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>重新整理 API 金鑰時，舊的 API 金鑰還會繼續運作嗎？

不會。 金鑰一經重新整理就會產生與舊金鑰具有相同範圍、權限和到期日的新金鑰。 舊的金鑰不再存在。

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>我可以為現有的 API 金鑰授與更多權限嗎？

您無法修改範圍，但您可以編輯它適用的套件清單。

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>如何知道金鑰過期或即將過期？

如果任何金鑰過期，我們會透過頁面頂端的警告訊息讓您知道。 我們也會在金鑰到期日前十天，向帳戶持有者傳送警告電子郵件，讓您預先採取行動。