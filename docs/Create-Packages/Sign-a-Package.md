---
title: "簽署 NuGet 套件 | Microsoft Docs"
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "說明已簽署套件如何用於啟用內容完整性驗證。"
keywords: "NuGet 套件簽署、NuGet 安全性、建立已簽署的套件"
ms.reviewer:
- karann-msft
- anangaur
ms.openlocfilehash: aaf6ab7d7a9e66d4d9519d8aa79f0d0fac646d3a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="fa9db-104">簽署 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="fa9db-104">Signing NuGet Packages</span></span>

<span data-ttu-id="fa9db-105">簽署套件是可確保套件自建立後未曾受到修改的程序。</span><span class="sxs-lookup"><span data-stu-id="fa9db-105">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa9db-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="fa9db-106">Prerequisites</span></span>

1. <span data-ttu-id="fa9db-107">要簽署的套件 (`.nupkg` 檔案)。</span><span class="sxs-lookup"><span data-stu-id="fa9db-107">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="fa9db-108">請參閱[建立套件](creating-a-package.md)。</span><span class="sxs-lookup"><span data-stu-id="fa9db-108">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="fa9db-109">nuget.exe 4.6.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fa9db-109">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="fa9db-110">請參閱如何[安裝 NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli)。</span><span class="sxs-lookup"><span data-stu-id="fa9db-110">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="fa9db-111">[程式碼簽署憑證](../reference/signed-packages-reference.md#get-a-code-signing-certificate)。</span><span class="sxs-lookup"><span data-stu-id="fa9db-111">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="fa9db-112">nuget.org 目前不接受簽署的套件。</span><span class="sxs-lookup"><span data-stu-id="fa9db-112">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="fa9db-113">您可以簽署套件以發佈至自訂摘要。</span><span class="sxs-lookup"><span data-stu-id="fa9db-113">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="fa9db-114">簽署套件</span><span class="sxs-lookup"><span data-stu-id="fa9db-114">Sign a package</span></span>

<span data-ttu-id="fa9db-115">若要簽署套件，請使用 [nuget sign](../tools/cli-ref-sign.md)：</span><span class="sxs-lookup"><span data-stu-id="fa9db-115">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="fa9db-116">如命令參考所述，您可以使用憑證存放區中可用的憑證，或使用檔案中的憑證。</span><span class="sxs-lookup"><span data-stu-id="fa9db-116">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="fa9db-117">簽署套件時的常見問題</span><span class="sxs-lookup"><span data-stu-id="fa9db-117">Common problems when signing a package</span></span>

- <span data-ttu-id="fa9db-118">此憑證對於程式碼簽署無效。</span><span class="sxs-lookup"><span data-stu-id="fa9db-118">The certificate is not valid for code signing.</span></span> <span data-ttu-id="fa9db-119">您必須確認指定的憑證具有適當的增強金鑰使用方法 (EKU 1.3.6.1.5.5.7.3.3)。</span><span class="sxs-lookup"><span data-stu-id="fa9db-119">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="fa9db-120">憑證不符合基本需求，例如 RSA SHA-256 簽章演算法，或 2048 或更高位元的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="fa9db-120">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="fa9db-121">憑證已過期或已撤銷。</span><span class="sxs-lookup"><span data-stu-id="fa9db-121">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="fa9db-122">時間戳記伺服器不符合憑證需求。</span><span class="sxs-lookup"><span data-stu-id="fa9db-122">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="fa9db-123">簽署的套件應包含時間戳記，以確定簽署憑證過期時，簽章仍保持有效。</span><span class="sxs-lookup"><span data-stu-id="fa9db-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="fa9db-124">簽署不含時間戳記時，簽署作業會產生 [NU3002 警告](../reference/Errors-and-Warnings.md#nu3002)。</span><span class="sxs-lookup"><span data-stu-id="fa9db-124">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="fa9db-125">驗證簽署的套件</span><span class="sxs-lookup"><span data-stu-id="fa9db-125">Verify a signed package</span></span>

<span data-ttu-id="fa9db-126">使用 [nuget verify](../tools/cli-ref-verify.md)以查看特定套件的簽章詳細資料：</span><span class="sxs-lookup"><span data-stu-id="fa9db-126">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="fa9db-127">安裝簽署的套件</span><span class="sxs-lookup"><span data-stu-id="fa9db-127">Install a signed package</span></span>

<span data-ttu-id="fa9db-128">簽署的套件不需要安裝任何特定動作；不過，如果內容在簽署後已經過修改，就會封鎖安裝並產生 [NU3008 錯誤](../reference/Errors-and-Warnings.md#nu3008)。</span><span class="sxs-lookup"><span data-stu-id="fa9db-128">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="fa9db-129">以不受信任的憑證簽署的套件，會視為未簽署，安裝時會如同其他未簽署的套件一樣不含任何警告或錯誤。</span><span class="sxs-lookup"><span data-stu-id="fa9db-129">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="fa9db-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fa9db-130">See also</span></span>

[<span data-ttu-id="fa9db-131">簽署的套件參考</span><span class="sxs-lookup"><span data-stu-id="fa9db-131">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
