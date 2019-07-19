---
title: 從 config.xml 遷移至 PackageReference 格式
description: 有關如何將專案從 config.xml 管理格式遷移至 PackageReference 的詳細資料, 如 NuGet 4.0 + 和 VS2017 和 .NET Core 2.0 所支援
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 39f260835989cbbcc7293d9db27ac7b2c32debaa
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317227"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>從封裝中遷移至 PackageReference

Visual Studio 2017 15.7 與更新版本支援將專案從 [packages.config](./packages-config.md) 管理格式移轉為 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 格式。

## <a name="benefits-of-using-packagereference"></a>使用 PackageReference 的優點

* **在一個位置管理所有專案**相依性:就像專案對專案參考和元件參考一樣, NuGet 套件參考 (使用`PackageReference`節點) 會直接在專案檔內進行管理, 而不是使用個別的封裝 .config 檔案。
* **最上層相依性的整齊觀點**:不同于 PackageReference, 您只會列出直接安裝在專案中的 NuGet 套件。 因此, NuGet 套件管理員 UI 和專案檔不會隨著下層相依性而變得雜亂。
* **效能改進**:使用 PackageReference 時, 套件會保留在*全域封裝*資料夾中 (如[管理全域套件和](../consume-packages/managing-the-global-packages-and-cache-folders.md)快取資料夾, 而不是解決方案中的`packages`資料夾中所述)。 因此, PackageReference 的執行速度較快, 且耗用的磁碟空間較少。
* **對相依性和內容流程進行細微控制**:使用 MSBuild 的現有功能, 可讓您有[條件地參考 NuGet 套件](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition), 並選擇每個目標 framework、設定、平臺或其他軸的套件參考。
* **PackageReference 正處於開發階段**:請參閱[GitHub 上的 PackageReference 問題](https://aka.ms/nuget-pr-improvements)。 封裝已不再進行開發。

### <a name="limitations"></a>限制

* Visual Studio 2015 和更早版本中未提供 NuGet PackageReference。 只可以在 Visual Studio 2017 中開啟已移轉的專案。
* 移轉目前不適用於 C++ 和 ASP.NET 專案。
* 某些套件可能無法與 PackageReference 完全相容。 如需詳細資訊, 請參閱[套件相容性問題](#package-compatibility-issues)。

### <a name="known-issues"></a>已知問題

1. 滑鼠右鍵快顯功能表中無法使用 `Migrate packages.config to PackageReference...` 選項 

#### <a name="issue"></a>問題 
 
當專案第一次開啟時，直到執行 NuGet 作業之前，NuGet 可能不會初始化。 這會造成移轉選項不會顯示在 `packages.config` 或 `References` 的滑鼠右鍵快顯功能表中。 

#### <a name="workaround"></a>因應措施 

執行以下任何一個 NuGet 動作： 
* 開啟 [套件管理員] UI - 在 `References` 上按一下滑鼠右鍵，並選取 `Manage NuGet Packages...` 
* 開啟 [套件管理員] 主控台 - 從 `Tools > NuGet Package Manager` 選取 `Package Manager Console` 
* 執行 NuGet 還原 - 在 [方案總管] 中的方案節點上按一下滑鼠右鍵，並選取 `Restore NuGet Packages` 
* 建置專案也會觸發 NuGet 還原 

您現在應該可以看到移轉選項。 請注意，ASP.NET 和 C++ 專案類型不支援且不顯示此選項。 

## <a name="migration-steps"></a>遷移步驟

> [!Note]
> 開始遷移之前, Visual Studio 會建立專案的備份, 以允許您在必要時[復原到 config.xml。](#how-to-roll-back-to-packagesconfig)

1. 使用`packages.config`開啟包含專案的方案。

1. 在**方案總管**中, 以滑鼠右鍵按一下 [**參考**] `packages.config`節點或檔案, 然後選取 [**將 PackageReference 遷移至**]。

1. 遷移程式會分析專案的 NuGet 套件參考, 並嘗試將它們分類成**最上層**相依性 (您直接安裝的 nuget 套件) 和可**轉移**的相依性 (已安裝為的套件最上層套件的相依性)。

   > [!Note]
   > PackageReference 支援可轉移的套件還原並動態解析相依性, 這表示不需要明確安裝可轉移的相依性。

1. 選擇性您可以選取封裝的**最上層**選項, 將 NuGet 套件分類為可轉移的相依性, 做為最上層的相依性。 此選項會針對包含不是以可轉移方式 (在`build`、 `buildCrossTargeting`、 `contentFiles`或`analyzers`資料夾中) 的資產, 以及標示為開發相依性 (`developmentDependency = "true"`) 的套件進行自動設定。

1. 檢查任何[套件相容性問題](#package-compatibility-issues)。

1. 選取 **[確定]** 開始進行遷移。

1. 在遷移結束時, Visual Studio 會提供一份報告, 其中包含備份的路徑、已安裝的套件清單 (最上層的相依性)、參考為可轉移相依性的套件清單, 以及在開頭移動. 報表會儲存至 [備份] 資料夾。

1. 驗證解決方案是否已建立並執行。 如果您遇到問題, 請[在 GitHub 上提出問題](https://github.com/NuGet/Home/issues/)。

## <a name="how-to-roll-back-to-packagesconfig"></a>如何回復為封裝 .config

1. 關閉已遷移的專案。

1. 將專案檔和`packages.config`備份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`是) 複製到專案資料夾。 刪除 obj 資料夾 (如果它存在於專案根目錄中)。

1. 開啟專案。

1. 使用 **工具 > NuGet 套件管理員 > 套件管理員主控台** 功能表命令來開啟 套件管理員主控台。

1. 在主控台中執行下列命令:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>在遷移後建立封裝

完成遷移之後, 建議您新增[nuget.exe](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget 封裝的參考, 然後使用[msbuild-t:pack](../reference/msbuild-targets.md#pack-target)來建立封裝, 以建立套件。 雖然在某些情況下`dotnet.exe pack` `msbuild -t:pack`, 您可以使用而不是, 但不建議這麼做。

## <a name="package-compatibility-issues"></a>套件相容性問題

PackageReference 中不支援某些在套件中支援的部分。 遷移會分析並偵測此類問題。 有一或多個下列問題的任何套件, 在遷移之後可能不會如預期般運作。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>在遷移之後安裝套件時, 會忽略 "install. ps1" 腳本

| | |
| --- | --- |
| **描述** | 使用 PackageReference 時, 請安裝 ps1 並卸載。在安裝或卸載套件時, 不會執行此 PowerShell 腳本。 |
| **可能的影響** | 相依于這些腳本以在目的專案中設定某些行為的封裝, 可能無法如預期般運作。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>在遷移之後安裝套件時, 無法使用「內容」資產

| | |
| --- | --- |
| **描述** | 套件的`content`資料夾中不支援使用 PackageReference 的資產, 而且會予以忽略。 PackageReference 新增的支援`contentFiles` , 以獲得更好的可轉移支援和共用內容。  |
| **可能的影響** | 中的`content`資產不會複製到專案和專案程式碼中, 而相依于那些資產是否需要重構。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>升級後安裝套件時, 不會套用 XDT 轉換

| | |
| --- | --- |
| **描述** | XDT 轉換不支援 PackageReference, 而且在`.xdt`安裝或卸載套件時, 會忽略檔案。   |
| **可能的影響** | XDT 轉換不會套用至任何專案 XML 檔案, 最常見的`web.config.install.xdt`是`web.config.uninstall.xdt`和, 這表示當安裝` web.config`或卸載封裝時, 不會更新專案的檔案。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>在遷移之後安裝套件時, 會忽略 lib 根中的元件

| | |
| --- | --- |
| **描述** | 使用 PackageReference 時, 會忽略不含目標`lib` framework 特定子資料夾的資料夾根目錄中所出現的元件。 NuGet 會尋找符合與專案的目標架構對應的目標 framework 標記 (TFM) 的子資料夾, 並將相符的元件安裝到專案中。 |
| **可能的影響** | 沒有子資料夾符合對應于專案目標 framework 的目標 framework 標記 (TFM) 的封裝, 在遷移期間轉換或安裝失敗後, 可能無法如預期般運作 |

## <a name="found-an-issue-report-it"></a>發現問題嗎？ 報表!

如果您遇到遷移體驗的問題, 請[在 NuGet GitHub 存放庫](https://github.com/NuGet/Home/issues/)中提出問題。
