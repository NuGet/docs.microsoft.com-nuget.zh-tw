---
title: 簽署的套件
description: NuGet 套件簽署的需求。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 85fdf7a41cc033d92bbd0326648142aec27a9970
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508796"
---
# <a name="signed-packages"></a>已簽署的套件

*NuGet 4.6.0 + 和 Visual Studio 2017 15.6 版和更新版本*

NuGet 套件可以包含數位簽章，以防止遭篡改的內容受到保護。 此簽章是從 x.509 憑證產生的，也會將真品證明證明新增至封裝的實際來源。

簽署的套件提供最強的端對端驗證。 有兩種不同類型的 NuGet 簽章：
- **作者簽名**。 作者簽名碼可保證在作者簽署套件之後，封裝未經過修改，不論是從哪個存放庫或封裝的傳輸方法傳遞。 此外，作者簽署的套件會提供額外的驗證機制給 nuget.org 發佈管線，因為簽署憑證必須事先註冊。 如需詳細資訊，請參閱 [註冊憑證](#signature-requirements-on-nugetorg)。
- 存放 **庫簽** 章。 存放庫簽章會針對存放庫中的 **所有** 套件提供完整性保證（不論其是否為作者簽署），即使這些套件是從與其簽署來源的原始存放庫不同的位置取得。   

如需建立作者簽署套件的詳細資訊，請參閱 [簽署封裝](../create-packages/Sign-a-package.md) 和 [nuget sign 命令](../reference/cli-reference/cli-ref-sign.md)。 您可以使用 [dotnet nuget 驗證](/dotnet/core/tools/dotnet-nuget-verify) 或 [nuget 驗證](../reference/cli-reference/cli-ref-verify.md) 命令來確認套件的簽章。

> [!Important]
> 目前只有 Windows 上的 nuget.exe 才支援作者簽署套件。 不過，所有上傳至 nuget.org 的套件都會自動簽署儲存機制。

## <a name="certificate-requirements"></a>憑證需求

套件簽署需要程式碼簽署憑證，這是一種特殊類型的憑證，適用于 `id-kp-codeSigning` 目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證的 RSA 公開金鑰長度必須是2048位或更高。

## <a name="timestamp-requirements"></a>時間戳記需求

簽署的套件應包含 RFC 3161 時間戳記，以確保簽章的有效性超過套件簽署憑證的有效期間。 用來簽署時間戳記的憑證必須適用于 `id-kp-timeStamping` 目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證的 RSA 公開金鑰長度必須是2048位或更高。

您可以在 (GitHub) 的套件簽章 [技術規格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) 中找到其他技術詳細資料。

## <a name="signature-requirements-on-nugetorg"></a>NuGet.org 上的特徵標記需求

nuget.org 具有接受已簽署套件的其他需求：

- 主要簽章必須是作者簽章。
- 主要簽章必須有單一有效的時間戳記。
- 作者簽名和其時間戳記簽章的 x.509 憑證：
  - 必須有 RSA 公開金鑰2048位或更高的版本。
  - 在 nuget.org 上的套件驗證期間，每個目前的 UTC 時間都必須在其有效期間內。
  - 必須連結至 Windows 上預設受信任的受根信任授權單位。 已拒絕使用自我發行憑證簽署的套件。
  - 必須適用于其用途： 
    - 作者簽署憑證必須適用于程式碼簽署。
    - 時間戳記憑證必須是有效的時間戳記。
  - 不得在簽署時撤銷。  (這可能不會在提交時 knowable，因此 nuget.org 會定期重新檢查撤銷狀態) 。
  
  
## <a name="related-articles"></a>相關文章

- [簽署 NuGet 套件](../create-packages/Sign-a-Package.md)
- [使用 dotnet CLI 驗證已簽署的套件](/dotnet/core/tools/dotnet-nuget-verify)
- [使用 nuget.exe驗證已簽署的套件 ](../reference/cli-reference/cli-ref-verify.md)
- [管理套件的信任界限](../consume-packages/installing-signed-packages.md)
