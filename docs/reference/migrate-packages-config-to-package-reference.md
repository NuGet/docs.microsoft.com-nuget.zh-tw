---
title: 從 package.config 移轉至 PackageReference 格式
description: 如何將專案從 package.config 管理格式移轉至 PackageReference 為 NuGet 4.0 + 和 VS2017 和.NET 核心 2.0 所支援的詳細資訊
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 2b15d60d4f71fb2777e36c6a948ad72b4e2bc594
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>從 packages.config 移轉至 PackageReference

Visual Studio 2017 15.7年預覽第 3 版和更新版本支援的移轉專案，從[packages.config](./packages-config.md)來管理格式[PackageReference](../consume-packages/Package-References-in-Project-Files.md)格式。

## <a name="benefits-of-using-packagereference"></a>使用 PackageReference 的優點

* **管理所有的專案相依性，在一個地方**： 如同專案對專案參考和組件參考，NuGet 封裝參考 (使用`PackageReference`節點) 直接在專案檔中所管理，而不是使用不同的packages.config 檔案。
* **最上層的相依性的整齊的檢視**： 不同於 packages.config，PackageReference 列出只有您直接在專案中所安裝的 NuGet 封裝。 如此一來，NuGet 封裝管理員 UI 和專案檔不會因為雜亂下層相依性。
* **效能改進**： 當使用 PackageReference，封裝會保留在*全域封裝*資料夾 (在上所述[管理全域封裝和快取資料夾](../consume-packages/managing-the-global-packages-and-cache-folders.md)而不是在`packages`方案中的資料夾。 如此一來，PackageReference 執行的速度快，並耗用較少的磁碟空間。
* **精確控制相依性，以及內容流程**： 使用 MSBuild 的現有功能可讓您[有條件地參照 NuGet 套件](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)，然後選擇 目標 framework 中，每個封裝參考組態，平台或其他樞紐分析表。
* **PackageReference 是真的開發**： 請參閱[PackageReference 發出 GitHub 上](https://aka.ms/nuget-pr-improvements)。 packages.config 不再是真的開發。

### <a name="limitations"></a>限制

* NuGet PackageReference 不是適用於 Visual Studio 2015 及更早版本。 只有在 Visual Studio 2017，可以開啟移轉的專案。
* 移轉目前不提供對於 c + + 和 ASP.NET 專案。
* 某些封裝可能無法與 PackageReference 完全相容。 如需詳細資訊，請參閱[封裝相容性問題](#package-compatibility-issues)。

## <a name="migration-steps"></a>移轉步驟

> [!Note]
> 開始移轉之前，Visual Studio 會建立可讓您的專案備份[向前復原回 packages.config](#how-to-roll-back-to-packagesconfig)如有必要。

1. 開啟包含專案所使用的方案`packages.config`。

1. 在**方案總管 中**，以滑鼠右鍵按一下**參考**節點或`packages.config`檔案，然後選取**將 packages.config 移轉至 PackageReference...**.

1. 遷移程式會分析專案的 NuGet 封裝會參照，並嘗試對其進行分類**最上層的相依性**（NuGet 封裝，您在安裝目錄） 和**可轉移的相依性**（做為相依性的最上層封裝已安裝的封裝）。

   > [!Note]
   > PackageReference 支援可轉移的封裝還原，並解析相依性，以動態方式表示，可轉移的相依性需要不明確安裝。

1. （選擇性）您可以選擇將所選取分類為可轉移的相依性為最上層的相依性的 NuGet 封裝**最上層**封裝的選項。 包含不會轉移性地流動資產封裝的自動設定這個選項 (在`build`， `buildCrossTargeting`， `contentFiles`，或`analyzers`資料夾) 及那些標示開發相依性 (`developmentDependency = "true"`)。

1. 檢閱任何[封裝相容性問題](#package-compatibility-issues)。

1. 選取**確定**即可開始移轉。

1. 在移轉程序的結束時，Visual Studio 會提供報表路徑來備份、 已安裝的封裝 （最上層相依性） 清單，做為可轉移的相依性，參考的封裝清單和清單開頭的識別的相容性問題的移轉。 報表會儲存到備份資料夾。

1. 驗證建置並執行方案。 如果您遇到問題， [GitHub 上的檔案發生問題](https://github.com/NuGet/Home/issues/)。

## <a name="how-to-roll-back-to-packagesconfig"></a>如何回復 packages.config

1. 關閉已移轉的專案。

1. 複製專案檔和`packages.config`從備份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 到專案資料夾。

1. 開啟專案。

1. 開啟使用 Package Manager Console**工具 > NuGet 套件管理員 > Package Manager Console**功能表命令。

1. 在主控台中執行下列命令：

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>封裝相容性問題

Packages.config 中支援某些層面 PackageReference 中不支援。 遷移程式會分析，並偵測到這類問題。 有一或多個下列問題的任何封裝可能無法如預期般在移轉之後。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>在移轉之後安裝套件時，會略過"install.ps1 」 指令碼

| | |
| --- | --- |
| **描述** | 與 PackageReference，install.ps1，uninstall.ps1 PowerShell 指令碼不會安裝或解除安裝封裝時執行。 |
| **可能的影響** | 封裝相依於這些指令碼來設定目的地專案中的某些行為可能無法如預期運作。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>移轉之後安裝此套件時，不使用 「 內容 」 資產

| | |
| --- | --- |
| **描述** | 封裝中的資產`content`資料夾 PackageReference 不支援，而且會忽略。 PackageReference 新增支援`contentFiles`擁有更可轉移的支援和共用的內容。  |
| **可能的影響** | 中的資產`content`不會複製到專案和專案相依於是否存在這些資產的程式碼需要重構。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>在升級之後安裝此套件時，不會套用 XDT 轉換

| | |
| --- | --- |
| **描述** | XDT 轉換不支援 PackageReference 和`.xdt`安裝或解除安裝封裝時要忽略的檔案。   |
| **可能的影響** | XDT 轉換不會套用至任何專案 XML 檔中，大多數情況下，`web.config.install.xdt`和`web.config.uninstall.xdt`，這表示專案的` web.config`安裝或解除安裝封裝時，都未更新檔案。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>在移轉之後安裝套件時，會忽略 lib 根目錄中的組件

| | |
| --- | --- |
| **描述** | PackageReference，組件將呈現的根目錄`lib`資料夾，但目標架構特定子資料夾不會被忽略。 NuGet 會尋找對應到專案的目標 framework 的目標 framework moniker (TFM) 比對的子資料夾，並在專案中安裝符合的組件。 |
| **可能的影響** | 沒有對應至專案的目標 framework 的目標 framework moniker (TFM) 比對的子資料夾的封裝可能無法如預期般轉換之後的行為或容錯移轉期間的安裝 |

## <a name="found-an-issue-report-it"></a>找出發生問題？ 回報 ！

如果您遇到移轉體驗有問題，請請[NuGet GitHub 儲存機制上的檔案發生問題](https://github.com/NuGet/Home/issues/)。
