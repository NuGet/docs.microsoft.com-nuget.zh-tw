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
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="fa80f-103">NuGet.org 上的個人帳戶</span><span class="sxs-lookup"><span data-stu-id="fa80f-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="fa80f-104">您必須建立個人帳戶，才能在 NuGet.org 上發佈和管理套件。</span><span class="sxs-lookup"><span data-stu-id="fa80f-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="fa80f-105">個人帳戶與組織帳戶</span><span class="sxs-lookup"><span data-stu-id="fa80f-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="fa80f-106">個人 (使用者) 帳戶是您在 NuGet.org 上的身分識別，且可以是任意數目組織的成員。</span><span class="sxs-lookup"><span data-stu-id="fa80f-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="fa80f-107">套件可以屬於組織帳戶，就像可以屬於個人帳戶一樣。</span><span class="sxs-lookup"><span data-stu-id="fa80f-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="fa80f-108">套件取用者看不到個別帳戶和組織帳戶之間的差異：兩者皆以套件 `owners` 形式出現。</span><span class="sxs-lookup"><span data-stu-id="fa80f-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="fa80f-109">組織帳戶有一或多個作為其成員的個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa80f-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="fa80f-110">這些成員可以管理一組套件，同時維持擁有權的單一身分識別。</span><span class="sxs-lookup"><span data-stu-id="fa80f-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="fa80f-111">新增新的個人帳戶</span><span class="sxs-lookup"><span data-stu-id="fa80f-111">Add a new individual account</span></span>

<span data-ttu-id="fa80f-112">您必須擁有個人 Microsoft 帳戶或 Azure Active Directory (AAD) 帳戶才能建立 NuGet.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa80f-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="fa80f-113">如果沒有的話，您可以[建立](https://signup.live.com)帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa80f-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="fa80f-114">如果您擁有 MSA 或 AAD 帳戶，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="fa80f-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="fa80f-115">跳到[NuGet.org 登入頁面](https://www.nuget.org/users/account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="fa80f-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="fa80f-116">按一下 [使用 Microsoft 帳戶登入]\*\*\*\* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa80f-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="fa80f-117">輸入您的 Microsoft 帳戶或 Azure Active Directory 帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fa80f-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="fa80f-118">請按一下 [是]\*\*\*\* 接受要提供給 *NuGet.org* 申請的權限。</span><span class="sxs-lookup"><span data-stu-id="fa80f-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![將權限授與 NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="fa80f-120">您將被重定向到*nuget.org*,並要求註冊使用者名。</span><span class="sxs-lookup"><span data-stu-id="fa80f-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="fa80f-121">在輸入方塊中指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="fa80f-121">Specify the username in the input box.</span></span> <span data-ttu-id="fa80f-122">請注意，使用者名稱**會**區分大小寫，且往後無法再變更或重新命名。</span><span class="sxs-lookup"><span data-stu-id="fa80f-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![在 NuGet.org 上指定使用者名稱](media/nuget-org-register.png) 

1. <span data-ttu-id="fa80f-124">按下 **「註冊」** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa80f-124">Click the **Register** button.</span></span>

<span data-ttu-id="fa80f-125">您現在擁有 NuGet.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa80f-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="fa80f-126">您可以在[帳戶設定](https://www.nuget.org/account)頁面上進行帳戶管理。</span><span class="sxs-lookup"><span data-stu-id="fa80f-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="fa80f-127">使用雙重要素驗證 (2FA)</span><span class="sxs-lookup"><span data-stu-id="fa80f-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="fa80f-128">雙重身份驗證(2FA)是登錄網站或應用時使用的額外安全層。</span><span class="sxs-lookup"><span data-stu-id="fa80f-128">Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps.</span></span> <span data-ttu-id="fa80f-129">使用 2FA,您必須使用 Microsoft 帳戶 (MSA) 登錄並提供只有您知道或有權訪問的另一種形式的身份驗證。</span><span class="sxs-lookup"><span data-stu-id="fa80f-129">With 2FA, you have to log in with your Microsoft Account (MSA) and provide another form of authentication that only you know or have access to.</span></span> <span data-ttu-id="fa80f-130">若要更有效地保護您的帳戶，請啟用雙重要素驗證 (建議)。</span><span class="sxs-lookup"><span data-stu-id="fa80f-130">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="fa80f-131">登入您的帳戶後，開啟您的設定檔，然後選擇 [登入帳戶]\*\*\*\* 下的 [啟用]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="fa80f-131">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![啟用 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="fa80f-133">您會看到一則訊息，告訴您下一次登入 *nuget.org* 時，系統會要求您提供額外的認證。</span><span class="sxs-lookup"><span data-stu-id="fa80f-133">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="fa80f-134">若要立即完成驗證，請先登出，然後再重新登入一次。</span><span class="sxs-lookup"><span data-stu-id="fa80f-134">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="fa80f-135">當您登入時，請選擇簡訊或電子郵件做為第二種形式的驗證。</span><span class="sxs-lookup"><span data-stu-id="fa80f-135">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="fa80f-136">確認已與 Microsoft 帳戶相關聯的電話號碼或電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fa80f-136">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="fa80f-137">您可能需要為您的帳戶輸入新的電話號碼或電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fa80f-137">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="fa80f-138">如果是這樣，請依照指示輸入必要資訊，然後按一下 [下一步]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="fa80f-138">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![啟用 2FA](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="fa80f-140">檢查您的裝置或電子郵件帳戶，然後輸入我們剛傳送給您的代碼。</span><span class="sxs-lookup"><span data-stu-id="fa80f-140">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![啟用 2FA](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="fa80f-142">請遵循任何其他指示來完成雙重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="fa80f-142">Follow any additional instructions to complete Two-factor authentication.</span></span>

> [!Tip]
> <span data-ttu-id="fa80f-143">為NuGet.org帳戶啟用 2FA 不會影響可能連結到您用於登入NuGet.org的Microsoft帳戶的其他帳戶或服務的身份驗證設置。</span><span class="sxs-lookup"><span data-stu-id="fa80f-143">Enabling 2FA for your NuGet.org account does not impact authentication settings for other accounts or services that may be linked to the Microsoft account you use to login to NuGet.org.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="fa80f-144">刪除 NuGet.org 帳戶</span><span class="sxs-lookup"><span data-stu-id="fa80f-144">Delete a NuGet.org account</span></span>

<span data-ttu-id="fa80f-145">如需其他帳戶相關工作 (例如刪除 NuGet.org 帳戶) 的說明，請參閱 [NuGet.org 帳戶管理](nuget-org-faq.md#nugetorg-account-management)。</span><span class="sxs-lookup"><span data-stu-id="fa80f-145">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
