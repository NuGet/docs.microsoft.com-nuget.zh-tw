---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495999"
---
<span data-ttu-id="06985-101">來自 `push` 命令的錯誤通常代表發生問題。</span><span class="sxs-lookup"><span data-stu-id="06985-101">Errors from the `push` command typically indicate the problem.</span></span> <span data-ttu-id="06985-102">例如，您可能忘記更新專案中的版本號碼，因而嘗試發行已經存在的套件。</span><span class="sxs-lookup"><span data-stu-id="06985-102">For example, you may have forgotten to update the version number in your project and are therefore trying to publish a package that already exists.</span></span>

<span data-ttu-id="06985-103">當您嘗試使用主機上已經存在的識別碼來發行套件時，也會看到錯誤。</span><span class="sxs-lookup"><span data-stu-id="06985-103">You also see errors when trying to publish a package using an identifier that already exists on the host.</span></span> <span data-ttu-id="06985-104">例如，名稱 "AppLogger" 已經存在。</span><span class="sxs-lookup"><span data-stu-id="06985-104">The name "AppLogger", for example, already exists.</span></span> <span data-ttu-id="06985-105">在這種情況下，`push` 命令會產生下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="06985-105">In such a case, the `push` command gives the following error:</span></span>

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

<span data-ttu-id="06985-106">如果您使用剛建立的有效 API 金鑰，則此訊息表示命名衝突，這無法從錯誤的「權限」部分中完全清除。</span><span class="sxs-lookup"><span data-stu-id="06985-106">If you're using a valid API key that you just created, then this message indicates a naming conflict, which isn't entirely clear from the "permission" part of the error.</span></span> <span data-ttu-id="06985-107">請變更套件識別碼、重新建置專案、重新建立 `.nupkg` 檔案，然後重試 `push` 命令。</span><span class="sxs-lookup"><span data-stu-id="06985-107">Change the package identifier, rebuild the project, recreate the `.nupkg` file, and retry the `push` command.</span></span>