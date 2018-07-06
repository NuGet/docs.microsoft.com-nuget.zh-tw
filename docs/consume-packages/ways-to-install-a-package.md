---
title: 安裝 NuGet 套件的方式
description: 描述將 NuGet 套件安裝到專案的程序，包括在磁碟上及適用的專案檔會發生什麼情況。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 0f59c3b7f1e32ae34889921c13d15074ef5c1260
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843377"
---
# <a name="different-ways-to-install-a-nuget-package"></a>安裝 NuGet 套件的不同方式

NuGet 套件會使用下表中的任一種方法來下載並安裝 (如果您尚未安裝這些項目，請參閱[安裝 NuGet 用戶端工具](../install-nuget-client-tools.md))。 套件可能會從快取擷取而不是下載。

| 方法 | 描述 |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet add package <package_name>` | (所有平台) 擷取 \<package_name\> 所識別的套件、在目前目錄的資料夾中展開其內容，並將參考新增到專案檔。 此外，也會擷取並安裝相依性。<ul><li>[安裝並使用套件 (dotnet CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[dotnet add package 命令](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| 套件管理員 UI (Visual Studio) | (Windows 和 Mac) 提供 UI，透過該 UI 可從指定套件來源瀏覽、選取套件及其相依性並安裝至專案。 將對於已安裝套件的參考新增至專案檔。<ul><li>[安裝並使用套件 (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[套件管理員 UI 參考 (Windows)](../tools/package-manager-ui.md)</li><li>[在專案中包含 NuGet 套件 (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| 套件管理員主控台 (Visual Studio)<br/>`Install-Package <package_name>` | (僅限 Windows) 從所選來源擷取 \<package_name\> 所識別的套件並安裝到方案中的指定專案，然後將參考新增到專案檔。 此外，也會擷取並安裝相依性。<ul><li>[安裝並使用套件 (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[套件管理員主控台指南](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (所有平台) 擷取 \<package_name\> 所識別的套件，並在目前目錄的資料夾中展開其內容；也可以擷取 `packages.config` 檔案中列出的所有套件。 另外也會擷取並安裝相依性，但不會對專案檔或 `packages.config` 進行任何變更。<ul><li>[安裝命令](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>安裝套件後會發生什麼事

簡單地說，不同的 NuGet 工具通常會在專案檔或 `packages.config` 中建立套件的參考，然後執行套件還原，從而有效地安裝套件。 例外狀況是 `nuget install`，它只會將套件展開到 `packages` 資料夾，且不會修改其他任何檔案。

一般程序如下：

1. (除 `nuget.exe` 外的所有工具) 將套件識別碼和版本記錄到專案檔或 `packages.config` 中。

2. 取得套件：
   - 檢查套件 (依據確切的識別碼和版本號碼) 是否已安裝在 *global-packages* 資料夾中，如[管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中所述。

   - 如果套件不在 *global-packages* 資料夾中，則會嘗試從[組態檔](Configuring-NuGet-Behavior.md)中所列的來源擷取套件。 對於線上來源，除非已使用 `nuget.exe` 命令指定 `-NoCache`，或已使用 `dotnet restore` 指定 `--no-cache`，否則會先嘗試從快取擷取套件。 (Visual Studio 和 `dotnet add package` 一律使用快取。)如果是從快取使用套件，則輸出中會出現 "CACHE"。 快取的到期時間為 30 分鐘。

   - 如果套件不在快取中，則會嘗試從組態中所列的來源下載套件。 如果已下載套件，輸出中會出現 "GET" 和 "OK"。

   - 如果無法從任何來源成功取得套件，此時安裝會失敗，並出現錯誤，例如 [NU1103](../reference/errors-and-warnings/NU1103.md)。 請注意，來自 `nuget.exe` 命令的錯誤只會顯示所檢查的最後一個來源，但表示無法從任何來源使用套件。

   取得套件時，可能套用 NuGet 組態中的來源順序為：

   - 若為使用 PackageReference 格式的專案，NuGet 先檢查來源本機資料夾和網路共用，然後才檢查 HTTP 來源。

   - 若為使用 `packages.config` 管理格式的專案，NuGet 會使用組態中的來源順序。 例外狀況是還原作業，在此情況下，會忽略來源順序，而且 NuGet 會使用先回應之來源的套件。

   - 一般而言，NuGet 檢查來源的順序並不重要，因為不管來源為何，只要套件具有相同的識別碼和版本號碼，便會是完全相同的套件。

3. (除 `nuget.exe` 外的所有工具) 將套件複本和其他資訊儲存在 *http-cache* 資料夾中，如[管理全域套件和快取資料夾](managing-the-global-packages-and-cache-folders.md)中所述。

4. 如果已下載，則將套件安裝到每個使用者的 *global-packages* 資料夾中。 NuGet 會針對每個套件識別碼建立子資料夾，然後針對每個已安裝的套件版本建立子資料夾。

5. 更新其他專案檔和資料夾：

    - 針對使用 PackageReference 的專案，更新儲存在 `obj/project.assets.json` 中的套件相依性關係圖。 套件內容本身不會複製到任何專案資料夾中。
    - 針對使用 `packages.config` 的專案，將符合專案之目標 Framework 的那些已展開套件部分複製到專案的 `packages` 資料夾中。 (當使用 `nuget install` 時，會複製整個已展開的套件，因為 `nuget.exe` 不會檢查專案檔來識別目標 Framework。)
    - 如果套件使用[來源和組態檔轉換](../create-packages/source-and-config-file-transformations.md)，則更新 `app.config` 和/或 `web.config`。

6. 安裝任何下層相依性 (若專案中尚未存在)。 此程序可能更新流程中的套件版本，如[相依性解析](../consume-packages/dependency-resolution.md)中所述。

7. (僅限 Visual Studio) 在 Visual Studio 視窗中顯示套件的讀我檔案 (如果有的話)。

## <a name="related-articles"></a>相關文章

- [套件耗用量的概觀及工作流程](../consume-packages/overview-and-workflow.md)
- [尋找及選擇套件](../consume-packages/finding-and-choosing-packages.md)
- [管理 NuGet 快取和 global-packages 資料夾](managing-the-global-packages-and-cache-folders.md)
- [設定 NuGet 行為](../consume-packages/configuring-nuget-behavior.md)
