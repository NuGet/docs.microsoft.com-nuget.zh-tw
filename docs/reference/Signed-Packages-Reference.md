---
title: 已簽署的套件
description: NuGet 封裝簽章需求。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 952256a24246543ecd4c37285cd001622aa2bc46
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426182"
---
# <a name="signed-packages"></a>已簽署的套件

*NuGet 4.6.0+ 和 Visual Studio 2017 15.6 版及更新版本*

NuGet 套件可以包含數位簽章可防止遭竄改的內容。 此簽章會產生來自 X.509 憑證，也將真實性證明，加上實際的套件來源。

已簽署的套件會提供最強的端對端驗證。 有兩種不同的 NuGet 簽章：
- **撰寫簽章**。 作者簽章可保證，封裝不之後已修改作者已登入的封裝，不論其儲存機制，或傳輸封裝傳遞的方法。 此外，作者簽署的套件提供額外的驗證機制以 nuget.org 發行管線，因為必須事先註冊簽署憑證。 如需詳細資訊，請參閱 <<c0> [ 登錄憑證](#signature-requirements-on-nugetorg)。
- **存放庫簽章**。 存放庫簽章提供完整性保證**所有**套件存放庫中，不論它們是作者帶正負號或不是，即使這些套件會取自原始它們所在的存放庫不同的位置帶正負號。   

如需建立作者已簽署的封裝的詳細資訊，請參閱 <<c0> [ 簽署封裝](../create-packages/Sign-a-package.md)並[nuget 登命令](../tools/cli-ref-sign.md)。

> [!Important]
> 目前支援封裝簽章，只有在 Windows 上使用 nuget.exe 時。 只有在 Windows 上使用 nuget.exe 或 Visual Studio 時，目前支援驗證的已簽署的套件。

## <a name="certificate-requirements"></a>憑證需求

封裝簽章需要程式碼簽署憑證，這是一種特別有效的憑證`id-kp-codeSigning`目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證必須具有 RSA 公用金鑰長度為 2048 位元或更高版本。

## <a name="timestamp-requirements"></a>時間戳記的需求

已簽署的套件應該包含 RFC 3161 時間戳記，以確保套件簽署憑證的有效期間以外的簽章有效性。 用來登入時間戳記的憑證必須適用於`id-kp-timeStamping`目的 [[RFC 5280 區段 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 此外，憑證必須具有 RSA 公用金鑰長度為 2048 位元或更高版本。

其他技術詳細資料可在[封裝簽章的技術規格](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。

## <a name="signature-requirements-on-nugetorg"></a>在 NuGet.org 上的簽章需求

nuget.org 具有接受已簽署的封裝的額外需求：

- 主要的簽章必須是作者簽章。
- 主要的簽章必須有單一有效的時間戳記。
- 作者簽章和其時間戳記簽章的 X.509 憑證：
  - 必須有 RSA 公開金鑰 2048 位元或更高。
  - 必須在每次目前的 UTC 時間的 nuget.org 上的 封裝驗證其有效期間內。
  - 必須鏈結至信任預設會在 Windows 上的受信任的根授權單位。 使用自我發行的憑證簽署的封裝會遭到拒絕。
  - 必須是有效的目的： 
    - 作者簽署憑證必須是有效簽署程式碼。
    - 時間戳記憑證必須是有效的時間戳記。
  - 必須不會撤銷在簽入時間。 （這可能不是 knowable 在提交時，所以 nuget.org 定期重新檢查撤銷狀態）。
  
  
## <a name="related-articles"></a>相關文章

- [簽署 NuGet 套件](../create-packages/Sign-a-Package.md)
- [管理封裝的信任界限](../consume-packages/installing-signed-packages.md)
