---
title: "如何發行 NuGet 套件 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/05/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "如何將 NuGet 套件發行至 nuget.org 或私用摘要以及如何在 nuget.org 上管理套件擁有權的詳細指示。"
keywords: "NuGet 套件發行、發行 NuGet 套件、NuGet 套件擁有權、發行至 nuget.org、私用 NuGet 摘要"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 610b20831b17ca5c1bae07546fde6eff3e2e43cc
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2018
---
# <a name="publishing-packages"></a>發行套件

建立套件且具有 `.nukpg` 檔案之後，只要透過簡單的流程，其他開發人員就能使用此套件 (不論公開或私用)：

- 如本主題中所述，所有開發人員都可以透過 [nuget.org](https://www.nuget.org/packages/manage/upload) 全域使用公用套件。
- 私用套件僅適用於小組或組織，方法是將它們裝載在檔案共用、私用 NuGet 伺服器、[Visual Studio Team Services 套件管理](https://www.visualstudio.com/docs/package/nuget/publish)或協力廠商存放庫 (例如 myget、ProGet、Nexus Repository 和 Artifactory)。 如需其他詳細資料，請參閱[裝載套件概觀](../hosting-packages/overview.md)。

本主題涵蓋發行至 nuget.org；若要發行至 Visual Studio Team Services，請參閱[套件管理](https://www.visualstudio.com/docs/package/nuget/publish)。

## <a name="publish-to-nugetorg"></a>發行至 nuget.org

針對 nuget.org，您必須先[註冊免費帳戶](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)或登入 (如果已註冊)：

![NuGet 註冊和登入位置](media/publish_NuGetSignIn.png)

接下來，您可以透過 nuget.org Web 入口網站上傳套件、從命令列推送至 nuget.org (需要 `nuget.exe` 4.1.0+)，或透過 Visual Studio Team Services 在 CI/CD 流程期間發行，如下列各節中所述。

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Web 入口網站：使用 nuget.org 上的 [Upload Package] \(上傳套件\) 索引標籤

![使用 NuGet 套件管理員上傳套件](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a>命令列

> [!Important]
> 若要將套件推送至 nuget.org，您必須使用 [nuget.exe 4.1.0 版或以上版本](https://www.nuget.org/downloads)，以實作必要的 [NuGet 通訊協定](../api/nuget-protocols.md)。

1. 按一下您的使用者名稱，以巡覽至您的帳戶設定。
1. 在 [API 金鑰] 下方，按一下 [複製到剪貼簿] 以擷取 CLI 中您需要的存取金鑰：

    ![從帳戶設定複製 API 金鑰](media/publish_APIKey.png)

1. 在命令提示字元中，執行下列命令：

    ```cli
    nuget setApiKey Your-API-Key
    ```

    這會在電腦上儲存您的 API 金鑰，讓您不需要在相同電腦上重新執行此步驟。

1. 使用下列命令，將套件推送至 NuGet 資源庫：

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

1. 設為公開之前，會掃描所有上傳至 nuget.org 的套件是否有病毒，並在發現任何病毒時予以拒絕。 也會定期掃描 nuget.org 上列出的所有套件。

1. 在您的 nuget.org 帳戶中，按一下 [Manage my packages] \(管理我的套件\)，以查看您剛剛發行的套件；您也會收到確認電子郵件。 請注意，您的套件進行編製索引可能需要一些時間，並顯示在其他人可以找到它的搜尋結果中；在這段期間，您會在套件頁面上看到下列訊息：

    ![指出套件尚未進行編製索引的訊息](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a>套件驗證和編製索引

推送至 NuGet.org 的套件會歷經數次驗證。 套件通過所有驗證檢查時，可能需要一些時間進行編製索引，並顯示在搜尋結果中。 編製索引完成之後，您會收到一封電子郵件，確認已成功發行套件。 如果套件讓驗證檢查失敗，則會更新套件詳細資料頁面以顯示相關聯的錯誤，而且您也會收到一封電子郵件通知您有關該錯誤。

套件驗證和編製索引通常在 15 分鐘內完成。 如果套件發行所需的時間超出預期，請前往[status.nuget.org](https://status.nuget.org/)，以檢查 NuGet.org 是否發生任何中斷。 如果所有系統都可以正常運作，而且在一個小時內未成功發行套件，請登入 NuGet.org，並使用套件頁面上的 [連絡客戶支援] 連結，與我們連絡。

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

如果您在持續整合/部署處理序期間，使用 Visual Studio Team Services 將套件推送至 nuget.org，則必須在 NuGet 工作中使用 `nuget.exe` 4.1 或以上版本。 在[於您的組建中使用最新的 NuGet](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog) 上可以找到詳細資料。

## <a name="managing-package-owners-on-nugetorg"></a>在 nuget.org 上管理套件擁有者

雖然每個 NuGet 套件的 `.nuspec` 檔案都會定義套件的作者，所以 nuget.org 資源庫不會使用該中繼資料來定義擁有權。 相反地，nuget.org 會將初始擁有權指派給發行套件的人員。 這是已透過 nuget.org UI 上傳套件的已登入使用者，或已搭配使用其 API 金鑰與 `nuget SetApiKey` 或 `nuget push` 的使用者。

所有套件擁有者都具有套件的完整權限，包含新增和移除其他擁有者，以及發行更新。

若要變更套件的擁有權，請執行下列動作：

1. 使用套件之目前擁有者的帳戶來登入 nuget.org。
1. 按一下您的使用者名稱，並按一下 [Manage my packages] \(管理我的套件)，然後按一下您想要管理的套件。
1. 按一下左側的 [管理擁有者] 連結。

在這裡，您有數個選項：

1. 若要新增擁有者，請輸入其 NuGet 帳戶名稱，然後按一下 [新增]。 這會將含有確認連結的電子郵件傳送給這個新的共同擁有者。 確認之後，該人員具有新增和移除擁有者的完整權限  (確認之後，[管理擁有者] 頁面會指出該人員的 [等待核准])。
1. 若要移除擁有者，請在 [管理擁有者] 上選取其名稱，然後按一下 [移除]。
1. 若要傳送擁有權 (擁有權變更時，或透過錯誤的帳戶發行套件之後)，只需要新增擁有者，而且在確認擁有權之後，即可從清單中將您移除。

若要將擁有權指派給公司或群組，請使用轉寄給適當小組成員的電子郵件別名來建立 nuget.org 帳戶。 例如，各種 Microsoft ASP.NET 套件都是由 [microsoft](http://nuget.org/profiles/microsoft) 和 [aspnet](http://nuget.org/profiles/aspnet) 帳戶共同擁有，這可簡化這類別名。

### <a name="recovering-package-ownership"></a>復原套件擁有權

套件有時可能沒有作用中的擁有者。 例如，原始擁有者可能已經離開產生套件的公司、遺失 nuget.org 認證，或資源庫中的更早 Bug 讓套件變成無擁有者。

如果您是套件的合法擁有者，而且需要重新獲得擁有權，請使用 nuget.org 上的[連絡表](https://www.nuget.org/policies/Contact)，向 NuGet 小組說明您的情況。 我們接著會遵循確認套件擁有權的程序，包含嘗試透過套件的專案 URL、Twitter、電子郵件或其他方式找出現有擁有者。 但是，如果全部都失敗，則我們可以傳送給您成為擁有者的新邀請。
