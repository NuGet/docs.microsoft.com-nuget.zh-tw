---
title: "如何發行 NuGet 套件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/5/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2342aabd-983e-4db1-9230-57c84fa36969
description: "如何將 NuGet 套件發行至 nuget.org 或私用摘要以及如何在 nuget.org 上管理套件擁有權的詳細指示。"
keywords: "NuGet 套件發行、發行 NuGet 套件、NuGet 套件擁有權、發行至 nuget.org、私用 NuGet 摘要"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: fab25931165afb65aa3fd09c5bc37492ce814a49
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="publishing-packages"></a><span data-ttu-id="51a34-104">發行套件</span><span class="sxs-lookup"><span data-stu-id="51a34-104">Publishing packages</span></span>

<span data-ttu-id="51a34-105">已使用 `nuget pack` [建立套件](../create-packages/creating-a-package.md)之後，其他開發人員使用它 (公開或私用) 的程序就會變得簡單：</span><span class="sxs-lookup"><span data-stu-id="51a34-105">Once you have [created a package](../create-packages/creating-a-package.md) with `nuget pack`, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="51a34-106">如本主題中所述，所有開發人員都可以透過 [nuget.org](https://www.nuget.org/packages/manage/upload) 全域使用公用套件。</span><span class="sxs-lookup"><span data-stu-id="51a34-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this topic.</span></span>
- <span data-ttu-id="51a34-107">私用套件僅適用於小組或組織，方法是將它們裝載在檔案共用、私用 NuGet 伺服器、[Visual Studio Team Services 套件管理](https://www.visualstudio.com/docs/package/nuget/publish)或協力廠商存放庫 (例如 myget、ProGet、Nexus Repository 和 Artifactory)。</span><span class="sxs-lookup"><span data-stu-id="51a34-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="51a34-108">如需其他詳細資料，請參閱[裝載套件概觀](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="51a34-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="51a34-109">本主題涵蓋發行至 nuget.org；若要發行至 Visual Studio Team Services，請參閱[套件管理](https://www.visualstudio.com/docs/package/nuget/publish)。</span><span class="sxs-lookup"><span data-stu-id="51a34-109">This topic covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="51a34-110">發行至 nuget.org</span><span class="sxs-lookup"><span data-stu-id="51a34-110">Publish to nuget.org</span></span>

<span data-ttu-id="51a34-111">針對 nuget.org，您必須先[註冊免費帳戶](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)或登入 (如果已註冊)：</span><span class="sxs-lookup"><span data-stu-id="51a34-111">For nuget.org, you must first [register for a free account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or sign in if already registered:</span></span>

![NuGet 註冊和登入位置](media/publish_NuGetSignIn.png)

<span data-ttu-id="51a34-113">接下來，您可以透過 nuget.org Web 入口網站上傳套件、從命令列推送至 nuget.org，或透過 Visual Studio Team Services 在 CI/CD 處理序期間發行，如下列各節中所述。</span><span class="sxs-lookup"><span data-stu-id="51a34-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line, or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="51a34-114">Web 入口網站：在 nuget.org 上使用 [上傳套件] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="51a34-114">Web portal: use the Upload Package tab on nuget.org:</span></span>

![使用 NuGet 套件管理員上傳套件](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a><span data-ttu-id="51a34-116">命令列：</span><span class="sxs-lookup"><span data-stu-id="51a34-116">Command line:</span></span>
> [!Important]
> <span data-ttu-id="51a34-117">若要將套件推送至 nuget.org，您必須使用 [nuget.exe 4.1.0 版或以上版本](https://www.nuget.org/downloads)，以實作必要 [NuGet 通訊協定](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="51a34-117">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="51a34-118">按一下您的使用者名稱，以巡覽至您的帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="51a34-118">Click on your user name to navigate to your account settings.</span></span>
2. <span data-ttu-id="51a34-119">在 [API 金鑰] 下方，按一下 [複製到剪貼簿] 以擷取 CLI 中您需要的存取金鑰：</span><span class="sxs-lookup"><span data-stu-id="51a34-119">Under **API Key**, click **copy to clipboard** to retrieve the access key you'll need in the CLI:</span></span>

    ![從帳戶設定複製 API 金鑰](media/publish_APIKey.png)

3. <span data-ttu-id="51a34-121">在命令提示字元中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="51a34-121">At a command prompt, run the following command:</span></span>

    ```
    nuget setApiKey Your-API-Key
    ```

    <span data-ttu-id="51a34-122">這會在電腦上儲存您的 API 金鑰，讓您不需要在相同電腦上重新執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="51a34-122">This stores your API key on the machine so that you need not do this step again on the same machine.</span></span>

4. <span data-ttu-id="51a34-123">使用下列命令，將套件推送至 NuGet 資源庫：</span><span class="sxs-lookup"><span data-stu-id="51a34-123">Push your package to NuGet Gallery using the command:</span></span>

    ```
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

5. <span data-ttu-id="51a34-124">設為公開之前，會掃描所有上傳至 nuget.org 的套件是否有病毒，並在發現任何病毒時予以拒絕。</span><span class="sxs-lookup"><span data-stu-id="51a34-124">Before being made public, all packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="51a34-125">也會定期掃描 nuget.org 上列出的所有套件。</span><span class="sxs-lookup"><span data-stu-id="51a34-125">All packages listed on nuget.org are also scanned periodically.</span></span>

6. <span data-ttu-id="51a34-126">在您的 nuget.org 帳戶中，按一下 [Manage my packages] (管理我的套件)，以查看您剛剛發行的套件；您也會收到確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="51a34-126">In your account on nuget.org, click **Manage my packages** to see the one that you just published; you'll also receive a confirmation email.</span></span> <span data-ttu-id="51a34-127">請注意，您的套件進行編製索引可能需要一些時間，並顯示在其他人可以找到它的搜尋結果中；在這段期間，您會在套件頁面上看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="51a34-127">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you'll see the following message on your package page:</span></span>

    ![指出套件尚未進行編製索引的訊息](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a><span data-ttu-id="51a34-129">套件驗證和編製索引</span><span class="sxs-lookup"><span data-stu-id="51a34-129">Package Validation and Indexing</span></span>

<span data-ttu-id="51a34-130">推送至 NuGet.org 的套件會歷經數次驗證。</span><span class="sxs-lookup"><span data-stu-id="51a34-130">Packages pushed to NuGet.org undergo several validations.</span></span> <span data-ttu-id="51a34-131">套件通過所有驗證檢查時，可能需要一些時間進行編製索引，並顯示在搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="51a34-131">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="51a34-132">編製索引完成之後，您會收到一封電子郵件，確認已成功發行套件。</span><span class="sxs-lookup"><span data-stu-id="51a34-132">Once indexing is complete, you'll receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="51a34-133">如果套件讓驗證檢查失敗，則會更新套件詳細資料頁面以顯示相關聯的錯誤，而且您也會收到一封電子郵件通知您有關該錯誤。</span><span class="sxs-lookup"><span data-stu-id="51a34-133">If the package fails a validation check, the package details page will update to display the associated error and you'll also receive an email notifying you about it.</span></span>

<span data-ttu-id="51a34-134">套件驗證和編製索引通常在 15 分鐘內完成。</span><span class="sxs-lookup"><span data-stu-id="51a34-134">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="51a34-135">如果套件發行所需的時間超出預期，請前往[status.nuget.org](https://status.nuget.org/)，以檢查 NuGet.org 是否發生任何中斷。</span><span class="sxs-lookup"><span data-stu-id="51a34-135">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="51a34-136">如果所有系統都可以正常運作，而且在一個小時內未成功發行套件，請登入 NuGet.org，並使用套件頁面上的 [連絡客戶支援] 連結，與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="51a34-136">If all systems are operational and the package hasn't been successfully published within an hour, please login to NuGet.org and contact us using the Contact Support link on the package page.</span></span>

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="51a34-137">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="51a34-137">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="51a34-138">如果您在持續整合/部署處理序期間，使用 Visual Studio Team Services 將套件推送至 nuget.org，則必須在 NuGet 工作中使用 nuget.exe 4.1 或以上版本。</span><span class="sxs-lookup"><span data-stu-id="51a34-138">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use nuget.exe 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="51a34-139">在[於您的組建中使用最新的 NuGet](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog) 上可以找到詳細資料。</span><span class="sxs-lookup"><span data-stu-id="51a34-139">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="51a34-140">在 nuget.org 上管理套件擁有者</span><span class="sxs-lookup"><span data-stu-id="51a34-140">Managing package owners on nuget.org</span></span>

<span data-ttu-id="51a34-141">雖然每個 NuGet 套件的 `.nuspec` 檔案都會定義套件的作者，所以 nuget.org 資源庫不會使用該中繼資料來定義擁有權。</span><span class="sxs-lookup"><span data-stu-id="51a34-141">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="51a34-142">相反地，nuget.org 會將初始擁有權指派給發行套件的人員。</span><span class="sxs-lookup"><span data-stu-id="51a34-142">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="51a34-143">這是已透過 nuget.org UI 上傳套件的已登入使用者，或已搭配使用其 API 金鑰與 `nuget SetApiKey` 或 `nuget push` 的使用者。</span><span class="sxs-lookup"><span data-stu-id="51a34-143">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="51a34-144">所有套件擁有者都具有套件的完整權限，包含新增和移除其他擁有者，以及發行更新。</span><span class="sxs-lookup"><span data-stu-id="51a34-144">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="51a34-145">若要變更套件的擁有權，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="51a34-145">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="51a34-146">使用套件之目前擁有者的帳戶來登入 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="51a34-146">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="51a34-147">按一下您的使用者名稱，並按一下 [Manage my packages] (管理我的套件)，然後按一下您想要管理的套件。</span><span class="sxs-lookup"><span data-stu-id="51a34-147">Click on your username, then on **Manage my packages**, then on the package you want to manage.</span></span>
1. <span data-ttu-id="51a34-148">按一下左側的 [管理擁有者] 連結。</span><span class="sxs-lookup"><span data-stu-id="51a34-148">Click the **Manage owners** link on the left side.</span></span>

<span data-ttu-id="51a34-149">在這裡，您有數個選項：</span><span class="sxs-lookup"><span data-stu-id="51a34-149">From here you have several options:</span></span>

1. <span data-ttu-id="51a34-150">若要新增擁有者，請輸入其 NuGet 帳戶名稱，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="51a34-150">To add an owner, enter their NuGet account name and click **Add**.</span></span> <span data-ttu-id="51a34-151">這會將含有確認連結的電子郵件傳送給這個新的共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="51a34-151">This sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="51a34-152">確認之後，該人員具有新增和移除擁有者的完整權限 </span><span class="sxs-lookup"><span data-stu-id="51a34-152">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="51a34-153">(確認之後，[管理擁有者] 頁面會指出該人員的 [等待核准])。</span><span class="sxs-lookup"><span data-stu-id="51a34-153">(Until confirmed, the **Manage owners** page indicates "pending approval" for that person).</span></span>
1. <span data-ttu-id="51a34-154">若要移除擁有者，請在 [管理擁有者] 上選取其名稱，然後按一下 [移除]。</span><span class="sxs-lookup"><span data-stu-id="51a34-154">To remove an owner, select their name on the **Manage owners** and click **Remove**.</span></span>
1. <span data-ttu-id="51a34-155">若要傳送擁有權 (擁有權變更時，或透過錯誤的帳戶發行套件之後)，只需要新增擁有者，而且在確認擁有權之後，即可從清單中將您移除。</span><span class="sxs-lookup"><span data-stu-id="51a34-155">To transfer ownership (as when ownership changes or a package was published under the wrong account), simply add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="51a34-156">若要將擁有權指派給公司或群組，請使用轉寄給適當小組成員的電子郵件別名來建立 nuget.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="51a34-156">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="51a34-157">例如，各種 Microsoft ASP.NET 套件都是由 [microsoft](http://nuget.org/profiles/microsoft) 和 [aspnet](http://nuget.org/profiles/aspnet) 帳戶共同擁有，這可簡化這類別名。</span><span class="sxs-lookup"><span data-stu-id="51a34-157">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="51a34-158">復原套件擁有權</span><span class="sxs-lookup"><span data-stu-id="51a34-158">Recovering package ownership</span></span>

<span data-ttu-id="51a34-159">套件有時可能沒有作用中的擁有者。</span><span class="sxs-lookup"><span data-stu-id="51a34-159">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="51a34-160">例如，原始擁有者可能已經離開產生套件的公司、遺失 nuget.org 認證，或資源庫中的更早 Bug 讓套件變成無擁有者。</span><span class="sxs-lookup"><span data-stu-id="51a34-160">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="51a34-161">如果您是套件的合法擁有者，而且需要重新獲得擁有權，請使用 nuget.org 上的[連絡表](https://www.nuget.org/policies/Contact)，向 NuGet 小組說明您的情況。</span><span class="sxs-lookup"><span data-stu-id="51a34-161">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="51a34-162">我們接著會遵循確認套件擁有權的程序，包含嘗試透過套件的專案 URL、Twitter、電子郵件或其他方式找出現有擁有者。</span><span class="sxs-lookup"><span data-stu-id="51a34-162">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="51a34-163">但是，如果全部都失敗，則我們可以傳送給您成為擁有者的新邀請。</span><span class="sxs-lookup"><span data-stu-id="51a34-163">But if all else fails, we can send you a new invite to become an owner.</span></span>
