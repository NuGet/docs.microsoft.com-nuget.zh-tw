---
title: 在 nuget.org 的組織
description: 在 nuget.org 的組織可協助您管理封裝發佈到群組或小組，公司環境中。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2018
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="d58e1-103">Nuget.org 的組織</span><span class="sxs-lookup"><span data-stu-id="d58e1-103">Organization on nuget.org</span></span>

<span data-ttu-id="d58e1-104">組織可讓企業和共同作業上使用單一 nuget.org 識別封裝的開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="d58e1-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="d58e1-105">封裝取用者組織帳戶會出現在 nuget.org 上現有的使用者帳戶與相同。</span><span class="sxs-lookup"><span data-stu-id="d58e1-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="d58e1-106">與組織帳戶的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="d58e1-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="d58e1-107">您的使用者帳戶是您在 nuget.org 的身分識別，而且可以是任意數目的組織成員。</span><span class="sxs-lookup"><span data-stu-id="d58e1-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="d58e1-108">封裝可以屬於像它屬於使用者帳戶的組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="d58e1-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="d58e1-109">封裝取用者沒有看到任何使用者帳戶或組織帳戶之間的差異： 兩者都顯示為封裝`owners`。</span><span class="sxs-lookup"><span data-stu-id="d58e1-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="d58e1-110">組織帳戶會有一或多個使用者帳戶做為其成員。</span><span class="sxs-lookup"><span data-stu-id="d58e1-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="d58e1-111">這些成員可以管理一組封裝，同時維持單一識別身分的擁有權。</span><span class="sxs-lookup"><span data-stu-id="d58e1-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="d58e1-112">加入新的組織</span><span class="sxs-lookup"><span data-stu-id="d58e1-112">Adding a new organization</span></span>

<span data-ttu-id="d58e1-113">若要加入新的組織，選取您的帳戶上 nuget.org，然後選取 **管理組織...** 功能表命令：</span><span class="sxs-lookup"><span data-stu-id="d58e1-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![管理員組織在 nuget.org 的功能表選項](media/org-manage-option.png)

<span data-ttu-id="d58e1-115">在下一個頁面上，選取**加入新的組織**按鈕：</span><span class="sxs-lookup"><span data-stu-id="d58e1-115">On the next page, select the **Add new organization** button:</span></span>

![若要建立新的組織在 nuget.org 的按鈕](media/org-add-new-option.png)

<span data-ttu-id="d58e1-117">在下一個頁面上，提供組織名稱和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="d58e1-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="d58e1-118">因為組織帳戶會共用相同的命名空間，做為使用者帳戶，則必須從現有的組織或使用者帳戶不同的組織名稱。</span><span class="sxs-lookup"><span data-stu-id="d58e1-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="d58e1-119">跨所有帳戶電子郵件地址必須也是唯一。</span><span class="sxs-lookup"><span data-stu-id="d58e1-119">The email address must also be unique across all accounts.</span></span>

![Nuget.org 上加入新的組織頁面](media/org-add-new-page.png)

<span data-ttu-id="d58e1-121">組織帳戶建立之後，您是系統管理員可以送出組織的封裝和加入組織成員。</span><span class="sxs-lookup"><span data-stu-id="d58e1-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="d58e1-122">轉換現有的組織帳戶</span><span class="sxs-lookup"><span data-stu-id="d58e1-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="d58e1-123">帳戶轉換為無法復原： 您無法轉換回給使用者帳戶的組織。</span><span class="sxs-lookup"><span data-stu-id="d58e1-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="d58e1-124">如果您正在為使用單一使用者帳戶的小組管理封裝，並想要將該帳戶轉換成組織中，使用**轉換您的帳戶是組織**選項**管理組織**頁面：</span><span class="sxs-lookup"><span data-stu-id="d58e1-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![轉換現有的帳戶是組織在 nuget.org 選項](media/org-transform-option.png)

<span data-ttu-id="d58e1-126">在下一個頁面上，指定不同的使用者帳戶指派為系統管理員的組織，然後選取**轉換**。</span><span class="sxs-lookup"><span data-stu-id="d58e1-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![輸入轉換是組織的使用者帳戶的資訊](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="d58e1-128">管理組織成員</span><span class="sxs-lookup"><span data-stu-id="d58e1-128">Managing organization members</span></span>

<span data-ttu-id="d58e1-129">組織系統管理員，您可以新增成員，藉由提供每個成員 nuget.org*使用者帳戶名稱*; 無法使用電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="d58e1-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="d58e1-130">然後，您會標示每個成員的共同作業者或具有下列權限的系統管理員：</span><span class="sxs-lookup"><span data-stu-id="d58e1-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="d58e1-131">權限</span><span class="sxs-lookup"><span data-stu-id="d58e1-131">Permission</span></span> | <span data-ttu-id="d58e1-132">共同作業者</span><span class="sxs-lookup"><span data-stu-id="d58e1-132">Collaborator</span></span> | <span data-ttu-id="d58e1-133">系統管理員</span><span class="sxs-lookup"><span data-stu-id="d58e1-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d58e1-134">管理組織的封裝</span><span class="sxs-lookup"><span data-stu-id="d58e1-134">Manage the organization's packages</span></span><br/><span data-ttu-id="d58e1-135">（提交新的封裝、 更新或 unlist 現有的封裝）</span><span class="sxs-lookup"><span data-stu-id="d58e1-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="d58e1-136">[是]</span><span class="sxs-lookup"><span data-stu-id="d58e1-136">Yes</span></span> | <span data-ttu-id="d58e1-137">[是]</span><span class="sxs-lookup"><span data-stu-id="d58e1-137">Yes</span></span> |
| <span data-ttu-id="d58e1-138">變更組織中繼資料</span><span class="sxs-lookup"><span data-stu-id="d58e1-138">Change organization metadata</span></span><br/><span data-ttu-id="d58e1-139">（電子郵件地址，通知設定）</span><span class="sxs-lookup"><span data-stu-id="d58e1-139">(email address, notification settings)</span></span> | <span data-ttu-id="d58e1-140">否</span><span class="sxs-lookup"><span data-stu-id="d58e1-140">No</span></span> | <span data-ttu-id="d58e1-141">[是]</span><span class="sxs-lookup"><span data-stu-id="d58e1-141">Yes</span></span> |
| <span data-ttu-id="d58e1-142">管理組織成員</span><span class="sxs-lookup"><span data-stu-id="d58e1-142">Manage organization members</span></span> | <span data-ttu-id="d58e1-143">否</span><span class="sxs-lookup"><span data-stu-id="d58e1-143">No</span></span> | <span data-ttu-id="d58e1-144">[是]</span><span class="sxs-lookup"><span data-stu-id="d58e1-144">Yes</span></span> |
| <span data-ttu-id="d58e1-145">要求或 co-ownership 組織封裝要求處理</span><span class="sxs-lookup"><span data-stu-id="d58e1-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="d58e1-146">否</span><span class="sxs-lookup"><span data-stu-id="d58e1-146">No</span></span> | <span data-ttu-id="d58e1-147">[是]</span><span class="sxs-lookup"><span data-stu-id="d58e1-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="d58e1-148">管理封裝</span><span class="sxs-lookup"><span data-stu-id="d58e1-148">Managing packages</span></span>

<span data-ttu-id="d58e1-149">您可以檢視所有封裝，在您的帳戶及其中您必須是成員的所有組織[管理封裝](https://www.nuget.org/account/Packages)頁面。</span><span class="sxs-lookup"><span data-stu-id="d58e1-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="d58e1-150">若要檢視您的帳戶或任何特定組織專用的封裝，使用帳戶篩選器右上方的頁面。</span><span class="sxs-lookup"><span data-stu-id="d58e1-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![使用帳戶篩選來管理封裝](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="d58e1-152">將封裝傳送到組織</span><span class="sxs-lookup"><span data-stu-id="d58e1-152">Transferring packages to an organization</span></span>
<span data-ttu-id="d58e1-153">如果您想要傳送部分封裝到新建立的組織，您可以透過要求來共同擁有封裝的組織帳戶，然後再移除自行為擁有者。</span><span class="sxs-lookup"><span data-stu-id="d58e1-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="d58e1-154">如果您是組織的系統管理員，沒有任何確認才能接受擁有權。</span><span class="sxs-lookup"><span data-stu-id="d58e1-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="d58e1-155">不過，如果您是共同作業者，以擁有者加入組織需要一個接受擁有權的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="d58e1-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="d58e1-156">發行套件</span><span class="sxs-lookup"><span data-stu-id="d58e1-156">Publishing packages</span></span>

<span data-ttu-id="d58e1-157">您將封裝發佈到使用者帳戶一樣，是組織發行封裝： 直接上傳至 nuget.org 的封裝，或發送封裝`nuget push`或`dotnet nuget push`CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="d58e1-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="d58e1-158">上傳封裝</span><span class="sxs-lookup"><span data-stu-id="d58e1-158">Uploading packages</span></span>

<span data-ttu-id="d58e1-159">當您直接上傳新的封裝上[nuget.org 上載](https://www.nuget.org/packages/manage/upload) 頁面上，您將封裝擁有者的使用者或組織帳戶：</span><span class="sxs-lookup"><span data-stu-id="d58e1-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![上傳封裝的帳戶選項](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="d58e1-161">使用 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="d58e1-161">Using API keys</span></span>

<span data-ttu-id="d58e1-162">推播封裝`nuget push`或`dotnet nuget push`CLI 命令，您必須取得 API 金鑰所需的這些命令。</span><span class="sxs-lookup"><span data-stu-id="d58e1-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="d58e1-163">如需詳細資訊，請參閱[發佈封裝](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)。</span><span class="sxs-lookup"><span data-stu-id="d58e1-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="d58e1-164">在建立新的 API 金鑰時，選取適當的組織中**封裝擁有者**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="d58e1-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="d58e1-165">您所建立的任何 API 金鑰是僅適用於所選的組織：</span><span class="sxs-lookup"><span data-stu-id="d58e1-165">Any API key you create is applicable only to the chosen organization:</span></span>

![API 金鑰與帳戶選項](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="d58e1-167">移除組織</span><span class="sxs-lookup"><span data-stu-id="d58e1-167">Removing an organization</span></span>

<span data-ttu-id="d58e1-168">身為使用者，您可以將自己移除組織選取`X`按鈕顯示您組織的成員資格：</span><span class="sxs-lookup"><span data-stu-id="d58e1-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![從組織移除使用者帳戶](media/org-remove-self-option.png)

<span data-ttu-id="d58e1-170">系統管理員可以從組織，包括其他系統管理員移除任何成員。</span><span class="sxs-lookup"><span data-stu-id="d58e1-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="d58e1-171">如果您的組織唯一的系統管理員，您無法移除自己，除非您以系統管理員身分加入另一個成員。</span><span class="sxs-lookup"><span data-stu-id="d58e1-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="d58e1-172">刪除組織帳戶</span><span class="sxs-lookup"><span data-stu-id="d58e1-172">Deleting an organization account</span></span>

<span data-ttu-id="d58e1-173">這項功能即將推出。</span><span class="sxs-lookup"><span data-stu-id="d58e1-173">This feature is coming soon.</span></span>
