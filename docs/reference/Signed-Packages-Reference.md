---
title: 簽署的套件
description: NuGet 套件簽署的需求。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 7384e8b30cb2ec5fe53ea0fe485858bc1f7b3c43
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238175"
---
# <a name="signed-packages"></a><span data-ttu-id="c241c-103">已簽署的套件</span><span class="sxs-lookup"><span data-stu-id="c241c-103">Signed packages</span></span>

<span data-ttu-id="c241c-104">*NuGet 4.6.0 + 和 Visual Studio 2017 15.6 版和更新版本*</span><span class="sxs-lookup"><span data-stu-id="c241c-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="c241c-105">NuGet 套件可以包含數位簽章，以防止遭篡改的內容受到保護。</span><span class="sxs-lookup"><span data-stu-id="c241c-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="c241c-106">此簽章是從 x.509 憑證產生的，也會將真品證明證明新增至封裝的實際來源。</span><span class="sxs-lookup"><span data-stu-id="c241c-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="c241c-107">簽署的套件提供最強的端對端驗證。</span><span class="sxs-lookup"><span data-stu-id="c241c-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="c241c-108">有兩種不同類型的 NuGet 簽章：</span><span class="sxs-lookup"><span data-stu-id="c241c-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="c241c-109">**作者簽名** 。</span><span class="sxs-lookup"><span data-stu-id="c241c-109">**Author Signature** .</span></span> <span data-ttu-id="c241c-110">作者簽名碼可保證在作者簽署套件之後，封裝未經過修改，不論是從哪個存放庫或封裝的傳輸方法傳遞。</span><span class="sxs-lookup"><span data-stu-id="c241c-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="c241c-111">此外，作者簽署的套件會提供額外的驗證機制給 nuget.org 發佈管線，因為簽署憑證必須事先註冊。</span><span class="sxs-lookup"><span data-stu-id="c241c-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="c241c-112">如需詳細資訊，請參閱 [註冊憑證](#signature-requirements-on-nugetorg)。</span><span class="sxs-lookup"><span data-stu-id="c241c-112">For more information, see [Register certificates](#signature-requirements-on-nugetorg).</span></span>
- <span data-ttu-id="c241c-113">存放 **庫簽** 章。</span><span class="sxs-lookup"><span data-stu-id="c241c-113">**Repository Signature** .</span></span> <span data-ttu-id="c241c-114">存放庫簽章會針對存放庫中的 **所有** 套件提供完整性保證（不論其是否為作者簽署），即使這些套件是從與其簽署來源的原始存放庫不同的位置取得。</span><span class="sxs-lookup"><span data-stu-id="c241c-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="c241c-115">如需建立作者簽署套件的詳細資訊，請參閱 [簽署封裝](../create-packages/Sign-a-package.md) 和 [nuget sign 命令](../reference/cli-reference/cli-ref-sign.md)。</span><span class="sxs-lookup"><span data-stu-id="c241c-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../reference/cli-reference/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="c241c-116">目前只有在 Windows 上使用 nuget.exe 時，才支援套件簽署。</span><span class="sxs-lookup"><span data-stu-id="c241c-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="c241c-117">[目前只有在使用 Windows 上的 nuget.exe或 Visual Studio 時，才支援驗證已簽署的套件 ](../reference/cli-reference/cli-ref-verify.md) 。</span><span class="sxs-lookup"><span data-stu-id="c241c-117">[Verification of signed packages is currently supported only when using nuget.exe](../reference/cli-reference/cli-ref-verify.md) or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="c241c-118">憑證需求</span><span class="sxs-lookup"><span data-stu-id="c241c-118">Certificate requirements</span></span>

<span data-ttu-id="c241c-119">套件簽署需要程式碼簽署憑證，這是一種特殊類型的憑證，適用于 `id-kp-codeSigning` 目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="c241c-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="c241c-120">此外，憑證的 RSA 公開金鑰長度必須是2048位或更高。</span><span class="sxs-lookup"><span data-stu-id="c241c-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="c241c-121">時間戳記需求</span><span class="sxs-lookup"><span data-stu-id="c241c-121">Timestamp requirements</span></span>

<span data-ttu-id="c241c-122">簽署的套件應包含 RFC 3161 時間戳記，以確保簽章的有效性超過套件簽署憑證的有效期間。</span><span class="sxs-lookup"><span data-stu-id="c241c-122">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="c241c-123">用來簽署時間戳記的憑證必須適用于 `id-kp-timeStamping` 目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="c241c-123">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="c241c-124">此外，憑證的 RSA 公開金鑰長度必須是2048位或更高。</span><span class="sxs-lookup"><span data-stu-id="c241c-124">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="c241c-125">您可以在 (GitHub) 的套件簽章 [技術規格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) 中找到其他技術詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c241c-125">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="c241c-126">NuGet.org 上的特徵標記需求</span><span class="sxs-lookup"><span data-stu-id="c241c-126">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="c241c-127">nuget.org 具有接受已簽署套件的其他需求：</span><span class="sxs-lookup"><span data-stu-id="c241c-127">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="c241c-128">主要簽章必須是作者簽章。</span><span class="sxs-lookup"><span data-stu-id="c241c-128">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="c241c-129">主要簽章必須有單一有效的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="c241c-129">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="c241c-130">作者簽名和其時間戳記簽章的 x.509 憑證：</span><span class="sxs-lookup"><span data-stu-id="c241c-130">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="c241c-131">必須有 RSA 公開金鑰2048位或更高的版本。</span><span class="sxs-lookup"><span data-stu-id="c241c-131">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="c241c-132">在 nuget.org 上的套件驗證期間，每個目前的 UTC 時間都必須在其有效期間內。</span><span class="sxs-lookup"><span data-stu-id="c241c-132">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="c241c-133">必須連結至 Windows 上預設受信任的受根信任授權單位。</span><span class="sxs-lookup"><span data-stu-id="c241c-133">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="c241c-134">已拒絕使用自我發行憑證簽署的套件。</span><span class="sxs-lookup"><span data-stu-id="c241c-134">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="c241c-135">必須適用于其用途：</span><span class="sxs-lookup"><span data-stu-id="c241c-135">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="c241c-136">作者簽署憑證必須適用于程式碼簽署。</span><span class="sxs-lookup"><span data-stu-id="c241c-136">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="c241c-137">時間戳記憑證必須是有效的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="c241c-137">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="c241c-138">不得在簽署時撤銷。</span><span class="sxs-lookup"><span data-stu-id="c241c-138">Must not be revoked at signing time.</span></span> <span data-ttu-id="c241c-139"> (這可能不會在提交時 knowable，因此 nuget.org 會定期重新檢查撤銷狀態) 。</span><span class="sxs-lookup"><span data-stu-id="c241c-139">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="c241c-140">相關文章</span><span class="sxs-lookup"><span data-stu-id="c241c-140">Related articles</span></span>

- [<span data-ttu-id="c241c-141">簽署 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="c241c-141">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="c241c-142">管理套件的信任界限</span><span class="sxs-lookup"><span data-stu-id="c241c-142">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
