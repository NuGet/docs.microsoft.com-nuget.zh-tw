---
title: 已簽署的套件
description: NuGet 封裝簽章需求。
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 992097281e21cd8cf37edf67fb1968b70c2b359b
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020506"
---
# <a name="signed-packages"></a><span data-ttu-id="08bd2-103">已簽署的套件</span><span class="sxs-lookup"><span data-stu-id="08bd2-103">Signed packages</span></span>

<span data-ttu-id="08bd2-104">*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 版及更新版本*</span><span class="sxs-lookup"><span data-stu-id="08bd2-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="08bd2-105">NuGet 套件可以包含數位簽章可防止遭竄改的內容。</span><span class="sxs-lookup"><span data-stu-id="08bd2-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="08bd2-106">此簽章會產生來自 X.509 憑證，也將真實性證明，加上實際的套件來源。</span><span class="sxs-lookup"><span data-stu-id="08bd2-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="08bd2-107">已簽署的套件會提供最強的端對端驗證。</span><span class="sxs-lookup"><span data-stu-id="08bd2-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="08bd2-108">有兩種不同的 NuGet 簽章：</span><span class="sxs-lookup"><span data-stu-id="08bd2-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="08bd2-109">**撰寫簽章**。</span><span class="sxs-lookup"><span data-stu-id="08bd2-109">**Author Signature**.</span></span> <span data-ttu-id="08bd2-110">作者簽章可保證，封裝不之後已修改作者已登入的封裝，不論其儲存機制，或傳輸封裝傳遞的方法。</span><span class="sxs-lookup"><span data-stu-id="08bd2-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="08bd2-111">此外，作者簽署的套件提供額外的驗證機制以 nuget.org 發行管線，因為必須事先註冊簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="08bd2-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="08bd2-112">如需詳細資訊，請參閱 <<c0> [ 登錄憑證](#register-certificate-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="08bd2-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="08bd2-113">**存放庫簽章**。</span><span class="sxs-lookup"><span data-stu-id="08bd2-113">**Repository Signature**.</span></span> <span data-ttu-id="08bd2-114">存放庫簽章提供完整性保證**所有**套件存放庫中，不論它們是作者帶正負號或不是，即使這些套件會取自原始它們所在的存放庫不同的位置帶正負號。</span><span class="sxs-lookup"><span data-stu-id="08bd2-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="08bd2-115">如需建立作者已簽署的封裝的詳細資訊，請參閱 <<c0> [ 簽署封裝](../create-packages/Sign-a-package.md)並[nuget 登命令](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="08bd2-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="08bd2-116">目前支援封裝簽章，只有在 Windows 上使用 nuget.exe 時。</span><span class="sxs-lookup"><span data-stu-id="08bd2-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="08bd2-117">只有在 Windows 上使用 nuget.exe 或 Visual Studio 時，目前支援驗證的已簽署的套件。</span><span class="sxs-lookup"><span data-stu-id="08bd2-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="08bd2-118">憑證需求</span><span class="sxs-lookup"><span data-stu-id="08bd2-118">Certificate requirements</span></span>

<span data-ttu-id="08bd2-119">封裝簽章需要程式碼簽署憑證，這是一種特別有效的憑證`id-kp-codeSigning`目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="08bd2-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="08bd2-120">此外，憑證必須具有 RSA 公用金鑰長度為 2048 位元或更高版本。</span><span class="sxs-lookup"><span data-stu-id="08bd2-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="08bd2-121">取得程式碼簽署憑證</span><span class="sxs-lookup"><span data-stu-id="08bd2-121">Get a code signing certificate</span></span>

<span data-ttu-id="08bd2-122">有效的憑證可能取自的公開憑證授權單位，例如：</span><span class="sxs-lookup"><span data-stu-id="08bd2-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="08bd2-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="08bd2-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="08bd2-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="08bd2-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="08bd2-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="08bd2-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="08bd2-126">全域符號</span><span class="sxs-lookup"><span data-stu-id="08bd2-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="08bd2-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="08bd2-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="08bd2-128">Certum</span><span class="sxs-lookup"><span data-stu-id="08bd2-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="08bd2-129">透過 Windows 受信任的憑證授權單位的完整清單可以取自[ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners)。</span><span class="sxs-lookup"><span data-stu-id="08bd2-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="08bd2-130">建立測試憑證</span><span class="sxs-lookup"><span data-stu-id="08bd2-130">Create a test certificate</span></span>

<span data-ttu-id="08bd2-131">基於測試目的，您可以使用自行發出的憑證。</span><span class="sxs-lookup"><span data-stu-id="08bd2-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="08bd2-132">若要建立自我發行的憑證，請使用[New-selfsignedcertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate.md)。</span><span class="sxs-lookup"><span data-stu-id="08bd2-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="08bd2-133">此命令會建立在目前使用者的個人憑證存放區中可用的測試憑證。</span><span class="sxs-lookup"><span data-stu-id="08bd2-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="08bd2-134">您可以開啟憑證存放區執行`certmgr.msc`以查看新建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="08bd2-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="08bd2-135">nuget.org 不接受封裝以自行發出的憑證簽署。</span><span class="sxs-lookup"><span data-stu-id="08bd2-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="08bd2-136">時間戳記的需求</span><span class="sxs-lookup"><span data-stu-id="08bd2-136">Timestamp requirements</span></span>

<span data-ttu-id="08bd2-137">已簽署的套件應該包含 RFC 3161 時間戳記，以確保套件簽署憑證的有效期間以外的簽章有效性。</span><span class="sxs-lookup"><span data-stu-id="08bd2-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="08bd2-138">用來登入時間戳記的憑證必須適用於`id-kp-timeStamping`目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="08bd2-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="08bd2-139">此外，憑證必須具有 RSA 公用金鑰長度為 2048 位元或更高版本。</span><span class="sxs-lookup"><span data-stu-id="08bd2-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="08bd2-140">其他技術詳細資料可在[封裝簽章的技術規格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="08bd2-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="08bd2-141">在 nuget.org 上的簽章需求</span><span class="sxs-lookup"><span data-stu-id="08bd2-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="08bd2-142">nuget.org 具有接受已簽署的封裝的額外需求：</span><span class="sxs-lookup"><span data-stu-id="08bd2-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="08bd2-143">主要的簽章必須是作者簽章。</span><span class="sxs-lookup"><span data-stu-id="08bd2-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="08bd2-144">主要的簽章必須有單一有效的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="08bd2-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="08bd2-145">作者簽章和其時間戳記簽章的 X.509 憑證：</span><span class="sxs-lookup"><span data-stu-id="08bd2-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="08bd2-146">必須有 RSA 公開金鑰 2048 位元或更高。</span><span class="sxs-lookup"><span data-stu-id="08bd2-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="08bd2-147">必須在每次目前的 UTC 時間的 nuget.org 上的 封裝驗證其有效期間內。</span><span class="sxs-lookup"><span data-stu-id="08bd2-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="08bd2-148">必須鏈結至信任預設會在 Windows 上的受信任的根授權單位。</span><span class="sxs-lookup"><span data-stu-id="08bd2-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="08bd2-149">使用自我發行的憑證簽署的封裝會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="08bd2-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="08bd2-150">必須是有效的目的：</span><span class="sxs-lookup"><span data-stu-id="08bd2-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="08bd2-151">作者簽署憑證必須是有效簽署程式碼。</span><span class="sxs-lookup"><span data-stu-id="08bd2-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="08bd2-152">時間戳記憑證必須是有效的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="08bd2-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="08bd2-153">必須不會撤銷在簽入時間。</span><span class="sxs-lookup"><span data-stu-id="08bd2-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="08bd2-154">（這可能不是 knowable 在提交時，所以 nuget.org 定期重新檢查撤銷狀態）。</span><span class="sxs-lookup"><span data-stu-id="08bd2-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="08bd2-155">在 nuget.org 上註冊憑證</span><span class="sxs-lookup"><span data-stu-id="08bd2-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="08bd2-156">若要提交已簽署的封裝，您必須先使用 nuget.org 中註冊憑證。您必須為憑證`.cer`DER 的二進位格式的檔案。</span><span class="sxs-lookup"><span data-stu-id="08bd2-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="08bd2-157">您可以使用 憑證匯出精靈，為二進位 DER 格式匯出現有的憑證。</span><span class="sxs-lookup"><span data-stu-id="08bd2-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![憑證匯出精靈](media/CertificateExportWizard.png)

<span data-ttu-id="08bd2-159">進階的使用者可以使用憑證匯出[匯出憑證的 PowerShell 命令](/powershell/module/pkiclient/export-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="08bd2-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="08bd2-160">若要向 nuget.org 中的憑證，請移至`Certificates`上一節`Account settings`網頁 （或組織的 [設定] 頁面），然後選取`Register new certificate`。</span><span class="sxs-lookup"><span data-stu-id="08bd2-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![已登錄的憑證](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="08bd2-162">一位使用者可以提交多個使用者，則可以註冊多個憑證和相同的憑證。</span><span class="sxs-lookup"><span data-stu-id="08bd2-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="08bd2-163">使用者一旦具有憑證註冊，所有未來的套件提交**必須**使用其中一個憑證來簽署。</span><span class="sxs-lookup"><span data-stu-id="08bd2-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="08bd2-164">使用者也可以從帳戶移除已註冊的憑證。</span><span class="sxs-lookup"><span data-stu-id="08bd2-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="08bd2-165">一旦移除憑證，使用該憑證簽署的封裝將會在提交失敗。</span><span class="sxs-lookup"><span data-stu-id="08bd2-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="08bd2-166">現有的封裝不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="08bd2-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="08bd2-167">設定套件簽署需求</span><span class="sxs-lookup"><span data-stu-id="08bd2-167">Configure package signing requirements</span></span>

<span data-ttu-id="08bd2-168">如果您是套件的唯一擁有者，您就會是所需的簽署人。</span><span class="sxs-lookup"><span data-stu-id="08bd2-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="08bd2-169">也就是說，您可以使用任何已註冊的憑證來簽署您的套件，並提交至 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="08bd2-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="08bd2-170">如果封裝有多個擁有者，根據預設，[任何] 擁有者的憑證可用來簽署封裝。</span><span class="sxs-lookup"><span data-stu-id="08bd2-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="08bd2-171">為封裝的共同擁有者，您可以覆寫 「 任何 」 與自己或任何其他共同擁有者設為所需的簽署人。</span><span class="sxs-lookup"><span data-stu-id="08bd2-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="08bd2-172">如果您的擁有者並沒有任何已註冊的憑證，則不允許未簽署的封裝。</span><span class="sxs-lookup"><span data-stu-id="08bd2-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="08bd2-173">同樣地，如果選取 [任何] 選項的其中一位擁有者已註冊的憑證封裝與另一個擁有者的預設值並沒有任何已註冊的憑證，然後 nuget.org 接受已簽署的封裝註冊的其中一個擁有者的簽章或不帶正負號封裝 （因為擁有者並沒有任何已註冊的憑證）。</span><span class="sxs-lookup"><span data-stu-id="08bd2-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![設定套件簽署](media/configure-package-signers.png)
