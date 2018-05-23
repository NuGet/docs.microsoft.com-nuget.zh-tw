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
# <a name="signed-packages"></a><span data-ttu-id="4900b-103">簽署的封裝</span><span class="sxs-lookup"><span data-stu-id="4900b-103">Signed packages</span></span>

<span data-ttu-id="4900b-104">*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 和更新版本*</span><span class="sxs-lookup"><span data-stu-id="4900b-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="4900b-105">NuGet 封裝可以包含數位簽章可防止遭竄改的內容。</span><span class="sxs-lookup"><span data-stu-id="4900b-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="4900b-106">此簽章會產生來自 X.509 憑證，也會增加實際的來源封裝的真實性證明。</span><span class="sxs-lookup"><span data-stu-id="4900b-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="4900b-107">簽署的封裝提供最強的端對端驗證。</span><span class="sxs-lookup"><span data-stu-id="4900b-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="4900b-108">作者簽章可確保封裝不已修改的作者從不論簽署封裝之後, 的儲存機制或什麼傳輸的方法傳送封裝。</span><span class="sxs-lookup"><span data-stu-id="4900b-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="4900b-109">此外，作者簽署的封裝提供 nuget.org 發行管線的其他驗證機制，因為必須事先註冊簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="4900b-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="4900b-110">如需詳細資訊，請參閱[登錄憑證](#register-certificate-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="4900b-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="4900b-111">如需有關建立已簽署的封裝的詳細資訊，請參閱[簽署封裝](../create-packages/Sign-a-package.md)和[nuget 登命令](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="4900b-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="4900b-112">目前支援封裝簽章，只有在 Windows 上使用 nuget.exe 時。</span><span class="sxs-lookup"><span data-stu-id="4900b-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="4900b-113">只有在 Windows 上使用 nuget.exe 或 Visual Studio 時，目前支援驗證簽署的封裝。</span><span class="sxs-lookup"><span data-stu-id="4900b-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="4900b-114">憑證需求</span><span class="sxs-lookup"><span data-stu-id="4900b-114">Certificate requirements</span></span>

<span data-ttu-id="4900b-115">封裝簽章需要程式碼簽署憑證，這是一種特殊類型的有效憑證`id-kp-codeSigning`用途 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="4900b-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="4900b-116">此外，憑證必須有 RSA 公開金鑰長度為 2048 位元或更高版本。</span><span class="sxs-lookup"><span data-stu-id="4900b-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="4900b-117">取得程式碼簽署憑證</span><span class="sxs-lookup"><span data-stu-id="4900b-117">Get a code signing certificate</span></span>

<span data-ttu-id="4900b-118">可能從類似的公開憑證授權單位取得有效的憑證：</span><span class="sxs-lookup"><span data-stu-id="4900b-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="4900b-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="4900b-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="4900b-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="4900b-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="4900b-121">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="4900b-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="4900b-122">全域符號</span><span class="sxs-lookup"><span data-stu-id="4900b-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="4900b-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="4900b-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="4900b-124">Certum</span><span class="sxs-lookup"><span data-stu-id="4900b-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="4900b-125">可從取得完整的 Windows 信任憑證授權單位清單[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。</span><span class="sxs-lookup"><span data-stu-id="4900b-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="4900b-126">建立測試憑證</span><span class="sxs-lookup"><span data-stu-id="4900b-126">Create a test certificate</span></span>

<span data-ttu-id="4900b-127">您可以基於測試目的使用自行發出的憑證。</span><span class="sxs-lookup"><span data-stu-id="4900b-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="4900b-128">若要建立自我發行的憑證，請使用[New-selfsignedcertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate.md)。</span><span class="sxs-lookup"><span data-stu-id="4900b-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="4900b-129">此命令會建立在目前使用者的個人憑證存放區中可用的測試憑證。</span><span class="sxs-lookup"><span data-stu-id="4900b-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="4900b-130">您可以開啟憑證存放區執行`certmgr.msc`以查看新建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="4900b-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="4900b-131">nuget.org 不接受封裝以自行發出的憑證簽署。</span><span class="sxs-lookup"><span data-stu-id="4900b-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="4900b-132">時間戳記需求</span><span class="sxs-lookup"><span data-stu-id="4900b-132">Timestamp requirements</span></span>

<span data-ttu-id="4900b-133">簽署的封裝應包含以確保套件簽署憑證的有效期間以外的簽章有效性 RFC 3161 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="4900b-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="4900b-134">用來登入時間戳記憑證必須是有效的`id-kp-timeStamping`用途 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="4900b-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="4900b-135">此外，憑證必須有 RSA 公開金鑰長度為 2048 位元或更高版本。</span><span class="sxs-lookup"><span data-stu-id="4900b-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="4900b-136">其他技術詳細資料位於[封裝簽章的技術規格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="4900b-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="4900b-137">在 nuget.org 的簽章需求</span><span class="sxs-lookup"><span data-stu-id="4900b-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="4900b-138">nuget.org 有接受已簽署的封裝的額外需求：</span><span class="sxs-lookup"><span data-stu-id="4900b-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="4900b-139">主要簽章必須是作者簽章。</span><span class="sxs-lookup"><span data-stu-id="4900b-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="4900b-140">主要簽章必須有單一的有效時間戳記。</span><span class="sxs-lookup"><span data-stu-id="4900b-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="4900b-141">作者簽章和其時間戳記簽章的 X.509 憑證：</span><span class="sxs-lookup"><span data-stu-id="4900b-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="4900b-142">必須有 RSA 公開金鑰 2048 位元或更高。</span><span class="sxs-lookup"><span data-stu-id="4900b-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="4900b-143">必須在每次目前的 UTC 時間上 nuget.org 的封裝驗證的有效期間內。</span><span class="sxs-lookup"><span data-stu-id="4900b-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="4900b-144">必須鏈結至信任預設會在 Windows 上的受信任的根授權單位。</span><span class="sxs-lookup"><span data-stu-id="4900b-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="4900b-145">使用自我發行的憑證簽署封裝會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="4900b-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="4900b-146">必須是有效的用途：</span><span class="sxs-lookup"><span data-stu-id="4900b-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="4900b-147">簽署憑證的作者必須是有效的程式碼簽署。</span><span class="sxs-lookup"><span data-stu-id="4900b-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="4900b-148">時間戳記憑證必須是有效的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="4900b-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="4900b-149">必須不會撤銷在簽入時間。</span><span class="sxs-lookup"><span data-stu-id="4900b-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="4900b-150">（這可能不是 knowable 送出時，讓 nuget.org 定期重新檢查撤銷狀態）。</span><span class="sxs-lookup"><span data-stu-id="4900b-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="4900b-151">Nuget.org 上註冊憑證</span><span class="sxs-lookup"><span data-stu-id="4900b-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="4900b-152">若要提交已簽署的封裝，您必須先向憑證 nuget.org。您需要做為憑證`.cer`DER 的二進位格式的檔案。</span><span class="sxs-lookup"><span data-stu-id="4900b-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="4900b-153">您可以使用 憑證匯出精靈，為二進位的 DER 格式匯出現有的憑證。</span><span class="sxs-lookup"><span data-stu-id="4900b-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![憑證匯出精靈](media/CertificateExportWizard.png)

<span data-ttu-id="4900b-155">進階的使用者可以匯出憑證使用[匯出憑證的 PowerShell 命令](/powershell/module/pkiclient/export-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="4900b-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="4900b-156">若要登錄 nuget.org 的憑證，請移至`Certificates`區段`Account settings`頁面 （或組織的設定頁面） 並選取`Register new certificate`。</span><span class="sxs-lookup"><span data-stu-id="4900b-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![已登錄的憑證](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="4900b-158">一位使用者可以提交多個憑證和相同的憑證來註冊多個使用者。</span><span class="sxs-lookup"><span data-stu-id="4900b-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="4900b-159">使用者一旦具有憑證註冊，所有未來的封裝提交**必須**使用其中一個憑證來簽署。</span><span class="sxs-lookup"><span data-stu-id="4900b-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="4900b-160">使用者也可以從帳戶移除已註冊的憑證。</span><span class="sxs-lookup"><span data-stu-id="4900b-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="4900b-161">一旦移除憑證，該憑證簽署封裝會在提交失敗。</span><span class="sxs-lookup"><span data-stu-id="4900b-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="4900b-162">現有的封裝不受影響。</span><span class="sxs-lookup"><span data-stu-id="4900b-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="4900b-163">設定套件簽署需求</span><span class="sxs-lookup"><span data-stu-id="4900b-163">Configure package signing requirements</span></span>

<span data-ttu-id="4900b-164">如果您是唯一的擁有者的封裝，您就需要簽署者。</span><span class="sxs-lookup"><span data-stu-id="4900b-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="4900b-165">也就是說，您可以使用任何已註冊的憑證簽署您的套件，並將提交至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="4900b-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="4900b-166">如果封裝有多個擁有者，根據預設，「 任何 」 擁有者的憑證可用來簽署套件。</span><span class="sxs-lookup"><span data-stu-id="4900b-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="4900b-167">做為封裝共同擁有者，您可以覆寫 「 任何 」 與自己或任何其他共同擁有者是必要的簽署者。</span><span class="sxs-lookup"><span data-stu-id="4900b-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="4900b-168">如果您擁有者沒有註冊任何憑證，然後將允許未簽署的封裝。</span><span class="sxs-lookup"><span data-stu-id="4900b-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="4900b-169">同樣地，如果選取"Any"選項的其中一個擁有者已註冊的憑證封裝與另一個擁有者的預設值並沒有註冊任何憑證，然後 nuget.org 接受已簽署的封裝與登錄的其中一個擁有者的簽章或不帶正負號封裝 （因為其中的擁有者沒有註冊任何憑證）。</span><span class="sxs-lookup"><span data-stu-id="4900b-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![設定封裝的簽署人](media/configure-package-signers.png)
