---
title: 簽署 NuGet 封裝參考
description: NuGet 封裝簽章需求。
author: rido-min
ms.author: rido-min
manager: unnir
ms.date: 04/24/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 751a8ff14bdc3a647985da4f908ad1a0fd0def9a
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2018
---
# <a name="signed-packages"></a><span data-ttu-id="5ec92-103">簽署的封裝</span><span class="sxs-lookup"><span data-stu-id="5ec92-103">Signed packages</span></span>

<span data-ttu-id="5ec92-104">*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 和更新版本*</span><span class="sxs-lookup"><span data-stu-id="5ec92-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="5ec92-105">NuGet 封裝可以包含數位簽章可防止遭竄改的內容。</span><span class="sxs-lookup"><span data-stu-id="5ec92-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="5ec92-106">此簽章會產生來自 X.509 憑證，也會增加實際的來源封裝的真實性證明。</span><span class="sxs-lookup"><span data-stu-id="5ec92-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="5ec92-107">簽署的封裝提供最強的端對端驗證。</span><span class="sxs-lookup"><span data-stu-id="5ec92-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="5ec92-108">作者簽章可確保封裝不已修改的作者從不論簽署封裝之後, 的儲存機制或什麼傳輸的方法傳送封裝。</span><span class="sxs-lookup"><span data-stu-id="5ec92-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="5ec92-109">取用者要求鎖定的環境可能需要使用特定作者憑證簽署的封裝。</span><span class="sxs-lookup"><span data-stu-id="5ec92-109">Consumers who demand a locked-down environment can require packages signed with a specific author certificate.</span></span>

<span data-ttu-id="5ec92-110">此外，作者簽署的封裝提供 nuget.org 發行管線的其他驗證機制，因為必須事先註冊簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="5ec92-110">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="5ec92-111">如需有關建立已簽署的封裝的詳細資訊，請參閱[簽署封裝](../create-packages/Sign-a-package.md)和[nuget 登命令](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="5ec92-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="5ec92-112">nuget.org 目前不接受簽署的封裝。</span><span class="sxs-lookup"><span data-stu-id="5ec92-112">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="5ec92-113">您可以簽署套件以發佈至自訂摘要。</span><span class="sxs-lookup"><span data-stu-id="5ec92-113">You can sign packages for publishing to custom feeds.</span></span>

> [!Important]
> <span data-ttu-id="5ec92-114">目前支援封裝簽章，只有在 Windows 上使用 nuget.exe 時。</span><span class="sxs-lookup"><span data-stu-id="5ec92-114">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="5ec92-115">只有在 Windows 上使用 nuget.exe 或 Visual Studio 時，目前支援驗證簽署的封裝。</span><span class="sxs-lookup"><span data-stu-id="5ec92-115">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="5ec92-116">憑證需求</span><span class="sxs-lookup"><span data-stu-id="5ec92-116">Certificate requirements</span></span>

<span data-ttu-id="5ec92-117">封裝簽章需要程式碼簽署憑證，這是一種特殊類型的有效憑證`id-kp-codeSigning`用途 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="5ec92-117">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="5ec92-118">此外，憑證必須有 RSA 公開金鑰長度為 2048 位元或更高版本。</span><span class="sxs-lookup"><span data-stu-id="5ec92-118">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="5ec92-119">取得程式碼簽署憑證</span><span class="sxs-lookup"><span data-stu-id="5ec92-119">Get a code signing certificate</span></span>

<span data-ttu-id="5ec92-120">有效的憑證可能會取得從公開憑證授權單位，例如：</span><span class="sxs-lookup"><span data-stu-id="5ec92-120">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="5ec92-121">Symantec</span><span class="sxs-lookup"><span data-stu-id="5ec92-121">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="5ec92-122">DigiCert</span><span class="sxs-lookup"><span data-stu-id="5ec92-122">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="5ec92-123">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="5ec92-123">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="5ec92-124">全域符號</span><span class="sxs-lookup"><span data-stu-id="5ec92-124">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="5ec92-125">Comodo</span><span class="sxs-lookup"><span data-stu-id="5ec92-125">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="5ec92-126">Certum</span><span class="sxs-lookup"><span data-stu-id="5ec92-126">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="5ec92-127">可從取得完整的 Windows 信任憑證授權單位清單[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。</span><span class="sxs-lookup"><span data-stu-id="5ec92-127">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="5ec92-128">建立測試憑證</span><span class="sxs-lookup"><span data-stu-id="5ec92-128">Create a test certificate</span></span>

<span data-ttu-id="5ec92-129">您可以基於測試目的使用自行發出的憑證。</span><span class="sxs-lookup"><span data-stu-id="5ec92-129">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="5ec92-130">若要建立自我發行的憑證，請使用[New-selfsignedcertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="5ec92-130">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

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

<span data-ttu-id="5ec92-131">此命令會建立在目前使用者的個人憑證存放區中可用的測試憑證。</span><span class="sxs-lookup"><span data-stu-id="5ec92-131">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="5ec92-132">您可以開啟憑證存放區執行`certmgr.msc`以查看新建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="5ec92-132">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="5ec92-133">時間戳記需求</span><span class="sxs-lookup"><span data-stu-id="5ec92-133">Timestamp requirements</span></span>

<span data-ttu-id="5ec92-134">簽署的封裝應包含以確保套件簽署憑證的有效期間以外的簽章有效性 RFC 3161 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="5ec92-134">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="5ec92-135">用來登入時間戳記憑證必須是有效的`id-kp-timeStamping`用途 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="5ec92-135">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="5ec92-136">此外，憑證必須有 RSA 公開金鑰長度為 2048 位元或更高版本。</span><span class="sxs-lookup"><span data-stu-id="5ec92-136">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="5ec92-137">其他技術詳細資料位於[封裝簽章的技術規格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="5ec92-137">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
