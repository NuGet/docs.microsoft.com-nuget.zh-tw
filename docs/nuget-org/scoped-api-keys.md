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
# <a name="scoped-api-keys"></a><span data-ttu-id="c9d44-103">限定範圍的 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="c9d44-103">Scoped API keys</span></span>

<span data-ttu-id="c9d44-104">若要讓 NuGet 成為更安全的套件發佈環境，您可以透過新增範圍來控制 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-104">To make NuGet a more secure environment for package distribution, you can take control of the API keys by adding scopes.</span></span>

<span data-ttu-id="c9d44-105">提供 API 金鑰範圍的能力可讓您更好控制 API。</span><span class="sxs-lookup"><span data-stu-id="c9d44-105">The ability to provide scope to your API keys give you better control on your APIs.</span></span> <span data-ttu-id="c9d44-106">您可以：</span><span class="sxs-lookup"><span data-stu-id="c9d44-106">You can:</span></span>

- <span data-ttu-id="c9d44-107">建立多個限定範圍的 API 金鑰，以用於不同套件配合不同的到期時間範圍。</span><span class="sxs-lookup"><span data-stu-id="c9d44-107">Create multiple scoped API keys that can be used for different packages with varying expiration timeframes.</span></span>
- <span data-ttu-id="c9d44-108">安全取得 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-108">Obtain API keys securely.</span></span>
- <span data-ttu-id="c9d44-109">編輯現有的 API 金鑰以變更套件適用性。</span><span class="sxs-lookup"><span data-stu-id="c9d44-109">Edit existing API keys to change package applicability.</span></span>
- <span data-ttu-id="c9d44-110">重新整理或刪除現有的 API 金鑰，但不使用其他金鑰來阻礙作業。</span><span class="sxs-lookup"><span data-stu-id="c9d44-110">Refresh or delete existing API keys without hampering operations using other keys.</span></span>

## <a name="why-do-we-support-scoped-api-keys"></a><span data-ttu-id="c9d44-111">為什麼支援限定範圍的 API 金鑰？</span><span class="sxs-lookup"><span data-stu-id="c9d44-111">Why do we support scoped API keys?</span></span>

<span data-ttu-id="c9d44-112">我們支援限定範圍的 API 金鑰，讓您擁有更細緻的權限。</span><span class="sxs-lookup"><span data-stu-id="c9d44-112">We support scopes for API keys to allow you to have more fine-grained permissions.</span></span> <span data-ttu-id="c9d44-113">過去，NuGet 一個帳戶提供一個 API 金鑰，而此方法有幾個缺點：</span><span class="sxs-lookup"><span data-stu-id="c9d44-113">Previously, NuGet offered a single API key for an account, and that approach had several drawbacks:</span></span>

- <span data-ttu-id="c9d44-114">**一個 API 金鑰控制所有套件**。</span><span class="sxs-lookup"><span data-stu-id="c9d44-114">**One API key to control all packages**.</span></span> <span data-ttu-id="c9d44-115">當多位開發人員涉及不同套件且共用一個發佈者帳戶時，使用用於管理所有套件的單一 API 金鑰會難以安全共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-115">With a single API key that is used to manage all packages, it is difficult to securely share the key when multiple developers are involved with different packages, and when they share a publisher account.</span></span>
- <span data-ttu-id="c9d44-116">**所有權限或無權限**。</span><span class="sxs-lookup"><span data-stu-id="c9d44-116">**All permissions or none**.</span></span> <span data-ttu-id="c9d44-117">具有 API 金鑰存取權的任何人即擁有套件全部權限 (發佈、推送和取消列出)。</span><span class="sxs-lookup"><span data-stu-id="c9d44-117">Anyone with access to the API key has all permissions (publish, push and un-list) on the packages.</span></span> <span data-ttu-id="c9d44-118">這通常不適合具有多個小組的環境。</span><span class="sxs-lookup"><span data-stu-id="c9d44-118">This is often not desirable in environment with multiple teams.</span></span>
- <span data-ttu-id="c9d44-119">**單一失敗點**。</span><span class="sxs-lookup"><span data-stu-id="c9d44-119">**Single point of failure**.</span></span> <span data-ttu-id="c9d44-120">單一 API 金鑰也表示單一失敗點。</span><span class="sxs-lookup"><span data-stu-id="c9d44-120">A single API key also means a single point of failure.</span></span> <span data-ttu-id="c9d44-121">如果金鑰遭到入侵，則所有與該帳戶建立關聯的套件都可能遭到入侵。</span><span class="sxs-lookup"><span data-stu-id="c9d44-121">If the key is compromised, all packages associated with the account could potentially be compromised.</span></span> <span data-ttu-id="c9d44-122">重新整理 API 金鑰是防堵洩漏並避免中斷 CI/CD 工作流程的唯一方式。</span><span class="sxs-lookup"><span data-stu-id="c9d44-122">Refreshing the API key is the only way to plug the leak and avoid an interruption to your CI/CD workflow.</span></span> <span data-ttu-id="c9d44-123">此外，您也可能想要撤銷個別人士的 API 金鑰存取權 (例如，員工離職時)。</span><span class="sxs-lookup"><span data-stu-id="c9d44-123">In addition, there may be cases when you want to revoke access to the API key for an individual (for example, when an employee leaves the organization).</span></span> <span data-ttu-id="c9d44-124">目前沒有清楚的方法可處理此問題。</span><span class="sxs-lookup"><span data-stu-id="c9d44-124">There isn’t a clean way to handle this today.</span></span>

<span data-ttu-id="c9d44-125">我們嘗試使用限定範圍的 API 金鑰來解決這些問題，且同時確保現有的工作流程都不中斷。</span><span class="sxs-lookup"><span data-stu-id="c9d44-125">With scoped API keys, we try to address these problems while making sure that none of the existing workflows break.</span></span>

## <a name="acquire-an-api-key"></a><span data-ttu-id="c9d44-126">取得 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="c9d44-126">Acquire an API key</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a><span data-ttu-id="c9d44-127">建立限定範圍的 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="c9d44-127">Create scoped API keys</span></span>

<span data-ttu-id="c9d44-128">您可以根據需求建立多個 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-128">You can create multiple API keys based on your requirements.</span></span> <span data-ttu-id="c9d44-129">一個 API 金鑰可以套用至一或多個套件、具有授與特定權限的不同範圍，以及具有與其建立關聯的到期日。</span><span class="sxs-lookup"><span data-stu-id="c9d44-129">An API key can apply to one or more packages, have varying scopes that grant specific privileges, and have an expiration date associated with it.</span></span>

<span data-ttu-id="c9d44-130">在下列範例中，您擁有名為 `Contoso service CI` 的 API 金鑰，它可用來推送特定 `Contoso.Service` 套件的套件，有效期限為 365 天。</span><span class="sxs-lookup"><span data-stu-id="c9d44-130">In the following example, you have an API key named `Contoso service CI` that can be used to push packages for specific `Contoso.Service` packages, and is valid for 365 days.</span></span> <span data-ttu-id="c9d44-131">這是一般案例：同一組織中有不同小組處理不同的套件，而小組成員獲得的金鑰，僅提供他們處理目前工作中套件的權限。</span><span class="sxs-lookup"><span data-stu-id="c9d44-131">This is a typical scenario where different teams within the same organization work on different packages, and the members of the team are provided the key that grants them privileges only for the package they are working on.</span></span> <span data-ttu-id="c9d44-132">到期日是避免過期或忘記金鑰的機制。</span><span class="sxs-lookup"><span data-stu-id="c9d44-132">The expiration serves as a mechanism to prevent stale or forgotten keys.</span></span>

![建立 API 金鑰](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a><span data-ttu-id="c9d44-134">使用 Glob 模式</span><span class="sxs-lookup"><span data-stu-id="c9d44-134">Use glob patterns</span></span>

<span data-ttu-id="c9d44-135">如果您要使用多個套件，且有龐大的套件清單要管理，您可以選擇使用萬用字元模式，同時選取多個套件。</span><span class="sxs-lookup"><span data-stu-id="c9d44-135">If you are working on multiple packages and have a large list of packages to manage, you can choose to use globbing patterns to select multiple packages together.</span></span> <span data-ttu-id="c9d44-136">例如，如果您想要授與金鑰給所有套件識別碼開頭為 `Fabrikam.Service` 的特定範圍，您可以在 [Glob 模式] 文字方塊中指定 `fabrikam.service.*` 來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="c9d44-136">For example, if you wish to grant specific scopes to a key for all packages whose ID starts with `Fabrikam.Service`, you could do this by specifying `fabrikam.service.*` in the **Glob pattern** text box.</span></span>

![建立 API 金鑰-2](media/scoped-api-keys-glob-pattern.png)

<span data-ttu-id="c9d44-138">使用 Glob 模式判斷 API 金鑰權限是否也適用於符合 Glob 模式的套件。</span><span class="sxs-lookup"><span data-stu-id="c9d44-138">Using glob patterns to determine API key permissions also applies to new packages matching the glob pattern.</span></span> <span data-ttu-id="c9d44-139">例如，如果您嘗試推送名為 `Fabrikam.Service.Framework` 的新套件，您可使用先前建立的金鑰完成此作業，因為套件符合 Glob 模式 `fabrikam.service.*`。</span><span class="sxs-lookup"><span data-stu-id="c9d44-139">For example, if you try to push a new package named `Fabrikam.Service.Framework`, you can do that with the key created previously, since the package matches the glob pattern `fabrikam.service.*`.</span></span>

## <a name="obtain-api-keys-securely"></a><span data-ttu-id="c9d44-140">安全取得 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="c9d44-140">Obtain API keys securely</span></span>

<span data-ttu-id="c9d44-141">基於安全性，新建立的金鑰絕不會顯示在螢幕中，且只能使用 [複製] 按鈕取得。</span><span class="sxs-lookup"><span data-stu-id="c9d44-141">For security, a newly created key is never shown on the screen and is only available using the **Copy** button.</span></span> <span data-ttu-id="c9d44-142">同樣地，頁面重新整理後即無法存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-142">Similarly, the key is not accessible after the page is refreshed.</span></span>

![建立 API 金鑰-3](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a><span data-ttu-id="c9d44-144">編輯現有的 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="c9d44-144">Edit existing API keys</span></span>

<span data-ttu-id="c9d44-145">您可能也想要更新金鑰權限和範圍，但不變更金鑰本身。</span><span class="sxs-lookup"><span data-stu-id="c9d44-145">You may also want to update the key permissions and scopes without changing the key itself.</span></span> <span data-ttu-id="c9d44-146">如果您的金鑰具有單一套件特定範圍，您可以選擇將相同的範圍套用至一或多個其他套件。</span><span class="sxs-lookup"><span data-stu-id="c9d44-146">If you have a key with specific scope(s) for a single package, you can choose to apply the same scope(s) on one or many other packages.</span></span>

![建立 API 金鑰-4](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a><span data-ttu-id="c9d44-148">重新整理或刪除現有的 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="c9d44-148">Refresh or delete existing API keys</span></span>

<span data-ttu-id="c9d44-149">帳戶擁有者可以選擇重新整理金鑰，如此一來，(套件的) 權限、範圍與到期日將維持不變，但會發出新的金鑰，讓舊的金鑰無法使用。</span><span class="sxs-lookup"><span data-stu-id="c9d44-149">The account owner can choose to refresh the key, in which case the permission (on packages), scope, and expiry remain the same, but a new key is issued making the old key unusable.</span></span> <span data-ttu-id="c9d44-150">這有利於管理過時金鑰或有可能外洩的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-150">This is helpful in managing stale keys or where there is any potential for an API key leakage.</span></span>

![建立 API 金鑰-5](media/scoped-api-keys-refresh.png)

<span data-ttu-id="c9d44-152">如果不再需要這些金鑰，您也可以選擇刪除它們。</span><span class="sxs-lookup"><span data-stu-id="c9d44-152">You may also choose to delete these keys if they are not needed anymore.</span></span> <span data-ttu-id="c9d44-153">刪除金鑰會移除該金鑰，並讓它無法使用。</span><span class="sxs-lookup"><span data-stu-id="c9d44-153">Deleting a key removes the key and makes it unusable.</span></span>

## <a name="faqs"></a><span data-ttu-id="c9d44-154">常見問題集</span><span class="sxs-lookup"><span data-stu-id="c9d44-154">FAQs</span></span>

### <a name="what-happens-to-my-old-legacy-api-key"></a><span data-ttu-id="c9d44-155">舊的 (舊版) API 金鑰會怎麼樣？</span><span class="sxs-lookup"><span data-stu-id="c9d44-155">What happens to my old (legacy) API key?</span></span>

<span data-ttu-id="c9d44-156">您的舊 API 金鑰 (舊版) 會繼續運作，且您想要它運作多久都可以。</span><span class="sxs-lookup"><span data-stu-id="c9d44-156">Your old API key (legacy) continues to work and can work as long as you want it to work.</span></span> <span data-ttu-id="c9d44-157">不過，如果超過 365 天未使用這些金鑰來推送套件，則會加以淘汰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-157">However, these keys will be retired if they have not been used for more than 365 days to push a package.</span></span> <span data-ttu-id="c9d44-158">如需詳細資料，請參閱部落格文章 [Changes to expiring API keys](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html) (即將過期 API 金鑰的變更)。</span><span class="sxs-lookup"><span data-stu-id="c9d44-158">For more details, see the blog post [Changes to expiring API keys](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html).</span></span> <span data-ttu-id="c9d44-159">您無法再重新整理此金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-159">You can no longer refresh this key.</span></span> <span data-ttu-id="c9d44-160">您需要刪除舊版金鑰，改建立新的限定範圍金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-160">You need to delete the legacy key and create a new scoped key instead.</span></span>

> [!NOTE]
> <span data-ttu-id="c9d44-161">此金鑰具有所有套件的全部權限，且永不過期。</span><span class="sxs-lookup"><span data-stu-id="c9d44-161">This key has all permissions on all the packages and it never expires.</span></span> <span data-ttu-id="c9d44-162">您應該考慮刪除此金鑰，並使用限定範圍的權限和明確到期日來建立新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-162">You should consider deleting this key and creating new keys with scoped permissions and definite expiry.</span></span>

### <a name="how-many-api-keys-can-i-create"></a><span data-ttu-id="c9d44-163">可以建立幾個 API 金鑰？</span><span class="sxs-lookup"><span data-stu-id="c9d44-163">How many API keys can I create?</span></span>

<span data-ttu-id="c9d44-164">您可以建立無數個 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-164">There is no limit on the number of API keys you can create.</span></span> <span data-ttu-id="c9d44-165">不過，建議您保持在可管理的計數，以免最後因為過時的金鑰太多，而不知道誰在何處使用它們。</span><span class="sxs-lookup"><span data-stu-id="c9d44-165">However, we advise you to keep it to a manageable count so that you do not end up having many stale keys with no knowledge of where and who is using them.</span></span>

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a><span data-ttu-id="c9d44-166">我可以刪除舊版 API 金鑰或立即停止嗎？</span><span class="sxs-lookup"><span data-stu-id="c9d44-166">Can I delete my legacy API key or discontinue using now?</span></span>

<span data-ttu-id="c9d44-167">是。</span><span class="sxs-lookup"><span data-stu-id="c9d44-167">Yes.</span></span> <span data-ttu-id="c9d44-168">您可以 (而且可能應該) 刪除舊版的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-168">You can--and you probably should--delete your legacy API key.</span></span>

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a><span data-ttu-id="c9d44-169">我可以找回不小心刪除的 API 金鑰嗎？</span><span class="sxs-lookup"><span data-stu-id="c9d44-169">Can I get back my API key that I deleted by mistake?</span></span>

<span data-ttu-id="c9d44-170">不會。</span><span class="sxs-lookup"><span data-stu-id="c9d44-170">No.</span></span> <span data-ttu-id="c9d44-171">刪除後，您只能建立新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-171">Once deleted, you can only create new keys.</span></span> <span data-ttu-id="c9d44-172">無法復原意外刪除的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-172">There is no recovery possible for accidentally deleted keys.</span></span>

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a><span data-ttu-id="c9d44-173">重新整理 API 金鑰時，舊的 API 金鑰還會繼續運作嗎？</span><span class="sxs-lookup"><span data-stu-id="c9d44-173">Does the old API key continue to work upon API key refresh?</span></span>

<span data-ttu-id="c9d44-174">不會。</span><span class="sxs-lookup"><span data-stu-id="c9d44-174">No.</span></span> <span data-ttu-id="c9d44-175">金鑰一經重新整理就會產生與舊金鑰具有相同範圍、權限和到期日的新金鑰。</span><span class="sxs-lookup"><span data-stu-id="c9d44-175">Once you refresh a key, a new key gets generated that has the same scope, permission, and expiry as the old one.</span></span> <span data-ttu-id="c9d44-176">舊的金鑰不再存在。</span><span class="sxs-lookup"><span data-stu-id="c9d44-176">The old key ceases to exist.</span></span>

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a><span data-ttu-id="c9d44-177">我可以為現有的 API 金鑰授與更多權限嗎？</span><span class="sxs-lookup"><span data-stu-id="c9d44-177">Can I give more permissions to an existing API key?</span></span>

<span data-ttu-id="c9d44-178">您無法修改範圍，但您可以編輯它適用的套件清單。</span><span class="sxs-lookup"><span data-stu-id="c9d44-178">You cannot modify the scope, but you can edit the package list it is applicable to.</span></span>

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a><span data-ttu-id="c9d44-179">如何知道金鑰過期或即將過期？</span><span class="sxs-lookup"><span data-stu-id="c9d44-179">How do I know if any of my keys expired or are getting expired?</span></span>

<span data-ttu-id="c9d44-180">如果任何金鑰過期，我們會透過頁面頂端的警告訊息讓您知道。</span><span class="sxs-lookup"><span data-stu-id="c9d44-180">If any key expires, we will let you know through a warning message at the top of the page.</span></span> <span data-ttu-id="c9d44-181">我們也會在金鑰到期日前十天，向帳戶持有者傳送警告電子郵件，讓您預先採取行動。</span><span class="sxs-lookup"><span data-stu-id="c9d44-181">We also send a warning e-mail to the account holder ten days before the expiration of the key so that you can act on it well in advance.</span></span>