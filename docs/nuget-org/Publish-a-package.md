---
title: 如何發佈 NuGet 套件
description: 如何將 NuGet 套件發行至 nuget.org 或私用摘要以及如何在 nuget.org 上管理套件擁有權的詳細指示。
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 937d051ff6dc49e3204f7d0cb22c4f29b99a2a7d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610605"
---
# <a name="publishing-packages"></a><span data-ttu-id="9ff40-103">發行套件</span><span class="sxs-lookup"><span data-stu-id="9ff40-103">Publishing packages</span></span>

<span data-ttu-id="9ff40-104">建立套件且具有 `.nupkg` 檔案之後，只要透過簡單的流程，其他開發人員就能使用此套件 (不論公開或私用)：</span><span class="sxs-lookup"><span data-stu-id="9ff40-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="9ff40-105">如本文中所述，所有開發人員都可以透過 [nuget.org](https://www.nuget.org/packages/manage/upload) 全域使用公用套件 (需要 NuGet 4.1.0+)。</span><span class="sxs-lookup"><span data-stu-id="9ff40-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="9ff40-106">私用套件僅適用於小組或組織，方法是將它們裝載在檔案共用、私用 NuGet 伺服器、[Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) 協力廠商存放庫 (例如 myget、ProGet、Nexus Repository 和 Artifactory)。</span><span class="sxs-lookup"><span data-stu-id="9ff40-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="9ff40-107">如需其他詳細資料，請參閱[裝載套件概觀](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9ff40-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="9ff40-108">此文章涵蓋發行至 nuget.org 的方法；若要發行至 Azure Artifacts，請參閱[套件管理](https://www.visualstudio.com/docs/package/nuget/publish)。</span><span class="sxs-lookup"><span data-stu-id="9ff40-108">This article covers publishing to nuget.org; for publishing to Azure Artifacts, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="9ff40-109">發行至 nuget.org</span><span class="sxs-lookup"><span data-stu-id="9ff40-109">Publish to nuget.org</span></span>

<span data-ttu-id="9ff40-110">針對 nuget.org，您必須使用 Microsoft 帳戶登入，系統會要求您向 nuget.org 註冊該帳戶。您也可以使用以較舊版本的入口網站建立的 nuget.org 帳戶來登入。</span><span class="sxs-lookup"><span data-stu-id="9ff40-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![NuGet 登入位置](media/publish_NuGetSignIn.png)

<span data-ttu-id="9ff40-112">接下來，您可以透過 nuget.org Web 入口網站上傳套件、從命令列推送至 nuget.org (需要 `nuget.exe` 4.1.0+)，或透過 Azure DevOps Services 在 CI/CD 流程期間發行，如下列各節中所述。</span><span class="sxs-lookup"><span data-stu-id="9ff40-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Azure DevOps Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="9ff40-113">Web 入口網站：使用 nuget.org 上的 [Upload Package] \(上傳套件\) 索引標籤</span><span class="sxs-lookup"><span data-stu-id="9ff40-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="9ff40-114">在 nuget.org 的上方功能表中選取 [上傳]，並瀏覽至套件位置。</span><span class="sxs-lookup"><span data-stu-id="9ff40-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![在 nuget.org 上上傳套件](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="9ff40-116">nuget.org 會告訴您該套件名稱是否可用。</span><span class="sxs-lookup"><span data-stu-id="9ff40-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="9ff40-117">如果不可使用，請在您專案中變更套件識別碼、重建，並再次嘗試上傳。</span><span class="sxs-lookup"><span data-stu-id="9ff40-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="9ff40-118">如果套件名稱可用，nuget.org 會開啟 [確認] 區段，您可在其中檢閱套件資訊清單的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9ff40-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="9ff40-119">若要變更任何中繼資料，請編輯您的專案 (專案檔或 `.nuspec` 檔案)、重建、重新建立套件，然後再次上傳。</span><span class="sxs-lookup"><span data-stu-id="9ff40-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="9ff40-120">在 [匯入文件] 底下，您可以貼上 Markdown、使用 URL 指向您的文件，或上傳文件檔案。</span><span class="sxs-lookup"><span data-stu-id="9ff40-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="9ff40-121">當所有資訊準備就緒時，請選取 [提交] 按鈕</span><span class="sxs-lookup"><span data-stu-id="9ff40-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="9ff40-122">命令列</span><span class="sxs-lookup"><span data-stu-id="9ff40-122">Command line</span></span>

<span data-ttu-id="9ff40-123">若要將套件推送至 nuget.org，您必須使用 [nuget.exe 4.1.0 版或以上版本](https://www.nuget.org/downloads)，以實作必要的 [NuGet 通訊協定](../api/nuget-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="9ff40-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="9ff40-124">您也需要 API 金鑰，這是在 nuget.org 上建立的。</span><span class="sxs-lookup"><span data-stu-id="9ff40-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="9ff40-125">建立 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="9ff40-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="9ff40-126">使用 dotnet nuget push 發行</span><span class="sxs-lookup"><span data-stu-id="9ff40-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="9ff40-127">使用 nuget push 發行</span><span class="sxs-lookup"><span data-stu-id="9ff40-127">Publish with nuget push</span></span>

1. <span data-ttu-id="9ff40-128">在命令提示字元中執行下列命令，將 `<your_API_key>` 取代為從 nuget.org 取得的金鑰：</span><span class="sxs-lookup"><span data-stu-id="9ff40-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="9ff40-129">此命令會將您的 API 金鑰儲存在 NuGet 設定中，如此您就不需要在同一部電腦上再次重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="9ff40-129">This command stores your API key in your NuGet configuration so that you don't need to repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="9ff40-130">使用下列命令，將套件推送至 NuGet 資源庫：</span><span class="sxs-lookup"><span data-stu-id="9ff40-130">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="9ff40-131">發行已簽署的套件</span><span class="sxs-lookup"><span data-stu-id="9ff40-131">Publish signed packages</span></span>

<span data-ttu-id="9ff40-132">若要提交已簽署的套件，必須先[註冊用來簽署套件的憑證](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="9ff40-132">To submit signed packages, you must first [register the certificate](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="9ff40-133">nuget.org 會拒絕不符合[簽署的套件需求](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)的套件。</span><span class="sxs-lookup"><span data-stu-id="9ff40-133">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="9ff40-134">套件驗證和編製索引</span><span class="sxs-lookup"><span data-stu-id="9ff40-134">Package validation and indexing</span></span>

<span data-ttu-id="9ff40-135">推送至 nuget.org 的套件會歷經數次驗證，例如病毒檢查。</span><span class="sxs-lookup"><span data-stu-id="9ff40-135">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="9ff40-136">(nuget.org 上的所有套件都會定期掃描)。</span><span class="sxs-lookup"><span data-stu-id="9ff40-136">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="9ff40-137">套件通過所有驗證檢查時，可能需要一些時間進行編製索引，並顯示在搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="9ff40-137">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="9ff40-138">編製索引完成之後，您會收到一封電子郵件，確認已成功發行套件。</span><span class="sxs-lookup"><span data-stu-id="9ff40-138">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="9ff40-139">如果套件讓驗證檢查失敗，則會更新套件詳細資料頁面以顯示相關聯的錯誤，而且您也會收到一封電子郵件通知您有關該錯誤。</span><span class="sxs-lookup"><span data-stu-id="9ff40-139">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="9ff40-140">套件驗證和編製索引通常在 15 分鐘內完成。</span><span class="sxs-lookup"><span data-stu-id="9ff40-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="9ff40-141">如果套件發佈所需的時間超出預期，請前往 [status.nuget.org](https://status.nuget.org/)，以檢查 nuget.org 是否發生任何中斷。</span><span class="sxs-lookup"><span data-stu-id="9ff40-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="9ff40-142">如果所有系統都可以正常運作，但未在一個小時內成功發佈套件，請登入 nuget.org，並使用套件頁面上的 [連絡客戶支援] 連結與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="9ff40-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="9ff40-143">若要查看封裝的狀態，請在 nuget.org 的帳戶名稱底下選取 [**管理套件**]。驗證完成時，您會收到確認電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9ff40-143">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="9ff40-144">請注意，您的套件進行編製索引可能需要一些時間，並顯示在其他人可以找到它的搜尋結果中；在這段期間，您會在套件頁面上看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="9ff40-144">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![指出套件尚未發行的訊息](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a><span data-ttu-id="9ff40-146">Azure DevOps Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="9ff40-146">Azure DevOps Services (CI/CD)</span></span>

<span data-ttu-id="9ff40-147">如果您在持續整合/部署處理序期間，使用 Azure DevOps Services 將套件推送至 nuget.org，則必須在 NuGet 工作中使用 `nuget.exe` 4.1 或以上版本。</span><span class="sxs-lookup"><span data-stu-id="9ff40-147">If you push packages to nuget.org using Azure DevOps Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="9ff40-148">在[於您的組建中使用最新的 NuGet](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog) 上可以找到詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9ff40-148">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="9ff40-149">在 nuget.org 上管理套件擁有者</span><span class="sxs-lookup"><span data-stu-id="9ff40-149">Managing package owners on nuget.org</span></span>

<span data-ttu-id="9ff40-150">雖然每個 NuGet 套件的 `.nuspec` 檔案都會定義套件的作者，所以 nuget.org 資源庫不會使用該中繼資料來定義擁有權。</span><span class="sxs-lookup"><span data-stu-id="9ff40-150">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="9ff40-151">相反地，nuget.org 會將初始擁有權指派給發行套件的人員。</span><span class="sxs-lookup"><span data-stu-id="9ff40-151">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="9ff40-152">這是已透過 nuget.org UI 上傳套件的已登入使用者，或已搭配使用其 API 金鑰與 `nuget SetApiKey` 或 `nuget push` 的使用者。</span><span class="sxs-lookup"><span data-stu-id="9ff40-152">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="9ff40-153">所有套件擁有者都具有套件的完整權限，包含新增和移除其他擁有者，以及發行更新。</span><span class="sxs-lookup"><span data-stu-id="9ff40-153">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="9ff40-154">若要變更套件的擁有權，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9ff40-154">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="9ff40-155">使用套件之目前擁有者的帳戶來登入 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="9ff40-155">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="9ff40-156">選取您的帳戶名稱，選取 [管理套件]，然後展開 [已發行的套件]。</span><span class="sxs-lookup"><span data-stu-id="9ff40-156">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="9ff40-157">選取您要管理的套件，然後在右側選取 [管理擁有者]。</span><span class="sxs-lookup"><span data-stu-id="9ff40-157">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="9ff40-158">在這裡，您有數個選項：</span><span class="sxs-lookup"><span data-stu-id="9ff40-158">From here you have several options:</span></span>

1. <span data-ttu-id="9ff40-159">移除 [目前擁有者] 底下所列的所有擁有者。</span><span class="sxs-lookup"><span data-stu-id="9ff40-159">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="9ff40-160">在 [新增擁有者]下，透過輸入其使用者名稱、訊息，並選取 [新增] 來新增擁有者。</span><span class="sxs-lookup"><span data-stu-id="9ff40-160">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="9ff40-161">此動作會將含有確認連結的電子郵件傳送給這個新的共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="9ff40-161">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="9ff40-162">確認之後，該人員具有新增和移除擁有者的完整權限</span><span class="sxs-lookup"><span data-stu-id="9ff40-162">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="9ff40-163">(確認之後，[目前擁有者] 區段會指出該人員等待核准。)</span><span class="sxs-lookup"><span data-stu-id="9ff40-163">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="9ff40-164">若要移轉擁有權 (擁有權變更時，或透過錯誤的帳戶發行套件之後)，請新增擁有者，而且在確認擁有權之後，即可從清單中將您移除。</span><span class="sxs-lookup"><span data-stu-id="9ff40-164">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="9ff40-165">若要將擁有權指派給公司或群組，請使用轉寄給適當小組成員的電子郵件別名來建立 nuget.org 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ff40-165">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="9ff40-166">例如，各種 Microsoft ASP.NET 套件都是由 [microsoft](https://nuget.org/profiles/microsoft) 和 [aspnet](https://nuget.org/profiles/aspnet) 帳戶共同擁有，這可簡化這類別名。</span><span class="sxs-lookup"><span data-stu-id="9ff40-166">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](https://nuget.org/profiles/microsoft) and [aspnet](https://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="9ff40-167">復原套件擁有權</span><span class="sxs-lookup"><span data-stu-id="9ff40-167">Recovering package ownership</span></span>

<span data-ttu-id="9ff40-168">套件有時可能沒有作用中的擁有者。</span><span class="sxs-lookup"><span data-stu-id="9ff40-168">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="9ff40-169">例如，原始擁有者可能已經離開產生套件的公司、遺失 nuget.org 認證，或資源庫中的更早 Bug 讓套件變成無擁有者。</span><span class="sxs-lookup"><span data-stu-id="9ff40-169">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="9ff40-170">如果您是套件的合法擁有者，而且需要重新獲得擁有權，請使用 nuget.org 上的[連絡表](https://www.nuget.org/policies/Contact)，向 NuGet 小組說明您的情況。</span><span class="sxs-lookup"><span data-stu-id="9ff40-170">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="9ff40-171">我們接著會遵循確認套件擁有權的程序，包含嘗試透過套件的專案 URL、Twitter、電子郵件或其他方式找出現有擁有者。</span><span class="sxs-lookup"><span data-stu-id="9ff40-171">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="9ff40-172">但是，如果全部都失敗，則我們可以傳送給您成為擁有者的新邀請。</span><span class="sxs-lookup"><span data-stu-id="9ff40-172">But if all else fails, we can send you a new invite to become an owner.</span></span>
