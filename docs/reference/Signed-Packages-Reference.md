---
title: 已簽署的套件
description: NuGet 封裝簽章需求。
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2018
---
# <a name="signed-packages"></a>簽署的封裝

*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 和更新版本*

NuGet 封裝可以包含數位簽章可防止遭竄改的內容。 此簽章會產生來自 X.509 憑證，也會增加實際的來源封裝的真實性證明。

簽署的封裝提供最強的端對端驗證。 作者簽章可確保封裝不已修改的作者從不論簽署封裝之後, 的儲存機制或什麼傳輸的方法傳送封裝。

此外，作者簽署的封裝提供 nuget.org 發行管線的其他驗證機制，因為必須事先註冊簽署憑證。 如需詳細資訊，請參閱[登錄憑證](#register-certificate-on-nugetorg)。

如需有關建立已簽署的封裝的詳細資訊，請參閱[簽署封裝](../create-packages/Sign-a-package.md)和[nuget 登命令](../tools/cli-ref-sign.md)。

> [!Important]
> 目前支援封裝簽章，只有在 Windows 上使用 nuget.exe 時。 只有在 Windows 上使用 nuget.exe 或 Visual Studio 時，目前支援驗證簽署的封裝。

## <a name="certificate-requirements"></a>憑證需求

封裝簽章需要程式碼簽署憑證，這是一種特殊類型的有效憑證`id-kp-codeSigning`用途 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證必須有 RSA 公開金鑰長度為 2048 位元或更高版本。

## <a name="get-a-code-signing-certificate"></a>取得程式碼簽署憑證

可能從類似的公開憑證授權單位取得有效的憑證：

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [全域符號](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

可從取得完整的 Windows 信任憑證授權單位清單[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。

## <a name="create-a-test-certificate"></a>建立測試憑證

您可以基於測試目的使用自行發出的憑證。 若要建立自我發行的憑證，請使用[New-selfsignedcertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate.md)。

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

## <a name="timestamp-requirements"></a>時間戳記需求

簽署的封裝應包含以確保套件簽署憑證的有效期間以外的簽章有效性 RFC 3161 時間戳記。 用來登入時間戳記憑證必須是有效的`id-kp-timeStamping`用途 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證必須有 RSA 公開金鑰長度為 2048 位元或更高版本。

其他技術詳細資料位於[封裝簽章的技術規格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。

## <a name="signature-requirements-on-nugetorg"></a>在 nuget.org 的簽章需求

nuget.org 有接受已簽署的封裝的額外需求：

- 主要簽章必須是作者簽章。
- 主要簽章必須有單一的有效時間戳記。
- 作者簽章和其時間戳記簽章的 X.509 憑證：
  - 必須有 RSA 公開金鑰 2048 位元或更高。
  - 必須在每次目前的 UTC 時間上 nuget.org 的封裝驗證的有效期間內。
  - 必須鏈結至信任預設會在 Windows 上的受信任的根授權單位。 使用自我發行的憑證簽署封裝會遭到拒絕。
  - 必須是有效的用途： 
    - 簽署憑證的作者必須是有效的程式碼簽署。
    - 時間戳記憑證必須是有效的時間戳記。
  - 必須不會撤銷在簽入時間。 （這可能不是 knowable 送出時，讓 nuget.org 定期重新檢查撤銷狀態）。

## <a name="register-certificate-on-nugetorg"></a>Nuget.org 上註冊憑證

若要提交已簽署的封裝，您必須先向憑證 nuget.org。您需要做為憑證`.cer`DER 的二進位格式的檔案。 您可以使用 憑證匯出精靈，為二進位的 DER 格式匯出現有的憑證。

![憑證匯出精靈](media/CertificateExportWizard.png)

進階的使用者可以匯出憑證使用[匯出憑證的 PowerShell 命令](/powershell/module/pkiclient/export-certificate.md)。

若要登錄 nuget.org 的憑證，請移至`Certificates`區段`Account settings`頁面 （或組織的設定頁面） 並選取`Register new certificate`。

![已登錄的憑證](media/registered-certs.png)

> [!Tip]
> 一位使用者可以提交多個憑證和相同的憑證來註冊多個使用者。

使用者一旦具有憑證註冊，所有未來的封裝提交**必須**使用其中一個憑證來簽署。

使用者也可以從帳戶移除已註冊的憑證。 一旦移除憑證，該憑證簽署封裝會在提交失敗。 現有的封裝不受影響。

## <a name="configure-package-signing-requirements"></a>設定套件簽署需求

如果您是唯一的擁有者的封裝，您就需要簽署者。 也就是說，您可以使用任何已註冊的憑證簽署您的套件，並將提交至 nuget.org。

如果封裝有多個擁有者，根據預設，「 任何 」 擁有者的憑證可用來簽署套件。 做為封裝共同擁有者，您可以覆寫 「 任何 」 與自己或任何其他共同擁有者是必要的簽署者。 如果您擁有者沒有註冊任何憑證，然後將允許未簽署的封裝。 

同樣地，如果選取"Any"選項的其中一個擁有者已註冊的憑證封裝與另一個擁有者的預設值並沒有註冊任何憑證，然後 nuget.org 接受已簽署的封裝與登錄的其中一個擁有者的簽章或不帶正負號封裝 （因為其中的擁有者沒有註冊任何憑證）。

![設定封裝的簽署人](media/configure-package-signers.png)
