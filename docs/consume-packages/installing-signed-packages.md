---
title: 管理套件的信任界限
description: 描述安裝已簽署 NuGet 套件及進行套件簽章信任設定的程序。
author: JonDouglas
ms.author: jodou
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 596ce330e434253e6fb200aa59ae4e14d47779ed
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774811"
---
# <a name="manage-package-trust-boundaries"></a>管理套件的信任界限

已簽署套件不需要任何特定動作就能安裝；不過，如果內容在簽署後已經過修改，就會顯示錯誤 [NU3008](../reference/errors-and-warnings/NU3008.md) 並禁止安裝。

> [!Warning]
> 以不受信任的憑證簽署的套件，會視為未簽署，安裝時會如同其他未簽署的套件一樣不含任何警告或錯誤。

## <a name="configure-package-signature-requirements"></a>設定套件簽章需求

> [!Note]
> 需要在 Windows 上安裝 NuGet 4.9.0+ 及 Visual Studio 15.9 或更新版本

您可以透過使用 [`nuget config`](../reference/cli-reference/cli-ref-config.md) 命令將 [nuget.config](../reference/nuget-config-file.md) 檔案中的 `signatureValidationMode` 設定為 `require`。

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

此模式會驗證所有的套件都是由 `nuget.config` 檔案中任何信任的憑證簽署。 此檔案讓您可依據憑證的指紋指定信任哪一個作者及 (或) 存放庫。

### <a name="trust-package-author"></a>信任套件作者

若要根據作者簽章來信任封裝，請使用 [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) 命令來設定 `author` nuget.config 中的屬性。

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
>使用 `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) (驗證命令) 以取得憑證指紋的 `SHA256` 值。


### <a name="trust-all-packages-from-a-repository"></a>信任存放庫中所有的套件

若要依據存放庫簽章信任套件，請使用 `repository` 元素：

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>信任套件擁有者

存放庫簽章包含提交時判斷套件擁有者的其他中繼資料。 您可以依據擁有者的清單從存放庫限制套件：

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

若套件擁有多位擁有者，且受信任的清單中有其中一位擁有者，那麼就會成功安裝套件。

### <a name="untrusted-root-certificates"></a>未受信任的根憑證

在某些情形下，您可能會想要使用未鏈結到本機電腦中受信任之根的憑證來啟用驗證。 您可以使用 `allowUntrustedRoot` 屬性自訂此行為。

### <a name="sync-repository-certificates"></a>同步存放庫憑證

套件存放庫應宣告其在[服務所引](../api/service-index.md)中使用的憑證。 不論如何，存放庫都會更新這些憑證，例如，當憑證到期時。 當發生這種情況時，使用特定原則的用戶端會需要更新組態以包含新增的憑證。 您可以使用 `nuget.exe` [受信任簽署者同步處理命令](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name)輕易地升級與存放庫建立關聯的受信任簽署者。

### <a name="schema-reference"></a>結構描述參考

用戶端原則的完整結構描述參考可在 [nuget.config 參考](../reference/nuget-config-file.md#trustedsigners-section)中找到

## <a name="related-articles"></a>相關文章

- [簽署 NuGet 套件](../create-packages/Sign-a-Package.md)
- [簽署的套件參考](../reference/Signed-Packages-Reference.md)
