---
title: 從 package.config 移轉至 PackageReference 格式
description: 如何從 package.config 管理格式的專案移轉至 PackageReference 所支援之 NuGet 4.0 + 和 VS2017 及.NET Core 2.0 的詳細資料
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: b05192038bff071ca7a5b8f2e0f735696d09bef6
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508266"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>從 packages.config 移轉至 PackageReference

Visual Studio 2017 15.7 與更新版本支援將專案從 [packages.config](./packages-config.md) 管理格式移轉為 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 格式。

## <a name="benefits-of-using-packagereference"></a>使用 PackageReference 的優點

* **管理所有專案相依性，在同一個地方**： 就像專案對專案參考和組件參考，NuGet 套件參考 (使用`PackageReference`節點) 所管理直接在專案檔中，而不是使用個別packages.config 檔案。
* **最上層相依性的整齊的檢視**： 不同於 packages.config，PackageReference 會列出只有您在專案中直接安裝這些 NuGet 套件。 如此一來，NuGet 套件管理員 UI 和專案檔不被雜亂無章下層相依性。
* **效能改進**： 當使用 PackageReference 時，封裝會在維護*全域套件*資料夾 (在上所述[管理全域套件和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)而非在`packages`方案內的資料夾。 如此一來，PackageReference 執行速度快，並取用較少的磁碟空間。
* **妥善控制相依性和內容流動**： 使用 MSBuild 的現有功能可讓您[有條件地參考 NuGet 套件](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)選擇每個目標架構的套件參考和組態，平台或其他樞紐分析表。
* **PackageReference 正在進行開發**： 請參閱 < [PackageReference 問題在 GitHub 上](https://aka.ms/nuget-pr-improvements)。 packages.config 已不再進行開發。

### <a name="limitations"></a>限制

* NuGet PackageReference 不提供在 Visual Studio 2015 和更早版本。 可以只在 Visual Studio 2017 中開啟已移轉的專案。
* 找不到目前適用於 c + + 和 ASP.NET 專案的移轉。
* 有些封裝可能無法完全相容，使用 PackageReference。 如需詳細資訊，請參閱 <<c0> [ 封裝相容性問題](#package-compatibility-issues)。

### <a name="known-issues"></a>已知問題

1. 滑鼠右鍵快顯功能表中無法使用 `Migrate packages.config to PackageReference...` 選項 

#### <a name="issue"></a>問題 
 
當專案第一次開啟時，直到執行 NuGet 作業之前，NuGet 可能不會初始化。 這會造成移轉選項不會顯示在 `packages.config` 或 `References` 的滑鼠右鍵快顯功能表中。 

#### <a name="workaround"></a>因應措施 

執行下列 NuGet 動作的任何一個： 
* 開啟 [套件管理員] UI - 在 `References` 上按一下滑鼠右鍵，並選取 `Manage NuGet Packages...` 
* 開啟 [套件管理員] 主控台 - 從 `Tools > NuGet Package Manager` 選取 `Package Manager Console` 
* 執行 NuGet 還原 - 在 [方案總管] 中的方案節點上按一下滑鼠右鍵，並選取 `Restore NuGet Packages` 
* 建置專案也會觸發 NuGet 還原 

您現在應該可以看到移轉選項。 請注意，ASP.NET 和 C++ 專案類型不支援且不顯示此選項。 

## <a name="migration-steps"></a>移轉步驟

> [!Note]
> 開始移轉之前，Visual Studio 會建立專案可讓您一份[向前復原回到 packages.config](#how-to-roll-back-to-packagesconfig)如有必要。

1. 開啟包含專案所使用的方案`packages.config`。

1. 在 [**方案總管] 中**，以滑鼠右鍵按一下**參考**節點或`packages.config`檔案，然後選取**Packages.config na PackageReference...**.

1. 遷移程式會分析專案的 NuGet 套件參考，並嘗試對其進行分類**最上層相依性**（您在直接安裝 NuGet 套件） 和**可轉移相依性**（已安裝為最上層套件的相依性的套件）。

   > [!Note]
   > PackageReference 支援可轉移套件還原，並解析相依性，以動態方式表示，可轉移相依性需要不明確安裝。

1. （選擇性）您可以選擇將歸類為最上層相依性可轉移相依性，藉由選取 NuGet 套件**最上層**封裝的選項。 此選項會自動設定的套件，其中包含的資產，不會轉移流動 (中`build`， `buildCrossTargeting`， `contentFiles`，或`analyzers`資料夾)，且這些標示為開發相依性 (`developmentDependency = "true"`)。

1. 檢閱任何[封裝相容性問題](#package-compatibility-issues)。

1. 選取 **確定**即可開始移轉。

1. 在移轉結束時，Visual Studio，請提供備份，已安裝的套件 （最上層相依性） 的清單，做為可轉移的相依性，參考的套件清單的開頭所識別的相容性問題的清單的路徑與報表移轉。 報表會儲存到備份資料夾中。

1. 解決方案會建置並執行驗證。 如果您遇到問題，[在 GitHub 上提出問題](https://github.com/NuGet/Home/issues/)。

## <a name="how-to-roll-back-to-packagesconfig"></a>如何回復到 packages.config

1. 關閉已移轉的專案。

1. 將專案檔案複製並`packages.config`從備份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 至專案資料夾。 如果它存在於專案根目錄，請刪除了 obj 資料夾。

1. 開啟專案。

1. 開啟 Package Manager Console**工具 > NuGet 套件管理員 > Package Manager Console**功能表命令。

1. 在主控台中執行下列命令：

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>封裝相容性問題

不支援 PackageReference packages.config 中所支援的某些層面。 遷移程式會分析並偵測到這類問題。 任何具有一或多個下列問題的封裝可能無法如預期般在移轉之後。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>在移轉之後安裝該套件時，會忽略"install.ps1 」 指令碼

| | |
| --- | --- |
| **描述** | 使用 PackageReference install.ps1 和 uninstall.ps1 PowerShell 指令碼不會安裝或解除安裝套件時執行。 |
| **潛在影響** | 封裝相依於這些指令碼來設定目的地專案中的某些行為可能不會如預期運作。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>在移轉之後安裝該套件時，不提供 「 內容 」 的資產

| | |
| --- | --- |
| **描述** | 在封裝中的資產`content`資料夾不支援 PackageReference，而且會忽略。 PackageReference 新增支援`contentFiles`更可轉移的支援和共用的內容。  |
| **潛在影響** | 中的資產`content`不會複製到專案和專案相依於這些資產是否存在的程式碼需要重構。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>在升級之後安裝套件時，不會套用 XDT 轉換

| | |
| --- | --- |
| **描述** | XDT 轉換不支援使用 PackageReference 和`.xdt`安裝或解除安裝套件時，會忽略檔案。   |
| **潛在影響** | XDT 轉換不會套用至任何專案的 XML 檔案，最常見`web.config.install.xdt`並`web.config.uninstall.xdt`，這表示專案的` web.config`安裝或解除安裝封裝時，不會更新檔案。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>在移轉之後安裝該套件時，會忽略 lib 根目錄中的組件

| | |
| --- | --- |
| **描述** | 使用 PackageReference，組件會呈現的根目錄`lib`資料夾，但特定子資料夾目標 framework 不會被忽略。 NuGet 會尋找相符的對應到專案的目標 framework 的目標 framework moniker (TFM) 的子資料夾，並會比對組件安裝至專案。 |
| **潛在影響** | 沒有相符的對應到專案的目標 framework 的目標 framework moniker (TFM) 的子資料夾的套件不能如預期轉換後或容錯移轉期間的安裝 |

## <a name="found-an-issue-report-it"></a>找出問題？ 報告它 ！

如果您遇到移轉體驗有問題時，請[NuGet GitHub 存放庫上提出問題](https://github.com/NuGet/Home/issues/)。
