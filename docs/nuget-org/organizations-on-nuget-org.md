---
title: 您在 NuGet.org 上的組織
description: 在 NuGet.org 上的組織可協助您管理群組發佈或在小組、公司環境中所發佈套件。
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427073"
---
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="c42f0-103">您在 NuGet.org 上的組織</span><span class="sxs-lookup"><span data-stu-id="c42f0-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="c42f0-104">組織能讓企業和開放原始碼專案在使用單一 NuGet.org 身分識別的套件上共同作業。</span><span class="sxs-lookup"><span data-stu-id="c42f0-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="c42f0-105">針對套件取用者，會出現和 NuGet.org 現有使用者帳戶相同的組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="c42f0-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="c42f0-106">組織帳戶與個別帳戶</span><span class="sxs-lookup"><span data-stu-id="c42f0-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="c42f0-107">組織帳戶有一或多個作為其成員的個別 (使用者) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c42f0-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="c42f0-108">這些成員可以管理一組套件，同時維持擁有權的單一身分識別。</span><span class="sxs-lookup"><span data-stu-id="c42f0-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="c42f0-109">個別帳戶是您在 NuGet.org 上的身分識別，且可以是任意數目的組織成員。</span><span class="sxs-lookup"><span data-stu-id="c42f0-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="c42f0-110">套件可以屬於組織帳戶，就像可以屬於個人帳戶一樣。</span><span class="sxs-lookup"><span data-stu-id="c42f0-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="c42f0-111">套件取用者看不到個別帳戶和組織帳戶之間的差異：兩者皆以套件 `owners` 形式出現。</span><span class="sxs-lookup"><span data-stu-id="c42f0-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="c42f0-112">新增組織</span><span class="sxs-lookup"><span data-stu-id="c42f0-112">Adding a new organization</span></span>

<span data-ttu-id="c42f0-113">若要新增組織，請選取您在 NuGet.org 上的帳戶，然後選取 [管理組織]\*\*\*\* 功能表命令：</span><span class="sxs-lookup"><span data-stu-id="c42f0-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![NuGet.org 上的管理員組織功能表選項](media/org-manage-option.png)

<span data-ttu-id="c42f0-115">在下一個頁面上，選取 [新增組織]\*\*\*\* 按鈕：</span><span class="sxs-lookup"><span data-stu-id="c42f0-115">On the next page, select the **Add new organization** button:</span></span>

![在 NuGet.org 上建立新組織的按鈕](media/org-add-new-option.png)

<span data-ttu-id="c42f0-117">在下一個頁面上，提供組織名稱和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="c42f0-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="c42f0-118">因為組織帳戶會共用和使用者帳戶相同的命名空間，所以組織名稱必須不同於任何其他現有的組織或使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="c42f0-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="c42f0-119">電子郵件地址在所有帳戶中也必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="c42f0-119">The email address must also be unique across all accounts.</span></span>

![在 NuGet.org 上新增組織頁面](media/org-add-new-page.png)

<span data-ttu-id="c42f0-121">建立組織帳戶之後，您就是管理員，且可以送出組織套件並新增組織成員。</span><span class="sxs-lookup"><span data-stu-id="c42f0-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="c42f0-122">將現有帳戶轉換成組織</span><span class="sxs-lookup"><span data-stu-id="c42f0-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="c42f0-123">帳戶轉換無法復原：您無法將組織轉換回使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="c42f0-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="c42f0-124">如果您要使用單一使用者帳戶以小組形式管理套件，且想要將該帳戶轉換成組織，請使用 [管理組織]\*\*\*\* 頁面上的 [Transform your account to an organization] \(將帳戶轉換成組織\)\*\*\*\* 選項：</span><span class="sxs-lookup"><span data-stu-id="c42f0-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![NuGet.org 上將現有帳戶轉換成組織的選項](media/org-transform-option.png)

<span data-ttu-id="c42f0-126">在下個頁面上，指定將不同的使用者帳戶指派為組織管理員，然後選取 [轉換]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="c42f0-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![輸入資訊以將使用者帳戶轉換為組織](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="c42f0-128">管理組織成員</span><span class="sxs-lookup"><span data-stu-id="c42f0-128">Managing organization members</span></span>

<span data-ttu-id="c42f0-129">身為組織管理員，您可以藉由提供每個成員的 NuGet.org「使用者帳戶名稱」\*\* 來新增成員；無法使用電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="c42f0-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="c42f0-130">然後，將每個成員標示為具有下列權限的共同作業者或管理員：</span><span class="sxs-lookup"><span data-stu-id="c42f0-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="c42f0-131">權限</span><span class="sxs-lookup"><span data-stu-id="c42f0-131">Permission</span></span> | <span data-ttu-id="c42f0-132">共同作業者</span><span class="sxs-lookup"><span data-stu-id="c42f0-132">Collaborator</span></span> | <span data-ttu-id="c42f0-133">系統管理員</span><span class="sxs-lookup"><span data-stu-id="c42f0-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c42f0-134">管理組織的套件</span><span class="sxs-lookup"><span data-stu-id="c42f0-134">Manage the organization's packages</span></span><br/><span data-ttu-id="c42f0-135">(提交新套件、更新或取消列出現有的套件)</span><span class="sxs-lookup"><span data-stu-id="c42f0-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="c42f0-136">是</span><span class="sxs-lookup"><span data-stu-id="c42f0-136">Yes</span></span> | <span data-ttu-id="c42f0-137">是</span><span class="sxs-lookup"><span data-stu-id="c42f0-137">Yes</span></span> |
| <span data-ttu-id="c42f0-138">變更組織中繼資料</span><span class="sxs-lookup"><span data-stu-id="c42f0-138">Change organization metadata</span></span><br/><span data-ttu-id="c42f0-139">(電子郵件地址、通知設定)</span><span class="sxs-lookup"><span data-stu-id="c42f0-139">(email address, notification settings)</span></span> | <span data-ttu-id="c42f0-140">否</span><span class="sxs-lookup"><span data-stu-id="c42f0-140">No</span></span> | <span data-ttu-id="c42f0-141">是</span><span class="sxs-lookup"><span data-stu-id="c42f0-141">Yes</span></span> |
| <span data-ttu-id="c42f0-142">管理組織成員</span><span class="sxs-lookup"><span data-stu-id="c42f0-142">Manage organization members</span></span> | <span data-ttu-id="c42f0-143">否</span><span class="sxs-lookup"><span data-stu-id="c42f0-143">No</span></span> | <span data-ttu-id="c42f0-144">是</span><span class="sxs-lookup"><span data-stu-id="c42f0-144">Yes</span></span> |
| <span data-ttu-id="c42f0-145">要求或處理組織套件的共用擁有權要求</span><span class="sxs-lookup"><span data-stu-id="c42f0-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="c42f0-146">否</span><span class="sxs-lookup"><span data-stu-id="c42f0-146">No</span></span> | <span data-ttu-id="c42f0-147">是</span><span class="sxs-lookup"><span data-stu-id="c42f0-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="c42f0-148">管理套件</span><span class="sxs-lookup"><span data-stu-id="c42f0-148">Managing packages</span></span>

<span data-ttu-id="c42f0-149">您可以在 [[管理套件]](https://www.nuget.org/account/Packages) 頁面中檢視您所有帳戶和隸屬所有組織中的所有套件。</span><span class="sxs-lookup"><span data-stu-id="c42f0-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="c42f0-150">若要檢視帳戶或任何特定組織的特定套件，請使用頁面右上方的帳戶篩選器。</span><span class="sxs-lookup"><span data-stu-id="c42f0-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![使用帳戶篩選器管理套件](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="c42f0-152">將套件傳輸到組織</span><span class="sxs-lookup"><span data-stu-id="c42f0-152">Transferring packages to an organization</span></span>
<span data-ttu-id="c42f0-153">如果您想要將部分套件傳輸至新建立的組織，您可以要求組織帳戶共同擁有該套件，然後以擁有者身分移除自己來完成此操作。</span><span class="sxs-lookup"><span data-stu-id="c42f0-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="c42f0-154">如果您是組織的管理員，則不需要確認即可接受擁有權。</span><span class="sxs-lookup"><span data-stu-id="c42f0-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="c42f0-155">不過，如果您是共同作業者，當以擁有者身分來新增組織時將需要其中一位管理員來接受擁有權。</span><span class="sxs-lookup"><span data-stu-id="c42f0-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="c42f0-156">發行套件</span><span class="sxs-lookup"><span data-stu-id="c42f0-156">Publishing packages</span></span>

<span data-ttu-id="c42f0-157">將套件發佈到組織就像將套件發佈到使用者帳戶一樣：直接將套件上傳至 NuGet.org，或透過 `nuget push` 或 `dotnet nuget push` CLI 命令推送套件。</span><span class="sxs-lookup"><span data-stu-id="c42f0-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="c42f0-158">上傳套件</span><span class="sxs-lookup"><span data-stu-id="c42f0-158">Uploading packages</span></span>

<span data-ttu-id="c42f0-159">當您在 [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) (NuGet.org 上傳) 頁面直接上傳新套件時，您會將套件擁有者指派給使用者或組織帳戶：</span><span class="sxs-lookup"><span data-stu-id="c42f0-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![使用帳戶選項上傳套件](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="c42f0-161">使用 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="c42f0-161">Using API keys</span></span>

<span data-ttu-id="c42f0-162">若要透過 `nuget push` 或 `dotnet nuget push` CLI 命令推送套件，您必須取得這些命令需要的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c42f0-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="c42f0-163">如需詳細資料，請參閱[發佈套件](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)。</span><span class="sxs-lookup"><span data-stu-id="c42f0-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="c42f0-164">建立新的 API 金鑰時，請在 [Package Owner] \(套件擁有者\)\*\*\*\* 下拉式清單中選取適當的組織。</span><span class="sxs-lookup"><span data-stu-id="c42f0-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="c42f0-165">您建立的任何 API 金鑰僅適用於所選組織：</span><span class="sxs-lookup"><span data-stu-id="c42f0-165">Any API key you create is applicable only to the chosen organization:</span></span>

![具有帳戶選項的 API 金鑰](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="c42f0-167">移除組織</span><span class="sxs-lookup"><span data-stu-id="c42f0-167">Removing an organization</span></span>

<span data-ttu-id="c42f0-168">身為使用者，您可以選取組織成員資格顯示的 **X** 按鈕，將自己從組織中移除：</span><span class="sxs-lookup"><span data-stu-id="c42f0-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![從組織中移除使用者帳戶](media/org-remove-self-option.png)

<span data-ttu-id="c42f0-170">管理員可以從組織中移除任何成員，包括其他管理員。</span><span class="sxs-lookup"><span data-stu-id="c42f0-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="c42f0-171">如果您是組織唯一的管理員，除非您將其他成員新增為管理員，否則無法移除自己。</span><span class="sxs-lookup"><span data-stu-id="c42f0-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="c42f0-172">刪除組織帳戶</span><span class="sxs-lookup"><span data-stu-id="c42f0-172">Deleting an organization account</span></span>

<span data-ttu-id="c42f0-173">您可以按一下組織頁面顯示的 [刪除]\*\*\*\* 按鈕，刪除組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="c42f0-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![刪除組織](media/org-delete-option.png)

<span data-ttu-id="c42f0-175">若要刪除組織，您必須按一下 [刪除組織]\*\*\*\* 確認按鈕確認作業。</span><span class="sxs-lookup"><span data-stu-id="c42f0-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
