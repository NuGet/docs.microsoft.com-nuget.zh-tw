---
title: 簽署 NuGet 套件
description: 說明已簽署套件如何用於啟用內容完整性驗證。
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: c0622520a325000d5fcb8fb884cb509ee4b641f4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901898"
---
# <a name="signing-nuget-packages"></a>簽署 NuGet 套件

已簽署套件允許內容完整性驗證檢查，其提供防止內容竄改的保護。 套件簽章也作為套件實際來源和消費者加強套件真確性的真實單一來源。 此指南會假設您已[建立套件](creating-a-package.md)。

## <a name="get-a-code-signing-certificate"></a>取得程式碼簽署憑證

您可以從公開憑證授權單位單位（例如 [DigiCert](https://www.digicert.com/code-signing/)、 [Global Sign](https://www.globalsign.com/en/code-signing-certificate/)、 [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)、 [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)等）取得有效的憑證。您可以從取得 Windows 信任之憑證授權單位單位的完整清單 [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list) 。

您可以基於測試目的使用自動發行的憑證。 不過，NuGet.org 不接受使用自我發行的憑證簽署的套件。深入瞭解如何 [建立測試憑證](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>匯出憑證檔案

* 您可以使用憑證匯出精靈將現有的憑證匯出為二進位 DER 格式。

  ![憑證匯出精靈](../reference/media/CertificateExportWizard.png)

* 您也可以使用 [Export-Certificate PowerShell 命令](/powershell/module/pkiclient/export-certificate)匯出認證。

## <a name="sign-the-package"></a>簽署套件

> [!note]
> 需要 nuget.exe 4.6.0 或更新版本。 即將推出 dotnet.exe 支援- [#7939](https://github.com/NuGet/Home/issues/7939)

使用 [nuget sign](../reference/cli-reference/cli-ref-sign.md) 簽署套件：

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> 憑證提供者通常也會提供時間戳記伺服器 URL，可用於上方顯示的 `Timestamper` 選擇性引數。 請洽詢提供者的文件及 (或) 支援人員，以取得該服務 URL。

* 您可以使用憑證存放區中可用的憑證，或使用檔案中的憑證。 請參閱 [nuget sign](../reference/cli-reference/cli-ref-sign.md) 的 CLI 參考。
* 簽署的套件應包含時間戳記，以確定簽署憑證過期時，簽章仍保持有效。 若不包含時間戳記，則簽署作業會產生[警告](../reference/errors-and-warnings/NU3002.md)。
* 您可以使用 [nuget verify](../reference/cli-reference/cli-ref-verify.md) 查看指定套件的簽章詳細資料。

## <a name="register-the-certificate-on-nugetorg"></a>在 NuGet.org 上註冊憑證

若要發佈已簽署的封裝，您必須先向 NuGet.org 註冊憑證。您需要憑證作為 `.cer` 二進位 DER 格式的檔案。

1. [登入](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) NuGet.org。
1. 前往 `Account settings` (若您想要使用組織帳戶來註冊憑證，則前往 `Manage Organization` **>** `Edit Organization`)。
1. 展開 `Certificates` 區段並選取 `Register new`。
1. 瀏覽並選取稍早匯出的憑證檔案。
  ![已註冊憑證](../reference/media/registered-certs.png)

**注意**
* 一位使用者可以提交多個憑證，且多位使用者可以註冊同一個憑證。
* 使用者在註冊憑證後，往後提交的所有套件都 **必須** 使用其中一項憑證簽署。 請參閱[在 NuGet.org 上管理您套件的簽署需求](#manage-signing-requirements-for-your-package-on-nugetorg)
* 使用者也可以從帳戶移除已註冊憑證。 移除憑證後，使用該憑證簽署的新套件將會提交失敗。 現有的套件則不會受影響。

## <a name="publish-the-package"></a>發行套件

您現在已準備好將封裝發佈至 NuGet.org。請參閱 [發行封裝](../nuget-org/Publish-a-package.md)。

## <a name="create-a-test-certificate"></a>建立測試憑證

您可以基於測試目的使用自動發行的憑證。 若要建立自動發行的憑證，請使用 [New-SelfSignedCertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate)。

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

此命令會建立測試憑證，可在目前使用者的個人憑證存放區中使用。 您可以透過執行 `certmgr.msc` 來開啟憑證存放區，以查看新建立的憑證。

> [!Warning]
> NuGet.org 不接受使用自動發行憑證簽署的套件。

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>在 NuGet.org 上管理您套件的簽署需求
1. [登入](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) NuGet.org。

1. 前往 `Manage Packages` 
   ![設定套件簽署者](../reference/media/configure-package-signers.png)

* 若您為套件的唯一擁有者，那麼您就是必要的簽署者，這表示您可以使用任何已註冊憑證，來簽署自己的套件並發佈至 NuGet.org。

* 根據預設，若套件擁有多位擁有者，則 [任何] 擁有者的憑證都可以用來簽署套件。 作為套件的共同擁有者，您可以將 [任何] 覆寫為自己或其他共同擁有者，使其成為必要簽署者。 如果您讓不具任何已註冊憑證的人員成為擁有者，會允許未簽署的套件。 

* 同樣地，若已為套件選取預設的 [任何] 選項，而該套件的其中一位擁有者具有已註冊憑證，但另一位則不具任何已註冊憑證，則不論是簽章由其中一位擁有者註冊的已簽署套件，或是未簽署的套件，NuGet.org 都會接受 (因為其中一位擁有者不具任何已註冊憑證)。

## <a name="related-articles"></a>相關文章

- [管理套件的信任界限](../consume-packages/installing-signed-packages.md)
- [簽署的套件參考](../reference/Signed-Packages-Reference.md)
