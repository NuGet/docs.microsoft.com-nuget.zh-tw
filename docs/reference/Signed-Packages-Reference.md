---
title: 已簽署的套件
description: NuGet 封裝簽章需求。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c36db9486ad787f19430c75fc38a2e9dd8ba6e37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550417"
---
# <a name="signed-packages"></a>已簽署的套件

*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 版及更新版本*

NuGet 套件可以包含數位簽章可防止遭竄改的內容。 此簽章會產生來自 X.509 憑證，也將真實性證明，加上實際的套件來源。

已簽署的套件會提供最強的端對端驗證。 有兩種不同的 NuGet 簽章：
- **撰寫簽章**。 作者簽章可保證，封裝不之後已修改作者已登入的封裝，不論其儲存機制，或傳輸封裝傳遞的方法。 此外，作者簽署的套件提供額外的驗證機制以 nuget.org 發行管線，因為必須事先註冊簽署憑證。 如需詳細資訊，請參閱 <<c0> [ 登錄憑證](#register-certificate-on-nugetorg)。
- **存放庫簽章**。 存放庫簽章提供完整性保證**所有**套件存放庫中，不論它們是作者帶正負號或不是，即使這些套件會取自原始它們所在的存放庫不同的位置帶正負號。   

如需建立作者已簽署的封裝的詳細資訊，請參閱 <<c0> [ 簽署封裝](../create-packages/Sign-a-package.md)並[nuget 登命令](../tools/cli-ref-sign.md)。

> [!Important]
> 目前支援封裝簽章，只有在 Windows 上使用 nuget.exe 時。 只有在 Windows 上使用 nuget.exe 或 Visual Studio 時，目前支援驗證的已簽署的套件。

## <a name="certificate-requirements"></a>憑證需求

封裝簽章需要程式碼簽署憑證，這是一種特別有效的憑證`id-kp-codeSigning`目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證必須具有 RSA 公用金鑰長度為 2048 位元或更高版本。

## <a name="get-a-code-signing-certificate"></a>取得程式碼簽署憑證

有效的憑證可能取自的公開憑證授權單位，例如：

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [全域符號](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

透過 Windows 受信任的憑證授權單位的完整清單可以取自[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。

## <a name="create-a-test-certificate"></a>建立測試憑證

基於測試目的，您可以使用自行發出的憑證。 若要建立自我發行的憑證，請使用[New-selfsignedcertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate.md)。

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

此命令會建立在目前使用者的個人憑證存放區中可用的測試憑證。 您可以開啟憑證存放區執行`certmgr.msc`以查看新建立的憑證。

> [!Warning]
> nuget.org 不接受封裝以自行發出的憑證簽署。

## <a name="timestamp-requirements"></a>時間戳記的需求

已簽署的套件應該包含 RFC 3161 時間戳記，以確保套件簽署憑證的有效期間以外的簽章有效性。 用來登入時間戳記的憑證必須適用於`id-kp-timeStamping`目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證必須具有 RSA 公用金鑰長度為 2048 位元或更高版本。

其他技術詳細資料可在[封裝簽章的技術規格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。

## <a name="signature-requirements-on-nugetorg"></a>在 nuget.org 上的簽章需求

nuget.org 具有接受已簽署的封裝的額外需求：

- 主要的簽章必須是作者簽章。
- 主要的簽章必須有單一有效的時間戳記。
- 作者簽章和其時間戳記簽章的 X.509 憑證：
  - 必須有 RSA 公開金鑰 2048 位元或更高。
  - 必須在每次目前的 UTC 時間的 nuget.org 上的 封裝驗證其有效期間內。
  - 必須鏈結至信任預設會在 Windows 上的受信任的根授權單位。 使用自我發行的憑證簽署的封裝會遭到拒絕。
  - 必須是有效的目的： 
    - 作者簽署憑證必須是有效簽署程式碼。
    - 時間戳記憑證必須是有效的時間戳記。
  - 必須不會撤銷在簽入時間。 （這可能不是 knowable 在提交時，所以 nuget.org 定期重新檢查撤銷狀態）。

## <a name="register-certificate-on-nugetorg"></a>在 nuget.org 上註冊憑證

若要提交已簽署的封裝，您必須先使用 nuget.org 中註冊憑證。您必須為憑證`.cer`DER 的二進位格式的檔案。 您可以使用 憑證匯出精靈，為二進位 DER 格式匯出現有的憑證。

![憑證匯出精靈](media/CertificateExportWizard.png)

進階的使用者可以使用憑證匯出[匯出憑證的 PowerShell 命令](/powershell/module/pkiclient/export-certificate.md)。

若要向 nuget.org 中的憑證，請移至`Certificates`上一節`Account settings`網頁 （或組織的 [設定] 頁面），然後選取`Register new certificate`。

![已登錄的憑證](media/registered-certs.png)

> [!Tip]
> 一位使用者可以提交多個使用者，則可以註冊多個憑證和相同的憑證。

使用者一旦具有憑證註冊，所有未來的套件提交**必須**使用其中一個憑證來簽署。

使用者也可以從帳戶移除已註冊的憑證。 一旦移除憑證，使用該憑證簽署的封裝將會在提交失敗。 現有的封裝不會受到影響。

## <a name="configure-package-signing-requirements"></a>設定套件簽署需求

如果您是套件的唯一擁有者，您就會是所需的簽署人。 也就是說，您可以使用任何已註冊的憑證來簽署您的套件，並提交至 nuget.org。

如果封裝有多個擁有者，根據預設，[任何] 擁有者的憑證可用來簽署封裝。 為封裝的共同擁有者，您可以覆寫 「 任何 」 與自己或任何其他共同擁有者設為所需的簽署人。 如果您的擁有者並沒有任何已註冊的憑證，則不允許未簽署的封裝。 

同樣地，如果選取 [任何] 選項的其中一位擁有者已註冊的憑證封裝與另一個擁有者的預設值並沒有任何已註冊的憑證，然後 nuget.org 接受已簽署的封裝註冊的其中一個擁有者的簽章或不帶正負號封裝 （因為擁有者並沒有任何已註冊的憑證）。

![設定套件簽署](media/configure-package-signers.png)
