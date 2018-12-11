---
title: 安裝已簽署 NuGet 套件
description: 描述安裝已簽署 NuGet 套件及進行套件簽章信任設定的程序。
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977832"
---
# <a name="install-a-signed-package"></a><span data-ttu-id="9395f-103">安裝簽署的套件</span><span class="sxs-lookup"><span data-stu-id="9395f-103">Install a signed package</span></span>

<span data-ttu-id="9395f-104">已簽署套件不需要任何特定動作就能安裝；不過，如果內容在簽署後已經過修改，就會顯示錯誤 [NU3008](../reference/errors-and-warnings/NU3008.md) 並禁止安裝。</span><span class="sxs-lookup"><span data-stu-id="9395f-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="9395f-105">以不受信任的憑證簽署的套件，會視為未簽署，安裝時會如同其他未簽署的套件一樣不含任何警告或錯誤。</span><span class="sxs-lookup"><span data-stu-id="9395f-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="9395f-106">設定套件簽章需求</span><span class="sxs-lookup"><span data-stu-id="9395f-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="9395f-107">需要在 Windows 上安裝 NuGet 4.9.0+ 及 Visual Studio 15.9 或更新版本</span><span class="sxs-lookup"><span data-stu-id="9395f-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="9395f-108">您可以透過使用 [`nuget config`](../tools/cli-ref-config) 命令將 [nuget.config](../reference/nuget-config-file) 檔案中的 `signatureValidationMode` 設定為 `require`。</span><span class="sxs-lookup"><span data-stu-id="9395f-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file) file using the [`nuget config`](../tools/cli-ref-config) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="9395f-109">此模式會驗證所有的套件都是由 `nuget.config` 檔案中任何信任的憑證簽署。</span><span class="sxs-lookup"><span data-stu-id="9395f-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="9395f-110">此檔案讓您可依據憑證的指紋指定信任哪一個作者及 (或) 存放庫。</span><span class="sxs-lookup"><span data-stu-id="9395f-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="9395f-111">信任套件作者</span><span class="sxs-lookup"><span data-stu-id="9395f-111">Trust package author</span></span>

<span data-ttu-id="9395f-112">若要依據作者憑證信任套件，請使用 [`trusted-signers`](..tools/cli-ref-trusted-signers) 命令設定 nuget.config 中的 `author` 屬性。</span><span class="sxs-lookup"><span data-stu-id="9395f-112">To trust packages based on the author signature use the [`trusted-signers`](..tools/cli-ref-trusted-signers) command to set the `author` property in the nuget.config.</span></span>

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
><span data-ttu-id="9395f-113">使用 `nuget.exe` [verify command](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) (驗證命令) 以取得憑證指紋的 `SHA256` 值。</span><span class="sxs-lookup"><span data-stu-id="9395f-113">Use the `nuget.exe` [verify command](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="9395f-114">信任存放庫中所有的套件</span><span class="sxs-lookup"><span data-stu-id="9395f-114">Trust all packages from a repository</span></span>

<span data-ttu-id="9395f-115">若要依據存放庫簽章信任套件，請使用 `repository` 元素：</span><span class="sxs-lookup"><span data-stu-id="9395f-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="9395f-116">信任套件擁有者</span><span class="sxs-lookup"><span data-stu-id="9395f-116">Trust Package Owners</span></span>

<span data-ttu-id="9395f-117">存放庫簽章包含提交時判斷套件擁有者的其他中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9395f-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="9395f-118">您可以依據擁有者的清單從存放庫限制套件：</span><span class="sxs-lookup"><span data-stu-id="9395f-118">You can restrict packages from a repository based on a list of owners:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

<span data-ttu-id="9395f-119">若套件擁有多位擁有者，且受信任的清單中有其中一位擁有者，那麼就會成功安裝套件。</span><span class="sxs-lookup"><span data-stu-id="9395f-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="9395f-120">未受信任的根憑證</span><span class="sxs-lookup"><span data-stu-id="9395f-120">Untrusted Root certificates</span></span>

<span data-ttu-id="9395f-121">在某些情形下，您可能會想要使用未鏈結到本機電腦中受信任之根的憑證來啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="9395f-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="9395f-122">您可以使用 `allowUntrustedRoot` 屬性自訂此行為。</span><span class="sxs-lookup"><span data-stu-id="9395f-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="9395f-123">同步存放庫憑證</span><span class="sxs-lookup"><span data-stu-id="9395f-123">Sync repository certificates</span></span>

<span data-ttu-id="9395f-124">套件存放庫應宣告其在[服務所引](https://docs.microsoft.com/en-us/nuget/api/service-index)中使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="9395f-124">Package repositories should announce the certificates they use in their [service index](https://docs.microsoft.com/en-us/nuget/api/service-index).</span></span> <span data-ttu-id="9395f-125">不論如何，存放庫都會更新這些憑證，例如，當憑證到期時。</span><span class="sxs-lookup"><span data-stu-id="9395f-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="9395f-126">當發生這種情況時，使用特定原則的用戶端會需要更新組態以包含新增的憑證。</span><span class="sxs-lookup"><span data-stu-id="9395f-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="9395f-127">您可以使用 `nuget.exe` [受信任簽署者同步處理命令](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-)輕易地升級與存放庫建立關聯的受信任簽署者。</span><span class="sxs-lookup"><span data-stu-id="9395f-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="9395f-128">結構描述參考</span><span class="sxs-lookup"><span data-stu-id="9395f-128">Schema reference</span></span>

<span data-ttu-id="9395f-129">用戶端原則的完整結構描述參考可在 [nuget.config 參考](/nuget/reference/nuget-config-file#trustedsigners-section)中找到</span><span class="sxs-lookup"><span data-stu-id="9395f-129">The complete schema reference for the client policies can be found in the [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="9395f-130">相關文章</span><span class="sxs-lookup"><span data-stu-id="9395f-130">Related articles</span></span>

- [<span data-ttu-id="9395f-131">安裝 NuGet 套件的各種方式</span><span class="sxs-lookup"><span data-stu-id="9395f-131">Different ways to install a NuGet Package</span></span>](ways-to-install-a-package.md)
- [<span data-ttu-id="9395f-132">簽署 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="9395f-132">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="9395f-133">簽署的套件參考</span><span class="sxs-lookup"><span data-stu-id="9395f-133">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)