---
title: 已簽署的套件
description: NuGet 套件簽署的需求。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 7384e8b30cb2ec5fe53ea0fe485858bc1f7b3c43
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428678"
---
# <a name="signed-packages"></a>已簽署的套件

*NuGet 4.6.0 + 和 Visual Studio 2017 15.6 版和更新版本*

NuGet 套件可以包含數位簽章，以提供保護來防止遭篡改的內容。 此簽章是從 x.509 憑證產生的，它也會將真實性證明新增至封裝的實際來源。

已簽署的套件提供最強的端對端驗證。 有兩種不同類型的 NuGet 簽章：
- **作者簽名**。 作者簽章可保證自作者簽署封裝後，封裝並未修改過，不論是從哪個存放庫或封裝的傳輸方法來傳遞。 此外，作者簽署的套件會針對 nuget.org 發佈管線提供額外的驗證機制，因為簽署憑證必須預先註冊。 如需詳細資訊，請參閱[註冊憑證](#signature-requirements-on-nugetorg)。
- 存放**庫簽**章。 存放庫簽章會針對存放庫中的**所有**套件提供完整性保證，不論它們是否為作者簽署，即使這些套件是從其簽署所在的原始存放庫以外的位置取得。   

如需建立作者簽署套件的詳細資訊，請參閱[簽署套件](../create-packages/Sign-a-package.md)和[nuget sign 命令](../reference/cli-reference/cli-ref-sign.md)。

> [!Important]
> 目前只有在 Windows 上使用 nuget.exe 時，才支援套件簽署。 [目前只有在 Windows 上使用 nuget.exe 或 Visual Studio 時，才支援已簽署套件的驗證](../reference/cli-reference/cli-ref-verify.md)。

## <a name="certificate-requirements"></a>憑證需求

套件簽署需要程式碼簽署憑證，這是一種特殊類型的憑證，適用于 `id-kp-codeSigning` 目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證的 RSA 公開金鑰長度必須為2048位或更高。

## <a name="timestamp-requirements"></a>時間戳記需求

已簽署的套件應包含 RFC 3161 時間戳記，以確保簽章的有效性超出封裝簽署憑證的有效期間。 用來簽署時間戳記的憑證必須是有效的 `id-kp-timeStamping` 目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證的 RSA 公開金鑰長度必須為2048位或更高。

如需其他技術詳細資料，請參閱套件簽章[技術規格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)（GitHub）。

## <a name="signature-requirements-on-nugetorg"></a>NuGet.org 上的簽章需求

nuget.org 對於接受已簽署的套件有額外的需求：

- 主要簽章必須是作者簽章。
- 主要簽章必須有單一有效的時間戳記。
- 撰寫簽章和其時間戳記簽章的 x.509 憑證：
  - 必須具有 RSA 公用金鑰2048位或更高版本。
  - 在 nuget.org 上的封裝驗證時，必須在其每個目前 UTC 時間的有效期間內。
  - 必須連結到 Windows 上預設信任的受根信任授權單位。 已使用自我發行憑證簽署的套件會遭到拒絕。
  - 必須是有效的目的： 
    - 作者簽署憑證必須有效，才能進行程式碼簽署。
    - 時間戳記憑證必須有效，以便於時間戳記。
  - 不得在簽署時撤銷。 （這在提交時可能不會 knowable，因此 nuget.org 會定期重新檢查撤銷狀態）。
  
  
## <a name="related-articles"></a>相關文章

- [簽署 NuGet 套件](../create-packages/Sign-a-Package.md)
- [管理套件的信任界限](../consume-packages/installing-signed-packages.md)
