---
title: 如何發佈 NuGet 套件
description: 如何將 NuGet 套件發行至 nuget.org 或私用摘要以及如何在 nuget.org 上管理套件擁有權的詳細指示。
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 02c6c8f3018bfd063c2d16a10381f88b54cac840
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429021"
---
# <a name="publishing-packages"></a>發行套件

建立套件且具有 `.nupkg` 檔案之後，只要透過簡單的流程，其他開發人員就能使用此套件 (不論公開或私用)：

- 如本文中所述，所有開發人員都可以透過 [nuget.org](https://www.nuget.org/packages/manage/upload) 全域使用公用套件 (需要 NuGet 4.1.0+)。
- 私用套件僅適用於小組或組織，方法是將它們裝載在檔案共用、私用 NuGet 伺服器、[Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) 協力廠商存放庫 (例如 myget、ProGet、Nexus Repository 和 Artifactory)。 如需其他詳細資料，請參閱[裝載套件概觀](../hosting-packages/overview.md)。

此文章涵蓋發行至 nuget.org 的方法；若要發行至 Azure Artifacts，請參閱[套件管理](https://www.visualstudio.com/docs/package/nuget/publish)。

## <a name="publish-to-nugetorg"></a>發行至 nuget.org

針對 nuget.org，您必須使用 Microsoft 帳戶登入，系統會要求您向 nuget.org 註冊該帳戶。您也可以使用以較舊版本的入口網站建立的 nuget.org 帳戶來登入。

![NuGet 登入位置](media/publish_NuGetSignIn.png)

接下來，您可以透過 nuget.org Web 入口網站上傳套件、從命令列推送至 nuget.org (需要 `nuget.exe` 4.1.0+)，或透過 Azure DevOps Services 在 CI/CD 流程期間發行，如下列各節中所述。

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Web 入口網站：使用 nuget.org 上的 [Upload Package] \(上傳套件\) 索引標籤

1. 在 nuget.org 的上方功能表中選取 [上傳]，並瀏覽至套件位置。

    ![在 nuget.org 上上傳套件](media/publish_UploadYourPackage.PNG)

1. nuget.org 會告訴您該套件名稱是否可用。 如果不可使用，請在您專案中變更套件識別碼、重建，並再次嘗試上傳。

1. 如果套件名稱可用，nuget.org 會開啟 [確認] 區段，您可在其中檢閱套件資訊清單的中繼資料。 若要變更任何中繼資料，請編輯您的專案 (專案檔或 `.nuspec` 檔案)、重建、重新建立套件，然後再次上傳。

1. 在 [匯入文件] 底下，您可以貼上 Markdown、使用 URL 指向您的文件，或上傳文件檔案。

1. 當所有資訊準備就緒時，請選取 [提交] 按鈕

### <a name="command-line"></a>命令列

若要將套件推送至 nuget.org，您必須使用 [nuget.exe 4.1.0 版或以上版本](https://www.nuget.org/downloads)，以實作必要的 [NuGet 通訊協定](../api/nuget-protocols.md)。 您也需要 API 金鑰，這是在 nuget.org 上建立的。

#### <a name="create-api-keys"></a>建立 API 金鑰

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>使用 dotnet nuget push 發行

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>使用 nuget push 發行

1. 在命令提示字元中執行下列命令，將 `<your_API_key>` 取代為從 nuget.org 取得的金鑰：

    ```cli
    nuget setApiKey <your_API_key>
    ```

    此命令會將您的 API 金鑰儲存在 NuGet 設定中，如此您就不需要在同一部電腦上再次重複此步驟。

    > [!NOTE]
    > API 金鑰不會用來向私人摘要進行驗證。 請參閱[`nuget sources` 命令](../reference/cli-reference/cli-ref-sources.md)，以管理用來驗證來源的認證。
    > 您可以從個別的 NuGet 伺服器取得 API 金鑰。 若要建立和管理 nuget.org 的 APIKeys，請參閱[發佈-api 金鑰](../quickstart/includes/publish-api-key.md)

1. 使用下列命令，將套件推送至 NuGet 資源庫：

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>發行已簽署的套件

若要提交已簽署的套件，必須先[註冊用來簽署套件的憑證](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg)。 

> [!Warning]
> nuget.org 會拒絕不符合[簽署的套件需求](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)的套件。

### <a name="package-validation-and-indexing"></a>套件驗證和編製索引

推送至 nuget.org 的套件會歷經數次驗證，例如病毒檢查。 (nuget.org 上的所有套件都會定期掃描)。

套件通過所有驗證檢查時，可能需要一些時間進行編製索引，並顯示在搜尋結果中。 編製索引完成之後，您會收到一封電子郵件，確認已成功發行套件。 如果套件讓驗證檢查失敗，則會更新套件詳細資料頁面以顯示相關聯的錯誤，而且您也會收到一封電子郵件通知您有關該錯誤。

套件驗證和編製索引通常在 15 分鐘內完成。 如果套件發佈所需的時間超出預期，請前往 [status.nuget.org](https://status.nuget.org/)，以檢查 nuget.org 是否發生任何中斷。 如果所有系統都可以正常運作，但未在一個小時內成功發佈套件，請登入 nuget.org，並使用套件頁面上的 [連絡客戶支援] 連結與我們連絡。

若要查看封裝的狀態，請在 nuget.org 的帳戶名稱底下選取 [**管理套件**]。驗證完成時，您會收到確認電子郵件。

請注意，您的套件進行編製索引可能需要一些時間，並顯示在其他人可以找到它的搜尋結果中；在這段期間，您會在套件頁面上看到下列訊息：

![指出套件尚未發行的訊息](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Services (CI/CD)

如果您在持續整合/部署處理序期間，使用 Azure DevOps Services 將套件推送至 nuget.org，則必須在 NuGet 工作中使用 `nuget.exe` 4.1 或以上版本。 在[於您的組建中使用最新的 NuGet](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog) 上可以找到詳細資料。

## <a name="managing-package-owners-on-nugetorg"></a>在 nuget.org 上管理套件擁有者

雖然每個 NuGet 套件的 `.nuspec` 檔案都會定義套件的作者，所以 nuget.org 資源庫不會使用該中繼資料來定義擁有權。 相反地，nuget.org 會將初始擁有權指派給發行套件的人員。 這是已透過 nuget.org UI 上傳套件的已登入使用者，或已搭配使用其 API 金鑰與 `nuget SetApiKey` 或 `nuget push` 的使用者。

所有套件擁有者都具有套件的完整權限，包含新增和移除其他擁有者，以及發行更新。

若要變更套件的擁有權，請執行下列動作：

1. 使用套件之目前擁有者的帳戶來登入 nuget.org。
1. 選取您的帳戶名稱，選取 [管理套件]，然後展開 [已發行的套件]。
1. 選取您要管理的套件，然後在右側選取 [管理擁有者]。

在這裡，您有數個選項：

1. 移除 [目前擁有者] 底下所列的所有擁有者。
1. 在 [新增擁有者]下，透過輸入其使用者名稱、訊息，並選取 [新增] 來新增擁有者。 此動作會將含有確認連結的電子郵件傳送給這個新的共同擁有者。 確認之後，該人員具有新增和移除擁有者的完整權限 (確認之後，[目前擁有者] 區段會指出該人員等待核准。)
1. 若要移轉擁有權 (擁有權變更時，或透過錯誤的帳戶發行套件之後)，請新增擁有者，而且在確認擁有權之後，即可從清單中將您移除。

若要將擁有權指派給公司或群組，請使用轉寄給適當小組成員的電子郵件別名來建立 nuget.org 帳戶。 例如，各種 Microsoft ASP.NET 套件都是由 [microsoft](https://nuget.org/profiles/microsoft) 和 [aspnet](https://nuget.org/profiles/aspnet) 帳戶共同擁有，這可簡化這類別名。

### <a name="recovering-package-ownership"></a>復原套件擁有權

套件有時可能沒有作用中的擁有者。 例如，原始擁有者可能已經離開產生套件的公司、遺失 nuget.org 認證，或資源庫中的更早 Bug 讓套件變成無擁有者。

如果您是套件的合法擁有者，而且需要重新獲得擁有權，請使用 nuget.org 上的[連絡表](https://www.nuget.org/policies/Contact)，向 NuGet 小組說明您的情況。 我們接著會遵循確認套件擁有權的程序，包含嘗試透過套件的專案 URL、Twitter、電子郵件或其他方式找出現有擁有者。 但是，如果全部都失敗，則我們可以傳送給您成為擁有者的新邀請。
