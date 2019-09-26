---
title: 簽署 NuGet 套件
description: 說明已簽署套件如何用於啟用內容完整性驗證。
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 1053a18926f63e02f0b1c100e7cc1cd293654ced
ms.sourcegitcommit: e4b0ff4460865db6dc7bc9f20e9f644d98493011
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71307206"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="8715f-103">簽署 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="8715f-103">Signing NuGet Packages</span></span>

<span data-ttu-id="8715f-104">已簽署套件允許內容完整性驗證檢查，其提供防止內容竄改的保護。</span><span class="sxs-lookup"><span data-stu-id="8715f-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="8715f-105">套件簽章也作為套件實際來源和消費者加強套件真確性的真實單一來源。</span><span class="sxs-lookup"><span data-stu-id="8715f-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="8715f-106">此指南會假設您已[建立套件](creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="8715f-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="8715f-107">取得程式碼簽署憑證</span><span class="sxs-lookup"><span data-stu-id="8715f-107">Get a code signing certificate</span></span>

<span data-ttu-id="8715f-108">有效的憑證可能可從公開憑證授權單位取得，例如 [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)、[DigiCert](https://www.digicert.com/code-signing/)、[Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)、[Global Sign](https://www.globalsign.com/en/code-signing-certificate/)、[Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)、[Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 等。受 Windows 信任的憑證授權單位完整清單可從 [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners) 取得。</span><span class="sxs-lookup"><span data-stu-id="8715f-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="8715f-109">您可以基於測試目的使用自動發行的憑證。</span><span class="sxs-lookup"><span data-stu-id="8715f-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="8715f-110">然而，NuGet.org 並不接受使用自動發行憑證簽署的套件。深入了解[如何建立測試憑證](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="8715f-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="8715f-111">匯出憑證檔案</span><span class="sxs-lookup"><span data-stu-id="8715f-111">Export the certificate file</span></span>

* <span data-ttu-id="8715f-112">您可以使用憑證匯出精靈將現有的憑證匯出為二進位 DER 格式。</span><span class="sxs-lookup"><span data-stu-id="8715f-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![憑證匯出精靈](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="8715f-114">您也可以使用 [Export-Certificate PowerShell 命令](/powershell/module/pkiclient/export-certificate)匯出認證。</span><span class="sxs-lookup"><span data-stu-id="8715f-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="8715f-115">簽署套件</span><span class="sxs-lookup"><span data-stu-id="8715f-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="8715f-116">需要 nuget.exe 4.6.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8715f-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="8715f-117">即將推出 dotnet 支援- [#7939](https://github.com/NuGet/Home/issues/7939)</span><span class="sxs-lookup"><span data-stu-id="8715f-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="8715f-118">使用 [nuget sign](../reference/cli-reference/cli-ref-sign.md) 簽署套件：</span><span class="sxs-lookup"><span data-stu-id="8715f-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="8715f-119">憑證提供者通常也會提供時間戳記伺服器 URL，可用於上方顯示的 `Timestamper` 選擇性引數。</span><span class="sxs-lookup"><span data-stu-id="8715f-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="8715f-120">請洽詢提供者的文件及 (或) 支援人員，以取得該服務 URL。</span><span class="sxs-lookup"><span data-stu-id="8715f-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="8715f-121">您可以使用憑證存放區中可用的憑證，或使用檔案中的憑證。</span><span class="sxs-lookup"><span data-stu-id="8715f-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="8715f-122">請參閱 [nuget sign](../reference/cli-reference/cli-ref-sign.md) 的 CLI 參考。</span><span class="sxs-lookup"><span data-stu-id="8715f-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="8715f-123">簽署的套件應包含時間戳記，以確定簽署憑證過期時，簽章仍保持有效。</span><span class="sxs-lookup"><span data-stu-id="8715f-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="8715f-124">若不包含時間戳記，則簽署作業會產生[警告](../reference/errors-and-warnings/NU3002.md)。</span><span class="sxs-lookup"><span data-stu-id="8715f-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="8715f-125">您可以使用 [nuget verify](../reference/cli-reference/cli-ref-verify.md) 查看指定套件的簽章詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8715f-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="8715f-126">在 NuGet.org 上註冊憑證</span><span class="sxs-lookup"><span data-stu-id="8715f-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="8715f-127">若要發佈已簽署套件，必須先在 NuGet.org 上註冊憑證。憑證必須為二進位 DER 格式的 `.cer` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8715f-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="8715f-128">[登入](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) NuGet.org。</span><span class="sxs-lookup"><span data-stu-id="8715f-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="8715f-129">前往 `Account settings` (若您想要使用組織帳戶來註冊憑證，則前往 `Manage Organization` **>** `Edit Organziation`)。</span><span class="sxs-lookup"><span data-stu-id="8715f-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="8715f-130">展開 `Certificates` 區段並選取 `Register new`。</span><span class="sxs-lookup"><span data-stu-id="8715f-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="8715f-131">瀏覽並選取稍早匯出的憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="8715f-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="8715f-132">![已註冊憑證](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="8715f-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="8715f-133">**注意**</span><span class="sxs-lookup"><span data-stu-id="8715f-133">**Note**</span></span>
* <span data-ttu-id="8715f-134">一位使用者可以提交多個憑證，且多位使用者可以註冊同一個憑證。</span><span class="sxs-lookup"><span data-stu-id="8715f-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="8715f-135">使用者在註冊憑證後，往後提交的所有套件都**必須**使用其中一項憑證簽署。</span><span class="sxs-lookup"><span data-stu-id="8715f-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="8715f-136">請參閱[在 NuGet.org 上管理您套件的簽署需求](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="8715f-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="8715f-137">使用者也可以從帳戶移除已註冊憑證。</span><span class="sxs-lookup"><span data-stu-id="8715f-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="8715f-138">移除憑證後，使用該憑證簽署的新套件將會提交失敗。</span><span class="sxs-lookup"><span data-stu-id="8715f-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="8715f-139">現有的套件則不會受影響。</span><span class="sxs-lookup"><span data-stu-id="8715f-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="8715f-140">發行套件</span><span class="sxs-lookup"><span data-stu-id="8715f-140">Publish the package</span></span>

<span data-ttu-id="8715f-141">您現在已準備好將套件發佈至 NuGet.org。請參閱[發佈套件](../nuget-org/Publish-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="8715f-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="8715f-142">建立測試憑證</span><span class="sxs-lookup"><span data-stu-id="8715f-142">Create a test certificate</span></span>

<span data-ttu-id="8715f-143">您可以基於測試目的使用自動發行的憑證。</span><span class="sxs-lookup"><span data-stu-id="8715f-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="8715f-144">若要建立自動發行的憑證，請使用 [New-SelfSignedCertificate PowerShell 命令](/powershell/module/pkiclient/new-selfsignedcertificate)。</span><span class="sxs-lookup"><span data-stu-id="8715f-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="8715f-145">此命令會建立測試憑證，可在目前使用者的個人憑證存放區中使用。</span><span class="sxs-lookup"><span data-stu-id="8715f-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="8715f-146">您可以透過執行 `certmgr.msc` 來開啟憑證存放區，以查看新建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="8715f-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="8715f-147">NuGet.org 不接受使用自動發行憑證簽署的套件。</span><span class="sxs-lookup"><span data-stu-id="8715f-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="8715f-148">在 NuGet.org 上管理您套件的簽署需求</span><span class="sxs-lookup"><span data-stu-id="8715f-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="8715f-149">[登入](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) NuGet.org。</span><span class="sxs-lookup"><span data-stu-id="8715f-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="8715f-150">前往 `Manage Packages` 
   ![設定套件簽署者](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="8715f-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="8715f-151">若您為套件的唯一擁有者，那麼您就是必要的簽署者，這表示您可以使用任何已註冊憑證，來簽署自己的套件並發佈至 NuGet.org。</span><span class="sxs-lookup"><span data-stu-id="8715f-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="8715f-152">根據預設，若套件擁有多位擁有者，則 [任何] 擁有者的憑證都可以用來簽署套件。</span><span class="sxs-lookup"><span data-stu-id="8715f-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="8715f-153">作為套件的共同擁有者，您可以將 [任何] 覆寫為自己或其他共同擁有者，使其成為必要簽署者。</span><span class="sxs-lookup"><span data-stu-id="8715f-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="8715f-154">如果您讓不具任何已註冊憑證的人員成為擁有者，會允許未簽署的套件。</span><span class="sxs-lookup"><span data-stu-id="8715f-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="8715f-155">同樣地，若已為套件選取預設的 [任何] 選項，而該套件的其中一位擁有者具有已註冊憑證，但另一位則不具任何已註冊憑證，則不論是簽章由其中一位擁有者註冊的已簽署套件，或是未簽署的套件，NuGet.org 都會接受 (因為其中一位擁有者不具任何已註冊憑證)。</span><span class="sxs-lookup"><span data-stu-id="8715f-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="8715f-156">相關文章</span><span class="sxs-lookup"><span data-stu-id="8715f-156">Related articles</span></span>

- [<span data-ttu-id="8715f-157">管理套件的信任界限</span><span class="sxs-lookup"><span data-stu-id="8715f-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="8715f-158">簽署的套件參考</span><span class="sxs-lookup"><span data-stu-id="8715f-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
