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
# <a name="individual-accounts"></a><span data-ttu-id="74111-103">個人帳戶</span><span class="sxs-lookup"><span data-stu-id="74111-103">Individual accounts</span></span>

<span data-ttu-id="74111-104">您必須建立個人帳戶，才能在 NuGet.org 上發佈和管理套件。</span><span class="sxs-lookup"><span data-stu-id="74111-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="74111-105">個人帳戶與組織帳戶</span><span class="sxs-lookup"><span data-stu-id="74111-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="74111-106">個人 (使用者) 帳戶是您在 NuGet.org 上的身分識別，且可以是任意數目組織的成員。</span><span class="sxs-lookup"><span data-stu-id="74111-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="74111-107">套件可以屬於組織帳戶，如同其可屬於個別帳戶。</span><span class="sxs-lookup"><span data-stu-id="74111-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="74111-108">套件取用者看不到個人帳戶和組織帳戶之間的差異：兩者皆以套件 `owners` 形式出現。</span><span class="sxs-lookup"><span data-stu-id="74111-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="74111-109">組織帳戶有一或多個作為其成員的個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="74111-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="74111-110">這些成員可以管理一組套件，同時維持擁有權的單一身分識別。</span><span class="sxs-lookup"><span data-stu-id="74111-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="74111-111">新增新的個人帳戶</span><span class="sxs-lookup"><span data-stu-id="74111-111">Add a new individual account</span></span>

<span data-ttu-id="74111-112">您必須擁有個人 Microsoft 帳戶或 Azure Active Directory (AAD) 帳戶才能建立 NuGet.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="74111-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="74111-113">如果沒有的話，您可以[建立](https://signup.live.com)帳戶。</span><span class="sxs-lookup"><span data-stu-id="74111-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="74111-114">如果您擁有 MSA 或 AAD 帳戶，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="74111-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="74111-115">前往 [uGet.org 登入頁面](https://www.nuget.org/users/account/LogOn)。</span><span class="sxs-lookup"><span data-stu-id="74111-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="74111-116">按一下 [使用 Microsoft 帳戶登入]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="74111-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="74111-117">輸入您的 Microsoft 帳戶或 Azure Active Directory 帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="74111-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="74111-118">請按一下 [是]  接受要提供給 *NuGet.org* 申請的權限。</span><span class="sxs-lookup"><span data-stu-id="74111-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![將權限授與 NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="74111-120">系統會將您重新導向至 *nuget.org*，並向您要求註冊使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="74111-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="74111-121">在輸入方塊中指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="74111-121">Specify the username in the input box.</span></span> <span data-ttu-id="74111-122">請注意，使用者名稱**會**區分大小寫，且往後無法再變更或重新命名。</span><span class="sxs-lookup"><span data-stu-id="74111-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![在 NuGet.org 上指定使用者名稱](media/nuget-org-register.png) 

1. <span data-ttu-id="74111-124">按一下 [註冊]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="74111-124">Click the **Register** button.</span></span>

<span data-ttu-id="74111-125">您現在擁有 NuGet.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="74111-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="74111-126">您可以在[帳戶設定](https://www.nuget.org/account)頁面上進行帳戶管理。</span><span class="sxs-lookup"><span data-stu-id="74111-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
