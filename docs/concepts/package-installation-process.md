---
title: 安裝套件時會發生什麼事？
description: 套件安裝程序的詳細資訊
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 634c421499b06f6b62d88a95f8703614dec5ace8
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699758"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>安裝 NuGet 套件時會發生什麼事？

簡單地說，不同的 NuGet 工具通常會在專案檔或 `packages.config` 中建立套件的參考，然後執行套件還原，從而有效地安裝套件。 例外狀況是 `nuget install`，它只會將套件展開到 `packages` 資料夾，且不會修改其他任何檔案。

一般程序如下：

1. (除 `nuget.exe` 外的所有工具) 將套件識別碼和版本記錄到專案檔或 `packages.config` 中。

   如果安裝工具是 Visual Studio 或 dotnet CLI，則工具會先嘗試安裝套件。 如果不相容，則套件不會新增至專案檔或 `packages.config`。

2. 取得套件：
   - 檢查套件 (依據確切的識別碼和版本號碼) 是否已安裝在 *global-packages* 資料夾中，如 [管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。

   - 如果套件不在 [ *全域封裝* ] 資料夾中，請嘗試從 [設定檔](../consume-packages/Configuring-NuGet-Behavior.md)中所列的來源抓取。 針對線上來源，除非已使用 `nuget.exe` 命令指定 `-NoCache`，或已使用 `dotnet restore` 指定 `--no-cache`，否則會先嘗試從 HTTP 快取擷取套件。  (Visual Studio，且 `dotnet add package` 一律使用快取。 ) 如果從快取使用封裝，輸出中就會出現 "cache"。 快取的到期時間為 30 分鐘。

   - 如果封裝是使用 [浮動版本](../consume-packages/Package-References-in-Project-Files.md#floating-versions)指定，或沒有最低版本，則 NuGet *會* 聯繫所有來源，以找出最符合的結果。
   範例： `1.*` ， `(, 2.0.0]` 。

   - 如果套件不在 HTTP 快取中，則會嘗試從組態中所列的來源下載套件。 如果已下載套件，輸出中會出現 "GET" 和 "OK"。 NuGet 會記錄正常詳細程度的 HTTP 流量。

   - 如果無法從任何來源成功取得套件，此時安裝會失敗，並出現錯誤，例如 [NU1103](../reference/errors-and-warnings/NU1103.md)。 請注意，來自 `nuget.exe` 命令的錯誤只會顯示所檢查的最後一個來源，但表示無法從任何來源使用套件。

   取得套件時，可能套用 NuGet 組態中的來源順序為：

   - NuGet 會先檢查來源本機資料夾和網路共用，然後才檢查 HTTP 來源。

3. 將套件複本和其他資訊儲存在 *http-cache* 資料夾中，如 [管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。

4. 如果已下載，則將套件安裝到每個使用者的 *global-packages* 資料夾中。 NuGet 會針對每個套件識別碼建立子資料夾，然後針對每個已安裝的套件版本建立子資料夾。

5. NuGet 會視需要安裝套件相依性。 此程序可能更新流程中的套件版本，如[相依性解析](../concepts/dependency-resolution.md)中所述。

6. 更新其他專案檔和資料夾：

    - 針對使用 PackageReference 的專案，更新儲存在 `obj/project.assets.json` 中的套件相依性關係圖。 套件內容本身不會複製到任何專案資料夾中。
    - 如果套件使用[來源和組態檔轉換](../create-packages/source-and-config-file-transformations.md)，則更新 `app.config` 和/或 `web.config`。

7. (僅限 Visual Studio) 在 Visual Studio 視窗中顯示套件的讀我檔案 (如果有的話)。

使用 NuGet 套件享受具生產力的程式碼！
