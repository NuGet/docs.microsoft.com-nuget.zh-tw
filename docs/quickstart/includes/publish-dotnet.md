---
ms.openlocfilehash: 9167b4b5943dd797c5a4cb20e53ee6832f0b3021
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623017"
---
1. <span data-ttu-id="c770c-101">變更為包含 `.nupkg` 檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c770c-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="c770c-102">執行下列命令，指定套件名稱 (使用套件識別碼) 並使用您的 API 金鑰來取代金鑰值：</span><span class="sxs-lookup"><span data-stu-id="c770c-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg --api-key qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 --source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="c770c-103">dotnet 會顯示發行程序的結果：</span><span class="sxs-lookup"><span data-stu-id="c770c-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="c770c-104">請參閱 [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push)。</span><span class="sxs-lookup"><span data-stu-id="c770c-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>