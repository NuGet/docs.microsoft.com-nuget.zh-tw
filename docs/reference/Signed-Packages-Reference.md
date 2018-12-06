---
title: 已簽署的套件
description: NuGet 封裝簽章需求。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 486bf4032e156168f9b2fef57ccdae0c372b2eff
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977507"
---
# <a name="signed-packages"></a><span data-ttu-id="e16dc-103">已簽署的套件</span><span class="sxs-lookup"><span data-stu-id="e16dc-103">Signed packages</span></span>

<span data-ttu-id="e16dc-104">*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 版及更新版本*</span><span class="sxs-lookup"><span data-stu-id="e16dc-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="e16dc-105">NuGet 套件可以包含數位簽章可防止遭竄改的內容。</span><span class="sxs-lookup"><span data-stu-id="e16dc-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="e16dc-106">此簽章會產生來自 X.509 憑證，也將真實性證明，加上實際的套件來源。</span><span class="sxs-lookup"><span data-stu-id="e16dc-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="e16dc-107">已簽署的套件會提供最強的端對端驗證。</span><span class="sxs-lookup"><span data-stu-id="e16dc-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="e16dc-108">有兩種不同的 NuGet 簽章：</span><span class="sxs-lookup"><span data-stu-id="e16dc-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="e16dc-109">**撰寫簽章**。</span><span class="sxs-lookup"><span data-stu-id="e16dc-109">**Author Signature**.</span></span> <span data-ttu-id="e16dc-110">作者簽章可保證，封裝不之後已修改作者已登入的封裝，不論其儲存機制，或傳輸封裝傳遞的方法。</span><span class="sxs-lookup"><span data-stu-id="e16dc-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="e16dc-111">此外，作者簽署的套件提供額外的驗證機制以 nuget.org 發行管線，因為必須事先註冊簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="e16dc-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="e16dc-112">如需詳細資訊，請參閱 <<c0> [ 登錄憑證](#register-certificate-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="e16dc-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="e16dc-113">**存放庫簽章**。</span><span class="sxs-lookup"><span data-stu-id="e16dc-113">**Repository Signature**.</span></span> <span data-ttu-id="e16dc-114">存放庫簽章提供完整性保證**所有**套件存放庫中，不論它們是作者帶正負號或不是，即使這些套件會取自原始它們所在的存放庫不同的位置帶正負號。</span><span class="sxs-lookup"><span data-stu-id="e16dc-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="e16dc-115">如需建立作者已簽署的封裝的詳細資訊，請參閱 <<c0> [ 簽署封裝](../create-packages/Sign-a-package.md)並[nuget 登命令](../tools/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="e16dc-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="e16dc-116">目前支援封裝簽章，只有在 Windows 上使用 nuget.exe 時。</span><span class="sxs-lookup"><span data-stu-id="e16dc-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="e16dc-117">只有在 Windows 上使用 nuget.exe 或 Visual Studio 時，目前支援驗證的已簽署的套件。</span><span class="sxs-lookup"><span data-stu-id="e16dc-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="e16dc-118">憑證需求</span><span class="sxs-lookup"><span data-stu-id="e16dc-118">Certificate requirements</span></span>

<span data-ttu-id="e16dc-119">封裝簽章需要程式碼簽署憑證，這是一種特別有效的憑證`id-kp-codeSigning`目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="e16dc-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="e16dc-120">此外，憑證必須具有 RSA 公用金鑰長度為 2048 位元或更高版本。</span><span class="sxs-lookup"><span data-stu-id="e16dc-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="e16dc-121">時間戳記的需求</span><span class="sxs-lookup"><span data-stu-id="e16dc-121">Timestamp requirements</span></span>

<span data-ttu-id="e16dc-122">已簽署的套件應該包含 RFC 3161 時間戳記，以確保套件簽署憑證的有效期間以外的簽章有效性。</span><span class="sxs-lookup"><span data-stu-id="e16dc-122">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="e16dc-123">用來登入時間戳記的憑證必須適用於`id-kp-timeStamping`目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="e16dc-123">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="e16dc-124">此外，憑證必須具有 RSA 公用金鑰長度為 2048 位元或更高版本。</span><span class="sxs-lookup"><span data-stu-id="e16dc-124">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="e16dc-125">其他技術詳細資料可在[封裝簽章的技術規格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="e16dc-125">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="e16dc-126">在 NuGet.org 上的簽章需求</span><span class="sxs-lookup"><span data-stu-id="e16dc-126">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="e16dc-127">nuget.org 具有接受已簽署的封裝的額外需求：</span><span class="sxs-lookup"><span data-stu-id="e16dc-127">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="e16dc-128">主要的簽章必須是作者簽章。</span><span class="sxs-lookup"><span data-stu-id="e16dc-128">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="e16dc-129">主要的簽章必須有單一有效的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="e16dc-129">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="e16dc-130">作者簽章和其時間戳記簽章的 X.509 憑證：</span><span class="sxs-lookup"><span data-stu-id="e16dc-130">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="e16dc-131">必須有 RSA 公開金鑰 2048 位元或更高。</span><span class="sxs-lookup"><span data-stu-id="e16dc-131">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="e16dc-132">必須在每次目前的 UTC 時間的 nuget.org 上的 封裝驗證其有效期間內。</span><span class="sxs-lookup"><span data-stu-id="e16dc-132">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="e16dc-133">必須鏈結至信任預設會在 Windows 上的受信任的根授權單位。</span><span class="sxs-lookup"><span data-stu-id="e16dc-133">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="e16dc-134">使用自我發行的憑證簽署的封裝會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="e16dc-134">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="e16dc-135">必須是有效的目的：</span><span class="sxs-lookup"><span data-stu-id="e16dc-135">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="e16dc-136">作者簽署憑證必須是有效簽署程式碼。</span><span class="sxs-lookup"><span data-stu-id="e16dc-136">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="e16dc-137">時間戳記憑證必須是有效的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="e16dc-137">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="e16dc-138">必須不會撤銷在簽入時間。</span><span class="sxs-lookup"><span data-stu-id="e16dc-138">Must not be revoked at signing time.</span></span> <span data-ttu-id="e16dc-139">（這可能不是 knowable 在提交時，所以 nuget.org 定期重新檢查撤銷狀態）。</span><span class="sxs-lookup"><span data-stu-id="e16dc-139">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="e16dc-140">相關文章</span><span class="sxs-lookup"><span data-stu-id="e16dc-140">Related articles</span></span>

- [<span data-ttu-id="e16dc-141">簽署 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="e16dc-141">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="e16dc-142">安裝已簽署的套件</span><span class="sxs-lookup"><span data-stu-id="e16dc-142">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
