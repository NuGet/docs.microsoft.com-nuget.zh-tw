---
title: 簽署封裝參考 |Microsoft 文件
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 簽署封裝功能描述。
keywords: NuGet 套件簽署、 簽章憑證
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a2a338596f7d98ded11da6fb02bafba3521249ab
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="signed-packages"></a>簽署的封裝

*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 和更新版本*

NuGet 封裝可以包含數位簽章可防止遭竄改的內容。 此簽章會產生來自 X.509 憑證，也會增加實際的來源封裝的真實性證明。

簽署的封裝提供最強的端對端驗證。 作者簽章可確保封裝不已修改的作者從不論簽署封裝之後, 的儲存機制或什麼傳輸的方法傳送封裝。

取用者要求鎖定的環境可能需要使用特定作者憑證簽署的封裝。

此外，作者簽署的封裝提供 nuget.org 發行管線的其他驗證機制，因為必須事先註冊簽署憑證。

如需有關建立已簽署的封裝的詳細資訊，請參閱[簽署封裝](../create-packages/Sign-a-package.md)和[nuget 登命令](../tools/cli-ref-sign.md)。

> [!Important]
> nuget.org 目前不接受簽署的封裝。 您可以簽署套件以發佈至自訂摘要。

## <a name="certificate-requirements"></a>憑證需求

封裝簽章需要程式碼簽署憑證，這是一種特殊類型的有效憑證`id-kp-codeSigning`用途 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證必須有 RSA 公開金鑰長度為 2048 位元或更高版本。

## <a name="get-a-code-signing-certificate"></a>取得程式碼簽署憑證

有效的憑證可能會取得從公開憑證授權單位，例如：

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [全域符號](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

可從取得完整的 Windows 信任憑證授權單位清單[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。

## <a name="create-a-test-certificate"></a>建立測試憑證

您可以基於測試目的使用自行發出的憑證。 若要建立自我發行的憑證，請使用[New-selfsignedcertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell 命令。

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

## <a name="timestamp-requirements"></a>時間戳記需求

簽署的封裝應包含以確保套件簽署憑證的有效期間以外的簽章有效性 RFC 3161 時間戳記。 用來登入時間戳記憑證必須是有效的`id-kp-timeStamping`用途 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證必須有 RSA 公開金鑰長度為 2048 位元或更高版本。

其他技術詳細資料位於[封裝簽章的技術規格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。
