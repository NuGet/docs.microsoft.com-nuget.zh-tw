---
title: 簽署 NuGet 套件
description: 說明已簽署套件如何用於啟用內容完整性驗證。
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a469cbdd218a0e9c18950bb0d36faf4dbcb42a01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="cbd2b-103">簽署 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="cbd2b-103">Signing NuGet Packages</span></span>

<span data-ttu-id="cbd2b-104">簽署套件是可確保套件自建立後未曾受到修改的程序。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbd2b-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="cbd2b-105">Prerequisites</span></span>

1. <span data-ttu-id="cbd2b-106">要簽署的套件 (`.nupkg` 檔案)。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="cbd2b-107">請參閱[建立套件](creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="cbd2b-108">nuget.exe 4.6.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="cbd2b-109">請參閱如何[安裝 NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli)。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="cbd2b-110">[程式碼簽署憑證](../reference/signed-packages-reference.md#get-a-code-signing-certificate)。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="cbd2b-111">nuget.org 目前不接受簽署的套件。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-111">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="cbd2b-112">您可以簽署套件以發佈至自訂摘要。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-112">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="cbd2b-113">簽署套件</span><span class="sxs-lookup"><span data-stu-id="cbd2b-113">Sign a package</span></span>

<span data-ttu-id="cbd2b-114">若要簽署套件，請使用 [nuget sign](../tools/cli-ref-sign.md)：</span><span class="sxs-lookup"><span data-stu-id="cbd2b-114">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="cbd2b-115">如命令參考所述，您可以使用憑證存放區中可用的憑證，或使用檔案中的憑證。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-115">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="cbd2b-116">簽署套件時的常見問題</span><span class="sxs-lookup"><span data-stu-id="cbd2b-116">Common problems when signing a package</span></span>

- <span data-ttu-id="cbd2b-117">此憑證對於程式碼簽署無效。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-117">The certificate is not valid for code signing.</span></span> <span data-ttu-id="cbd2b-118">您必須確認指定的憑證具有適當的增強金鑰使用方法 (EKU 1.3.6.1.5.5.7.3.3)。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-118">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="cbd2b-119">憑證不符合基本需求，例如 RSA SHA-256 簽章演算法，或 2048 或更高位元的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-119">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="cbd2b-120">憑證已過期或已撤銷。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-120">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="cbd2b-121">時間戳記伺服器不符合憑證需求。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-121">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="cbd2b-122">簽署的套件應包含時間戳記，以確定簽署憑證過期時，簽章仍保持有效。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-122">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="cbd2b-123">簽署不含時間戳記時，簽署作業會產生 [NU3002 警告](../reference/Errors-and-Warnings.md#nu3002)。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-123">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="cbd2b-124">驗證簽署的套件</span><span class="sxs-lookup"><span data-stu-id="cbd2b-124">Verify a signed package</span></span>

<span data-ttu-id="cbd2b-125">使用 [nuget verify](../tools/cli-ref-verify.md)以查看特定套件的簽章詳細資料：</span><span class="sxs-lookup"><span data-stu-id="cbd2b-125">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="cbd2b-126">安裝簽署的套件</span><span class="sxs-lookup"><span data-stu-id="cbd2b-126">Install a signed package</span></span>

<span data-ttu-id="cbd2b-127">簽署的套件不需要安裝任何特定動作；不過，如果內容在簽署後已經過修改，就會封鎖安裝並產生 [NU3008 錯誤](../reference/Errors-and-Warnings.md#nu3008)。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-127">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="cbd2b-128">以不受信任的憑證簽署的套件，會視為未簽署，安裝時會如同其他未簽署的套件一樣不含任何警告或錯誤。</span><span class="sxs-lookup"><span data-stu-id="cbd2b-128">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="cbd2b-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cbd2b-129">See also</span></span>

[<span data-ttu-id="cbd2b-130">簽署的套件參考</span><span class="sxs-lookup"><span data-stu-id="cbd2b-130">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
