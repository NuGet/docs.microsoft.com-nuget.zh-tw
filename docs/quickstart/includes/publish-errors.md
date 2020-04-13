---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495999"
---
來自 `push` 命令的錯誤通常代表發生問題。 例如，您可能忘記更新專案中的版本號碼，因而嘗試發行已經存在的套件。

當您嘗試使用主機上已經存在的識別碼來發行套件時，也會看到錯誤。 例如，名稱 "AppLogger" 已經存在。 在這種情況下，`push` 命令會產生下列錯誤：

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

如果您使用剛建立的有效 API 金鑰，則此訊息表示命名衝突，這無法從錯誤的「權限」部分中完全清除。 請變更套件識別碼、重新建置專案、重新建立 `.nupkg` 檔案，然後重試 `push` 命令。