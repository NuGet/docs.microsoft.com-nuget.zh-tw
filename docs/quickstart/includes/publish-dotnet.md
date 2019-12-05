---
ms.openlocfilehash: 1df35c96124584bddbe58b8dd6587e3fff256ef9
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825303"
---
1. <span data-ttu-id="411b8-101">變更為包含 `.nupkg` 檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="411b8-101">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="411b8-102">執行下列命令，指定套件名稱 (使用套件識別碼) 並使用您的 API 金鑰來取代金鑰值：</span><span class="sxs-lookup"><span data-stu-id="411b8-102">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```dotnetcli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="411b8-103">dotnet 會顯示發行程序的結果：</span><span class="sxs-lookup"><span data-stu-id="411b8-103">dotnet displays the results of the publishing process:</span></span>

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

<span data-ttu-id="411b8-104">請參閱 [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push)。</span><span class="sxs-lookup"><span data-stu-id="411b8-104">See [dotnet nuget push](/dotnet/core/tools/dotnet-nuget-push).</span></span>